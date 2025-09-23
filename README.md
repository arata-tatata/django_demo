# Djangoハンズオン：発展的なメモアプリ（当日用README）

**ゴール:** 参加者全員が「ロケット画面 🚀」に到達し、最小構成のメモアプリを動かす。

---

## 目次
- [1. 進め方（当日のルール）](#1-進め方当日のルール)
- [2. Quick Start（最短到達）](#2-quick-start最短到達)
- [3. STEP 1〜6（詳細手順）](#3-step-16詳細手順)
- [4. プロジェクト構成（イメージ）](#4-プロジェクト構成イメージ)
- [5. 第4部：メモアプリ最短実装（コード付き）](#5-第4部メモアプリ最短実装コード付き)
- [6. AIプロンプト集（困ったら貼る）](#6-aiプロンプト集困ったら貼る)
- [7. 今日使うコマンドまとめ（チートシート）](#7-今日使うコマンドまとめチートシート)
- [8. よくある詰まり（Troubleshooting）](#8-よくある詰まりtroubleshooting)
- [9. ライセンス](#9-ライセンス)

---

## 1. 進め方（当日のルール）
- コマンドは **このREADMEからコピペOK**。上から**順番に**実行。
- エラーが出たら **すぐ手を挙げて！**（全員で進めます）
- 休憩や再開時は **仮想環境を再度有効化** してから続行。
- 目標は **ロケット画面** と **メモ一覧ページ** の2つ。

---

## 2. Quick Start（最短到達）
以下を実行するとロケット画面に到達します。

```bash
# Mac / Linux
python3 --version
mkdir django_demo && cd django_demo
python3 -m venv .venv
source .venv/bin/activate

# Windows
py --version
mkdir django_demo && cd django_demo
py -m venv .venv
.venv\Scripts\activate

# 共通
pip install django
django-admin startproject memoproject .
python manage.py migrate
python manage.py runserver
```

ブラウザで **http://127.0.0.1:8000/** → ロケット画面 🚀 が出ればOK！

---

## 3. STEP 1〜6（詳細手順）

### STEP 1: Pythonのインストール確認
```bash
# Mac / Linux
python3 --version
# Windows
py --version
```

### STEP 2: プロジェクト用フォルダの作成
```bash
# Mac / Linux
mkdir django_demo
cd django_demo
# Windows
mkdir django_demo
cd django_demo
```

### STEP 3: 仮想環境の作成と有効化
```bash
# Mac / Linux
python3 -m venv .venv
source .venv/bin/activate
# Windows
py -m venv .venv
.venv\Scripts\activate
```
> ✅ 行頭に `(.venv)` が表示されれば有効化成功。  
> 🔁 端末を開き直した時は、**再度有効化**してから作業を再開。

### STEP 4: Djangoのインストール
```bash
pip install django
```

### STEP 5: プロジェクトの作成（最後の `.` を忘れずに）
```bash
django-admin startproject memoproject .
```

### STEP 6: 初期設定 & サーバ起動
```bash
python manage.py migrate
python manage.py runserver
```

---

## 4. プロジェクト構成（イメージ）

```text
django_demo/
├── .venv/            # Python仮想環境（Git対象外）
│
├── memoproject/      # ① プロジェクト設定
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py   # ★ サイト全体の設定（アプリ登録など）
│   ├── urls.py       # ★ サイト全体のURLの入口（玄関）
│   └── wsgi.py
│
├── memos/            # ② メモアプリ（第4部で作成）
│   ├── __init__.py
│   ├── admin.py      # 管理画面設定
│   ├── apps.py
│   ├── migrations/   # DB設計の履歴
│   ├── models.py     # ★ データ構造（Model）
│   ├── templates/
│   │   └── memos/
│   │       └── memo_list.html
│   ├── urls.py       # ★ アプリ内URL（新規作成）
│   └── views.py      # ★ 処理（View）
│
└── manage.py         # ★ Djangoの管理ツール
```

---

## 5. 第4部：メモアプリ最短実装（コード付き）
> ゴール：トップ(`/`)に「新規作成フォーム + メモ一覧」を表示

### 5.1 アプリ作成と登録
```bash
# Mac / Linux
python3 manage.py startapp memos
# Windows
py manage.py startapp memos
```

`memoproject/settings.py` に `memos` を追加：
```python
# memoproject/settings.py
INSTALLED_APPS = [
    'django.contrib.admin','django.contrib.auth','django.contrib.contenttypes',
    'django.contrib.sessions','django.contrib.messages','django.contrib.staticfiles',
    'memos',  # 追加
]
```

### 5.2 モデル（データ構造）
```python
# memos/models.py
from django.db import models

class Memo(models.Model):
    title = models.CharField(max_length=100)
    body = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

マイグレーション：
```bash
python manage.py makemigrations
python manage.py migrate
```

（任意）管理画面で編集したい場合：
```python
# memos/admin.py
from django.contrib import admin
from .models import Memo

@admin.register(Memo)
class MemoAdmin(admin.ModelAdmin):
    list_display = ('id','title','created_at')
    search_fields = ('title','body')
```
```bash
python manage.py createsuperuser
```

### 5.3 フォーム・ビュー・URL
```python
# memos/forms.py
from django import forms
from .models import Memo

class MemoForm(forms.ModelForm):
    class Meta:
        model = Memo
        fields = ('title','body')
```

```python
# memos/views.py
from django.shortcuts import render, redirect
from .models import Memo
from .forms import MemoForm

def memo_list_create(request):
    if request.method == 'POST':
        form = MemoForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('memo_list')
    else:
        form = MemoForm()
    memos = Memo.objects.order_by('-created_at')
    return render(request, 'memos/memo_list.html', {'form': form, 'memos': memos})
```

```python
# memoproject/urls.py
from django.contrib import admin
from django.urls import path
from memos.views import memo_list_create

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', memo_list_create, name='memo_list'),
]
```

### 5.4 テンプレート
`memos/templates/memos/memo_list.html` を新規作成：
```html
<!doctype html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <title>メモ</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <style>
      body{font-family:system-ui,Segoe UI,Roboto,sans-serif;margin:40px}
      form,.memo{max-width:780px}
      input,textarea{width:100%;padding:8px;margin:6px 0;box-sizing:border-box}
      .memo{padding:12px;border:1px solid #ddd;border-radius:8px;margin:12px 0}
      .time{color:#666;font-size:12px}
      button{padding:8px 12px;cursor:pointer}
    </style>
  </head>
  <body>
    <h1>メモ</h1>

    <h2>新規作成</h2>
    <form method="post">
      {% csrf_token %}
      <label>タイトル</label>{{ form.title }}
      <label>本文</label>{{ form.body }}
      <button type="submit">保存</button>
    </form>

    <h2>一覧</h2>
    {% for m in memos %}
      <div class="memo">
        <strong>{{ m.title }}</strong>
        <div class="time">{{ m.created_at|date:"Y-m-d H:i" }}</div>
        <div>{{ m.body|linebreaksbr }}</div>
      </div>
    {% empty %}
      <p>まだメモがありません。</p>
    {% endfor %}
  </body>
</html>
```

### 5.5 動作確認
```bash
python manage.py runserver
```
ブラウザで `http://127.0.0.1:8000/` → その場でメモ作成 → 下に表示されたら成功！

---

## 6. AIプロンプト集（困ったら貼る）

**6.1 エラー原因を特定して直す（Django）**
```
あなたは熟練Djangoメンター。以下の前提で、原因仮説→確認手順→修正案→再発防止を「Step 1→」形式で提示して。
- OS: (Mac/Windows)
- Python: `python3 --version` / `py --version` の結果
- 仮想環境: 有効化済みか(Yes/No)
- 実行コマンド: （貼り付け）
- フルエラーログ: （貼り付け）
- 期待結果:
```

**6.2 コードレビュー（短く具体的に）**
```
以下のDjangoコードを、(1) セキュリティ (2) 可読性 (3) 初学者の理解 の観点で
直すべき箇所をBefore/Afterの完全コードで。各理由は1行で。
# ここにコードを貼る
```

**6.3 本日の手順をA4で要約して（配布用）**
```
「Django入門ハンズオン：今日使うコマンドと用語」をA4/1枚で。
- セクション: 仮想環境, pip, プロジェクト/アプリ, migrate/runserver
- 形式: 箇条書き + 1行説明 + 1コマンド例
```

---

## 7. 今日使うコマンドまとめ（チートシート）
```bash
# Mac / Linux
python3 --version
mkdir django_demo && cd django_demo
python3 -m venv .venv && source .venv/bin/activate

# Windows
py --version
mkdir django_demo && cd django_demo
py -m venv .venv && .venv\Scripts\activate

# 共通
pip install django
django-admin startproject memoproject .
python manage.py startapp memos
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

---

## 8. よくある詰まり（Troubleshooting）
- **`django-admin: command not found`** → 仮想環境が有効か確認し、`pip install django` を再実行。  
- **PowerShellで `.venv\Scripts\activate` が拒否される** → 管理者で  
  `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` を実行して再試行。  
- **`python` と `py` のどっち？** → Windowsは `py` 推奨、Mac/Linuxは `python3` 推奨。  
- **再開時にエラーが多発** → 端末を開き直したら **必ず仮想環境を再有効化**。

---

## 9. ライセンス
MIT









# Djangoハンズオン：発展的なメモアプリ（当日用README）

**ゴール:** 参加者全員が「ロケット画面 🚀」に到達し、最小構成のメモアプリを動かす。

---

## 目次
- [1. 進め方（当日のルール）](#1-進め方当日のルール)
- [2. Quick Start（最短到達）](#2-quick-start最短到達)
- [3. AIプロンプト集（困ったらAIに貼る）](#3-aiプロンプト集困ったらaiに貼る)
- [4. STEP 1〜6（詳細手順）](#4-step-16詳細手順)
- [5. プロジェクト構成（イメージ）](#5-プロジェクト構成イメージ)
- [6. 第4部：メモアプリ最短実装（コード+テンプレ+CSS）](#6-第4部メモアプリ最短実装コードテンプレcss)
- [7. 今日使うコマンドまとめ（チートシート）](#7-今日使うコマンドまとめチートシート)
- [8. よくある詰まり（Troubleshooting）](#8-よくある詰まりtroubleshooting)
- [9. ライセンス](#9-ライセンス)

---

## 1. 進め方（当日のルール）
- コマンドは **このREADMEからコピペOK**。上から**順番に**実行。
- エラーが出たら **すぐ手を挙げて！**（全員で進めます）
- 休憩や再開時は **仮想環境を再度有効化** してから続行。
- 目標は **ロケット画面** と **メモ一覧ページ** の2つ。
- **機密情報はGitに上げない**（`.env`などはリポジトリ外 or `.gitignore`）。

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

## 3. AIプロンプト集（困ったらAIに貼る）

### 🧑‍🏫 AIの設定部分（固定：そのままコピー）
```
あなたはDjangoハンズオンの現場コーチです。以下を読み、私の状況を素早く把握し、
「要約 → 原因仮説 → 確認手順 → 解決手順 → 再発防止」の順に、手を動かせる形で出力してください。
各ステップは“Step 1, Step 2, …”で番号を振り、実行コマンドは必ずコードブロックで示すこと。
OSコマンドは1つのコードブロックにまとめ、`# Mac/Linux` と `# Windows` のコメントで分けてください。

[どんなイベントに参加中なのか]: Django入門ハンズオン（ゴール：ロケット画面→簡易メモアプリ）
[どんな返答がいいか]: 最短で動く手順重視 / 丁寧な解説付き / リスク注意喚起あり
[どんなAI必要?（ロール指定）]: デバッガ / 講師 / 設計者 / レビュア
[ゴール]: `http://127.0.0.1:8000/`でロケット画面、またはメモ一覧表示
[制約やNG]: 破壊的操作はNG、長い理屈より手順優先
不足情報がある場合は、最初に3つ以内の確認質問を出してから、現時点のベスト手順を提案してください。
```

### 📝 参加者入力部分（ここだけ埋める）
```
[ユーザーの環境]: OS=macOS または Windows（仮想環境=有効/無効）
[相談・エラー内容]: （例：`python manage.py runserver` で起動エラー）
```

---

## 4. STEP 1〜6（詳細手順）

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
> 💡 動作確認：`python -c "import django,sys;print(django.get_version())"`（Windowsは`py -c`も可）

### STEP 5: プロジェクトの作成（最後の `.` を忘れずに）
```bash
django-admin startproject memoproject .
```

### STEP 6: 初期設定 & サーバ起動（停止方法含む）
```bash
python manage.py migrate
python manage.py runserver
```
- アクセス: **http://127.0.0.1:8000/**（ロケット画面🚀が出ればOK）
- **停止方法（フォアグラウンド実行の停止）**  
  ```bash
  # Mac / Linux（ターミナル内で）
  Ctrl + C

  # Windows（コマンドプロンプト / PowerShell）
  Ctrl + C
  ```

---

## 5. プロジェクト構成（イメージ）
```text
django_demo/
├── .venv/            # Python仮想環境（Git対象外）
│
├── memoproject/      # ① プロジェクト設定
│   ├── settings.py   # ★ サイト全体の設定（アプリ登録など）
│   ├── urls.py       # ★ サイト全体のURLの入口
│   └── ...
│
├── memos/            # ② メモアプリ（第4部で作成）
│   ├── models.py     # ★ データ構造（Model）
│   ├── views.py      # ★ 処理（View）
│   ├── urls.py       # ★ アプリ内URL
│   └── templates/
│       └── memos/
│           └── memo_list.html
│
└── manage.py         # ★ Djangoの管理ツール
```
> 🔐 **.env / 機密情報**：APIキーやシークレットは`.env`へ。Git管理から除外（`.gitignore`）。当日は説明のみ、実演は次回以降でOK。

---

## 6. 第4部：メモアプリ最短実装（コード+テンプレ+CSS）
> ゴール：トップ(`/`)に「新規作成フォーム + メモ一覧」を表示

### 6.1 アプリ作成と登録
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

### 6.2 モデル（データ構造）
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

### 6.3 フォーム・ビュー・URL
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

### 6.4 テンプレート（＋なぜこのディレクトリ構造か）
`memos/templates/memos/memo_list.html` を新規作成：
```html
{% load static %}
<!doctype html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <title>メモ</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link rel="stylesheet" href="{% static 'memos/css/memos.css' %}">
  </head>
  <body class="page">
    <h1 class="page-title">メモ</h1>

    <h2 class="section-title">新規作成</h2>
    <form method="post" class="memo-form">
      {% csrf_token %}
      <label for="title">タイトル</label>
      {{ form.title }}
      <label for="body">本文</label>
      {{ form.body }}
      <button type="submit" class="btn-save">保存</button>
    </form>

    <h2 class="section-title">一覧</h2>
    {% for m in memos %}
      <div class="memo-card">
        <strong class="memo-title">{{ m.title }}</strong>
        <div class="time">{{ m.created_at|date:"Y-m-d H:i" }}</div>
        <div class="memo-body">{{ m.body|linebreaksbr }}</div>
      </div>
    {% empty %}
      <p class="empty">まだメモがありません。</p>
    {% endfor %}
  </body>
</html>
```

**なぜ `templates/memos/...` の2段構造？（要点）**  
- 同名テンプレートの**衝突回避**（アプリ間で同じ`index.html`等があっても安全）  
- **再利用性**が上がる（部分テンプレや他アプリに持ち運びやすい）  
- Djangoの既定（`<app_label>/<model>_list.html`）に**自然に沿う**  

### 6.5 CSS（静的ファイルの超基礎）
```bash
# Mac / Linux
mkdir -p memos/static/memos/css

# Windows
mkdir memos\static\memos\css
```

`memos/static/memos/css/memos.css` を作成：
```css
body{font-family:system-ui,Segoe UI,Roboto,sans-serif;margin:40px}
.page-title{font-size:28px;margin-bottom:8px}
.section-title{font-size:18px;margin:22px 0 6px}
.memo-form input,.memo-form textarea{width:100%;padding:8px;margin:6px 0;box-sizing:border-box}
.memo-card{padding:12px;border:1px solid #ddd;border-radius:8px;margin:12px 0}
.memo-title{font-weight:600}
.time{color:#666;font-size:12px}
.btn-save{padding:8px 12px;cursor:pointer}
```

> 開発中は`runserver`が自動で`static/`を配信。  
> 本番は`STATIC_ROOT`と`collectstatic`、Webサーバ（例：Nginx）で配信するのが基本。

**（参考設定：本番時）**
```python
# memoproject/settings.py
STATIC_URL = 'static/'
# 本番で使うとき
# STATIC_ROOT = BASE_DIR / 'staticfiles'
```
```bash
# 本番でのアセット集約
python manage.py collectstatic
```

### 6.6 動作確認
```bash
python manage.py runserver
```
ブラウザで `http://127.0.0.1:8000/` → その場でメモ作成 → 下に表示されたら成功！

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
- **PowerShellで `.venv\Scripts\activate` が拒否** → 管理者で  
  `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` を実行。  
- **`python` と `py` のどっち？** → Windowsは `py` 推奨、Mac/Linuxは `python3` 推奨。  
- **再開時にエラー多発** → 端末を開き直したら **必ず仮想環境を再有効化**。  
- **静的ファイルが反映されない** → テンプレ頭で`{% load static %}`、パスは`memos/...`で合わせる。

---

## 9. ライセンス
MIT


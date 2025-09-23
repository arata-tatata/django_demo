# Djangoハンズオン：発展的なメモアプリ（当日用README）

**ゴール:** 参加者全員が「ロケット画面 🚀」に到達し、最小構成のメモアプリを動かす。

---

## 目次
- [1. 進め方（当日のルール）](#1-進め方当日のルール)
- [2. Quick Start（最短到達）](#2-quick-start最短到達)
- [3. AIプロンプト集（困ったらAIに貼る）](#3-aiプロンプト集困ったらaiに貼る)
- [4. STEP 1〜6（詳細手順）](#4-step-16詳細手順)
- [5. プロジェクト構成（イメージ）](#5-プロジェクト構成イメージ)
- [6. 第4部：メモアプリ最短実装（コード付き）](#6-第4部メモアプリ最短実装コード付き)
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
[ユーザーの環境]: OS=macOS, 仮想環境=有効/無効
[相談・エラー内容]: （例：`python manage.py runserver` でエラーが出る）
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

## 5. プロジェクト構成（イメージ）

```text
django_demo/
├── .venv/            
├── memoproject/      
│   ├── settings.py   # ★ サイト全体の設定
│   ├── urls.py       # ★ サイト全体のURL
│   └── ...
├── memos/            # ② メモアプリ（第4部で作成）
│   ├── models.py     # ★ データ構造（Model）
│   ├── templates/    
│   │   └── memos/
│   │       └── memo_list.html
│   ├── urls.py       # ★ アプリ内URL
│   └── views.py      # ★ 処理（View）
└── manage.py         # ★ 管理ツール
```

---

## 6. 第4部：メモアプリ最短実装（コード付き）
（※ここは既存の手順そのまま。割愛）

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

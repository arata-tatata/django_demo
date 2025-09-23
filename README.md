# Djangoハンズオン：発展的なメモアプリ

このリポジトリは、Djangoハンズオンで作成するメモアプリの完成形コードと、ハンズオンの手順をまとめた資料です。

---

## 1. このアプリについて

ユーザー登録・ログイン機能を備えた、カテゴリ分けができるメモアプリケーションです。  
このハンズオンを通じて、Djangoの基本的なMVT構造、アプリ分割の考え方、ユーザー認証の基礎を学びます。

---

## 2. 環境構築（コマンドは **1行ずつ** コピーして実行してください）

各ステップに **Mac/Linux** と **Windows** の手順があります。自分のOSを開いて進めてください。

### Step 0: Python のインストール確認

<details>
<summary><b>Mac / Linux</b></summary>

Python のバージョン確認（3.10+ を推奨）
```bash
python3 --version
必要なら Homebrew で Python を導入（任意）

bash
コードをコピーする
brew install python
</details> <details> <summary><b>Windows</b></summary>
Python ランチャーのバージョン確認

powershell
コードをコピーする
py --version
Python コマンドのバージョン確認（環境によっては py ではなく python を使います）

powershell
コードをコピーする
python --version
</details>
Step 1: 作業用フォルダの作成と移動
<details> <summary><b>Mac / Linux</b></summary>
フォルダ作成

bash
コードをコピーする
mkdir memoproject
移動

bash
コードをコピーする
cd memoproject
</details> <details> <summary><b>Windows</b></summary>
フォルダ作成

powershell
コードをコピーする
mkdir memoproject
移動

powershell
コードをコピーする
cd memoproject
</details>
Step 2: 仮想環境の作成
<details> <summary><b>Mac / Linux</b></summary>
仮想環境を .venv に作成

bash
コードをコピーする
python3 -m venv .venv
</details> <details> <summary><b>Windows</b></summary>
仮想環境を .venv に作成（ランチャー使用）

powershell
コードをコピーする
py -m venv .venv
ランチャーが無い場合

powershell
コードをコピーする
python -m venv .venv
</details>
Step 3: 仮想環境の有効化
<details> <summary><b>Mac / Linux</b></summary>
アクティベート

bash
コードをコピーする
source .venv/bin/activate
</details> <details> <summary><b>Windows</b></summary>
PowerShell でアクティベート

powershell
コードをコピーする
.venv\Scripts\activate
</details>
✅ 行頭に (.venv) と表示されればOK。
⚠️ PowerShellの実行ポリシーでエラーが出る場合は管理者で次を実行 → Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

Step 4: Django のインストール（OS共通）
最新版をインストール

bash
コードをコピーする
pip install django
（バージョン固定にしたい場合の例）

bash
コードをコピーする
pip install "django>=5,<6"
Step 5: Django プロジェクトの作成（OS共通）
カレントディレクトリ直下にプロジェクトを作成（最後の . を忘れない）

bash
コードをコピーする
django-admin startproject memoproject .
Step 6: アプリの作成（OS共通）
メモ機能

bash
コードをコピーする
python manage.py startapp memos
ユーザー管理

bash
コードをコピーする
python manage.py startapp accounts
Step 7: 開発サーバ起動の動作確認（OS共通）
初期マイグレーション

bash
コードをコピーする
python manage.py migrate
サーバ起動

bash
コードをコピーする
python manage.py runserver
ブラウザで http://127.0.0.1:8000/ を開き、Django のロケット画面が出れば成功です。

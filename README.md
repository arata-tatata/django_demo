# Djangoハンズオン：発展的なメモアプリ

このリポジトリは、Djangoハンズオンで作成するメモアプリの完成形コードと、ハンズオンの手順をまとめた資料です。

---

## 1. このアプリについて

ユーザー登録・ログイン機能を備えた、カテゴリ分けができるメモアプリケーションです。  
このハンズオンを通じて、Djangoの基本的なMVT構造、アプリ分割の考え方、ユーザー認証の基礎を学びます。

---

## 2. 環境構築

このハンズオンを始めるための環境構築を行います。  
「ターミナル」（Mac）または「コマンドプロンプト / PowerShell」（Windows）を開いて、以下のコマンドを順にコピー＆ペーストしてください。

---

### Step 0: Pythonのインストール確認

```bash
# Mac / Linux
python3 --version

# Windows
py --version
Step 1: プロジェクト用フォルダの作成と移動
bash
コードをコピーする
# Mac / Linux
mkdir memoproject
cd memoproject

# Windows
mkdir memoproject
cd memoproject
Step 2: Python仮想環境の作成
bash
コードをコピーする
# Mac / Linux
python3 -m venv .venv

# Windows
py -m venv .venv
# または
python -m venv .venv
Step 3: 仮想環境の有効化
bash
コードをコピーする
# Mac / Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
✅ 成功のサイン: コマンド実行後、行頭に (.venv) が表示されればOK！

Step 4: Djangoのインストール
bash
コードをコピーする
pip install django
Step 5: Djangoプロジェクトの作成
bash
コードをコピーする
django-admin startproject memoproject .
⚠️ 注意: 最後の .（ピリオド）を忘れないこと！

Step 6: Djangoアプリケーションの作成
bash
コードをコピーする
# メモ機能用アプリ
python manage.py startapp memos

# ユーザー管理機能用アプリ
python manage.py startapp accounts
🎉 お疲れ様でした！
これで開発を始めるための全ての準備が整いました。

yaml
コードをコピーする

---

これならREADMEにそのまま貼り付けできるし、コピーも一括でできます。  

👉 質問：  
このREADMEは **初学者向けに（解説多め）** でいいですか？  
それとも **イベント用に（コマンド中心でシンプル）** にしますか？

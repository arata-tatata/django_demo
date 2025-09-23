環境構築
このハンズオンを始めるための環境構築を行います。
手元のPCで「ターミナル」（Mac）または「コマンドプロンプト」か「PowerShell」（Windows）を開いて、以下のコマンドを1行ずつコピー＆ペーストして実行してください。
Step 1: プロジェクト用フォルダの作成と移動
まず、今回の作業をすべて格納する専用のフォルダを作成し、その中に移動します。
Mac / Linux の場合
code
Bash
# 「memoproject」という名前のフォルダを作成します
mkdir memoproject

# 作成した「memoproject」フォルダの中に移動します
cd memoproject
Windows の場合
code
Powershell
# 「memoproject」という名前のフォルダを作成します
mkdir memoproject

# 作成した「memoproject」フォルダの中に移動します
cd memoproject
Step 2: Python仮想環境の作成
次に、このプロジェクト専用のクリーンなPython環境（砂場）を作成します。.venvという名前の仮想環境フォルダが作られます。
Mac / Linux の場合
code
Bash
python3 -m venv .venv
Windows の場合
code
Powershell
# pythonランチャーがインストールされている場合
py -m venv .venv

# または、直接pythonを指定する場合
python -m venv .venv
Step 3: 仮想環境の有効化
作成した仮想環境（砂場）の中に入ります。このコマンドを実行すると、ターミナルの見た目が少し変わります。
Mac / Linux の場合
code
Bash
source .venv/bin/activate
Windows の場合
code
Powershell
.venv\Scripts\activate```

**✅ 成功のサイン:** コマンドを実行した後、行の先頭に `(.venv)` という表示が出れば成功です！

---

### Step 4: Djangoのインストール

いよいよDjango本体を、今いる仮想環境の中にインストールします。このコマンドはOS共通です。

```bash
pip install django
Step 5: Djangoプロジェクトの作成
Djangoのコマンドを使って、Webサイト全体の設計図となるファイル群を自動生成します。
⚠️ 注意： 最後の . (ピリオド) を絶対に忘れないでください！
code
Bash
# このコマンドはOS共通です
django-admin startproject memoproject .
Step 6: Djangoアプリケーションの作成
最後に、このプロジェクトの主要な機能となる「メモ機能(memos)」と「ユーザー管理機能(accounts)」の2つのアプリの骨組みを作成します。
code
Bash
# このコマンドはOS共通です

# ① メモ機能用のmemosアプリを作成
python3 manage.py startapp memos

# ② ユーザー管理機能用のaccountsアプリを作成
python3 manage.py startapp accounts
お疲れ様でした！これで開発を始めるための全ての準備が整いました。

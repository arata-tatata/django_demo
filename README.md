# Django環境構築：簡単なメモアプリ作成

このリポジトリは、Djangoハンズオンで作成するメモアプリの完成形コードと、環境構築の手順をまとめた資料です。  
**ゴール:** 全員が「ロケット画面 🚀」にたどり着くこと！

---

## 1. ハンズオンの進め方

- コマンドは **READMEやスライドからコピペOK！**
- エラーが出たら **すぐ手を挙げて！**（みんなで一緒に進めます）
- 少しずつ確実に。ゴールは「ロケット画面」！

---

## 2. STEP 1〜6

### STEP 1: Pythonのインストール確認

#### Mac / Linux
```bash
python3 --version
```
#### Windows
```powershell
py --version
```
### STEP 2: プロジェクト用フォルダの作成
これから作る全ファイルをまとめるルートフォルダ django_demo を作り、その中へ移動します。

#### Mac / Linux
```bash
mkdir django_demo
```
```bash
cd django_demo
```
#### Windows
```powershell
mkdir django_demo
```
```powershell
cd django_demo
```
### STEP 3: 仮想環境の作成と有効化

#### Mac / Linux
```bash
python3 -m venv .venv
```
```bash
source .venv/bin/activate
```
#### Windows
```powershell
py -m venv .venv
```
```powershell
.venv\Scripts\activate
```
✅ 成功のサイン: 行頭に (.venv) が表示されればOK！

### STEP 4: Djangoのインストール
#### 共通
```bash
pip install django
```
### STEP 5: プロジェクトの作成
Djangoの設計図「プロジェクト」を作成します。
名前は memoproject にし、最後の .（ピリオド）を忘れないでください！
#### 共通
```bash
django-admin startproject memoproject .
```
ここでできあがったもの
```text
django_demo/
├── .venv/
├── memoproject/   <-- これができた！
└── manage.py      <-- これもできた！
```
### STEP 6: 初期設定 & サーバ起動
#### 共通
```bash
python manage.py migrate
```
```bash
python manage.py runserver
```
ブラウザで http://127.0.0.1:8000/ にアクセスし、ロケット画面 🚀 が表示されれば成功です！







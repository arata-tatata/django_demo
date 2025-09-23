# Djangoハンズオン：発展的なメモアプリ

このリポジトリは、Djangoハンズオンで作成するメモアプリの完成形コードと、ハンズオンの手順をまとめた資料です。

## 1. このアプリについて

ユーザー登録・ログイン機能を備えた、カテゴリ分けができるメモアプリケーションです。
このハンズオンを通じて、Djangoの基本的なMVT構造、アプリ分割の考え方、ユーザー認証の基礎を学びます。

## 2. 環境構築

ハンズオンを進めるための環境構築コマンド一覧です。

```bash
# プロジェクトフォルダ作成
mkdir memoproject
cd memoproject

# 仮想環境の作成と有効化
python3 -m venv .venv
source .venv/bin/activate  # Mac/Linuxの場合

# Djangoのインストール
pip install django

# プロジェクトとアプリの作成
django-admin startproject memoproject .
python3 manage.py startapp memos
python3 manage.py startapp accounts

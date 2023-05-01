# Next.js × Laravel の環境構築

https://twitter.com/risingmigisan/status/1480069973687291908?lang=ja

## 前提

- M1Mac 対応
- Intel 製チップ Mac の場合は`.docker/db/Dockerfile`を以下の通り修正
- Windows での動作確認は行っていない

```diff
- FROM --platform=linux/x86_64 mysql:8.0
+ FROM mysql:8.0

ENV TZ=UTC

COPY my.cnf /etc/my.cnf
```

## コンテナ起動

```sh
docker-compose up -d --build
```

## Laravel インストール

```sh
docker-compose exec api composer create-project laravel/laravel .
```

`api`ディレクトリ内に Laravel がインストールされる

`localhost:80`にアクセスすると Laravel のウェルカムページが表示される

## Next.js インストール

```sh
docker-compose exec front yarn create next-app  --typescript .

# 開発用サーバー起動
docker-compose exec front yarn dev
```

`front`ディレクトリ内に Next.js がインストールされる

`localhost:3000`にアクセスすると Next.js のウェルカムページが表示される

開発用サーバーの停止は`control + c`

# Laravel で React フレームワークの Next.js 使う方法

https://www.webopixel.net/php/1724.html

# DB接続

dc exec db bash

mysql -u root -ppassword

# migration

https://www.ritolab.com/posts/25

https://qiita.com/mdrq/items/f10e488caa4497eec79b

# 新規作成
dc exec api php artisan make:migration create_users_table --create=users

# 編集（編集内容がわかりやすいファイル名にすると◎）

dc exec api php artisan make:migration modify_users_table --table=users

# マイグレーション実行

dc exec api php artisan migrate

# ロールバック

一番最後に実行したマイグレーションが無かったことになる

php artisan migrate:rollback

マイグレーションを３世代前にロールバックする

php artisan migrate:rollback --step=3

全てのマイグレーションをロールバックする

php artisan migrate:reset

全てのマイグレーションをロールバックし、再度マイグレーションを実行する

php artisan migrate:refresh


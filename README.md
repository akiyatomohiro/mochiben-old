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

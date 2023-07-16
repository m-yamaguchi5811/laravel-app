# laravel-app
このリポジトリにはLaravelの初期設定済みのソースが置いてあります。<br>Laravelでサービスを開始する際にクローンしてお使いください。

## 構成・バージョン
- Laravel Framework 10.15.0
- MySQL 8.0.32
- Redis 7.0.12
- Vue.js 3.3.4
- Mailpit

### 1．クローンする
```
git clone https://github.com/m-yamaguchi5811/laravel-app.git
```
### 2．envファイルを準備する
「.env.development」を「.env」に変更する

### 3．アプリのサービス名に変更する
以下のファイルの「laravel-app」の部分をサービス名に修正する。<br>
（修正しなくて使用できますので、取り敢えず動かしたい場合はそのままで大丈夫です。）
#### docker-compose.yml
```
4行目
laravel-app:
```

#### .env
```
7行目
APP_SERVICE="laravel-app"
```

### 5．パッケージをインストール
```
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php82-composer:latest \
    composer install --ignore-platform-reqs
```

### 6．Sailコマンドの設定
以下のコマンドを実行してSailコマンドを使いやすくする。
```
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
```

### 7．Sailコマンドでコンテナを起動する
```
sail up -d
```

### 8．ブラウザで確認する
以下のURLにアクセスする。<br>
http://localhost/
<br>
<br>

## 補足
### ■Sailコマンド
#### コンテナ作成・起動
```
sail up
```
#### コンテナ作成・起動（バックグラウンド）
正常に動いている場合こちらをおすすめします。
```
sail up -d
```
#### コンテナ停止
```
sail stop
```
#### コンテナ一覧（起動しているコンテナのみ）
```
sail ps
```
#### アプリのコンテナに接続
```
sail shell
```
#### MySQLに接続
```
sail mysql
```
#### Redisに接続
```
sail redis
```
#### artisanコマンド
`sail artisan` のみ実行すると、<b>help</b> が表示されます。
```
sail artisan [command]
```
#### PHPUnit実行
```
sail test
```
#### Composer
```
sail composer []
```

### ■npmコマンド(vueを使用するとき)
開発環境
```
sail exec [アプリのコンテナ名] npm run dev
```
本番環境（ビルド）
```
sail exec [アプリのコンテナ名] npm run build
```
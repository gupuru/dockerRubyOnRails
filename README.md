# dockerRubyOnRails


## 1. これ実行

```
docker-compose run web rails new . --force --database=mysql --skip-bundle
```

## 2. Gemfileのtherubyracer gemのコメントを外す

```
gem 'therubyracer', platforms: :ruby
```

## 3. build

```
docker-compose build
```

## 4. config/database.yml 内のhostに```db```を指定

```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  password:
  host: db
```

## 5. データベース作成

```
 docker-compose run web rake db:create
```

## 6. ipアドレス確認

```
docker-machine ip default
```

## 7. server立ち上げる

```
docker-compose up
```

終了はCtrl + c

## 8. 確認

```
さっき調べたipアドレス:3000
``` 

# Hello Worldを作る

## 1. Rails起動

```
docker-compose up -d
```

## 2. コンテナ確認

コンテナ一覧表示

```
docker ps
```

こんな感じで表示される

```
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                    NAMES
a496312af42d        dockerrubyonrails_web   "bundle exec rails s "   5 hours ago         Up 20 minutes       0.0.0.0:3000->3000/tcp   dockerrubyonrails_web_1
6852f4fa3794        mysql:5.6               "docker-entrypoint.sh"   5 hours ago         Up 20 minutes       3306/tcp                 dockerrubyonrails_db_1
```

ここでrailsのコンテナのNAMESをコピー

## 3. コンテナに入る


```
docker exec -it コンテナのNAMES bash
```


## 4. generateする

これ実行

```
rails generate controller welcome index
```

Ctrl + P + Qでコンテナからでる。

## 5. ファイルができているか確認

app/controllers/welcome_controller.rb
config/routes.rb

routes.rbにあるパス確認

```
  get 'welcome/index'
```

## 6. Hello Worldが表示されているのを確認

```
dockerのipアドレス:3000/welcome/index
```

## 7. コンテナ終了

```
docker-compose stop
```

## 8. rails頑張ろう！！

とりあえず、ここ見ながら、やればいいよー

http://railsguides.jp/getting_started.html

## 補足

基本的にrailsのコマンドはコンテナの中に入って実行ー

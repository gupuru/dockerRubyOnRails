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

# is07_mayo_rails_docker
DockerでRails環境を作る

## 作業ログ

### ignore修正編

```
$ git checkout -b fix-gitignore
$ git commit --allow-empty -m "ignoreの内容を修正"
$ git git add .gitignore
## ------------------------- Commit ID : 927fb7f ##
$ git commit -m "gitignoreを修正"

######## PR作成マージ ########
```

### Rails_Docker作成

```
# masterブランチの最新化とローカルブランチの削除
$ git checkout master
$ git pull
$ git branch -D fix-gitignore

# Rails環境を作成
$ git checkout -b add-rails_docker
$ git commit --allow-empty -m "ignoreの内容を修正"

# Railsアプリケーションを作成する作業
$ git add .
$ git commit -m "Rails一式を追加"
## ------------------------- Commit ID : 4df0288 ##
$ git push origin add-rails_docker

######## PR作成マージ ########
```

### Rails Application作成

```
# masterブランチの最新化とローカルブランチの削除
$ git checkout master
$ git pull
$ git branch -D add-rails_docker

## Dockerを実際に動かしてrails appを作成する
$ cp env.example .env
$ docker-compose run --rm app rails new . --force --database=mysql --skip-bundle
$ sudo chown -R $USER:$USER .
$ git add .
$ git commit -m "Create Rails APP"
## ------------------------- Commit ID : 451dee1 ##

$ docker-compose build

## DB変更をする
$ git add config/database.yml
$ git commit -m "databaseの設定をdockerに合わせる"

## 動作確認とコンテナ起動
$ docker-compose up -d

## mysqlの設定したuserに権限を与える
$ docker exec -it is_mysql bash
# mysql -uroot -p
mysql > GRANT ALL PRIVILEGES ON *.* TO 'ENVに書いたMYSQL_USER'@'%';
mysql > FLUSH PRIVILEGES;
mysql > exit;
# exit

## DBの作成とmigrationをする
$ docker-compose run --rm app rails db:create db:migrate

## アクセスして確認してみる

## 残りの差分をコミット
$ git add .
$ git commit -m "差分commit"

$ git push origin head

######## PR作成マージ ########
```

課題5 - Herokuアプリケーションを使ってみる
==========================================

Heroku Connect を使った課題。

### 使い方

```
$ heroku create <app-name>
$ heroku push origin master
$ heroku open
```

Heroku Connect の設定を終えた後、`https://<app-name>.herokuapp.com/accounts` を開く。

### メモ

最初にローカル環境で動かしたとき、冒頭の

```python
url = urlparse.urlparse(os.environ.get('DATABASE_URL'))
db = "dbname=%s user=%s password=%s host=%s " % (url.path[1:], url.username, url.password, url.hostname)
schema = "schema.sql"
conn = psycopg2.connect(db)
cur = conn.cursor()
```

エラーになった。
これは以前、
[[Python]HerokuでDjangoアプリケーション開発を始めるためのテンプレート - dackdive's blog](http://dackdive.hateblo.jp/entry/2015/12/22/110707)
で `DATABASE_URL` とかいじってたのがいけなかったっぽい。

またその解決方法としては、[Show Contacts Locally](http://clouddatafacts.com/heroku-connect/flask_psycopg2/flask_psycopg2_prebuilt_get.html#show-contacts-locally) にあるように
本番環境の `DATABASE_URL` を取得して export してあげればよかった。

```
$ heroku config
=== zakiyama-swtt16-minihacks Config Vars
DATABASE_URL: postgres://xtrhccebofdnoi:edf4cce...@<ip address>.compute-1.amazonaws.com:5432/d6vguddji3uu4g
```

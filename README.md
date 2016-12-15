課題5 - Herokuアプリケーションを使ってみる
==========================================

[Salesforce World Tour Tokyo 2016 の Minihacks](https://developer.salesforce.com/ja/worldtour2016/minihacks) の課題のうち、
「課題5 - Herokuアプリケーションを使ってみる」の解答例です。

その他の課題については https://github.com/zaki-yama/swtt2016-minihacks を参照。

Heroku Connect を使った課題。

### 使い方

```zsh
$ heroku create <app-name>
$ heroku push origin master
$ heroku open

# アドオン追加
$ heroku addons:create heroku-postgresql:hobby-dev
$ heroku addons:create herokuconnect
# Heroku Connect の管理画面を開く
$  heroku addons:open herokuconnect
```


Heroku Connect の設定を終えた後、`https://<app-name>.herokuapp.com/accounts` を開く。

また、ローカルで動かす場合は Python と virtualenv をインストールした後

```zsh
$ virtualenv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
$ heroku local web
```

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

```
21:12:27 web.1   |  OperationalError: could not translate host name "None" to address: nodename nor servname provided, or not known
```

その解決方法としては、参考リンク後半の [Show Contacts Locally](http://clouddatafacts.com/heroku-connect/flask_psycopg2/flask_psycopg2_prebuilt_get.html#show-contacts-locally) にあるように
本番環境の `DATABASE_URL` を取得して export してあげればよかった。

```
$ heroku config
=== zakiyama-swtt16-minihacks Config Vars
DATABASE_URL: postgres://xtrhccebofdnoi:edf4cce...@<ip address>.compute-1.amazonaws.com:5432/d6vguddji3uu4g

$ export DATABASE_URL=postgres://xtrhccebofdnoi:edf4cce...@<ip address>.compute-1.amazonaws.com:5432/d6vguddji3uu4g
```

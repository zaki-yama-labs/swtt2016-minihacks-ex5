課題5 - Herokuアプリケーションを使ってみる
==========================================

### メモ

冒頭の

```python
url = urlparse.urlparse(os.environ.get('DATABASE_URL'))
db = "dbname=%s user=%s password=%s host=%s " % (url.path[1:], url.username, url.password, url.hostname)
schema = "schema.sql"
conn = psycopg2.connect(db)
cur = conn.cursor()
```

でさっそくエラー。おそらく
[[Python]HerokuでDjangoアプリケーション開発を始めるためのテンプレート - dackdive's blog](http://dackdive.hateblo.jp/entry/2015/12/22/110707)
で `DATABASE_URL` とかいじってたのがいけなかったっぽい。

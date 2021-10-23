---
title: django学習（1）
categories: 一般
author: 'ゆぴ'
tags:
- ja
- archlinux
- 学習
- python
- django
- シリーズ
excerpt: Djangoをゆぴと共に学習してみませんか?
date: 2020-12-05 
cover: '/image/cover/studydjango.webp'
---

## まずはじめに

この記事は私がdjangoをある程度使えるようになるまで続ける予定です。そしてこの記事を書いている私はまったく持っての初心者なのでそこのところご了承ください。

### プロジェクトを作る
{% codeblock %}
alert('Hello World!');
{% endcodeblock %}
```cmd
django-admin startproject プロジェクト名

（例） django-admin startproject dashboard
```

### 起動してみる

とりあえず、弄る前に起動してみます

```cmd
python manage.py runserver
```

恐らく、8000番ポートが使用されていなければ http://localhost:8000 で接続が可能だと想います。
ちなみにこれは開発サーバーなので、runserverで起動している間に編集した場合は自動でリロードが行われます。便利ですね。

### アプリケーションを作る

さて、最初に作成したdashboardフォルダーの中に入り以下のコマンドを実行してください。

```cmd
python manage.py startapp todo
```

これで、dashboardフォルダーの中にtodoというフォルダーが生成されたと想います。
ちなみに、公式ドキュメントにはプロジェクトとアプリケーションの違いが以下のように記載されています。

> プロジェクトとアプリの違いは何でしょうか？ アプリとは、ウェブログシステム、公的記録のデータベース、小規模な投票アプリなど、何かを行う Web アプリケーションです。プロジェクトは、特定のウェブサイトの構成とアプリのコレクションです。プロジェクトには複数のアプリを含めることができます。 アプリは複数のプロジェクトに存在できます。

### ビューを作ってみる

ビューは主にDjangoで描画などを行う際に使用されるファイルです。

#### todo/views.py

```python
from django.http import HttpResponse

def index(request):
  return HttpResponse("ハロー！")
```

さて、これで表示するものはできました。次にリンクがありませんよね、これじゃあどうやって接続すればいいのかわかりません。
そこで出てくるのがurls.pyです。基本的に`/`に接続があったら〇〇のviewsに飛ばすなどと言ったことができるファイルだと考えておけば問題ありません。

!!! info tip
    アプリケーション（todo）の方にはurls.pyは存在しないため、自分で作成してください。

#### todo/urls.py

```python
from django.urls import path

from . import views

urlpatterns = [
  path('', views.index, name='index')
]
```

#### dashboard/urls.py

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
  path('todo/', include('todo.urls')),
  path('admin/', admin.site.urls),
]
```

さて、いっきによくわからないものが出てきました。。。まず、`dashboard/urls.py`の方から準に見ていきましょう。
このファイルでは、`http://localhost:8000/todo`などで接続したユーザーの処理をtodoアプリのurls.pyに渡しています。
`include`はアクセスした時点が`http://localhost:8000/todo`だった場合、`/todo`の部分のみをtodoアプリのurls.pyに渡すような感じです。

そうしたら、`http://localhost:8000/todo`に接続してみましょう。`ハロー！`と出たなら成功です！

## 参考

https://docs.djangoproject.com/ja/3.1/intro/tutorial01/

## 最後に

最後まで読んでいただき感謝感激です。この記事は現状参考とほぼ同じことになっていますが、今後もっと多くのことに挑戦していくつもりです。
次回はデータベースに接続し、実際にデータの追加、削除を行ってみようと想います。


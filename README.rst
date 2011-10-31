==================
django-staticfiles
==================

.. warning:: このドキュメントは `django-staticfiles <http://readthedocs.org/docs/django-staticfiles/>`_ の翻訳です。

.. This is a Django app that provides helpers for serving static files.

これは静的ファイルを配信するためのヘルパーを提供するDjangoアプリケーションです。

.. Django developers mostly concern themselves with the dynamic parts of web
   applications -- the views and templates that render new for each request. But
   web applications have other parts: the static media files (images, CSS,
   Javascript, etc.) that are needed to render a complete web page.

ほとんどのDjango開発者は、ウェブアプリケーションにはリクエスト毎に新しくビューやテンプレートをレンダリングする動的な部分があって、それ以外にも、一つのウェブページの全て表示するためには画像、CSS、JavaScriptなどの静的なメディアファイルを扱う部分もあるということも考慮しなければいけません。

.. For small projects, this isn't a big deal, because you can just keep the media
   somewhere your web server can find it. However, in bigger projects -- especially
   those comprised of multiple apps -- dealing with the multiple sets of static
   files provided by each application starts to get tricky.

小さなプロジェクトでは、これは重要なことではない。なぜなら、Webサーバがメディアファイルの置いている場所を見つけることができるように置いておくだけだからです。しかしより大きなプロジェクト(特に複数のアプリケーションで構成される場合)では、個々のアプリケーションが複数の静的ファイルをまとめて使うと複雑になってきます。

.. That's what ``staticfiles`` is for:

静的ファイルとは何を指しているのでしょう？ :

  .. Collecting static files from each of your Django apps (and any other
     place you specify) into a single location that can easily be served in
     production.

  Djangoアプリケーションの個々の静的ファイルを一つの場所(他に指定した任意の場所)に集めることは本番環境で静的ファイルを配信することが容易になります。

.. The main website for django-staticfiles is
   `github.com/jezdez/django-staticfiles`_ where you can also file tickets.

django-staticfilesのメインのウェブサイトは `github.com/jezdez/django-staticfiles`_ で、チケットを作成することもできます。

.. note::

   .. django-staticfiles is now part of Django (since 1.3) as ``django.contrib.staticfiles``.

      The django-staticfiles 0.3.X series will only receive security and data los
      bug fixes after the release of django-staticfiles 1.0. Any Django 1.2.X
      project using django-staticfiles 0.3.X and lower should be upgraded to use
      either Django >= 1.3's staticfiles app or django-staticfiles >= 1.0 to
      profit from the new features and stability.

      You may want to chose to use django-staticfiles instead of Django's own
      staticfiles app since any new feature (additionally to those backported
      from Django) will be released first in django-staticfiles.

   django-staticfilesはDjango 1.3から ``django.contrib.staticfiles`` としてDjangoの一部になりました。

   django-staticfilesの0.3.Xは1.0のリリース後はセキュリティとデータがなくなるバグのバグフィックスしか行いません。
   Django 1.2.X で 0.3.X 以下のバージョンを使っている場合は、django-staticfilesのバージョン1.0以上を使うかDjango 1.3のstaticfilesにアップグレードしてください。

   django-staticfilesで先に新しい機能がリリースされるので、django-staticfilesを使いたい場合は、Django付属のstaticfilesアプリケーションの代わりにdjango-staticfilesを使うことができます。

.. Installation
   ------------

インストール
---------------------

.. Use your favorite Python packaging tool to install ``staticfiles``
   from `PyPI`_, e.g.::

- `PyPI`_ から ``staticfiles`` をインストールするための好きなPythonのパッケージツールが使えます。例として ::

    pip install django-staticfiles

  .. You can also install the `in-development version`_ of django-staticfiles
     with ``pip install django-staticfiles==dev``.

  ``pip install django-staticfiles==dev`` とすると、django-staticfilesの `in-development version`_ をインストールすることができます。

.. Added ``"staticfiles"`` to your ``INSTALLED_APPS`` setting::

- ``INSTALLED_APPS`` に ``"staticfiles"`` を追加して下さい。 ::

    INSTALLED_APPS = [
        # ...
        "staticfiles",
    ]

.. Set your ``STATIC_URL`` setting to the URL that handles serving
   static files::

- ``STATIC_URL`` に静的ファイルを配信させたいURLを設定して下さい。 ::

    STATIC_URL = "/static/"

.. In development mode (when ``DEBUG = True``) the ``runserver`` command will
   automatically serve static files::

- 開発モード(``DEBUG = True`` の時)の時に、 ``runserver`` コマンドで静的ファイルを自動的に配信します。

    python manage.py runserver

.. Once you are ready to deploy all static files of your site in a central
   directory (``STATIC_ROOT``) to be served by a real webserver (e.g. Apache_,
   Cherokee_, Lighttpd_, Nginx_ etc.), use the ``collectstatic`` management
   command::

- サイトの全ての静的ファイルをデプロイする準備ができたら、 ``collectstatic`` 管理コマンドを使って下さい。 ::

    python manage.py collectstatic

  .. See the webserver's documentation for descriptions how to setup serving
     the deployment directory (``STATIC_ROOT``).

  デプロイするディレクトリ(``STATIC_ROOT``)に配信するための設定方法は、ウェブサーバーのドキュメントを見てください。

.. (optional) In case you use Django's admin app, make sure the
   ``ADMIN_MEDIA_PREFIX`` setting is set correctly to a subpath of
   ``STATIC_URL``::

- (オプション) Djangoのadminアプリケーションを使う場合は、 ``ADMIN_MEDIA_PREFIX`` の設定を ``STATIC_URL`` のサブパスに正しく設定して下さい。 ::

     ADMIN_MEDIA_PREFIX = STATIC_URL + "admin/"

.. _github.com/jezdez/django-staticfiles: http://github.com/jezdez/django-staticfiles
.. _in-development version: http://github.com/jezdez/django-staticfiles/tarball/develop#egg=django-staticfiles-dev
.. _PyPI: http://pypi.python.org/pypi/django-staticfiles
.. _Apache: http://httpd.apache.org/
.. _Lighttpd: http://www.lighttpd.net/
.. _Nginx: http://wiki.nginx.org/
.. _Cherokee: http://www.cherokee-project.com/

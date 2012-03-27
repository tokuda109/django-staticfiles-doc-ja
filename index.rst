.. include:: ./README.rst

.. Differences to ``django.contrib.staticfiles``
   ---------------------------------------------

``django.contrib.staticfiles`` との違い
----------------------------------------------------------------

.. Features of ``django-staticfiles`` which Django's ``staticfiles`` **doesn't**
   support:

Djangoの ``staticfiles`` では **サポートしていない** ``django-staticfiles`` の機能:

.. Runs on Django 1.2.X.

* Django 1.2.X で動作します。

.. :attr:`~django.conf.settings.STATICFILES_EXCLUDED_APPS` settings -- A
   sequence of dotted app paths that should be ignored when searching for
   static files.

* :attr:`~django.conf.settings.STATICFILES_EXCLUDED_APPS` は、静的ファイルを探す時に、無視すべきものをドット区切りのアプリケーションのパスのシーケンスで指定します。

.. :attr:`~django.conf.settings.STATICFILES_IGNORE_PATTERNS` settings -- A
   sequence of glob patterns of files and directories to ignore when running
   ``collectstatic``.

* :attr:`~django.conf.settings.STATICFILES_IGNORE_PATTERNS` は、 ``collectstatic`` を実行した時に無視するファイルやディレクトリのパターンを指定します。

.. Legacy 'media' dir file finder -- a staticfiles finder that supports the
   location for static files that a lot of 3rd party apps support
   (``staticfiles.finders.LegacyAppDirectoriesFinder``).

* 静的ファイルのファインダは、ほとんどのサードパーティのアプリケーションの静的ファイルの場所をサポートします。

.. See the :doc:`settings` docs for more information.

より詳細な情報は :doc:`settings` を見てください。

Contents
--------

.. toctree::
   :maxdepth: 2

   commands
   helpers
   settings
   changelog

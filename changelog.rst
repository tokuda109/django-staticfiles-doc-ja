.. Changelog
   =========

変更履歴
===============

v1.1.2 (2011-08-25)
-------------------

.. Fixed a minor bug in how `django-appconf`_ was used.

* `django-appconf`_ の使われ方の小さなバグをフィックスしました。

v1.1.1 (2011-08-22)
-------------------

.. Fixed resolution of relative paths in ``CachedStaticFilesStorage``.

* ``CachedStaticFilesStorage`` で相対パスの解決方法をフィックスしました。

.. Started to use `django-appconf`_ and `versiontools`_.

* `django-appconf`_ と `versiontools`_ の使用を始めました。

.. _`django-appconf`: http://django-appconf.rtfd.org/
.. _`versiontools`: http://pypi.python.org/pypi/versiontools

v1.1 (2011-08-18)
-----------------

.. Pulled all changes from upstream Django:

* Djangoの変更からpullしました。

  .. ``static`` template tag to refer to files saved with the
     ``STATICFILES_STORAGE`` storage backend. It’ll use the storage ``url``
     method and therefore supports advanced features such as serving files
     from a cloud service.

  * ``STATICFILES_STORAGE`` ストレージバックエンドで保管したファイルを参照するための``static`` テンプレートタグを。
    ストレージで ``url`` メソッドを使って、クラウドサービスからファイルを配信するような高度な機能を使う

  .. ``CachedStaticFilesStorage`` which caches the files it saves (when
     running the ``collectstatic`` management command) by appending the MD5
     hash of the file's content to the filename. For example, the file
     ``css/styles.css`` would also be saved as ``css/styles.55e7cbb9ba48.css``

  * ``CachedStaticFilesStorage`` は、ファイル( ``collectstatic`` 管理コマンドを実行した時に集めたファイル)をキャッシュする時にファイルの内容からMD5ハッシュを使ってファイル名を付けて保存します。

  .. Added a ``staticfiles.storage.staticfiles_storage`` instance of the
     configured ``STATICFILES_STORAGE``.

  * ``STATICFILES_STORAGE`` の代わりに ``staticfiles.storage.staticfiles_storage`` を追加しました。

  .. ``--clear`` option for the management command which clears the
     target directory (by default ``STATIC_ROOT``) before collecting

  * 管理コマンドの ``--clear`` オプションはファイルを収集する前に、目的のディレクトリ(デフォルトでは ``STATIC_ROOT``)を消去します。

  .. Stop trying to show directory indexes in the included ``serve`` view.

  * ``serve`` ビューに含まれているディレクトリのインデックスを表示するのをやめました。

  .. Correctly pass kwargs to the URL patterns when using the static URL
     patterns helper.

  * 静的ファイル用のURLパターンのヘルパー関数を使う時に、URLパターンにキーワード引数

.. Use sys.stdout in management command, not self.stdout which was only
   introduced in a later Django version.

* 管理コマンドでDjangoの最新バージョンで導入されたself.stdoutではなく、sys.stdoutを使っています。

* Refactored AppSettings helper class to be only a proxy for Django's
  settings object instead of a singleton on its own.

.. Updated list of supported Django versions: 1.2.X, 1.3.X and 1.4.X

* サポートするDjangoのバージョンを1.2.X、1.3.X、1.4.Xに修正しました。

.. Updated list of supported Python versions: 2.5.X, 2.6.X and 2.7.X

* サポートするPythonのバージョンを2.5.X、2.6.X、2.7.Xに修正しました。

v1.0.1 (2011-03-28)
-------------------

.. Fixed an encoding related issue in the tests.

* テスト時にエンコーディングに関する問題のバグをフィックスしました。

.. Updated tox configuration to use 1.3 release tarball.

* Django 1.3のtarballtox configuration to useをアップデートしました。

.. Extended docs a bit.

* ドキュメントを少し追加しました。

v1.0 (2011-03-23)
-----------------

.. note::

   .. ``django-staticfiles`` is a backport of the staticfiles app in
      Django contrib. If you're upgrading from ``django-staticfiles`` < ``1.0``,
      you'll need to make a few changes. See changes below.

   ``django-staticfiles`` は、Django contribのstaticfilesアプリケーションを移植したものです。 ``django-staticfiles``  < ``1.0`` からアップグレードする場合は何点か修正をしなければいけません。以下の修正点を見てください。

.. Renamed ``StaticFileStorage`` to ``StaticFilesStorage``.

* ``StaticFileStorage`` を ``StaticFilesStorage`` に名前を変えました。

.. Application files should now live in a ``static`` directory in each app
   (previous versions of ``django-staticfiles`` used the name ``media``,
   which was slightly confusing).

* アプリケーションのファイルは個々のアプリケーションの ``static`` ディレクトリ( ``django-staticfiles`` の以前のバージョンでは ``media`` というディレクトリ名)に置いて下さい。

.. The management commands ``build_static`` and ``resolve_static`` are now
   called ``collectstatic`` and ``findstatic``.

* ``build_static`` と ``resolve_static`` の管理コマンドを、 ``collectstatic`` と ``findstatic`` に変えました。

.. The settings ``STATICFILES_PREPEND_LABEL_APPS`` and
   ``STATICFILES_MEDIA_DIRNAMES`` were removed.

* ``STATICFILES_PREPEND_LABEL_APPS`` と ``STATICFILES_MEDIA_DIRNAMES`` の設定を削除しました。

.. The setting ``STATICFILES_RESOLVERS`` was removed, and replaced by the new
   ``STATICFILES_FINDERS`` setting.

* ``STATICFILES_RESOLVERS`` の設定を削除して、新しく ``STATICFILES_FINDERS`` で設定するように変えました。

.. The default for ``STATICFILES_STORAGE`` was renamed from
   ``staticfiles.storage.StaticFileStorage`` to
   ``staticfiles.storage.StaticFilesStorage``

* ``STATICFILES_STORAGE`` のデフォルト値を ``staticfiles.storage.StaticFileStorage`` から ``staticfiles.storage.StaticFilesStorage`` に変えました。

.. If using ``runserver`` for local development (and the setting
   ``DEBUG`` setting is ``True``), you no longer need to add
   anything to your URLconf for serving static files in development.

* ローカルの開発環境で ``runserver`` (設定の ``DEBUG`` を ``True`` に設定している)を使った場合、
  開発時に静的ファイルを配信するURLをURLconfに追加する必要はない。

v0.3.4 (2010-12-25)
-------------------

.. Minor documentation update.

* ドキュメントを少しアップデートしました。

v0.3.3 (2010-12-23)
-------------------

.. warning::

   .. django-staticfiles was added to Django 1.3 as a contrib app.

      The django-staticfiles 0.3.X series will only receive security and data los
      bug fixes after the release of django-staticfiles 1.0. Any Django 1.2.X
      project using django-staticfiles 0.3.X and lower should be upgraded to use
      either Django 1.3's staticfiles app or django-staticfiles >= 1.0 to profit
      from the new features and stability.

      You may want to chose to use django-staticfiles instead of Django's own
      staticfiles app since any new feature (additionally to those backported
      from Django) will be released first in django-staticfiles.

   django-staticfilesはDjango 1.3でcontribアプリケーションとして追加されました。

   django-staticfilesの0.3.Xは1.0のリリース後はセキュリティとデータがなくなるバグのバグフィックスしか行いません。
   Django 1.2.X で 0.3.X 以下のバージョンを使っている場合は、
   django-staticfilesのバージョン1.0以上を使うかDjango 1.3のstaticfilesにアップグレードしてください。

   django-staticfilesで先に新しい機能がリリースされるので、django-staticfilesを使いたい場合は、Django付属のstaticfilesアプリケーションの代わりにdjango-staticfilesを使うことができます。

.. Fixed an issue that could prevent the ``build_static`` management command
   to fail if the destination storage doesn't implement the ``listdir``
   method.

* 目的のストレージで ``listdir`` メソッドが実装されていない場合に、 ``build_static`` 管理コマンドで、防げるようにフィックスしました。

.. Fixed an issue that caused non-local storage backends to fail saving
   the files when running ``build_static``.

* ``build_static`` を実行したときにローカルではないストレージバックエンドでファイルの保管に失敗する問題をフィックスしました。

v0.3.2 (2010-08-27)
-------------------

.. Minor cosmetic changes

* 簡単な変更をしました。

.. Moved repository back to Github: http://github.com/jezdez/django-staticfiles

* レポジトリをGithubに戻した。(http://github.com/jezdez/django-staticfiles)

v0.3.1 (2010-08-21)
-------------------

.. Added Sphinx config files and split up README.

* Sphinxのコンフィグファイルを追加して、READMEをいくつかのファイルに分割しました。

  .. Documetation now available under
     `django-staticfiles.readthedocs.org <http://django-staticfiles.readthedocs.org/>`_

  ドキュメントは以下の場所にあります。
  `django-staticfiles.readthedocs.org <http://django-staticfiles.readthedocs.org/>`_

v0.3.0 (2010-08-18)
-------------------

.. Added resolver API which abstract the way staticfiles finds files.

* staticfilesがファイルを探すベースとなるAPIを追加しました。

.. Added staticfiles.urls.staticfiles_urlpatterns to avoid the catch-all
   URLpattern which can make top-level urls.py slightly more confusing.
   From Brian Rosner.

* トップレベルのurls.pyが煩雑になってきたので、URLpatternから全てのURLを探索するのを避けるために、staticfiles.urls.staticfiles_urlpatternsを追加しました。これは、Brian Rosnerからのフォークです。

.. Minor documentation changes

* ドキュメントを少し修正しました。

.. Updated testrunner to work with Django 1.1.X and 1.2.X.

* Django 1.1.X と 1.2.X で動作するテストをアップデートしました。

.. Removed custom code to load storage backend.

* ストレージバックエンドを読み込む独自のコードを削除しました。

v0.2.0 (2009-11-25)
-------------------

.. Renamed build_media and resolve_media management commands to build_static
   and resolve_media to avoid confusions between Django's use of the term
   "media" (for uploads) and "static" files.

* Django で使われている "media" (アップロード用)と "static" ファイルの用語において、紛らわしさを避けるために、管理コマンドのbuild_mediaとresolve_mediaをbuild_staticとresolve_mediaに変えました。

.. Rework most of the internal logic, abstracting the core functionality away
   from the management commands.

* 管理コマンドからコア関数の内部処理のほとんどを書き直しました。

.. Use file system storage backend by default, ability to override it with
   custom storage backend

* デフォルトでシステムストレージバックエンドのファイルを、カスタムストレージバックエンドで上書きできるようにしました。

.. Removed --interactive option to streamline static file resolving.

* 静的ファイルの処理する--interactiveオプションを削除しました。

.. Added extensive tests

* 拡張テストを追加しました。

.. Uses standard logging

* 標準のloggingを使うようにしました。

v0.1.2 (2009-09-02)
-------------------

.. Fixed a typo in settings.py

* settings.pyのタイプミスをフィックスしました。

.. Fixed a conflict in build_media (now build_static) between handling
   non-namespaced app media and other files with the same relative path.

* 名前空間が決まっていないアプリケーションのメディアファイルと同じ相対パスの他のファイルとの
  間のbuild_media(今はbuild_static)内のコンフリクトをフィックスしました。

v0.1.1 (2009-09-02)
-------------------

.. Added README with a bit of documentation :)

* ドキュメントの一部として、READMEを追加しました。

v0.1.0 (2009-09-02)
-------------------

.. Initial checkin from Pinax' source.

* Pinaxのソースからの最初のチェックイン。

.. Will create the STATIC_ROOT directory if not existent.

* STATIC_ROOT ディレクトリがない場合は作成します。

.. Settings
   ========

設定
========

.. _STATIC_ROOT:

``STATIC_ROOT``
---------------

.. :Default: ``''`` (Empty string)

:Default: ``''`` (空の文字列)

.. The absolute path to the directory that contains static content after using
   :ref:`collectstatic`.

:ref:`collectstatic` を使うときに、静的コンテンツを置いているディレクトリへの絶対パスを指定します。

.. Example: ``"/home/example.com/static/"``

例: ``"/home/example.com/static/"``

.. When using the :ref:`collectstatic` management command this will be used to
   collect static files into, to be served under the URL specified as
   STATIC_URL_.

:ref:`collectstatic` の管理コマンドを使って、静的ファイルを集めた時、STATIC_URL_で指定したURLで配信されることになります。

.. This is a **required setting** to use :ref:`collectstatic` -- unless you've
   overridden STATICFILES_STORAGE_ and are using a custom storage backend.

これは :ref:`collectstatic` を使うのに **必須** です。STATICFILES_STORAGE_を上書きしない限り、独自のストレージバックエンドが使われます。

.. warning::

   .. This is not a place to store your static files permanently under
      version control; you should do that in directories that will be found by
      your STATICFILES_FINDERS_ (by default, per-app ``'static'`` subdirectories,
      and any directories you include in STATICFILES_DIRS_ setting). Files from
      those locations will be collected into STATIC_ROOT_.

   これはバージョン管理で静的ファイルをずっと置いておくための場所ではありません。STATICFILES_FINDERS_で見つけられたディレクトリでそうするべきです。(アプリケーション毎の ``'static'`` サブディレクトリと、STATICFILES_DIRS_で設定したディレクトリがデフォルトで)
   この場所にあるファイルはSTATIC_ROOT_に集められます。

.. See also STATIC_URL_.

STATIC_URL_も確認して下さい。

.. _STATIC_URL:

``STATIC_URL``
--------------

:Default: ``None``

.. URL that handles the files served from ``STATIC_ROOT`` and used by
   ``runserver`` in development mode (when ``DEBUG = True``).

開発モード(``DEBUG = True`` の時)で、 ``runserver`` を使った時に ``STATIC_ROOT`` から配信されたファイルを処理するためのURLを指定します。

Example: ``"/site_media/static/"`` or ``"http://static.example.com/"``

.. It must end in a slash if set to a non-empty value.

値を空白にしない場合はスラッシュを最後にしなければいけません。

.. See also STATIC_ROOT_.

STATIC_ROOT_も確認して下さい。

.. _STATICFILES_DIRS:

``STATICFILES_DIRS``
--------------------

:Default: ``[]``

.. This setting defines the additional locations the staticfiles app will traverse
   if the :class:`FileSystemFinder` finder is enabled, e.g. if you use the
   :ref:`collectstatic` or :ref:`findstatic` management command or use the
   static file serving view.

この設定は :class:`FileSystemFinder` ファインダが有効化されるか
:ref:`collectstatic` か :ref:`findstatic` の管理コマンドを使うか、

.. This should be set to a list or tuple of strings that contain full paths to
   your additional files directory(ies) e.g.::

これは、ファイルディレクトリのフルパスの文字列をリストかタプルとして設定してください。例として ::

    STATICFILES_DIRS = (
        "/home/special.polls.com/polls/static",
        "/home/polls.com/polls/static",
        "/opt/webfiles/common",
    )

.. Prefixes (optional)
   """""""""""""""""""

プレフィックス(オプション)
""""""""""""""""""""""""""""""""""""""

.. In case you want to refer to files in one of the locations with an additional
   namespace, you can **OPTIONALLY** provide a prefix as ``(prefix, path)``
   tuples, e.g.::

新たな名前空間でファイルを置く場合、 ``(prefix, path)`` のようにタプルでプリフィックス指定してください。例として ::

    STATICFILES_DIRS = (
        # ...
        ("downloads", "/opt/webfiles/stats"),
    )

.. Example:

例:

.. Assuming you have STATIC_URL_ set ``'/static/'``, the :ref:`collectstatic`
   management command would collect the stats files in a ``'downloads'``
   subdirectory of STATIC_ROOT_.

STATIC_URL_に ``'/static/'`` と設定しているものとすると、 :ref:`collectstatic` 管理コマンドはSTATIC_ROOT_のサブディレクトリ ``'downloads'`` にある静的ファイルを集めるでしょう。

.. This would allow you to refer to the local file
   ``'/opt/webfiles/stats/polls_20101022.tar.gz'`` with
   ``'/static/downloads/polls_20101022.tar.gz'`` in your templates, e.g.::

テンプレートで ``'/static/downloads/polls_20101022.tar.gz'`` とすると、ローカルファイルの ``'/opt/webfiles/stats/polls_20101022.tar.gz'`` を参照するようになります。例として ::

    <a href="{{ STATIC_URL }}downloads/polls_20101022.tar.gz">

``STATICFILES_EXCLUDED_APPS``
-----------------------------

:Default: ``[]``

.. A sequence of app paths that should be ignored when searching for static
   files::

静的ファイルを探索する時に無視するアプリケーションのパスを順番に指定します。 ::

    STATICFILES_EXCLUDED_APPS = (
        'annoying.app',
        'old.company.app',
    )

.. _STATICFILES_STORAGE:

``STATICFILES_STORAGE``
-----------------------

:Default: ``'staticfiles.storage.StaticFileStorage'``

.. The file storage engine to use when collecting static files with the
   :ref:`collectstatic` management command.

:ref:`collectstatic` 管理コマンドで静的ファイルを集めるときに使うファイルストレージエンジンです。

``STATICFILES_FINDERS``
-----------------------

:Default: ``('staticfiles.finders.FileSystemFinder',
             'staticfiles.finders.AppDirectoriesFinder')``

.. The list of finder backends that know how to find static files in
   various locations.

様々な場所にある静的ファイルをどのように探索するかを処理するファインダバックエンドのリストです。

.. The default will find files stored in the STATICFILES_DIRS_ setting
   (using :class:`staticfiles.finders.FileSystemFinder`) and in a
   ``static`` subdirectory of each app (using
   :class:`staticfiles.finders.AppDirectoriesFinder`)

デフォルトでSTATICFILES_DIRS_で設定した場所(`staticfiles.finders.FileSystemFinder` を使って) と、個々のアプリケーション内の ``static`` サブディレクトリ内(:class:`staticfiles.finders.AppDirectoriesFinder` を使って)に置かれているファイルを探します。

.. One finder is disabled by default:
   :class:`staticfiles.finders.DefaultStorageFinder`. If added to
   your STATICFILES_FINDERS_ setting, it will look for static files in
   the default file storage as defined by the ``DEFAULT_FILE_STORAGE``
   setting.

デフォルトで :class:`staticfiles.finders.DefaultStorageFinder` は無効化されています。
STATICFILES_FINDERS_に設定を追加する場合、 ``DEFAULT_FILE_STORAGE`` の設定で指定されたデフォルトのファイルストレージ内の静的ファイルを探します。

.. note::

   .. When using the ``AppDirectoriesFinder`` finder, make sure your apps
      can be found by staticfiles. Simply add the app to the
      ``INSTALLED_APPS`` setting of your site.

   ``AppDirectoriesFinder`` ファインダを使う時は、staticfilesによって確実に見つけることができます。サイトの ``INSTALLED_APPS`` の設定にアプリケーションを追加するのは簡単です。

.. Static file finders are currently considered a private interface, and this
   interface is thus undocumented.

静的ファイルのファインダは現在非公開で、ドキュメント化されていません。

.. Legacy 'media' dir finder (optional)
   """"""""""""""""""""""""""""""""""""

古い 'media' ディレクトリのファインダ(オプション)
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

.. To ease the burden of upgrading a Django project from a non-``staticfiles``
   setup, the optional finder backend
   :class:`staticfiles.finders.LegacyAppDirectoriesFinder` is shipped as part of
   ``django-staticfiles``. When added to the STATICFILES_FINDERS_ setting, it'll
   enable ``staticfiles`` to use the ``media`` directory of the apps in
   ``INSTALLED_APPS``, similarly
   :class:`staticfiles.finders.AppDirectoriesFinder`.

``staticfiles`` を使っていないDjangoプロジェクトのアップグレードの負担を軽減するために、オプションの :class:`staticfiles.finders.LegacyAppDirectoriesFinder` ファインダーバックエンドは ``django-staticfiles`` の一部として追加されました。
STATICFILES_FINDERS_ に設定を追加した時に、 ``INSTALLED_APPS`` にあるアプリケーションの ``media`` を使うために ``staticfiles`` を :class:`staticfiles.finders.AppDirectoriesFinder` と同じように有効にして下さい。

.. This is especially useful for 3rd party apps that haven't been switched over
   to the ``static`` directory instead. If you want to use both ``static``
   **and** ``media``, don't forget to have
   :class:`staticfiles.finders.AppDirectoriesFinder` in the
   STATICFILES_FINDERS_, too.

これは、サードパーティのアプリケーションが ``media`` の代わりに ``static`` ディレクトリを使うように切り替えられていない場合は特に有効です。
``static`` と ``media`` の両方を使う場合、STATICFILES_FINDERS_に :class:`staticfiles.finders.AppDirectoriesFinder` を入れるのも忘れないで下さい。

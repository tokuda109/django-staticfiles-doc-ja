.. Management Commands
   ===================

管理コマンド
================

.. highlight:: console

.. _collectstatic:

collectstatic
-------------

.. Collects the static files from all installed apps and copies them to the
   :ref:`STATICFILES_STORAGE`.

インストールしている全てのアプリケーションから静的ファイルを集めて :ref:`STATICFILES_STORAGE` にコピーします。

.. Duplicate file names are resolved in a similar way to how template resolution
   works. Files are initially searched for in :ref:`STATICFILES_DIRS` locations,
   followed by apps in the order specified by the ``INSTALLED_APPS`` setting.

ファイル名の重複は、テンプレートが処理と同じような方法で解決するようにしています。ファイルは :ref:`STATICFILES_DIRS` に指定した場所や ``INSTALLED_APPS`` の設定で指定した順にアプリケーションの場所から最初に検索されます。

.. Some commonly used options are:

一般的に使用するオプションは次のとおりです:

``--noinput``

    .. Do NOT prompt the user for input of any kind.

    あらゆる種類の入力を求めるプロンプトを表示しない。

``-i PATTERN`` or ``--ignore=PATTERN``

    .. Ignore files or directories matching this glob-style pattern. Use multiple
       times to ignore more.

    glob-styleのパターンに一致したファイルやディレクトリは無視します。さらに無視するには何回も使用して下さい。

``-n`` or ``--dry-run``

    .. Do everything except modify the filesystem.

    ファイルシステムを変更する以外のすべてを実行することができます。

``-l`` or ``--link``

    .. Create a symbolic link to each file instead of copying.

    コピーの代わりに、それぞれのファイルへのシンボリックリンクを作成します。

``--no-default-ignore``

    .. Don't ignore the common private glob-style patterns ``'CVS'``, ``'.*'``
       and ``'*~'``.

    ``'CVS'`` や ``'.*'`` や ``'*~'`` のプライベートのglob-styleのパターンに無視しません。

``-c`` or ``--clear``

    .. versionadded:: 1.1

    .. Clear the existing files before trying to copy or link the original file.

    コピーかオリジナルのファイルにリンクする前に既にあるファイル消去します。

``--no-post-process``

    .. versionadded:: 1.1

    .. Don't call the
       :meth:`~staticfiles.storage.StaticFilesStorage.post_process`
       method of the configured :ref:`staticfiles_storage` storage backend.

    設定済みの :ref:`staticfiles_storage` ストレージバックエンドの :meth:`~staticfiles.storage.StaticFilesStorage.post_process` メソッドを実行しません。

.. For a full list of options, refer to the collectstatic management command help
   by running::

オプションの全てのリストについては、collectstaticの管理コマンドでhelpを実行して確認して下さい。 ::

   $ python manage.py collectstatic --help

.. _findstatic:

findstatic
----------

.. Searches for one or more relative paths with the enabled finders::

有効化されているファインダーで一つ以上の相対パスを探索します。 ::

   $ python manage.py findstatic css/base.css admin/js/core.css
   /home/special.polls.com/core/media/css/base.css
   /home/polls.com/core/media/css/base.css
   /home/polls.com/src/django/contrib/admin/media/js/core.js

.. By default, all matching locations are found. To only return the first match
   for each relative path, use the ``--first`` option::

デフォルトでは、一致するすべての場所が検索されます。``--first``オプションを使うと、それぞれの相対パスから最初に一致したものを返します。 ::

   $ python manage.py findstatic css/base.css --first
   /home/special.polls.com/core/media/css/base.css

.. This is a debugging aid; it'll show you exactly which static file will be
   collected for a given path.

これはデバッグ用で、静的ファイルが指定されたパスから正しく集められたか表示します。

runserver
---------

.. Overrides the core ``runserver`` command if the ``staticfiles`` app
   is installed (in ``INSTALLED_APPS``) and adds automatic serving of static
   files and the following new options.

``staticfiles`` アプリケーションが( ``INSTALLED_APPS`` に)インストールされている場合、Djangoの ``runserver`` コマンドが上書きされます。静的ファイルの自動的な配信機能と以下の新しいオプションが追加されました。

``--nostatic``

.. Use the ``--nostatic`` option to disable serving of static files with the
   ``staticfiles`` app entirely. This option is only available if the
   ``staticfiles`` app is in your project's ``INSTALLED_APPS`` setting.

``--nostatic`` オプションを使うと、``staticfiles`` アプリケーションで静的ファイルの配信できないようにします。
このオプションはセッティングのプロジェクトの ``INSTALLED_APPS`` の設定で ``staticfiles`` がインストールされている時のみ使えます。

.. Example usage::

使用例 ::

    django-admin.py runserver --nostatic

``--insecure``

.. Use the ``--insecure`` option to force serving of static files with the
   ``staticfiles`` app even if the ``DEBUG`` setting is ``False``.

``--insecure`` オプションを使うと、設定の ``DEBUG`` を ``False`` にしていても ``staticfiles`` アプリケーションで静的ファイルを強制的に配信します。

.. warning::

  .. By using this you acknowledge the fact that it's
     **grossly inefficient** and probably **insecure**.

     This is only intended for local development, should
     **never be used in production** and is only available if the
     ``staticfiles`` app is in your project's ``INSTALLED_APPS`` setting.

  これを使用することで、 **非効率的** で **セキュアではない** ということを把握してください。

  ローカル環境とセッティングの ``INSTALLED_APPS`` で ``staticfiles`` がインストールされている時のみを対象としているので、 **本番の環境では使わないで下さい** 。

.. Example usage::

使用例 ::

    django-admin.py runserver --insecure

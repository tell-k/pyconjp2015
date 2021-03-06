=====================================================
PyPIデビュー2015
=====================================================

| tell-k
| PyCon JP 2015 (2015.10.11)

お前誰よ？
=====================================

.. image:: https://pbs.twimg.com/profile_images/1045138776224231425/3GD8eWeG_200x200.jpg
.. image:: _static/images/vxjmiemo.png

* tell-k
* BeProud.inc
* 情弱プログラマー
* 「猫はいません」
* http://tell-k.github.io/pyconjp2015/


目的/動機
=====================================

* 趣味でちょいちょいPyPIにアップロードするようになった
* 一通り自分の中でやり方が固まってきた
* 振り返りも兼ねて、一通りまとめておきたかった
* 初心者の人でも、迷わず、事故らず、サクッと、ちゃんとやってる感を醸しだしつつ、 **マサカリ** を投げられないように、PyPIにデビューできるようになるといいですね。

趣味
=====================================

* https://pypi.python.org/pypi/sphinxjp.themes.basicstrap
* https://pypi.python.org/pypi/sphinxjp.themes.revealjs
* https://pypi.python.org/pypi/sphinxcontrib-gravatar
* https://pypi.python.org/pypi/django-modelsdoc
* https://pypi.python.org/pypi/goolabs
* https://pypi.python.org/pypi/csquery
* https://pypi.python.org/pypi/woothee-python

対象
=====================================

* Pythonでライブラリを配布してみたい人
* PyPIとかパッケージング周りがまだよく分からない人

対象
=====================================

* ぶっちゃけ調べるのがだるいので、まとめておいて欲しい人

.. image:: _static/images/ljj0l-e4.png
   :width: 70%

Pythonプロフェッショナルプログラミング 第2版
===============================================

.. image:: http://ecx.images-amazon.com/images/I/51ZNlK0%2Bn-L._SL160_.jpg
   :width: 20%

* 今日話す内容の半分くらいこの本に書いてあります

目次
==========================================

* PyPIとは？
* PyPAとは？
* Pythonパッケージ作成
* 便利サービス
* トラブルシューティング
* 参考
* まとめ

PyPIとは？
=====================================

.. image:: _static/images/3x4hkmn6.png
   :width: 80%

PyPiとは？
=====================================

* Python Package Index(https://pypi.python.org/pypi)
* PSF(Python Software Foundation)が運営するPythonパッケージを管理するためのサイト/リポジトリ
* ここにPythonパッケージをアップロードする
* **パイピーアイ** と読むそうです。

PyPAとは？
=====================================

.. image:: _static/images/zli4wet3.png
   :width: 80%

PyPAとは？
=====================================

* Python Package Authority(https://github.com/pypa)
* https://bitbucket.org/pypa/
* Pythonパッケージに関連する諸々取りまとめる **有志のコミュニティ** です
* 「setuptools」や「pip」 や 「virtualenv」 のなどのパッケージング関連のライブラリの管理
* 次世代PyPIの `Warehouse <https://warehouse.python.org/>`_ も開発
* パッケージ関連のPEPなどを提案/推進
* **パイピーエー** と勝手に読んでいます

Pythonパッケージ作成
=====================================

Pythonパッケージ作成
=====================================

1. アカウント作成(https://pypi.python.org/pypi?%3Aaction=register_form)
2. setup.pyを書く
3. パッケージ登録 & アップロード

2. setup.py
=====================================

* setuptools ... パッケージングするための必須ツール
* setup.py ... パッケージのメタデータを記載

.. code-block:: python

  from setuptools import setup, find_packages

  setup(
      name='sample',
      version='1.0.0',
      url='https://github.com/pypa/sampleproject',
      packages=find_packages(exclude=['tests*']),
  )

3. パッケージ登録
=====================================

.. code-block:: bash

 # パッケージ登録
 $ python setup.py register 
 # 指示に従って入力

 # パッケージアップロード
 $ python setup.py sdist upload

終わりです。簡単ですね。


そういうわけにもいきますまい...
=====================================

.. figure:: _static/images/wuuz3mx_.png
   :width: 70%

Pythonパッケージ作成
=====================================

1. setup.pyを書く
2. 開発する
3. テストする
4. 配布物を決める
5. 登録/アップロード

構成
=====================================

例えば「sample」というパッケージを妄想する

.. code-block:: bash

 sample
   ├── MANIFEST.in
   ├── README.rst
   ├── sample        <- Pythonパッケージ
   │   └── __init__.py
   ├── setup.cfg
   ├── setup.py
   └── tests         <- テストコード
      ├── __init__.py
      └── test_sample.py

* **setup.cfg** は「setup.py」のdefault値や、aliasを管理する設定ファイル
* **MANIFEST.in**  は 配布物に含める内容を定義します。後述します。

1. setup.pyを書く
=====================================

* パッケージのメタデータを記述するファイル。
* 「setuptools」の setup関数を実行。
* pipで配布されるパッケージは必ずこれが必要。

setup.pyに書く事
=====================================

* name ....................... パッケージ名
* version ..................... バージョン番号 ex) 1.2.0
* description ............. パッケージの説明
* long_description ... パッケージの説明(長)(ReST)
* url ............................. プロジェクトのURL
* author ..................... 作者名
* author_email ......... 作者のメアド
* license ....................... ライセンス ex) MIT
* classifiers ................ カテゴリ

setup.pyに書く事
=====================================

* keywords ................. 関連キーワード
* packages ................. インストール対象パッケージのパス
* install_requires ........ 依存パッケージ
* tests_require ........... setup.py test のための依存パッケージ
* extras_require ......... インストール時には必要のない追加依存パッケージ
* entry_points ............ プラグインサポート

* 参考: http://docs.python.jp/3/distutils/setupscript.html
* 参考: https://packaging.python.org/en/latest/distributing/#setup-args

setup.pyの例
=====================================

.. code-block:: python

 setup(
     name='sample',
     version='1.0.0',
     description='A sample Python project',
     long_description=long_description,
     url='https://github.com/pypa/sampleproject',
     author='The Python Packaging Authority',
     author_email='pypa-dev@googlegroups.com',
     license='MIT',
     classifiers=[
         'Development Status :: 3 - Alpha',
         'Intended Audience :: Developers',
         'Topic :: Software Development :: Build Tools',
         'License :: OSI Approved :: MIT License',
         'Programming Language :: Python :: 2',
         'Programming Language :: Python :: 3',
     ],
     keywords='sample setuptools development',
     packages=find_packages(exclude=['contrib', 'docs', 'tests*']),
     install_requires=['peppercorn'],
  )

参考: https://github.com/pypa/sampleproject/blob/master/setup.py

classifiers is 何?
=====================================

* Pythonパッケージをカテゴライズする情報
* PyPIの `classifiersのページ <https://pypi.python.org/pypi?:action=browse>`_ から辿れるようになる。
* `classifiersの一覧 <https://pypi.python.org/pypi?:action=list_classifiers>`_ から選ぶことができる。

classifiers
=====================================

* Frameworkの細かいバージョン指定

::

 Framework :: Django
 Framework :: Django :: 1.4
 Framework :: Django :: 1.5
 Framework :: Django :: 1.6
 Framework :: Django :: 1.7
 Framework :: Django :: 1.8

* 開発ステータス

::

 Development Status :: 1 - Planning
 Development Status :: 2 - Pre-Alpha
 Development Status :: 3 - Alpha
 Development Status :: 4 - Beta
 Development Status :: 5 - Production/Stable
 Development Status :: 6 - Mature
 Development Status :: 7 - Inactive

version
=====================================

* `PEP440 Version Identification and Dependency Specification <https://www.pypa.io/en/latest/peps/#pep440s>`_ 
* バージョン番号のつけ方についてのPEP

::

 1.2.0.dev1  # Development release
 1.2.0a1     # Alpha Release
 1.2.0b1     # Beta Release
 1.2.0rc1    # Release Candidate
 1.2.0       # Final Release
 1.2.0.post1 # Post Release
 15.10       # Date based release
 23          # Serial release

version
=====================================

* PyPAのガイドでは、 `Sematic Versioning <http://semver.org/lang/ja/>`_  も推奨
* **メジャー.マイナー.パッチ** の3つからなるバージョン番号。例 **1.2.0**

::

  バージョンナンバーは、メジャー.マイナー.パッチとし、バージョンを上げるには、
  
  - APIの変更に互換性のない場合はメジャーバージョンを、
  - 後方互換性があり機能性を追加した場合はマイナーバージョンを、
  - 後方互換性を伴うバグ修正をした場合はパッチバージョンを上げます。
 
  プレリリースやビルドナンバーなどのラベルに関しては、メジャー.マイナー.パッチの
  形式を拡張する形で利用することができます。

via http://semver.org/lang/ja/

version
=====================================

* 「setup.py」やソースコードなど、あちこちにバージョン番号を書くと更新を忘れたりします。
* ソースコードの一箇所に書いて、それを「setup.py」から参照する。

.. code-block:: python

  def find_version(*file_paths):
      version_file = read(*file_paths)
      version_match = re.search(r"^__version__ = ['\"]([^'\"]*)['\"]",
                                version_file, re.M)
      if version_match:
          return version_match.group(1)
      raise RuntimeError("Unable to find version string.")

  setup(
     ...
     version=find_version("package", "__init__.py")
     ...
  )

via `Single-sourcing the Project Version <https://packaging.python.org/en/latest/single_source_version/#single-sourcing-the-version>`_

long_description
=====================================

* PyPI上で表示される長い説明文
* `reStructuredText <http://docutils.sourceforge.net/rst.html>`_ に対応。綺麗に整形される
* Markdownに対応してません。

.. image:: _static/images/m5j2qspj.png

long_description
=====================================

* README.rst のファイルの中身を setup に渡す

.. code-block:: python

 with open(path.join(here, 'README.rst'), encoding='utf-8') as f:
     long_description = f.read()

  setup(
     ...
     long_description=long_description,
     ...
  )

via https://github.com/pypa/sampleproject/blob/master/setup.py

packages
====================================

* 実際にインストールされるPythonパッケージのパス
* 「setuptools」に「find_packages」という便利関数があります。
* プロジェクト内から適当にPythonパッケージを探してくれる

.. code-block:: python

 from setuptools import find_packages

 setup(
    ...
    packages=find_packages(exclude=['tests*'])
    ...
 )

excludeで適切に除外
====================================

* 「packages」には「pip install」した時に必要なものだけを指定しよう
* テストコードは、ライブラリ利用時には不要。
* 除外しない場合、そのままトップレベルにインストールされてしまう。

.. code-block:: python

 # × 除外しない
 packages=find_packages()

 # ○ 除外する
 packages=find_packages(exclude=['tests*'])

.. code-block:: python

 # 除外しなかった場合
 import sample
 import tests.test_sample  # トップレベルでテストコードがインストールされてしまう


install_requires
====================================

* 依存パッケージ
* 「pip install」時に一緒にインストールしてくれる

.. code-block:: python

 setup(
    ...
    install_requires=[
       'Hoge',
    ]
    ...
 )

install_requires VS requirements.txt
=========================================

* 「pip freeze」
* インストールされているPythonパッケージを一覧で出してくれる。

.. code-block:: bash

 $ pip freeze > requirements.txt

* requirements.txt

::

 # インストール済みパッケージの一覧を出してくれる
 # バージョンを固定
 Spam==1.0.0
 Ham==2.1.0
 Egg==1.3.0

install_requiresにこれ使えば？
=========================================

* 一見問題なさそうに見える方法
* 依存パッケージは、バージョン固定でインストールされる

.. code-block:: python

 with open('requiments.txt') as fp:
        requires = fp.readlines()

 install_requires=requires

バージョン固定されると単純に困る
=========================================

.. code-block:: bash

 $ pip install Spam
 $ pip freeze | grep Spam
 Spam==1.1.0 
 # => Spamの最新版 1.1.0 が インストール

 $ pip install sample
 $ pip freeze | grep Spam
 Spam==1.0.0 
 # => install_requires の バージョン固定により1.0.0になってしまう

 ＿人人人人人人人人人人人人人人人＿
 ＞　突然のダウングレード！！！　＜
 ￣Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^￣

 # 別パッケージが同様に、別のバージョン番号を固定で指定してると、
 # バージョン競合が発生しインストールに失敗するケースも...

とてもつらい
=========================================

.. image:: _static/images/p1fcoye0.png
   :width: 40%

install_requires の 役割
=========================================

* そのパッケージを動かすための **最低限必要とする依存パッケージ**
* 「pip freeze」による 「requirements.txt」は **Python実行環境を再現するため**
* それぞれ主な利用用途が違う
* 「install_requires」は、最低限必要なバージョンを記載する程度に留めましょう
* バージョンを指定する場合はドキュメントやREADMEに記載があると親切

::

  # そもそもバージョンを指定しない
  install_requires=['Ham']
 
  # 最低限必要なバージョンだけを記載
  install_requires=['Ham>=1.0.0']

  # 範囲を限定的にするとか
  install_requires=['Ham>=1.0.0,<2']

  # requirements.txtにもバージョン指定なし、範囲指定を記述可能
  # install_requiresにバージョンを固定しないというのが大事

* 参考: `install_requires vs Requirements files <http://python-packaging-user-guide.readthedocs.org/en/latest/requirements/>`_

開発する
=================================

* Python2/3両対応
* 開発モード

Python2/3両対応
=================================

* Python2.7 は積極的にサポートはされませんが2020年までメンテされます
* Python2.8 はありません
* Python2 の利用者は結構います。ライブラリやアプリなどがPython3に移行仕切れていない
* スムーズ移行できるように両対応しておくのが良い
* 小さいパッケージであれば難しくはありません
* 参考: `Python2.5からPython3.3で動作するツールの作り方 <http://shimizukawa.bitbucket.org/pyconapac2013-how-to-make-with-python2-to-3/index.html>`_

Python2/3両対応
=================================

* 2/3の互換性を保つライブラリを利用する(pipでインストール可能)

  * `six <https://pypi.python.org/pypi/six>`_
  * `python-future <https://pypi.python.org/pypi/future>`_

* __future__ で Py3 の機能を利用する

  .. code-block:: python

    from __future__ import division, print_function, absolute_import, unicode_literals

  * 参考: `Python 2/3 両対応のために \`unicode_literals\` を使うべきか <http://methane.hatenablog.jp/entries/2014/01/18>`_

* 2to3 というツールはメンテコストが高そうなのでオススメしないです

  * 参考: `2014/05/25 Sphinxメンテナ日記: 2to3やめてsixに切り換えました <http://www.freia.jp/taka/blog/sphinx-dev-remove-2to3/index.html>`_

sixの例
=================================

.. code-block:: python

 import six

 d = {'hoge1': 'fuga', 'hoge2': 'fuga', }

 # python2
 for k, v in d.iteritems():
     print(k, v)

 # python3
 for k, v in d.items():
     print(k, v)

 # python2, 3 両方
 for k, v in six.iteritems(d):
     print(k, v)


先達の知見を得る
=================================

* 困ったら他の著名なライブラリがどうやってるか参考にすると良い
* 慣習的に互換性を吸収するようなモジュールは **compat.py** という名前が多い。
* githubでお気に入りのライブラリの **compat.py** を探そう。

Python3しか対応しないのもあり
==================================

.. image:: http://cdn-ak.f.st-hatena.com/images/fotolife/n/niguruta/20101015/20101015123332.jpg
   :width: 90%

開発モード
=================================

* 「pip install -e .」
* 「python setup.py develop」 と一緒
* 「sitepackages」にパスを通してライブラリとして利用できるようになる。
* これを知らなくてキツかった。。。
* 参考: `Pythonライブラリパスをコントロールする <http://aodag.posthaven.com/python-3>`_

開発モード
==================================

.. code-block:: bash

  $ pip install -e .

  # そのまま動作確認可能
  $ python 
  Python 3.4.3 (default, Mar 23 2015, 04:19:36) 
  [GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.57)] on darwin
  Type "help", "copyright", "credits" or "license" for more information.
  >>> import sample
  >>> sample.main()
  Call your main application code here

テスト
==================================

* 利用者視点で採用する際の後押しになる
* サポートされるべき範囲が適切にテストできてるか確認できる
* tox, pytestなど充実したライブラリがある

tox
==================================

* https://testrun.org/tox/latest/
* 複数のPythonのバージョンを一気にテストできる便利ツール
* パッケージオーナーにはおなじみ
* pipでインストールして設定ファイル(tox.ini)を作るだけ使えます。

.. code-block:: bash

 $ pip install tox

tox.iniの例
==================================

* 処理系のインストールは事前に必要です

:: 

 [tox]
 envlist=py27,py34,py35,pypy

 [testenv]
 commands=
     python setup.py test 


.. code-block:: bash

 # 全バージョンでテストを実行
 $ tox 

 # バージョンを指定してテスト実行
 $ tox -e py35


どこまでサポートすればいいの？
==================================

* Python3系は 3.5, 3.4, 3,3 
* Python2系は 2.7
* 3.2以下は ユニコードリテラル(u"hoge")が使えなかったり、ユーザー数も少ない事から、対応を切り捨てたりするライブラリもあります。
* 互換性のためのライブラリの「python-future」も切り捨てています。
* pip の次メジャーバージョンアップ(7 -> 8)の時は切り捨てるそうです。
* 参考: `Dropping support for Python 3.2 in pip 8?  <https://groups.google.com/forum/#!msg/pypa-dev/Ef0PF2ZGAv0/hrO4BHkOBQAJ>`_

pytest
==================================

* http://pytest.org/latest/
* assert の失敗時の情報を増やしてくれる -> 見易い
* unittestのようにクラスを使わなくても良い
* unittestのようにassertXXXを沢山おぼえなくても良い
* テストランナーとしても使い易い

assertが賢くなる例
==================================

.. code-block:: bash

  $ py.test test_assert.py

  ...

  =========== FAILURES =============
  __________ test_main _____________

      def test_main():
          lst1 = ['test1', 'test2']
          lst2 = ['test1', 'test3']

  >       assert lst1 == lst2, 'Not equal lists'

  E       AssertionError: Not equal lists
  E       assert ['test1', 'test2'] == ['test1', 'test3']
  E         At index 1 diff: 'test2' != 'test3'
  E         Full diff:
  E         - ['test1', 'test2']
  E         ?                ^
  E         + ['test1', 'test3']
  E         ? 


setup.py testから呼ぶ
==================================

* 「 **setup.py test** でテストする奴は良く訓練された **Pythonista** だ」
* 「setup.py test」てテストができれば誰も迷わなくて幸せ
* 「pytest」を実行するために「py.test」コマンドを実行する必要がある
* 「setup.py test」で呼び出せるようにしたい
* ドキュメントに書いてあります
* `Integration with setuptools test commands <https://pytest.org/latest/goodpractises.html#integration-with-setuptools-test-commands>`_

setup.py testから呼ぶ
==================================

* setup.py でtestコマンドをカスタマイズできます。

.. code-block:: python

 import sys

 from setuptools.command.test import test as TestCommand

 class PyTest(TestCommand):
     user_options = [('pytest-args=', 'a', "Arguments to pass to py.test")]

     def initialize_options(self):
         TestCommand.initialize_options(self)
         self.pytest_args = []

     def finalize_options(self):
         TestCommand.finalize_options(self)
         self.test_args = []
         self.test_suite = True

     def run_tests(self):
         #import here, cause outside the eggs aren't loaded
         import pytest
         errno = pytest.main(self.pytest_args)
         sys.exit(errno)

setup.py testから呼ぶ
==================================

* cmdclassを活用するとテスト以外のコマンドも追加できたりします。便利ですね。

.. code-block:: python

 setup(
     ...
     tests_require = ['pytest'],
     cmdclass = {'test': PyTest},
     ...
     )

.. code-block:: bash

 # py.testが実行される
 $ python setup.py test

coverage
==================================

* pytestからcoverage取れるpytest-covというプラグラインがある
* "--cov-report term-missing" がおすすめ。テストが通ってない行番号を教えてくれる

::

 $ python setup.py test -a "--cov sample --cov-report term-missing"

.. image:: _static/images/s8kwn9ff.png


配布物を決める
==================================

* ソースコード以外に配布すべきもの
* setup.py
* setup.cfg
* README.rst
* MANIFEST.in ... 追加ファイルの定義
* tox.ini
* テストコード
* ドキュメント

MANIFEST.in
==================================

* sdist(ソースディストリビューション)に一緒に追加したいファイルを定義するファイル
* ビルドコマンドを叩くとこれに従って配布パッケージを生成してくれる

::

 include README.rst
 include tox.ini
 include setup.cfg
 recursive-include docs *
 recursive-include tests *
 include sample/*.dat

ビルド
==================================

* 配布物が決まったらビルドする
* sdist ... ソースディストリビューション
* wheel ... バイナリパッケージ

sdist
==================================

* ソースディストリビューション
* MANIFEST.in に従って配布内容をで固めてくれる

.. code-block:: bash

 # ビルド
 $ python setup.py sdist

 # 直下のdistにsdistが生成されます
 $ ls dist
 sample-0.0.1.tar.gz

wheel
==================================

* バイナリパッケージ
* `PEP427 The Wheel Binary Package Format 1.0 <https://www.python.org/dev/peps/pep-0427/>`_
* ビルド済みのパッケージを配布可能。
* デファクトスタンダードな「egg」を「pip」は取り扱わなかった。
* 「wheel」はPEP準拠フォーマットなので「pip」も対応。
* 直接インストール可能なので、インストール時間の短縮につながる。
* wheelパッケージの作成には「wheel」のインストールが必要です。
* wheelパッケージのインストールには「wheel」は必要ありません。

.. code-block:: bash

 $ pip install wheel

wheel
==================================

* パッケージの作成
* 対象の環境に応じたパッケージの作成ができる

.. code-block:: bash

 $ python setup.py bdist_wheel

 # python3にしか対応しない
 $ python setup.py bdist_wheel --python-tag=py3


wheel
==================================

* Python2と3の両方に対応している場合
* setup.cfgに「universal = 1 」と書いておくと良いです。

::

 [wheel]
 universal = 1
 
.. code-block:: bash

 $ python setup bdist_wheel
 $ ls
 sample-0.0.1-py2.py3-none-any.whl

アップロード
==================================

* いよいよPyPIにアップロード
* アカウント作成
* パッケージの登録
* パッケージのアップロード
* 「testpypi.python.org」 の利用
* ドキュメントのアップロード

アカウントの作成
==================================

.. image:: _static/images/ydjsq6a_.png

https://pypi.python.org/pypi?%3Aaction=register_form

パッケージの登録
==================================

* setup.py registerで登録

.. code-block:: bash

 $ ./setup.py register
 running register
 running egg_info
 writing tesdat.egg-info/PKG-INFO
 writing top-level names to sample.egg-info/top_level.txt
 writing dependency_links to sample.egg-info/dependency_links.txt
 reading manifest file 'sample.egg-info/SOURCES.txt'
 writing manifest file 'sample.egg-info/SOURCES.txt'
 running check
 We need to know who you are, so please choose either:
  1. use your existing login,

 ...

 Registering sample to https://pypi.python.org/pypi
 Server response (200): OK
 I can store your PyPI login so future submissions will be faster.
 (the login will be stored in /home/tell-k/.pypirc)
 Save your login (y/N)?y

パッケージの登録
==================================

* ~/.pypircという設定ファイルが生成されます。
* ここにID/PASSを設定しておけばアップロードする際に毎回聞かれません。
* 平文なのであまりおすすめはしません

::

 [distutils]
 index-servers =
    pypi
 
 [pypi]
 username: tell-k
 password: xxxxxxxxxxxx

パッケージのアップロード
==================================

* ビルドコマンドに続けて upload を追加
* ビルドしてそのままアップロードされる
* あとは確認するのみ

.. code-block:: bash

 # 事前に「setup.py」 の記述内容をチェック
 $ python setup.py check -r -s

 $ python setup.py sdist bdist_wheel upload

 # × uplaod単体では利用できない
 $ python upload
 running upload
 error: No dist file created in earlier command

Twineでのアップロード(推奨)
==================================

* https://pypi.python.org/pypi/twine
* PyPAではtwineを利用してのアップロードが推奨されている。
* TLS通信でよりセキュア
* uploadが単体できる -> 何度もビルドしなくて良い。確認が取れたものだけだアップロードできる
* 別途インストールが必要
* 参考 `Upload your distributions <https://python-packaging-user-guide.readthedocs.org/en/latest/distributing/#upload-your-distributions>`_

.. code-block:: bash

 $ pip install twine
 $ twine uplaod dist/*

testpypi.python.org の利用
==================================

* とりあえず試してみたい
* http://testpypi.python.org を利用して実験しましょう。
* 実験用のpypiで、わかりやすいラベル以外はpypiと一緒
* アカウント作成は **もう一回必要**

.. image:: _static/images/lttwh7en.png

pypircの設定
==================================

::

 [distutils]
 index-servers=
     pypi
     pypitest

 [pypitest]
 repository = https://testpypi.python.org/pypi
 username = <your user name goes here>
 password = <your password goes here>

 [pypi]
 repository = https://pypi.python.org/pypi
 username = <your user name goes here>
 password = <your password goes here>

testpypiへの操作
=================================

.. code-block:: bash

 パッケージ登録
 $ python setup.py register -r https://testpypi.python.org/pypi

 アップロード
 $ python setup.py sdist upload -r https://testpypi.python.org/pypi

 インストール
 $ pip install -i https://testpypi.python.org/pypi <package name>
 
 依存パッケージがあるようのものは「--extra-index-url」を利用すると良い
 $ pip install --extra-index-url https://testpypi.python.org/pypi <package name>


その他のTips
=====================================

* ドキュメントのアップロード
* コマンドラインツール
* Githubのバージョンタグをつける
* Djangoアプリみたいなの

ドキュメントのアップロード
=====================================

* setup.py と同階層にdocs(Sphinxドキュメント)を用意
* 「Sphinx」のインストールが必要です。

setup.cfg::

 [upload_docs]
 upload-dir = _build/sphinx/html

.. code-block:: bash

 # Sphinxをビルドしてアップロード
 $ python setup.py build_sphinx upload_docs

 # アップロード後はpyhthonhosted.orgのURLで確認できる 
 # pypiからリンクが貼られれます
 http://pythonhosted.org/<packge name>/

コマンドラインツール
=====================================

* コマンドラインツールを作りたい場合
* setup.pyの「entry_points」に「console_scripts」を指定する

.. code-block:: python

 entry_points = {
     "console_scripts": [
         "sayhello=sample.commands:hello",
     ]
 }

 # sample.commandsモジュールのhello関数を呼び出す

* インストール時にPythonと同じ実行パスにコマンドを作成してくれる

.. code-block:: bash

 $ pip install sample

 $ sayhello
 Hello! my name is hoge.

 $ which sayhello
 /usr/local/bin/sayhello


Githubのバージョンタグをつける
=====================================

* PyPIが落ちた時や、過去のバージョンをPyPIから削除した場合の保険
* 後から利用者が追えるようにGithubにバージョンタグを付けてあげると親切

.. code-block:: bash

 # リリース時点でタグを切る
 $ git tag -am "Version 1.0.0" v1.0.0
 $ git push origin --tags


Githubのバージョンタグをつける
=====================================

.. image:: _static/images/x9134jfl.png
   :width: 80%

Djangoアプリみたいなの
=====================================

* 再利用可能な Djangoアプリ の配布
* 公式ドキュメントに書いてあります。
* `Advanced tutorial: How to write reusable apps <https://docs.djangoproject.com/en/1.8/intro/reusable-apps/>`_

* 拡張機能を備えるライブラリや、フレームワークにはそれぞれの流儀があるのでそれに従う方が良いでしょう。

便利サービス
=====================================

便利サービス
=====================================

* Pythonパッケージを運用する上で手助けてくれるサービスを紹介します。

* Travis CI
* Coveralls
* Code Climate
* Read The Docs
* Requires.io
* Shields.io

Travis CI
=====================================

* https://travis-ci.org/
* CIサービス
* 複数のPythonのバージョンをサポートしている
* 「tox」で一気にテストを流すたりすることができます。
* 今だと `Circle CI <https://circleci.com/>`_ や `Wercker <http://wercker.com/>`_ などの選択肢もあります。
* 設定ファイル(.travis.yml)を設置します。

.travis.yml例
=====================================

* 「tox」を単純に実行するとどのバージョンで落ちたのかわかりづらい
* matrixを使ってTOXENV渡して個別にtoxを動かすとわかりやすくなる。

::

 language: python
 python: 3.4
 env:
   matrix:
    - TOXENV=py26
    - TOXENV=py27
    - TOXENV=py33
    - TOXENV=py34
    - TOXENV=pypy
    - TOXENV=flake8
 install:
   - pip install tox
   - if test "$TOXENV" = py34 ; then pip install coveralls ; fi
 script: tox
 after_script:
   - if test "$TOXENV" = py34 ; then coveralls ; fi

* 参考: `travisでtoxをつかうtips <http://pelican.aodag.jp/tag/travis.html>`_


Coveralls
=====================================

* https://coveralls.io
* カバレッジを計測してくれるサービスです。

.. image:: _static/images/6n4sok0b.png
   :width: 70%

Coveralls
=====================================

* travisでテスト実行後に取ったカバレッジをcoverallsにPOSTしています

::

 install:
   - pip install tox
   - if test "$TOXENV" = py34 ; then pip install coveralls ; fi
 script: tox
 after_script:
   - if test "$TOXENV" = py34 ; then coveralls ; fi


Code Climate
=====================================

* https://codeclimate.com
* コードの品質をチェックしてくれます。
* 去年までPython未対応でしたが、対応されました。やりましたね。
* リファクタリング本に載ってるような内容を指摘してくれます。

.. image:: _static/images/phbb_i4h.png
   

Code Climate
=====================================

.. image:: _static/images/qkkl6cdq.png
   :width: 80%

Read The Docs
=====================================

* https://readthedocs.org/
* Sphinxドキュメントをホスティングしてくれます。
* PyPIではなくこちらにドキュメントをホスティングするライブラリは多いです
* バージョン管理もしてくれる

.. image:: _static/images/to6rlori.png
   :width: 80%

Requires.io
=====================================

* https://requires.io/
* 依存パッケージの更新チェックをしてくれます。
* 「setup.py」 だけではなく 「requirements.txt」 や 「tox.ini」 なども同時にチェックしてくれます。

Requires.io
=====================================

.. image:: _static/images/vvbm341_.png
   :width: 80%

Sheilds.io
=====================================

* http://shields.io/
* PyPIのみならずいろんなバッジを用意してくれる。
* パッケージのメタデータを読み取ってくれる。

.. image:: _static/images/d1iqgbwa.png
   :width: 80%

トラブルシューティング
=====================================

トラブルシューティング
=====================================

* まちがってアップロードした!
* 一度消したらバージョン番号が再利用できない!
* 説明文(reST)がちゃんとレンダリングされてない!

まちがってアップロードした!
=====================================

* PyPiの管理画面から削除できることができます。

.. image:: _static/images/by6w58ku.png
   :width: 80%

一度消したら同じバージョン番号が使えない！
==========================================

* そういう仕様らしいです。。。
* 諦めましょう。別のバージョン番号をつけるとかにしましょう。

.. image:: _static/images/oibkxoxp.png
   :width: 30%

説明文がレンダリングされていない!
=====================================

* reSTとしてうまく認識されてないケース
* 直さずに放置されていると残念。
* PyPiの管理画面から更新できます。

.. image:: _static/images/0-myl_qn.png
   :width: 50%


今日話さなかった事
=====================================

* C拡張を伴うようなパッケージ 
* インストーラーを伴うようなパッケージ
* クローズドな環境でのPythonパッケージの活用

参考URL
===============================

Python Packaging Authority
    https://www.pypa.io/en/latest/

PEP Summaries
    https://www.pypa.io/en/latest/peps/

Python Packaging User Guide
    https://python-packaging-user-guide.readthedocs.org/en/latest/

vinta/awesome-python
    https://github.com/vinta/awesome-python

PyPIデビュー
    http://www.freia.jp/taka/docs/pyhack4/pypi/

PyPIデビュー
    http://note.crohaco.net/2014/pypi-debut/


参考URL
===============================

PyPIにパッケージ登録する
    http://qiita.com/edvakf@github/items/d82cd7ab77ea2b88506c

How To Package Your Python Code
    http://python-packaging.readthedocs.org/en/latest/index.html

Sharing Your Labor of Love: PyPI Quick and Dirty
    https://hynek.me/articles/sharing-your-labor-of-love-pypi-quick-and-dirty/

Python: PyPIにパッケージをアップロードする最新の推奨な方法
    http://elicon.blog57.fc2.com/blog-entry-422.html

Windows での Python 2.7/3.4 の拡張モジュールビルド環境
    http://qiita.com/methane/items/2210712763b91e75fdf0

パッケージングの今
    http://www.slideshare.net/aodag/ss-39068785

パッケージングの今と未来
    http://www.slideshare.net/aodag/ss-26183017

まとめ
===============================

* 長々と書きましたが、全てを最初からやる必要はありません。
* PyPI にデビューすれば、パッケージンングについて自然と学び始められます。
* testpypi を利用すれば、誰に迷惑をかけることなく何度も試せます。
* 是非試しみてください。

.. image:: _static/images/m4naltmy.png


Special Thanks
===============================

* 突然のレビュー依頼にも関わらず、快くご対応くださりありがとうございます。
* @shimizukawa 氏
* @crohaco 氏 
* 参考資料の作者の皆様

ご静聴ありがとうとございました
====================================

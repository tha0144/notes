# Pythonをexeファイルに変換する

サードパーティが配布するパッケージ <a target="_blank" href="https://github.com/pyinstaller/pyinstaller/releases" alt="Pyinstallerリリースページ">Pyinstaller</a> を使う。

1. まずサードパーティ製パッケージを管理するツール __pip__ をインストール  
    [こちらの記事](https://www.python-izm.com/tips/pip/){:target="_blank"}などを参照
   1. まずコマンドプロンプトで
        ```command
        python -m pip -V
        ```
        で pip のバージョンを確認（インストールされていればバージョンが表示される）。  
   2. インストールされていなければ、[こっち](https://bootstrap.pypa.io/get-pip.py)から __get_pip.py__ をダウンロード、コマンドプロンプトで
        ```
        python get-pip.py
        ```
        を実行。
    3. 【番外】インストール済みのパッケージ一覧を表示する場合、
        ```
        python -m pip list
        ```
        を、特定のパッケージがインストールされているかを確認する場合は
        ```
        python -m pip freeze |grep packageName
        ```
        を実行。
2. pip を使ってパッケージをインストールする。  
    具体的には、コマンドプロンプトで
    ```
    pip install packageName
    ```
    または
    ```
    pip install 'packageName==varsion'
    ```
    とする（後者はパッケージのバージョンを指定する場合）。
3. パッケージをアップグレードする場合、
    ```
    pip install --upgrade packageName
    ```
    とする。  
    `packageName`として`pip`とすると、pip自身のアップグレードもできる。
4. アンインストールする場合は
    ```
    pip uninstall packageName
    ```
5. 本題（やっとかよ）  
    Pythonプログラムをexeファイルに変換するためには、Pyinstallerをインストールし、 __変換したいファイルが存在するディレクトリで__
    ```
    pyinstaller filename.py --onefile
    ```
    をコマンドプロンプトで実行するだけ。  
    コマンドを実行すると、実行時のカレントディレクトリの __dist__ ディレクトリ配下にexeファイルが生成される。  
    オプションの`--onefile`はexeファイル1つにまとめるためのもの。  
    これがないと、dist配下に実行に必要な種々のファイルが生成され、exeファイル単体では動作しなくなる。
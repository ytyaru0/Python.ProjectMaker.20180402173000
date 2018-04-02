# このソフトウェアについて

プロジェクト一式を作成する。

# 目的

コードを書くとき、`src`, `res`, `test`, `lib`, のようなディレクトリ構造をつくることがある。お決まりなのに毎回作成するのは面倒なので。

# 使い方

ヘルプ表示。
```sh
python3 ProjectMaker.py
```

`/tmp/work/flow/do`配下ファイルを`src`とする。
```sh
python3 ProjectMaker.py y
python3 ProjectMaker.py do
```

指定する。
```sh
python3 ProjectMaker.py {path} {ext} {category1} {category2} {category3} ... -{dirname} -{filename}
```

出力ディレクトリ名は`{lang}.{日時}`。`lang`は`ext`のフルネーム版。もし引数があれば`{lang}.{dirname}.{日時}`とする。

## 位置引数

i|略|意味
-|--|----
0|{path}|出力先ディレクトリ
1|{ext}|対象ファイルタイプ
2..|{category}|テンプレートタイプ。順序は階層をあわらす
2..|-{...}|テンプレートの引数。{category}以降にあり、`-`が先頭につく。

### {ext}

* py, sh, md, js, html, css, cs, ...

拡張子。プログラミング言語。バージョンによる言語の違いもある。どうするか。

### {category}

#### {category1}

* py
    * test, HTTP, DB, Server, ...
* html
    * index.html, css/, js/

##### py/test

* /
    * src/
        * {{filename}}.py
    * test/
        * {{filename}}Test.py

```python
class {{filename}}:
    def __init__(self):
        pass
```
```python
import sys, pathlib
sys.path.append(pathlib.Path(__file__).parent.parent / 'src')
from {{filename}} import {{filename}}
import unittest
class {{filename}}Test(unittest.TestCase):
    def test_init(self):
        ins = {{filename}}()
        self.assertEqual({{filename}}, type(ins))
    def test_raise(self):
        with self.assertRaises(Exception) as e:
            raise Exception('A')
        self.assertEqual('A', e.exception.args[0])

if __name__ == '__main__':
    unittest.main()
```

`pathlib`を使うことからPython3.4以上。

実行コマンドは以下。

```sh
python3 {{dirpath}}/test/{{filename}}Test.py
```

どんな場合でも単体テストはあるので、これがpyの基本。

##### py/db/sqlite

* /
    * res/
        * {{filename}}.sqlite3
    * src/
        * database/
            * {{filename}}/
                * {{filename}}Initializer.py
                * sql/
                * tsv/
            * framework/
                * DbInitializer.py
                * DbTransacter.py
    * test/
        * {{filename}}Test.py

内容は未検討、未実装。

##### py/server/html

* /
    * res/
        * db/
            * {{filename}}.sqlite3
        * html/
            * index.html
        * css/
            * style.css
        * js/
        * md/
    * src/
        * server.py
        * database/
            * {{filename}}/
                * {{filename}}Initializer.py
                * sql/
                * tsv/
            * framework/
                * DbInitializer.py
                * DbTransacter.py
    * test/
        * {{filename}}Test.py

HttpServer。テストとDBは基本。

##### html/blog

* Html.{Title}.{datetime}/
    * css/
        * style.css
    * html/
    * js/
    * md/
    * index.html

ほかにも以下のように多様な形式がありうる。

* Q&A
* F&Q
* api-reference
* book
* novel
* poem
* memo
* code-tips
* app

#### コマンドと対応ファイルの例

コマンド|対応ファイル
--------|------------
`py`|py/3/context/ui/c/helloworld.py
`py2`|py/2/context/ui/c/helloworld.py
`py cui`|py/3/context/ui/c/main.py
`py cui args`|py/3/context/ui/c/args.py
`py cui main`|py/3/context/ui/c/main.py
`py cui parse`|py/3/context/ui/c/parse.py
`py gui`|py/3/context/ui/g/tk/helloworld.py
`py gui tk`|py/3/context/ui/g/tk/helloworld.py
`py gui tk button`|py/3/context/ui/g/tk/button.py
`py gui tk entry`|py/3/context/ui/g/tk/entry.py
`py db`|py/3/context/db/sqlite/mapper.py
`py db sqlite`|py/3/context/db/sqlite/sqlite.py
`py db dataset`|py/3/context/db/sqlite/mapper.py
`py http`|py/3/context/http/helloworld.py
`py http wrapper`|py/3/context/http/wrapper.py
`py http scrape`|py/3/context/http/scrape/helloworld.py
`py http server`|py/3/context/server/simple/
`py http server cgi`|py/3/context/server/cgi/
`py http server api`|py/3/context/server/api/
`py http server`|py/3/context/server/simple/helloworld.sh
`py syntax`|/py/3/syntax/class.py
`py syntax class`|/py/3/syntax/class.py
`py designpattern`|py/3/designpattern/singleton.py
`py singleton`|py/3/designpattern/singleton.py
`py test`|py/3/context/test/test.py

# 開発環境

* [Raspberry Pi](https://ja.wikipedia.org/wiki/Raspberry_Pi) 3 Model B
    * [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) GNU/Linux 8.0 (jessie)
        * [pyenv](http://ytyaru.hatenablog.com/entry/2019/01/06/000000)
            * Python 3.6.4

# ライセンス

このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)


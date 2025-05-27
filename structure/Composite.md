# Composite

## 概要
* 個々のオブジェクトと、それらを含むコンテナを同一のインターフェースで扱う。

## メリット
- クライアントコードが、個々の要素と全体構造を区別せずに扱える。
- 構造を柔軟に拡張・変更しやすい。
- 再帰的な処理が自然に記述できる。

## デメリット
- デザインが抽象的になりやすく、構造が複雑になることもある。

## 利用例
- ファイルシステム（フォルダとファイル）
- 組織図（部署と個人）
- 数式や構文木（演算子とオペランド）

## サンプル（Python）

```python
from abc import ABC, abstractmethod

# コンポーネント（共通インターフェース）
class Graphic(ABC):
    @abstractmethod
    def draw(self):
        pass

# リーフ（基本要素）
class Line(Graphic):
    def draw(self):
        print("線を描画")

class Circle(Graphic):
    def draw(self):
        print("円を描画")

# コンポジット（複合要素）
class Picture(Graphic):
    def __init__(self):
        self.children = []

    def add(self, graphic: Graphic):
        self.children.append(graphic)

    def draw(self):
        print("絵を描画開始")
        for child in self.children:
            child.draw()
        print("絵を描画終了")

# 使用例
line = Line()
circle = Circle()
picture = Picture()
picture.add(line)
picture.add(circle)

big_picture = Picture()
big_picture.add(picture)
big_picture.add(Circle())

big_picture.draw()
```

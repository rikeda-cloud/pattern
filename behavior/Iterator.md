# Iterator

## 概要
* コレクションの内部構造を隠し、要素を順番にアクセスする方法を提供する

## メリット
- コレクションの内部構造を隠せる。
- 同じコレクションに対して複数のイテレータ（例えば順方向・逆方向）を用意できる。
- コレクションと走査ロジックを分離できる。

## デメリット
- 設計がやや複雑になる。

## 利用例
- プログラミング言語の標準ライブラリのイテレータ
- ファイルシステムのディレクトリ走査

## サンプル
```python
class Iterator:
    def __init__(self, collection):
        self.collection = collection
        self.index = 0

    def has_next(self):
        return self.index < len(self.collection)

    def next(self):
        item = self.collection[self.index]
        self.index += 1
        return item

# 使い方
items = [1, 2, 3]
iterator = Iterator(items)

while iterator.has_next():
    print(iterator.next())
```

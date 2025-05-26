# Interpreter

## 概要
* 文法ルールをクラス構造で表現し、入力された文字列などの文を解析して意味を実行・評価する仕組みを作る。

## メリット
- 文法をオブジェクト指向的に表現できる。

## デメリット
- 複雑な式を再帰的に解釈するため、実行速度が遅くなることがある。

## 利用例
- データベースのクエリ言語や検索条件の解析。
- カスタムスクリプト言語の実装
- 正規表現のパターン解析

## サンプル
```python
class Number:
    def __init__(self, value):
        self.value = value
    def interpret(self):
        return self.value

class Add:
    def __init__(self, left, right):
        self.left = left
        self.right = right
    def interpret(self):
        return self.left.interpret() + self.right.interpret()

expr = Add(Number(3), Add(Number(5), Number(2)))  # 3 + (5 + 2)
print(expr.interpret())  # 10
```

# Visitor

## 概要
* 処理をデータ構造の外に分離し、あとから自由に追加できる仕組み。

## メリット
- 構造を変更せずに、新しい処理を追加できる。
- 処理ロジックがVisitorにあるため、データクラスは純粋な構造だけを持てる。

## デメリット
- 構造が変わるとすべてのVisitorクラスを修正する必要がある。
- ダブルディスパッチが必要で複雑、そのため、可読性の低下する。

## 利用例
- 構文解析（AST）
- 金融・会計システム

## サンプル
```python
# 要素（Element）クラス群
class Shape:
    def accept(self, visitor):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def accept(self, visitor):
        return visitor.visit_circle(self)

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def accept(self, visitor):
        return visitor.visit_rectangle(self)

# Visitor クラス
class AreaCalculator:
    def visit_circle(self, circle):
        return 3.14 * circle.radius ** 2

    def visit_rectangle(self, rectangle):
        return rectangle.width * rectangle.height

# 利用コード
shapes = [Circle(5), Rectangle(4, 6)]
visitor = AreaCalculator()

for shape in shapes:
    area = shape.accept(visitor)
    print(f"Area: {area}")
```

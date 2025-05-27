# Bridge

## 概要
* 機能の抽象部分と実装部分を分離し、それぞれを独立して拡張可能にする。

## メリット
- 抽象と実装を分離することで、両者を独立して拡張可能。
- クラスの爆発的な増加を防ぎ、変更に強い設計ができる。

## デメリット
- 過剰設計になりやすい。

## 利用例
- デバイスやプラットフォームごとに異なる実装を持つシステム
- データベースの抽象化
- CleanArchitectureのRepository

## サンプル
```python
# 実装部分のインターフェース
class DrawingAPI:
    def draw_circle(self, x, y, radius):
        pass

# 実装1
class DrawingAPI1(DrawingAPI):
    def draw_circle(self, x, y, radius):
        print(f"API1で円を描く: 座標({x},{y}), 半径{radius}")

# 実装2
class DrawingAPI2(DrawingAPI):
    def draw_circle(self, x, y, radius):
        print(f"API2で円を描く: 座標({x},{y}), 半径{radius}")

# 抽象部分
class Shape:
    def __init__(self, drawing_api):
        self.drawing_api = drawing_api

    def draw(self):
        pass

    def resize(self, factor):
        pass

# 具体的な抽象クラス（拡張可能）
class Circle(Shape):
    def __init__(self, x, y, radius, drawing_api):
        super().__init__(drawing_api)
        self.x = x
        self.y = y
        self.radius = radius

    def draw(self):
        self.drawing_api.draw_circle(self.x, self.y, self.radius)

    def resize(self, factor):
        self.radius *= factor

# 使用例
circle1 = Circle(5, 10, 7, DrawingAPI1())
circle2 = Circle(5, 10, 7, DrawingAPI2())

circle1.draw()  # API1で円を描く: 座標(5,10), 半径7
circle2.draw()  # API2で円を描く: 座標(5,10), 半径7

circle1.resize(2)
circle1.draw()  # API1で円を描く: 座標(5,10), 半径14
```

# Prototype

## 概要
* 既存のインスタンスをコピーして新しいインスタンスを生成する

## メリット
- 複製元をもとにしてオブジェクトを生成できるため、生成コストを削減できる。
- サブクラス化せずに新しい型のオブジェクトを生成可能。

## デメリット
- クローン処理の実装が複雑(循環参照、ディープコピー)になりやすい。

## 利用例
- ゲームのキャラクターや敵の生成
- インフラテンプレートの複製
- AIの構成済みモデル構造の複製

## サンプル
```python
import copy

# Prototype クラス
class Shape:
    def clone(self):
        return copy.deepcopy(self)

# ConcretePrototype
class Circle(Shape):
    def __init__(self, radius, color):
        self.radius = radius
        self.color = color

    def draw(self):
        print(f"Drawing Circle: radius={self.radius}, color={self.color}")

# 使用例
original = Circle(10, "red")
clone1 = original.clone()
clone2 = original.clone()

clone1.color = "blue"
clone2.radius = 20

original.draw()  # Drawing Circle: radius=10, color=red
clone1.draw()    # Drawing Circle: radius=10, color=blue
clone2.draw()    # Drawing Circle: radius=20, color=red
```

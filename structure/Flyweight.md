# Flyweight パターン

## 概要
* 共通の状態を１つのインスタンスで使い回し、大量に生成されるオブジェクトのメモリ使用量を削減する。

## メリット
- メモリ使用量が大幅に削減される。
- 一貫性のある共通データを集中管理できる。

## デメリット
- 状態の分離（内部状態／外部状態）が複雑で理解しにくい。
- パフォーマンス向上と引き換えに、コードの柔軟性がやや下がる。
- マルチスレッド環境で状態共有に注意が必要。

## 利用例
- フォントレンダリング（文字ごとにオブジェクトを生成しない）
- グラフィックエンジンでのオブジェクト共有（例：木、兵士などの大量表示）

## サンプル（Python）
```python
class TreeType:
    """内部状態（共有部分）"""
    def __init__(self, name, color, texture):
        self.name = name
        self.color = color
        self.texture = texture

    def draw(self, x, y):
        print(f"Drawing {self.name} tree at ({x},{y}) with color {self.color} and texture {self.texture}")

class TreeFactory:
    """Flyweightの生成と共有を管理"""
    _tree_types = {}

    @staticmethod
    def get_tree_type(name, color, texture):
        key = (name, color, texture)
        if key not in TreeFactory._tree_types:
            TreeFactory._tree_types[key] = TreeType(name, color, texture)
        return TreeFactory._tree_types[key]

class Tree:
    """外部状態（位置）は個別、内部状態（形状）は共有"""
    def __init__(self, x, y, tree_type):
        self.x = x
        self.y = y
        self.type = tree_type

    def draw(self):
        self.type.draw(self.x, self.y)

# 使用例
forest = []
tree_type = TreeFactory.get_tree_type("Pine", "Green", "Rough")
for i in range(10):
    forest.append(Tree(i, i * 2, tree_type))

for tree in forest:
    tree.draw()
```

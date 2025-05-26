# TemplateMethod

## 概要
* 処理の骨組みをスーパークラスで定義し、一部の処理内容はサブクラスに任せる。

## メリット
- 処理の流れを共通化できる。
- コードの再利用性が高まる。

## デメリット
- サブクラスの数が増えやすい
- 処理の流れが固定されるため、柔軟に流れを変えたい場合に不向き。

## 利用例
- Djangoのクラスベースビュー
- テストケースの実行
- データの読み込み→処理→保存の流れを固定し、分析ロジックだけ変えたい場合

## サンプル
```python
from abc import ABC, abstractmethod

# 抽象クラス（テンプレート）
class ReportGenerator(ABC):
    def generate(self):
        self.header()
        self.body()
        self.footer()

    def header(self):
        print("=== Report Start ===")

    @abstractmethod
    def body(self):
        pass

    def footer(self):
        print("=== Report End ===\n")

# 具体クラス1
class SalesReport(ReportGenerator):
    def body(self):
        print("売上レポート：100件の売上データ")

# 具体クラス2
class InventoryReport(ReportGenerator):
    def body(self):
        print("在庫レポート：商品Aが欠品中")

# 実行
sales = SalesReport()
sales.generate()

inventory = InventoryReport()
inventory.generate()
```

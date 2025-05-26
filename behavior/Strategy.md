# Strategy

## 概要
* アルゴリズムをカプセル化し、それを実行時に切り替え可能にする

## メリット
- アルゴリズムの切り替えが簡単で、コードの拡張性・保守性が向上する。

## デメリット
- クラスが増える

## 利用例
- ソートアルゴリズムの切り替え
- 画像の圧縮アルゴリズムの切り替え
- 支払い方法の切り替え
- ストレージ基盤の切り替え

## サンプル
```python
from abc import ABC, abstractmethod

# Strategyインターフェース
class TaxStrategy(ABC):
    @abstractmethod
    def calculate(self, amount):
        pass

class JapanTax(TaxStrategy):
    def calculate(self, amount):
        return amount * 1.1

class USTax(TaxStrategy):
    def calculate(self, amount):
        return amount * 1.07

class NoTax(TaxStrategy):
    def calculate(self, amount):
        return amount

# Context
class ShoppingCart:
    def __init__(self, strategy: TaxStrategy):
        self.strategy = strategy

    def checkout(self, amount):
        total = self.strategy.calculate(amount)
        print(f"税込金額: {total:.2f}円")

# 利用例
cart = ShoppingCart(JapanTax())
cart.checkout(1000)  # → 税込金額: 1100.00円

cart.strategy = USTax()
cart.checkout(1000)  # → 税込金額: 1070.00円

cart.strategy = NoTax()
cart.checkout(1000)  # → 税込金額: 1000.00円
```

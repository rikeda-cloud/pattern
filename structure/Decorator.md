# Decorator パターン

## 概要
* 既存のオブジェクトに対して動的に機能を追加できる構造で、継承を使わず、オブジェクトのラップによって振る舞いを拡張する。

## メリット
- 継承よりも柔軟に機能追加ができる。
- 組み合わせによって多様な機能構成を作れる。

## デメリット
- 多重ラップによる可視性低下でデバッグが難しくなる。
- 設計がやや抽象的になり、初心者には理解しづらい。
- デコレータ間の順序依存があるとバグの原因になりやすい。

## 利用例
- ロギング、認証、キャッシュの付与
- Webフレームワークのミドルウェア

## サンプル（Python）
```python
from abc import ABC, abstractmethod

# コンポーネント（共通インターフェース）
class Notifier(ABC):
    @abstractmethod
    def send(self, message: str):
        pass

# 具体コンポーネント
class EmailNotifier(Notifier):
    def send(self, message: str):
        print(f"Email: {message}")

# デコレータの基本クラス
class NotifierDecorator(Notifier):
    def __init__(self, wrapped: Notifier):
        self._wrapped = wrapped

    def send(self, message: str):
        self._wrapped.send(message)

# 追加機能A：SMS通知
class SMSDecorator(NotifierDecorator):
    def send(self, message: str):
        self._wrapped.send(message)
        print(f"SMS: {message}")

# 追加機能B：Slack通知
class SlackDecorator(NotifierDecorator):
    def send(self, message: str):
        self._wrapped.send(message)
        print(f"Slack: {message}")

# 利用例
notifier = EmailNotifier()
notifier = SMSDecorator(notifier)
notifier = SlackDecorator(notifier)

notifier.send("サーバがダウンしました")
```

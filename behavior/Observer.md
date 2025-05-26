# Observer

## 概要
* あるオブジェクトの状態が変化したときに、関連する複数のオブジェクトに自動で通知を送る仕組み。

## メリット
- 通知処理と通知管理を分離できる。
- 結合を切れる。

## デメリット
- デバッグが難しい。
- 過剰な通知による性能低下。

## 利用例
-  GUIイベント処理
- サーバー監視システム

## サンプル
```python
# イベントバス (Subjectの役割)
class EventBus:
    def __init__(self):
        self._subscribers = {}

    def subscribe(self, event_type, handler):
        if event_type not in self._subscribers:
            self._subscribers[event_type] = []
        self._subscribers[event_type].append(handler)

    def publish(self, event_type, data):
        handlers = self._subscribers.get(event_type, [])
        for handler in handlers:
            handler(data)

# イベントの種類
EVENT_STOCK_PRICE_UPDATED = "stock_price_updated"

# Observer役（購読者）の関数
def display_update(price):
    print(f"[Display] 株価が更新されました: {price}")

def log_update(price):
    print(f"[Logger] 株価のログ記録: {price}")

# 利用例
event_bus = EventBus()

# 購読者登録
event_bus.subscribe(EVENT_STOCK_PRICE_UPDATED, display_update)
event_bus.subscribe(EVENT_STOCK_PRICE_UPDATED, log_update)

# イベント発行（状態変化を通知）
event_bus.publish(EVENT_STOCK_PRICE_UPDATED, 101.7)
event_bus.publish(EVENT_STOCK_PRICE_UPDATED, 102.3)
```

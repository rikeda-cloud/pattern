# Adapter

## 概要
* 既存のクラスのインターフェースを呼び出し側が期待する別のインターフェースに変換する。

## メリット
- 既存のクラスを変更せずに、新しいインターフェースに対応可能。
- レガシーコードや外部ライブラリとの統合が容易になる。

## デメリット
- Adapterクラスの設計・実装が増え、システムが複雑になる。

## 利用例
- 新旧APIの橋渡し
- サードパーティライブラリの異なるインターフェースを既存システムに適合
- 異なるデータフォーマットやプロトコル間の相互変換
- API Gateway
- ORM

## サンプル
```python
# 既存のクラス（旧インターフェース）
class JapanesePlug:
    def connect_to_japanese_socket(self):
        print("Connected to Japanese socket.")

# 新しいインターフェース
class USASocketInterface:
    def connect(self):
        pass

# Adapter
class Adapter(USASocketInterface):
    def __init__(self, japanese_plug):
        self.japanese_plug = japanese_plug

    def connect(self):
        # 既存のメソッドを新インターフェースに適合
        self.japanese_plug.connect_to_japanese_socket()

# 使用例
japanese_plug = JapanesePlug()
adapter = Adapter(japanese_plug)
adapter.connect()  # Output: Connected to Japanese socket.
```

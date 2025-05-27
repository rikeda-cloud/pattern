# Proxy

## 概要
* 本物のオブジェクトへのアクセスをコントロールするための代理オブジェクトを用意する。

## メリット
- 本物のオブジェクトの生成・処理を遅延（遅延初期化）が可能。
- 本物のオブジェクトをキャッシュ・ロギング・監視などで拡張可能。
- ネットワーク越しのリモートアクセスを抽象化可能。

## デメリット
- システム構造が複雑になる。
- 本物のオブジェクトをラップするため、処理コストが増える場合がある。

## 利用例
- アクセス制御（Protection Proxy）
- 遅延初期化（Virtual Proxy）
- ネットワーク越し呼び出し（Remote Proxy）
- 処理の差し込み（Smart Proxy）
- 高速化／再利用（Cache Proxy）

## サンプル（Python）
```python
from abc import ABC, abstractmethod

# Subject インターフェース
class Image(ABC):
    @abstractmethod
    def display(self):
        pass

# RealSubject（本物のオブジェクト）
class RealImage(Image):
    def __init__(self, filename):
        self.filename = filename
        self.load_from_disk()

    def load_from_disk(self):
        print(f"Loading {self.filename} from disk...")

    def display(self):
        print(f"Displaying {self.filename}")

# Proxy（代理オブジェクト）
class ProxyImage(Image):
    def __init__(self, filename):
        self.filename = filename
        self.real_image = None

    def display(self):
        if self.real_image is None:
            self.real_image = RealImage(self.filename)
        self.real_image.display()
```

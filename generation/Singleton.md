# Singleton

## 概要
* インスタンスを1つだけ生成し、どこからでもアクセスできるようにする。

## メリット
- どこからでも同じインスタンスを使える。
- リソースの無駄な生成を防止できる。
- インスタンスが1つであることを保証できるため、状態の整合性を保てる。

## デメリット
- シングルトンインスタンスが変更されると、システム全体に影響を与える可能性がある。
- テストが難しくなる。
- 並列処理やマルチスレッド環境では、スレッドセーフな実装が必要。

## 利用例
- アプリケーション全体で共有される設定ファイル
- ログ出力の一元管理
- DB接続管理
- キャッシュ管理
- Vaultサーバ(環境変数や秘密情報の管理などの一元化)

## サンプル
```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:  # 1回だけ実行される
            print("Creating new instance")
            cls._instance = super().__new__(cls)
        return cls._instance

# 使用例
obj1 = Singleton()
obj2 = Singleton()

print(obj1 is obj2)  # True
```

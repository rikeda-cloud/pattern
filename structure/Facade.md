# Facade パターン

## 概要
* 複雑なサブシステム群に対する統一された窓口を提供する。


## メリット
- クライアントが複雑な内部構造を知らなくて済むため、システムの使用が簡単になる。
- サブシステムを変更しても、Facadeがインターフェースを隠蔽することで影響を最小化できる。

## デメリット
- Facadeが肥大化するとモノリス化する恐れがある。
- 柔軟性や詳細な操作性はやや制限される。

## 利用例
- オーケストレーションパターンのオーケストレーター
- ライブラリやAPIのラッパー（OpenCVなど）
- ビルドツール（`make`, `webpack` などが内部を抽象化）

## サンプル（Python）
```python
# サブシステムA
class CPU:
    def freeze(self):
        print("CPU: freeze")

    def jump(self, position):
        print(f"CPU: jump to {position}")

    def execute(self):
        print("CPU: execute")

# サブシステムB
class Memory:
    def load(self, position, data):
        print(f"Memory: load {data} at {position}")

# サブシステムC
class HardDrive:
    def read(self, sector):
        print(f"HardDrive: read sector {sector}")
        return f"data_from_sector_{sector}"

# Facade
class Computer:
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.hard_drive = HardDrive()

    def start(self):
        print("=== Starting computer ===")
        self.cpu.freeze()
        data = self.hard_drive.read(123)
        self.memory.load(0, data)
        self.cpu.jump(0)
        self.cpu.execute()
```

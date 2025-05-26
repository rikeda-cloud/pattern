# Memento

## 概要
* オブジェクトの状態を外部に保存し、後でその状態を復元できるようにする。Commandパターンと機能が類似するが、状態そのものを保存するのが特徴。

## メリット
- Undo/Redoの実装が簡単。
- オブジェクトの内部状態を外部に見せずに記録・復元できる。

## デメリット
- 状態の記録にメモリを大量に必要とする。
- 保存頻度やタイミングによって、パフォーマンスに影響する。

## 利用例
- フォームの入力の途中保存・復元
- バージョン管理システム
- 仮想マシンのスナップショット

## サンプル
```python
# Memento（状態を保存するクラス）
class Memento:
    def __init__(self, state: str):
        self._state = state

    def get_state(self) -> str:
        return self._state

# Originator（状態を持つオブジェクト）
class TextEditor:
    def __init__(self):
        self._content = ""

    def write(self, text: str):
        self._content += text

    def save(self) -> Memento:
        return Memento(self._content)

    def restore(self, memento: Memento):
        self._content = memento.get_state()

    def __str__(self):
        return self._content

# Caretaker（Mementoを管理）
class History:
    def __init__(self):
        self._history = []

    def push(self, memento: Memento):
        self._history.append(memento)

    def pop(self) -> Memento:
        return self._history.pop() if self._history else None

# 利用例
editor = TextEditor()
history = History()

editor.write("Hello, ")
history.push(editor.save())  # 状態保存

editor.write("World!")
print(editor)  # Hello, World!

# Undo操作
memento = history.pop()
if memento:
    editor.restore(memento)
print(editor)  # Hello, 
```

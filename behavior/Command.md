# Command

## 概要
* 操作をオブジェクトとして扱えるようにする。

## メリット
- 処理の実行、履歴管理やUndoを実装しやすい。
- 新しくコマンドを追加するときに新しいクラスを作成するだけで拡張可能。

## デメリット
- 単純な処理にこのパターンを適用すると必要以上に複雑になる。

## 利用例
- ターン制ゲームのリプレイ機能
- CLIツール
- マイクロサービスの補償トランザクション

## サンプル
```python
# 受け手 (Receiver)
class Light:
    def on(self):
        print("ライトがONになった")
    def off(self):
        print("ライトがOFFになった")

# コマンドのインターフェース
class Command:
    def execute(self): pass
    def undo(self): pass

# 具体的コマンド
class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.on()
    def undo(self):
        self.light.off()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.off()
    def undo(self):
        self.light.on()

# インボーカー
class RemoteControl:
    def __init__(self):
        self.history = []

    def press(self, command):
        command.execute()
        self.history.append(command)

    def press_undo(self):
        if self.history:
            command = self.history.pop()
            command.undo()

# 動作確認
light = Light()
remote = RemoteControl()

remote.press(LightOnCommand(light))   # ライトがONになった
remote.press(LightOffCommand(light))  # ライトがOFFになった
remote.press_undo()                    # ライトがONになった (最後の操作取り消し)
remote.press_undo()                    # ライトがOFFになった (その前の操作取り消し)
```

# Factory Method

## 概要
* オブジェクトの生成処理をサブクラスに委譲。

## メリット
- 新しい製品クラスを追加しても、既存コードを変更せずに対応できる。
- オブジェクト生成のカプセル化により、再利用性や保守性が向上する。
- インスタンス化のロジックを一元化し、サブクラスによる切り替えが容易になる。

## デメリット
- クラス数が増えるため、小規模なシステムでは冗長になる可能性がある。

## 利用例
- 異なるフォーマットのドキュメントを動的に生成。
- OSごとに異なるUIパーツを生成。
- ログの出力先（ファイル、コンソール、リモートサーバ）を切り替える。
- プラグインアーキテクチャで、外部から提供されるモジュールの動的生成。

## サンプル
```python
# Product（製品）
class Document:
    def open(self): pass

# ConcreteProduct（具体製品）
class PDFDocument(Document):
    def open(self):
        print("Opening PDF Document")

class WordDocument(Document):
    def open(self):
        print("Opening Word Document")

# Creator（生成者）
class Application:
    def create_document(self):  # Factory Method
        pass

    def open_document(self):
        doc = self.create_document()
        doc.open()

# ConcreteCreator（具体生成者）
class PDFApplication(Application):
    def create_document(self):
        return PDFDocument()

class WordApplication(Application):
    def create_document(self):
        return WordDocument()

# 使用例
pdf_app = PDFApplication()
pdf_app.open_document()  # => Opening PDF Document

word_app = WordApplication()
word_app.open_document()  # => Opening Word Document
```

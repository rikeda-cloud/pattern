# Builder

## 概要
* 複雑なオブジェクトを構築手順と部品の組み立てを分離し、柔軟に構成できるようにする。

## メリット
- 同じ構築手順でも、部品を変えることで異なる製品を生成可能
- 複雑な構築ロジックを分離できる

## デメリット
- 構築が簡単なものに使うと冗長になる

## 利用例
- フォームやUIの構築
- ゲームキャラクターの生成
- データベースクエリ構築

## サンプル
```python
# Product
class HTMLDocument:
    def __init__(self):
        self.content = []

    def add(self, line):
        self.content.append(line)

    def render(self):
        return "\n".join(self.content)

# Builder
class HTMLBuilder:
    def __init__(self):
        self.doc = HTMLDocument()

    def add_title(self, title):
        self.doc.add(f"<h1>{title}</h1>")

    def add_paragraph(self, text):
        self.doc.add(f"<p>{text}</p>")

    def add_list(self, items):
        self.doc.add("<ul>")
        for item in items:
            self.doc.add(f"<li>{item}</li>")
        self.doc.add("</ul>")

    def get_result(self):
        return self.doc

# Director
class HTMLDirector:
    def __init__(self, builder):
        self.builder = builder

    def build_simple_page(self):
        self.builder.add_title("Sample Page")
        self.builder.add_paragraph("This is a sample paragraph.")
        self.builder.add_list(["Item 1", "Item 2", "Item 3"])

# 使用例
builder = HTMLBuilder()
director = HTMLDirector(builder)
director.build_simple_page()
document = builder.get_result()

print(document.render())
```

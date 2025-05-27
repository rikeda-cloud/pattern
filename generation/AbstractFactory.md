# AbstructFactory

## 概要
* 具象クラスに依存せずに、関連オブジェクトのファミリーを生成できるようにすること。

## メリット
- クライアントコードが具象クラスに依存せず、インターフェース経由で使用できる。
- 新しい製品群を追加しても、既存コードを変更せずに対応できる。

## デメリット
- 抽象クラスや具体的なファクトリ・製品の数が増え、構造が複雑になる。

## 利用例
- ゲームのキャラクター装備
- 通知システム
- データベースドライバ

## サンプル
```python
# 抽象製品
class Connection:
    def connect(self): pass

class QueryBuilder:
    def build_query(self): pass

# 具体製品（MySQL）
class MySQLConnection(Connection):
    def connect(self):
        print("Connecting to MySQL")

class MySQLQueryBuilder(QueryBuilder):
    def build_query(self):
        print("Building MySQL query")

# 具体製品（PostgreSQL）
class PostgresConnection(Connection):
    def connect(self):
        print("Connecting to PostgreSQL")

class PostgresQueryBuilder(QueryBuilder):
    def build_query(self):
        print("Building PostgreSQL query")

# 抽象ファクトリ
class DatabaseFactory:
    def create_connection(self): pass
    def create_query_builder(self): pass

# 具体ファクトリ
class MySQLFactory(DatabaseFactory):
    def create_connection(self):
        return MySQLConnection()
    def create_query_builder(self):
        return MySQLQueryBuilder()

class PostgresFactory(DatabaseFactory):
    def create_connection(self):
        return PostgresConnection()
    def create_query_builder(self):
        return PostgresQueryBuilder()

# クライアント
def run(factory: DatabaseFactory):
    conn = factory.create_connection()
    query = factory.create_query_builder()
    conn.connect()
    query.build_query()

# 使用例
run(MySQLFactory())
run(PostgresFactory())
```

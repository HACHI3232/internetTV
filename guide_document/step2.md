## STEP2: テーブルの構築

1.ターミナルを開きRoot権限を持つユーザーで MySQL へ接続

```jsx
mysql -u[ユーザー名] -p
```

2.新しいデータベースを作成するために、以下のコマンドを実行

```sql
CREATE DATABASE internet_tv;
```

3.データベースが作成されたことを確認

```sql
SHOW DATABASES;
```

4.作成したデータベースに切り替える

```sql
USE internet_tv;
```

****ステップ2: テーブルの構築****

例として、Channel テーブルとProgramテーブルのクエリを記載しています。

```sql
-- Creating Channel Table
CREATE TABLE Channel (
  id BIGINT NOT NULL AUTO_INCREMENT,
  channel_name VARCHAR(100) NOT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE Program (
  id BIGINT NOT NULL AUTO_INCREMENT,
  program_title VARCHAR(100) NOT NULL,
  program_details VARCHAR(200) NOT NULL,
  PRIMARY KEY (id)
);
```

channelテーブルとProgramテーブルが作成されているか確認

```sql
mysql> SHOW TABLES;
+-----------------------+
| Tables_in_internet_tv |
+-----------------------+
| Channel               |
| Program               |
+-----------------------+
2 rows in set (0.00 sec)
```

channelテーブルとProgramテーブルのカラムが挿入されているか確認
```sql
-- カラムの確認
DESCRIBE テーブル名;

```

```sql
mysql> DESCRIBE Channel;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | bigint       | NO   | PRI | NULL    | auto_increment |
| channel_name | varchar(100) | NO   |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
2 rows in set (0.01 sec)

mysql> DESCRIBE Program;
+-----------------+--------------+------+-----+---------+----------------+
| Field           | Type         | Null | Key | Default | Extra          |
+-----------------+--------------+------+-----+---------+----------------+
| id              | bigint       | NO   | PRI | NULL    | auto_increment |
| program_title   | varchar(100) | NO   |     | NULL    |                |
| program_details | varchar(200) | NO   |     | NULL    |                |
+-----------------+--------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

### チャレンジ

[テーブル設計](database_design/table_design.md)を開いて下記のサンプルデータを実際に打ち込んで入れてみましょう。

Seasons Table,Episodes Table,Genres Table,ProgramSlots Table,ViewCounts Table,ProgramGenres Table

全てのテーブルが作成されたか見てみましょう。下記のようになるはずです。
※Seqel SceなどのMySQL のクライアントツールを仕様して確認する事も可能です。


```sql
-- テーブル一覧の確認
SHOW TABLES;
```

```sql
mysql> SHOW TABLES;
+-----------------------+
| Tables_in_internet_tv |
+-----------------------+
| Channel               |
| Episode               |
| Genre                 |
| Program               |
| ProgramGenre          |
| ProgramSlot           |
| Season                |
| ViewCount             |
+-----------------------+
8 rows in set (0.00 sec)
```

テーブルの構築ができましたね！[STEP3](guide_document/step3.md)でサンプルデータを挿入していきましょう！

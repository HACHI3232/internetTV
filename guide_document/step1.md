## STEP1: データベースの作成

では、データベースの構築から初めていきましょう！


1.ターミナルを開きRoot権限を持つユーザーで MySQL へ接続

```sql
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
Database changedと出れば切り替え完了です！

[STEP2](Guide Document/step2.md)へ進みましょう！

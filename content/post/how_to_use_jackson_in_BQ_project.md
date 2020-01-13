---
title: "Bigquery と Dataflow の備忘録（随時更新）"
date: 2020-01-13T05:21:56+09:00
draft: false
---

### Bigquery と Dataflow の備忘録（随時更新）
####  やることリスト
- BQから特定のスキーマをjsonに出力する。
- スキーマjsonでパーティションテーブルを作成する
- BQの日時の取り込みパーティションに対して、任意の日付でデータを入れる。
- jacksonを使用してDataflowで上記の抜いてきたスキーマjsonを読み込ませて加工して、BQに挿入する。

---

##### BQから特定のスキーマをjsonに出力する。
BQから特手のテーブルのスキーマファイルを抜く方法は下記である  
> bq show --schema --format=prettyjson [PROJECT_ID]:[DATASET].[TABLE] > [SCHEMA_FILE]

参考元：https://stackoverflow.com/questions/43195143/is-there-a-way-to-export-a-bigquery-tables-schema-as-json

注意点はformat指定が普通のjsonだと階層式になってくれない。

---

##### スキーマjsonでパーティションテーブルを作成する
> bq mk --time_partitioning_type=DAY --table [DATASET].[TABLE] [SCHEMA_FILE]  
> 例 : bq mk --time_partitioning_type=DAY --table 'jp_data_set.jp_table_sub_secound' .\jp_table_schema.json

 
取り込み型パーティション（日ごと）でスキーマはjsonファイルを使って作成する。  


---

##### BQの日時の取り込みパーティションに対して、任意の日付でデータを入れる。

> bq load --source_format=NEWLINE_DELIMITED_JSON '[DATASET].[TABLE]$[YYYYMMDD]' [DATA_FILE]  
> 例 : bq load --source_format=NEWLINE_DELIMITED_JSON  'data_set.table_name$20010101' .\table_data.json .\table_schema.json

YYYYMMDDの日にデータを挿入する。

※別のテーブル移動する場合の例
> 例 : bq query --use_legacy_sql=false --destination_table 'data_set.table_name$20010101' 'SELECT * FROM jp_data_set.jp_table_subsub';
---

##### jacksonを使用してDataflowで上記の抜いてきたスキーマjsonを読み込ませて加工して、BQに挿入する。
resorucesにスキーマjsonを入れて、アウトプットの時のテーブルスキーマとして使用する。

https://github.com/machitomo/bq_to_bq_dataflow_smaple

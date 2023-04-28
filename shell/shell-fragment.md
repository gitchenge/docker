#### 扫描表里可能的敏感字段

```sql
-- 设置要查找的数据库名
SET @database_name = 'database';
-- 设置要查找的表（使用'|'分隔）
SET @table_name_pattern = 'table_1|table_2';
-- 设置要查找的字段名（使用'|'分隔）
SET @field_name_pattern = 'field_1|field_2';

-- 查询匹配的表和字段
SELECT
  TABLE_SCHEMA,
  TABLE_NAME,
  GROUP_CONCAT(COLUMN_NAME) COLUMNS
FROM
  INFORMATION_SCHEMA.COLUMNS
WHERE
  TABLE_SCHEMA = @database_name
  AND TABLE_NAME REGEXP @table_name_pattern
  AND COLUMN_NAME REGEXP @field_name_pattern
GROUP BY TABLE_SCHEMA, TABLE_NAME;
```

#### 提取出所有用到的表

```shell
find . -name "*.xml" -type f -exec pcregrep -ioM "(from|join)\s+\S+" {} \; \
| sed "s/\`//g; s/from//Ig; s/join//Ig; s/ //g; s/\t//g; s/)//g; /(/d" \
| awk 'NF' | sort -t '.' -k 2 | uniq > tables.txt
```

```shell
find . -name "*.xml" -type f -exec pcregrep -ioM "(from|join)\s+\S+" {} \; \
| sed "s/\`//g; s/from//Ig; s/join//Ig; s/ //g; s/\t//g; s/)//g; /(/d" \
| awk 'NF' | sort -t '.' -k 2 | uniq | grep -v '\.' | tr '\n' ',' > table_names.txt
```

```sql
SET @db_name = 'database';
SET @table_names = 'table1,table2,table3';

SELECT table_name, TRIM(table_comment) AS table_comment
FROM information_schema.tables
WHERE table_schema = @db_name AND FIND_IN_SET(table_name, @table_names)
```
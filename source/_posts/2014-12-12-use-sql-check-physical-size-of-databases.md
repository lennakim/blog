title: sql查询某个数据库个个表占用的空间大小
date: 2014-12-12 17:57:25
tags: sql database
---

如图

```
+-----------------------+---------+
| Table                 | MB      |
+-----------------------+---------+
| account_versions      | 2752.97 |
| fund_sources          |    0.20 |
| id_documents          |    0.41 |
| identities            |    1.52 |
| members               |    1.52 |
| orders                | 1355.75 |
| partial_trees         |  671.02 |
| payment_addresses     |    1.88 |
| tips                  |    0.02 |
| tokens                |    2.89 |
| trades                |  229.94 |
| two_factors           |    0.48 |
| versions              |   46.08 |
| withdraws             |    1.52 |
+-----------------------+---------+

```

sql语句如下:

``` sql
SELECT table_name AS "Tables",
round(((data_length + index_length) / 1024 / 1024), 2) "Size in MB"
FROM information_schema.TABLES
WHERE table_schema = "<DB_NAME>"
ORDER BY (data_length + index_length) DESC;
```

把 DB_NAME替换成需要查询的数据库名即可, 应该只适用于 Mysql / MariaDB.
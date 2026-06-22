#### **第1关：创建数据表**

题目描述：

创建客商表 gk，表结构如下：

* **hyh** (会员号): `varchar(4)`，主键
* **name** (姓名): `varchar(10)`，不能为空
* **sex** (性别): `varchar(1)`
* **tel** (电话号码): `varchar(11)`，值唯一
* **dept** (部门): `varchar(20)`，不能为空

**参考答案：**

**SQL**

```
create table gk (
    hyh varchar(4) primary key,
    name varchar(10) not null,
    sex varchar(1),
    tel varchar(11) unique,
    dept varchar(20) not null
);
```

---

#### **第2关：数据表结构修改**

题目描述：

打开 sale 数据库，对 gzry (工作人员数据表) 执行以下操作：

1. 在数据表 `gzry` 增加奖金字段：`jj`，`int` 型。
2. 在数据表 `gzry` 修改员工姓名字段 (`gyxm`) 类型为：`varchar(20)`。
3. 在数据表 `gzry` 删除学历 (`xl`) 字段。

**参考答案：**

**SQL**

```
alter table gzry add jj int;
alter table gzry modify gyxm varchar(20);
alter table gzry drop column xl;
```

---

#### **第3关：数据记录修改**

**题目描述：**

1. **插入数据：** 在 `gzry` 表插入一条数据：
   * 姓名: 陈林, 出生日期: 1975-1-1, 学历: 研究生, 工资: 3000, 部门: 办公室。
2. **修改数据：** 修改 `gzry` 数据表，将**销售部**工作的所有员工工资增加 200 元。
3. **删除数据：** 删除 `gzry` 数据表中**学历为初中**的所有员工。

**参考答案：**

**SQL**

```
-- 第一题：插入数据
insert into gzry(gyxm, csrq, xl, gz, bm) values('陈林', '1975-01-01', '研究生', 3000, '办公室');

-- 第二题：修改工资
update gzry set gz = gz + 200 where bm = '销售部';

-- 第三题：删除初中学历员工
delete from gzry where xl = '初中';
```

---

#### **第4关：数据查询一 (基础查询)**

题目描述：

查询工作人员数据表 (gzry) 中销售部 (bm) 员工的姓名 (gyxm) 和 工资 (gz)，按工资降序排列。

**参考答案：**

**SQL**

```
select gyxm, gz
from gzry
where bm = '销售部'
order by gz desc;
```

---

#### **第5关：数据查询二 (分组统计)**

题目描述：

查询各部门 (bm) 名称、部门的人数 (列名为rs) 和 工资 (gz) 的和 (列名为gzh)，按工资和 (gzh) 降序排列。

**参考答案：**

**SQL**

```
select bm, count(*) as rs, sum(gz) as gzh
from gzry
group by bm
order by gzh desc;
```

---

#### **第6关：数据查询三 (多表连接)**

题目描述：

根据销售单 xsd 和工作人员 gzry 数据表查询：

员工姓名 (gyxm) 和每个员工对应的实际付款 (sjfk) 总金额 (命名为zje)。

* 只显示总金额**小于 10000** 的数据。
* 按总金额 (`zje`) **降序**排列。

**参考答案：**

**SQL**

```
select t2.gyxm, sum(t1.sjfk) as zje
from xsd t1, gzry t2
where t1.gyh = t2.gyh
group by t2.gyxm
having zje < 10000
order by zje desc;
```

---

#### **第7关：数据查询四 (子查询/排除)**

题目描述：

根据销售单 xsd 和顾客 gk 数据表，查询没有任何销售单的顾客名 (name) 和电话 (tel)。

**参考答案：**

**SQL**

```
select name, tel
from gk
where hyh not in (
    select distinct hyh
    from xsd
);
```

---

#### **第8关：创建视图**

题目描述：

建立视图 gzry_view，显示销售部的员工工号 (gyh)、员工姓名 (gyxm)、学历 (xl)、工资 (gz) 和电话 (dh)。

**参考答案：**

**SQL**

```
create view gzry_view as
select gyh, gyxm, xl, gz, dh
from gzry
where bm = '销售部';
```

---

**提示：** 考试时请注意标点符号必须是英文半角状态，SQL语句末尾建议加上分号 `;`。祝你考试顺利！

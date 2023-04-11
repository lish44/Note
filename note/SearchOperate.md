### 查询操作
--------
### student表
| id  | name | gender | score | class |
| :-: | :-:  | :-:    | :-:   | :-:   |
| 1   | 小明 | F      | 90    | 1     |
| 2   | 小红 | M      | 85    | 1     |
| 3   | 小黄 | F      | 75    | 2     |
| 4   | 小黑 | F      | 70    | 2     |
|     |      |        |       |       |

--------

查询所有记录

`select * from xx;`

--------


查单列或多列字段记录

`select k1, k2 from xx;` - - k1 k2 想查询的字段 xx 表

--------


条件查询 

支持 `>` `<` `>=` `<=` `=` `!=` - - opt


`select * from score where k opt condition;` - - k 字段 opt 操作 condition 条件

还支持`and` `or` `not` 与 或 非 

分数在70~90的人: `select * from student where score > 70 and score < 90;` 或者`select * form student where score between 70 and 90;`

除开女生并且是1班的: `select * form student where not gender = 'F' and class = 1;`


--------

排序

默认升序 降序加desc：`select * from student order by score desc;`

--------
new ↓

`<>` 不等于
```sql
select t.name, i.identity_num
from student t
join identity i
on t.id = i.id
where t.city <> '杭州';
```

### 操作封成api (CREATE PROCEDURE)

> 创建存储过程。存储过程是一种封装了一系列SQL语句和控制语句的程序，可以被多次调用，提高了SQL语句的复用性和可维护性。

```sql
CREATE PROCEDURE calc(IN a INT, IN b INT, OUT c INT)
BEGIN
   SET c = a + b;
END
```
- IN 就是输入
- OUT 就是输出

```sql
SET @a = 1;
SET @b = 2;
CALL calc(@a, @b, @c);
SELECT @c;
```

列2：
```sql
CREATE PROCEDURE get_user_by_id (IN user_id INT)
BEGIN
  SELECT * FROM users WHERE id = user_id;
END
```
- 可以通过调用 CALL get_user_by_id(1) 来查询 id 为 1 的用户信息。

### 联表查询

#### 外连接 outer join

**left join** 

数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。 在使用left jion时，on和where条件的区别如下：

1. on条件是在生成临时表时使用的条件，它不管on中的条件是否为真，都会返回左边表中的记录。

2. where条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有left join的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。

**right join** 

原理同上，只不过左右顺序反了



#### 内连接 inner join

--------

### 分组查询
假设有一个学生表格 Student，其中包含了学生的 ID、姓名、性别和年龄信息：

| ID | Name   | Gender | Age |
|----|--------|--------|-----|
| 1  | Alice  | Female | 18  |
| 2  | Bob    | Male   | 20  |
| 3  | Carol  | Female | 19  |
| 4  | David  | Male   | 21  |
| 5  | Emily  | Female | 20  |
| 6  | Frank  | Male   | 19  |
| 7  | Gloria | Female | 18  |
| 8  | Henry  | Male   | 20  |


可以使用以下 SQL 查询语句对学生按照性别进行分组，并统计每个分组中的学生数量和平均年龄：
```sql
SELECT Gender, COUNT(*) AS Count, AVG(Age) AS AvgAge

FROM Student

GROUP BY Gender;
```
执行这个查询语句后，将得到以下结果：

| Gender | Count | AvgAge |
|--------|-------|--------|
| Female | 4     | 19.25  |
| Male   | 4     | 20.25  |

这个结果表示，学生表格中共有 4 个女生和 4 个男生，女生的平均年龄为 19.25 岁，男生的平均年龄为 20.25 岁。这个查询结果可以帮助我们了解不同性别学生的数量和年龄分布情况，从而为学校的招生和教学提供参考。

**其实就是把每组用特定条件计算出来** 
---







# 基本操作

| 操作                   | 指令                                      | 提示                          |
| :-:                    | :-:                                       | :-:                           |
| 开启                   | `mysql.server start`                      |                               |
| 关闭                   | `mysql.server stop`                       |                               |
| 重启                   | `mysql.server restart`                    |                               |
| 连接                   | `mysql -u root -p xx`                     | xx 为密码                     |
| 退出                   | `exit;`                                   |                               |
| 查所有数据库           | `show databases;`                         |                               |
| 创建数据库             | `create database xx`                      | xx 数据库名                   |
| 删除数据库             | `drop database xx`                        | xx 数据库名                   |
| 进入数据库             | `use xx`                                  | xx 数据库名                   |
| 创建数据表             | `create table x1(x2 x3,..);`              | x1 表名 x2 字段名 x3 数据类型 |
|                        | `create tabke school（name VARCHAR(20)）` | [更多约束](#约束)             |
| 查看当前数据库有哪些表 | `show tables;`                            |                               |
| 查看单个表结构         | `desc xx;`                                | xx 表名                       |
| 查看表的信息           | `select * from xx`                        | xx 表名 * 所有字段            |
| 添加字段               | `alter table x1 add x2 x3 `               | 同上                          |
| 插入数据               | `insert into xx values(x1,x2)`            | xx 表名 x1 x2为对应字段       |
|                        |                                           |                               |


### 表的操作
| 操作             | 关键字         | 列句                                  | 提示                                                                                          |
| :-:              | :-:            | :-:                                   | :-:                                                                                           |
| 插入一行数据     | `insert`       | `insert into` xx `values`(v1,v2);     | xx 表名 v1 v2为对应字段值                                                                     |
| 添加字段         | `alter`-`add`  | `alter table` xx `add` k t            | xx表名 k 字段名 t数据类型                                                                     |
| 删一行           | `delete`       | `delete from` xx where k = v;         | xx 表名 k 字段名 v对应值名                                                                    |
| 删整个表         | `drop`         | `drop table` xx;                      | xx 表名                                                                                       |
| 删字段           | `alter`-`drop` | `alter table` xx `drop` k             | xx 表名 k 字段名                                                                              |
| 改某个字段内容   | `update`-`set` | `update` xx `set` k = v where k1 = v1 | xx 表名 k 需要修改的字段名 v 需要修改的内容 k1 需要约束的字段 没有约束k的那一列全部都会被修改 |
| 查看某些字段内容 | `select`       | select k1, k2 from xx                 | xx 表名 k1 字段名 k2 字段名2                                                                  |
|                  |                |                                       |                                                                                               |

删除时字段名相同会被一起删掉


### 约束 
主键

> 其实就是一个唯一ID，（可GUID，可自增）

> 确定一条记录不重复且唯一性 一般id字段来表示[详细介绍传送门](https://www.liaoxuefeng.com/wiki/1177760294764384/1218728391867808)

    给已有的字段添加主键：alter table xx add primary key(k);
    
    修改字段方式添加主键：alter table xx modify k t primary key auto_increment;
    
    删除主键约束：alter table xx drop primary key;
    
    带AUTO_INCREMENT 先去掉再删：alter table xx modify k t; - - k 字段 t 类型
	
联合主键

> 其实就是因为主键不能相同，有时候需要多对多且关系唯一，比如多个老师对多个班级

> 两个或更多的字段都设置为主键

    create table xx (id int, name varchar(10), primary key(id,name));

自增约素
> 自动增长 添加时必须有主键约束
    
    创建：create table xx (id int primary key auto_increment, name varchar); 
    
    添加时不需要手动输入id ：insert into xx (k1,k2) values(v1,v2); 

唯一约束
> 约束修饰的字段的值不可重复
    
    关键字 unique 可以再创建表时添加也可以后面单独添加
    
    单独添加：alter table xx add unique(k);
    
    modify 添加：alter table xx modify k t unique;
    
    删除：alter table xx drop index(k);
    
非空约束
> 字段不能为空

    关键字 not null 创建时可添加
    
默认约束
> 插入字段值没有给值就给默认值
    
    关键字 default v 
    
    create table xx (id int, name varchar(20) not null default v);

外键约束
> 使两个或多个表进行关联
    
    关键语法 foreign key(k) references xx(k1) - - k 为外键将关联到xx表的k1字段 
[更多详细内容](https://www.liaoxuefeng.com/wiki/1177760294764384/1218728424164736) 

### 常用数据类型 
[完整](https://www.runoob.com/mysql/mysql-data-types.html)

+ 整数
    + `INT(4)、FLOAT(4)、DOUBLE(8)`
+ 时间日期
    + `DATE` ex - - 1997-1-7
+ 字符串
    + `CHAR` 定长- -空格空格填充 、`VARCHAR` 变长 

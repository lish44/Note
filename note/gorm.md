### Gorm


### 分页查询

```go
offset := (pageNum - 1) * pageSize
db.Limit(pageSize).Offset(offset).Find(&users)
```
> 通过将页码和每页记录数带入公式计算出偏移量

- pageNum 是当前页码
- pageSize 是每页记录数，就是每页显示多少条数据
- offset 是查询结果的偏移量
 


### 重新更改主键id

> 思路就是新建一个表 把旧数据同步到新表上面去



1. 创建一个新的表，结构和旧表一样，但主键 id 是从 1 开始自增的。
2. 把旧表中的数据插入到新表中，注意插入数据时，需要指定新表的主键 id，可以使用 MySQL 的 set 命令，例如：SET @ID := 0; INSERT INTO new_table(id, name, age, birthday) SELECT (@ID:=@ID+1) AS id, name, age, birthday FROM old_table;
3. 把新表的名字改为旧表的名字。
4. 删除旧表

```go
// 创建一个新的表，结构和旧表一样，但主键 id 是从 1 开始自增的。
db.Exec("CREATE TABLE new_users LIKE users;")
db.Exec("ALTER TABLE new_users MODIFY id bigint unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY;")

// 把旧表中的数据插入到新表中
db.Exec("SET @ID := 0;")
db.Exec("INSERT INTO new_users(id, name, age, birthday) SELECT (@ID:=@ID+1) AS id, name, age, birthday FROM users;")

// 把新表的名字改为旧表的名字
db.Exec("RENAME TABLE users TO old_users, new_users TO users;")

// 删除旧表
db.Exec("DROP TABLE old_users;")

```

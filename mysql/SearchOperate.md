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





注解方式

hibernate.cfg.xml 配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- 数据库连接信息 -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/test</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password"></property>
        <!-- 方言 -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQL5Dialect</property>
        <!-- 自动创建表 -->
        <property name="hibernate.hbm2ddl.auto">update</property>

		<!-- 每次创建一个表就要在这添加索引 -->
        <mapping class="com.game.User" />
        <mapping class="com.game.Grade" />

    </session-factory>
</hibernate-configuration>

```

Grade.class 结构 set get 结构好像是必须的 hibernate 底层要用来初始化?
```java
package com.game;


import javax.persistence.*;

@Entity
@Table(name = "grade")
public class Grade {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "score")
    private double score;

    @ManyToOne(fetch = FetchType.LAZY)// 懒加载模式 表示一个grade对应一个user
    @JoinColumn(name = "user_id")// 关联的字段
    private User user;

    public User getUser() {
        return user;
    }

    public void setUser(User user) {
        this.user = user;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }
}
```

user.class 
```java
package com.game;

import javax.persistence.*;
import java.util.AbstractList;
import java.util.ArrayList;
import java.util.List;

@Entity
@Table(name = "user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "username")
    private String username;

    @Column(name = "password")
    private String password;

    public User(String username, String password) {
        this.username = username;
        this.password = password;
        this.grades = new ArrayList<>(); //用了懒加载 这要先实例化?
    }
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)//
    private List<Grade> grades;


    public void setId(Long id) {
        this.id = id;
    }

    public Long getId() {
        return id;
    }


    public List<Grade> getGrades() {
        return grades;
    }

    public void setGrades(List<Grade> grades) {
        this.grades = grades;
    }
}
```

CascadeType.ALL 表示进行所有级联操作，包括增加、修改、删除等操作。除了 ﻿ALL 外，还有其他级联操作类型，例如：
+ CascadeType.PERSIST：级联新增操作。
+ CascadeType.MERGE：级联修改操作。
+ CascadeType.REMOVE：级联删除操作。
+ CascadeType.REFRESH：级联刷新操作。
+ CascadeType.DETACH：级联分离操作。


test 测试
```java

public class Main {
    public static void main(String[] args) {

        Configuration configuration = new Configuration().configure("hibernate.cfg.xml");
        SessionFactory sessionFactory = configuration.buildSessionFactory();
        Session session = sessionFactory.openSession();
        Transaction tx = null;
        try {
            tx = session.beginTransaction();

            // 创建一个 User 实体并设置属性
            User user = new User("aniu","erccs");

            // 创建一个 Grade 实体并设置属性
            Grade grade = new Grade();
            grade.setScore(90.0);
            grade.setUser(user);

            // 将 Grade 实体添加到 User 实体的 grades 属性中
            user.getGrades().add(grade);

            // 保存 User 实体到数据库中
            session.save(user);

            tx.commit();
        } catch (Exception e) {
            if (tx != null) {
                tx.rollback();
            }
            e.printStackTrace();
        } finally {
            session.close();
        }


```


### getCurrentSession()与openSession()的区别？

在 SessionFactory 启动的时候，Hbernate 会根据配置创建相应的 CurrentSessionContext，在 getCurrentSession( 被调用的时候，实际被执行的方法是CurrentSessionContext.currentSession()。在 currentSession() 执行时，如果当前 Session 为空，currentSession 会调用SessionFactory的openSession。所以getCurrentSession0 对于 Java EE 来说是更好的获取 Session 的方法。

用geCurentSession0创建的session会绑定到当前线程中，而采用openSession0创建的session则不会

采用getCurrentSession()创建的session在commit或rollback时会自动关闭，而采用openSession()创建的session必须手动关闭

使用getCurrentSession0需要在hibernate.cfg. xm/文件中加入如下配置：

如果使用的是本地事务 （jdbc事务）

+ sproperty name='hibernate.current_session_context_class">threade/property>

如果使用的是全局事务 （ita事务）

+ sproperty name="hibernate.current_session_context_class">jtad/property>

如果使用的是session的管理机制（不太常用）

+ sproperty name='hibernate.currentsession_context_class">managed<property>


### 什么是JPA?
相同处：
1. 都跟数据库操作有关，JPA 是JDBC 的升华，升级版。
2. JDBC和JPA都是一组规范接口
3. 都是由SUN官方推出的

不同处：
1. JDBC是由各个关系型数据库实现的， JPA 是由ORM框架实现
2. JDBC 使用SQL语句和数据库通信。JPA用面向对象方式，通过ORM框架来生成SQL，进行操作。
3. JPA在JDBC之上的，JPA也要依赖JDBC才能操作数据库。

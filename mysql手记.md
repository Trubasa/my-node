- 命令行的启动与关闭

    ```bash
        net start mysql
        net stop mysql
        # net start 命令适用于系统注册的所有服务，不一定要是mysql
    ```

- 命令行进入数据库

    ```bash
        # mysql -u[用户名] -P[端口号] -h[ip] -p[密码]
        
        #访问本地3306数据库，后续输入密码
        mysql -uroot -p

        #访问指定ip机器上对应端口的数据库，用户与密码也直接给出
        mysql -uroot -P3303 -h192.168.46.201 -p123456

    ```

- 修改控制台提示符，帮助用户梳理关系

    ```bash
        # 登陆进数据库后输入 prompt [提示符] 
        
        # 设置数据库命令行的提示符为 用户@ip 数据库，这样可以协助用户，减少误操作，另外，\D 完整日期
        prompt /u@/p/d
    ```
- 数据库操作

    ```bash
        # 创建数据库test
        create database test

        # 试用数据库test
        use test

        # 以utf8格式床架那数据库
        create database test character set utf8

        # 修改
        alert database test character set utf8

        # 删除数据库test
        drop database test

        # 查看所有的数据库
        show databases;
    ```

- 表操作

    ```bash
        # 创建表user，id为主键自增，name不能为空，不能重复， age 为正 ，性别默认为3
        create table user(
            id smallint unsigned primary key auto_increment,
            name varchar(20) not null unique key,
            age tinyint unsigned,
            sex ENUM("1","2","3") default 3
        )

        drop table user

        # 显示该数据库所有的表
        show table 
        # 显示数据库test 的表
        show table from  test
    ```

- 字段操作

    ```bash
        # 删除user表的name字段
        alter table user drop column name
    ```

- 行操作

    ```
        insert user(name,age) values("jack",18);

        select * from user
    ```

- 外键约束

    ```bash
        # 插入字段
        alter table user add name varchar(10) not null;

        # 插入约束
        alter table user add foreign key (pid) references provinces (id);

        # provinces 行的删除会导致user这边行的删除 除了cascade，还有set null，restrict等
        alter table user add foreign key (pid) references provinces (id) on delete cascade;

        # 查看表的构建，可以看到外键等约束
        show create table user

        # 移除约束
        alter table user drop foreign key user_ibfk_1;
    ```

---
layout: post
category: 数据库
tags: Linux Postgresql 
description: 在 Debian 下安装 Postgresql 数据库，并记录的常用操作。如： 添加删除用户，添加删除数据库。查询数据库等。
---

### 安装 Postgresql

    sudo apt-get install postgresql

### 连接到 Postgresql
  当使用 apt 包管理器安装时，默认创建了一个 Linux 标准系统用户 postgres。当用户使用此用户名登陆时，就可以管理 postgresql 数据库了

    sudo -u postgres psql postgres
    
### Postgresql 数据库操作
  1. 添加用户，并赋予创建数据库的权限

        create user phonebook with password 'phonebook' createdb;

  2. 创建数据库，并为数据库分配用户和权限

        CREATE DATABASE test_db OWNER tangjiujun;
        GRANT ALL PRIVILEGES ON DATABASE test_db to tangjiujun;
        
  3. \c: 可以通过\c databasename  切换数据库
  4. \l: 数据库列表的详细信息
  5. \d: 该数据库下所有表的详细信息
  6. \dg: 查看系统用户和组分配
  7. 删除数据库

        sudo -u postgres dropdb test_db
        
  8. 删除用户

        sudo -u postgres dropuser tangjiujun

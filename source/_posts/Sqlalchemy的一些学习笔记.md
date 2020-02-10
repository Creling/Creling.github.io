---
title: Sqlalchemy的一些学习笔记
url: 371.html
id: 371
categories:
  - Python
date: 2019-05-06 23:04:47
tags:
---

### Sqlalchemy的正确打开方式

    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, create_engine, Text, Boolean
    from sqlalchemy.orm import sessionmaker
    
    # 首先创建链接
    engine = create_engine(
        &#039;sqlite:///books.db?check_same_thread=False&#039;, echo=False)
    # 依据上文创建的链接初始化一个Session类
    Session = sessionmaker(bind=engine)
    # 创建一个Session类实例
    session = Session()
    
    # 数据库模型的基类
    Base = declarative_base()
    
    class BookDatabase(Base):  # 继承Base类
        __tablename__ = &#039;Books&#039;  # 此模型类对应的表名
    
        id = Column(Integer, primary_key=True, autoincrement=True)  # 主键自增
        bookName = Column(String(40))
        pathString = Column(Text)
        unique=True)  # 唯一性要求
        hasDownload = Column(Boolean, default=False)
    
    Base.metadata.create_all(engine)  # 创建数据库

### query的几种用法

说几点印象深刻的 1.获取某一字段（某一列）的所有值

    session.query(BookDatabase.bookName).all()  # 以上文的BookDatabase类和bookName字段值为例

2.修改某一字段的值

    book.hasDownload = True
    session.commit() 
    # 记得要commit(), 当然，也可以用update()来修改

PS: print(session.query(XXXX))可以看到具体的SQL语句，e.g.

    print(session.query(BookDatabase.bookName))
    output:
    SELECT &quot;Books&quot;.&quot;bookName&quot; AS &quot;Books_bookName&quot; 
    FROM &quot;Books&quot;

一些参考文档 [SQlAlchemy的增删改查](https://www.cnblogs.com/chenxi67/p/10376617.html) [SQLAlchemy技术文档（中文版）（全）](https://blog.csdn.net/Lotfee/article/details/57406450) [Python:数据库操作模块SQLAlchemy](http://blog.sina.com.cn/s/blog_4ddef8f80101g6cl.html)
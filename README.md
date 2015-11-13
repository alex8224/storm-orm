# storm-orm

该项目的来源是 https://storm.canonical.com/Tutorial , 一个Python的ORM框架,本项目基于 storm 0.20　进行的修改, 遵循LGPL 2.1, 这也是storm本身的开源许可

添加了如下功能

1. store.raw_execute 
2. Resulset.fetchall
3. Resultset.fetchone
4. Resulset.get_select_sql

## 目的:
1. 可以继续使用 `Storm` 的表达式构造查询, 通过 raw_execute方法执行SQL语句,　可以使用异步的驱动完成后面的查询

```python
    class User(object):
        __storm_table__ = "user"
        user_id = Int(primary=True)
        username = Unicode()
        age = Int()


    sql, param = store.find(User, User.username==u'alex').get_select_sql()
    ...
    cursor = connection.cursor()
    cursor.execute(sql, param)
    for row in cursor.fetchall():
        #do something on row
        pass
    
```

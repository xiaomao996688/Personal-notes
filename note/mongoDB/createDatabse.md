## 创建数据库语法
```
语法：use DATABASE_NAME
sql
use test_database

```
1. use 创建数据库，如果已经有了就是选择这个数据库
2. db 命令来显示当前的数据库
3. show dbs 显示所有数据库

```
创建成功后向数据库中插入数据
db.test_01.insert({name: 'zll', age:18})
WriteResult({ "nInserted" : 1 })
WriteResult是插入语句后返回的结果
```

## 删除数据库语法
```
语法： db.dropDatabase()
test_01.dropDatabase()
删除当前的数据库，默认为test
注意： 
db.dropDatabase() 是删除当前分支的数据库
成功后返回的是 {"ok":1}
```
## 创建集合
```
语法：db.createCollection('name')
```
1. show tables #show collections

## 删除集合
```
语法：db.collection.drop()
db.test.drop()
执行命令后返回 true

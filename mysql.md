[TOC]

# 下载mysql图形界界面
DBeaver

# node 使用 
```js
// npm i mysql
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost', // 连接地址
  port: '3306', // 端口号
  user     : 'me', // 用户名
  password : 'secret', // 密码
  database : 'my_db' // 数据库名
});

connection.connect((err) => {
    if(err) {
        console.log('----连接失败----',err)
        return 
    }
    console.log(`---连接成功----端口号为:${port}`,connection.threadId)
});

connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});

connection.end();
```

# 新增表
```js
const s = `CREATE TABLE test_test (id INT, name VARCHAR(255), age INT(3), city VARCHAR(255))`

connection.query(s,(error, results, fields) => {})
```
***
# 增
```js
```
***
# 删
```js
```
***
# 改
```js
```
***
# 查
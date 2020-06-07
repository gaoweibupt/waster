## 数据库操作标准库
go语言的标准库也提供了访问关系型数据库的接口 database/sql, 这是典型的桥接模式的实现。<br/>
sql包值提供了sql数据库的泛用接口，实际使用sql包的时候还得注入一个数据库的驱动程序。<br/>
mysql的常用驱动程序是
```
github.com/go-sql-driver/mysql
```
实际操作数据库的入口对象为sql.DB, 主要实现了两个功能:
*  通过驱动程序打开和关闭实际的底层数据库的连接
*  管理数据库连接

## go 操作mysql

#### 1.驱动注册和建立连接

```
    mysqlDB, err = sql.Open("mysql", "root:123456@(127.0.0.1:3306)/payment?charset=utf8")

	// 最大连接数
	mysqlDB.SetMaxOpenConns(100)
	// 闲置连接数
	mysqlDB.SetMaxIdleConns(20)
	// 最大连接周期
	mysqlDB.SetConnMaxLifetime(100 * time.Second)

    mysqlDB.Ping()

```

** 什么是长连接？**

* 短连接: 连接->数据传输->关闭连接
* 长连接

** sql.Open **
函数返回了sql.DB的指针
函数并不会直接建立数据库连接，当第一次进行数据库操作时才真正的建立连接

#### 2.写入数据
```
    mysqlDB.Exec("insert INTO product_order(uid,product_id,pay_amount,create_time,update_time) values(?,?,?,?,?)",
		userID, productID, payAmount, timeUnix, timeUnix)
```

#### 3.查询数据

查询
```
   mysqlDB.Query("SELECT * FROM product_order WHERE uid = ?", userID) 
```

#### 4.更新数据
```
    mysqlDB.Exec("update product_order set pay_status=?, update_time=? where id > ?", status, timeUnix, id)```
```
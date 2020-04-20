# DATABASE

##  nosql(非关系型)

![image-20200304111807812](https://github.com/moodsjinxin/moods/blob/master/images/image-20200304111807812.png)



## mysql

### 数据库引擎

- 作用在表上不同的表可以有不同的引擎

- MYIsam

  - 共有3个文件（结构、数据、索引）
  - 查询索引得到数据地址去数据表中查询数据（需要回表）
  - ![image-20200329095945664](C:\Users\金鑫\AppData\Roaming\Typora\typora-user-images\image-20200329095945664.png)

- Innodb

  - 共2个文件（架构、数据索引）无需回表

  - 叶子结点存放数据，数据以B加树形式存储

  - ![image-20200329100139645](C:\Users\金鑫\AppData\Roaming\Typora\typora-user-images\image-20200329100139645.png)

  - Innodb解决幻读（在可重复读的基础上）

    - MVCC(多版本并发控制)
  
      url ： https://www.jianshu.com/p/133694f3163d
    
      多版本并发控制。InnoDB为每行记录添加了一个版本号（系统版本号），每当修改数据时，版本号加一。
    
      在读取事务开始时，系统会给事务一个当前版本号，事务会读取版本号<=当前版本号的数据，这时就算另一个事务插入一个数据，并立马提交，新插入这条数据的版本号会比读取事务的版本号高，因此读取事务读的数据还是不会变
  
  - 三种锁
    - 记录锁（recored locks） 唯一索引， 为一条记录加锁
    - 间隙所 （GAP LOCK）基于非唯一索引，锁定的是一段区间
    - 临键锁 （next-key lock） 


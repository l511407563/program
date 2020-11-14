#### 目录
[一、查询](#one)
    [基础查询](#one-1)
    [条件查询](#one-2)
    [排序查询](#one-3)
    [常见函数](#one-4)
    [分组函数](#one-5)
    [分组查询](#one-6)
    [连接查询](#one-7)
    [子查询](#one-8)
    [分页查询](#one-9)
    [union联合查询](#one-10)
    
[二、增删改](#two)
    [插入语句](#two-1)
    [修改语句](#two-2)
    [删除语句](#two-3)

[三、约束](#three)
    [库和表的管理](#three-1)
    [常见数据类型介绍](#three-2)
    [常见约束](#three-3)
    [标识列](#three-4)

[四、事务](#four)
    [事务和事务处理](#four-1)

[五、视图](#five)

[六、存储过程](#six)

[七、流程控制](#seven)

[八、MySQL简介](#eight)

[九、存储引擎](#nine)

[十、索引](#ten)

[十一、性能分析前提知识](#eleven)

[十二、explain](#twelve)

[十三、索引优化](#thirteen)

[十四、锁](#fourteen)

[十五、主从复制](#fifteen)

#### <h3 id="one">一、查询</h3>

<h5 id="one-1">基础查询</h5>
```
    语法：
    select 查询列表 from 表名;
    
    特点：
        1、查询列表可以是: 表中的字段、常量值、表达式、函数
        2、查询的结果是一个虚拟的表格、临时性

    #1.查询单个字段
    select 字段名 from 表名;

    #2.查询多个字段
    select 字段名1,字段名2,字段名3 from 表名;

    #3.查询所有字段 
    select * from 表名;

    #4.着重号``
    select name from 表名;
    select `name` from 表名;
    上下两个语句相等，``只是为了区别里面的name是表里的字段还是关键字，增强可读性

    #5.查询常量值
    select 100;
    select 'john';
    mysql中没有字符串，只有字符型

    #6.查询表达式
    select 100*100;

    #7.查询函数
    select VERSION();

    #8.起别名
    // 使用AS
    select 100%98 AS "结果";
    select last_name AS "姓", first_name AS "名" from 表名;
    // 使用空格
    select last_name 姓, first_name 名 from 表名;
    优点：
        1.方便别人理解，提高可读性
        2.可以区分查询字段重名的情况

    #9.去重(DISTINCT)
    select distinct userName from 表名;

    #10.+号的作用
    只能作为运算符，不能作为连接符
    select '100'+90; 如果两边都可以转换成数值，则继续计算，190
    select 'abc'+90; 如果转换不了，就计为0计算，90
    select null+90;  如果有null，就为null， NULL

    #11.拼接符(CONCAT)
    select concat('a','b','c') AS '结果';
```

<h5 id="one-2">条件查询</h5>
```
    语法：
    select 查询列表 from 表名 where 筛选条件;

    分类：
        一、按条件表达式筛选
        二、按逻辑运算符筛选
        三、模糊查询
            like(包含)
                1. 查询字段name中所有包含'王'的数据(%为通配符)
                select * from tables where `name` like '%王%';
                2. 查询字段name中第二个字符为'五'的数据(占位符_)
                select * from tables where `name` like '_五%';
                3. 查询字段name中第二个字符为下划线_的数据(转义字符\)
                select * from tables where `name` like '_\_%';
                4. 查询字段name中第二个字符为下划线_的数据(使用ESCAPE自定义转义字符$)
                select * from tables where `name` like '_$_%' escape '$';

            between and(在什么和什么之间)
                查询id为3到10之间的数据
                select * from tables where id between 3 and 10;
                注：
                    1. 包含3，10 [3,10]
                    2. 不能倒序 

            in(代替或)
                查询id为4或5或6的数据
                select * from tables where id=4 or id=5 or id=6;
                select * from tables where id in(4,5,6);

            is null()
                查询所有数据为null的数据(IS NULL)
                select * from tables where is null;
                查询所有数据不为null的数据(IS NOT NULL)
                select * from tables where is not null;
                安全等于(<=>)
                select * from tables where <=>null;
                不等于(<>)
                select * from tables where <>null;
        
```

<h5 id="one-3">排序查询</h5>
```
    语法：
        select 查询列表 from 表名 where 筛选条件 order by 排序列表 【asc|desc】;
        order by: 根据什么排序
        asc: 升序
        desc: 降序

```

<h5 id="one-4">常见函数</h5>
```
    语法：
        select 函数名(实参列表) 【from 表名】 where 筛选条件;

    分类：
        单行函数
            1.1 字符函数
                #length 获取参数值的字节个数
                #concat 拼接字符
                #upper  转换大写
                #lower  转换小写
                #substr、substring  截取字符
                #instr  返回子串在主串的初始索引,找不到返回0
                #trim   去字符的前后的指定字符
                #lpad   用指定的字符，进行左边填充指定长度
                #rpad   用指定的字符，进行右边填充指定长度
                #replace    替换
            1.2 数学函数
                #round  四舍五入
                #ceil   向上取整
                #floor  向下取整
                #truncate   截断
                #mod    取余
            1.3 日期函数
                #now    返回当前系统日期+时间
                #curdate    返回当前系统日期，不包含时间
                #curtime    返回当前时间，不包含日期
                #year(now()) 获取指定的部分,年、月、日、时、分、秒
                #str_to_date('1999-8-8','%Y-%c-%d') str_to_date('4-3 1992','%c-%d %Y') 将字符通过指定的格式转换成日期
                #date_format(now(), '%y年%m月%d日') 将日期转换成字符
            1.4 其他函数
            1.5 流程控制函数
                #if(提交表达式, success, error)  if(10<5, '大', '小')
                #case
```

<h5 id="one-5">分组函数</h5>
```
    分组函数
        功能：做统计使用
            #sum 求和
            #avg 平均值
            #max 最大值
            #min 最小值
            #count 计算个数
```

<h5 id="one-6">分组查询</h5>
```
    语法：
        select 函数名(实参列表) 【from 表名】 where 筛选条件 【group by子句】;

    SELECT sum(salary) 和, round(avg(salary),2) 平均,max(salary) 最高,min(salary) 最低,count(salary) 个数 
    FROM tables;
            特点：
                1.sum和avg一般用于处理数值型数据; max、min、count可以处理任何类型
                2.sum、avg、max、min、count都忽略null值
                3.可以和distinct搭配实现去重
                    #查询 去重数据之和 和 未去重数据之和
                    select sum(distinct salary),sum(salary) from tables;
                4.count函数详细介绍
                    #统计表的行数(只要行内有一个字段的值不为null就会统计)
                    select count(*) from tables;
                    #统计表的行数(实际上是每行加一个1,并统计行数)
                    select count(1) from tables;
                    效率：
                        MYISAM存储引擎下，count(*)的效率高，因为引擎自带计数器
                        INNODB存储引擎下，count(*)和count(1)效率差不多，比count(字段)高
                        所以一般默认使用 count(*) 来统计行数
                5.和分组函数一同查询的字段要求是group by后的字段
            
            #案例1：查询每个工种的最高工资
                SELECT MAX(salary), joy_id 
                FROM tables 
                GROUP BY job_id;
            
            #案例2：查询每个位置上的部门个数
                SELECT COUNT(*), location_id 
                FROM tables 
                GROUP BY location_id;

            #案例3：查询邮箱中包含a字符的，每个部门的平均工资
                SELECT AVG(salary),department_id 
                FROM tables 
                WHERE email LIKE '%a%' 
                GROUP BY department_id;

            #案例4：查询有奖金的每个领导手下员工的最高工资
                SELECT MAX(salary),manager_id 
                FROM tables 
                WHERE commission_pct IS NOT NULL
                GROUP BY manager_id;

            #案例5：查询哪个部门的员工个数>2
            #第一步：查询每个部门的员工个数
                SELECT COUNT(*),department_id 
                FROM tables 
                GROUP BY department_id;
            #第二步：根据第一步的结果进行筛选，查询哪个部门的员工个数>2
            #添加分组后的筛选 having
                SELECT COUNT(*),department_id 
                FROM tables 
                GROUP BY department_id 
                HAVING count(*)>2;

            #案例6：查询每个工种有奖金的(commission_pct)员工的最高工资>12000的工种编号和最高工资
            #第一步：查询每个工种有奖金的员工的最高工资
                SELECT MAX(salary),job_id 
                FROM tables 
                GROUP BY job_id;
            #第二步：根据第一步的结果进行筛选，查询>12000的工种编号和最高工资
                SELECT MAX(salary),job_id 
                FROM tables
                WHERE commission_pct IS NOT NULL
                GROUP BY job_id
                HAVING MAX(salary)>12000;
            
            分组筛选特点:
                1.分组前筛选
                    数据源：原始表
                    位置：gourp by子句 的前面
                    连接关键字：where

                2.分组后筛选
                    数据源：分组后的结果集
                    位置：gourp by子句 的后面
                    连接关键字：having

                3.分组函数做条件肯定放在having子句中，因为原始表肯定没有分组函数

                4.优先使用分组前筛选，性能更好

                5.排序放在整个查询语句的最后
```

<h5 id="one-7">连接查询</h5>
```
    含义：多表查询，查询字段来自多个表
    语法：
        select 字段1,字段2 from tables1, tables2;
    
    笛卡尔乘积现象：表1有m行，表2有n行，结果=m*n行
    发生原因：没有有效的连接条件
    如何避免：添加有效的连接条件

    SELECT `name`,`boyName`
    FROM tables1,tables2
    WHERE tables1.boyfriend_id=tables2.id;

    分类：
        按年代分类：
            sq192标准(mysql仅支持内连接)
            sq199标准【标准】：支持所有内连接，外连接(mysql中不支持全外连接)，交叉连接
        按功能分类：
            内连接：
                等值连接
                非等值连接
                自连接
            外连接：
                左外连接
                右外连接
                全外连接
            交叉连接

    一、sq192标准
        #1.等值连接
        #案例1：查询女名和对应的男名
            SELECT `name`,`boyName`
            FROM tables1,tables2
            WHERE tables1.boyfriend_id=tables2.id;

        #2.非等值连接
        #案例1：查询员工的工资和工资级别
            SELECT salary,level
            FROM tables1 e,tables2 g
            WHERE salary BETWEEN g.`lowest_sal`=g.`highest_sal`;

        #3.自连接
        #案例1：查询 员工名和上级名称
            SELECT e.id1,e.id2,g.id1,g.id2
            FROM tables1 e,tables2 g
            WHERE e.`id1`=e.`id2`;

    
    二、sq199标准
        语法：
            select 查询列表
            from 表1 别名【连接类型】
            join 表2 别名
            on 连接条件
            【where 筛选条件】
            【group by 分组】
            【having 筛选条件】
            【order by 排序列表】

        连接类型分类：
            内连接：inner
            外连接：
                左外连接：left【outer】
                右外连接：right【outer】
                全外连接：full【outer】
            交叉连接：cross
        
        #内连接
        语法：
            select 查询列表
            from 表1 别名
            inner join 表2 别名
            on 连接条件;

        #外连接
        语法：




```

<h5 id="one-8">子查询</h5>
```
    含义：出现在其他语句(增删查改)中的select语句，成为子查询或者内查询
        外部的的查询称为主查询或者外查询

    分类：
        按子查询出现的位置：
            select后面
                仅仅支持标量子查询
            from后面
                支持表子查询
            where或having后面
                标量子查询(单行)  子查询返回一个结果(比如返回一个人名)
                列子查询(多行)    子查询返回多个结果(比如返回多个人名)
                    列子查询常用操作符：
                        IN/NOT_IN 等于列表中的任意一个
                        ANY|SOME  和子查询返回的某一个值比较
                        ALL       和子查询返回的所有值比较
                行子查询    子查询返回多个字段的值，公用一个判断条件(比如返回最大工资和最小工资)
            exists后面(相关子查询)
                支持表子查询  子查询返回1或者0
        按功能(结果集的行列数不同)：
            标量子查询(结果集只有一行一列)
            列子查询(结果集只有一列多行)
            行子查询(结果集有一行多列)
            表子查询(结果集一般为多行多列)


```

<h5 id="one-9">分页查询</h5>
```
    语法：
        select 查询列表
        from 表
        【join type join 表2
        on 连接条件
        where 筛选条件
        group by 分组字段
        having 分组后的筛选
        order by 排序的字段】
        limit 【pageNo】,pageSize;

        pageNo分页的起始索引(起始索引从0开始)
        pageSize分页的每页条数

        SELECT *
        FROM tables
        LIMIT 0,5;
```

<h5 id="one-10">union联合查询</h5>
```
    含义：将多条查询语句的结果合并成一个结果
    场景：要查询的结果来自多个表，且多个表没有直接的连接关系，但查询的信息一致时
    语法：
        查询语句1
        UNION
        查询语句2
        UNION
        ...

    特点：
        1.要求多条查询语句的查询列数是一致的
        2.要求多条查询语句的查询的每一列的类型和顺序最好一致
        3.UNION 关键字自动去重。UNION ALL 关键字不去重
```

#### <h3 id="two">二、增删改</h3>

<h5 id="two-1">插入语句</h5>
```
    语法：
    方式一：
    插入单行
    INSERT INTO 表名(列名1,列名2,...)
    VALUES(值1,值2,...);

    插入多行
    INSERT INTO 表名(列名1,列名2,...)
    VALUES(值1,值2,...)
    ,(值1,值2,...)
    ,(值1,值2,...),
    ,...;

    支持子查询
    INSERT INTO 表名(name,age)
    SELECT '张三',19;
    
    方式二：
    只支持插入单行，不支持插入多行和子查询
    INSERT INTO 表名
    SET 列名1=值,列名2=值,...;

    特点：
        1.插入的值的类型要与列的类型一致或兼容(可进行类型转换)
        2.varchar、char、datetime等值要加单引号或者双引号
        3.不可以为NULL的列必须插入值，可以为NULL的列如何插入值?
            方式一：插入NULL
            方式二：不写列，也不写字段
        4.列数和值的个数必须一致
        5.可以省略列名，默认所有列
```

<h5 id="two-2">修改语句</h5>
```
    1.修改单表中的记录：
    语法：
    UPDATE 表名
    SET 列=新值,列=新值,...
    WHERE 筛选条件;

    2.修改多表中的记录：
    sq192语法：
    UPDATE 表1 别名,表2 别名
    SET 列=值,...
    WHERE 连接条件
    AND 筛选条件;

    sq199语法：
    UPDATE 表1 别名
    INNER|LEFT|RIGHT JOIN 表2 别名
    ON 连接条件
    SET 列=值,...
    WHERE 筛选条件;

```

<h5 id="two-3">删除语句</h5>
```
    语法：
    删除方式一：delete
    1.单表删除
    DELETE FROM 表名 WHERE 筛选条件;
    2.多表删除

    删除方式二：truncate
    直接删除整张表
    TRUNCATE TABLE 表名;

```

#### <h3 id="three">三、约束</h3>

<h5 id="three-1">库和表的管理</h5>
```
    一、库的管理
    创建、修改、删除

    二、表的管理
    创建、修改、删除

    创建：create
    修改：alter
    删除：drop

    表的复制
    #1.仅仅复制表的结构
    CREATE TABLE 新表 LIKE 旧表

    #2.复制表的结构+数据
    CREATE TABLE 新表 
    SELECT * FROM 旧表;

    #3.只复制部分数据
    CREATE TABLE 新表
    SELECT 要复制的列
    FROM 旧表
    WHERE 条件;
```

<h5 id="three-2">常见数据类型介绍</h5>

实际开发，所选择的类型越简单越好，能保存数值的类型越小越好

一、整型
整数类型|字节|范围
----|----|----
Tinyint|1|  
Smallint|2|  
Mediumint|3|  
Int、integer|4|  
Bigint|8|  

```
    #1.如何设置有符号和无符号
    INT 默认有符号
    INT UNSIGNED 设置无符号

    #2.如果插入的数值超出范围，会报out of range异常，并且插入临界值

    #3.如果不设置长度，会有默认的长度

    #4.ZEROFILL 0填充，并且自动添加 UNSIGNED
```
    
    
    
    

二、浮点型(小数)
浮点数类型|字节|范围
----|----|----
float|4|  
double|8|  

定点数类型|字节|范围
----|----|----
DEC(M,D) <br> DECIMAL(M,D)|M + 2|  

```
    1.浮点型
        float(M,D)
        double(M,D)

    2.定点型
        DEC(M,D)
        DECIMAL(M,D)

    特点:
        1.M和D
        M：整数部位+小数部位
        D：小数部位
        如果超过范围，则插入临界值

        2.M和D都可以省略
        如果是decimal，则M默认为10，D默认为0
        如果是float和double，则会根据插入的数值的精度来决定精度

        3.定点型的精确度较高，如果要求插入数值的精度较高如货币运算等则考虑使用
```

三、字符型
字符串类型|M的意思|特点|空间的耗费|效率
----|----|----|----|----
char(M)|最大的字符数，可以省略，默认为1|固定长度的字符|比较耗费|高
varchar(M)|最大的字符数，不可以省略|可变长度的字符|比较节省|低

```
    较短的文本: char、varchar
    较短的二进制: binary、varbinary
    枚举值: enum
    集合: set
    较长的文本: text、blob(较长的二进制)
```

四、日期型
日期和时间类型|字节|最小值|最大值|范围
----|----|----|----|----|----
date|4|1000-01-01|9999-12-31|只保存日期
datetime|8|1000-01-01 00:00:00|9999-12-31 23:59:59|保存日期+时间
timestamp|4|19700101080001|2038年的某个时刻|保存日期+时间
time|3|-838:59:59|838:59:59|只保存时间
year|1|1901|2155|只保存年

```
    特点：
    #1.datetime
        字节：8
        范围：1000-9999
        不受时区影响

    #2.timestamp
        字节：4
        范围：1970-2038
        受时区影响

    #3.设置时区
        SHOW VARIABLES LIKE 'time_zone';
        SET time_zone='+9:00';  // 东9区，+8:00东八区

```

<h5 id="three-3">常见约束</h5>
```
    含义：用于限制表中的数据，为了保证表中的数据的准确性和可靠性
    CREATE TABLE 表名(
        字段名 字段类型 列级约束
        表级约束
    )

    表记约束语法：
        1.写在各个字段的最下面
        2.【constraint 约束名】 约束类型(字段名)

    分类：六大约束
        1.NOT NULL: 非空，用于保证该字段的值不能为空
        比如姓名、学号等
        2.DEFAULT: 默认，用于保证该字段的值有默认值
        比如性别
        3.PRIMARY KEY: 主键，用于保证该字段的值具有唯一性，并且非空
        比如学号、员工编号等
        4.UNIQUE: 唯一，用于保证该字段的值具有唯一性，可以为空
        比如座位号
        5.CHECK: 检查约束【mysql中不支持】
        6.FOREIGN KEY: 外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值

    约束的添加分类：
        列级约束：
            只支持默认、非空、主键、唯一
            列级约束只能应用在一列上

        表级约束：
            只支持主键、唯一、外键
            表级约束可以应用在多列上

    例：
        CREATE TABLE 表名(
            id INT PRIMARY KEY, #主键
            seat INT,
            majorid INT,
            CONSTRAINT uq UNIQUE(seat), #唯一键
            #major(id) 当前从表的majorid字段受到 主表major表的字段id的限制
            CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id), #外键
        )

    主键和唯一的区别：
                保证唯一性      是否允许为空        一个表中可以有多个      是否允许组合
        主键        唯一           非空                 0或1个            是，但不推荐
        唯一        唯一           可以为空             任意个            是，但不推荐

    外键的特点：
        1.要求在从表设置外键关系
        2.从表的外键列的类型和从表的外键列的类型一致或者兼容，名称无要求
        3.主表的关联列必须是一个key(一般是主键或者唯一)
        4.插入数据时，先插入主表，再插入从表
        5.删除数据时，先删除从表，再删除主表
    
```

<h5 id="three-4">标识列</h5>
``` 
    又称自增长列
    含义：可以不用手动的插入值，系统提供默认的序列值
    关键字：auto_increment
    语法：
        CREATE TABLE 表名(
            id INT PRIMARY KEY AUTO_INCREMENT,
        )
    特点：
        1.标识列不必须和主键搭配，但要求是一个key(主键，唯一)
        2.一个表最多只有一个标识列
        3.标识列的类型只能是数值型
        4.标识列可以通过 SET auto_increment_increment=3; 设置步长(每次增长的数值)
            也可以通过手动插入值，设置起始值

```

#### <h3 id="four">四、事务</h3>

<h5 id="four-1">事务和事务处理</h5>
```
    事务：
        一个或一组相互依赖的sql语句组成一个执行单元，这个执行单元要么全部执行，要么全部不执行。

    回滚：
        所有受到影响的数据返回到事务开始以前的状态。

    存储引擎对事务的支持：
        mysql5.5版本以上使用innoDB存储引擎，支持事务

    事务的acid属性
        1.原子性(Atomicity)
            一个事务不可在分割，要么都执行，要么都不执行
        2.一致性(Consistency)
            一个事务会使数据从一个一致性状态转变到另外一个一致性状态
        3.隔离性(Isolation)
            一个事务的执行不受其他事务干扰(即事务内部操作的数据对并发的事务是隔离的)
            隔离性需要隔离级别处理
        4.持久性(Durability)
            一个事务一旦提交，则会永久的改变数据库的数据

    事务的使用步骤
        隐式事务：事务没有明显的开启和结束的标记
        比如insert、update、delete语句

        显示事务：事务具有明显的开启和结束的标记
        前提：必须先设置(insert、update、delete等语句)自动提交功能为禁用
        禁用自动提交功能：set autocommit=0;

        注意：在一些mysql客户端工具中，例如DBeaver客户端，执行事务需要开启 允许多条提交 "allowMultiQueries", 否则执行多条语句的时候会报错
        编辑连接 ---> 连接设置 ---> 驱动属性 ---> allowMultiQueries 改为 true

        步骤1：开启事务
            set autocommit=0;
            start transaction;(可选的)
        步骤2：编写事务中的sql语句(select insert update delete)
            语句1;
            语句2;
            ...
        步骤3：结束事务
            commit; 提交事务
            rollback; 回滚事务

    事务的并发问题
        同时运行多个事务时，当这些事务访问数据库中相同的数据时，如果没有隔离，就会导致各种并发问题；
        1.脏读(读取之后数据回滚)：对于两个事务T1，T2，T1读取了T2更新但是没有提交的数据，如果T2回滚了，T1读取的就是临时且无效的。
        2.不可重复读(读取之后数据更新)：对于两个事务T1，T2，T1读取了一个字段，然后T2更新了该字段，之后，T1再次读取同一个字段，值就不同了。
        3.幻读(读取之后数据新增)：对于两个事务T1，T2，T1从一个表中读取了一个字段，T2向表中插入新数据，T1再次读取同一个表，就会多出几行。

    事务的隔离级别
                                        脏读                不可重复读              幻读
        读未提交数据(read uncommitted)   可以                   可以                 可以 
        读已提交数据(read committed)     不可以                 可以                 可以
        可重复读(repeatable read)        不可以                 不可以               可以
        串行化(serializable)             不可以                不可以                不可以

    mysql的默认隔离级别：可重复读(repeatable read) 
    orcle默认隔离级别：读已提交数据(read committed)

    查看mysql的隔离级别
        select @@tx_isolation;

    设置mysql的隔离级别
        set session|global transaction isolation level 隔离级别

    设置回滚保存点
    savepoint 节点名; 
    回滚点后面执行的sql语句都回滚，回滚点前的sql语句无法回滚
    例：
    savepoint a; #这是保存点a
    rollback to a; #回滚到保存点a

    delete和truncate在事务使用时的区别
        delete可以回滚
        truncate回滚无效

```

#### <h3 id="five">五、视图</h3>
```
    含义：常用的且比较复杂的sql查询语句的公共部分的提取封装
    语法：
        CREATE VIEW (

        )

    视图和表的区别
            关键字      是否实际占用物理空间           使用     
    视图    view            无(只保存sql逻辑)       增删改查

    表      table           有(保存数据)            增删改查
```

#### <h3 id="six">六、存储过程</h3>
```

```

#### <h3 id="seven">七、流程控制</h3>
```

```

#### <h3 id="eight">八、MySQL简介</h3>
```

```

#### <h3 id="nine">九、存储引擎</h3>
```

```

#### <h3 id="ten">十、索引</h3>
```

```

#### <h3 id="eleven">十一、性能分析前提知识</h3>
```

```

#### <h3 id="twelve">十二、explain</h3>
```

```

#### <h3 id="thirteen">十三、索引优化</h3>
```

```

#### <h3 id="fourteen">十四、锁</h3>
```

```

#### <h3 id="fifteen">十五、主从复制</h3>
```

```
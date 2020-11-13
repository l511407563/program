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
    插入语句
    修改语句
    删除语句

[三、约束](#three)
    库和表的管理
    常见数据类型介绍
    常见约束

[四、事务](#four)
    事务和事务处理

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

<h4 id="one-1">基础查询</h4>
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

<h4 id="one-2">条件查询</h4>
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
        
```

<h4 id="one-3">排序查询</h4>
```
    语法：
        select 查询列表 from 表名 where 筛选条件 order by 排序列表 【asc|desc】;
        order by: 根据什么排序
        asc: 升序
        desc: 降序

```

<h4 id="one-4">常见函数</h4>
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

<h4 id="one-5">分组函数</h4>
```
    分组函数
        功能：做统计使用
            #sum 求和
            #avg 平均值
            #max 最大值
            #min 最小值
            #count 计算个数
```

<h4 id="one-6">分组查询</h4>
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

<h4 id="one-7">连接查询</h4>
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

<h4 id="one-8">子查询</h4>
```

```

<h4 id="one-9">分页查询</h4>
```

```

<h4 id="one-10">union联合查询</h4>
```

```

#### <h3 id="two">二、增删改</h3>
```

```

#### <h3 id="three">三、约束</h3>
```

```

#### <h3 id="four">四、事务</h3>
```

```

#### <h3 id="five">五、视图</h3>
```

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
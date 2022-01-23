mysql关键字不区分大小写

1.1、 操作数据库
创建数据库
CREATE DATABASE IF NOT EXISTS westo;
1
删除数据库
DROP DATABASE IF EXISTS westo
1
使用数据库
 --tab 键的上面，如果你的表名或者字段名是一个特殊的字符，就需要带
 USE `school`
1
2
查看数据库
SHOW DATBASE  --查看所有数据库
1
1.2、数据库的列属性
数值

tinyint 十分小的数据 1个字节

smallint 较小的数据 2个字节

mediumint 中等大小的数据 3个字节

int 标准的整数 4个字节 （常用）

bigint 较大的数据 8个字节

float 浮点数 4个字节

double 浮点数 8个字节 （精度问题！）

decimal 字符串形式的浮点数 金融计算问题 ，一般都是使用decimal

字符串

char 字符串固定大小 0~255
varchar 可变字符串 0~65535 常用的变量 String
tinytext 微型文本 2^8-1
text 文本串 2^16-1 保存大文本
时间日期

java.util.Date

data YYYY-MM-DD 日期格式
time HH: mm: ss 时间格式
datetime YYYY-MM-DD HH: mm: ss 最常用的时间格式
timestamp 时间戳 1970.1.1到现在的毫秒数！ 也较为常用！
year 年份表示
null

没有值
注意：不能用NULL进行运算
1.3、数据库的字段属性 （重点）
Unsigned:

无符号的整数
声明了该列不能声明为负数
zerofill:

0填充
不足的位数，使用0来填充 int(3) 3–>003
自增:

自动再上一条的基础上+1
通常用来设计唯一的主键 index，必须是整数型
可以自定义设计主键自增的起始值与步长
非空 not null

设置为not null，不给它赋值，就会报错！
null 如果不填值就默认为null
默认

设置默认值
1.4、创建数据库表（重点）
--目标 ： 创建一个school数据库
--创建学生表（列，字段） 使用SQL创建
--学号int 登录密码,姓名，性别,出生日期,家庭住址

--注意点：使用英文的()，表的名称和字段尽量使用``括起来
--AUTO_INCREMENT 自增
--字符串使用 ''括起来！
--所有的语句后面加,最后一句后面不用加
--PRIMARY KEY 主键，一个表格主键

CREATE TABLE IF NOT EXISTS `student`(
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
    `name` varchar(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
    `pwd` varchar(20) NOT NULL DEFAULT '123456' COMMENT '密码',
    `sex` varchar(2) NOT NULL DEFAULT '男' COMMENT '性别',
    `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
    `address` varchar(100) DEFAULT NULL COMMENT '家庭住址',
    `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

格式：

CREATE TABLE [IF NOT EXISTS] `表名`(
	`字段名` 列类型 [属性] [索引] [注释],
    `字段名` 列类型 [属性] [索引] [注释],
    ......
    `字段名` 列类型 [属性] [索引] [注释]
)[表类型][字符属性][注释]

常用命令

SHOW CREATE DATABASE school  --查看创建数据库的语句
SHOW CREATE TABLE student --查看student数据表的的定义语句
DESC student --显示表的结构

1.5、数据表的类型
/*
INNODB 默认使用
MYISAM 早些年使用
*/

MYISAM	INNODB
事务支持	不支持	支持
数据行锁定	不支持	支持
外键约束	不支持	支持
全文索引	支持	不支持
表空间的大小	较小	较大，约为2倍
常规使用操作：

MYISAM 节约空间，速度较快

INNODB 安全性能高，事务的处理，多表多用户操作

在物理空间的存储位置

所有的数据库文件都存在data目录下，一个文件夹对应一个数据库

本质还是文件的存储！

MySQL引擎在物理文件上的区别

innoDB 在数据库表中只有一个 *.frm文件，以及上级目录下的ibdata1文件
MYISAM 对应文件
*.frm 表结构的定义文件
*.MYD 数据文件（data）
*.MYI 索引文件（index）
设置数据库的字符集编码

CHARSET=utf8
1
不设置的话，会是MySQL默认的字符集编码 （不支持中文！）

MySQL的默认字符集编码是Latin1，不支持中文

在my.ini中配置默认的编码

character-set-server=utf8
1
1.6、修改删除表
修改

--修改表名：ALTER TABLE 旧表名 RENAME AS 新表名
ALTER TABLE teacher RENAME AS teacher1
--增加表的字段：ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE teacher1 ADD age int(11)

--修改表的字段（重命名，修改约束！）
--ALTER TABLE 表名 MODIFY 字段名 列属性[]
ALTER TABLE teacher1 MODIFY age VARCHAR(11) --修改约束
--ALTER TABLE 表名 CHANGE 旧名字 新名字 列属性[]
ALTER TABLE teacher1 CHANGE age age1 INT(11) --字段重命名

--删除表的字段： ALTER TABLE 表名 DROP 字段名
ALTER TABLE teacher1 DROP age1

删除

--删除表（如果存在再删除）
DROP TABLE [IF EXISTS] 表名
1
2
所有的创建、删除操作尽量增加判断语句

注意点：

``字段名使用这个包裹！
注释 /**/
sql关键字大小写不敏感
所有符号全部用英文！
2、 MySQL数据管理
2.1、外键（了解即可）
方式一、在创建表的时候，增加约束（麻烦，比较复杂）

CREATE TABLE IF NOT EXISTS `grade`(
	`gradeid` INT(4) NOT NULL AUTO_INCREMENT COMMENT '年级id',
    ...
    PRIMARY KEY(`gradeid`),
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 学生表的gradeid字段，要去引用年级表的gradeid字段
-- 定义外键key
-- 给这个外键添加约束 （执行引用） references引用

CREATE TABLE IF NOT EXISTS `student`(
	`id` INT(4) NOT NULL AUTO_INCREMENT '匿名' COMMENT '学生id',
    ...
    PRIMARY KEY(`id`),
    KEY `FK_gradeid` (`gradeid`),
    CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `gradeid`
)ENGINE=INNODB DEFAULT CHARSET=utf8

删除外键关系的表的时候，必须要先删除引用别人的表（从表），再删除被引用的的表（主表）

方式二：创建表成功后，添加外键约束

CREATE TABLE IF NOT EXISTS `grade`(
	`gradeid` INT(4) NOT NULL AUTO_INCREMENT COMMENT '年级id',
    ...
    PRIMARY KEY(`gradeid`),
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 学生表的gradeid字段，要去引用年级表的gradeid字段
-- 定义外键key
-- 给这个外键添加约束 （执行引用） references引用

CREATE TABLE IF NOT EXISTS `student`(
	`id` INT(4) NOT NULL AUTO_INCREMENT '匿名' COMMENT '学生id',
    ...
    PRIMARY KEY(`id`),
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 创建表的时候没有外键约束
ALTER TABLE `student`
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY(`gradeid`) REFERENCES `gradeid`

-- ALTER TABLE 表 ADD CONSTRAINT 约束 FOREIGN KEY(作为外键的列) REFERENCES 哪个表（哪个字段）

以上的操作都是物理外键，数据库级别的外键，不建议使用！（避免数据过多造成困扰,这里了解即可）

最佳实践：

数据库就是单纯的表，只用来存储数据，只有行（数据）与列（字段）

我们想使用多张表的数据，想使用外键（程序去实现）

2.2、DML语言（全部记住）
**数据库的意义：**数据存储，数据管理

DML语言：数据操作语言

insert

update

delete

2.3、添加
insert

-- insert into 表名（[字段名1,字段名2,字段名3..]） values('值1'),('值2'),('值3')...
INSERT INTO `grade` ('gradename') VARCHAR ('大四')

-- 由于主键自增我们可以省略（如果不写表的字段，它就会一一对应）
INSERT INTO `grade` VALUES('大四')

-- 一般写插入语句，我们一定要数据和字段一一对应

-- 插入多个字段
INSERT INTO `grade`(`gradename`)
VALUES('大二'),('大一')

INSERT INTO `student`(`name`) VALUES('张三')

INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES('张三','aaaaa','男')

INSERT INTO `student`(`name`,`pwd`,`sex`) 
VALUES('李四','aaaaa','男'),('王五','aaaaa','男')

语法：insert into 表明([字段名1],[字段名2],[字段名3],…) values(‘值1’),(‘值2’),(‘值3’),…

注意事项：

字段与字段之间使用英文逗号隔开

字段是可以省略的，但是后面的值要一一对应，不能少

可以同时插入多条数据，VALUES后面的值，需要使用逗号隔开即可，VALUES()(),…

2.4、修改
update 修改谁 （条件） set 原来的值 =新的值

-- 修改学院名字，带了简介的
UPDATE `student` SET `name` = '狂神' WHERE id= 1

-- 不指定条件的情况下， 会改变所有的表
UPDATE `student` SET `name`='扬起'

-- 语法：
-- UPDATE 表名 SET `column_name`=value,`column_name`=value,...  WHERE 条件

条件：where 字句 运算符 id等于某个值，大于某个值，在某区间内修改

操作符	含义	范围	结果
=	等于	5=6	false
<>	不等于	5<>6	true
>		大于	5>6	false
>	<	小于	5>6	true
>	<=	小于等于	5<=6	true
>	=	大于等于	5>=6	false
>	BETWEEN…AND…	在某个范围内	[2,5]	/
>	AND	我和你 &&	5>1 and a>2	false
>	OR	我或你 ||	5>1 or 1>2	true
>	-- 通过多个条件定位数据
>	UPDATE `student` SET `name`='扬起' WHERE `name`='扬起1' AND `sex`='女'
>	1
>	2
>	语法： UPDATE 表名 SET column_name=value,column_name=value,… WHERE 条件

注意：

column_name 是数据库的列，尽量带上``

条件，筛选的条件，如果没有指定，则修改所有的列

value，是一个具体的值，也可以是一个变量

多个设置的属性之间使用逗号隔开

UPDATE `student` SET `birthday`=CURRENT_TIME WHERE `name`='扬起3' AND `sex`='女'
1
2.5、删除
delete 命令

语法：delete from 表名 where 条件

-- 删除数据 （不要忘了加条件！）
DELETE FROM `student`      -- 有条件情况下避免这样写

DELETE FROM `student` WHERE `id`=1;
1
2
3
4
TRUNCATE命令

作用: 完全清空一个数据库表，表的结构和索引约束不会变！

-- 清空 student表
TRUNCATE `student`
1
2
delete 与 TRUNCATE 区别

相同点：都能删除数据，都不会删除表结构
不同：
TRUNCATE 重新设置 自增列 计数器会归零
TRUNCATE 不会影响事务
-- 测试delete 和 TRUNCATE 区别
CREATE TABLE `test`(
	`id` INT(4) NOT NULL AUTO_INCREMENT,
    `coll` VARCHAR(20) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO `test`(`coll`) VALUES('1')('2')('3')

DELETE FROM `test` -- 不会影响自增

TRUNCATE TABLE `test` -- 自增会归零

了解即可： DELETE删除的问题，重启数据库，现象

INNODB 自增列会重1开始（存在内存当中，断电即失）
MyISAM 继续从上一个自增量开始（存在文件中，不会丢失）
3、DQL查询数据（最重点）
3.1、DQL
（Data Query Language：数据查询语言）

所有的查询操作都用它 SELECT
简单的查询，复杂的查询它都能做
数据库中最核心的语言，最重要的语言
使用频率最高的语句
Select完整语法：

select语法：

SELECT [ALL|DISTINCT]
{*|table.*|[table.field1[as aliast1][,table.field2[as aliast2]][,...]]}
FROM table_name [as table_alias]
	[left|right|inner join table_name2]  -- 联合查询
	[WHERE ...]  -- 指定结果需满足的条件
	[GROUP BY]   -- 指定结果按照那几个字端来分组
	[HAVING]     -- 过滤分组的记录必须要满足的次要条件
	[ORDER BY ...]   -- 指定查询记录按一个或多个条件排序
	[LIMIT {[offset,]row_count|row_countOFFSET offset}]; -- 指定查询记录从哪条，查询记录需要几条

注意： []代表可选的，{}代表必选的

3.2、指定查询字段
-- 查询全部的学生   SELECT 字段 FROM 表
SELECT * FROM student

-- 查询指定字段
SELECT `StudentNo`,`StudentName` From student

-- 别名，给结果起一个名字 AS 可以给字段取名，也可以给表取别名
SELECT `StudentNo` AS 学号,`StudentName` AS 学生姓名 From student AS s

-- 函数Concat(a,b)
SELECT CONCAT('姓名：',StudenName) AS 新名字 FROM student

语法：SELECT 字段 … FROM 表

有的时候，列名字不是那么的见名知意。我们起别名AS 字段名 as 别名 表名 as 别名

去重distinct

作用：去除SELECT查询出来的结果中重复的数据，只显示一条

-- 查询一下有哪些同学参加了考试，成绩
SELECT * FROM `result`  -- 显示全部的考试成绩
SELECT `StudentNo` FROM `result` -- 查询有哪些同学参加了考试
SELECT DISTINCT `StudentNo` FROM `result`  -- 发现重复数据，去重

数据库的列（表达式）

SELECT VERSION()  -- 查看系统版本（函数）
SELECT 100*3-1 AS '计算结果'  -- 用来计算（表达式）
SELECT @@auto_increment_increment   -- 查询自增的步长 （变量）

SELECT `StudentNo`,`StudentResult`+1 AS '提分后' FROM result

数据库中的表达式：文本值，列，NULL，函数，计算表达式，系统变量…

select 表达式 FROM 表

3.3、where条件字句
作用：检索数据中 符合条件 的值

搜索的条件由一个或多个表达式组成！结果 布尔值

逻辑运算符

运算符	语法	描述
and &&	a and b a&&b	逻辑与，两个都为真，结果为真
or ||	a or b a||b	逻辑或，其中一个为真，结果为真
Not ！	not a ！a	逻辑非，真为假，假为真
尽量使用英文字母

-- ============================== where ==============================
SELECT `studentNo`,`StudentResult` FROM result

-- 查询考试成绩在95~100分之间
SELECT `studentNo`,`StudentResult` FROM result
WHERE StudentResult>=95 AND StudentResult<=100
-- and &&
SELECT `studentNo`,`StudentResult` FROM result
WHERE StudentResult>=95 && StudentResult<=100

-- 模糊查询（区间）
SELECT `studentNo`,`StudentResult` FROM result
WHERE StudentResult BETWEEN 95 AND 100

-- 除了1000号学生之外的同学的成绩
SELECT `studentNo`,`StudentResult` FROM result
WHERE studentNo!=1000

-- != not
SELECT `studentNo`,`StudentResult` FROM result
WHERE NOT studentNo=1000

模糊查询：比较运算符

运算符	语法	描述
IS NULL	a is null	如果操作符为null，结果为真
IS NOT NULL	a is not null	如果操作符部位null，结果为真
BETWEEN	a between b and c	若a在 b和c 之间，则结果为真
Like	a like b	SQL匹配，如果a匹配b，则结果为真
In	a in (a1,a2,a3…)	假设a在a1，或者a2…其中一个值中，则结果为真
-- ======================== 模糊查询 ================================
-- 查询姓刘的同学
-- like结合  %(代表0到任意个字符)  _（一个字符）
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `studentName` Like '刘%'

-- 查询姓刘的同学,名字的后面只有一个字的
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `studentName` LIKE '刘_'

-- 查询姓刘的同学,名字的后面只有两个字的
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `studentName` LIKE '刘__'

-- 查询名字中间有嘉字的同学  %嘉%
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `studentName` LIKE '%嘉%'

-- =============== in（具体的一个或多个值） ==================================================
-- 查询 1001，1002,1003 号学员
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `studentNo` in (1001,1002,1003);

-- 查询在安徽，河南洛阳学员
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `Address` in ('安徽','河南洛阳');

-- ====== null not null ========
-- 查询地址为空的同学 null ''
SELECT `studentNo`,`StudentName` FROM `student`
WHERE Address='' OR address is null

-- 查询有出生日期的同学  不为空
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `BornDate` is NOT NULL

-- 查询没有出生日期的同学  为空
SELECT `studentNo`,`StudentName` FROM `student`
WHERE `BornDate` is NULL

3.4、联表查询
JOIN 对比

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-3MhnMLUC-1634102858354)(C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210911095814482.png)]



-- ============================== 联表查询  join =================================
-- 查询参加考试的同学（学号、姓名、科目编号、分数）   需要两张表 
SELECT * FROM student
SELECT * FROM result

/*思路：
1.分析需求，分析查询的字段来自哪些表，（连接查询）
2.确定使用哪些连接查询？ 7种
确定交叉点（这两张表中哪些数据是相同的）
判断条件：学生表中studentNo = 成绩表 studentNo
*/

-- join (连接的表) on （判断条件）         连接查询
-- where            等值查询

-- INNER JOIN
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student As s
INNER JOIN result AS r
ON s.studentNo = r.studentNo

-- RIGHT JOIN
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student As s
RIGHT JOIN result AS r
ON s.studentNo = r.studentNo

-- LEFT JOIN
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student As s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo

操作	描述
inner join	如果表中至少有一个匹配，就返回行
left join	会从左表中返回所有的值，即使右表中没有匹配
right join	会从右表中返回所有的值，即使左表中没有匹配
-- 查询缺考的同学
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student As s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo
WHERE StudentResult is NULL

-- 思考题（查询了参加考试的同学信息：学号、学生姓名、科目名、分数）
/*思路：
1.分析需求，分析查询的字段来自哪些表，student、result、subject（连接查询）
2.确定使用哪种连接查询？ 7种
确定交叉点（这两张表中哪个数据是相同的）
判断条件：学生表中studentNo = 成绩表中studentNo
*/
SELECT s.studentNo,studentName,SubjectName,`StudentResult`
FROM student s
RIGHT JOIN result r
ON r.studentNo=s.studentNo
INNER JOIN `subject` sub
ON r.SubjectNo = r.SubjectNo
WHERE `SubjectResult` is not null

-- 我要查询哪些数据 select...
-- 从哪几张表中查 FROM 表 *** JOIN 连接的表 on 交叉条件
-- 假设存在一种多张表查询，慢慢来，先查询两张表然后再慢慢增加

-- FROM a LEFT JOIN b
-- FROM a RIGHT JOIN b


自连接

自己的表和自己连接，核心：一张表拆为两张一样的表即可

父类

categoryid	categoryName
2	信息技术
3	软件开发
5	美术设计
子类

pid	categoryid	categoryName
3	4	数据库
2	8	办公信息
3	6	web开发
5	7	美术设计
操作：查询父类对应的子类关系

父类	子类
信息技术	办公信息
软件开发	数据库
软件开发	web开发
美术设计	ps技术
-- 查询父子信息:把一张表看成两张一模一样的表
SELECT a.`categoryName` AS '父栏目',b.`categoryName` AS '子栏目'
FROM `category` as a,`category` as b
WHERE a.`categoryid`=b.`pid`

-- 查询学员所属年级（学员，学生的姓名，年级名称）
SELECT studentNo,studentName,`GradeName`
FROM student s
INNER JOIN `grade` g
ON s.`GradeID`=g.`GradeID`

-- 查询科目所属的年级（科目名称，年级名称）
SELECT `SubjectName`,`GradeName`
FROM `subject` sub
INNER JOIN `grade` g
ON sub.`GradeID`=g.`GradeID`

-- 查询参加了 数据库结构 考试的同学信息：学号，学生姓名，科目名，分数
SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`studentNo`=r.`studentNo`
INNER JOIN `subject` sub
ON r.`SubjectNo`=sub.`SubjectNo`
WHERE subjectName='数据库结构'

3.5、分页和排序
排序

-- =========================== 分页 limit 和排序 order by ============================
-- 排序： 升序 ASC ， 降序 DESC
-- ORDER BY 通过哪个字段排序，怎么排
-- 查询的结果根据 成绩降序 排序
SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`studentNo`=r.`studentNo`
INNER JOIN `subject` sub
ON r.`SubjectNo`=sub.`SubjectNo`
WHERE subjectName='数据库结构'  
ORDER BY StudentResult ASC

分页

--  为什么要分页？
--  缓解数据库压力，给人的体验更好，瀑布流

-- 分页，每页只显示五条数据
-- 语法：limit 当前页 页面大小
SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`studentNo`=r.`studentNo`
INNER JOIN `subject` sub
ON r.`SubjectNo`=sub.`SubjectNo`
WHERE subjectName='数据库结构'  
ORDER BY StudentResult ASC
LIMIT 1,5

-- 第一页  limit 0,5
-- 第二页  limit 5,5
-- 第三页  limit 10,5
-- 第n页  limit (n-1)*pageSize,pageSize
-- 【pageSize：页面大小】
-- 【（n-1）*pageSize起始值】
-- 【n：当前页】
-- 【数据总数/页面大小 = 总页数】

语法：limit 查询起始下标 ,ageSize

3.6、子查询
where (这个值是计算出来的)

本质： 在where语句中嵌套一个子查询语句

where (select * from)

-- ======================== where ===========================

-- 1、查询 数据库结构 的所有考试结果（学号、科目编号、成绩） 降序排列
-- 方式一：使用连接查询
SELECT `StudentNo`,r.`SubjectNo`,`StudentResult`
FROM `result` r
INNER JOIN `subject` sub
ON r.SubjectNo = sub.SubjectNo
WHERE SubjectName = '数据库结构'
ORDER BY StudentResult DESC

-- 方式二：使用子查询（由里及外）
SELECT `StudentNo`,r.`SubjectNo`,`StudentResult`
FROM `result`
WHERE StudentNo =(
    SELECT StudentNo FROM `subject` 
    WHERE SubjectName = '数据库结构'
)
ORDER BY StudentResult DESC

-- 分数不小于80分的学生的学号和姓名
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM student s
INNER JOIN result r
ON s.`StudentNo` = R.`StudentNo`
WHERE `StudentResult` >= 80

-- 在这个基础上增加一个科目， 高等数学
-- 查询 高等数学 的编号
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM student s
INNER JOIN result r
ON s.`StudentNo` = R.`StudentNo`
WHERE `StudentResult` >= 80 and `SubjectNo` = (
	SELECT `SubjectNo` FROM `subject`
    WHERE `SubjectName` = '高等数学'
)
-- 再改造(由里及外)
SELECT DISTINCT `StudentNo`,`StudentName` FROM student WHERE `StudetNo` IN (
	SELECT `StudentNo` FROM result WHERE `StudentResult` >= 80 AND `SubjectNo` = (
    	SELECT `SubjectNo` FROM `subject` WHERE `SubjectName` = '高等数学'
    )
)

-- 联系：查询 C语言 前五名同学成绩的信息（学号，姓名，分数）
-- 使用子查询

3.7、分组和过滤
-- 查询不同课程的平均分，最高分，最低分
-- 核心：（根据不同的课程分组）
SELECT `SubjectName`, AVG(`StudentResult`) AS 平均分,MAX(`StudentResult`),MIN(`StudentResult`)
FROM result r
INNER JOIN `subject` sub
ON r.`SubjectNo` = sub.`SubjectNo`
GROUP BY r.`SubjectNo` -- 通过什么字段分组
HAVING 平均分>80
1
2
3
4
5
6
7
8
4、MySQL函数
官网：https://dev.mysql.com/doc/refman/8.0/en/built-in-function-reference.html

4.1、常用函数
-- ======================= 常用函数 ==========================

-- 数学运算
SELECT ASC(-8) -- 绝对值
SELECT CEILING(9.4) -- 向上取整
SELECT FLOOR(9.4)  -- 想下去整
SELECT RAND() -- 返回一个随机数
SELECT SING() -- 判断一个数的符号 0-0  负数返回-1 ， 正数返回 1

-- 字符串函数
SELECT CHAR_LENGTH('即使再小的帆也能返航！')  -- 字符串长度
SELECT CONCAT('我','爱'，'你')  -- 拼接字符串
SELECT INSERT('我爱编程helloWord',1,2,'超级热爱')  -- 查询，从某个位置开始替换某个长度
SELECT LOWER('YANGQI') -- 小写字母
SELECT UPPER('yangqi') -- 大写字母
SELECT INSTR('yangqi','q') -- 返回第一次出现的字符的索引
SELECT REPLACE('杨起一定能坚持成功','坚持','努力')  -- 替换出现的指定字符串
SELECT SUBSTR('杨起一定能够坚持成功',4,6) -- 返回指定的子字符串 （源字符串，截取的位置，截取的长度）
SELECT REVERSE('wywywy') -- 反转

-- 查询姓 周 的同学，改为邹
SELECT REPLACE(studentName，'周','邹') FROM student
WHERE studentName Like '周%'

-- 时间和日期函数 （记住）
SELECT CURRENT_DATE()  -- 获取当前日期
SELECT SURDATE()  -- 获取当前日期
SELECT NOW()  -- 获取当前的时间
SELECT LOCALTIME() -- 本地时间
SELECT SYSDATE()  -- 系统时间

SELECT YEAR(NOW()) -- 获取当前年
SELECT MONTH(NOW())
SELECT DAY(NOW())
SELECT HOUR(NOW())
SELECT MINUTE(NOW())
SELECT SECOND(NOW())

-- 系统
SELECT SYSTEM_USER() -- 系统用户
SELECT USER()
SELECT VERSION()

4.2、聚合函数（常用）
函数名称	描述
COUNT()	计数
SUM()	求和
AVG()	平均值
MAX()	最大值
MIN()	最小值
…	…
-- ======================== 聚合函数 =======================
-- 都能够统计 表中的数据
SELECT COUNT(studentname) FROM student; -- Count（指定列） ，会忽略null值
SELECT COUNT(*) FROM student; -- Count（*）  不会忽略null值 ，本质：计算行数
SELECT COUNT(1) FROM student; -- Count（1）  不会忽略 所有的null值 ，本质：计算行数

SELECT SUM(`StudentResult`) AS '总分' FROM result
SELECT AVG(`StudentResult`) AS '平均值' FROM result
SELECT MAX(`StudentResult`) AS '最大值' FROM result
SELECT MIN(`StudentResult`) AS '最小值' FROM result

-- 查询不同课程的平均分，最高分，最低分
-- 核心：（根据不同的课程分组）
SELECT `SubjectName`, AVG(`StudentResult`) AS 平均分,MAX(`StudentResult`),MIN(`StudentResult`)
FROM result r
INNER JOIN `subject` sub
ON r.`SubjectNo` = sub.`SubjectNo`
GROUP BY r.`SubjectNo` -- 通过什么字段分组
HAVING 平均分>80

4.3、数据库级别的MD5加密（扩展）
什么是MD5？

主要增强算法复杂性和不可逆性。

MD5不可逆，具体的值得md5是一样的

MD5破解网站的原理，背后有一个字典，MD5加密后的值 加密前的值

-- =============== 测试MD5加密 ==================
CREATE TABLE `testmd5`(
	`id` INT(4) NOT NULL,
    `name` VARCHAR(20) NOT NULL,
    `pwd` VARCHAR(20) NOT NULL,
    PRIMARY KEY(`id`)
)ENGING=INNODB DEFAULT CHARSET=utf8

-- 明文密码
INSERT INTO `testmd5` VALUES(1,'zhangsan','123456'),(2,'lisi','123456'),(1,'wangwu','123456')

-- 加密
UPDATE `tsetmd5` SET `pwd`=MD5(pwd) WHERE id=1

UPDATE `tsetmd5` SET `pwd`=MD5(pwd) WHERE id!=1

UPDATE `tsetmd5` SET `pwd`=MD5(pwd) -- 加密全部密码

-- 插入的时候加密
INSERT INTO `testmd5` VALUES(4,'xiaoming',MD5('123456'))

-- 如何校验：将用户传进来的密码，进行md5进行加密，然后对比加密后的值
SELECT * FROM `testmd5` WHERE `name`='xiaoming' AND pwd = MD5('123456')

5、事务
5.1、什么是事务
要么都成功，要么都失败！

1、SQL执行 A给B 转账 A 2000 -------> B 200 B 200

2、SQL执行 B收到 A 的钱 A 1800 ------> B 400

将一组SQL放在一个批次里面去执行

事务原则：ACID 原则 ： 原子性(Atomicity)、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）

参考链接：https://blog.csdn.net/dengjili/article/details/82468576

原子性(Atomicity)

要么都成功，要么都失败！

一致性（Consistency）

事务前后的数据总数一致！

持久性（Durability）

数据转移成功之前如果断电，数据不变

数据一旦提交，不可逆，被持久化到数据库中！

隔离性（Isolation）

事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启事务，不能被其他事务的操作数据所干扰，事物之间要相互隔离

隔离所导致的一些问题

脏读：

指一个事务读取了另外一个事务未提交的数据。

不可重复读：

在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）

虚读(幻读)：

是指在一个事务内读取到了别的事务插入的数据，导致前后读取数量总量不一致。

5.2、事务操作
-- ======================== 事务 ======================
-- mysql 是默认开启事务自动提交的
SET autocommit = 0   /* 关闭 */
SET autocommit = 1   /* 开启（默认的） */

-- 手动处理事务
SET autocommit = 0  -- 关闭自动提交
-- 事务开启
START TRANSACTION   -- 标记一个事务的开始，从这个之后的sql 都在同一个事务中

INSERT XX
INSERT XX

-- 提交：持久化（成功！）
COMMIT
-- 回滚：回到原来的样子（失败！）
ROLLBACK
-- 事务结束
SET autocommit = 1  -- 开启自动提交

-- 了解
SAVEPOINT 保存点名  -- 设置一个事物的保存点
ROLLBACK TO SAVEPOINT 保存点名  -- 回滚到保存点


-- 转账
CREATE DATABASE shop CHARACTER SET utf8 COLLATE utf8_general_ci
USE shop

CREATE TABLE `acount`(
	`id` NOT NULL AUTO_INCREMENT,
    `name` VARCHAR(20) NOT NULL,
    `money` DECIMAL(9,2) NOT NULL,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO `acount`(`name`,`money`)
VALUES('A',2000.00),('B',10000.00)
-- 模拟转账：事务
SET autocommit =0; -- 关闭自动提交
START TRANSACTION -- 开启一个事务
UPDATE account SET `money`=`money`-500 WHERE `name` ='A'  -- A减500
UPDATE account SET `money`=`money`+500 WHERE `name` ='B'  -- B加500

COMMIT;   -- 提交事务
ROLLBACK;  -- 回滚  

SET autocommit=1; -- 恢复默认值

6、索引
MySQL官方对索引的定义为：索引（index）是帮助MySQL高效获取数据的数据结构。 正常：0.5s 利用索引：0.000001s

提取句子主干，就可以得到索引的本质：索引是数据结构。

6.1、索引的分类
在一个表中，主键索引只能有一个，唯一索引可以有多个

主键索引（PRIMARY KEY）
唯一的标识，主键不可重复，只能有一个列作为主键
唯一索引（UNIQUE KEY）
避免重复的列出现，唯一索引可以重复，多个列都可以标识为 唯一索引
常规索引（KEY / INDEX）
默认的，index。key关键字来设置
全文索引（FULLTEXT）
在特定的数据库引擎下才有，MyISAM
快速定位数据
-- 索引的使用
-- 1、在创建表的时候给字段增加索引
-- 2、创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM `student`

-- 增加一个全文索引  （索引名） 列名                              ALTER修改表
ALTER TABLE school.student ADD FULLTEXT INDEX `studentkey`(`studentName`)

-- EXPLAIN 分析sql执行的状况
EXPLAIN SELECT * FROM student;   -- 非全文索引

EXPLAIN SELECT * FROM student WHERE MATCH(studentName) AGAINST('刘');  -- 全文索引 
1
2
3
4
5
6
7
8
9
10
11
12
13
14
6.2、测试索引
CREATE TABLE `app_user`(
	`id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    `name` VARCHAR(50) DEFAULT '匿名' COMMIT '用户昵称',
    `email` VARCHAR(50) NOT NULL COMMIT '用户邮箱',
    `phone` VARCHAR(20) DEFAULT '' COMMIT '手机号',
    `gender` TINYINT(4) UNSIGNED DEFAULT '0' COMMIT '性别：（0：男；1：女）',
    `password` VARCHAR(100) NOT NULL COMMIT '密码',
    `age` TINYINT(4) DEFAULT '0' COMMIT '年龄',
    `create_time` DATETIME DEFAULT CURRENT_TIMESTAMP,
    `update_time` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIME,
    PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8 COMMIT='app用户表'

-- 插入100万条数据   55.176 sec
DELIMITER $$  -- 写函数之前必写
CREATE FUNCTION mock_data()   -- 创建函数
RETURNS INT   -- 返回值
BEGIN 
	DECLARE num INT DEFAULT 1000000;
	DECLARE i INT DEFAULT 0;
	
	WHILE i<num DO
		-- 插入语句  CONCAT()拼接字符串
		INSERT INTO app_user(`name`,`email`,`phone`,`gender`,`password`,`age`) 
		VALUES(CONCAT('用户',i),'1551952250@qq.com',  
	    CONCAT('18',FLOOR(RAND()*(999999999-1000000000)+100000000)),   -- FLOOR()向下取整
	    FLOOR(RAND()*2),UUID(),FLOOR(RAND()*100))  
		SET i = i+1;
	END WHILE;
	RETURN i;
END;
SELECT mock_data();

SELECT * FROM app_user WHERE `name`='用户9999';   -- 0.993 sec
SELECT * FROM app_user WHERE `name`='用户9999';   -- 1.098 sec
SELECT * FROM app_user WHERE `name`='用户9999';   -- 0.788 sec

EXPLAIN SELECT * FROM app_user WHERE `name` = '用户9999';

SELECT * FROM student

-- 索引名： id_表明_字段名
-- CREATE INDEX 索引名 on 表（字段）
CREATE INDEX id_app_user_name ON app_user(`name`);

SELECT * FROM app_user WHERE `name`='用户9999';   -- 0.001 sec

EXPLAIN SELECT * FROM app_user WHERE `name` = '用户9999';

索引在小数据量的时候用处不大，但是在大数据的时候，区别十分明显。

6.3、索引原则
索引不是越多越好
不要对进程变动数据加索引
小数据的表不需要加索引
索引一般加在常用来查询的字段上
索引的数据结构

Hash类型的索引

Btree：InnoDB的默认数据结构

参考文档：http://blog.codinglabs.org/articles/theory-of-mysql-index.html

7、权限管理和备份
7.1、用户管理
SQL命令操作

用户表：mysql.user

本质：对这张表进行增删改查

-- 创建用户   CREATE USER 用户名 IDENTIFIED BY 密码
CREATE USER yangqi IDENTIFIED BY '123456'

-- 修改密码  （修改当前用户的密码）
SET PASSWORD = PASSWORD('123456')

-- 修改密码（修改指定用户的密码）
SET PASSWORD FOR yangqi = PASSWORD('123456')

-- 重命名 RENAME USER 原来名字 TO 新名字
RENAME USER yangqi TO yangqi2

-- 用户授权 ALL PRIVILEGES 全部权限 ， 库，表
-- ALL PRIVILEGES除了给别人授权，其他都能干
GRANT ALL PRIVILEGES ON *.* TO yangqi2

-- 查询权限
SHOW GRANTS FOR yangqi2 -- 查看指定用户的权限
SHOW GRANTS FOR root@localhost

-- ROOT用户授权：GRANT ALL PRIVILEGES ON *.* TO yangqi2 'root@localhost' WITH GRANT OPTION

-- 撤销权限 REVOKE 哪些权限，在哪个库撤销，给谁撤销
REVOKE ALL PRIVILEGES ON *.* FROM yangqi2

-- 删除用户
DROP USER yangqi2 

7.2、MySQL备份
为什么要备份：

保证重要的数据不丢失
数据转移
MySQL数据库备份方式：

直接拷贝物理文件（data文件）
在可视化工具中手动导出
在想要导出的 表或库 右键 导出或转储
使用命令行（win+r 输入cmd）导出 mysqldump 命令行使用
# mysqldump -h主机 -u用户名 -p密码 数据库 表名 >物理磁盘位置/文件位置
mysqldump -hlocalhost -uroot -p123456 school student >D:/a.sql
# 成功后显示：mysqldump:[Warning] Using a password on the command line interface can be insecure.

# mysqldump -h主机 -u用户名 -p密码 数据库 表名1 表2 表3 >物理磁盘位置/文件位置
mysqldump -hlocalhost -uroot -p123456 school student >D:/b.sql

# mysqldump -h主机 -u用户名 -p密码 数据库 >物理磁盘位置/文件位置
mysqldump -hlocalhost -uroot -p123456 school >D:/c.sql


#导入
#登陆的情况下，切换到指定的数据库
# source 备份文件
source d:a.sql

mysql -u用户名 -p密码 数据库 <备份文件

假设你要备份数据库，以防数据库丢失。

把数据库给别人用，把sql文件给别人

8、规范数据库设计
8.1、为什么需要设计
当数据库比较复杂的时候，我们就需要设计了

糟糕的数据库设计：

数据冗余，浪费空间
数据库插入和删除都会麻烦，异常【屏蔽使用物理外键】
程序性能差
良好的数据库设计：

节省内存空间
保证数据库的完整性
方便我们开发系统
软件开发中，关于数据库的设计：

分析需求：分析业务和需要处理的数据库的需求
概要设计：设计关系图E-R图
设计数据库的步骤：（个人博客）

收集信息，分析需求
用户表（用户登录注销、用户的个人信息、写博客、创建分类）
分类表（文章分类、谁创建的）
文章表（文章的信息）
友链表（友链信息）
自定义表（系统信息、某个关键的字，或者一些主字段） key：value
说说表（发表心情… ID content create_time）
标识实体（把需求落地到每个字段）
标识 实体之间的关系
写博客：user–> blog
创建分类：user --> category
关注：user --> user
友链：links
评论： user -->user --> blog
前台的图片什么的：ant.design

8.2、三大范式
为什么需要数据规范化？

信息最重要
更新异常
插入异常
无法正常显示信息
删除异常
丢失有效的信息
三大范式（了解） （规范数据库的设计）

第一范式（1NF）：

原子性：保证每一列不可再分

第二范式（2NF）：

前提：满足第一范式

每一张表只描述一件事情。

第三范式（3NF）：

前提：满足第一范式 和 第二范式

第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。

规范 和 性能的问题：

关联查询的表不得超过三张表

考虑商业化的需求和目标，（成本，用户体验！）数据库的性能更加重要
在规范性能的问题的时候，需要适当的考虑一下 规范性！
故意给某些表增加一些冗余的字段。（从多表查询中变为单表查询）
故意增加一些计算列（从大数据量降为小数据量的查询：索引）
9、JDBC（重点）
9.1、数据库驱动
 驱动：声卡、显卡、数据库

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-a8cVl9MZ-1634102996239)(C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210916102402111.png)]

我们的程序通过 数据库驱动 和数据库打交道

##　9.2、JDBC

SUN公司为了简化 开发人员（对数据库的统一操作），提供了一个（Java操作数据库的）规范，俗称 JDBC

这些规范的实现由厂商去做~

对于开发人员来说，我们只需要掌握JDBC接口的操作即可！

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Jk4X1EhX-1634102996243)(C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210916103153270.png)]

java.sql

javax.sql

还需要导入数据库驱动包 ：mysql-connector-java-5.1.47.jar

9.3、第一个JDBC程序
创建测试数据库

数据库：

CREATE DATABASE jdbcStudy CHARACTER SET utf8 COLLATE utf8_general_ci;

USE jdbcStudy;

CREATE TABLE users(
	`id` INT PRIMARY KEY,
    `name` VARCHAR(40),
    `password` VARCHAR(40),
    `email` VARCHAR(60),
    `birthday` DATE
) ;

INSERT INTO users(`id`,`name`,`email`,`birthday`)
VALUES(1,'zhangsan','123456','zs@qq.com','1998-10-07'),
(2,'lisi','123456','ls@qq.com','1999-10-07'),
(3,'wangwu','123456','ww@qq.com','2000-10-07');

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
1、创建一个普通项目

2、导入数据库驱动

！数据库导入

3、编写测试代码

package com.yangqi.Demo1
    
//我的第一个JDBC程序
public class JdbcFirstDemo{
	public static void main(String[] args) throws ClassNotFoundException {
        //1.加载驱动
        // DriverManager.register
        Class.forName("com.mysql.jdbc.Driver");//固定写法，加载驱动
        //2.用户信息和url
        String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";
        String username ="root";
        String password = "123456";
        //3.连接成功，数据库对象   Connection代表数据库
        Connection connection = DriverManager.getConnection(url,username,password);
        //4.创建执行SQL对象   Statement  执行sql的对象
        Statement statement = connection.createStatement();
        
        //5.执行SQL的对象，去执行SQL，可能存在结果，查看返回结果
        String sql = "SELECT * FROM users";
        
        ResultSet resultSet = statement.executeQuery(sql);// 返回的结果集
        
        while(resultSet.next()){
            System.out.println("id="+resultSet.getObject("id"));
            System.out.println("name="+resultSet.getObject("name"));
            System.out.println("pwd="+resultSet.getObject("password"));
            System.out.println("birthday="+resultSet.getObject("birthday"));
            System.out.println("email="+resultSet.getObject("email"));
            System.out.println("======================================");
        }
        
        //6.释放连接
    	resultSet.close();
        statement.close();
        connection.close();
        
    }
}

步骤总结：

加载驱动
连接数据库 DirverMannager
获得执行sql的对象 Statement
获得返回的结果集
释放连接
DriverManager

// DriverManager.registerDriver(com.mysql.jdbc.Driver());
Class.forName("com.mysql.jdbc.Driver"); //固定写法，加载驱动

//connection 代表数据库
//数据库设置自动提交
//事务提交
//事务回滚
	connection.rollback();
	connection.commit();
	connection.setAutoCommit();
1
2
3
4
5
6
7
8
9
10
URL

String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";

//mysql  ---3306
//协议://主机地址:端口号/数据库名?参数1&参数2&参数3

//oracle  ---1521
//jdbc:oracle:thin:@localhost:1521:sid
1
2
3
4
5
6
7
Statement 执行SQL的对象 PrepareStatement执行SQL的对象

String sql = "SELECT * FROM users"; //编写sql语句

statement.executeQuery();  //查询操作返回ResultSet
statement.execute();   //执行任何sql语句
statement.executeUpdate();  //执行增、删、改操作，返回一个受影响的行数
1
2
3
4
5
ResultSet查询的结果集：封装了所有的查询结果集

获得指定的数据类型

resultSet.getObject();   //在不知道列类型的情况下使用
//如果知道列的类型就是用指定的类型
resultSet.getString();
resultSet.getInt();
resultSet.getFloat();
resultSet.getDate();
...
1
2
3
4
5
6
7
遍历 指针

resultSet.beforeFirst();  // 移动到最前面
resultSet.afterLast();   // 移动到最后面
resultSet.next();  //移动到下一个数据
resultSet.previous();  // 移动到前一行
resultSet.absolute(row);  //移动到指定行
1
2
3
4
5
释放资源

 //6.释放连接
resultSet.close();
statement.close();
connection.close();  //耗资源，用完关掉！
1
2
3
4
9.4、statement对象
JDBC中的statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可。

Statement对象的executeUpdate方法，用于向数据库发送增、删、改的sql语句，executeUpdate执行完后，将会返回一个整数（增、删、改语句导致了数据库几行数据发生了改变）。

Statement.executeQuery方法用于向数据库发送查询语句，executeQuery方法返回代表查询结果的ResultSet对象。

CRUD操作-create

使用executeUpdate(String sql) 方法完成数据添加操作，示例操作：

Statement st = conn.createStatement();
String sql = "insert into user(...) VALUES(...)";
int num = st.executeUpdate(sql);
if(num>0){
    System.out.println("插入成功！");
}
1
2
3
4
5
6
CRUD 操作-delete

使用executeUpdate(Steing sql)方法完成数据库的删除操作，示例操作：

Statement st = conn.createStatement();
String sql = "delete from user where id = 1";
int num =st.executeUpdate(sql);
if(num>0){
    Syetem.out.println("删除成功！");
}
1
2
3
4
5
6
CRUD 操作-update

使用executeUpdate(String sql)方法完成数据库的修改操作，示例操作：

Statement st = conn.createStatement();
String sql = "update user Set name = yangqi where id = 2";
int num = st.executeUpdate(sql);
if(num>0){
    System.out.println("修改成功！")
}
1
2
3
4
5
6
CRUD 操作-read

使用executeQuery(String sql)方法完成数据查询操作，示例操作：

Statement st = conn.createStatement();
String sql = "select * from user where id = 1";
ResultSet rs = st.executeQuery(sql);
if(rs.next()){
    //根据获取的数据类型，分别调用rs的相应方法映射到Java对象中
    
}
1
2
3
4
5
6
7
代码实现

提取工具类

src目录下创建dp.properties(配置类单独放出来)

driver = com.mysql.jdbc.Driver
url = jdbc:mysql://localhost:3306/jdbcstudy? useUnicode=true&characterEncoding=utf8&useSSL=true  //useSSL安全连接
username = root
password = 123456
1
2
3
4
单独创建一个包，包里面创建一个工具类JdbcUtils

import...
    
public class JdbcUtils{
    
    private static String driver = null;
    private static String root = null;
    private static String username = null;
    private static String password = null;
    
    static{                      //创建该类对象就调用
        
        try{
           Input in = JdbcUtils.class.getClassLoader().getResourceAsStream("dp.properties");// getClassLoader()获取类加载器         getResourceAsStream()获取资源 
            Properties properties = new Properties();//将流放到properties里面
    		properties.load(in);          //加载流
            
            driver = properties.getProperty("driver");
            root = properties.getProperty("root");
            username = properties.getProperty("username");
            password = properties.getProperty("password");
            
            //1.驱动只需要加载一次
            Class.forName(driver);
            
        }catch(Exception e)
            e.printStackTrace();
    }
    
    //获取连接
    public static Connection getConnection() thows SQLException{
        return DriverManager.getConnection(url,username,password);
    }
    
    //释放连接资源
    public static void release(Connection conn,Statement st,ResultSet rs){
        if(rs != null){
            try{
                rs.close();
        	}catch(SQLException e){
            	e.printStackTrace();
        	}
        }
        if(st != null){
            try{
                st.close();
        	}catch(SQLException e){
            	e.printStackTrace();
        	}
        }
        if(conn != null){
            try{
                conn.close();
        	}catch(SQLException e){
            	e.printStackTrace();
        	}
        }
    }

} 

编写怎么增、删、改：executeUpdate

创建测试类TestInsert

import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            st = conn.createStatement();     //获得SQL的执行对象
            String sql = "INSERT INTO   users(id,name,password,email,birthday)"+" VALUES(4，'yangqi','123456','1551952250@qq.com','2000-10-07') "; //主键不能重复
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("插入成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}

创建测试类TestDelete

import...
    
public class TestDelete{
    public static void main(String[] args){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            st = conn.createStatement();     //获得SQL的执行对象
            String sql = "delete from users where id = 4";
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("删除成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}

创建测试类TestUpdate
import...
    
public class TestUpdate{
    public static void main(String[] args){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        

        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            st = conn.createStatement();     //获得SQL的执行对象
            String sql = "Update users set `name` = 'zhangsan',`email` = '1551952250@qq.com' where id = 1";
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("更新成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}

创建测试类TestSelect executeQuery
import...
    
public class TestSelect{
    public static void main(String[] args){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            st = conn.createStatement();     //获得SQL的执行对象
            String sql = "select * from users where id = 2";
            rs = st.executeQuery(sql);
            while(rs.next()){
                System.out.println(rs.getString("name"));
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}

SQL注入的问题

sql 存在漏洞，会被攻击导致数据泄露 SQL会被拼接or

import...
    
public class SQL注入{
    public static void main(String[] args){
     	
        //login("yangqi","123456"); 正常登陆  
        login(" 'or '1=1"," 'or '1=1"); //可以登录
        
    }
    //登录业务
    public static void login(String username,String password){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            st = conn.createStatement();     //获得SQL的执行对象
            String sql = "select * from users where name = '"+username+"' AND password = '"+password+"'";
            rs = st.executeQuery(sql);
            while(rs.next()){
                System.out.println("name");
                System.out.println("password"+"登陆成功");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}

9.5、PreparedStatement对象
PreparedStatement可以防止SQL注入，效果更好！

新增一个包

新增，创建一个新的测试类 TestInsert
import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        PreparedStatement st = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            
            //区别
            //使用？占位符代替参数
            String sql = "INSERT INTO   users(id,`name`,`password`,`email`,`birthday`)"+" VALUES(?,?,?,?,?) ";                     
            st = conn.PreparedStatement(sql);//预编译SQL,先写sql，然后不执行
            //手动给参数赋值
            st.setInt(1,4);
            st.setString(2,"wangyong");
            st.setString(3,'123456');
            st.setString(4,"1551952250@qq.com");
            //注意点：sql.Date     数据库   java.sql.Date()
            //       util.Date   Java    new Date().getTime() 获得时间戳
            st.setDate(5,new java.sql.Date(new Date().getTime()))
                
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("插入成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,null);
            
        }
    }
}

删除,创建一个新的测试类 TestDelete
import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        PreparedStatement st = null;
        

        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            
            //区别
            //使用？占位符代替参数
            String sql = "delete from users where id=?";                     
            st = conn.PreparedStatement(sql);//预编译SQL,先写sql，然后不执行
            //手动给参数赋值
            st.setInt(1,4);
                
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("插入成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,null);
            
        }
    }
}

更新,创建一个新的测试类 TestUpdate
import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        PreparedStatement st = null;
        

        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            
            //区别
            //使用？占位符代替参数
            String sql = "Update users set `name`=? where id=?";                     
            st = conn.PreparedStatement(sql);//预编译SQL,先写sql，然后不执行
            //手动给参数赋值
            st.setString(1,"扬启");
            st.setInt(2,1);
                
            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("插入成功!");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,null);
            
        }
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
查询,创建一个新的测试类 TestSelect
import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            
            //区别
            //使用？占位符代替参数
            String sql = "SELECT * FROM users WHERE id=?";                     
            st = conn.PreparedStatement(sql);//预编译SQL,先写sql，然后不执行
            //手动给参数赋值
            st.setString(1,1);
                
            rs = st.executeQuery(sql);
            if(rs.next()){
                System.out.println(rs.getString("name"));
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,null);
            
        }
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
防止注入

import...
    
public class SQL注入{
    public static void main(String[] args){
     	
        //login("yangqi","123456"); 正常登陆  
        login("' 'or '1=1","123456"); //可以登录
        
    }
    //登录业务
    public static void login(String username,String password){
        Connection conn = null;
        PerparedStatement st = null;
        ResultSet rs = null;
        
        try{
            conn = JdbcUtils.getrConnection();
            
            //PreparedStatement 防止SQL注入的本质，把传递过来的参数当成字符
            //假设其中存在转义字符，比如说 ' 会被直接转义
            String sql = "select * from users where name = ? AND password = ?";//mybatis
            st = conn.PerparedStatement(sql);
            st.setString(1,"扬启");
            st.setString(2,123456);
            
            rs = st.executeQuery(sql);
            while(rs.next()){
                System.out.println("name");
                System.out.println("password"+"登陆成功");
            }
            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,rs);
            
        }
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
9.6、事务
要么都成功，要么都失败

ACID原则

原子性：要么都成功，要么都失败

一致性：总数不变

隔离性：多个线程互不干扰

持久性：一旦提交不可逆，持久化到数据库

隔离性的问题：

脏读：一个事务读取了另一个没有提交的数据

不可重复读：在同一个事务内，重复读取表中的数据，表数据发生改变

虚读（幻读）：在一个事务内，读取到了别人插入的数据，导致前后读出来的结果不一致

-- 创建账户表
CREATE TABLE account(
	`id` INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(40),
    `money` FLOAT
);

-- 插入测试数据
insert into account(name,money) values('A',1000)
insert into account(name,money) values('B',1000)
insert into account(name,money) values('C',1000)
1
2
3
4
5
6
7
8
9
10
11
创建测试类TestTransaction

import...
    
public class TestInsert{
    public static void main(String[] args){
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;
        try{
            conn = JdbcUtils.getrConnection();  //获取数据库连接
            //关闭数据库的自动提交（自动会开启事务）
            conn.setAutoCommit(false);//开启事务
            
            String sql1 = "Update account set money=money-100 where id='A'";    
            st = conn.PreparedStatement(sql1);
            st.executeUpdate();
            String sql2 = "Update account set money=money+100 where id='B'";     
            st = conn.PreparedStatement(sql2);
            st.executeUpdate();
            
            //业务完毕，提交事务
            conn.commit();
            System.out.println("成功！");
            
        }catch(SQLException e){
            try{
                conn.rollback(); //如果失败则回滚事务
            }catch(SQLException){
                e1.printStackTrace();
            }
            e.printStackTrace();
        }finally{
            JdbcUtils.release(conn,st,null);
            
        }
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
开启事务 conn.setAutoCommint(false);
一组业务执行完毕，提交事务
可以在catch语句中显示的定义回滚语句，但默认失败就会回滚

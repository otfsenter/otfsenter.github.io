# java

5个问题

- 没有体系，像无头苍蝇

- 学习动力不够，学的知识点不知道应用场景，没有乐趣

- 深度不够，看不懂源码，多态不懂，基础差
- 如何快速学习技术、编程、框架、设计模式，不知道会导致学新东西不够快
- 没有建立正确的编程思维，不知道对不懂的问题下手，要建立自己的思维体系，从不懂一直到找到入口，有自己的一套思维体系。



Java后端技术体系

## java基础

### 第一阶段：建立编程思想

#### java概述



 `如何快速学习java技术`

 java历史

 java特点

 sublime

 `java运行机制`

 `jdk`

 转义字符

 `java开发规范`

 java api









#### 变量



 `数据类型`
 变量基本使用
 数据类型转换

#### 运算符



 运算符介绍
 算数运算符
 关系运算符
 逻辑运算符
 赋值运算符
 三元运算符
 优先级
 `二进制`
 位运算符

#### 控制结构



 顺序
 分支（if else switch）
 `循环（for、while、do while）`
 break
 continue
 return

#### 数组、排序、查找



 `数组`
 排序
 查找 

#### 面向对象编程（基础）



 类与对象
 `成员方法`
 `成员方法传参机制`
 overload
 可变参数
 作用域
 构造器
 this

#### 面向对象编程（中级）



 包
 访问修饰符
 `封装`
 `继承`
 `多态`
 super
 overwrite
 object类详解
 断点调试



#### 项目&学以致用，编程之乐



 零钱通

 房屋出租系统
 迷宫问题
 八皇后问题
 汉诺塔问题

### 第二阶段：提升编程能力
#### 面向对象编程（高级）



 `类变量和类方法`
 理解main方法语法
 代码块
 单例设计模式
 final关键字
 抽象类
 `接口`
 `内部类`

#### 枚举和注解



 自定义类实现枚举
 enum关键字实现枚举
 JDK内置的基本注解类型
 元注解：对注解进行注解

#### Exception



 异常的概念
 `异常体系图`
 常见的异常
 `异常处理`
 自定义异常
 throw和throws的对比

#### 常用类



 包装类
 `String`
 `StringBuffer`
 `StringBuilder`
 Math
 Date、Calendar、LocalDate...
 System
 Arrays
 BigInteger BigDecimal

 集合



 `集合框架体系`
 Collection
 List
- `ArrayList`
- LinkedList
- `Vector`


 Set

- `HashSet`
- LinkedHashSet
- TreeSet


 Map

- `HashMap`
- Hashtable
- LinkedHashMap
- TreeMap
- Properties

 Collections

 泛型



 泛型语法
 自定义泛型
 泛型类
 泛型接口
 泛型方法
 泛型继承和通配符

 线程（基础）



 线程介绍

 `线程使用`

- 继承Thread
- 实现Runnable

 线程方法
 线程生命周期

 `Synchronized`

 `互斥锁`

 死锁

 IO流



 文件

- 概念
- 常用操作


 IO流原理及流的分类

 节点流和处理流

 `输入流`

 InputStream

- FileInputStream
- BufferedInputStream
- ObjectInputStream


 Reader

- FileReader
- BufferedReader
- InputStreamReader

 `输出流`

 OutputStream

- FileOutputStream
- BufferedOutputStream
- ObjectOutputStream


 Writer

- FileWriter
- BufferedWriter
- OutputStreamWriter

 Properties类


 坦克大战



#### 第三阶段：分析需求，代码实现能力

 网络编程



 网络基础

 InetAddress

 Socket

 `TCP编程`

- 字节流

- 字符流

 UDP编程

 反射



 反射机制

 Class类

 类的加载

 `反射获取类的结构信息`

- Class
- Field
- Method
- Constructor
- 访问属性
- 访问方法

 mysql基础



后面讲高级篇（优化、集群和项目实战）

 mysql安装和配置
 数据库

- 创建
- 查看、删除数据库
- 备份恢复数据库


 表

- 创建
- 删除
- 修改

 `mysql数据类型`

 `CRUD`

 insert
 update
 delete
 select

- 单表
- 多表


 `函数`

- 统计函数
- 时间日期
- 字符串函数
- 数学函数
- 流程控制

 内连接

 外连接

 约束

- not null
- primary key
- unique
- foreign key
- check
- 自增长

 索引

- 主键索引
- 唯一索引（UNIQUE）
- 普通索引（INDEX）
- 全文索引

 事务

 JDBC和连接池



 JDBC概述

 JDBC快速入门

 `JDBC API`

- PreparedStatement
- DriverManager
- Statement
- ResultSet

 JDBCUtils

 `事务`

 批处理

 `连接池`

- DataSource
- DBCP
- C3P0
- Proxool
- BoneCP
- `Druid`

 Apache-DBUtils

 `DAO增删改查-BasicDao`

 正则表达式



 快速入门

 正则表达式基本语法

 `三个常用类`

- Pattern
- Matcher
- PatternSyntaxException

 `分组、捕获、反向引用`

 `元字符`

- 限定符
- 选择匹配符
- 分组组合和反向引用符
- 特殊字符
- 字符匹配符
- 定位符

 应用实例

 java 8 java11 新特性



 java8新特性

- `lambda`
- `函数式接口`
- 接口静态方法
- 接口默认方法
- 方法引用
- 构造器引用
- `stream API`
- 并行流
- 串行流
- Optional
- 新时间日期API

 java11新特性

 代码层面新特性

- JShell
- `类型推断`
- `集合增强API`
- Stream加强
- 新增字符串处理方法
- Optional加强
- InputStream增强API
- 标准Java异步HTTP客户

 其他新特性

- 简化的编译运行
- 支持Unicode 10
- Epsilon垃圾搜集器
- ZGC
- JFR
- 支持Linux容器
- 支持G1上的并行完全垃圾搜集
- 增加加密算法、代替RC4
- 最新HTTPS安全协议TLS 1.3
- 移除和废弃的内容

 项目



 骑士周游问题

算法、优化

 满汉楼

 多用户通信系统

推消息、私聊、发文件



## java高级

## java web

## 主流的框架和项目管理

## 分布式、微服务、并行架构

## DevOps（开发运维一体化），自动化部分管理项目，解决CI/CD

## 大数据技术

## 项目

## 大厂的高频面试题

## 底层源码、内核研究









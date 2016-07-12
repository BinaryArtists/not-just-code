## ORM

  1. [什么是ORM?](http://www.cnblogs.com/double1030/archive/2009/02/01/1382062.html)

### 简介

  * 对象关系映射（Object Relational Mapping，简称ORM）模式是一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系数据库中。那么，到底如何实现持久化呢？一种简单的方案是采用硬编码方式，为每一种可能的数据库访问操作提供单独的方法。
  * 这种方案存在以下不足：
    1. 持久化层缺乏弹性。一旦出现业务需求的变更，就必须修改持久化层的接口
    2. 持久化层同时与域模型与关系数据库模型绑定，不管域模型还是关系数据库模型发生变化，毒药修改持久化曾的相关程序代码，增加了软件的维护难度。

  * ORM提供了实现持久化层的另一种模式，它采用映射元数据来描述对象关系的映射，使得ORM中间件能在任何一个应用的业务逻辑层和数据库层之间充当桥梁。Java典型的ORM中间件有:Hibernate,ibatis,speedframework。
  * ORM的方法论基于三个核心原则：
　　1. 简单：以最基本的形式建模数据。
　　2. 传达性：数据库结构被任何人都能理解的语言文档化。
　　3. 精确性：基于数据模型创建正确标准化了的结构。

### 概念

  * 让我们从O/R开始。字母O起源于"对象"(Object),而R则来自于"关系"(Relational)。几乎所有的程序里面，都存在对象和关系数据库。在业务逻辑层和用户界面层中，我们是面向对象的。当对象信息发生变化的时候，我们需要把对象的信息保存在关系数据库中。
  * 当你开发一个应用程序的时候(不使用O/R Mapping),你可能会写不少数据访问层的代码，用来从数据库保存，删除，读取对象信息，等等。你在DAL中写了很多的方法来读取对象数据，改变状态对象等等任务。而这些代码写起来总是重复的。

  * ORM解决的主要问题是对象关系的映射。域模型和关系模型分别是建立在概念模型的基础上的。域模型是面向对象的，而关系模型是面向关系的。一般情况下，一个持久化类和一个表对应，类的每个实例对应表中的一条记录，类的每个属性对应表的每个字段。
  * ORM技术特点：
    1. 提高了开发效率。由于ORM可以自动对Entity对象与数据库中的Table进行字段与属性的映射，所以我们实际可能已经不需要一个专用的、庞大的数据访问层。
    2. ORM提供了对数据库的映射，不用sql直接编码，能够像操作对象一样从数据库获取数据。

### 优缺点

  * ORM的缺点是会牺牲程序的执行效率和会固定思维模式。
  * 从系统结构上来看,采用ORM的系统一般都是多层系统，系统的层次多了，效率就会降低。ORM是一种完全的面向对象的做法，而面向对象的做法也会对性能产生一定的影响。

  * 在我们开发系统时，一般都有性能问题。性能问题主要产生在算法不正确和与数据库不正确的使用上。ORM所生成的代码一般不太可能写出很高效的算法，在数据库应用上更有可能会被误用，主要体现在对持久对象的提取和和数据的加工处理上，如果用上了ORM,程序员很有可能将全部的数据提取到内存对象中，然后再进行过滤和加工处理，这样就容易产生性能问题。
  * 在对对象做持久化时，ORM一般会持久化所有的属性，有时，这是不希望的。
  * 但ORM是一种工具，工具确实能解决一些重复，简单的劳动。这是不可否认的。但我们不能指望工具能一劳永逸的解决所有问题，有些问题还是需要特殊处理的，但需要特殊处理的部分对绝大多数的系统，应该是很少的。

  * [ORM需要么](http://www.jdon.com/44208)
    > 在实际开发中只有参与业务逻辑才需真正的对象，因为要规范调用参数或接口，其他情况都不是必须使用对象的。所以我认为大家应该放开思想，不要局限于条条框框。以简洁，高效，实用为目的写程序做设计。所谓的标准也是为达此目的而立的，有悖于此的标准都将被淘汰。

### 现有相关框架

目前众多厂商和开源社区都提供了持久层框架的实现，常见的有：

      Apache OJB （http://db.apache.org/ojb/）
      Cayenne （http://objectstyle.org/cayenne/）
      Jaxor （http://jaxor.sourceforge.net）
      Hibernate （http://www.hibernate.org）
      iBatis （http://www.ibatis.com）
      jRelationalFramework （http://ijf.sourceforge.net）
      mirage （http://itor.cq2.org/en/oss/mirage/toon）
      SMYLE （http://www.drjava.de/smyle）
      TopLink （http://otn.oracle.com/products/ias/toplink/index.html）

### 对象－关系映射模式

从《公共仓库元模型：开发指南》一书第8章CWM元仓库中摘录出来的内容，实现了公共仓库元模型(CWM)的UML图到Microsoft SQL Server数据库的映射，是一种将对象层次结构映射成关系型结构的方法。个人认为可以作为将本体(Ontology)文件存储到关系型数据库中的一种可借鉴方法。

     基本情况：公共仓库元模型(CWM)是对象管理组织(OMG)的一种和数据仓库相关的元模型标准，采用UML表示的对象层次结构，在保存到数据库中时由于面向对象的数据库技术的不完善(理论研究和商业应用都不是主流)，所以该书的作者倾向于使用成熟的关系型数据库来保存－这也是存储本体时所遇到的问题。

     采用方法：将UML模型中的各种元素通过转换，保存为数据库模式。由于CWM是一种元模型，因此模型的实例也是一种模型，将这种实例以数据库数据的形式保存。使用数据库中比较成熟的存储过程技术提高开发和执行效率。

     1、数据类型映射模式

     1.1简单数据类型模式：建立UML和关系型数据库中简单数据类型的映射表以指导映射。
     1.2枚举数据类型模式：每种枚举类型对应一个表，只有一个列(_EnumLiteral_)表示枚举值。
     1.3基于类的数据类型模式：使用外键约束，将基础列与基于类的类型实例相关联。

     2、类映射模型

     每个类对应一个表。单值属性、多值属性、继承关系可以用下述方法映射，而引用属性将在关联映射模式中提到。

     2.1单值属性模式：是cardinality的上界为1的属性，映射到类所对应的表的列上。若其下界也为1（必须有的属性），列属性为NOT NULL。
     2.2多值属性模式：每个多值属性映射成一个独立的表，使用外键连接到类所对应的表上。
     2.3继承模式：每加入一个类的实例时，根据其继承关系自顶向下生成每个类的对象，这些对象具有相同的ID（根对象对应记录的主键）。删除对象实例时，自底向上删除数据。遇到从中间删的情况怎么办？多重继承怎么处理？（金龙飞）

     3、关联映射模式

     3.1一对一关联模式：在关联两端各加一列。
     3.2一对多关联模式：和3.1一样。如果多这端是有序的，还需加入一列表示序号。
     3.3多对多关联模式：将关联单独作一个表。
     3.4组合关联模式：注意级联式删除。
     3.5反演关联模式：关联两端指向相关的类型，和普通关联一样。
     3.6成对关联模式：关联记录两个类间的关系，用交集类表示关联，表示成一个单独的表，每个关联对应一个表，用外键表示它们间的关系。
     3.7关联上的OCL需要分析成对应的存储过程代码。
     3.8保证关联的cardinality也需要分析成对应的存储过程代码。

     4、引用映射模式


     在UML中不存在的MOF特征，指属性是声明为引用类型的实例。用存储过程实现。
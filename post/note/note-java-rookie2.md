# Java新手的通病(2)——缺乏面向对象的基本功

- pubdate: 2015-04-25 14:17:11
- tags: java

1.基于接口的继承(implements)和基于实现的继承(extends)各有什么优点、缺点？

-------------------------

##*1.基于接口的继承(implements)和基于实现的继承(extends)各有什么优点、缺点？*

implements接口实现可以让一个类可以有多种类型（类型丰富），因为java接口实现可以是多个的，缺点就是必须实现接口的所有方法。
extends继承可以重用一些父类的方法（一般抽象类就是实现了一些通用的方法），缺点就是java类只支持单继承（接口之间可以多继承），只有继承了该类的子类才可以被引申为该类型。

##*2.继承(包括extends和implements)有什么缺点?*

extends缺点: 只能单继承，而且类型有限，一个类很难扩充为一个混合类型。　　
implements缺点: 必须实现该接口的所有方法，这就导致如果往一个接口新增一个方法，所有实现该接口的类都必须实现该方法。

##*3.多态（polymorphism）有什么缺点？*

java作为一门面向对象的语言。面向对象的三大特性：封装、继承、多态。可以说封装和继承是为多态服务的，没有继承就没有多态。多态可以提高程序可复用性（抽象类）、可扩充性和可维护性（接口）。

缺点：1.只有非private方法才能被继承，也就是说基类中的private方法的应优先采用不同的名字（用以区别）。2.如果子类和基类拥有相同的成员变量（类型和名字），那么在子类中需要用到基类的该变量需指定super.field,默认的是导出子类的域。

##*4.为什么Java可以多继承interface，而不可以多继承class？*

首先明确一点，java中一个子类只能继承一个父类，但可以实现多个接口。有一种情况很特殊，就是**接口之间可以多继承**。  

为什么不能多继承class：

1.若子类继承的父类中拥有相同的成员变量，子类在引用该变量时将无法判别使用哪个父类的成员变量。　　
2.若一个子类继承的多个父类拥有相同方法，同时子类并未覆盖该方法（若覆盖，则直接使用子类中该方法），那么调用该方法时将无法确定调用哪个父类的方法。

为什么可以多继承interface:

为了拓展子类的功能，Java使用接口以克服不使用多继承带来的不足。接口是一个特殊的抽象类，**接口中成员变量均默认为 static final 类型**，即常量，且接口中的方法都为抽象的，都没有方法体。具体方法只能由实现接口的类实现，**在调用的时候始终只会调用实现类的方法**（不存在歧义），因此不存在多继承的第二个缺点；而又因为接口只有静态的常量，但是由于静态变量是在编译期决定调用关系的，即使存在一定的冲突也会在编译时提示出错；**而引用静态变量一般直接使用类名或接口名，从而避免产生歧义**，因此也不存在多继承的第一个缺点。对于一个接口继承多个父接口的情况也一样不存在这些缺点。


##*5.假如让你写一个小游戏（比如人机对战的五子棋），你会如何设计类结构？*

感觉棋子应该是一个类，它有自己的属性（颜色，位置).棋盘应该是一个类（有大小，用二维数组表示），它有一些自己的行为，比如重置一盘棋,撤销当前操作，判定棋局获胜方等等。

##*6.类结构设计时，如何考虑可扩展性？*

> 1 面向接口的编程
>     接口是一种特殊的抽象类，所有方法都是抽象方法。实现封装隔离
> 2 优先使用对象的组合而非类继承
>   例如
>   class A(){
>           public void t1(){}
>   }
>   class B 想调用A里的方法t1，那么这样写
>   class B(){
>           public void t1(){
>               A a=new A();
>               a.t1();
>           }
>   }
>  
> 3 分层
>   典型三层构架  表现层-->逻辑层-->数据层
>   表现层：展示数据,人机交互，手机参数调用逻辑层
>   逻辑层：进行数据的逻辑校验，逻辑判断，实现业务功能，处理相关功能，处理后续流程，组织数据返    回给表现层
>   数据层：实现数据持久化，实现对象和持久化数据的双向映射
> 4 层间交互的基本原则
>     <1>表现层调用逻辑层，逻辑层调用数据层，不可逆
>     <2>层间交互也通过接口
> 5 开闭原则
>     可以在不改变已有代码的基础上，增加新功能
>     
> 6 依赖性倒置原则
>     依赖抽象而不依赖具体实现
> 7 接口隔离原则
>     不要使用通用接口，为不同用户使用不同接口。就是不要把各个用户不同的需求全放在一个接口里，而是一个用户一个接口。
> 8 替换原则
>     子类应当可以替换父类并出现在父类能够出现的地方

参考网址: [http://blog.163.com/huangbingliang@yeah/blog/static/94161399201072281304/](http://blog.163.com/huangbingliang@yeah/blog/static/94161399201072281304/)

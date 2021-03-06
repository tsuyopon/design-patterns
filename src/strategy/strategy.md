#策略(Strategy)模式
##意图
定义一系列的算法，把它们一个个封装起来，并且使它们可相互替换。策略模式可以使算法可独立于使用它的客户而变化.策略模式变化的是算法

策略模式结构图

![策略模式](./uml2.png "策略模式结构图")

##策略模式中主要角色
* 抽象策略(Strategy）角色：定义所有支持的算法的公共接口。通常是以一个接口或抽象来实现。Context使用这个接口来调用其ConcreteStrategy定义的算法
* 具体策略(ConcreteStrategy)角色：以Strategy接口实现某具体算法
环境(Context)角色：持有一个Strategy类的引用，用一个ConcreteStrategy对象来配置

##策略模式的优点和缺点
###策略模式的优点：
1. 策略模式提供了管理相关的算法族的办法
2. 策略模式提供了可以替换继承关系的办法 将算封闭在独立的Strategy类中使得你可以独立于其Context改变它
3. 使用策略模式可以避免使用多重条件转移语句。

###策略模式的缺点：
1. 客户必须了解所有的策略 这是策略模式一个潜在的缺点
2. Strategy和Context之间的通信开销
3. 策略模式会造成很多的策略类

##策略模式适用场景
1. 许多相关的类仅仅是行为有异。“策略”提供了一种用多个行为中的一个行为来配置一个类的方法
2. 需要使用一个算法的不同变体。
3. 算法使用客户不应该知道的数据。可使用策略模式以避免暴露复杂的，与算法相关的数据结构
4. 一个类定义了多种行为，并且 这些行为在这个类的操作中以多个形式出现。将相关的条件分支移和它们各自的Strategy类中以代替这些条件语句

##策略模式与其它模式
* Template模式：模板方法模式与策略模式的不同在于，策略模式使用委派的方法提供不同的算法行为，而模板方法使用继承的方法提供不同的算法行为
* 享元模式(flyweight模式)：如果有多个客户端对象需要调用 同样的一睦策略类的话，就可以使它们实现享元模式


##一. 举例说明

以前做了一个程序，程序的功能是评价几种加密算法时间，程序的使用操作不怎么变，变的是选用各种算法。

###结构如下：
![结构](./uml1.png)


>Algorithm：抽象类，提供算法的公共接口。

>RSA_Algorithm：具体的RSA算法。

>DES_Algorithm：具体的DES算法。

>BASE64_Algorithm：具体的Base64算法。

在使用过程中，我只需要对外公布Algorithm_Context这个类及接口即可。



它定义了算法家族，分别封装起来，让它们之间可以互相替换，此算法的变化，不会影响到使用算法的客户.

这里的关键就是将算法的逻辑抽象接口（DoAction）封装到一个类中（Context），再通过委托的方式将具体的算法实现委托给具体的 Strategy 类来实现（ConcreteStrategeA类）。
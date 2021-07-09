IOC理论推导（控制思想）

1.UserDao接口
2.UserDaoImpl实现类
3.UserService实现接口
4.UserServiceImpl业务实现类

之前：
程序不能适用与用户的变更
在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改源代码！（会破坏程序完整性）
如果程序代码量十分大，修改一次的成本代价十分昂贵！

private UserDao userDao = new UserDaoOracleImpl();

![image](https://user-images.githubusercontent.com/75358006/124963006-df676480-e051-11eb-9ab9-7f8d4aa7e713.png)


现在：
我们使用一个Set接口实现（已经发生了革命性的变化）

private UserDao userDao;
//利用set进行动态实现值的注入
public void setUserDao(UserDao userDao){
    this.userDao = userDao;
}

![image](https://user-images.githubusercontent.com/75358006/124963045-ec845380-e051-11eb-8c70-91fae9f01a0b.png)



之前，程序是主动创建对象！控制权在程序员手上！--> 用户的每一个需求都会让程序员修改代码
使用了set注入后，程序不再具有主动性，而是变成了被动的接受对象

这种思想从本质上解决了问题，程序员不用再去管理对象的创建（用户调用）了。
系统的耦合性大大降低，可以更加专注地在业务的实现上！这是IOC的原型！

就是控制反转/控制权的反转/获得依赖对象的方式反转

![image](https://user-images.githubusercontent.com/75358006/124963306-39682a00-e052-11eb-849a-2f6164db9df1.png)


IOC本质

IoC是Spring框架的核心内容，使用多种方式完美的实现了IoC，可以使用XML配置，也可以使用注解，新版本的Spring也可以零配置实现IoC。
Spring容器在初始化时先读取配置文件，根据配置文件或元数据创建与组织对象存入容器中，程序使用时再从Ioc容器中取出需要的对象。

![image](https://user-images.githubusercontent.com/75358006/124964039-1e49ea00-e053-11eb-8b9d-ca2f49950e60.png)

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI）。

3.HelloSpring

Hello 对象是谁创建的 ?  hello 对象是由Spring创建的

Hello 对象的属性是怎么设置的 ?  hello 对象的属性是由Spring容器设置的

这个过程就叫控制反转 :

控制 : 谁来控制对象的创建 , 传统应用程序的对象是由程序本身控制创建的 , 使用Spring后 , 对象是由Spring来创建的

反转 : 程序本身不创建对象 , 而变成被动的接收对象 .

依赖注入 : 就是利用set方法来进行注入的.

IOC是一种编程思想，由主动的编程变成被动的接收

可以通过newClassPathXmlApplicationContext去浏览一下底层源码 .

























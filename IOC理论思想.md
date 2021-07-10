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

![image](https://user-images.githubusercontent.com/75358006/125151633-1d5fa800-e17a-11eb-8619-6aa867a18e11.png)

OK , 到了现在 , 我们彻底不用再程序中去改动了 , 要实现不同的操作 , 只需要在xml配置文件中进行修改 , 所谓的IoC,一句话搞定 : 对象由Spring 来创建 , 管理 , 装配 ! 

4.IOC（Spring IOC容器）创建对象的方式

1.使用无参构造方法创建对象，默认实现
2.假设要是用有参构造创建对象
（1）下标赋值
```
<!--有参构造：下标赋值-->
<bean id="user" class="com.kuang.pojo.User">
    <constructor-arg index="0" value="yyLEARN"/>
</bean>
```

（2）类型
```
<!--第二种，通过类型创建，不建议使用，只支持一个参数-->
<bean id="user" class="com.kuang.pojo.User">
    <constructor-arg type="java.lang.String" value="yylearn2"/>
</bean>
```

（3）参数名
```
<!--第三种，直接通过参数名来设置-->
<bean id="user" class="com.kuang.pojo.User">
    <constructor-arg name="name" value="yylearn0"/>
</bean>
```


总结：在配置文件加载的时候，容器中管理的对象bean就已经初始化了

5.Spring配置

5.1 别名
```
<!--别名，如果添加了别名，也能获取出来-->
<alias name="user" alias="vivian"/>
```


5.2 Bean的配置
```
<!--没有用userT，对象也被创建了
id：bean的唯一标识符，也就是相当于我们学的对象名
class：bean对象所对应的全限定名：包名+类型
name：也是别名，而且name可以同时取多个别名-->
<bean id="userT" class="com.kuang.pojo.UserT" name="user2 u3,u4;u4"><!--空格，逗号，分号都可以分割-->
     <property name="name" value="不知道叫啥了"/>
</bean>
```


5.3 import
一般用于团队开发使用，可以将多个配置文件导入合并为一个
假设，现在项目中有多个人进行开发，这三个人负责不同的类开发，不同的类需要注册在不同的bean中，我们可以利用import将所有人的beans.xml合并为一个总的！使用的时候，直接使用总的配置就可以了
-张三
-李四
-王五
-applicationContext.xml
```
<!--三个配置被合并-->
<import resource="beans.xml"/>
<import resource="beans2.xml"/>
<import resource="beans3.xml"/>
```

6.DI依赖注入


6.1 构造器注入
前面讲过

6.2 Set方式注入（重点）
* 依赖注入：Set方法注入！
* 依赖：bean对象的创建依赖于容器
* 注入：bean对象中的所有属性，由容器来注入

【环境搭建】
1.复杂类型
```

public class Address {

    private String address;

    public String getAddress() {
        return address;
    }
    
    public void setAddress(String address) {
        this.address = address;
    }
}

```
2.真实测试对象

```
public class Student {

    private String name;
    private Address address;
    private String[] books;
    private List<String> hobbies;
    private Map<String,String> card;
    private Set<String> games;
    private String wife;
    private Properties info;
}
```
3.beans.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--怎样注入所有的值-->

    <!--第一种，普通值注入，value-->
    <bean id="student" class="com.kuang.pojo.Student">
        <property name="name" value="vivian"/>
    </bean>

</beans>
```

4.测试类
```
public class MyTest {

    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

        Student student = (Student) context.getBean("student");
        System.out.println(student.getName());

    }
}
```

5.完善注入信息
```
<bean id="address" class="com.kuang.pojo.Address">
        <property name="address" value="西安"/>
    </bean>

    <bean id="student" class="com.kuang.pojo.Student">
        <!--第一种，普通值注入，value-->
        <property name="name" value="vivian"/>
        <!--第二种，bean注入，ref-->
        <property name="address" ref="address"/>

        <!--数组注入，ref-->
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>西游记</value>
                <value>水浒传</value>
                <value>三国演义</value>
            </array>
        </property>

        <!--List-->
        <property name="hobbies">
            <list>
                <value>听歌</value>
                <value>敲代码</value>
                <value>看电影</value>
            </list>
        </property>

        <!--Map-->
        <property name="card">
            <map>
                <entry key="身份证" value="11111111111111"/>
                <entry key="银行卡" value="1233456789"/>
                <entry key="" value=""/>
            </map>
        </property>

        <!--Set-->
        <property name="games">
            <set>
                <value>LOL</value>
                <value>COC</value>
                <value>BOB</value>
            </set>
        </property>

        <!--null
        <property name="wife" value=""/>
        -->
        <property name="wife">
            <null/>
        </property>

        <!--properties
        key=value-->
        <property name="info">
            <props><!--属性配置+多个项-->
                <prop key="driver">20210710</prop>
                <prop key="url">男</prop>
                <prop key="username">小明</prop>
                <prop key="password">123456</prop>
            </props>
        </property>

    </bean>
```




6.3 拓展方式注入

我们可以使用p命名空间和c命名空间进行注入

官方解释：
![image](https://user-images.githubusercontent.com/75358006/125164836-e4015980-e1c6-11eb-96dc-33045b29b4b3.png)

使用：
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入，可以直接注入属性，但要依赖第三方的约束-->
    <bean id="user" class="com.kuang.pojo.User" p:name="vivian" p:age="18"/>

    <!--c命名空间注入，可以通过构造器注入：constructor-args-->
    <bean id="user2" class="com.kuang.pojo.User" c:age="18" c:name="yy"/>

</beans>
```

测试：

```
@Test
public void test2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    //显式的声明了类型，不用每次进行强转
    User user = context.getBean("user", User.class);
    System.out.println(user);

    User user2 = context.getBean("user2", User.class);
    System.out.println(user2);
}
```

注意点：p命名和c命名空间不能直接使用，需要导入xml约束！
'''
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
'''


6.4 bean的作用域

![image](https://user-images.githubusercontent.com/75358006/125169411-9d1e5e80-e1dc-11eb-8cd6-1656d6786457.png)

1.单例模式（Spring默认机制）
![image](https://user-images.githubusercontent.com/75358006/125169508-2170e180-e1dd-11eb-9ec9-bd4ebfb58f49.png)
每个都引用的是同一个对象
```
<bean id="user2" class="com.kuang.pojo.User" c:age="18" c:name="yy" scope="singleton"/>
```
2.原型模式：每次从容器中get的时候，都会产生一个新对象
![image](https://user-images.githubusercontent.com/75358006/125169512-23d33b80-e1dd-11eb-9534-ea7d66360899.png)
每个都创建新的对象
```
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
```
3.其余的request（创建完对象）、session（session中）、application（全局），这些只能在web开发中使用到











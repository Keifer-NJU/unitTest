# Junit 单元测试

## 总结清单

- 测试方法必须是public void，即公共、无返回数据。可以抛出异常。
- **类名：** 定义测试类，类名是由`被测试类名Test`构成。例如：CalculatorTest
- **包名：** 定义的测试类需要放在`xxx.xxx.xxx.test`包中。例如：package com.mylifes1110.test;
- **方法名：** 测试方法的方法名有两种定义方式`test测试方法`和`测试方法`。例如：testAdd和add
- **返回值：** 因为我们的方法只是在类中测试，可以独立运行，所以不需要处理任何返回值，所以这里使用`void`。例如：public void add();
- **参数列表：** 因为我们的方法是用来测试的，至于参数列表的传入是没有必要的。我们在测试的时候自行传入需要的参数测试即可。所以在此参数列表为`空`。例如：例如：public void add();
- **@Test注解：** 测试是需要运行来完成的。如果我们只有一个main方法，显然在结构上还是需要我们去注释掉测试过的。解决此问题这里我们需要在测试方法上方加`@Test`注解来完成测试，只要是加该注解的方法，可以单独运行此方法来完成测试。
- **@Test注解jar包Junit4、5：** @Test注解是需要我们导入jar包才能使用的。jar包有两个分别是：`junit-4.13-rc-2`和`hamcrest-core-1.3`。这里我使用的是Junit4，单元测试还有Junit5，版本差异我没有做了解。主要是可以完成测试才是硬道理！
- **IDEA快捷导入Junit4、5：** 使用IDEA的小伙伴，你们的福音来了。我们可以先创建测试类和方法，然后在测试方法上方加入`@Test`注解，此时IDEA显示的@Test注解是飘红的，这时候我们使用`Alt + Enter`组合键来打开导入Junit单元测试列表，然后再选择Junit4或者Junit5确定即可导入成功！这时候再查看注解就没有飘红了！

## 普通使用

https://juejin.cn/post/6844903791494447112#heading-10

https://www.bilibili.com/video/av54938732/?p=5



## Springboot 的单元测试和集成测试实践及采坑过程

### 单元测试 

**创建快捷键：在需要添加测试的类中使用：shift+ctrl+t**  

**测试框架使用Junit, 模拟框架使用mockito**



SpringBoot创建的Maven项目中，会默认添加spring-boot-starter-test依赖。

Spring Boot 提供了一个强大的类以使测试变得简单：[@SpringBootTest](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/context/SpringBootTest.html) 注解

#### Junit 框架

注解—执行顺序——断言

**Hamcrest框架和assertThat：**

1.JUnit4.4引入了Hamcrest框架，Hamcest提供了一套匹配符Matcher，这些匹配符更接近自然语言，可读性高，更加灵活；
2.使用全新的断言语法：assertThat，结合Hamcest提供的匹配符，只用这一个方法，就可以实现所有的测试；
3.assertThat语法如下：
   assertThat(T actual, Matcher<T> matcher);
   assertThat(String reason, T actual, Matcher<T> matcher);
   其中actual为需要测试的变量，matcher为使用Hamcrest的匹配符来表达变量actual期望值的声明；
4.注意事项：
   a.必须导入JUnit4.4之后的版本才能使用assertThat方法；
   b.不需要继承TestCase类，但是需要测试方法前必须加“@Test”。

#### 模拟框架 mockito

**使用Mockito一般分三个步骤：**

**1、模拟测试类所需的外部依赖的Mock对象，然后将此Mock对象注入到测试类中；**

**2、执行测试代码；**

**3、判断执行结果是否达到预期；**

**1、[JUnit+Mockito单元测试之打桩when().thenReturn()](https://blog.csdn.net/moshowgame/article/details/100983711);**

- **什么是Mock 测试**

  Mock 测试就是在测试过程中，对于某些`不容易构造`（如 HttpServletRequest 必须在Servlet 容器中才能构造出来）或者`不容易获取`的对象（如 JDBC 中的ResultSet 对象,JPA的CRUDRepository,需要执行数据库操作的），用一个虚拟的对象（Mock 对象）来创建（覆盖方法返回）以便测试的测试方法。

  在以下情况可以采用模拟对象来替代真实对象：

  - 真实对象的行为是不确定的（例如，当前的时间或温度）；
  - 真实对象很难搭建起来；
  - 真实对象的行为很难触发（例如，网络错误）；
  - 真实对象速度很慢（例如，一个完整的数据库，在测试之前可能需要初始化）；
  - 真实的对象是用户界面，或包括用户界面在内；
  - 真实的对象使用了回调机制；
  - 真实对象可能还不存在；
  - 真实对象可能包含不能用作测试（而不是为实际工作）的信息和方法。

**Stub 打桩**

**注意：只能对mock对象进行stub。**

Mockito 中 `when().thenReturn();` 这种语法来定义对象方法和参数（输入），然后在 thenReturn 中指定结果（输出）。此过程称为 `Stub 打桩` 。一旦这个方法被 stub 了，就会一直返回这个 stub 的值。

`!!!`Stub 打桩 需要注意的是:

1. 对于 static 和 final 方法， Mockito 无法对其 when(…).thenReturn(…) 操作。
2. 当我们连续两次为同一个方法使用 stub 的时候，他只会只用最新的一次。

- **迭代打桩**
- **void如何打桩**
- **抛出异常**
- **Any()**

**2、[SpringBoot基础之MockMvc单元测试](https://zhuanlan.zhihu.com/p/61342833)**

MockMvc是由spring-test包提供，**实现了对Http请求的模拟，能够直接使用网络的形式，转换到Controller的调用，使得测试速度快、不依赖网络环境。**同时提供了一套验证的工具，结果的验证十分方便。

**即针对以下代码，需模拟发出/listAll的http请求，用MockMvc**

```java
@RequestMapping(value = "listAll", method = RequestMethod.GET)
    @ResponseBody
    public List<PmsBrand> getBrandList(){
        return pmsBrandService.listAllBrand();
    }
```

**3、MockBean的作用与危害**

**作用：https://juejin.cn/post/6844903924248346637#heading-7**

1. **Mock 数据**

   在单元测试中，Service 层的调用往往涉及到对数据库、中间件等外部依赖。而在单元测试 AIR 原则中，单元测试应该是可以重复执行的，不应受到外界环境的影响的。此时我们可以通过 Mock 一个实现来处理这种情况。

   **如果不需要对静态方法，私有方法等特殊进行验证测试，则仅仅使用 Spring boot 自带的 Mockito 即可完成相关的测试数据 Mock。若需要则可以使用 PowerMock，简单实用，结合 Spring 可以使用注解注入。**

2. **SpringBoot 在执行单元测试时，会将该注解的 Bean 替换掉 IOC 容器中原生 Bean。**

**危害：https://segmentfault.com/a/1190000014122154**

​	@MockBean会改变springboot application context 中的bean， 导致使用了@MockBean的测试类之间需要不同的application context, 从而导致springboot 	application context 重启，也就会导致变慢。

​	因此，测试时需要了解依赖边界，不需要Mock的，就不要Mock, 比如： service, repository等，对于外部依赖，统一在配置层完成mock，比如：client, redis, 	rabbitmq等

# 测试覆盖检查 Jacoco

- **[官网](https://www.eclemma.org/jacoco/)**

- **[测试报告解读](https://www.jianshu.com/p/96271d21bf38)**

- **[测试覆盖统计原理](https://www.jianshu.com/p/50c5cc021396)**
  - JaCoCo主要通过代码注入的方式来实现上面覆盖率的功能
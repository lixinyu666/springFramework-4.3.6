


#Part I. Spring框架概述
<br/>
Spring框架是一个轻量级和一个一站式的解决方案，以构建您的企业就应用程序。然而，Spring是模块化的，允许您只使用那些您需要的部分，而不必使用其余的部分。你可以在任何web框架上使用IoC容器，也可以只使用Hibernate集成代码或JDBC抽象层。Spring框架支持声明式事务管理，通过RMI或Web服务的远程访问你的应用程序的逻辑，并且支持多种持久化数据的方式。它提供了一个功能齐全的MVC框架，并且能够透明地集成AOP到您的软件实现。

Spring被设计成非侵入性的，这意味着你的逻辑代码通常情况下不依赖于框架本身。在您的集成层（如数据访问层），将会存在一些数据访问技术的依赖和Spring的库。不管怎样，从你其余的代码中分离这些依赖应该是很容易的。

本文档是Spring框架功能的参考指南。如果您对该文档有任何请求、评论或问题，请将其张贴在用户邮件列表上。对框架本身的问题应该问在StackOverflow (see https://spring.io/questions)。
<br/>

##1. 开始使用Spring
<br/>
本参考指南提供有关Spring框架的详细信息。它提供了所有功能的全面文档，以及Spring提供的基本概念（如“依赖注入”）的一些背景。

如果您刚开始使用Spring，您也许应该通过创建Spring Boot应用程序开始使用Spring框架。Spring Boot提供了一个快速（和武断的）的方法来创建用于生产环境的基于Spring的应用。它是基于Spring框架的，支持约定大于配置，被设计为可以快速启动并且尽可能快的运行起来。

你可以使用[start.spring.io](http://start.spring.io/)生成一个基本的项目或遵循“[Getting Started](https://spring.io/guides)”指南中的一个，例如[指导构建一个RESTful 风格的Web服务](https://spring.io/guides/gs/rest-service/)指南。除了容易理解吸收之外，这些指南主要是基于任务的，它们中的大多数是基于Spring Boot的。它们也包含了Spring的其它工程，当解决一个特定问题时你可能会考虑它们。
<br/>

##2. Spring框架介绍
<br/>
Spring框架是一个为开发java应用的综合基础架构提供支持的java平台。Spring处理基础架构，以便您可以专注于应用程序。

Spring使你能创建“普通java对象构建应用程序”(POJOs)并能非侵入式的将企业服务应用到普通Java对象(POJOs)上。
此功能完全适用于Java SE项目模型，部分适用于java EE。

作为应用程序开发人员，您可以从Spring平台获益的例子：

* 在一个数据库事务中执行一个Java方法而不必处理事务APIs 
* 使一个本地的Java方法可以远程调用而不必处理远程APIs 
* 使一个本地Java方法变为管理操作而不必处理JMX APIs 
* 使一个本地Java方法变为消息处理器而不必处理JMS APIs
<br/>

##2.1 依赖注入与控制反转
<br/>
Java应用——一个不精确的术语，既可以表示受限制的嵌入式应用又可以表示N层服务端的企业级应用——通常由许多对象构成，这些对象协作形成完整的应用程序。因此一个应用程序中的对象是相互依赖的。

尽管Java平台提供了丰富的应用开发功能，但是它缺少把这些基本构建模块组织成一个连贯整体的方法，并把组织基本构建模块的任务留给了架构师和开发者。虽然你可以使用设计模式例如工厂模式、抽象工厂模式、生成器模式、装饰模式、服务定位模式来创建构成应用的各种类和对象实例，但这些设计模式很简单：命名的最佳方法、模式的作用描述、应用模式的位置、模式解决的问题等等。模式使最佳实践形式化了，这意味着你必须在你的应用中自己实现它。

Spring框架中的控制反转(IoC)组件通过提供一种形式化方法解决了这个问题，这个形式化方法将不同的组件创建到一个随时可用的完整的工作应用中。Spring框架将形式化的设计模式编码成了你可以集成到你自己的应用中的最好对象。许多组织和机构用这种方式应用Spring框架来构建鲁棒的、可维护的应用。

>    
`背景`
“问题是什么是控制反转？” 2004年Martin Fowler在他的网站上提出了这个关于控制反转(IoC)问题。Fowler建议重新命名这个原理使它更一目了然并且提出了依赖注入。

<br/>

##2.2 模块
<br/>
Spring框架包含的功能大约由20个模块组成。这些模块按组可分为核心容器、数据访问/集成，Web，AOP(面向切面编程)、设备、消息和测试，如下图所示。
<br/>
**Spring框架概述**

![Spring框架概述](/assets/spring-overview.png)

接下来的章节列出了每个功能可用的模块、它们的工件名字以及它们包含的主题。工件名字与[依赖管理工具](#2.2.1-核心容器)中使用的artifact IDs有关。
<br/>

###2.2.1 核心容器

[核心容器](README.md#2.2.1-核心容器)功能包括`spring-core`, `spring-beans`, `spring-context`, `spring-context-support`, 和 `spring-expression(Spring表现语言)`模块。

`spring-core`和`spring-beans`模块[提供了框架的基础结构部分](README.md#2.2.1-核心容器)，包含控制反转(IoC)和依赖注入(DI)功能。BeanFactory是工厂模式的高级实现。它去掉了程序单例模式的需求并且允许你从实际的程序逻辑中解耦配置和依赖关系。

上下文(`spring-context`)模块建立在由[Core模块和Beans模块](README.md#2.2.1-核心容器)提供的坚实基础上：它是在类似于JNDI注册表式的框架风格模式中访问对象的一种方法。上下文模块继承了Beans模块的功能，并添加了对国际化（例如使用资源捆绑）、事件传播、资源加载和上下文透明创建（例如通过Servlet容器）的支持。上下文模块也支持Java EE功能例如EJB，JMX和基本的远程。`ApplicationContext`接口是上下文模块的焦点。`spring-context-support`支持将缓存(EhCache, Guava, JCache), 邮件(JavaMail),调度(CommonJ, Quartz)和模板引擎(FreeMarker, JasperReports, Velocity)等第三方库集成进Spring应用程序上下文中。

`spring-expression`模块提供了强大的[表达式语言](README.md#2.2.1-核心容器)用来在运行时查询和操作对象图。它是JSP 2.1规范中统一表达式语言(unified EL)的扩展。这个语言支持setting和getting属性值，属性分配，方法调用，访问数组、集合和索引器的内容，逻辑和算术操作，变量命名，从Spring Ioc容器中通过名字检索对象。它也支持它还支持列表投影、选择以及常见的列表聚合。
<br/>

###2.2.2 AOP和仪器

`spring-aop`模块提供了[AOP](README.md#2.2.1-核心容器) Alliance-compliant(AOP联盟)面向切面编程的实现，例如允许你自定义方法拦截器和切入点来清晰的解耦功能实现上应该分开的代码。使用源码级的元数据功能，你也可以将行为信息合并到你的代码中，在某种程度上这类似于.NET的属性值。

独立的`spring-aspects`模块提供了与AspectJ的集成。

`spring-instrument`模块提供了类设备支持和类加载器的实现，它们可以在某些应用服务器中使用。`spring-instrument-tomcat`模块包含了Tomcat的Spring设备代理。
<br/>
###2.2.3 信息

Spring 4框架中包含了`spring-messaging`模块，它对Spring集成项目例如`Message`, `MessageChannel`, `MessageHandler`和其它作为消息应用服务基础的项目进行了重要的抽象。这个模块也包含了一系列将消息映射到方法上的注解，这个注解与基于编程模型Spring MVC注解类似。
<br/>

###2.2.4 数据访问/集成

数据访问/集成层包括JDBC,ORM,OXM,JMS和业务模块。

`spring-jdbc`模块提供了[JDBC](#README.md#2.2.1-核心容器)抽象层，不需要再编写单调的JDBC代码，解析数据库提供商指定的错误编码。

`spring-tx`模块为实现指定接口和所有的普通Java对象(POJOs)的类提供[编程式(programmatic)和声明式(declarative)的业务管理](#README.md#2.2.1-核心容器)。

`spring-orm`模块提供流行的[对象关系映射](#README.md#2.2.1-核心容器)APIs的集成层，包括[JPA](#README.md#2.2.1-核心容器), [JDO](#README.md#2.2.1-核心容器)和[Hibernate](#README.md#2.2.1-核心容器)。在使用`spring-orm`模块时，你可以将Spring的其它功能与这些O/R-mapping框架结合起来使用，例如前面提到的简单声明式业务管理的功能。

`spring-oxm`模块提供对[Object/XML映射](#README.md#2.2.1-核心容器)实现例如JAXB，Castor，XMLBeans, JiBx和XStream的抽象层。

`spring-jms`模块（[Java消息服务](#README.md#2.2.1-核心容器)）包含产生和处理消息的功能。从Spring 4.1框架开始它提供了与`spring-messaging`的集成。
<br/>

###2.2.5 Web

网络层包含`spring-web`, `spring-webmvc`, `spring-websocket`和`spring-webmvc-portlet`模块。

`spring-web`模块提供基本的面向网络集成功能，例如multipart文件上传功能，使用Servlet监听器来初始化Ioc容器和面向网络的应用程序上下文。它也包含了HTTP客户端和Spring远程支持中网络相关的部分。

`spring-webmvc`模块（也被称为Web-Servlet模块）包含了Spring的model-view-controller([MVC](#README.md#2.2.1-核心容器))和REST Web Services的网络应用实现。Spring的MVC框架提供了对领域模型代码，web表单，Spring框架其他功能的完全分离。

`spring-webmvc-portlet`组件（也被称为Web-Portlet模块）提供MVC的实现，被用于Portlet环境的`spring-webmvc`模块功能的镜像。
<br/>

###2.2.6 Test

`spring-test`模块支持[单元测试](#README.md#2.2.1-核心容器)，Spring组件和JUnit或TestNG的[集成测试](#README.md#2.2.1-核心容器)。它提供了Spring的`ApplicationContext`s [加载](#README.md#2.2.1-核心容器)和这些上下文[缓存](#README.md#2.2.1-核心容器)的一致。它也提供了可以单独测试代码的[模拟对象](#README.md#2.2.1-核心容器)。
<br/>

##2.3 使用场景
<br/>
前面描述的搭积木方式使Spring在许多场景中都有一个合理选择，从运行在资源受限的嵌入式应用到全面成熟的企业级应用都在使用Spring的业务管理功能和网络框架集成。
<br/>
**下图是典型的、成熟的Spring web应用**

![典型的、成熟的Spring web应用](/assets/overview-full.png)

Spring的[声明式业务管理功能](#README.md#2.2.1-核心容器)使web应用全面的业务化，如果你用过EJB容器管理业务的话你会发现它们基本一样。你所有自定义的业务逻辑都可以用POJOs实现并通过Spring的IoC容器管理。附加业务包括支持邮件发送和验证，这个是独立于web层之外的，你可以自由选择验证规则执行的位置。Spring对ORM的支持与JPA和Hibernate进行了集成；例如，当你使用Hibernate时，你可以继续使用你现有的映射文件和标准的Hibernate `SessionFactory`配置。表单控制器被无缝的将web层和领域模型进行了集成，对于你的领域模型来讲不再需要`ActionForms`或其它的将HTTP参数转换成值的。

**下图是使用第三方Web框架的Spring中间层**

![使用第三方Web框架的Spring中间层](/assets/overview-thirdparty-web.png)

有时，不允许你完全切换到一个不同的框架。Spring 框架不强制使用它,它不是一个全有或全无的解决方案。现有的前端 Struts, Tapestry, JSF 或其他 UI 框架，可以集成一个基于 Spring 中间件，它允许你使用 Spring 事务的功能。你只需要将业务逻辑连接使用 `ApplicationContext` 和使用 `WebApplicationContext`集成到你的 web 层。


**下图是远程使用场景**

![远程使用场景](/assets/overview-remoting.png)

当你需要通过 web 服务访问现有代码时，可以使用 Spring 的 `Hessian-`, `Burlap-`, `Rmi-` 或 `JaxRpcProxyFactory` 类。启用远程访问现有的应用程序并不难。


**下图是EJBs-包装现有的POJOs**

![EJBs-包装现有的POJOs](/assets/overview-ejb.png)

Spring 框架也提供了 Enterprise JavaBeans [访问和抽象层](#README.md#2.2.1-核心容器)，使你能重用现有的 POJOs,并且在需要声明安全的时候打包他们成为无状态的 bean 用于可伸缩，安全的 web 应用里。
<br/>


###2.2.1 依赖管理和命名约定

依赖管理和依赖注入是不同的概念。为了让 Spring 的这些不错的功能运用到运用程序中（比如依赖注入），你需要收集所有的需要的库（JAR文件），并且在编译、运行的时候将它们放到你的类路径中。这些依赖不是虚拟组件的注入，而是物理的资源在文件系统中（通常）。依赖管理过程包括定位这些资源，存储它们并添加它们到类路径。依赖可以是直接（如我的应用程序运行时依赖于 Spring ），或者是间接（如我的应用程序依赖 `commons-dbcp` ，而 `commons-dbcp` 又依赖于 `commons-pool`）。间接的依赖也被称为 “transitive （传递）”，它是最难识别和管理的依赖。

如果你将使用 Spring，你需要复制哪些包含你需要的 Spring 功能的 jar包。为了使这个过程更加简单，Spring 被打包为一组模块，这些模块尽可能多的分开依赖关系。例如，如果不想写一个 web 应用程序，你就不需要引入 Spring-web 模块。为了在本指南中标记 Spring 库模块我们使用了速记命名约定 `spring-*` 或者 `spring-*.jar` ，其中`*`代表模块的短名（比如 `spring-core`,`spring-webmvc`, `spring-jms` 等）。实际的jar 文件的名字，通常是用模块名字和版本号级联（如spring-core-4.1.4.BUILD-SNAPSHOT.jar）。

每个 Spring Framework 发行版本将会放到下面的位置：

*    Maven Central （Maven 中央库），这是 Maven 查询的默认库，而不需要任何特殊的配置就能使用。许多常用的 Spring 的依赖库也存在与Maven Central ，并且 Spring 社区的很大一部分都使用 Maven 进行依赖管理，所以这是最方便他们的。jars 命名格式是 `spring-*-<version>.jar` ， Maven groupId 是`org.springframework`。
*    公共 Maven 仓库还拥有 Spring 专有的库。除了最终的 GA 版本，这个库还保存开发的快照和里程碑。JAR 文件的名字是和 Maven Central 相同的形式，所以这是让 Spring 的开发版本使用其它部署在 Maven Central 库的一个有用的地方。该库还包含一个用于发布的 zip 文件包含所有Spring jar，方便下载。

所以首先，你要决定用什么方式管理你的依赖，通常建议你使用自动系统像 Maven, Gradle 或 Ivy, 当你也可以下载 jar。

下面是 Spring 中的组件列表。更多描述，详见[2.2. 模块](#README.md#2.2.1-核心容器)。

**Table 2.1. Spring Framework Artifacts**

![Spring Framework Artifacts](/assets/粘贴图片.png)

**spring的依赖和依赖spring**

虽然Spring提供了大量对企业和其他外部工具的集成和支持，它有意地将其强制依赖保持在绝对最低限度：你无需查找和下载（甚至自动）大量的jar库，以便 使用Spring的简单用例。 对于基本依赖注入，只有一个强制性的外部依赖，这是用于日志记录的（有关日志选项的更详细描述，请参见下文）。

接下来，我们概述配置依赖于Spring的应用程序所需的基本步骤，首先使用Maven，然后使用Gradle，最后使用Ivy。 在所有情况下，如果有什么不清楚，请参考依赖管理系统的文档，或者查看一些示例代码 - Spring本身使用Gradle在构建时管理依赖关系，我们的示例主要使用Gradle或Maven。

**Maven 依赖管理**

如果你使用Maven进行依赖关系管理，你甚至不需要显式提供日志记录依赖关系。 例如，要创建应用程序上下文并使用依赖注入来配置应用程序，你的Maven依赖关系将如下所示：

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.7.RELEASE</version>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

就是这样。注意，如果不需要针对Spring API进行编译，范围(scope)可以声明为运行时(runtime)，这通常是基本依赖注入使用用例。

上面的示例使用Maven Central存储库。 要使用Spring Maven存储库（例如，用于里程碑或开发人员快照），你需要在Maven配置中指定存储库位置。完整版本：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.release</id>
        <url>http://repo.spring.io/release/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

里程碑：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.milestone</id>
        <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

以及快照：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.snapshot</id>
        <url>http://repo.spring.io/snapshot/</url>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
```

**Maven的“物料清单”的依赖**

在使用Maven时，可能会意外混合不同版本的Spring JAR。例如，你可能会发现第三方库或另一个Spring项目将传递依赖项拉入旧版本。 如果你忘记自己显式声明一个直接依赖，可能会出现各种意想不到的问题。
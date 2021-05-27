### Swagger2文档



>Swagger 3.0 发布已经有一段时间了，它于 2020.7 月 发布，但目前市面上使用的主流版本还是 Swagger 2.X 版本和少量的 1.X 版本，然而作为一名合格的程序员怎么能不折腾新技术呢？所以本期就大家带来一篇最新版 Swagger 的内容，本文会带大家看最新版 Swagger 有哪些改变？又是如何将老版本 Swagger 升级到新版的？
>
>## Swagger 是什么？
>
>Swagger 是一个用于生成、描述和调用 RESTful 接口的 Web 服务。通俗的来讲，Swagger 就是将项目中所有（想要暴露的）接口展现在页面上，并且可以进行接口调用和测试的服务。
>
>> PS：Swagger 遵循了 OpenAPI 规范，OpenAPI 是 Linux 基金会的一个项目，试图通过定义一种用来描述 API 格式或 API 定义的语言，来规范 RESTful 服务开发过程。
>
>Swagger 官网地址：https://swagger.io/
>
>## Swagger 有什么用？
>
>从上述 Swagger 定义我们不难看出 Swagger 有以下 3 个重要的作用：
>
>1. **将项目中所有的接口展现在页面上**，这样后端程序员就不需要专门为前端使用者编写专门的接口文档；
>2. 当接口更新之后，只需要修改代码中的 Swagger 描述就可以实时生成新的接口文档了，从而**规避了接口文档老旧不能使用的问题**；
>3. 通过 Swagger 页面，我们可以**直接进行接口调用，降低了项目开发阶段的调试成本**。
>
>## Swagger 旧版本使用
>
>Swagger 旧版本也就是目前市面上主流的 V2 版本是 Swagger 2.9.2，在讲新版本之前，我们先来回顾一下 Swagger 2.9.2 是如何使用的。
>
>Swagger 2.9.2 的使用分为以下 4 步：
>
>1. 添加依赖
>2. 开启 Swagger 功能
>3. 配置 Swagger 文档摘要信息
>4. 调用接口访问
>
>下面我们分别来看。
>
>#### 1.添加依赖
将这两个依赖添加带项目中：
>
>```java
><!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
><dependency>
>    <groupId>io.springfox</groupId>
>    <artifactId>springfox-swagger2</artifactId>
>    <version>2.9.2</version>
></dependency>
>
><!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
><dependency>
>    <groupId>io.springfox</groupId>
>    <artifactId>springfox-swagger-ui</artifactId>
>    <version>2.9.2</version>
></dependency>
>```
>
>#### 为什么是“springfox”？
>
>问：我们要使用的是 Swagger，为什么要搜索“springfox”？
>
>答：**Swagger 可以看作是一个遵循了 OpenAPI 规范的一项技术，而 springfox 则是这项技术的具体实现。** 就好比 Spring 中的 AOP 和 DI 一样，前者是思想，而后者是实现。
>
>#### 2.开启Swagger
>
>在 Spring Boot 的启动类或配置类中添加 `@EnableSwagger2` 注释，开启 Swagger，部分核心代码如下：
>
>```java
>@EnableSwagger2
>@SpringBootApplication
>public class Application {...
>```
>
>#### 3.配置摘要信息
>
>```java
>import org.springframework.context.annotation.Bean;
>import org.springframework.context.annotation.Configuration;
>import springfox.documentation.builders.RequestHandlerSelectors;
>import springfox.documentation.spi.DocumentationType;
>import springfox.documentation.spring.web.plugins.Docket;
>import springfox.documentation.swagger2.annotations.EnableSwagger2;
>
>@Configuration
>public class SwaggerConfig {
>    @Bean
>    public Docket createRestApi() {
>        return new Docket(DocumentationType.SWAGGER_2) // 1.SWAGGER_2
>                .select()
>                .apis(RequestHandlerSelectors.basePackage("com.example.swaggerv2.controller")) // 2.设置扫描路径
>                .build();
>    }
>}
>```
>
>#### 4.访问Swagger
>
>项目正常启动之后使用“http://localhost:8080/swagger-ui.html”访问Swagger页面，如下图所示：
>![image.png](https://cdn.nlark.com/yuque/0/2021/png/92791/1615728303023-5e55240b-f22b-4ae5-8846-e8ce343c19f0.png#align=left&display=inline&height=563&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1126&originWidth=2928&size=143162&status=done&style=none&width=1464)
>
>## Swagger 最新版使用
>
>Swagger 最新版的配置步骤和旧版本是一样，只是每个具体的配置项又略有不同，具体步骤如下。
>
>#### 1.添加依赖
>
>```xml
><!-- https://mvnrepository.com/artifact/io.springfox/springfox-boot-starter -->
><dependency>
>  <groupId>io.springfox</groupId>
>  <artifactId>springfox-boot-starter</artifactId>
>  <version>3.0.0</version>
></dependency>
>```
>
>从上述配置可以看出，Swagger 新版本的依赖项只有一个，而旧版本的依赖项有两个，相比来说也简洁了很多。
>
>#### 2.开启Swagger
>
>在 Spring Boot 的启动类或配置类中添加 `@EnableOpenApi` 注释，开启 Swagger，部分核心代码如下：
>
>```java
>@EnableOpenApi
>@SpringBootApplication
>public class Application {...
>```
>
>#### 3.配置摘要信息
>
>```java
>import org.springframework.context.annotation.Bean;
>import org.springframework.context.annotation.Configuration;
>import springfox.documentation.builders.RequestHandlerSelectors;
>import springfox.documentation.oas.annotations.EnableOpenApi;
>import springfox.documentation.spi.DocumentationType;
>import springfox.documentation.spring.web.plugins.Docket;
>
>@Configuration
>public class SwaggerConfig {
>    @Bean
>    public Docket createRestApi() {
>        return new Docket(DocumentationType.OAS_30) // v2 不同
>                .select()
>                .apis(RequestHandlerSelectors.basePackage("com.example.swaggerv3.controller")) // 设置扫描路径
>                .build();
>    }
>}
>```
>
>从上述代码可以看出 `Docket` 的配置中只有文档的类型设置新老版本是不同的，新版本的配置是 `OAS_30` 而旧版本的配置是 `SWAGGER_2`。
>
>> PS：OAS 是 OpenAPI Specification 的简称，翻译成中文就是 OpenAPI 说明书。
>
>#### 4.访问Swagger
>
>新版本的 Swagger 访问地址和老版本的地址是不同的，新版版的访问地址是“localhost:8080/swagger-ui/“”。
>
>新版本和老版本的区别主要体现在以下 4 个方面：
>
>1. 依赖项的添加不同：新版本只需要添加一项，而老版本需要添加两项；
>2. 启动 Swagger 的注解不同：新版本使用的是 `@EnableOpenApi`，而老版本是 `@EnableSwagger2`；
>3. Docket（文档摘要信息）的文件类型配置不同：新版本配置的是 `OAS_3`，而老版本是 `SWAGGER_2`；
>4. Swagger UI 访问地址不同：新版本访问地址是“http://localhost:8080/swagger-ui/”，而老版本访问地址是“http://localhost:8080/swagger-ui.html”。
>
>## 总结
>
>Swagger 新版本让人印象深刻的优点有两个：第一，配置变得简单了，比如依赖项配置减少了 50%，第二，新版 Swagger 页面设计风格有了不小的改变，新版的页面让人感觉更加现代化也更加具有科技感了，总体来说美观了不少。
>
>值得一提的是 Swagger 的整个升级过程很平滑，从老版本升级到新版本，只需要简单的配置即可，那些用于描述接口的注解还是延续了老版本的用法，这样就可以在不修改大部分主要代码的情况下，可以成功到最新版本啦。


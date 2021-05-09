

## P4.第一个Spring boot程序

### pom.xml

+ parent: 继承`spring-boot-starter-parent`的依赖配置, 控制版本与打包内容

+ 项目元数据信息: 创建时候输入的Project Metadata部分, 也就是Maven项目的基本元素, 包括: groupId, artifactId, version, name, description等
+ dependencies: 项目具体依赖, 这里包含了`spring-boot-starter-web`用于实现HTTP接口(该依赖包含了Spring MVC), 官方描述: 使用Spring MVC构建Web应用程序的入门者, 使用Tomcat作为默认嵌入式容器. 



## P5.IDEA快速创建及彩蛋

修改端口号

`resources->application.properties`

增加: server.port = xxxx



## P6.Spring boot 自动装配原理

### 原理初探

#### 自动配置: 

**pom.xml**

+ spring-boot-dependencies: 核心依赖在父工程中
+ 我们在写或者引入一些springboot依赖的时候, 不需要指定版本, 因为有这些版本仓库



**启动器:** 

+ ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
  </dependency>
  ```

+ 启动器: 说白了就是Springboot的启动场景

+ 比如`spring-boot-starter-web`, 他就会帮我们自动导入web环境所有的依赖

+ springboot会将所有的功能场景, 都变成一个个的启动器

+ 如果我们要使用什么功能, 就只需要找到对应的`starter`启动器就可以了



**主程序: **

```java
//@标注这个类是一个springboot的应用: 启动类下的所有资源被导入
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        //将spring boot 应用启动
        SpringApplication.run(Application.class, args);
    }

}
```

+ 注解

  + ```java
    @SpringBootConfiguration: springboot的配置
    	@Configuration: spring配置类
    	@Component: 说明这也是一个spring的组件
    	
    @EnableAutoConfiguration: 自动配置
    ```

**结论:** 

spring boot所有自动配置都是在启动的时候扫描并加载: `spring.factories`所有的自动配置类都在这里面, 但是不一定生效, 要判断条件是否成立, 只要导入对应的start, 就有对应的启动器了, 有了启动器, 我们自动装配就会生效, 然后就配置成功! 

1. spring boot在启动的时候, 葱类路径下`/META-INF/spring.factories`获取指定的值;
2. 将这些自动配置的类导入容器, 自动配置就会生效, 帮我进行自动配置;
3. 以前我们需要自动配置的东西, 现在spring boot帮我们都做了;
4. 整合javaEE, 解决方案和自动配置的东西都在`spring-boot-autoconfigure-2.3.1.RELEASE.jar`这个包下;
5. 它会把所有需要导入的组件, 以类名的方式返回, 这些组件就会被添加到容器;
6. 容器中存在非常多的`xxxAutoConfiguration`的文件(@Bean), 就是这些类给容器中导入这个场景需要的所有组件, 并自动配置, @Configuration, JavaConifg!
7. 有了自动配置类, 才免去我们手动配置. 



## P7 了解下启动类怎么运行

#### SpringApplication

这个类主要做了: 

1. 推断应用的类型是普通的项目还是Web项目
2. 查找并加载所有可用初始化器, 设置到initalizers属性中
3. 找出所有的应用程序监听器, 设置到listener属性中
4. 推断并设置main方法的定义类, 找到运行的主类
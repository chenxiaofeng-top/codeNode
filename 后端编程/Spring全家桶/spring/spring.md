## spring 

1. 对象的管理，对象的实例化由spring来控制
   - 控制反转
2. 对象的方法管理，方法的拦截
   - 切面编程

## spring mvc 核心

- 初始化
  - 在web.xml中配置一个Servlet，把所有的请求都交给spring mvc处理，并把spring mvc的配置文件以参数传入。
  - 在spring mvc配置三大件，
    - 处理映射器，分析请求url,找到合适的处理适配器（通过注解，不需要配置），
    - 处理适配器，处理url请求，返回相关数据给到视图解析器（真正的处理器，由我们写，即业务）（通过注解，不需要配置），
    - 视图解析器，显示给用户（通过注解，不需要配置）
    - 注解开启
      - <context:annotation-config/ >：自动注入注解
      - <context:component-scan base-package="com.xx.xx" />  ：扫描
      - <mvc:annotation-driven />：只需要扫描所有带@Controller注解的类
      - 静态资源，有两种方式：
        1. <mvc:default-servlet-handler />
        2. <mvc:resources mapping="/admin/**" location="/,/admin/" />
  - 写controller类，即业务
- 整合各种框架
  - mybatis
    - 数据库配置文件
- 功能：
  - 拦截器
  - 文件上传下载
    - ![image-20220313223825134](C:\oneDrive\J学习笔记\codingNote\后端编程\Spring全家桶\spring\img\image-20220313223825134.png)

## 核心

### 基本构成

- 一个表对应一个实体
- Dao由接口和接口~~实现类~~(改成mapper.xml)组成
- 一个mybatis-config.xml配置文件，数据库连接信息

### 构成顺序

1. SqlSessionFactoryBuilder(**mybatis-config.xml**)--->SqlSessionFactory--->SqlSession(**mapper.xml**)--->java接口
2. mybatis-config.xml引入mapper.xml，mapper.xml中namespace指向了java接口类
3. 样例：

- SqlSessionFactoryBuilder读取mybatis-config.xml，生成SqlSessionFactory

```java
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```

- 从 SqlSessionFactory 中获取 SqlSession，SqlSession解析mapper成java接口

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    BlogMapper mapper = session.getMapper(BlogMapper.class);
    Blog blog = mapper.selectBlog(101);
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
    <select id="selectBlog" resultType="Blog">
        select * from Blog where id = #{id}
    </select>
</mapper>
```

mybatis-config.xml样例

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```



## 功能

### xml配置

- 引入properties文件

```xml
<properties resource="org/mybatis/example/config.properties">
    <property name="username" value="dev_user"/>
    <property name="password" value="F2Fa3!33TYyg"/>
</properties>

<dataSource type="POOLED">
  <property name="driver" value="${driver}"/>
  <property name="url" value="${url}"/>
  <property name="username" value="${username}"/>
  <property name="password" value="${password}"/>
</dataSource
```

### 类型别名（typeAliases）

```xml
<typeAliases>
    <package name="domain.blog"/>
</typeAliases>
```

### 类型处理器（typeHandlers）

MyBatis 在设置预处理语句（PreparedStatement）中的参数或从结果集中取出一个值时， 都会用类型处理器将获取到的值以合适的方式转换成 Java 类型。下表描述了一些默认的类型处理器。

以重写已有的类型处理器或创建你自己的类型处理器来处理不支持的或非标准的类型。 具体做法为：

- 实现 org.apache.ibatis.type.TypeHandler 接口，

- 或继承一个很便利的类 org.apache.ibatis.type.BaseTypeHandler， 并且可以（可选地）将它映射到一个 JDBC 类型。比如：
```java
// ExampleTypeHandler.java
@MappedJdbcTypes(JdbcType.VARCHAR)
public class ExampleTypeHandler extends BaseTypeHandler<String> {

    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, String parameter, JdbcType jdbcType) throws SQLException {
        ps.setString(i, parameter);
    }

    @Override
    public String getNullableResult(ResultSet rs, String columnName) throws SQLException {
        return rs.getString(columnName);
    }

    @Override
    public String getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        return rs.getString(columnIndex);
    }

    @Override
    public String getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        return cs.getString(columnIndex);
    }
  }
```

```xml
<!-- mybatis-config.xml 全局-->
<typeHandlers>
  <typeHandler handler="org.mybatis.example.ExampleTypeHandler"/>
</typeHandlers>
```

```xml
<!-- mapper.xml 单个字段 roundingMode-->
<resultMap type="org.apache.ibatis.submitted.rounding.User" id="usermap2">
    <id column="id" property="id"/>
    <result column="name" property="name"/>
    <result column="funkyNumber" property="funkyNumber"/>
    <result column="roundingMode" property="roundingMode" typeHandler="org.apache.ibatis.type.EnumTypeHandler"/>
</resultMap>
```

### 事务管理器

```xml
<!-- mybatis-config.xml 一般就这么用了-->
<!--如果你正在使用 Spring + MyBatis，则没有必要配置事务管理器，因为 Spring 模块会使用自带的管理器来覆盖前面的配置。-->
<transactionManager type="JDBC"/>
```

### **数据源（dataSource）**

所谓数据源，即封装连接数据库的基本操作，增加池的概念，增加访问数据库性能，减少连接断开上的损耗。

三种mybatis自带的数据源类型，无第三方数据源，则用**POOLED**

- **UNPOOLED**：这个数据源的实现会每次请求时打开和关闭连接
- **POOLED**：这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。 这种处理方式很流行，能使并发 Web 应用快速响应请求。
- **JNDI** – 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用。这种数据源配置只需要两个属性：

```java
<dataSource type="org.myproject.C3P0DataSourceFactory">
  <property name="driver" value="org.postgresql.Driver"/>
  <property name="url" value="jdbc:postgresql:mydb"/>
  <property name="username" value="postgres"/>
  <property name="password" value="root"/>
</dataSource>
```

### 映射器（mappers）

```xml
<!-- 使用相对于类路径的资源引用 -->
<mappers>
    <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
    <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
    <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
```

```xml
<!-- 将包内的映射器接口实现全部注册为映射器 -->
<!-- 把mapper.xml放到接口的同一目录下 -->
<!-- 或着在resources中创建同一目录 -->
<mappers>
    <package name="org.mybatis.builder"/>
</mappers>
```



## XML 映射器 mapper.xml

- select

```xml
<!-- 方法名id，参数parameterType(可以不写，自动识别)，返回类型resultType  -->
<select id="selectPerson" parameterType="int" resultType="hashmap">
    SELECT * FROM PERSON WHERE ID = #{id}
</select>

<select
  id="selectPerson"
  parameterType="int"
  parameterMap="deprecated" 目前已被废弃
  resultType="hashmap"
  resultMap="personResultMap"
  flushCache="false"
  useCache="true"
  timeout="10"
  fetchSize="256"
  statementType="PREPARED"
  resultSetType="FORWARD_ONLY">
```

- 其它
```xml
  <insert
    id="insertAuthor"
    parameterType="domain.blog.Author"
    flushCache="true"
    statementType="PREPARED"
    keyProperty=""
    keyColumn=""
    useGeneratedKeys=""
    timeout="20">
  
  <update
    id="updateAuthor"
    parameterType="domain.blog.Author"
    flushCache="true"
    statementType="PREPARED"
    timeout="20">
  
  <delete
    id="deleteAuthor"
    parameterType="domain.blog.Author"
    flushCache="true"
    statementType="PREPARED"
    timeout="20">
      
 <insert id="insertAuthor">
  insert into Author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>

<update id="updateAuthor">
  update Author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>

<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
```

- insert 获得插入数据库时的主键

```xml
自动生成的主键,多条语句也生效
<insert id="insertAuthor" useGeneratedKeys="true"
        keyProperty="id">
    insert into Author (username, password, email, bio) values
    <foreach item="item" collection="list" separator=",">
        (#{item.username}, #{item.password}, #{item.email}, #{item.bio})
    </foreach>
</insert>
```

##   SQL 代码片段

```xml
<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
<include refid="userColumns">
    <property name="alias" value="t1"/>
</include>

另外共同对象的空判断，可以省Sql
```

## 结果映射

```xml
<!-- SQL 映射 XML 中 -->
<select id="selectUsers" resultType="User">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>

<resultMap id="userResultMap" type="User">
  <id property="id" column="user_id" />
  <result property="username" column="user_name"/>
  <result property="password" column="hashed_password"/>
</resultMap>
<select id="selectUsers" resultMap="userResultMap">
  select user_id, user_name, hashed_password
  from some_table
  where id = #{id}
</select>
```

- 一对一映射，查询另一个表，形成一个对象，可能需要在Sql取别名

```xml
单个对象用association，通过javaType告诉mybatis生成什么类型的对象，可以指定resultMap="authorResult"
<association property="author" javaType="Author" >
    <id property="id" column="author_id"/>
    <result property="username" column="author_username"/>
    <result property="password" column="author_password"/>
    <result property="email" column="author_email"/>
    <result property="bio" column="author_bio"/>
    <result property="favouriteSection" column="author_favourite_section"/>
</association>
```

- 一对多映射，可能需要在Sql中取别名
  - 可以嵌套association

```xml
多个对象用collection，通过ofType告诉mybatis生成List<obj>中的obj是什么类型
<collection property="posts" ofType="Post">
    <id property="id" column="post_id"/>
    <result property="subject" column="post_subject"/>
    <association property="author" javaType="Author"/>
    <collection property="comments" ofType="Comment">
        <id property="id" column="comment_id"/>
    </collection>
    <collection property="tags" ofType="Tag" >
        <id property="id" column="tag_id"/>
    </collection>
    <discriminator javaType="int" column="draft">
        <case value="1" resultType="DraftPost"/>
    </discriminator>
</collection>
```

## discriminator 标签

- https://www.hxstrive.com/subject/mybatis.htm?id=206
- https://www.jianshu.com/p/0235e9245056
- 针对同一条sql在不同的情况返回不同的值，对应相关的映射

## 缓存

```xml
<cache/>

<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

## 动态 SQL

- if
- choose (when, otherwise)
- trim (where, set)
- foreach

```xml
<if test="author != null and author.name != null">
    AND author_name like #{author.name}
</if>

<choose>
    <when test="title != null">
        AND title like #{title}
    </when>
    <when test="author != null and author.name != null">
        AND author_name like #{author.name}
    </when>
    <otherwise>
        AND featured = 1
    </otherwise>
</choose>

<foreach item="item" index="index" collection="list"
         open="ID in (" separator="," close=")" nullable="true">
    #{item}
</foreach>
```


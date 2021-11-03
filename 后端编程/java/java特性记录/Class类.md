1. 同一个类可以生成多个对象，但只有一个Class对象

2. instanceof 匹配指定类型及其父类，而Class只能匹配指定类型，可以用==

```java
       Integer n = new Integer(123);
     
       boolean b1 = n instanceof Integer; // true，因为n是Integer类型
       boolean b2 = n instanceof Number; // true，因为n是Number类型的子类
     
       boolean b3 = n.getClass() == Integer.class; // true，因为n.getClass()返回Integer.class
       boolean b4 = n.getClass() == Number.class; // false，因为Integer.class!=Number.class
```

3. 属性获取：
  ```java
  Field getField(name)：根据字段名获取某个public的field（包括父类）
  Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
  Field[] getFields()：获取所有public的field（包括父类）
  Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）
  ```

  

4. Field 获得的属性的信息：

 ```java
 getName():返回字段名称，例如，"name"
 getType():返回字段类型，也是一个Class实例，例如，String.class
 get(Object obj) ： 取得obj对象这个Field上的值
 set(Object obj, Object value) ： 向obj对象的这个Field设置新值value
 getModifiers():返回字段的修饰符，它是一个int，不同的bit表示不同的含义。
  
 Modifier 更多信息
 Field f = String.class.getDeclaredField("value");
 f.getName(); // "value"
 f.getType(); // class [B 表示byte[]类型
 int m = f.getModifiers();
 Modifier.isFinal(m); // true
 Modifier.isPublic(m); // false
 Modifier.isProtected(m); // false
 Modifier.isPrivate(m); // true
 Modifier.isStatic(m); // false
 
 //允许获取私有字段
 Field.setAccessible(true)
 ```

5. Method 获得的属性的信息：

   ```java
   所有Method信息
   Method getMethod(name, Class...)：获取某个public的Method（包括父类）
   Method getDeclaredMethod(name, Class...)：获取当前类的某个Method（不包括父类）
   Method[] getMethods()：获取所有public的Method（包括父类）
   Method[] getDeclaredMethods()：获取当前类的所有Method（不包括父类）
       
       
   一个Method对象包含一个方法的所有信息：
   getName()：方法名称，例如："getScore"；
   getReturnType()：返回值类型，也是一个Class实例，例如：String.class；
   getParameterTypes()：方法的参数类型，是一个Class数组，例如：{String.class, int.class}；
   getModifiers()：返回方法的修饰符，它是一个int，不同的bit表示不同的含义。
       
   允许调用私有方法：
   Method.setAccessible(true)
       
       
   ```

   6,构造方法

   ```
   public且无参数构造方法
   Person p = Person.class.newInstance();
   
   有参
   Class cls = Class.forName("com.demo.Person");
   Constructor c = cls.getConstructor(String.class,int.class);
   Person p = (Person) c.newInstance("张三",23);
   
   
   ```

   


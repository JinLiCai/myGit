1.Java Bean 简介



Java Bean  (也称为Bean) 是一个遵循特定写法的Java类，只不过这个类需要遵循一些编码的约定，通常具有如下特点：

1).它是一个公开的（public）类；

2).它有一个默认的构造方法，也就是不带参数的构造方法（在实例化Java Bean 时，要调用默认的构造方法）。

3).它提供setXXX()方法和getXXX()来让外部程序设置和获取Java Bean 的属性。

4).它实现 java.io.Serializable或者java.io.Externalizable接口，以支持序列化。

**综上所述，符合上述条件的类，我们都可把它看成是 Java Bean组件。**

2.Java Bean 的作用



​        JavaBean在J2EE开发中，通常用于封装数据，对于遵循以上写法的JavaBean组件，其它程序可以通过反射技术实例化JavaBean对象，并且通过反射那些遵守命名规范的方法，从而获知JavaBean的属性，进而调用其属性保存数据。

3.Java Bean 的属性命名



​        属性（property）是 Java Bean 组件内部状态的抽象表示，外部程序使用属性来设置和获取 Java Bean 组件的状态，为了让外部程序能够知道 Java Bean 提供了哪些属性，我们在编写Java Bean 时必须遵循标准的命名方式。

例如：一个String类型的username属性，它对应的方法如下：

public String getUsername()

public void setUsername(String username)

也就是为每一个属性添加getXXX()方法和setXXX()方法,其中属性名字的第一个字母大写，然后就在名字前面加上“get”和“set”。这样的属性是可读写的属性，如果只有get方法，那么这个属性是只读属性；如果一个属性只有set方法，那么这个属性是只写属性。get/set 命名方式有一个例外，那就是对于Boolean类型的属性，应该使用 is/set 命名方式，在下面的实例中具体说明。 

4.举例Java Bean的创建及规范



```
package anli;

public class Javabean {

 private String username;//用户名
 private String passward;//密码
 //注意：对于Boolean类型的属性getxxx()方法与其他类型的方法有点区别
 private boolean married = false;
 public String getUsername() {
   return username;
 }
 public void setUsername(String username) {
   this.username = username;
 }
 public String getPassward() {
   return passward;
 }
 public void setPassward(String passward) {
   this.passward = passward;
 }
 public boolean isMarried() {//boolean类型的getxxx()方法为isxxx()
   return married;
 }
 public void setMarried(boolean married) {
   this.married = married;
 }    
}
```

常见笔试题：

以下哪些方法属于Java Bean 规范的方法呢？

​    A.getName()   

​    B.getName(String name)  

​    C.setName(String name)

​    D.setName()   

​    E.setFlag(boolean flag)    

​    F.isFlag()

解析：setXXX()方法有参数，getXXX()方法没有参数，Boolean类型的getXXX()方法为isXXX()。

参考答案：A.C.E.F

5.Java Bean 的属性类型

​       Java Bean 有4种类型的属性：简单属性（simple property）、索引属性（indexed property）、绑定属性（bound property）和约束属性（constrained property）在 JSP 中支持简单属性和索引属性，所以在这里小编只介绍Java Bean 的简单属性和索引属性。

 a.简单属性

简单属性就是接收单个值的属性，即只要采用get/set命名即可。

b.索引属性

索引属性就是获取和设置数组时使用的属性，要运用索引属性，需要提供两对get/set方法，一对用于数组，另一对用于数组中的元素，语法格式如下：

publicPropertyType[] getPropertyName()

publicvoid setPropertyName(PropertyType[] values)

publicPropertyType getPropertyName(int index)

public void setPropertyName(int index ,PropertyType value)

例如，有一个索引属性 age,它的get/set方法如下：

```
package anli;

public class App {
   
 private String[] age;

 public String[] getAge() {
   return age;
 }

 public void setAge(String[] age) {
   this.age = age;
 }
 public String getAge(int i) {
   return age[i];
 }

 public void setAge(int i,String newAge) {
   age[i] = newAge;
  
```

























**1.Java Bean 简介**

Java Bean  (也称为Bean) 是一个遵循特定写法的Java类，只不过这个类需要遵循一些编码的约定，通常具有如下特点：

1).它是一个公开的（public）类；

2).它有一个默认的构造方法，也就是不带参数的构造方法（在实例化Java Bean 时，要调用默认的构造方法）。

3).它提供setXXX()方法和getXXX()来让外部程序设置和获取Java Bean 的属性。

4).它实现 java.io.Serializable或者java.io.Externalizable接口，以支持序列化。

**综上所述，符合上述条件的类，我们都可把它看成是 Java Bean组件。**

**2.Java Bean 的作用**

​        JavaBean在J2EE开发中，通常用于封装数据，对于遵循以上写法的JavaBean组件，其它程序可以通过反射技术实例化JavaBean对象，并且通过反射那些遵守命名规范的方法，从而获知JavaBean的属性，进而调用其属性保存数据。

**3. Java Bean 的属性命名**

​        属性（property）是 Java Bean 组件内部状态的抽象表示，外部程序使用属性来设置和获取 Java Bean 组件的状态，为了让外部程序能够知道 Java Bean 提供了哪些属性，我们在编写Java Bean 时必须遵循标准的命名方式。

例如：一个String类型的username属性，它对应的方法如下：

public String getUsername()

public void setUsername(String username)

也就是为每一个属性添加getXXX()方法和setXXX()方法,其中属性名字的第一个字母大写，然后就在名字前面加上“get”和“set”。这样的属性是可读写的属性，如果只有get方法，那么这个属性是只读属性；如果一个属性只有set方法，那么这个属性是只写属性。get/set 命名方式有一个例外，那就是对于Boolean类型的属性，应该使用 is/set 命名方式，在下面的实例中具体说明。 

**4. 举例说明 Java Bean 的创建以及要遵循的规范** 



![img](https://mmbiz.qpic.cn/mmbiz_png/VFicV5vyK5ulAAMHjnqoJP7TziciaoCRicbphNcH9LUfH4RfyPPZkdtuO0YJ3SCpPKYbtiaK3L2ic5K82cQryOibN0jWA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

常见笔试题：

以下哪些方法属于Java Bean 规范的方法呢？

​    A.getName()   

​    B.getName(String name)  

​    C.setName(String name)

​    D.setName()   

​    E.setFlag(boolean flag)    

​    F.isFlag()

解析：setXXX()方法有参数，getXXX()方法没有参数，Boolean类型的getXXX()方法为isXXX()。参考答案：A.C.E.F

**5. Java Bean 的属性类型**

​       Java Bean 有4种类型的属性：简单属性（simple property）、索引属性（indexed property）、绑定属性（bound property）和约束属性（constrained property）在 JSP 中支持简单属性和索引属性，所以在这里小编只介绍Java Bean 的简单属性和索引属性。

 a.简单属性

简单属性就是接收单个值的属性，即只要采用get/set命名即可。

b.索引属性

索引属性就是获取和设置数组时使用的属性，要运用索引属性，需要提供两对get/set方法，一对用于数组，另一对用于数组中的元素，语法格式如下：

 public  PropertyType[]  getPropertyName()

 public  void  setPropertyName(PropertyType[]  values)

 public  PropertyType  getPropertyName(int  index)

 public  void  setPropertyName(int  index ,PropertyType  value)

例如，有一个索引属性 age,它的get/set方法如下：



![img](https://mmbiz.qpic.cn/mmbiz_png/VFicV5vyK5ulAAMHjnqoJP7TziciaoCRicbpILicm0y2tIibjrMp11JjvXEN0CM0OGclwMC8jVgUk4FJKP4fFaUs4ABQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
























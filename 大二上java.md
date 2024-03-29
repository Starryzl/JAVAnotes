# 1.可变参数

​	方法在定义时，可以定义一个参数，能够接收任意多个值，在一个方法参数中只能有一个可变参数，并且只能是最后一个参数

![image-20230909124329049](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230909124329049.png)



# 2.设计模式（23种）



## 2.1单例模式

​	在内存中只有一个对象

​	方式：构造器私有化（防止其他类new），本类提供一个能够获取唯一对象的静态方法

​	实现：两种

### 2.1.1预加载（饿汉模式）

### 在类中创建一个属性，本类类型的，并且同时new出对象




      public class PreloadSingleton {
      public static PreloadSingleton instance = new PreloadSingleton();
       
       //其他的类无法实例化单例类的对象
       private PreloadSingleton() {
       };
       
       public static PreloadSingleton getInstance() {
              return instance;
       }
       }


### 2.1.2懒加载（懒汉模式）


​       
​      public class Singleton {
​      private static Singleton instance=null;
​       
​       private Singleton(){
​       };
​       
       public static Singleton getInstance()
       {
              if(instance==null)
              {
                     instance=new Singleton();
              }
              return instance;
              
       }
       }


## 2.2工厂模式

简单工厂、抽象工厂、工厂方法

### 2.2.1简单工厂模式

静态工厂 -- 不需要实例化工厂

![image-20230909131443663](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230909131443663.png)





![image-20230909131752408](C:\Users\Starry_z666\AppData\Roaming\Typora\typora-user-images\image-20230909131752408.png)



### 实例工厂 -- 先创建工厂对象，再去获取产品对象

```
public class BJOrderPizza extends OrderPizza {
       Pizza createPizza(String ordertype) {
              Pizza pizza = null;
              if (ordertype.equals("cheese")) {
                     pizza = new LDCheesePizza();
              } else if (ordertype.equals("pepper")) {
                     pizza = new LDPepperPizza();
              }
              return pizza;
       }
}
```



## 2.3 代理模式

### 2.3.1静态代理

​		优点：简单	缺点：会有很多类

### 2.3.2动态代理

- JDK- --- 目标必须有接口
- CGLIB -- 可以没有接口 -- 生成子类的方法



# 3.JDBC

http://t.csdn.cn/aZH9n



```
1.jdbc的概念
JDBC（Java DataBase Connectivity：java数据库连接）是一种用于执行SQL语句的Java API，可以为多种关系型数据库提供统一访问，它是由一组用Java语言编写的类和接口组成的。
JDBC的作用：可以通过java代码操作数据库
2.jdbc的本质
其实就是java官方提供的一套规范(接口)。用于帮助开发人员快速实现不同关系型数据库的连接！
```

​	操作数据库--

​	一套接口和工具--

​	数据库厂商提供驱动包--



​	不重要  -- 现在用的很少

​				 -- 所有的操作数据库的框架 底层都是jdbc



## 3.1操作数据库的步骤：

​	1、加载驱动

​		Class.forName("驱动类")

​	2、获取连接对象

​	Connection conn = DriverManager.getConnection(url,"root","root");

​	3、执行sql--Statement对象

​	4、处理结果

​	5、关闭资源



```
public class TestJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/qq1?serverTimezone=UTC&useUnicode=true&chacterEncoding=utf8";

        try {
            //加载驱动
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conn = DriverManager.getConnection(url,"root","root");
            System.out.println(conn);

            Statement st = conn.createStatement();
            //增删改只需要sql语句变，其他不变
            String sql = "update student set NAME  = 'abc' where id = 7"; //dml语句 insert update delete

            //返回值--受影响的行数
            int result = st.executeUpdate(sql);
            System.out.println(result);

            //释放资源
            st.close();
            conn.close();
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}
```



## 3.2 JDBC工具类

- 为啥需要工具类呢？
- 因为在上个案例中的dao层的代码，很多都是重复的
- 程序员一但碰到重复代码，就要想办法解决

#### 1.工具类的抽取

- 配置文件(在src下创建config.properties)

  ```
  driverClass=com.mysql.jdbc.Driver
  url=jdbc:mysql://localhost:3306/db1
  username=root
  password=root
  ```

- 工具类：com.lichee02.utils.JDBCUtils

```
/*
    JDBC工具类
 */
public class JDBCUtils {
    //1.私有构造方法
    private JDBCUtils(){};

    //2.声明配置信息变量
    private static String driverClass;
    private static String url;
    private static String username;
    private static String password;
    private static Connection conn;

    //3.静态代码块中实现加载配置文件和注册驱动
    static{
        try{
            //通过类加载器返回配置文件的字节流
            InputStream is = JDBCUtils.class.getClassLoader().getResourceAsStream("config.properties");

            //创建Properties集合，加载流对象的信息
            Properties prop = new Properties();
            prop.load(is);

            //获取信息为变量赋值
            driverClass = prop.getProperty("driverClass");
            url = prop.getProperty("url");
            username = prop.getProperty("username");
            password = prop.getProperty("password");

            //注册驱动
            Class.forName(driverClass);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //4.获取数据库连接的方法
    public static Connection getConnection() {
        try {
            conn = DriverManager.getConnection(url,username,password);
        } catch (SQLException e) {
            e.printStackTrace();
        }

        return conn;
    }

    //5.释放资源的方法
    public static void close(Connection conn, Statement stat, ResultSet rs) {
        if(conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if(stat != null) {
            try {
                stat.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if(rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void close(Connection conn, Statement stat) {
        close(conn,stat,null);
    }
}

```



## 3.3SQL注入攻击

### 3.3.1 sql注入攻击的演示

分析：

- ​	登陆的时候，会调用UserDaoImpl .findByLoginNameAndPassword 方法
- ​	此方法中的sql语句如下

```
//2.定义SQL语句
String sql = "SELECT * FROM user WHERE loginname='"+loginName+"' AND password='"+password+"'";
System.out.println(sql);
//3.获取操作对象，执行sql语句，获取结果集
st = conn.createStatement();
rs = st.executeQuery(sql);
//4.获取结果集
if (rs.next()) {
    //5.封装
    user = new User();
    user.setUid(rs.getString("uid"));
    ....
}
//6.返回
return user;
```



- 输入aaa和aaa’ or ‘1’='1 (注意引号)最终sql拼接完变为：

```
SELECT * FROM user WHERE loginname='aaa' AND password='aaa' or '1'='1'
```




- 这样的sql语句，会将user表中所有数据都查询出来

- 所以最终查询到用户了，就登陆进去了

### 3.3.2 sql注入攻击的原理

- ​	按照正常道理来说，我们在密码处输入的所有内容，都应该认为是密码的组成
- 但是现在Statement对象在执行sql语句时，将一部分内容当做查询条件来执行了

### 3.3.3PreparedStatement的介绍

- 预编译sql语句的执行者对象。在执行sql语句之前，将sql语句进行提前编译

- 明确sql语句的格式后，就不会改变了。剩余的内容都会认为是参数

- 参数使用?作为占位符

- 为参数赋值的方法：setXxx(参数1,参数2);

  - 参数1：?的位置编号(编号从1开始)

  - 参数2：?的实际参数

- 执行sql语句的方法

  - 执行insert、update、delete语句：int executeUpdate();

  - 执行select语句：ResultSet executeQuery();



### 3.3.4PreparedStatement的使用

```
/*
	 使用PreparedStatement的登录方法，解决注入攻击
*/
@Override
public User findByLoginNameAndPassword(String loginName, String password) {
    //定义必要信息
    Connection conn = null;
    PreparedStatement pstm = null;
    ResultSet rs = null;
    User user = null;
    try {
        //1.获取连接
        conn = JDBCUtils.getConnection();
        //2.创建操作SQL对象
        String sql = "SELECT * FROM user WHERE loginname=? AND password=?";
        pstm = conn.prepareStatement(sql);
        //3.设置参数
        pstm.setString(1,loginName);//设置第一个?参数
        pstm.setString(2,password);//设置第二个?参数
        System.out.println(sql);
        //4.执行sql语句，获取结果集
        rs = pstm.executeQuery();
        //5.获取结果集
        if (rs.next()) {
            //6.封装
            user = new User();
            user.setUid(rs.getString("uid"));//如果有别名，必须用别名
            user.setUcode(rs.getString("ucode"));
            user.setUsername(rs.getString("username"));
            user.setPassword(rs.getString("password"));
            user.setGender(rs.getString("gender"));
            user.setDutydate(rs.getDate("dutydate"));
            user.setBirthday(rs.getDate("birthday"));
            user.setLoginname(rs.getString("loginname"));
        }
        //7.返回
        return user;
    }catch (Exception e){
        throw new RuntimeException(e);
    }finally {
        JDBCUtils.close(conn,pstm,rs);
    }
}


```





# 4.反射

http://t.csdn.cn/ktagq



# 5.mybatis框架



软件开发层次

```
软件开发层次
界面--表现层--html css js
处理业务--业务逻辑层--最重要的
数据处理--数据访问层--和数据库打交道--操作数据库
数据库--MySql
```

```
表现层
{
	业务逻辑层
}
业务逻辑层{
数据访问层
}
数据访问层{

}
```

## 5.1mybatis的开发步骤

```
mybatis的开发步骤
1、创建一个maven工程
2、引入mybatis和数据库相关jar包
3、编写主配置文件--不需要记住--只需要会改
4开发代码---- 数据访问层代码DAO
软件分层
	表现层-->业务逻辑层-->数据访问层-->数据库
	业务逻辑-- com.tencent.service
	数据访问 ---comtencent.dao/mapper
两种开发方式
	创建包
	com.tencent.service :放业务层接口
	com.tencent.service.impl: 业务层接口的实现类
	com.tencent.dao:数据访问层接口
	com.tencent.dao.impl: 数据访问层接口的实现类

	a、传统方式
		编写接口:XXXDao 	XXX---操作的类

		编写实现类:XXXDaolmpl	--先不要写具体实现

		编写对象关系映射文件:XXXMapper.xml 	--注意namespace必须写
			标签属性
				每个标签的id不能重复
				parameterType:参数(传递给sql的数据)类型
				resultType: 返回结果类型 只有select标签有

		继续编写实现类:
			依赖SqlSessionFactory对象
			利用session的api操作数据库
		把映射文件放入主配置文件
	b、接口方式
```


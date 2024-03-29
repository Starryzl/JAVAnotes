# SSM框架整理

## 1.mybatis   --  
​     SqlSessionFactory --- 
​     SqlSession            ---

### 1.1作用：orm 框架           

​			Object   Relational   Mapper框架    

​          面向对象语言和关系型数据库    数据不匹配的问题
​          两类：
​	全自动  ：  不会sql就可以操作数据  -- 性能较差    
​	半自动  ： 执行手写sql  ---  性能较好    

### 1.2配置文件：
​          mybatisCore.xml  --  开发环境相关          主配置文件
​          mapper.xml         --  程序员需要编写的    对象关系映射文件  
​          <selelct>dql  <insert><update><delete> dml  ddl-create  drop 
​	parameterType-sql需要传入数据     resultType-select封装返回结果
​	

​		怎么解决数据返回不能封装成实体类的问题？   
​	resultMap  -  属性和列名的对象关系，一对一   一对多 多对多的映射关系   
​	<association>  <collection> 
​           动态sql  ：      name  age   sex    查询
​	<sql>  <set>  <include>   <if>  <for>   <where>   

### 1.3执行流程：
​	1、构建SqlSessionFactory对象   --   SqlSessionFactoryBuilder.build(mybatisCore.xml )
​	2、获取SqlSession对象  --  从工厂取出一个  openSession();
​	3、SqlSession的API  执行sql语句    从mapper.xml找到对应的sql
​	4、事务是否需要提交     session.commit();
​	5、SqlSession关闭  close();      回收到连接池

SqlSession的对象创建最佳实践：
	方法内创建     --    

### 1.4四个一致：
​	只写一个接口    --     Mapper接口的方式开发DAO     
​	实现类 ：   不需要自己写     SqlSession.getMapper(接口)--返回接口的实现类对象
​		mapper.xml  namespace==接口的全路径（限定）名称一致
​		mapper.xml  标签的id ==  接口中的方法名一致
​		mapper.xml  标签的parameterType==接口中方法的参数类型一致
​		mapper.xml  标签的resultType == 接口中方法的返回类型一致
​	原理：动态代理

补充  N+1问题 --- 延迟加载   lazy="true"
	部门  -- 员工
	

### 1.5.缓存：增加查询效率
​	一级缓存  ：  SqlSession级别    开启    
​	二级缓存：   SqlSessionFactory/Mapper级别   关闭    选择第三方缓存框架
​	缓存的命中：二级缓存--一级缓存--数据库
​	缓存的清空：dml   flush

## 2.spring--轻量级的javaee框架   --  

​	轻量级：体积小     低侵入   使用简单
​	核心功能：IOC  AOP
​	IOC：控制反转  --   对象的生命周期（管理） -- 对象的赋值
​	DI：依赖注入    --   对象在需要时 由spring容器自动赋值
​	SpringIOC容器：
​		BeanFactory   ：提供了基础的IOC功能   主要用于框架内
​		ApplicationContext：提供了开发中常见的功能需求 对BeanFactory  用于开发
​		

依赖注入的方式？
		构造器注入：需要有顺序时   
		setter注入： 开发中常用的
	接口注入：没讲

底层原理：反射    -- 在运行时注入---会有编译期检查

IOC注解： @AutoWired   :按类型注入
	 @Qualifier      :按名称注入---一个接口下多实现类

AOP：面向切面编程   --  日志 、权限 、统一处理
原理：动态代理   
	实现方式：
		1、JDKProxy--接口-生成接口的实现类
			InvocationHandler
		2、CGLIB	--继承--生成这个类的子类

bean的生命周期
       1、实例化   构造器---
       2、初始化   init-method
       3、销毁      destroy-method---当bean销毁前做的事情--释放资源

bean的单例：
	bean默认单例的  --scope：singleton、prototype

事务：本身不提供事务功能--管理jdbc事务--AOP
作用：事实的企业级开发框架--不是javaee标准
          管理各个层次对象，面向接口编程，减少耦合，提供企业级开发的常见功能，
          让我们更专注于业务，把一些非业务功能进行了整合
注解：
	标识bean：  @Component -- 通用注解 -- 有些类不好分层
		   @Service  --业务层    @Repository-数据访问层
		   
	AOP注解：@Advice   @Aspect      

## 3.springmvc:
​	mvc:显示和业务分离   
​	基于什么实现的 ？Servlet---核心控制器-DispatcherServlet
​	注解：
​		@Controller +@ResponseBody  ==  @RestController      
​		请求映射注解：
​			@RequestMapping--处理客户端的任何请求方法
​			@GetMapping    --  405
​			@PostMapping
​		Json相关：@ResponseBody--把对象转成json格式
​			@RequestBody  -- 把json转成对象
​		请求参数相关：
​			@PathVariable   restful  
​			@RequestParam("name")
​		跨域:  @Cross
​			1、域名不同   2、端口不同
​	执行流程：
​		1、进入核心控制器
​		2、通过访问请求 找对应的Controller--方法
​		3、处理请求   
​		4、返回给核心控制器
​		5、响应结果
Filter： 过滤器  -- 基于路径url
Servlet API：
​	HttpServletRequest
​	HttpServletResponse
​	HttpSession--
​	都是有tomcat管理   
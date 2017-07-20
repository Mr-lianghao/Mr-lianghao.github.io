## Mybatis所处的位置
Mybatis处在持久层，和数据库打交道

## 为什么需要Mybatis
引入MyBatis的目的：主要是为了弥补JDBC的硬编码问题：
 1. 解决频发链接数据库
 2. 解决sql代码的硬编码
 3. 解决占位符硬编码
 4. 解决结果集硬编码

## 我们使用Mybatis需要做的事
1. 配置SqlMapConfig.xml，Mybatis全局配置文件
2. mapper.xml,存放sql语句的文件
3. 通过sqlSessionFactory获取session进行操作，但这些都是Mybatis环境帮我们做的

## 入门程序
 1. 导入jar包
 2. log4j
 3. SqlMapConfig.xml全局环境变量的配置
 4. po类
 5. 编写po类的映射文件，也就是编写sql语句的
 6. 在全局配置文件中加载映射文件
 7. 根据业务需求，在映射文件中编写相应的sql语句
 8. 编写程序进行测试

## Mybatis和Hibernate的区别

## SqlSession和SqlSessionFactoryBuilder以及SqlSessionFactory

## 在DAO中使用Mybatis进行开发
1. 传统方式：该方式需要定义dao接口和实现类
  1. 编写接口和实现类
  2. 编写映射文件User.xml并根据需要，码上sql语句
2. 传统方式存在的问题：
  1. Dao方法体存在重复代码：通过SqlSessionFactory创建SqlSession，调用SqlSession的数据库操作方法
  2. 调用sqlSession的数据库操作方法需要指定statement的id，这里存在硬编码，不利于开发维护。

## 使用Mapper动态代理的方式

Mapper接口开发方法只需要程序员编写Mapper接口（相当于Dao接口），由Mybatis框架根据接口定义创建接口的动态代理对象，代理对象的方法体同上边Dao接口实现类方法。
### Mapper代理方式需要遵循的规范：
  1. Mapper.xml文件中的namespace与mapper接口的类路径相同。
  2. Mapper接口方法名和Mapper.xml中定义的每个statement的id相同
  3. Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql 的parameterType的类型相同
  4. Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

### Mapper方式的开发步骤
1. 编写接口文件：UserMapper.java
```java
Public interface UserMapper {
	//根据用户id查询用户信息
	public User findUserById(int id) throws Exception;
	//查询用户列表
	public List<User> findUserByUsername(String username) throws Exception;
	//添加用户信息
	public void insertUser(User user)throws Exception;
}

```

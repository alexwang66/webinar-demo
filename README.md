#Spring Boot集成MyBatis的基础项目

#MyBatis3.3.0

#Spring Boot 1.3.0.RELEASE

项目使用Spring Boot 1.3.0.RELEASE + Mybatis3.3.0

项目集成了Mybatis分页插件和通用Mapper插件

项目使用的mysql数据库，根据需要可以切换为其他数据库


```java
@Configuration
//注意，由于MapperScannerConfigurer执行的比较早，所以必须有下面的注解
//MyBatisConfig.class是一个包含了SqlSessionFactory配置的类
@AutoConfigureAfter(MyBatisConfig.class)
public class MyBatisMapperScannerConfig {

    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer() {
        MapperScannerConfigurer mapperScannerConfigurer = new MapperScannerConfigurer();
        mapperScannerConfigurer.setSqlSessionFactoryBeanName("sqlSessionFactory");
        mapperScannerConfigurer.setBasePackage("tk.mybatis.springboot.mapper");
        Properties properties = new Properties();
        properties.setProperty("mappers", "tk.mybatis.springboot.util.MyMapper");
        properties.setProperty("notEmpty", "false");
        properties.setProperty("IDENTITY", "MYSQL");
        //这里使用的通用Mapper的MapperScannerConfigurer，所有有下面这个方法
        mapperScannerConfigurer.setProperties(properties);
        return mapperScannerConfigurer;
    }

}

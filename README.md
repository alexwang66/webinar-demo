#CICD Webinar project

## 目的是将 JFrog Artifactory 的元数据做可视化
Artifactory 的元数据能够聚合软件交付的需求，构建，测试，部署等环节的关键数据，将这些数据可视化，可以展示软件交付流程的健康状态，帮助团队基于数据进行持续改进。

### 注意：
项目使用Spring Boot 1.3.0.RELEASE + Mybatis3.3.0

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

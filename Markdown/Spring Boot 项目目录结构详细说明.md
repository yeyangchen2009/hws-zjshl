# Spring Boot 项目目录结构详细说明

## 概述

Spring Boot 项目采用 Maven 或 Gradle 的标准目录结构，遵循约定优于配置的原则，使项目结构清晰、易于维护。

## 标准目录结构

```
my-spring-boot-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── myproject/
│   │   │               ├── MyProjectApplication.java      # 主启动类
│   │   │               ├── config/                        # 配置类目录
│   │   │               │   ├── WebConfig.java
│   │   │               │   └── DatabaseConfig.java
│   │   │               ├── controller/                    # 控制器目录
│   │   │               │   ├── UserController.java
│   │   │               │   └── HomeController.java
│   │   │               ├── service/                       # 服务层目录
│   │   │               │   ├── UserService.java
│   │   │               │   └── impl/
│   │   │               │       └── UserServiceImpl.java
│   │   │               ├── repository/                    # 数据访问层目录
│   │   │               │   ├── UserRepository.java
│   │   │               │   └── ProductRepository.java
│   │   │               ├── entity/                        # 实体类目录
│   │   │               │   ├── User.java
│   │   │               │   └── Product.java
│   │   │               ├── dto/                           # 数据传输对象目录
│   │   │               │   ├── UserDto.java
│   │   │               │   └── request/
│   │   │               │       └── CreateUserRequest.java
│   │   │               ├── exception/                     # 异常处理目录
│   │   │               │   ├── CustomException.java
│   │   │               │   └── GlobalExceptionHandler.java
│   │   │               └── utils/                         # 工具类目录
│   │   │                   ├── DateUtils.java
│   │   │                   └── StringUtils.java
│   │   ├── resources/
│   │   │   ├── static/                                    # 静态资源目录
│   │   │   │   ├── css/
│   │   │   │   │   └── style.css
│   │   │   │   ├── js/
│   │   │   │   │   └── app.js
│   │   │   │   └── images/
│   │   │   │       └── logo.png
│   │   │   ├── templates/                                 # 模板文件目录（Thymeleaf等）
│   │   │   │   ├── index.html
│   │   │   │   └── user/
│   │   │   │       └── profile.html
│   │   │   ├── application.yml                            # 主配置文件
│   │   │   ├── application-dev.yml                        # 开发环境配置
│   │   │   ├── application-prod.yml                       # 生产环境配置
│   │   │   ├── logback-spring.xml                         # 日志配置文件
│   │   │   ├── data.sql                                   # 初始化数据脚本
│   │   │   ├── schema.sql                                 # 数据库结构脚本
│   │   │   └── i18n/                                      # 国际化文件目录
│   │   │       ├── messages.properties
│   │   │       ├── messages_en.properties
│   │   │       └── messages_zh_CN.properties
│   │   └── webapp/                                        # Web应用目录（可选）
│   │       ├── WEB-INF/
│   │       │   └── web.xml
│   │       └── index.jsp
│   └── test/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── myproject/
│       │               ├── MyProjectApplicationTests.java # 主测试类
│       │               ├── controller/                    # 控制器测试
│       │               │   └── UserControllerTest.java
│       │               ├── service/                       # 服务层测试
│       │               │   └── UserServiceTest.java
│       │               └── repository/                    # 数据访问层测试
│       │                   └── UserRepositoryTest.java
│       └── resources/
│           ├── application-test.yml                       # 测试环境配置
│           └── test-data.sql                              # 测试数据脚本
├── target/                                                # 编译输出目录（Maven）
├── build/                                                 # 编译输出目录（Gradle）
├── pom.xml                                                # Maven 项目配置文件
├── build.gradle                                           # Gradle 项目配置文件
├── gradlew                                                # Gradle Wrapper 脚本（Unix）
├── gradlew.bat                                            # Gradle Wrapper 脚本（Windows）
├── gradle/                                                # Gradle Wrapper 目录
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── .gitignore                                             # Git 忽略文件
├── README.md                                              # 项目说明文档
├── Dockerfile                                             # Docker 配置文件
├── docker-compose.yml                                     # Docker Compose 配置
└── docs/                                                  # 项目文档目录
    ├── api.md
    └── deployment.md
```

## 详细目录说明

### 1. src/main/java/ - 主要源代码目录

#### 1.1 主启动类

- **位置**: `src/main/java/com/example/myproject/MyProjectApplication.java`
- **作用**: 包含 `@SpringBootApplication` 注解的主类，是应用程序的入口点
- **特点**: 通常包含 `main` 方法，用于启动 Spring Boot 应用

#### 1.2 config/ - 配置类目录

- **作用**: 存放各种配置类，如 Web 配置、数据库配置、安全配置等
- **常见文件**:
  - `WebConfig.java`: Web 相关配置
  - `DatabaseConfig.java`: 数据库配置
  - `SecurityConfig.java`: 安全配置
  - `RedisConfig.java`: Redis 配置

#### 1.3 controller/ - 控制器目录

- **作用**: 存放 REST API 控制器和 Web 控制器
- **注解**: `@RestController`, `@Controller`
- **职责**: 处理 HTTP 请求，调用服务层，返回响应

#### 1.4 service/ - 服务层目录

- **作用**: 业务逻辑层，处理核心业务逻辑
- **结构**:
  - 接口: `UserService.java`
  - 实现类: `impl/UserServiceImpl.java`
- **注解**: `@Service`

#### 1.5 repository/ - 数据访问层目录

- **作用**: 数据访问层，与数据库交互
- **类型**:
  - JPA Repository: 继承 `JpaRepository`
  - MyBatis Mapper: 使用 `@Mapper` 注解
- **注解**: `@Repository`

#### 1.6 entity/ - 实体类目录

- **作用**: 数据库实体类，映射数据库表
- **注解**: `@Entity`, `@Table`, `@Id`, `@Column` 等
- **特点**: 通常包含 getter/setter 方法

#### 1.7 dto/ - 数据传输对象目录

- **作用**: 用于不同层之间的数据传输
- **分类**:
  - `request/`: 请求 DTO
  - `response/`: 响应 DTO
  - `vo/`: 视图对象

#### 1.8 exception/ - 异常处理目录

- **作用**: 自定义异常类和全局异常处理器
- **文件**:
  - 自定义异常: `CustomException.java`
  - 全局异常处理: `@ControllerAdvice` 类

#### 1.9 utils/ - 工具类目录

- **作用**: 存放各种工具类和辅助方法
- **常见工具类**:
  - `DateUtils.java`: 日期工具类
  - `StringUtils.java`: 字符串工具类
  - `JsonUtils.java`: JSON 工具类

### 2. src/main/resources/ - 资源文件目录

#### 2.1 static/ - 静态资源目录

- **作用**: 存放静态文件，如 CSS、JavaScript、图片等
- **访问**: 可通过 HTTP 直接访问
- **结构**:
  - `css/`: 样式表文件
  - `js/`: JavaScript 文件
  - `images/`: 图片文件

#### 2.2 templates/ - 模板文件目录

- **作用**: 存放视图模板文件
- **模板引擎**: Thymeleaf, FreeMarker, JSP 等
- **特点**: 服务器端渲染的页面模板

#### 2.3 配置文件

- **application.yml/properties**: 主配置文件
- **application-{profile}.yml**: 环境特定配置
- **logback-spring.xml**: 日志配置
- **data.sql**: 数据初始化脚本
- **schema.sql**: 数据库结构脚本

#### 2.4 i18n/ - 国际化目录

- **作用**: 存放多语言资源文件
- **文件命名**: `messages_{locale}.properties`

### 3. src/test/ - 测试代码目录

#### 3.1 测试类结构

- **单元测试**: 测试单个组件或方法
- **集成测试**: 测试多个组件的协作
- **端到端测试**: 测试完整的业务流程

#### 3.2 测试注解

- `@SpringBootTest`: Spring Boot 测试
- `@WebMvcTest`: Web 层测试
- `@DataJpaTest`: JPA 层测试
- `@MockBean`: 模拟 Bean

### 4. 项目配置文件

#### 4.1 Maven 配置 (pom.xml)

```xml
- 项目基本信息
- 依赖管理
- 插件配置
- 构建配置
```

#### 4.2 Gradle 配置 (build.gradle)

```groovy
- 插件配置
- 依赖管理
- 任务定义
- 构建脚本
```

### 5. 其他重要文件

#### 5.1 .gitignore

- **作用**: Git 版本控制忽略文件
- **内容**: 编译输出、IDE 配置、日志文件等

#### 5.2 README.md

- **作用**: 项目说明文档
- **内容**: 项目介绍、安装指南、使用说明

#### 5.3 Dockerfile

- **作用**: Docker 镜像构建配置
- **用途**: 容器化部署

## 最佳实践

### 1. 包命名规范

- 使用反向域名: `com.company.project`
- 按功能分层: `controller`, `service`, `repository`
- 保持一致性和简洁性

### 2. 文件组织原则

- **按功能分层**: 不同层次的类放在对应包中
- **按模块分组**: 大型项目可按业务模块划分
- **遵循约定**: 使用 Spring Boot 约定的目录结构

### 3. 配置文件管理

- **环境分离**: 不同环境使用不同配置文件
- **敏感信息**: 使用环境变量或配置中心
- **配置分类**: 按功能模块组织配置

### 4. 测试代码组织

- **镜像结构**: 测试包结构与源码包结构对应
- **分层测试**: 按层次编写对应的测试
- **测试数据**: 独立的测试配置和数据

## 总结

Spring Boot 的目录结构设计遵循了 Maven/Gradle 的标准约定，通过清晰的分层架构和合理的包组织，使得项目具有良好的可维护性和可扩展性。理解并遵循这种目录结构有助于：

1. **提高开发效率**: 标准化的结构降低学习成本
2. **便于团队协作**: 统一的约定减少沟通成本
3. **简化部署流程**: 标准结构便于自动化构建和部署
4. **提升代码质量**: 清晰的分层有助于代码组织和测试

正确使用 Spring Boot 目录结构是构建高质量企业级应用的基础。

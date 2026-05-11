# 开发者技术社区平台

![Build Status](https://img.shields.io/badge/build-passing-green.svg)
![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)

## 项目简介

本项目是一个面向互联网开发者的内容分享平台，采用前后端分离架构，致力于帮助开发者成长和技术交流。平台提供文章发布、评论互动、收藏分享、消息通知等核心功能，为开发者打造一个专业的技术交流社区。

## 技术栈

| 分类 | 技术 | 版本 |
| :--- | :--- | :--- |
| 后端框架 | Spring Boot | 2.7.x |
| ORM框架 | MyBatis-Plus | 3.5.x |
| 数据库 | MySQL | 5.7+ / 8.0+ |
| 分布式缓存 | Redis | 5.0+ |
| 本地缓存 | Caffeine | 2.9.x |
| 消息队列 | RocketMQ | 4.9.x |
| 容器化 | Docker | 20.10+ |

## 核心特性

### 🔄 异步消息处理
- 基于 **RocketMQ** 实现点赞、评论、收藏、消息推送等操作的异步处理
- 实现核心业务与统计、通知模块的解耦，提升系统吞吐量和稳定性

### 🚀 高性能缓存架构
- **Redis** 实现白名单控制、用户活跃度排行、计数统计
- **Caffeine + Redis** 多级缓存设计，解决首页、专栏等热门数据的吞吐量瓶颈
- 完善的缓存一致性保障机制

### 📊 全链路日志追踪
- **AOP + 自定义注解 + MDC + TraceID** 实现日志全链路追踪
- 支持动态业务码（bizCode）注入、方法耗时统计与性能监控
- **Logback 自定义追加器** 实现异常邮件告警

### ⚡ 性能优化
- **Redis Pipeline** 批处理优化网络开销
- **@Async** 异步执行提升响应速度
- 并行访问优化，减少 60% 页面初始化时间

### 🐳 容器化部署
- 编写 **Docker Compose** 编排脚本
- 实现"一键拉起"开发环境，大幅缩短本地环境搭建时间

## 项目结构

```plaintext
paicoding/
├── paicoding-api/         # API 定义层
│   └── src/main/java/com/example/app/api/
│       ├── model/         # 数据模型（DO/DTO/VO）
│       └── enums/         # 枚举定义
├── paicoding-core/        # 核心组件层
│   └── src/main/java/com/example/app/core/
│       ├── cache/         # 缓存组件
│       ├── search/        # 搜索组件
│       ├── trace/         # 链路追踪
│       └── util/          # 工具类
├── paicoding-service/     # 业务服务层
│   └── src/main/java/com/example/app/service/
│       ├── article/       # 文章服务
│       ├── comment/       # 评论服务
│       ├── user/          # 用户服务
│       └── message/       # 消息服务
├── paicoding-ui/          # 前端资源层
│   └── src/main/resources/
│       ├── static/        # 静态资源
│       └── templates/     # 页面模板
├── paicoding-web/         # Web 控制层
│   └── src/main/java/com/example/app/web/
│       ├── controller/    # REST API 控制器
│       ├── config/        # 配置类
│       └── interceptor/   # 拦截器
└── pom.xml                # 父级 Maven 配置
```

## 快速开始

### 环境要求

- JDK 1.8+
- Maven 3.4+
- MySQL 5.7+ / 8.0+
- Redis 5.0+
- RocketMQ 4.9+

### 本地开发

1. **克隆项目**
```bash
git clone https://github.com/cyh6213/kaifazhe.git
cd kaifazhe/paicoding
```

2. **配置数据库**
```bash
# 创建数据库
CREATE DATABASE IF NOT EXISTS developer_community DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. **修改配置文件**

编辑 `paicoding-web/src/main/resources-env/dev/application-dal.yml`，配置数据库连接信息：

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/developer_community?useSSL=false&serverTimezone=Asia/Shanghai&characterEncoding=utf8mb4
    username: your_username
    password: your_password
```

4. **启动服务**

```bash
mvn clean install -DskipTests
cd paicoding-web
mvn spring-boot:run
```

5. **访问应用**

服务启动后，访问 `http://localhost:8080`

### Docker 一键启动

```bash
# 使用 Docker Compose 启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps

# 停止服务
docker-compose down
```

## API 文档

启动服务后，访问 `http://localhost:8080/doc.html` 查看完整的 API 文档。

## 目录说明

| 目录 | 说明 |
| :--- | :--- |
| `paicoding-api/` | 公共 API 定义，包含数据模型和枚举 |
| `paicoding-core/` | 核心组件，包含缓存、搜索、日志追踪等工具 |
| `paicoding-service/` | 业务逻辑层，处理具体业务逻辑 |
| `paicoding-ui/` | 前端资源，包含静态文件和页面模板 |
| `paicoding-web/` | Web 控制层，处理 HTTP 请求和响应 |

## 贡献指南

欢迎提交 Issue 和 Pull Request！

## 许可证

本项目采用 Apache License 2.0 许可证，详见 LICENSE 文件。
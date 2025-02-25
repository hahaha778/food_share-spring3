# 云南美食分享平台

## 项目介绍
这是一个基于Vue.js和Spring Boot的云南美食分享平台，旨在为用户提供一个分享美食、交流烹饪经验的在线社区。平台特别关注云南地方特色美食的展示和文化传播，支持美食菜谱发布、评论互动、营养分析等功能。

## 技术栈

### 前端技术
- Vue.js 2.6.11
  - Vue Router 路由管理
  - Vuex 状态管理
  - Axios HTTP客户端
- Element UI 2.15.14
  - 组件化开发
  - 主题定制
- WangEditor 富文本编辑器
- ECharts 4.8.0 数据可视化

### 后端技术
- Spring Boot 2.2.4
  - 自动配置
  - 依赖注入
  - AOP切面
- MyBatis ORM框架
  - SQL映射
  - 动态SQL
  - 缓存管理
- MySQL 5.7+ 数据库
- JWT 用户认证
- RESTful API设计
- Maven 项目管理

## 环境要求
- Node.js 12+
- JDK 1.8+
- MySQL 5.7+
- Maven 3.6+
- IDE推荐
  - 前端: VSCode/WebStorm
  - 后端: IntelliJ IDEA
  - 数据库: Navicat/MySQL Workbench

## 项目结构
```
food-share-platform/
├── 前端/
│   └── food-share-view/        # Vue.js前端项目
│       ├── src/
│       │   ├── api/           # API接口
│       │   ├── assets/        # 静态资源
│       │   ├── components/    # 公共组件
│       │   ├── router/        # 路由配置
│       │   ├── store/         # Vuex状态管理
│       │   ├── utils/         # 工具类
│       │   └── views/         # 页面组件
│       ├── public/            # 静态资源
│       └── package.json       # 项目依赖
├── 后端/
│   └── food-share-api/        # Spring Boot后端项目
│       ├── src/
│       │   ├── main/
│       │   │   ├── java/
│       │   │   │   └── cn/kmbeast/
│       │   │   │       ├── controller/  # 控制器
│       │   │   │       ├── service/     # 服务层
│       │   │   │       ├── mapper/      # 数据访问层
│       │   │   │       ├── pojo/        # 实体类
│       │   │   │       ├── utils/       # 工具类
│       │   │   │       └── config/      # 配置类
│       │   │   └── resources/           # 配置文件
│       └── pom.xml                      # Maven依赖
└── sql/
    └── food_share.sql                   # 数据库脚本
```

## 快速开始

### 数据库配置
1. 创建MySQL数据库：
```bash
CREATE DATABASE food_share DEFAULT CHARACTER SET utf8mb4;
```
2. 导入数据库脚本：
```bash
mysql -u your_username -p food_share < sql/food_share.sql
```

### 后端配置
1. 修改配置文件 `后端/food-share-api/src/main/resources/application.yml`：
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/food_share?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai
    username: your_username
    password: your_password
```

### 后端启动
1. 进入后端项目目录：
```bash
cd 后端/food-share-api
```
2. 安装Maven依赖：
```bash
mvn install
```
3. 运行Spring Boot应用：
```bash
mvn spring-boot:run
```

### 前端启动
1. 进入前端项目目录：
```bash
cd 前端/food-share-view
```
2. 安装依赖：
```bash
npm install
```
3. 启动开发服务器：
```bash
npm run serve
```

## 主要功能

### 用户功能
- 用户注册与登录
- 个人信息管理
- 密码修改
- 头像上传

### 美食管理
- 美食菜谱发布
- 图片上传处理
- 分类管理
- 菜谱搜索

### 社交互动
- 评论功能
- 点赞功能
- 内容分享
- 用户关注

### 营养分析
- 营养成分录入
- 营养分析报告
- 饮食建议
- 饮食记录

### 系统管理
- 用户管理
- 内容审核
- 分类管理
- 数据统计

## 安全特性
- JWT身份认证
- 密码加密存储
- XSS防护
- CSRF防护
- SQL注入防护
- 文件上传限制

## 性能优化
- 前端优化
  - 路由懒加载
  - 组件按需加载
  - 图片懒加载
  - 静态资源压缩
- 后端优化
  - 数据库索引优化
  - 查询缓存
  - 连接池管理
  - 分页查询

## 开发建议
1. 遵循编码规范
2. 使用Git进行版本控制
3. 编写单元测试
4. 做好代码注释
5. 定期代码审查

## 部署说明
1. 生产环境配置
2. 服务器要求
3. 负载均衡配置
4. 数据库优化
5. 监控配置

## 常见问题
1. 数据库连接问题
2. 跨域配置问题
3. 文件上传限制
4. 性能优化建议

## 更新日志
[版本更新记录]

## 贡献指南
欢迎提交问题和改进建议，一起完善这个项目！

## 版权信息
本项目仅用于学习和教育目的。 
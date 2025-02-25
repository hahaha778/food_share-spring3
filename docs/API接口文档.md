# 美食分享平台API接口文档

## 1. 接口规范

### 1.1 请求规范
```
基础URL: http://api.foodshare.com/v1

请求头:
- Content-Type: application/json
- Authorization: Bearer <token>
- Accept-Language: zh-CN

响应格式:
{
    "code": 200,          // 状态码
    "message": "success", // 提示信息
    "data": {}           // 响应数据
}
```

### 1.2 错误码说明
```
200: 成功
400: 请求参数错误
401: 未授权
403: 禁止访问
404: 资源不存在
500: 服务器错误
```

## 2. 用户接口

### 2.1 用户注册
```
POST /user/register

请求参数：
{
    "username": "string",   // 用户名
    "password": "string",   // 密码
    "email": "string",      // 邮箱
    "phone": "string"       // 手机号
}

响应数据：
{
    "code": 200,
    "message": "注册成功",
    "data": {
        "userId": 1,
        "username": "string",
        "token": "string"
    }
}
```

### 2.2 用户登录
```
POST /user/login

请求参数：
{
    "username": "string",   // 用户名
    "password": "string"    // 密码
}

响应数据：
{
    "code": 200,
    "message": "登录成功",
    "data": {
        "userId": 1,
        "username": "string",
        "token": "string",
        "avatar": "string"
    }
}
```

### 2.3 获取用户信息
```
GET /user/info

请求头：
Authorization: Bearer <token>

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "userId": 1,
        "username": "string",
        "nickname": "string",
        "avatar": "string",
        "email": "string",
        "phone": "string"
    }
}
```

## 3. 菜谱接口

### 3.1 发布菜谱
```
POST /cookbook/create

请求头：
Authorization: Bearer <token>
Content-Type: multipart/form-data

请求参数：
{
    "title": "string",        // 标题
    "content": "string",      // 内容
    "categoryId": 1,          // 分类ID
    "cover": "file",          // 封面图片
    "ingredients": "string",  // 食材
    "steps": "string",        // 步骤
    "isPublish": true        // 是否发布
}

响应数据：
{
    "code": 200,
    "message": "发布成功",
    "data": {
        "cookbookId": 1
    }
}
```

### 3.2 获取菜谱列表
```
GET /cookbook/list

请求参数：
{
    "categoryId": 1,      // 分类ID（可选）
    "keyword": "string",  // 搜索关键词（可选）
    "page": 1,           // 页码
    "pageSize": 10       // 每页数量
}

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "total": 100,
        "list": [
            {
                "id": 1,
                "title": "string",
                "cover": "string",
                "author": {
                    "id": 1,
                    "username": "string",
                    "avatar": "string"
                },
                "likeCount": 0,
                "commentCount": 0,
                "createTime": "2024-01-01 00:00:00"
            }
        ]
    }
}
```

### 3.3 获取菜谱详情
```
GET /cookbook/detail/{id}

路径参数：
- id: 菜谱ID

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "id": 1,
        "title": "string",
        "content": "string",
        "cover": "string",
        "ingredients": "string",
        "steps": "string",
        "author": {
            "id": 1,
            "username": "string",
            "avatar": "string"
        },
        "category": {
            "id": 1,
            "name": "string"
        },
        "nutriments": [
            {
                "id": 1,
                "name": "string",
                "value": "string",
                "unit": "string"
            }
        ],
        "likeCount": 0,
        "commentCount": 0,
        "createTime": "2024-01-01 00:00:00"
    }
}
```

## 4. 评论接口

### 4.1 发表评论
```
POST /comment/create

请求头：
Authorization: Bearer <token>

请求参数：
{
    "cookbookId": 1,     // 菜谱ID
    "parentId": 1,       // 父评论ID（可选）
    "content": "string"  // 评论内容
}

响应数据：
{
    "code": 200,
    "message": "评论成功",
    "data": {
        "commentId": 1
    }
}
```

### 4.2 获取评论列表
```
GET /comment/list

请求参数：
{
    "cookbookId": 1,  // 菜谱ID
    "page": 1,        // 页码
    "pageSize": 10    // 每页数量
}

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "total": 100,
        "list": [
            {
                "id": 1,
                "content": "string",
                "author": {
                    "id": 1,
                    "username": "string",
                    "avatar": "string"
                },
                "likeCount": 0,
                "createTime": "2024-01-01 00:00:00",
                "replies": [
                    {
                        "id": 2,
                        "content": "string",
                        "author": {
                            "id": 2,
                            "username": "string",
                            "avatar": "string"
                        },
                        "createTime": "2024-01-01 00:00:00"
                    }
                ]
            }
        ]
    }
}
```

## 5. 营养分析接口

### 5.1 添加营养信息
```
POST /nutriment/add

请求头：
Authorization: Bearer <token>

请求参数：
{
    "cookbookId": 1,
    "nutriments": [
        {
            "nutrimentId": 1,
            "value": "string"
        }
    ]
}

响应数据：
{
    "code": 200,
    "message": "添加成功",
    "data": null
}
```

### 5.2 获取营养分析报告
```
GET /nutriment/report/{cookbookId}

路径参数：
- cookbookId: 菜谱ID

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "cookbookId": 1,
        "nutriments": [
            {
                "id": 1,
                "name": "string",
                "value": "string",
                "unit": "string",
                "percentage": "string"
            }
        ],
        "recommendations": [
            {
                "type": "string",
                "content": "string"
            }
        ]
    }
}
```

## 6. 文件上传接口

### 6.1 上传图片
```
POST /file/upload

请求头：
Authorization: Bearer <token>
Content-Type: multipart/form-data

请求参数：
- file: 文件对象

响应数据：
{
    "code": 200,
    "message": "上传成功",
    "data": {
        "url": "string",
        "filename": "string"
    }
}
```

## 7. 搜索接口

### 7.1 搜索菜谱
```
GET /search/cookbook

请求参数：
{
    "keyword": "string",   // 搜索关键词
    "categoryId": 1,       // 分类ID（可选）
    "tags": ["string"],    // 标签（可选）
    "page": 1,            // 页码
    "pageSize": 10        // 每页数量
}

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "total": 100,
        "list": [
            {
                "id": 1,
                "title": "string",
                "cover": "string",
                "description": "string",
                "author": {
                    "id": 1,
                    "username": "string",
                    "avatar": "string"
                },
                "category": {
                    "id": 1,
                    "name": "string"
                },
                "tags": ["string"],
                "likeCount": 0,
                "commentCount": 0,
                "createTime": "2024-01-01 00:00:00"
            }
        ]
    }
}
```

## 8. 统计接口

### 8.1 获取用户统计数据
```
GET /stats/user

请求头：
Authorization: Bearer <token>

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "cookbookCount": 0,    // 发布菜谱数
        "likeCount": 0,        // 获赞数
        "commentCount": 0,     // 评论数
        "followCount": 0,      // 关注数
        "followerCount": 0     // 粉丝数
    }
}
```

### 8.2 获取菜谱统计数据
```
GET /stats/cookbook/{id}

路径参数：
- id: 菜谱ID

响应数据：
{
    "code": 200,
    "message": "success",
    "data": {
        "viewCount": 0,     // 浏览数
        "likeCount": 0,     // 点赞数
        "commentCount": 0,   // 评论数
        "shareCount": 0,    // 分享数
        "collectCount": 0    // 收藏数
    }
}
``` 
# 数据库设计

数据库表设计



## User

| key        | type     | description        |
| ---------- | -------- | ------------------ |
| uid        | INT      | 用户id，主键       |
| email      | CHAR     | 邮箱               |
| permission | TINYINT  | 权限               |
| nickname   | CHAR     | 用户名             |
| birthday   | DATETIME | 创建用户时间       |
| sex        | CHAR     | 性别               |
| avatar     | CHAR     | 头像               |
| publish    | INT      | 发布帖子数量       |
| heat       | INT      | 所有帖子的访问总量 |
| star       | INT      | 收到的赞           |
| hate       | INT      | 收到的批评         |



## Archive

| key        | type     | description      |
| ---------- | -------- | ---------------- |
| id         | INT      | 帖子id           |
| author_uid | INT      | 作者uid          |
| title      | CHAR     | 标题             |
| kind       | TINYINT  | 帖子类型         |
| contents   | TEXT     | 帖子内容         |
| views      | INT      | 访问量           |
| update_at  | DATETIME | 最后一次更新时间 |
| create_at  | DATETIME | 创建时间         |
| delete_at  | DATETIME | 删除时间         |



## discuss

| key        | type     | description |
| ---------- | -------- | ----------- |
| discuss_id | INT      | 评论id      |
| archive_id | INT      | 帖子id      |
| user_id    | INT      | 写者id      |
| seat       | INT      | 楼层        |
| contents   | CHAR     | 评论内容    |
| star       | INT      | 收到的赞    |
| create_at  | DATETIME | 创建时间    |
| delete_at  | DATETIME | 删除时间    |


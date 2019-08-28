# 数据库设计

数据库表设计



## User

| key        | type    | description        |
| :--------- | :------ | :----------------- |
| uid        | INT     | 用户id，主键       |
| email      | CHAR    | 邮箱               |
| nickname   | CHAR    | 用户名             |
| password   | CHAR    | 密码               |
| status     | INT     | 状态，封禁等       |
| user_dlc   | INT     | 指向User_dlc(外键) |



## User_dlc

| key           | type     | description        |
| ------------- | -------- | ------------------ |
| user_dlc_id   | INT      | 主键               |
| user_id       | INT      | 指向User表(外键)   |
| avatar        | CHAR     | 头像               |
| publish       | INT      | 发布帖子数量       |
| heat          | INT      | 所有帖子的访问总量 |
| sex           | CHAR     | 性别               |
| permission    | TINYINT  | 权限               |
| birthday      | DATETIME | 创建用户时间       |
| star          | INT      | 收到的赞           |
| hate          | INT      | 收到的批评         |
| archive_array | TEXT     | 帖子id的json数组   |
| options       | TEXT     | 扩展、可选         |





## Archive

| key           | type     | description      |
| ------------- | -------- | ---------------- |
| archive_id    | INT      | 帖子id           |
| author_id     | INT      | 作者uid(外键)    |
| title         | CHAR     | 标题             |
| kind          | TINYINT  | 帖子类型         |
| contents      | TEXT     | 帖子内容         |
| views         | INT      | 访问量           |
| update_at     | DATETIME | 最后一次更新时间 |
| create_at     | DATETIME | 创建时间         |
| delete_at     | DATETIME | 删除时间         |
| discuss_array | TEXT     | 评论的id数组     |
| options       | TEXT     | 扩展、可选       |



## discuss

| key        | type     | description  |
| ---------- | -------- | ------------ |
| discuss_id | INT      | 评论id       |
| archive_id | INT      | 帖子id(外键) |
| author_id  | INT      | 写者id(外键) |
| seat       | INT      | 楼层         |
| contents   | CHAR     | 评论内容     |
| star       | INT      | 收到的赞     |
| create_at  | DATETIME | 创建时间     |
| delete_at  | DATETIME | 删除时间     |
| options    | TEXT     | 扩展、可选   |


# # 接口设计
这是futanaicha论坛的api设计

## table of contents
### [account-service](#account-service)

+ `POST /api/account/new`创建用户
+ `GET /api/account/profile/$uid` 获取用户信息
+ `POST /api/account/profile/$uid` 修改用户信息
+ `GET /api/account/exist/$name` 判断用户是否存在

### [archive-service](#archive-service)

+ `POST /api/archive/new` 创建帖子
+ `GET /api/archive/del/$id` 删除帖子

+ `POST /api/archive/modify/$id` 修改帖子
+ `GET /api/archive/detail/$id` 获取帖子详细信息
+ `GET /api/archive/table/$page` 按照页数获取帖子列表

### [discuss-service](#discuss-service)

+ `POST /api/discuss/new` 创建评论
+ `GET /api/discuss/$id` 获取id帖子的评论

### [search-service](#search-service)

+ `GET /api/search` 搜索帖子

### [session-service](#session-service)

+ `POST /api/session/login` 登录
+ `GET /api/session/exist` 判断用户是否在线
+ `POST /api/session/permission` 判断用户权限
+ `GET /api/session/user` 根据cookie判断用户

### [static-service](#static-service)

+ `POST /api/static/upload` 上传资源

+ `GET /static/$date/$hash` 获取静态资源



## account-service

> account-service 账户相关操作

### POST /api/account/new

```typescript
// 例如：POST /api/account/new 用于创建新用户
Request = {
    method: "POST",
     heafers: {
        "Content-Type": "application/json"
    }   
    body: {
    	username: string
    	email: string
    	password: string //做两次hash计算
    	avatar: string
	}
}
```

```typescript
interface Response {
    code: number
    data:{
        uid: number
    }
}
```





### GET /api/account/profile/$uid

```typescript
// 例如：POST /api/account/profile/1 返回uid=1的用户信息
Request = {
    method: "GET"
}
```

```typescript
interface Response {
    code: number
    data: {
        uid: number
        username: string
        avatar: string
    }
}
```



### POST /api/account/profile/$uid

```typescript
// 例如：POST /api/account/profile/1 修改uid=1的用户数据
Request = {
    method: "POST",
     heafers: {
        "Content-Type": "application/json"
    }   
    body: {
    	username: string
    	email: string
    	password: string //做两次hash计算
    	avatar: string
	}
}
```

```typescript
interface Response {
    code: number
    data:{
        uid: number
    }
}
```



### GET /api/account/exist/$name

```typescript
// 例如：POST /api/account/exist/xxx 判断用户名是否存在
Request = {
    method: "POST"
}
```

```typescript
interface Response {
    code: number
    data:{
        username: string
        exist: bool
    }
}
```





## archive-service

> archive-service 用于帖子相关操作

### POST /api/archive/new

```typescript
// 例如： PSOT `/api/archive/new`
Request = {
    method: "POST",
    heafers: {
        "Content-Type": "application/json"
    }
    body: {
    	title: string
    	contents: string
    	hide: string //需要隐藏的内容
    	kind: number //种类
    	cover: string //封面
    	summary: string
	}
}
```

```typescript
interface Response {
    code: number // code<0失败，code=0成功
    data: {
        archive_id: number //创建的帖子id
    }
}
```



### GET /api/archive/table/$page

```typescript
// 例如：GET `/api/archive/table/1` 获取第一页的数据
Request = {
    method: "GET",
    params:{
        page: number
    }
}
```

```typescript
interface Response {
    code: number    // 正确为0， 错误为-1，权限不足为-2
    total: number   // 帖子总数
    residue：number // 剩余帖子数量
    data: Item[]	// 具体的内容
}
```

```typescript
interface Item {
    id: number
    title: string
    author: string
    author_id: number
    create_at: string
    update_at: string
    summary: string //摘要
    cover: string   
    kinds: number
    views: number
}
```



### GET /api/archive/detail/$id

```typescript
// 例如：GET `/api/archive/detail/1` 获取id=1的帖子的详细内容
Request = {
    method: "GET",
    params:{
        id: number
    }
}
```

```typescript
interface Response {
    code: number    // 正确为0， 错误为-1，权限不足为-2
    data: {
    	id: number  
    	title: string 
    	author: string 
    	author_id: number
    	create_at: string
    	update_at: string
    	contents: string //具体的内容
    	hide: string //隐藏的内容，返回空
    	cover: string   
    	kinds: number
    	views: number
    }
}
```



### GET /api/archive/del/$id

```typescript
// 例如：GET `/api/archive/del/1` 删除id=1的帖子
Request = {
    method: "GET",
    params:{
        id: number
    }
}
```

```typescript
interface Response {
    code: number
    data: {
        archive_id: number
        delete_at: string
    }
}
```





### POST /api/archive/modify/$id

```typescript
// 例如：GET `/api/archive/modify/1` 修改id=1的帖子
Request = {
    method: "GET",
    params:{
        id: number
    }
    heafers: {
        "Content-Type": "application/json"
    }
    body:{
    	title: string
        hide: string
        contents: string
        cover: string
	}
}
```

```typescript
interface Response {
    code: number
    data: {
        archive_id: number
        update_at: string
    }
}
```





## discuss-service

> discuss-service 评论相关操作

### POST /api/discuss/new

```typescript
// 例如：GET `/api/discuss/new` 创建评论
Request = {
    method: "GET",
    heafers: {
        "Content-Type": "application/json"
    }
    body:{
    	archive_id: number //帖子id
        contents: string
    }
}
```

```typescript
interface Response {
    code: number    // 正确为0， 错误为-1，权限不足为-2
    data: {
		seat:number //楼层
        create_at:string //创建时间
    }
}
```



### GET /api/discuss/$id

```typescript
// 例如：GET `/api/export/discuss/1?limit=50` 获取帖子id=1的评论，前50个
Request = {
    method: "GET",
    params:{
        id: number
    }
    query:{
    	limit:number
    }
}
```

```typescript
interface Response {
    code: number    // 正确为0， 错误为-1，权限不足为-2
    total: number   // 评论总数
    residue：number // 剩余评论的数量
    data: Item[]	// 具体评论的内容
}
```

```typescript
interface Item {
    id: number
    nickname: string
    avatar: string
    create_at: string
    contents: string
}
```



## search-service

> 搜索模块

### GET /api/search

```typescript
// 例如：GET `/api/search?kind=1&keyword=loli` 搜索相关的内容
Request = {
    method: "GET",
    query:{
    	kind: number
        keyword: string
        page: number
    }
}
```

```typescript
interface Response {
    code: number
    totail: number
    residue：number //剩余
    data: Item[]
}
```

```typescript
interface Item {
    id: number
    title: string
    author: string
    author_id: number
    create_at: string
    update_at: string
    summary: string //摘要
    cover: string   
    kinds: number
    views: number
}
```





## session-service

> 在线会话模块

### POST /api/session/login

```typescript
// 例如：POST `/api/session/login` 用户登录
Request = {
    method: "POST",
    heafers: {
        "Content-Type": "application/json"
    }
    body: {
    	username: string
    	password: string
	}
}
```

```typescript
interface Response {
    code: number
    data: {
        cookie: string
    }
}
```



### GET /api/session/exist

```typescript
// 例如：GET `/api/session/exist?username=xxx` 判断会话中是否有该用户
Request = {
    method: "GET",
    heafers: {
        "Content-Type": "application/json"
    }
    query: {
    	uid?: number
    	username?: string
	}
}
```

```typescript
interface Response {
    code: number
    data: {
        exist: bool
    }
}
```



### POST /api/session/permission

```typescript
// 例如：POST `/api/session/permission` 判断会话中用户的权限
Request = {
    method: "GET",
    heafers: {
        "Content-Type": "application/json"
    }
    body: {
    	type: number
    	uid: number
	}
}
```

```typescript
interface Response {
    code: number
    data: {
        type: number
        uid: number
        power: bool
    }
}
```



### GET /api/session/user

```typescript
// 例如：POST `/api/session/user` 通过cookie判断会话中用户信息
Request = {
    method: "GET",
    heafers: {
        "Content-Type": "application/json"
    }
    body: {
    	cookie: string
	}
}
```

```typescript
interface Response {
    code: number
    data: {
        uid: number
        username: bool
    }
}
```





## static-service

> 静态文件处理模块

### POST /api/static/upload

```typescript
// 例如：POST /api/static/upload 上传数据
Request = {
    method: "GET",
    heafers: {
        "Content-Type": "multipart/form-data"
    }
    body:{
    	file: File //文件
        size: string // 分辨率 例如@120x180
    }
}
```

```typescript
interface Response {
    code: number
    data: {
        hash: string //图片hash
        url: string  //图片路径
    }
}
```



### GET /static/$date/$hash

```typescript
//例如 /static/2019-8-29/dhquiiuw.jpg 获取静态资源
```


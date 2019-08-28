# # 接口设计
这是futanaicha论坛的api设计

## table of contents
+  [export-service](#export-service)
+  [account-service](#account-service)
+  [archive-service](#archive-service)
+  [discuss-service](#discuss-service)
+  [search-service](#search-service)
+  [session-service](#session-service)
+  [static-service](#static-service)



## export-service

> export-service 是读取数据的总出口

### GET /api/export/table/$page

```typescript
// 例如：GET `/api/export/table/1` 获取第一页的数据
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



### GET /api/export/archive/$id

```typescript
// 例如：GET `/api/export/archive/1` 获取id=1的帖子的详细内容
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
    data: Item	    // 具体的内容
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
    contents: string //具体的内容
    cover: string   
    kinds: number
    views: number
}
```



### GET /api/export/discuss/$id

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
	avatar:string
    create_at: string
    contents：string
}
```



## account-service



## archive-service



## discuss-service



## search-service



## session-service



## static-service
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

### GET /api/export

```typescript
// 例如：GET `/api/export?page=1`
Request = {
    method: "GET",
    query : {
        page: number
    }
}
```

```typescript
interface Response {
    code: number    // 正确为0， 错误为-1
    total: number   // 帖子总数
    residue：number //剩余帖子数量
    data: Archive[]
}
```

```typescript
interface Archive {
	id: number
	title: string
	author: string
	author_id: number
    summary: string //摘要
    cover: string   //封面
    kinds: number   //种类
	views: number
	create_at: string
	update_at: string
}
```



## account-service



## archive-service



## discuss-service



## search-service



## session-service



## static-service
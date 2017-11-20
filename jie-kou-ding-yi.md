# 接口文档 


## 文件列表

     POST /fileopera/list
     
### 描述
   
    根据父节点获取文件与文件夹信息
   
### Parameters
 ```
   {
     pid:11112323,
   }
 ```

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "data":[
    {
       path "/zhq/测试",
       "name":'测试',
       "f_id":'1232321',
       "is_dir":'1',
       "totol":'22222222',
       "num":2 
       } 
  ]
  
  

}
```

   
## 创建文件



	POST /fileopera/create

### 描述
     创建文件或文件夹同时更新全目录缓存 与 文件大小总数缓存
### Parameters
 ```
   {
     pid:11112323,
     name:'测试'
        }
 ```

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "path":"/zhq/测试",
  "name":'测试',
  "f_id":'1232321',
  "error":''
}
```
## 删除文件或文件夹



	POST /fileopera/delete

### 描述
     删除文件或文件夹同时更新全目录缓存 与 文件大小总数缓存 (支持批量)

### Parameters

{
  filelist:[id]
}
### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "error":'',
  "taskid":''
}
```
## 修改名称



	POST /fileopera/rename
### 描述
    根据 id 改名字  (支持批量)

### Parameters

filelist:[{"id":"1232321","newname":"CrossOver1"}]



### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "error":'',
  "taskid":''
}

```
## 移动文件



	POST /fileopera/move

### 描述
   移动文件到其他目录  同时更新 用户全目录缓存(支持批量)



### Parameters

filelist:[{"id":"12313","tofid":"123123","newname":"测试"}]



### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
"code": "0",
"msg": "Success",
"error":'',
"taskid":''
}

```

## 复制文件



	POST /fileopera/move

### 描述
   
复制的时候先找到 当前path的位置 然后向后移动文件数量大小 取出 更新path 然后复制到目录缓存/发送文件缓存中等数据库更新后 更新全文件缓存




### Parameters

filelist:[{"id":"xxxx","tofid":"xxxxx","newname":"xxxx"}]



### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
"code": "0",
"msg": "Success",
"error":'',
"taskid":''
}

```




## 发送文件



	POST /fileopera/send

### 描述
  发送目录创建待发送文件任务 缓存处理与复制同
### Parameters

filelist:[{"id":"1232",toid:'1232'}]



### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
"code": "0",
"msg": "Success",
"error":'',
"taskid":''
}

```


## 接收文件



	POST /fileopera/send


### Parameters

filelist:[{"pid":"1232"}]



### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
"code": "0",
"msg": "Success",
"error":'',
"taskid":''
}

```





## 任务查询接口



	POST /task/query


### Parameters

taskid:1111111


### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
"errno": "0",
"status": "Success",
"error":'',
"task_error":''
}

```















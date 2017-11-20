# 接口文档 


## 上传文件

## 创建文件



	POST /fileopera/create


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


## 发送文件



	POST /fileopera/send


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













# 接口文档 


## 上传文件

## 创建文件



	POST /fileopera/create


### Parameters
 ```
   {
     pid:xxxx,
     path:xxxx
   }
 ```

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "path":"xxxx",
  "name":'xxxxx',
  "f_id":'xxxxx',
  "error":''
}
```
## 删除文件或文件夹



	POST /fileopera/delete


### Parameters

{
  filelist:[xxxxxx]
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

filelist:[{"id":"xxxxxx","newname":"CrossOver1"}]



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





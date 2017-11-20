# 接口文档 


## 上传文件

## 创建文件夹



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
## 获取素材信息



	GET /fileopera/rename


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
## 文件素材树



	POST /resourcefolder/folderTree


### Parameters

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| id			| String			|  <p>素材或文件夹Id.</p>							|
| type			| String			|  <p>素材类型.</p>							|
| team_id			| String			|  <p>团队ID.</p>							|

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "result":"true"
}
```
## 批量获取素材信息



	POST /matter/listByIds


### Parameters

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| id			| String			|  <p>素材Id.</p>							|

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "result":"true"
}
```
## 批量移动文件



	POST /Resourcefolder/move


### Parameters

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| id			| String			|  <p>素材或文件夹Id.</p>							|
| type			| String			|  <p>素材类型.</p>							|
| from_folder_id			| String			|  <p>父文件ID.</p>							|
| team_id			| String			|  <p>团队ID.</p>							|
| to_folder_id			| String			|  <p>到那个文件.</p>							|

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "result":"true"
}
```
## 更新文件信息



	POST /Resourcefolder/update


### Parameters

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| id			| String			|  <p>素材或文件夹Id.</p>							|
| type			| String			|  <p>素材类型.</p>							|
| title			| String			|  <p>素材名称.</p>							|
| intro			| String			|  <p>素材简介.</p>							|
| from_folder_id			| String			|  <p>父文件ID.</p>							|
| team_id			| String			|  <p>团队ID.</p>							|
| to_folder_id			| String			|  <p>去往哪个文件.</p>							|

### Success Response

Success-Response:

```
HTTP/1.1 200 OK
{
  "code": "0",
  "msg": "Success",
  "result":"true"
}
```

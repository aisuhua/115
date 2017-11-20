# 接口文档 

- [resource](#resource)
	- [创建文件夹](#创建文件夹)
	- [删除素材或文件夹](#删除素材或文件夹)
	- [获取素材信息](#获取素材信息)
	- [文件素材树](#文件素材树)
	- [批量获取素材信息](#批量获取素材信息)
	- [批量移动文件](#批量移动文件)
	- [更新文件信息](#更新文件信息)


# resource
## 上传文件
    思路 :上传文件的时候 生成文件信息 更新文件与文件夹对应表 在redis 中生成
## 创建文件夹



	POST /Resourcefolder/create


### Parameters
 ```
   {
     pid:xxxx,
     file:xxxxx
   }
 ```

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
## 删除素材或文件夹



	POST /resourcefolder/delete


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
## 获取素材信息



	GET /resourcefolder/detail


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

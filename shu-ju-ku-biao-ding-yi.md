### 数据库表设计
  数据库设计想法
  1.上传后的文件存入文件地址表 同时在文件表中也对应一条记录
  2.文件表记录所有文件以及目录 还有父子关系
  3.目录文件对应表 记录目录下的文件与子目录
  4.文件副本存储 发送或复制时候生成的临时数据
  
    
**用户表\(t\_user\)**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | int | 主键 | | | | |
| user\_name | varchar | 用户名称 | | | | |
| nick\_name | varchar | 用户昵称 | | | | |
| phone | int | 手机号 | | | | |
| password | varchar | 密码 | | | | |
| status | tinyint | 用户状态\(0,1\) | | | | |
| created\_time | int | 创建时间 | | | | |
| updated\_time | int | 修改时间 | | | | |

**文件地址表\(t\_file_addres\)**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int | 主键 | | | | |
| file\_MD5 | varchar | 文件MD5 | | | | |
| file\_size | varchar | 文件夹详情 | | | | |
| file\_type | varchar | 文件类型 | | | | |
| files\_size | int | 文件大小 | | | | |
| file\_addres | varchar | 文件地址 | | | | |
| status | tinyint | 文件夹状态\(0,1\) | | | | |
| created\_time | int | 创建时间 | | | | |
| updated\_time | int | 修改时间 | | | | |

**文件表\(t\_file\)**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int | 主键 | | | | |
| parent\_id | int | 父Id | | | | |
| sorting | double | 排序 | | | | |
| file_link | int | 真实文件ID | | | | |
| user\_id | int | 用户id | | | | |
| path | varchar(255)| 目录地址(/root/www) | | | | |
| name | varchar | 文件名 | | | | |
| id_dir | tinyint | 是否是目录| | | | |
| files\_num | int | 文件夹下文件总数 | | | | |
| files\_size | int | 文件夹下文件总大小 | | | | |
| status | tinyint | 文件夹状态\(0,1\) | | | | |
| created\_time | int | 创建时间 | | | | |
| updated\_time | int | 修改时间 | | | | |


**文件发送表**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| file\_id | int | 主键\(文件或文件夹\) | | | | |
| send_user\_id | int | 发送用户id | | | | |
| take_user\_id | int | 接收用户id | | | | |
| type | tinyint | \(文件或者文件夹\) | | | | |
| status | tinyint | 是否接收\(0,1\) | | | | |
| created\_time | int | 发送时间 | | | | |
| updated\_time | int | 接收时间 | | | | |

**目录文件对应关系表\(t\_index\)**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| file\_id | int | 主键 | | | | |
| folder\_id | int | 主键 | | | | |
| path | varchar | 上级目录 | | | | |
| file\_name | varchar | 文件名称 | | | | |
| search\_key | varchar | (/父id/子id/孙id..记录到data_id的父id为止) | | | | |
| type | tinyint | \(文件或者文件夹\) | | | | |
| user\_id | int | 用户id | | | | |
| status | tinyint | 状态\(0,1\) | | | | |
| created\_time | int | 创建时间 | | | | |
| updated\_time | int | 修改时间 | | | | |
**文件操作任务表**

| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| task\_id | int | 主键 | | | | |
| data\_id | int | \(文件或文件夹Id\) | | | | |
| user\_id | int | 用户id | | | | |
| type | tinyint | 操作类型 | | | | |
| error | int | 错误类型 | | | | |
| created\_time | int | 发送时间 | | | | |
| updated\_time | int | 接收时间 | | | | |


**文件副本表\(临时存储,记录发送文件的信息副本\)t_(任务号)_copy_index**
| 字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| task\_id | int | 主键 | | | | |
| id | int | 主键 | | | | |
| parent\_id | int | 父Id | | | | |
| sorting | double | 排序 | | | | |
| file_link | int | 真实文件ID | | | | |
| user\_id | int | 用户id | | | | |
| path | varchar(255)| 目录地址(/root/www) | | | | |
| name | varchar | 文件名 | | | | |
| id_dir | tinyint | 是否是目录| | | | |
| files\_num | int | 文件夹下文件总数 | | | | |
| files\_size | int | 文件夹下文件总大小 | | | | |
| status | tinyint | 文件夹状态\(0,1\) | | | | |
| created\_time | int | 创建时间 | | | | |
| updated\_time | int | 修改时间 | | | | |




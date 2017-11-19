# 简易文件系统设计方案

### 目标

1.支持多用户  
2.数据库需要支持存储超过100亿\(?\)  
3.每次操作文件数量不能超过100万,大小不能超过500G  
4.文件发送后.对方可以在任意时候接收不受影响

### 设计与思路
        
#### 数据库存储问题

#### 发送与接收问题

#### 功能冲突问题

### 数据库设计


**用户表(t_user)**

|字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| user_id | int | 主键| | | | |
| user_name |varchar | 用户名称 | | | | |
| nick_name | varchar | 用户昵称 | | | | |
| phone | int | 手机号| | | | |
| password | varchar | 密码 | | | | |
| status | tinyint | 用户状态(0,1) | | | | |
| created_time | int | 创建时间 | | | | |
| updated_time | int | 修改时间| | | | |
**文件表(t_file)**

|字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int | 主键| | | | |
| file_name | varchar | 文件名称| | | | |
| file_MD5 | varchar | 文件MD5| | | | |
| file_size | varchar | 文件夹详情| | | | |
| file_type | varchar | 文件类型 | | | | |
| files_size | int | 文件大小| | | | |
| file_addres | varchar | 文件地址 | | | | |
| status | tinyint | 文件夹状态(0,1) | | | | |
| created_time | int | 创建时间 | | | | |
| updated_time | int | 修改时间| | | | |

**文件夹表(t_folder)**

|字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int |  主键|  |  |  |  |
| parent_id | int | 父Id |  |  |  |  |
| sorting | double | 排序 |  |  |  |  |
| user_id | int | 用户id |  |  |  |  |
| title | varchar |  文件夹名|  |  |  |  |
| intro | varchar |  文件夹详情|  |  |  |  |
| files_num | int | 文件夹下文件总数 |  |  |  |  |
| files_size | int |  文件夹下文件总大小|  |  |  |  |
| status | tinyint | 文件夹状态(0,1) |  |  |  |  |
| created_time | int | 创建时间 |  |  |  |  |
| updated_time | int |  修改时间|  |  |  |  |

**对应关系表(t_index)**

|字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| data_id | int |  主键|  |  |  |  |
| folder_id | int | 主键 |  |  |  |  |
| type | tinyint |  (文件或者文件夹)|  |  |  |  |
| user_id | int | 用户id |  |  |  |  |
| status | tinyint | 状态(0,1) |  |  |  |  |
| created_time | int | 创建时间 |  |  |  |  |
| updated_time | int |  修改时间|  |  |  |  |


**文件发送表**

|字段 | 类型 | 描述 | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| data_id | int | 主键(文件或文件夹)| | | | |
| user_id | int | 用户id (主键)| | | | |
| type | tinyint | (文件或者文件夹)| | | | |
| status | tinyint | 是否接收(0,1) | | | | |
| created_time | int | 发送时间 | | | | |
| updated_time | int | 接收时间| | | | |
**文件打包表(临时存储)**



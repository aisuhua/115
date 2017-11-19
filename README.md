# 简易文件系统设计方案

### 目标

1.支持多用户  
2.数据库需要支持存储超过100亿\(?\)  
3.每次操作文件数量不能超过100万,大小不能超过500G  
4.文件发送后.对方可以在任意时候接收不受影响

### 设计与思路

大致思路如下:

  ![](/assets/系统架构.png)

##### nginx集群

```
 一台作为主服务器，若干备服务器 每个服务器上安装Keepalived 服务 
 主服务器出现异常了或是宕机了 根据keepalived 状态 切换到可用的备用服务器
 这样比较方便进行水平扩展 与保证系统可适用性
```

##### 缓存

```
 采用redis 做 文件的目录缓存和文件夹顶点缓存 
 目录缓存: 主要缓存用户常用的目录信息 (目录下文件数 文件大小 子目录等信息)
 文件夹顶点缓存: 缓存发送文件夹的相关信息 从给定目录向下缓存一定层级的结构信息
```

##### mysql集群

```
  考虑到大数据存储压力 数据库设计为 <分布式DB方案>mysql做存储 mycat做代理
  进行 分库，分表，集群，负载均衡
  优点
  1.水平切分DB，有效降低了单台机器的负载，也减小了宕机的可能性。
  2.集群方案：解决DB宕机带来的单点DB不能访问问题。
  3.读写分离策略：极大限度提高了应用中Read数据的速度和并发量。
```

#### 功能冲突问题

采取乐观锁模式 对数据加锁处理

### 数据库表设计

**用户表\(t\_user\)**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | int | 主键 |  |  |  |  |
| user\_name | varchar | 用户名称 |  |  |  |  |
| nick\_name | varchar | 用户昵称 |  |  |  |  |
| phone | int | 手机号 |  |  |  |  |
| password | varchar | 密码 |  |  |  |  |
| status | tinyint | 用户状态\(0,1\) |  |  |  |  |
| created\_time | int | 创建时间 |  |  |  |  |
| updated\_time | int | 修改时间 |  |  |  |  |

**文件表\(t\_file\)**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int | 主键 |  |  |  |  |
| file\_name | varchar | 文件名称 |  |  |  |  |
| file\_MD5 | varchar | 文件MD5 |  |  |  |  |
| file\_size | varchar | 文件夹详情 |  |  |  |  |
| file\_type | varchar | 文件类型 |  |  |  |  |
| files\_size | int | 文件大小 |  |  |  |  |
| file\_addres | varchar | 文件地址 |  |  |  |  |
| status | tinyint | 文件夹状态\(0,1\) |  |  |  |  |
| created\_time | int | 创建时间 |  |  |  |  |
| updated\_time | int | 修改时间 |  |  |  |  |

**文件夹表\(t\_folder\)**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| id | int | 主键 |  |  |  |  |
| parent\_id | int | 父Id |  |  |  |  |
| sorting | double | 排序 |  |  |  |  |
| user\_id | int | 用户id |  |  |  |  |
| title | varchar | 文件夹名 |  |  |  |  |
| intro | varchar | 文件夹详情 |  |  |  |  |
| files\_num | int | 文件夹下文件总数 |  |  |  |  |
| files\_size | int | 文件夹下文件总大小 |  |  |  |  |
| status | tinyint | 文件夹状态\(0,1\) |  |  |  |  |
| created\_time | int | 创建时间 |  |  |  |  |
| updated\_time | int | 修改时间 |  |  |  |  |

**目录对应关系表\(t\_index\)**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| data\_id | int | 主键 |  |  |  |  |
| folder\_id | int | 主键 |  |  |  |  |
| type | tinyint | \(文件或者文件夹\) |  |  |  |  |
| user\_id | int | 用户id |  |  |  |  |
| status | tinyint | 状态\(0,1\) |  |  |  |  |
| created\_time | int | 创建时间 |  |  |  |  |
| updated\_time | int | 修改时间 |  |  |  |  |

**文件发送表**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| data\_id | int | 主键\(文件或文件夹\) |  |  |  |  |
| user\_id | int | 用户id |  |  |  |  |
| to_user\_id | int | 用户id |  |  |  |  |
| type | tinyint | \(文件或者文件夹\) |  |  |  |  |
| status | tinyint | 是否接收\(0,1\) |  |  |  |  |
| created\_time | int | 发送时间 |  |  |  |  |
| updated\_time | int | 接收时间 |  |  |  |  |

**文件操作任务表**

| 字段 | 类型 | 描述 |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| task\_id | int | 主键 |  |  |  |  |
| data\_id | int | \(文件或文件夹Id\) |  |  |  |  |
| user\_id | int | 用户id  |  |  |  |  |
| type | tinyint | 操作类型 |  |  |  |  |
| error | int | 错误类型 |  |  |  |  |
| created\_time | int | 发送时间 |  |  |  |  |
| updated\_time | int | 接收时间 |  |  |  |  |


**文件副本表\(临时存储,记录发送文件的信息副本\)**


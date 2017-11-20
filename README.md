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
 文件ID 有序集合  集合内容为父文件夹id 按照文件夹父子关系排序
 采用redis hash 作为用户目录缓存  键值对为 目录id 和 (目录下文件数 文件大小 子目录等信息) 的json   字符串   
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

#### 具体实现
    为了保证系统稳定性和效率 先加上2个限制 
    1.文件深度限制为20层
    2.文件大小限制为255位
      对文件的操作采取异步操作 用户操作触发后存入队列
    根据队列新建或修改索引 用户通过扫队列任务的状态
    来获知结果 
    目录缓存 : 记录用户常用的目录 (redis)
    文件大小与数量: 为每个用户建立2个有序集合分别存入文件夹内文件大小 与 数量 每次操作文件都更新缓存 这样有助于统计与排序 (ssdb|redis)
 
    目录缓存结构 用户id 为 key  {id}:{
       path:''
       empty:'' //是否为空
       is_dir:''//是否是文件夹
       p_id:''//
       id:''
       children [] //缓存分页的文件目录对象
    }
    具体实现见 接口文档
    
   
#### 功能冲突问题

采取乐观锁模式 对数据加锁处理



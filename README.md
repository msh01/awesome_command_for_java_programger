# 献给java程序员的常用Linux运维命令
[toc]

## 部署安装

```shell
# 杀死指定端口号的进程。比如我想要杀死8080端口目前监听的进程  
fuser -k -n tcp 8080
# 后台启动应用并把日志输入到指定的日志文件
nohup java -jar /software/apps/test/demo-0.0.1-SNAPSHOT.jar   > /software/logs/test/demo.log 2>&1 &
# 实时查看日志
tail -f  /software/logs/test/demo.log
# 查看服务对应的端口是否处于监听状态
netstat -apn | grep 8080 

```



## 资源监控

###  监控服务器可用内存

```shell
free -h 
```

###  监控服务器硬盘剩余存储

```shell
df -h
```

### 监控所有docker容器资源占用，并格式化输出

```shell
docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}" --no-stream
```

### 监控MongoDB磁盘占用

```javascript
// mongodb 存储空间占用 单位为GB
db.stats(1024*1024*1024);
```

### 监控MySQL磁盘占用

```sql
-- 在c中会有一个默认的数据库：information_schema，里面有一个Tables表记录了所有表的信息。使用该表来看数据库所占空间大小的代码如下：
-- 单位为GB
SELECT TABLE_SCHEMA, SUM(DATA_LENGTH)/1024/1024/1024 FROM TABLES GROUP BY TABLE_SCHEMA;
```





## 中间件相关

### nginx

```shell
 # 启动
/usr/local/nginx/sbin/nginx
# 停止
/usr/local/nginx/sbin/nginx -s stop
# 重新加载配置
/usr/local/nginx/sbin/nginx -s reload
# 检测配置文件是否正确
/usr/local/nginx/sbin/nginx  -t
```

### fastdfs 

```shell
# 启动，重启，停止



# tracker
/usr/bin/fdfs_trackerd  /etc/fdfs/tracker.conf  start
/usr/bin/fdfs_trackerd  /etc/fdfs/tracker.conf  restart
/usr/bin/fdfs_trackerd  /etc/fdfs/tracker.conf  stop


# storage  注意，storage.conf中配置的tracker的地址不能用localhost，应该用内网ip取代
/usr/bin/fdfs_storaged /etc/fdfs/storage.conf  start
/usr/bin/fdfs_storaged /etc/fdfs/storage.conf  restart
/usr/bin/fdfs_storaged /etc/fdfs/storage.conf  stop
```


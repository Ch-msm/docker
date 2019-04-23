Kafka工作时必须有确定的ip和端口，故运行容器时必须通过环境变量进行设置：

* `IP` 设置ip
* `PORT` 设置端口

例如:
```
$ docker run -d --restart=always \
  -p 9092:9092 \
  -e IP=172.17.0.1 -e PORT=9092 \
  --name "kafka" xm69/kafka:2.2.0
```

# 镜像制作步骤

注意:
1. 下载kafka和zookeeper并解压到resource/中,解压后文件夹应去除版本号；

2. 修改app/kafka/config/server.properties中对应配置项为列这样；
listeners=PLAINTEXT://0.0.0.0:9092
advertised.listeners=PLAINTEXT://localhost:9092
# 以下两个配置必须配合使用, 即检查间隔时间必须小于等于offsets超时时间.
## Frequency at which to check for stale offsets
offsets.retention.check.interval.ms=60000
## Offsets older than this retention period will be discarded
offsets.retention.minutes=1

3. 将app/zookeeper/conf/中的zoo_sample.cfg重命名为"zoo.cfg"。
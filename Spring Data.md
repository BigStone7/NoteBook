```shell
elasticsearch    | OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
elasticsearch    | {"type": "server", "timestamp": "2019-07-05T05:02:41,399+0000", "level": "WARN", "component": "o.e.b.ElasticsearchUncaughtExceptionHandler", "cluster.name": "docker-cluster", "node.name": "183f926dd64b",  "message": "uncaught exception in thread [main]" , 
elasticsearch    | "stacktrace": ["org.elasticsearch.bootstrap.StartupException: ElasticsearchException[failed to bind service]; nested: AccessDeniedException[/usr/share/elasticsearch/data/nodes];",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:163) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.execute(Elasticsearch.java:150) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.cli.EnvironmentAwareCommand.execute(EnvironmentAwareCommand.java:86) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.cli.Command.mainWithoutErrorHandling(Command.java:124) ~[elasticsearch-cli-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.cli.Command.main(Command.java:90) ~[elasticsearch-cli-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:115) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:92) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "Caused by: org.elasticsearch.ElasticsearchException: failed to bind service",
elasticsearch    | "at org.elasticsearch.node.Node.<init>(Node.java:580) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.node.Node.<init>(Node.java:251) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:221) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:221) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:349) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:159) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "... 6 more",
elasticsearch    | "Caused by: java.nio.file.AccessDeniedException: /usr/share/elasticsearch/data/nodes",
elasticsearch    | "at sun.nio.fs.UnixException.translateToIOException(UnixException.java:90) ~[?:?]",
elasticsearch    | "at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:111) ~[?:?]",
elasticsearch    | "at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:116) ~[?:?]",
elasticsearch    | "at sun.nio.fs.UnixFileSystemProvider.createDirectory(UnixFileSystemProvider.java:389) ~[?:?]",
elasticsearch    | "at java.nio.file.Files.createDirectory(Files.java:692) ~[?:?]",
elasticsearch    | "at java.nio.file.Files.createAndCheckIsDirectory(Files.java:799) ~[?:?]",
elasticsearch    | "at java.nio.file.Files.createDirectories(Files.java:785) ~[?:?]",
elasticsearch    | "at org.elasticsearch.env.NodeEnvironment.lambda$new$0(NodeEnvironment.java:271) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.env.NodeEnvironment$NodeLock.<init>(NodeEnvironment.java:208) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.env.NodeEnvironment.<init>(NodeEnvironment.java:268) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.node.Node.<init>(Node.java:271) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.node.Node.<init>(Node.java:251) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:221) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:221) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:349) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:159) ~[elasticsearch-7.2.0.jar:7.2.0]",
elasticsearch    | "... 6 more"] }
elasticsearch exited with code 1

```



docker容器启动命令：

docker run -itd --name es -p 9200:9200 -p 9300:9300 -v /data0/elasticsearch/data/:/usr/share/elasticsearch/data -v /data0/elasticsearch/logs/:/usr/share/elasticsearch/logs -e "discovery.type=single-node" 39.98.93.235:5000/my-es

部署elasticsearch时需要把数据和日志挂载在宿主机上，防止docker容器意外宕机时，可以保证数据的安全和方便根据日志进行错误排查。

把docker容器中的/usr/share/elasticsearch/data挂载到宿主机的/data0/elasticsearch/data下，日志同理。

但是看似很简单的命令，却报错了java.nio.file.AccessDeniedException: /usr/share/elasticsearch/data/nodes，看到这个错误的时候以为是容器中的/usr/share/elasticsearch/data/nodes目录权限不够，然后就开始各种授权，但是不行，折腾了半天时间，最后发现真正的原因是宿主机上的/data0/elasticsearch/data目录权限不足导致的！！！但是错误日志报的却是docker容器下的 /usr/share/elasticsearch/data/nodes目录，哎 浪费了大半天，仔细想想 把这2个文件绑定一起了，宿主机权限不足导致无法写入，影响到docker容器也无法正常写入，遇到问题还是要多思考啊！

具体解决方案很简单，就是给/usr/share/elasticsearch/data这个命令授权，日志文件目录同理。

chmod 777 /usr/share/elasticsearch/data
--------------------- 
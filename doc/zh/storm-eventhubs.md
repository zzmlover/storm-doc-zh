---
title: Azue Event Hubs 集成
layout: documentation
documentation: true
---

针对 Microsoft Azure Eventhubs 的 Storm spout 和 bolt 实现

### build ###
	mvn clean package

### 运行 topology 示例 ###
要运行 topology 示例, 您需要去修改 config.properties 文件与 eventhubs 配置. 
以下是一个例子:

	eventhubspout.username = [username: policy name in EventHubs Portal]
	eventhubspout.password = [password: shared access key in EventHubs Portal]
	eventhubspout.namespace = [namespace]
	eventhubspout.entitypath = [entitypath]
	eventhubspout.partitions.count = [partitioncount]

	# if not provided, will use storm's zookeeper settings
	# zookeeper.connectionstring=zookeeper0:2181,zookeeper1:2181,zookeeper2:2181

	eventhubspout.checkpoint.interval = 10
	eventhub.receiver.credits = 1024

然后您可以使用 storm.cmd 来提交 topology 示例:

	storm jar {jarfile} com.microsoft.eventhubs.samples.EventCount {topologyname} {spoutconffile}
	where the {jarfile} should be: eventhubs-storm-spout-{version}-jar-with-dependencies.jar

### 运行 EventHubSendClient ###
我们包括一个简单的 EventHubs send client 用于测试.
您可以像下面这样来运行 client:

	java -cp .\target\eventhubs-storm-spout-{version}-jar-with-dependencies.jar com.microsoft.eventhubs.client.EventHubSendClient
 	[username] [password] [entityPath] [partitionId] [messageSize] [messageCount]

如果想要发送消息到所有的 partition（分区）, 使用 "-1" 作为 partitionId.

### Windows Azure Eventhubs ###
	http://azure.microsoft.com/en-us/services/event-hubs/


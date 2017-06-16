# SparkStreaming-DirectKafka010

使用spark streaming Direct方式手动控制kafka消费偏移度

并将偏移度保存在zookeeper中

（代码中还有保存在本地文件系统中，稍微改动可以保存在其他存储中）

主要代码如下
```java

...

val kafkaParams = Map[String, Object](
      "bootstrap.servers" -> broker,
      "key.deserializer" -> classOf[StringDeserializer],
      "value.deserializer" -> classOf[StringDeserializer],
      "group.id" -> group,
      "auto.offset.reset" -> "latest",
      "enable.auto.commit" -> (false: java.lang.Boolean)
    )

...

KafkaUtils
    .createDirectStream[String, String](
        ssc,    //spark context
        PreferConsistent,
        Subscribe[String, String](topics, kafkaParams, newOffset)) // topic, kafkaParams, Manual offset
```





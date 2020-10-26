## word-count

入门的字数统计，注意这个只能用storm 0.9.2版本    
WordCount实例过程：  
(1)Spout中内置系列英文语句，随机发送;  
(2)使用一个Bolt接收Spout发送的消息，进行归一化处理，即拆词，发射；  
(3)按字段分组，接收上一个Bolt发送的单词，进行词频累加，并且排序，发射；  
(4)实时输出词频结果。  

线上环境运行步骤： 
mvn package
storm jar ./word-count-0.0.1-SNAPSHOT.jar com.blueegg.wordcount.WordCountTopology  word_count
storm ui中会出现拓扑，从supervisor summary看到在host3中运行，在host3 storm目录log下有worker-6700.log日志

## 如何获取maven依赖库

search.maven.org找storm-core，apache发布的

## 打包

把第三方库打包进去：mvn assembly:assembly  
不打包第三方库： mvn package  

## 进阶思考

为何每次排序字段不一样，如何改成一样？
storm每次发射一行数据过来，这个行是spout中我们写死的，normalizerBolt只是按空格分隔了下，去掉就变成行排序
由于没有历史的记录，故应该是无法打印每次单词排序一样的
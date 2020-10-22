# elasticsearch

# 1.1ES简介

ES是使用java 语言并且基于lucence编写的搜索引擎框架，他提供了分布式的全文搜索功能，提供了一个统一的基于restful风格的web 接口。

lucence:一个搜索引擎底层

分布式：突出ES的横向扩展能力

全文检索：将一段词语进行分词，并将分出的词语统一的放在一个分词库中，再搜索时，根据关键字取分词库中检索，找到匹配的内容（倒排索引）。

restful风格的web 接口：只要发送一个http请求，并且根据请求方式的不同，携带参数的不同，执行相应的功能。

应用广泛：WIKI, github,Gold man

# 1.2ES的由来

```
回忆时光**

许多年前，一个刚结婚的名叫 Shay Banon 的失业开发者，跟着他的妻子去了伦敦，他的妻子在那里学习厨师。 在寻找一个赚钱的工作的时候，为了给他的妻子做一个食谱搜索引擎，他开始使用 Lucene 的一个早期版本。

直接使用 Lucene 是很难的，因此 Shay 开始做一个抽象层，Java 开发者使用它可以很简单的给他们的程序添加搜索功能。 他发布了他的第一个开源项目 Compass。

后来 Shay 获得了一份工作，主要是高性能，分布式环境下的内存数据网格。这个对于高性能，实时，分布式搜索引擎的需求尤为突出， 他决定重写 Compass，把它变为一个独立的服务并取名 Elasticsearch。

第一个公开版本在2010年2月发布，从此以后，Elasticsearch 已经成为了 Github 上最活跃的项目之一，他拥有超过300名 contributors(目前736名 contributors )。 一家公司已经开始围绕 Elasticsearch 提供商业服务，并开发新的特性，但是，Elasticsearch 将永远开源并对所有人可用。

```

# 1.3ES和solr

1.solr 查询死数据，速度比es快。但是数据如果是改变的，solr查询速度会降低很多，ES的查询速度没有明显的改变

2.solr搭建集群 依赖ZK，ES本身就支持集群搭建

3.最开始solr 的社区很火爆，针对国内文档 少，ES出现后，国内社区火爆程度 上升，，ES的文档非常健全

4.ES对云计算和大数据支持很好

# 1.4倒排索引

1.将存放的数据以一定的方式进行分词，并将分词的内容存放到一个单独的分词库中。

2.当用户取查询数据时，会将用户的查询关键字进行分词，然后去分词库中匹配内容，最终得到数据的id标识

3.根据id标识去存放数据的位置拉去指定数据

# 2.1elasticsearch安装

http://hub.daocloud.io/    docker 镜像工厂地址

```yml
version: "3.1"
services:
  elasticsearch:
      image: daocloud.io/library/elasticsearch:6.5.4
      restart: always
      container_name: elasticsearch
      ports:
        - 9200:9200
  kibana:
      image: daocloud.io/library/kibana:6.5.4
      restart: always
      container_name: kibana
      ports:
        - 5601:5601
      environment:
        - elasticsearch_url=http://192.168.169.128:9200
      depends_on:
        - elasticsearch
```

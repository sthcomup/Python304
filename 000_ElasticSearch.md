[Elasticsearch原理](http://developer.51cto.com/art/201904/594615.htm)

[ik中文分词器的安装](https://www.jianshu.com/p/6c27faf42c7b)

##### ElasticSearch的安装配置

- ElasticSearch服务器[官方文档](https://www.elastic.co/guide/cn/elasticsearch/guide/current/running-elasticsearch.html)

  1. 5.0开始，ElasticSearch 安全级别提高了，不允许采用root帐号启动，所以我们要添加一个用户
2. wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-<version>.tar.gz
  3. tar -xvf elasticsearch-6.3.2.tar.gz
  4. cd elasticsearch-<version>
	5. ./bin/elasticsearch
  
- IK中文分词器

  - IK插件的版本,要和ElasticSearch对应,否则出错

  - ./bin/elasticsearch-plugin install [https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.6.1/elasticsearch-analysis-ik-5.6.1.zip]

  - 移除名为 ik 的analyzer和tokenizer,请分别使用 ik_smart 和 ik_max_word

    >ik_max_word 和 ik_smart 什么区别?
    >ik_max_word: 会将文本做最细粒度的拆分，比如会将“中华人民共和国国歌”拆分为“中华人民共和国,中华人民,中华,华人,人民共和国,人民,人,民,共和国,共和,和,国国,国歌”，会穷尽各种可能的组合；
    >ik_smart: 会做最粗粒度的拆分，比如会将“中华人民共和国国歌”拆分为“中华人民共和国,国歌”。
  
- [HayStack配置](https://blog.csdn.net/AC_hell/article/details/52875927)

  - 下载

    - pip install django-haystack
  	- pip install elasticsearch
  	
  - 注册

    - ```python
     INSTALLED_APPS = [
      'haystack', # 全文检索
      ]
      ```
  
  - 路由
  
    - url(r'^search/', include('haystack.urls')),
    
  - 配置
  
    	```python
  HAYSTACK_CONNECTIONS = {
        'default': {
            'ENGINE': 'haystack.backends.elasticsearch_backend.ElasticsearchSearchEngine',
            'URL': 'http://192.168.103.210:9200/', # Elasticsearch服务器ip地址，端口号固定为9200
            'INDEX_NAME': 'meiduo_mall', # Elasticsearch建立的索引库的名称
        },
    }
    
    # 当添加、修改、删除数据时，自动生成索引
    HAYSTACK_SIGNAL_PROCESSOR = 'haystack.signals.RealtimeSignalProcessor'
    ```
  
  - 创建索引类
  
    ```python
    from haystack import indexes
    from .models import SKU
    
    class SKUIndex(indexes.SearchIndex, indexes.Indexable):
        """SKU索引数据模型类"""
        text = indexes.CharField(document=True, use_template=True)
    
        def get_model(self):
            """返回建立索引的模型类"""
            return SKU
    
        def index_queryset(self, using=None):
            """返回要建立索引的数据查询集"""
            return self.get_model().objects.filter(is_launched=True)
    ```
    
  - 手动生成索引```python manage.py rebuild_index```
  
    
## 1.训练数据

CONLL格式，其中各列含义如下：

```
1	ID	当前词在句子中的序号，１开始.
2	FORM	当前词语或标点  
3	LEMMA	当前词语（或标点）的原型或词干，在中文中，此列与FORM相同
4	CPOSTAG	当前词语的词性（粗粒度）
5	POSTAG	当前词语的词性（细粒度）
6	FEATS	句法特征，在本次评测中，此列未被使用，全部以下划线代替。
7	HEAD	当前词语的中心词
8	DEPREL	当前词语与中心词的依存关系
```

在CONLL格式中，每个词语占一行，无值列用下划线'_'代替，列的分隔符为制表符'\t'，行的分隔符为换行符'\n'；句子与句子之间用空行分隔。

示例如：

```
1       坚决    坚决    a       ad      _       2       方式
2       惩治    惩治    v       v       _       0       核心成分
3       贪污    贪污    v       v       _       7       限定
4       贿赂    贿赂    n       n       _       3       连接依存
5       等      等      u       udeng   _       3       连接依存
6       经济    经济    n       n       _       7       限定
7       犯罪    犯罪    v       vn      _       2       受事

1       最高    最高    n       nt      _       3       限定
2       人民    人民    n       nt      _       3       限定
3       检察院  检察院  n       nt      _       4       限定
4       检察长  检察长  n       n       _       0       核心成分
5       张思卿  张思卿  n       nr      _       4       同位语
```

## 2.使用示例
#### 训练

```
from lightnlp.sp import GDP

gdp_model = GDP()

train_path = '/home/lightsmile/NLP/corpus/dependency_parse/THU/train.sample.conll'
vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'


gdp_model.train(train_path, dev_path=train_path, vectors_path=vec_path, save_path='./gdp_saves')
```

#### 测试

```
gdp_model.load('./gdp_saves')
gdp_model.test(train_path)
```

#### 预测

```
word_list = ['最高', '人民', '检察院', '检察长', '张思卿']
pos_list = ['nt', 'nt', 'nt', 'n', 'nr']
heads, rels = gdp_model.predict(word_list, pos_list)
print(heads)
print(rels)
```

预测结果如下，其中程序会自动在语句和词性序列首部填充``，因此返回的结果长度为`len(word_list) + 1`：

```
[0, 3, 3, 4, 0, 4]
['<ROOT>', '限定', '限定', '限定', '核心成分', '同位语']
```

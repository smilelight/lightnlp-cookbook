# 关系抽取，re
## 1.训练数据

训练数据示例如下，其中各列分别为`实体1`、`实体2`、`关系`、`句子`

```
钱钟书	辛笛	同门	与辛笛京沪唱和聽钱钟书与钱钟书是清华校友，钱钟书高辛笛两班。
元武	元华	unknown	于师傅在一次京剧表演中，选了元龙（洪金宝）、元楼（元奎）、元彪、成龙、元华、元武、元泰7人担任七小福的主角。
```

#### 

## 2.使用示例
#### 训练

```
from lightnlp.tc import RE

re = RE()

train_path = '/home/lightsmile/Projects/NLP/ChineseNRE/data/people-relation/train.sample.txt'
dev_path = '/home/lightsmile/Projects/NLP/ChineseNRE/data/people-relation/test.sample.txt'
vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'

re.train(train_path, dev_path=dev_path, vectors_path=vec_path, save_path='./re_saves')
```

#### 测试

```
re.load('./re_saves')
re.test(dev_path)
```

#### 预测

```
print(re.predict('钱钟书', '辛笛', '与辛笛京沪唱和聽钱钟书与钱钟书是清华校友，钱钟书高辛笛两班。'))
```

预测结果：

```
(0.7306928038597107, '同门') # return格式为（预测概率，预测标签）
```
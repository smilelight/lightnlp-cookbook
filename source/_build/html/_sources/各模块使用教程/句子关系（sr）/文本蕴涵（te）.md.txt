## 1.训练数据

tsv文件类型

训练数据示例如下，其中各列分别为`前提`、`假设`、`关系`，其中关系包括`entailment，蕴含`、`neutral，中立`、`contradiction，矛盾`

```
是的，我想一个洞穴也会有这样的问题      我认为洞穴可能会有更严重的问题。        neutral
几周前我带他和一个朋友去看幼儿园警察    我还没看过幼儿园警察，但他看了。        contradiction
航空旅行的扩张开始了大众旅游的时代，希腊和爱琴海群岛成为北欧人逃离潮湿凉爽的夏天的令人兴奋的目的地。    航空旅行的扩大开始了许多旅游业的发展。  entailment
当两名工人待命时，一条大的白色管子正被放在拖车上。      这些人正在监督管道的装载。      neutral
男人俩互相交换一个很大的金属环，骑着火车向相反的方向行驶。      婚礼正在教堂举行。      contradiction
一个小男孩在秋千上玩。  小男孩玩秋千    entailment
```

## 2.使用示例
#### 训练

```
from lightnlp.sr import TE

te_model = TE()

train_path = '/home/lightsmile/Projects/liuhuaiyong/ChineseTextualInference/data/te_train.tsv'
dev_path = '/home/lightsmile/Projects/liuhuaiyong/ChineseTextualInference/data/te_dev.tsv'
vec_path = '/home/lightsmile/NLP/embedding/char/token_vec_300.bin'

te_model.train(train_path, vectors_path=vec_path, dev_path=train_path, save_path='./te_saves')
```

#### 测试

```
te_model.load('./te_saves')
te_model.test(dev_path)
```

#### 预测

```
print(te_model.predict('一个小男孩在秋千上玩。', '小男孩玩秋千'))
print(te_model.predict('两个年轻人用泡沫塑料杯子喝酒时做鬼脸。', '两个人在跳千斤顶。'))
```

预测结果为：

```
(0.4755808413028717, 'entailment')
(0.5721057653427124, 'contradiction')
```

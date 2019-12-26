## 1.训练数据

tsv文件格式

训练数据示例如下：

```
呵呵    是王若猫的。
不是    那是什么？
怎么了  我很难过，安慰我~
开心点哈,一切都会好起来 嗯 会的
我还喜欢她,怎么办       我帮你告诉她？发短信还是打电话？
短信    嗯嗯。我也相信
你知道谁么      肯定不是我，是阮德培
许兵是谁        吴院四班小帅哥
```

## 2.使用示例
#### 训练

```
from lightnlp.tg import CB

cb_model = CB()

train_path = '/home/lightsmile/NLP/corpus/chatbot/chat.train.sample.tsv'
dev_path = '/home/lightsmile/NLP/corpus/chatbot/chat.test.sample.tsv'
vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'

cb_model.train(train_path, vectors_path=vec_path, dev_path=train_path, save_path='./cb_saves')
```

#### 测试

```
cb_model.load('./cb_saves')

cb_model.test(train_path)
```

#### 预测

```
print(cb_model.predict('我还喜欢她,怎么办'))
print(cb_model.predict('怎么了'))
print(cb_model.predict('开心一点'))
```

预测结果为：

```
('我你告诉她？发短信还是打电话？', 0.8164891742422521)
('我难过，安慰我', 0.5596837521537591)
('嗯会的', 0.595637918475396)
```

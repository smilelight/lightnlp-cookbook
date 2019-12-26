## 1.训练数据

tsv文件格式

训练数据示例如下：

```
Hi.     嗨。
Hi.     你好。
Run.    你用跑的。
Wait!   等等！
Hello!  你好。
I try.  让我来。
I won!  我赢了。
Oh no!  不会吧。
Cheers! 干杯!
He ran. 他跑了。
```

## 2.使用示例
#### 训练

```
from lightnlp.tg import MT

mt_model = MT()

train_path = '/home/lightsmile/NLP/corpus/translation/mt.train.sample.tsv'
dev_path = '/home/lightsmile/NLP/corpus/translation/mt.test.sample.tsv'
source_vec_path = '/home/lightsmile/NLP/embedding/english/glove.6B.100d.txt'
target_vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'

mt_model.train(train_path, source_vectors_path=source_vec_path, target_vectors_path=target_vec_path,
               dev_path=train_path, save_path='./mt_saves')
```

#### 测试

```
mt_model.load('./mt_saves')

mt_model.test(train_path)
```

#### 预测

```
print(mt_model.predict('Hello!'))
print(mt_model.predict('Wait!'))
```

预测结果为：

```
('你好。', 0.6664615107892047)
('！', 0.661789059638977)
```
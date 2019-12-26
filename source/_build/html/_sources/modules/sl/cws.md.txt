# 中文分词（cws）
## 1.训练数据

BIS

训练数据示例如下：

```
4 S
日 S
清 B
晨 I
， S
同 B
样 I
在 S
安 B
新 I
县 I
人 B
民 I
政 I
府 I
门 B
前 I
， S
不 B
时 I
有 S
民 B
众 I
专 B
程 I
来 I
此 S
拍 B
照 I
留 B
念 I
， S
有 S
的 S
甚 B
至 I
穿 B
着 I
统 B
一 I
的 S
服 B
饰 I
拍 B
起 I
了 S
集 B
体 I
照 I
。 S
```

## 2.使用示例
### 1.训练

```
from lightnlp.sl import CWS

cws_model = CWS()

train_path = '/home/lightsmile/NLP/corpus/cws/train.sample.txt'
dev_path = '/home/lightsmile/NLP/corpus/cws/test.sample.txt'
vec_path = '/home/lightsmile/NLP/embedding/char/token_vec_300.bin'

cws_model.train(train_path, vectors_path=vec_path, dev_path=dev_path, save_path='./cws_saves')
```

### 2.测试

```
cws_model.load('./cws_saves')

cws_model.test(dev_path)
```

### 3.预测

```
print(cws_model.predict('抗日战争时期，胡老在与侵华日军交战中四次负伤，是一位不折不扣的抗战老英雄'))
```

预测结果：

```
['抗日战争', '时期', '，', '胡老', '在', '与', '侵华日军', '交战', '中', '四次', '负伤', '，', '是', '一位', '不折不扣', '的', '抗战', '老', '英雄']
```
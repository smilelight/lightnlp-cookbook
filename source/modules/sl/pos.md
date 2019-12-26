# 词性标注（pos）
## 1.训练数据

BIS

训练数据示例如下：

```
只 B-c
要 I-c
我 B-r
们 I-r
进 B-d
一 I-d
步 I-d
解 B-i
放 I-i
思 I-i
想 I-i
， S-w
实 B-i
事 I-i
求 I-i
是 I-i
， S-w
抓 B-v
住 I-v
机 B-n
遇 I-n
， S-w
开 B-l
拓 I-l
进 I-l
取 I-l
， S-w
建 B-v
设 I-v
有 S-v
中 B-ns
国 I-ns
特 B-n
色 I-n
社 B-n
会 I-n
主 I-n
义 I-n
的 S-u
道 B-n
路 I-n
就 S-c
会 S-v
越 S-d
走 S-v
越 S-d
宽 B-a
广 I-a
。 S-w
```

## 2.使用示例
### 1.训练

```
from lightnlp.sl import POS

pos_model = POS()

train_path = '/home/lightsmile/NLP/corpus/pos/train.sample.txt'
dev_path = '/home/lightsmile/NLP/corpus/pos/test.sample.txt'
vec_path = '/home/lightsmile/NLP/embedding/char/token_vec_300.bin'

pos_model.train(train_path, vectors_path=vec_path, dev_path=dev_path, save_path='./pos_saves')
```

### 2.测试

```
pos_model.load('./pos_saves')

pos_model.test(dev_path)
```

### 3.预测

```
print(pos_model.predict('向全国各族人民致以诚挚的问候！'))
```

预测结果：

```
[('向', 'p'), ('全国', 'n'), ('各族', 'r'), ('人民', 'n'), ('致以', 'v'), ('诚挚', 'a'), ('的', 'u'), ('问候', 'vn'), ('！', 'w')]
```
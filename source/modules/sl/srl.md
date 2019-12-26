# 语义角色标注（srl）
## 1.训练数据

CONLL

训练数据示例如下，其中各列分别为`词`、`词性`、`是否语义谓词`、`角色`，每句仅有一个谓语动词为语义谓词，即每句中第三列仅有一行取值为1，其余都为0.

```
宋浩京  NR      0       O
转达    VV      0       O
了      AS      0       O
朝鲜    NR      0       O
领导人  NN      0       O
对      P       0       O
中国    NR      0       O
领导人  NN      0       O
的      DEG     0       O
亲切    JJ      0       O
问候    NN      0       O
，      PU      0       O
代表    VV      0       O
朝方    NN      0       O
对      P       0       O
中国    NR      0       B-ARG0
党政    NN      0       I-ARG0
领导人  NN      0       I-ARG0
和      CC      0       I-ARG0
人民    NN      0       E-ARG0
哀悼    VV      1       rel
金日成  NR      0       B-ARG1
主席    NN      0       I-ARG1
逝世    VV      0       E-ARG1
表示    VV      0       O
深切    JJ      0       O
谢意    NN      0       O
。      PU      0       O
```

## 2.使用示例
### 1.训练

```
from lightnlp.sl import SRL

srl_model = SRL()

train_path = '/home/lightsmile/NLP/corpus/srl/train.sample.tsv'
dev_path = '/home/lightsmile/NLP/corpus/srl/test.sample.tsv'
vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'


srl_model.train(train_path, vectors_path=vec_path, dev_path=dev_path, save_path='./srl_saves')
```

### 2.测试

```
srl_model.load('./srl_saves')

srl_model.test(dev_path)
```

### 3.预测

```
word_list = ['代表', '朝方', '对', '中国', '党政', '领导人', '和', '人民', '哀悼', '金日成', '主席', '逝世', '表示', '深切', '谢意', '。']
pos_list = ['VV', 'NN', 'P', 'NR', 'NN', 'NN', 'CC', 'NN', 'VV', 'NR', 'NN', 'VV', 'VV', 'JJ', 'NN', 'PU']
rel_list = [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]

print(srl_model.predict(word_list, pos_list, rel_list))
```

预测结果：

```
{'ARG0': '中国党政领导人和人民', 'rel': '哀悼', 'ARG1': '金日成主席逝世'}
```
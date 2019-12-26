## 1.训练数据

格式大致如下, 其中每行代表一个`sentence`和对应的`Actions`，两者用`|||`分隔，其中Actions包括三种：`Shift`、`REDUCE_R`和`REDUCE_L`，分别代表`移入`、`右规约`、`左规约`，其中sentence和Actions之间的序列长度对应关系为`len(Actions) = 2 * len(sentence) - 1` ：

```
Bell , based in Los Angeles , makes and distributes electronic , computer and building products . ||| SHIFT SHIFT REDUCE_R SHIFT SHIFT SHIFT SHIFT REDUCE_L REDUCE_R REDUCE_R REDUCE_R SHIFT REDUCE_R SHIFT REDUCE_L SHIFT REDUCE_R SHIFT REDUCE_R SHIFT SHIFT REDUCE_R SHIFT REDUCE_R SHIFT REDUCE_R SHIFT REDUCE_R SHIFT REDUCE_L REDUCE_R SHIFT REDUCE_R
`` Apparently the commission did not really believe in this ideal . '' ||| SHIFT SHIFT SHIFT SHIFT REDUCE_L SHIFT SHIFT SHIFT SHIFT REDUCE_L REDUCE_L REDUCE_L REDUCE_L REDUCE_L REDUCE_L SHIFT SHIFT SHIFT REDUCE_L REDUCE_R REDUCE_R SHIFT REDUCE_R SHIFT REDUCE_R
```

## 2.使用示例
#### 训练

```
from lightnlp.sp import TDP

tdp_model = TDP()

train_path = '/home/lightsmile/Projects/NLP/DeepDependencyParsingProblemSet/data/train.sample.txt'
dev_path = '/home/lightsmile/Projects/NLP/DeepDependencyParsingProblemSet/data/dev.txt'
vec_path = '/home/lightsmile/NLP/embedding/english/glove.6B.100d.txt'

tdp_model.train(train_path, dev_path=dev_path, vectors_path=vec_path,save_path='./tdp_saves')
```

#### 测试

```
tdp_model.load('./tdp_saves')
tdp_model.test(dev_path)
```

#### 预测

```
from pprint import pprint
pprint(tdp_model.predict('Investors who want to change the required timing should write their representatives '
                         'in Congress , he added . '))
```

预测结果如下：

```
{DepGraphEdge(head=(',', 14), modifier=('he', 15)),
 DepGraphEdge(head=('<ROOT>', -1), modifier=('Investors', 0)),
 DepGraphEdge(head=('Congress', 13), modifier=(',', 14)),
 DepGraphEdge(head=('Investors', 0), modifier=('who', 1)),
 DepGraphEdge(head=('he', 15), modifier=('added', 16)),
 DepGraphEdge(head=('in', 12), modifier=('Congress', 13)),
 DepGraphEdge(head=('representatives', 11), modifier=('in', 12)),
 DepGraphEdge(head=('required', 6), modifier=('timing', 7)),
 DepGraphEdge(head=('should', 8), modifier=('their', 10)),
 DepGraphEdge(head=('the', 5), modifier=('change', 4)),
 DepGraphEdge(head=('the', 5), modifier=('required', 6)),
 DepGraphEdge(head=('their', 10), modifier=('representatives', 11)),
 DepGraphEdge(head=('their', 10), modifier=('write', 9)),
 DepGraphEdge(head=('timing', 7), modifier=('should', 8)),
 DepGraphEdge(head=('to', 3), modifier=('the', 5)),
 DepGraphEdge(head=('want', 2), modifier=('to', 3)),
 DepGraphEdge(head=('who', 1), modifier=('want', 2))}
```

返回的格式类型为`set`，其中`DepGraphEdge`为命名元组，包含`head`和`modifier`两元素，这两元素都为`(word, position)`元组

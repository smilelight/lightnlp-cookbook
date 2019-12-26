## 1.训练数据

## 2.使用示例
#### 训练

```
from lightnlp.sl import POS

pos_model = POS()

train_path = '/home/lightsmile/NLP/corpus/pos/train.sample.txt'
dev_path = '/home/lightsmile/NLP/corpus/pos/test.sample.txt'
vec_path = '/home/lightsmile/NLP/embedding/char/token_vec_300.bin'

pos_model.train(train_path, vectors_path=vec_path, dev_path=dev_path, save_path='./pos_saves')
```

#### 测试

```
pos_model.load('./pos_saves')

pos_model.test(dev_path)
```

#### 预测

```
print(pos_model.predict('向全国各族人民致以诚挚的问候！'))
```

预测结果：

```
[('向', 'p'), ('全国', 'n'), ('各族', 'r'), ('人民', 'n'), ('致以', 'v'), ('诚挚', 'a'), ('的', 'u'), ('问候', 'vn'), ('！', 'w')]
```
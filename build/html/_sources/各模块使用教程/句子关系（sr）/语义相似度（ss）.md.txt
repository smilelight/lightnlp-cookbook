## 1.训练数据

tsv文件类型

训练数据示例如下，其中各列分别为`语句a`，`语句b`，`相似关系`，包括`0，不相似`，`1，相似`：

```
1       怎么更改花呗手机号码    我的花呗是以前的手机号码，怎么更改成现在的支付宝的号码手机号    1
2       也开不了花呗，就这样了？完事了  真的嘛？就是花呗付款    0
3       花呗冻结以后还能开通吗  我的条件可以开通花呗借款吗      0
4       如何得知关闭借呗        想永久关闭借呗  0
5       花呗扫码付钱    二维码扫描可以用花呗吗  0
6       花呗逾期后不能分期吗    我这个 逾期后还完了 最低还款 后 能分期吗        0
7       花呗分期清空    花呗分期查询    0
8       借呗逾期短信通知        如何购买花呗短信通知    0
9       借呗即将到期要还的账单还能分期吗        借呗要分期还，是吗      0
10      花呗为什么不能支付手机交易      花呗透支了为什么不可以继续用了  0
```

## 2.使用示例
#### 训练

```
from lightnlp.sr import SS

ss_model = SS()

train_path = '/home/lightsmile/Projects/NLP/sentence-similarity/input/atec/ss_train.tsv'
dev_path = '/home/lightsmile/Projects/NLP/sentence-similarity/input/atec/ss_dev.tsv'
vec_path = '/home/lightsmile/NLP/embedding/char/token_vec_300.bin'

ss_model.train(train_path, vectors_path=vec_path, dev_path=train_path, save_path='./ss_saves')
```

#### 测试

```
ss_model.load('./ss_saves')
ss_model.test(dev_path)
```

#### 预测

```
print(float(ss_model.predict('花呗更改绑定银行卡', '如何更换花呗绑定银行卡')))
```

预测结果：

```
0.9970847964286804
```
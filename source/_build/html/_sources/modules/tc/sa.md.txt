# 情感极性分析，sa
## 1.训练数据

tsv文件格式

训练数据示例如下：

```
        label   text
0       0       备胎是硬伤！
1       0       要说不满意的话，那就是动力了，1.5自然吸气发动机对这款车有种小马拉大车的感觉。如今天气这么热，上路肯定得开空调，开了后动力明显感觉有些不给力不过空调制冷效果还是不错的。
2       0       油耗显示13升还多一点，希望慢慢下降。没有倒车雷达真可恨
3       0       空调不太凉，应该是小问题。
4       0       1、后排座椅不能平放；2、科技感不强，还不如百万帝豪，最希望增加车联网的车机。像你好博越一样。3、全景摄像头不清楚，晚上基本上用处不大
5       1       车子外观好看，车内空间大。
6       1       最满意的真的不只一点，概括一下最满意的就是性价比了。ps:虽然没有s7性价比高(原厂记录仪,绿净)
7       0       底盘调教的很低，坐的感觉有些别扭，视角不是很好。
8       0       开空调时，一档起步动力不足。车子做工有点马虎。
```

#### 

## 2.使用示例
#### 训练

```
from lightnlp.tc import SA

# 创建SA对象
sa_model = SA()

train_path = '/home/lightsmile/Projects/NLP/chinese_text_cnn/data/train.sample.tsv'
dev_path = '/home/lightsmile/Projects/NLP/chinese_text_cnn/data/dev.sample.tsv'
vec_path = '/home/lightsmile/Downloads/1410356697_浅笑哥fight/自然语言处理/词向量/sgns.zhihu.bigram-char'

# 只需指定训练数据路径，预训练字向量可选，开发集路径可选，模型保存路径可选。
sa_model.train(train_path, vectors_path=vec_path, dev_path=dev_path, save_path='./sa_saves')
```

#### 测试

```
# 加载模型，默认当前目录下的`saves`目录
sa_model.load('./sa_saves')

# 对train_path下的测试集进行读取测试
sa_model.test(train_path)
```

#### 预测

```
sa_model.load('./sa_saves')

from pprint import pprint

pprint(sa_model.predict('外观漂亮，安全性佳，动力够强，油耗够低'))
```

预测结果：

```
(1.0, '1') # return格式为（预测概率，预测标签）
```

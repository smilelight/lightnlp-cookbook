# 文本摘要，ts
## 1.训练数据

tsv文件格式

训练数据示例如下：

```
徐州18岁农家女孩宋爽，今年考入清华大学。除了自己一路闯关，年年拿奖，还帮妹妹、弟弟制定学习计划，姐弟仨齐头并进，妹妹也考上区里最好的中学。这个家里的收入，全靠父亲务农和打零工，但宋爽懂事得让人心疼，曾需要200元奥数竞赛的教材费，她羞于开口，愣是急哭了... 戳腾讯公益帮帮她们！#助学圆梦# 江苏新闻的秒拍视频   徐州农家女孩考上清华，她的懂事让人心酸…
盖被子，摇摇篮，汪星人简直要把萌娃宠上天～细致周到有耐心，脾气还好，汪星人不愧是一届带娃好手[笑而不语]偶买噶视频的秒拍视频      带娃好手汪星人！把宝宝们宠上天[憧憬]
人们通常被社会赋予的"成功"所定义，“做什么工作”“赚多少钱”都用来评判一个人的全部价值，很多人出现身份焦虑。身份焦虑不仅影响幸福感，还会导致精神压力，甚至自杀。如果你也有身份焦虑，这个短片或许会有帮助。秒拍视频  感到压力大的同学看过来！如何缓解身份焦虑？[并不简单]
网友@星蓝seiran 教大家自制的捕捉器教程，简单方便，里面的洗洁精换成肥皂水或洗衣粉水都可以（用于溶解蟑螂腹部油脂防止爬出），白糖稍微多放点。怕蟑螂的童鞋，可以换成不透明的瓶子。转需~     这个厉害了！[good]
```

## 2.使用示例
#### 训练

```
from lightnlp.tg import TS

ts_model = TS()

train_path = '/home/lightsmile/NLP/corpus/text_summarization/ts.train.sample.tsv'
dev_path = '/home/lightsmile/NLP/corpus/text_summarization/ts.test.sample.tsv'
vec_path = '/home/lightsmile/NLP/embedding/word/sgns.zhihu.bigram-char'

ts_model.train(train_path, vectors_path=vec_path, dev_path=train_path, save_path='./ts_saves')
```

#### 测试

```
ts_model.load('./ts_saves')

ts_model.test(train_path)
```

#### 预测

```
test_str = """
            近日，因天气太热，安徽一老太在买肉路上突然眼前一黑，摔倒在地。她怕别人不扶她，连忙说"快扶我起来，我不讹你，地上太热我要熟了！"这一喊周围人都笑了，老人随后被扶到路边休息。(颍州晚报)[话筒]最近老人尽量避免出门!
            """

print(ts_model.predict(test_str))
```

预测结果为：

```
('，我不讹你，地上太热我要熟了！[允悲]', 0.03261186463844203)
```

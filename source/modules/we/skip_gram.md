# 跳字模型，skip_gram
## 1.训练数据

就普通的文本格式

训练数据示例如下：

```
第一章 陨落的天才
    
    “斗之力，三段！”
    望着测验魔石碑上面闪亮得甚至有些刺眼的五个大字，少年面无表情，唇角有着一抹自嘲，紧握的手掌，因为大力，而导致略微尖锐的指甲深深的刺进了掌心之中，带来一阵阵钻心的疼痛……
    “萧炎，斗之力，三段！级别：低级！”测验魔石碑之旁，一位中年男子，看了一眼碑上所显示出来的信息，语气漠然的将之公布了出来……
    中年男子话刚刚脱口，便是不出意外的在人头汹涌的广场上带起了一阵嘲讽的骚动。
    “三段？嘿嘿，果然不出我所料，这个“天才”这一年又是在原地踏步！”
    “哎，这废物真是把家族的脸都给丢光了。”
    “要不是族长是他的父亲，这种废物，早就被驱赶出家族，任其自生自灭了，哪还有机会待在家族中白吃白喝。”
    “唉，昔年那名闻乌坦城的天才少年，如今怎么落魄成这般模样了啊？”
```

## 2.使用示例
skip_gram共实现了三种模型，分别为基础softmax模型(SkipGramBaseModule)、基于负采样的优化模型(SkipGramNegativeSamplingModule)、基于层次softmax的优化模型(SkipGramHierarchicalSoftmaxModule).

三种模型提供的接口一致，如下所示：

#### 导入接口

```
from lightnlp.we import SkipGramBaseModule, SkipGramNegativeSamplingModule, SkipGramHierarchicalSoftmaxModule  # 分别导入skip_gram不同模型
```

#### 训练

```
# skip_gram_model = SkipGramHierarchicalSoftmaxModule()
skip_gram_model = SkipGramNegativeSamplingModule()
# skip_gram_model = SkipGramBaseModule()

train_path = '/home/lightsmile/NLP/corpus/novel/test.txt'
dev_path = '/home/lightsmile/NLP/corpus/novel/test.txt'

skip_gram_model.train(train_path, dev_path=dev_path, save_path='./skip_gram_saves')
```

#### 测试

```
skip_gram_model.load('./skip_gram_saves')

skip_gram_model.test(dev_path)
```

#### 预测

```
test_target = '族长'
print(skip_gram_model.evaluate(test_target, '他'))
print(skip_gram_model.evaluate(test_target, '提防'))
```

预测结果：

```
1.0
0.002815224463120103
```

#### 保存词向量

```
skip_gram_model.save_embeddings('./skip_gram_saves/skip_gram_ns.bin')
```

`./skip_gram_saves/skip_gram_ns.bin`文件内容：

```
623 300
<unk> -0.69455165 -1.3275498 -1.1975913 -0.3417502 0.13073823 1.3608844 0.15316872 -2.295731 0.45459792 0.09420798 -0.73944765 0.11755463 -1.6275359 0.6623806 0.8247673 1.7149547 -0.49345177 -0.5932094 -1.3025115 0.40126365 1.8675354 0.46296182 0.81418717 -0.51671696 -1.328723 -0.27371547 -1.5537426 1.0326972 0.11647574 0.1607528 0.5110576 -1.2010366 -0.81535685 0.5231469 2.212553 0.43934354 -0.8626878 1.5049676 -0.8135034 -0.8322859 0.068298176 0.7376674 0.6459309 0.07635216 -0.77374196 0.29933965 1.6596211 0.46682465 -0.8282705 -0.22142725 1.7853647 1.4777366 -0.63895816 2.1443112 -2.2435715 0.85962945 1.6643075 1.082537 -0.6922347 -2.2418396 -0.20210272 -1.2102528 -0.48685002 0.65887684 -0.2534356 -1.0342008 -1.1101105 0.94670665 0.21063486 -0.2467249 0.16507177 0.61120677 0.27850544 -1.0511587 -0.9382702 -0.105773546 -1.2759126 0.77076215 1.6730801 0.7634321 0.22365877 -1.7401465 -1.6434158 0.94023687 -1.3609751 -2.153141 0.3826534 0.32158422 -2.4204254 -2.1351569 -0.7265906 1.2896249 -1.6444998 0.62701744 3.9122646e-05 -1.348553 1.6431069 0.4589956 -1.8367497 0.81131816 0.13370599 0.9231004 -0.2677846 0.22468318 0.10889411 -1.0416583 0.016111592 -0.36729148 0.24761267 -1.143464 -0.6162608 -0.6412186 0.79434645 -0.11785016 1.8588868 -0.06067674 -1.1092484 -0.039183926 -0.5137064 -0.15945728 -1.4222018 0.31517547 -0.81327593 0.0048671463 -0.18886662 0.28870773 1.0241542 0.24846096 0.15484594 0.83580816 -0.59276813 0.12078259 -0.2424585 -0.1992609 -1.7673252 -0.45719153 0.3185026 0.052791957 0.072982006 0.27393457 0.24782388 -1.073425 0.2915962 -0.52252334 -0.0066470583 -0.4599936 0.34365907 0.7187273 -0.7599531 -0.5792492 1.1238049 0.8469614 -0.078110866 0.20481071 -0.015566204 0.39713895 0.27844605 -0.37874687 -0.32269904 0.18351592 -1.2942557 1.0065168 2.6649168 -0.09024592 -0.115473986 -0.29874867 0.5950803 -0.6491804 0.9974534 -1.0031152 -2.4024782 -0.11324192 0.3452371 -0.68466026 -0.7123374 -0.61712 -2.0060632 0.49333447 0.4248587 -0.05601518 0.099164896 1.8789287 -0.2811404 0.91072047 2.713236 1.3424015 -0.007254917 -1.2505476 -0.7478102 0.7299547 -0.089441456 -0.43519676 0.45425606 0.49322376 -1.0130681 -0.56024987 -0.74189216 0.5030309 -1.023638 -1.7686493 0.638495 0.612898 0.5948498 2.5866709 0.1675552 -0.059030745 -0.3356758 0.66674125 1.1920244 0.24162059 1.3198696 0.28690717 -2.68874 -0.48055518 -1.5761619 0.14664873 0.83967185 -0.7924626 0.7860132 -0.7246394 1.0014578 0.14658897 -0.64450735 0.86360186 2.015226 -0.06311106 0.54246426 -2.120671 0.60732156 -0.9577766 -0.962489 -0.13819228 -1.9003396 1.477142 0.13473822 -1.3756094 0.21764572 0.71171355 0.03748321 -0.393383 0.011907921 0.5097328 -0.710836 0.8421267 -0.89845014 -0.31148115 -0.12334009 -0.58898896 0.35046947 0.26125875 1.1667713 -0.77842957 -0.5580311 0.7409664 -1.3743105 -0.8576632 0.8552787 -0.70344007 -0.86729395 0.8507328 0.081006676 -0.36887273 0.93737006 -0.8049869 -1.1607035 -1.4482615 -0.4097167 0.45684943 -0.71613914 0.41646683 2.408504 -0.29688725 -0.45588523 -2.1563365 0.6449749 0.06401941 -0.5306914 1.9065568 -0.8465525 2.175783 0.6279667 -0.18118665 -0.7002306 0.08241815 -1.2743592 0.86315835 0.2589759 -0.11746242 -2.0128748 0.85062236 1.7910615 -0.23783809 0.22933501 0.8359954 -0.16953708 0.711695 -0.13198276 1.3160635 0.48212075 -0.83564043
<pad> 0.9462378 -1.0530922 0.26814827 0.75049055 -0.43643618 0.90060383 0.38048416 0.3394666 -0.6542603 -1.2994871 0.2035602 0.13271607 -0.0821392 0.6386408 -0.53183955 -0.21759015 1.3303281 -0.4926919 1.2892267 0.49860442 1.6501433 -0.5349831 1.7068337 1.1600994 0.4631011 1.0019102 -0.080210954 0.35248953 0.88543874 0.08718851 -0.50338817 -1.4847835 -0.5894625 -1.0142589 -0.37832302 -1.6291661 -0.12362847 1.8569889 0.47709444 0.6944984 1.5645366 -1.643663 -0.4542581 -1.7151413 -0.8393249 0.9062153 -0.047601987 -1.101938 -0.68224543 -0.39662254 0.5475226 -1.2819566 -0.86349916 -0.07766274 -0.27872422 -0.8497833 1.7615329 0.2950122 0.68848085 -0.26785335 0.08160306 0.5527327 -1.1441914 -0.8601009 -0.2983682 1.4938309 -0.7786196 0.29549783 0.08286876 0.33651295 0.45808968 0.10132327 -0.94001776 1.0869813 1.7297467 0.6415491 -3.0990815 -0.70891887 -0.62066174 0.8763827 0.75606215 0.18597008 0.782098 0.07622817 -0.55206585 0.72135127 -0.019433482 0.5038495 -0.94488984 1.4516689 0.18088494 1.3465247 -0.74685186 0.99718165 0.065872364 0.98572636 0.8221382 0.768447 -0.4056811 -0.9117917 -2.05203 -0.78518504 0.12391317 -0.033092286 0.46701878 -1.1559975 -0.89441043 0.36609322 -2.0792224 -0.57335913 -1.0121179 0.6026655 1.0777911 0.09417599 0.26320156 2.6018775 -0.2755741 0.9520457 -0.04128785 0.32038128 -0.5574524 0.26191193 0.18591642 -1.9010495 -0.27394825 0.65679026 0.29634175 -0.60466653 -1.3784024 0.7435744 -1.4532461 -0.037048157 -0.5559504 -1.1130326 -2.0174382 1.9073203 0.21787305 -0.14302431 -0.29675826 0.33756196 1.4894477 0.7317302 -2.0191894 -1.1759464 0.8036417 -0.37761644 0.9244614 -0.7413941 -0.08381902 -1.4885721 -1.6779492 -0.59202635 1.0431904 0.7708446 -0.041408855 -1.2213532 -0.2857886 0.7738537 -0.7683973 -0.3201996 -0.4752588 0.14970754 -1.5409429 0.4487029 -1.5121255 0.56920415 0.11346252 1.4692949 -0.0945662 2.142825 -2.618194 1.4771916 0.6997561 1.0059751 0.24992754 -1.8951392 -0.8522846 0.98763144 -0.8822291 0.11832724 -1.0928622 1.2359277 0.80170745 1.0475003 1.5270966 0.95872986 0.8958471 -1.2497357 -0.31796277 -0.8195951 0.51742077 -0.22876325 -0.5562857 -1.924446 1.2476108 -0.35275942 -1.6121302 0.57726604 0.20068043 1.1353028 -2.4147425 -0.8989361 -1.4968843 0.6448405 -0.8628415 0.88103485 -0.3248718 1.0207465 -1.3894114 -0.90123475 -2.6463938 0.9470338 -0.11909193 -0.61639553 0.7213106 0.8824293 -0.39685965 1.6633297 -1.107534 0.4709047 0.33735672 -0.056239445 0.35526997 -0.9191851 1.2952671 -0.75040734 -1.7293545 -0.5775496 0.006652971 0.3147311 -0.85833013 0.09456847 -1.0624956 -0.9020722 -0.09103666 1.7845771 1.9998456 -1.727455 -2.2023408 0.3902349 -0.24948567 -1.6048291 0.14066061 0.44590333 -0.93849236 -1.1319045 -0.62959474 -0.12584576 0.91559213 1.2120887 1.6113585 -0.2791995 -0.11430749 -2.109812 0.7273863 0.7348798 1.119425 0.89362687 0.25193694 0.07618663 0.07243939 -0.4955755 1.0170685 1.5341507 -0.5218003 -1.6152122 0.9274748 -1.6640632 -1.3126534 0.11114946 -0.65346044 -0.6130383 0.7909551 0.22126918 1.6984801 1.2792808 0.5046258 1.2279602 0.9770026 -1.145929 -0.0426054 -0.94418496 0.5853211 1.007048 0.36722738 0.17046496 -0.041508738 0.8590547 0.08046034 -0.60373837 0.64457446 -0.25976962 0.960138 1.0904832 1.8453016 0.018720066 1.3756162 1.0828762 -1.249238 0.79106873
， 0.900907 0.07571198 -0.7531744 1.374081 -0.051039666 0.7277553 -1.5629473 1.4199361 0.43262932 -0.68931437 0.38527122 -0.95629644 -0.67784256 1.0736706 -0.73837465 1.0659839 1.3746638 0.13170229 0.44516808 -1.3651135 0.6797121 -0.41324878 -0.74141294 0.6231089 -0.40646043 1.5950443 -0.4391045 -0.8985314 -1.1638266 -1.533541 0.5106473 -0.07254573 1.17701 0.14969468 -0.6091943 -0.0053135455 -0.24863426 0.8653415 -0.49431074 0.40305167 -0.019052468 -1.4530281 0.9524088 0.19623129 1.0812551 -0.7029672 0.98020416 0.4018916 -0.5362254 0.9625411 -0.86386 0.8559593 0.5985731 -0.31617114 -0.17114832 1.3930514 -1.2128835 1.4938599 0.7294261 0.0069873203 0.3011275 0.2884637 -0.4047188 1.379296 1.2289892 -1.3085986 -0.6356538 0.7275725 1.1327684 0.7107664 -0.6704246 1.5707167 -1.0520607 -0.43741754 -0.9605017 0.16557963 0.36883283 1.1963758 -0.33144 -0.7518608 1.893332 1.1943464 -0.78934395 -0.76964295 0.53341806 0.31912255 -0.12965271 0.82504976 0.40652457 0.53250855 0.58478385 0.41374293 -2.470195 -1.086166 0.35800576 -0.28109965 0.58450735 0.21001115 -0.5292711 -0.1143292 0.16091391 0.094074145 1.031662 -0.8089014 -1.628064 -1.2236967 -0.32958752 -0.820402 0.47758663 -0.898437 -1.8655137 -0.21954364 1.1573626 -0.104117766 -2.2046013 -0.8208049 1.1086514 -0.054544605 0.2467652 0.2508907 0.2763308 -0.7736183 0.09024833 0.83370477 0.05262025 0.43588457 0.18531433 -1.0218358 -1.2482029 1.6342846 0.1350406 0.48319736 -1.1814651 -0.4395637 -0.9084532 -0.13163663 0.54032123 -0.06305807 -2.0849159 0.10013642 0.6293322 -0.4718163 0.36614272 0.5720268 -1.5570002 -1.2315079 -0.44615552 0.29496512 0.16977848 -1.2484412 -0.43556735 -1.1373686 -0.9494889 -0.338307 -1.0883887 1.1661576 -0.0350004 1.320882 0.6900581 0.13241628 0.5577205 0.6651418 -0.08530449 -1.8400815 0.8255675 -0.16105038 -0.29304776 0.8107121 0.6333308 -1.0940876 0.88024515 -0.5324785 0.43230054 0.049219586 -0.71814626 1.1409131 0.8139713 -0.061693516 1.1890107 0.5615759 -0.37580553 -1.2222782 0.20085296 -1.016764 0.19151224 -0.65262973 0.37048474 0.9163911 -0.24613668 1.9023395 0.43596944 0.2687087 0.47053918 0.8914297 -0.004240907 -0.47343937 -0.6866243 -0.09460539 0.73561066 -0.62427306 0.60132945 0.17795962 -1.1010085 -0.6280967 0.18861601 -1.375108 -0.021241438 -0.79842293 -0.4369373 0.40747282 -1.1733543 -1.6447479 -0.45784566 1.8135945 -1.3265601 0.09651274 0.67698365 0.28879938 0.6917941 0.62988585 0.50987977 0.72340196 -0.46958932 -0.3729695 -0.012005955 0.4500639 0.2354974 -0.44309667 -0.30639353 1.7849098 -0.47391504 -0.097441934 -0.87036467 0.4343567 -0.73129076 0.34823084 -0.9211271 -1.4157289 -0.14143807 -0.17118739 0.20365688 0.49579987 -0.28146592 0.17587937 0.73483443 -0.7240221 0.21285006 -1.1389073 -0.872867 -0.808176 0.78133965 0.778077 0.84429437 -0.6242826 -1.6780285 0.89954937 -1.0216842 0.69884956 -0.47699523 -1.1182262 -0.94061846 0.8274227 0.77821773 -0.6390419 -0.03573271 0.24811082 -0.19128142 -0.95383316 1.0210499 0.31598154 0.935698 0.12872082 -0.079226725 -0.68159103 0.47343037 0.5274688 -1.1747869 -0.6254046 1.3211188 -0.6488405 -0.16827887 0.45877635 0.7407617 0.5414452 1.4700226 -0.17359328 0.43262202 0.13622835 -0.04152306 0.7327739 0.38002792 0.44764686 0.7599607 1.3506728 -1.2795128 0.5494145 -0.9258237 -0.10960347 1.3573207 0.87325376
的 -0.20160268 -0.21241257 -0.4043321 2.1909928 0.49679247 -0.1325275 0.42584014 0.24683614 -0.9702372 -1.8741518 -0.7252045 -0.49983644 -0.65247107 0.76959157 0.8259947 -0.6513283 -0.8979589 1.3167363 -0.2347999 1.0080328 0.04068194 -0.70863515 -0.3246833 -0.42160204 -1.4620594 -0.8168891 -0.28889376 0.96584153 -0.06742255 1.7455348 1.4442544 0.24048196 1.2854279 0.14298542 -0.6515416 -0.7833069 -1.2629595 -2.1125658 1.0249085 0.40845707 -1.2015674 -1.5291021 2.2098982 -2.1091754 -0.41207585 -1.0482799 0.78599465 0.31762454 -0.5183959 -1.3728874 -0.15425354 0.0436417 0.25058135 1.4118088 -1.0422605 -0.07541436 -1.1068802 0.9455314 -0.5711538 -0.6461189 -0.18952727 -0.21206772 0.7762203 0.02701252 -0.20934224 0.22475724 0.83357966 0.2729621 0.44660333 -1.3553737 0.52011245 0.805614 1.4149666 1.6287401 1.6888571 -0.48137692 -0.31397444 -0.9113469 -0.84345376 0.6603501 -0.01110802 -0.07945263 -0.3899895 -0.5179783 0.16231695 -0.8189658 0.4745495 0.25934523 0.44624203 0.38669428 0.48463246 -1.2172782 0.81605846 0.8540907 0.44676793 -2.2456388 0.39226332 0.32102612 1.3043944 0.8576041 0.20862296 -0.51472336 1.3458765 0.0749595 -0.09046895 2.0222366 0.66191554 1.2438471 1.487185 -0.8989187 0.74124473 -0.023372192 -0.44223523 0.6265085 -0.77208 -1.2376994 -0.015103638 0.05522992 0.09492233 -0.23367663 -0.51066947 0.7461931 0.027357863 0.96861994 0.32018813 1.3833076 -0.25898007 -0.78406125 -0.45310873 0.014744817 0.29670417 -0.14763092 -0.69623804 -0.5450609 0.94851893 0.26137534 1.1350462 -0.37602738 1.2355423 -0.5942697 -0.40257028 0.14945346 -1.1114887 -0.33638072 -0.8206219 -0.49885294 0.48334897 -0.18454923 0.37010637 -0.1678072 0.37671828 0.4342044 -0.6350701 -0.45998573 -0.017748803 0.7512209 -0.077632286 -0.014426709 0.3794435 -1.424685 -0.9906908 -0.18001547 0.5476539 0.5737612 1.0301657 -1.4586309 -0.13719666 1.2435308 -0.83659005 -0.5306402 0.5618243 0.09081328 -1.3465264 1.4966936 0.09357808 -1.1012143 -0.8601246 1.5156639 2.2984858 0.48021093 0.48690277 0.10015719 -1.1285332 0.033390086 0.75665116 0.33436894 -0.76391685 0.38092253 -0.5958041 0.14064594 -0.97736394 -0.61810505 -0.19199394 0.5802718 -2.0147579 1.2695452 -0.76885015 2.0117762 1.6867042 0.40166444 -1.2177283 0.9590221 0.42674235 -0.19682969 0.5186299 -1.2642647 -0.8827122 0.6405918 -0.75486416 1.4068292 0.08357187 -1.7767766 -1.399881 -0.48782966 -0.17888801 -0.2964377 0.46553472 0.5966398 1.6487685 -0.9368118 -2.1757812 0.3725775 0.17232625 -0.57584375 -2.0905218 1.1426715 0.16465737 -0.21529475 0.04670203 -1.2801889 0.96900284 1.024924 1.7386234 -0.42269483 -0.019390948 0.21670038 1.6658463 0.50636417 -0.5177907 -0.028692413 -0.20513107 -0.5925592 0.9350939 -0.31975344 -0.77178174 0.64559805 -0.19214787 -0.59565204 0.044145744 -0.67553836 -0.6401371 -0.7174468 -0.08718807 1.4099891 -0.64017993 0.093481496 -1.288413 -2.2056794 0.29075697 0.068356246 0.14803462 -0.89601153 -0.86346716 -0.49652 0.27589476 -1.5443418 -0.377951 -0.351205 -0.7131136 0.14281324 1.0897856 -0.5939442 1.2551428 -0.9339728 0.016592525 0.04654862 -0.40097335 0.62805176 2.1380942 -1.3083881 0.7333389 -0.36281568 0.07450257 0.018646415 -0.7296821 -0.9214585 -0.5921474 -0.30300933 -0.6692921 0.43340573 0.78606945 -0.34040892 0.2503277 0.037954286 0.40688336 1.2049704 0.10686994 1.8918518 1.416152 0.9152621
了 -0.11100567 1.8244103 0.99881077 -0.1217553 -1.2965926 2.5752037 -0.52939695 -0.024460727 1.481322 -1.6454383 -0.32412064 -0.812192 -0.6247802 0.5879142 -0.99333626 -0.09178917 1.2610664 0.17786814 -0.09755645 -1.381767 0.3328385 -0.28843904 -0.8976809 0.51493317 -0.2354604 0.7267729 -0.2759223 -0.875182 0.80424625 -0.68562067 0.345338 -0.36612466 0.68599254 -0.69162357 -0.74803936 0.4015563 -0.19871116 0.64606947 1.5207865 -0.5436914 0.7913142 -0.8087305 0.8900298 -1.2114931 0.29318812 0.010917914 0.794381 0.22564566 0.45246655 0.035850927 0.90022266 0.30116358 -0.08802621 0.22181591 -1.3465856 0.45377666 -1.1994032 -1.1599623 -0.90402436 0.4413774 -0.60787785 -0.18609983 -0.28758097 0.86769056 1.070895 0.18053351 1.5689834 -0.825002 -0.1844389 0.8352371 -2.0554366 -1.1158409 -1.1282442 0.3164764 0.81705356 1.3285462 -1.1886504 0.34115657 1.4381564 0.18249284 -2.3909829 -0.7105743 -1.3165226 2.6451735 0.044927556 1.8649187 -0.7606436 1.3267876 -0.8695353 -0.82985395 0.53350765 -1.5758001 0.07124073 0.3113274 -0.31943765 0.19381034 -0.40180263 -1.2200341 -0.46648136 -0.9460392 1.56903 -0.023224937 -0.109002806 -0.122972146 -0.38673204 -0.34158748 0.8986403 -1.3978604 0.30148593 0.10867346 0.5560802 0.6666235 -0.9128663 -0.11801989 -1.6656537 0.470698 1.1878209 0.21174078 -1.3163888 -0.88419724 1.2939 1.0864538 -0.59195155 1.3402531 0.9949826 1.0850434 1.9927737 -0.05526331 -0.9249912 -0.99546725 0.19423905 0.34155425 0.116912715 0.46196705 -0.22920796 0.62712306 0.19182688 2.545757 0.0005199494 0.047344636 1.4041449 -0.4366798 -0.30238223 -0.8592163 -0.1450108 -1.0397685 -1.7507579 0.35720333 -1.0890079 -1.0088387 -2.166981 -0.119711794 -0.894902 -0.34313017 -0.83818877 1.8535222 -0.35545102 1.1037723 -0.30759943 -0.073416024 -0.6099894 -0.082894325 0.5696355 0.02636172 -0.4934832 0.8380404 0.6522451 0.23057912 -0.97358364 -0.20894456 -0.6702974 -1.350783 -1.494697 0.6830102 -0.6583244 1.4899143 1.3386569 0.8388928 0.53304636 0.10571614 -1.6693112 0.34666675 -0.18932551 -1.1207005 -0.13619985 -0.37456858 1.6312733 -1.0417099 0.18789463 0.76180553 0.3472593 0.746827 -0.59724313 1.1076568 0.39835903 0.3250713 -0.890195 0.851977 -1.8276579 -0.5058599 0.038222674 -0.40975145 0.34742656 -0.656784 0.52408326 -0.24545604 0.6244086 1.5422938 -0.11375929 0.4439602 1.194646 0.108786985 -1.2637025 0.30540422 -0.6331694 -0.10961318 -0.269253 0.3094217 0.37967274 0.4198166 -0.7752912 0.93305284 -0.51205474 0.10966317 0.42575598 1.3847312 0.09545336 0.35880265 1.3952161 -0.50513256 0.6978953 -0.42724264 0.61427826 0.42278302 1.3981684 -0.21110083 -1.2695825 0.3271231 -0.18441366 -0.18477333 -1.5454911 0.89642715 -1.0348141 0.9462476 -0.97564644 0.33486953 0.015225394 0.66027576 -0.016567787 0.38754386 0.33223125 -0.01711932 0.81019586 1.8340786 -0.8252963 0.53832585 0.7248964 1.0357465 -1.7218229 0.7785235 -0.059777193 -1.6390696 -0.13061148 1.6316975 0.9055566 0.31447434 -0.050311707 -0.14748432 -1.152082 -0.32038185 -0.20986848 -0.3397427 0.7406922 0.19800813 -0.37535998 0.8428346 -0.74992263 -1.8344332 1.7500505 -0.019035367 -0.17899665 -1.7635467 0.27003205 -0.07612512 -0.0870243 0.9975619 -0.7678579 -0.51703197 -1.0690825 1.4577312 1.6575297 -0.5548624 0.60410196 1.4686142 0.36586297 0.55307645 -0.72146875 -1.1415323 1.8086451 -1.4277877
… 1.5090982 -0.12030965 -0.49108917 0.553509 0.8591837 0.36316723 0.67062587 -0.35389656 -0.37601423 0.4347592 -0.21231161 -0.0190618 -0.092252515 -0.8948071 -0.35531363 -0.6883051 0.98320943 -1.3508446 1.3872787 0.038260926 1.3760954 -0.96063673 -0.40200645 1.1017556 0.3531388 1.588081 1.8033375 -0.269804 -0.57227546 -0.93687373 0.21478365 -0.3091859 -0.28627992 -0.44842216 0.28986707 0.50668955 -0.12714297 0.40329775 0.2786915 -0.15945554 -0.072181724 -1.1862227 0.43608934 0.5287543 -0.15116562 0.28055522 0.33410925 -0.2543533 0.13481624 0.822775 -0.25385746 -1.9061172 -0.33296132 0.6996039 -0.02980973 0.15660484 0.92750925 0.14352156 0.51745534 0.83292395 -2.6289806 0.19450875 -0.19730678 0.69921744 0.6158621 -0.55871856 -0.8584412 -0.12929948 0.029738523 0.3390188 -1.9727246 -0.78936666 -2.1812136 -1.0392722 2.047485 0.32518044 -0.18576339 1.2273303 -0.1372615 -0.10400256 0.7829299 0.614227 1.2265315 -0.32849684 -1.829169 2.396865 -0.18662089 0.41651145 0.67483145 -0.25038102 0.91003495 -0.623002 0.8042123 -0.29000333 0.5248564 -0.5109571 -1.2964711 -0.68491465 -1.663857 0.89274037 0.38988277 -0.021962767 0.103607625 -0.010340261 -0.24129027 -0.19017185 -0.30158663 -1.6015892 0.15792845 -0.25693515 0.17915845 0.5200748 0.4175489 -0.4977316 -0.6749868 -0.5071436 -0.8346771 -0.88110495 0.025185872 -0.4367816 0.04352713 0.39762473 -0.46531925 -0.43724746 -0.7177102 -0.3682369 0.561147 -0.39390326 0.35378152 0.41432992 0.26307502 0.24112928 0.37295812 0.34381458 0.035766784 -1.3103579 -1.791835 0.022306077 1.1904793 -0.58638793 0.14341566 -0.30051395 0.40474305 1.1653486 -1.51402 -0.8725059 0.31818748 -0.47912052 -0.78443474 -1.8794175 1.0267793 0.5685301 -0.5732909 0.46504852 0.9766738 0.32158154 -0.6603262 0.110638835 0.899724 0.6087294 -0.29793775 0.031041417 -0.29028177 0.95917696 0.029481404 -1.0456511 0.20962428 2.5877905 0.30777544 1.4205157 -0.5609667 1.3714185 -1.6550691 -0.3033392 -1.0271896 0.7320804 1.7060531 -0.20705949 -0.25557384 -0.1358627 0.08981131 0.16696481 -0.23829576 1.0140337 0.6376786 -0.8297083 0.6914956 1.2876294 1.1641147 0.5714225 -0.5951064 -0.40035194 0.05664461 -0.07712284 0.5560351 -0.09779525 -0.16741481 -1.0268891 -0.7811151 0.9260142 -0.3978502 0.50975585 0.2891867 -0.46284804 0.40699214 -0.6509738 -1.0038178 -0.2018522 0.8137981 -0.22531015 1.2800273 -1.543597 0.50349194 -0.65495837 1.5992006 -0.15456946 -0.39201578 1.024163 0.05098209 1.2978015 -0.6115874 -0.09561463 -1.5342172 0.80156255 -1.1532938 -0.21155114 -1.1255947 0.49859214 -0.8305734 0.76576126 1.0035298 -1.2507325 0.034969218 -2.0024865 1.3010553 -0.0128532 -1.8367712 -0.47018003 -1.626798 0.5764391 -0.10373195 0.013681615 0.6368426 -0.27328128 -0.72183806 -1.1314341 -1.4741199 -0.7339853 1.0301492 -0.013149526 -1.26929 -0.5952624 -1.0160192 -0.00892491 0.52773505 0.1007514 0.047913335 -1.2911471 -0.942016 1.6295937 1.5446011 0.4706358 -0.41318798 -0.8102736 1.1772252 -1.1744756 0.39915764 -1.1615202 1.1721202 -0.68552047 -0.7426144 -1.2427216 0.06827004 -2.04893 1.0171161 -0.18418719 -0.17167264 0.01688471 -0.5838595 0.50578314 -0.34972578 0.5766365 0.23884809 -0.1105168 0.0633554 2.8148367 0.26426396 0.51255965 -0.8230475 0.5432819 0.122535184 0.04558672 0.79334635 0.6718906 -0.8498224 0.3440884 0.87352926 0.46972504 0.33059952 0.9709751
少女 0.43625292 -0.49615338 -0.80635625 -0.95218086 -0.7034901 -0.24982916 -0.19628817 -0.6407552 1.1144902 -0.18383415 0.240521 -0.48174432 -0.43238354 1.5460479 0.17876568 1.1772094 0.7226882 -0.40163878 -0.27529833 0.6727029 0.6616228 -0.4649058 -0.82819325 0.077967666 0.22773252 0.47824302 1.263238 0.16044211 -0.8465441 -0.03908252 1.5012993 -0.6464531 1.2720991 0.7075523 0.2655532 -0.16548817 0.18449956 -1.57685 -0.3937183 1.1220738 -0.024133356 0.061765857 0.9063283 0.63651776 -0.9984391 1.7219917 -0.16911109 0.3950257 -0.44229308 -0.042594746 -0.18409568 1.5873259 1.5174317 -0.7761925 0.85540444 -0.25851408 -1.7153916 0.21526498 -0.30503598 -1.0740207 -0.26189303 -0.7361771 0.3404945 0.6267011 1.6266515 -0.7249698 -2.5369713 -0.040242277 -0.1521137 -1.2230408 0.105983995 0.24729799 0.66424936 0.7428047 0.8017003 -1.6448103 -1.3638207 0.22201629 -1.6191676 1.7650356 0.8733405 1.2922136 0.15274213 0.56989926 1.3315401 0.3242414 -1.5333288 0.9968748 -0.26946962 -1.7603902 -0.06785398 -1.4466665 -0.2051215 1.0579334 -1.6114388 -0.6311598 -0.42203426 1.2702805 0.049536392 -1.5223664 -1.1988252 -0.005043749 1.2519345 -0.1971786 -0.15249117 -0.09027343 -0.68423694 0.05290712 1.1976366 -0.55118096 0.43239573 -0.3921759 -0.10146248 -0.84204507 -1.5519683 0.41450986 0.08121465 0.70506895 0.36502063 -1.8334937 0.0016303719 0.8337098 0.8315608 2.1455774 0.5289709 -0.15538014 0.18361539 1.5023578 -1.5350997 -0.34078425 -0.17852718 -0.2980528 0.3791773 0.13815962 1.0244071 0.3535323 0.45246312 -1.0676222 0.26734406 -0.7833891 -0.4830871 -0.81460315 0.40275338 -0.4218575 1.2936684 0.36921188 2.0835738 0.29924822 0.607953 0.13717254 1.3793758 -0.17895296 0.25180477 1.0935096 -2.4911408 0.059239827 1.4227028 1.0269765 -0.012899189 0.667102 -1.654389 0.32084498 -1.3945848 0.9240499 0.14125341 -0.40186697 0.46305555 1.4799619 -0.1761365 0.08784475 -0.16064519 -0.32681388 -0.9726041 -0.46950138 -0.10297061 -0.1305801 1.2899957 -0.20281254 1.5096477 0.579964 -2.1962826 -1.0500919 -0.75640684 -0.68146974 -0.61898047 -0.038223892 -0.63422275 -0.40183118 0.71116716 1.7054831 1.2117803 0.5540193 -0.7673277 0.8996408 2.1318727 1.3070806 0.3919676 -0.19198467 0.37812284 -1.5805892 1.622781 0.4241692 0.9778187 0.5272743 0.6481839 -0.91835433 -1.2837874 -1.0056475 -0.03336126 1.7704506 0.59232867 -0.6739266 0.4252755 -0.04943613 1.933676 -1.0441738 0.4929349 -0.5993543 -0.97701305 0.6164371 -1.2127788 1.2599823 -0.5473247 0.93479854 -0.6774386 0.59664416 -0.5358335 -0.6079708 0.7937759 0.5176709 0.2346288 -2.056608 -0.35982183 -0.6090097 0.8602409 0.055992365 -0.6665505 0.6803273 0.8781159 -0.028397428 0.6073012 0.5945208 0.7166259 -0.48727062 0.25150546 0.06475472 -0.33076963 -0.9388699 -0.47334203 1.1939013 0.78029764 0.022830477 -1.198792 1.2806718 0.1218006 0.05305545 1.0819892 -0.8576298 1.796153 -0.05783273 1.4125075 0.22831114 -0.14899425 -0.5525253 -0.8165426 0.043676265 -0.641531 -0.37138024 1.5661736 -1.2548814 0.12986626 -0.9875852 0.4007069 -0.23187949 0.4992489 0.2498534 -1.1453637 1.7015793 -0.91252553 0.07962135 0.7060094 -2.1144807 0.18295327 0.30965614 -0.36403483 0.39038125 -0.580957 0.33897293 -0.1780094 -0.03921564 0.55165535 -0.44981298 0.706237 0.13913499 -0.35856977 -0.20512235 -0.3393937 -1.9689944 2.374302 0.087832846
```
# 模型

- ner: BiLstm-Crf
- cws: BiLstm-Crf
- pos: BiLstm-Crf
- srl:BiLstm-Crf
- sa: TextCnn
- re: TextCnn,当前这里只是有监督关系抽取
- lm: Lstm,基础的LSTM，没有使用Seq2Seq模型
- ss: 共享LSTM + 曼哈顿距离
- te:共享LSTM + 全连接
- tdp: lstm + mlp + shift-reduce(移入规约)
- gdp: lstm + mlp + biaffine（双仿射）
- cbow: base、hierarchical_softmax、negative_sampling
- skip_gram: base、hierarchical_softmax、negative_sampling
- cb: Seq2Seq+Attention
- mt: Seq2Seq+Attention
- ts: Seq2Seq+Attention
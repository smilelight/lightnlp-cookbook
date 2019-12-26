# 安装

```
pip install lightNLP
```

建议使用国内源来安装，如使用以下命令：

```
pip install -i https://pypi.douban.com/simple/ lightNLP
```

## 安装依赖

由于有些库如pytorch、torchtext并不在pypi源中或者里面只有比较老旧的版本，我们需要单独安装一些库。

### 安装pytorch

请使用最新版本的Pytorch！

具体安装参见[pytorch官网](https://pytorch.org/get-started/locally/)来根据平台、安装方式、Python版本、CUDA版本来选择适合自己的版本。

### 安装torchtext

使用以下命令安装最新版本torchtext：

```
pip install https://github.com/pytorch/text/archive/master.zip
```
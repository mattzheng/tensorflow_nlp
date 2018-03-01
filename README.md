# NER任务
序列标注任务中，NER任务是非常常见的。使用较多：`biLSTM+CRF`，现有也有流行的`IDCNN+CRF`

## 1 现有的比较好的开源中文项目的库有：

 - [zjy-ucas/ChineseNER](https://github.com/zjy-ucas/ChineseNER)
 - [koth/kcws](https://github.com/koth/kcws)，加了IDCNN模块
 - [crownpku/Information-Extraction-Chinese](https://github.com/crownpku/Information-Extraction-Chinese/tree/master/NER_IDCNN_CRF)
 - [thunlp/TensorFlow-NRE](https://github.com/thunlp/TensorFlow-NRE)
 - [Determined22/zh-NER-TF](https://github.com/Determined22/zh-NER-TF)

还有一些比较成熟的模块：

 - [rockingdingo/deepnlp](https://github.com/rockingdingo/deepnlp/tree/master/deepnlp/pos)，开放了模型的使用，并且也可以根据其模型进行训练，目前也支持了`bilstm_crf、bilstm`

此中笔者最喜欢：[crownpku/Information-Extraction-Chinese](https://github.com/crownpku/Information-Extraction-Chinese/tree/master/NER_IDCNN_CRF)

模型中，训练集以及代码封装的非常好。只要把训练集模型放在指定的目录即可。

**该训练集标注的规范为IOB1:**
现有数据只包含以下三种实体类别：`机构组织ORG, 人名PER 和 位置LOC`

## 2 训练集参考：
训练数据(example.train)、验证数据(example.dev)和测试数据(example.test)，以及在wikipedia中文语料上预训练好的中文的字向量(vec.txt)

训练数据(example.train)、验证数据(example.dev)和测试数据(example.test)样式为：

```
海 O
钓 O
比 O
赛 O
地 O
点 O
在 O
厦 B-LOC
门 I-LOC
与 O
金 B-LOC
门 I-LOC
之 O
间 O
的 O
海 O
域 O
。 O

这 O
座 O
依 O
山 O
傍 O
水 O
的 O
博 O
物 O
馆 O
由 O
国 O
内 O
一 O
流 O
的 O
设 O
计 O
师 O
主 O
持 O
设 O
计 O
， O
整 O
个 O
建 O
筑 O
群 O
精 O
美 O
而 O
恢 O
宏 O
。 O

但 O
作 O
为 O
一 O
个 O
共 O
产 O
党 O
员 O
、 O
人 O
民 O
公 O
仆 O
， O
应 O
当 O
胸 O
怀 O
宽 O
阔 O
， O
真 O
正 O
做 O
到 O
“ O
先 O
天 O
下 O
之 O
忧 O
而 O
忧 O
， O
后 O
天 O
下 O
之 O
乐 O
而 O
乐 O
” O
， O
淡 O
化 O
个 O
人 O
的 O
名 O
利 O
得 O
失 O
和 O
宠 O
辱 O
悲 O
喜 O
， O
把 O
改 O
革 O
大 O
业 O
摆 O
在 O
首 O
位 O
， O
这 O
样 O
才 O
能 O
超 O
越 O
自 O
我 O
， O
摆 O
脱 O
世 O
俗 O
， O
有 O
所 O
作 O
为 O
。 O

```

中文的字向量(vec.txt)样式为：

```
16691 100
, -0.058550 0.125846 -0.083195 0.031818 -0.183519 ...
的 0.087197 -0.083435 0.057956 0.143120 -0.000068
```

## 3 语料获取:
高级模型的任务，训练集都弥足珍贵。中文实体识别的公开语料也是非常之少。
除了比赛、开源的数据集，如果自己去整可以有以下两种方式：

 - 1.用现成标注工具进行标注
 - 2.从已知的不同实体的词库出发，爬取含有相关词库的语料作为标注数据。

相关工具与语料、数据集的详情表可见：[crownpku/Awesome-Chinese-NLP](https://github.com/crownpku/awesome-chinese-nlp)


----------


### 延伸一：NER中标签规范（参考：[Correct example of IOB1 vs IOB2](https://github.com/stanfordnlp/CoreNLP/pull/230)）：
其中NER训练集默认只接受`IOB1`以及`IOB2`两种方案。
标签列表如下：

* B，即Begin，表示开始
* I，即Intermediate，表示中间
* E，即End，表示结尾
* S，即Single，表示单个字符
* O，即Other，表示其他，用于标记无关字符

用`Example:  Bill   works for  Bank   of     America and takes the Boston Philadelphia train.`这句话举例一下看看不同规格应该如何标注：


----------


### 参考资源：
[DL4NLP —— 序列标注：BiLSTM-CRF模型做基于字的中文命名实体识别](https://www.cnblogs.com/Determined22/p/7238342.html)

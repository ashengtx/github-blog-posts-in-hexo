---
title: Train Chinese Word2Vec
date: 2017-10-18 00:12:56
tags: NLP
---

代码在这[github](https://github.com/ashengtx/nlp-basic/tree/master/train-word2vec)

## 1 准备语料

分好词的文本，空格隔开，一行一个句子。


>你们 觉得 我们 看起来 够 年轻 溜进 高中 吗 ？
嗨 ， 亲爱 的 。 你 现在 肯定 忙 着 开会 呢 。
因为 你 想 在 进 养老院 前 娶妻生子 。
我 就 一天 24 小时 都 得 在 她 眼皮子 底下 。
找条 牢靠 的 链子 或者 别的 什么 固定 住 这些 灯 。
为了 不让 别的 父母 经历 我 的 遭遇 。
我要 去 赴约 会 ， 必须 学 跳舞 。 现在 就学 。
有时候 我们 信任 的 人 替 我们 做 了 这样 的 选择 。
好 吧 。 那么 ， 我 想 现在 能 做 的 有限 。
我 尊重 这点 ， 并且 会 不惜一切 保护 隐私 不 被 侵犯 。

分词可以用[jieba](https://github.com/fxsjy/jieba)

## 2 训练

用[gensim](https://radimrehurek.com/gensim/models/word2vec.html)训练

```python
import os
# import modules & set up logging
import gensim, logging
from gensim.models import Word2Vec
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

data_path = "./corpus"

class MySentences(object):
    def __init__(self, dirname):
        self.dirname = dirname
 
    def __iter__(self):
        for fname in os.listdir(self.dirname):
            for line in open(os.path.join(self.dirname, fname), encoding='utf8'):
                yield line.split()

sentences = MySentences(data_path) # a memory-friendly iterator
model = Word2Vec(sentences, size=300, window=5, min_count=5, workers=4)
model.save('./my-word2vec')
```

## 3 相似度计算

```python
# import modules & set up logging
import gensim, logging
from gensim.models import Word2Vec
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

model = Word2Vec.load("./my-word2vec")
print("(你, 我)的相似度是：", model.wv.similarity("你", "我"))
print("'你'的word2vec向量：")
print(model.wv['你'])
```

output:
```
(你, 我)的相似度是： 0.999860664953
'你'的word2vec向量：
[  1.12045869e-01  -1.68860483e-03   1.11759543e-01  ... ]
```

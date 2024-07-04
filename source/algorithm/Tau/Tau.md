# Tau

Evolution of tissue-specific expression of ancestral genes across vertebrates and insects中计算组织特异表达基因提到了一个参数`Tau`，文中参考文献`Genome-wide midrange transcription profiles reveal expression level relationships in human tissue specification.`，就来瞅一眼到底是个什么。

## 定义

$$\tau$$（Tau）定义为：
$$
\tau =  \frac{\sum_{n=1}^\N{(1-x_i)}}{N-1}
$$
其中，N为组织数量，基因x~i~为归一化后的表达谱。

TAU Index 计算，对于每一个基因基于他在不同组织的表达量，计算出一个0~1的数字。如果是1，那么这个基因就是在某个组织里面特异性表达。如果是接近1，比如0.9，那么就是组织偏好性表达。如果是接近0，那么就是倾向于组成型表达。

## 脚本

随手写一个python的脚本吧，还是比较抽象的，可以直接用TBtools

```python
import pandas as pd
import sys

exp_profile = sys.argv[1] # expression profile component normalized by the maximal component value
# 多个重复可求平均

exp_df = pd.read_csv(exp_profile, header=0, index_col=None, sep="\t")
n = exp_df.shape[1]
tau_df = exp_df.apply(lambda x: (n - x.sum)/(n-1), axis = 1)
```

## 参考

https://www.jianshu.com/p/8de865a420ad 参考CJ大哥
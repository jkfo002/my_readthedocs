# Tau

Evolution of tissue-specific expression of ancestral genes across vertebrates and insects中计算组织特异表达基因提到了一个参数`Tau`，文中参考文献`Genome-wide midrange transcription profiles reveal expression level relationships in human tissue specification.`，就来瞅一眼到底是个什么。

## 定义

$$\tau$$（Tau）定义为：
$$
\tau =  \frac{\sum_{n=1}^\N{(1-x_i)}}{N-1}
$$
其中，N为组织数量，基因x~i~为归一化后的表达谱。

TAU Index 计算，对于每一个基因基于他在不同组织的表达量，计算出一个0~1的数字。如果是1，那么这个基因就是在某个组织里面特异性表达。如果是接近1，比如0.9，那么就是组织偏好性表达。如果是接近0，那么就是倾向于组成型表达。

## 应用

`Evolution of tissue-specific expression of ancestral genes across vertebrates and insects`

计算$$\tau$$使用log~2~(TPMs+1)对表达矩阵进行normalized，定义**Tau > 0.75**与**maximum expressuib >= log~2~(5)**（由Tau分布定义）。

为了将基因分配给每个tissue，有
$$
expression~proportion~per~tissue = \frac{tissue~expr}{all~tissue~expr}\\
tissue~expr = \frac{\sum_{r=1}^\R{log_2(TMPs + 1)}}{R}\\
all~tissue~expr = \frac{\sum_{n=1}^\N{tissue~expr)}}{N}
$$

> where ‘tissue_expr’ is the average normalized log2(TPMs + 1) expression of the gene in the target tissue and ‘all_tissue_expr’ is the sum of the average normalized log2(TPMs + 1) expression values across all tissues.

几个标准：

> Specifically, we applied the following steps for each gene in each species (Extended Data Fig. 2c): (1) if the difference in expression proportion between the two most highly expressed tissues was ≥0.10 and their ratio ≥1.7, we associated the gene only with the top tissue. (2) If the above conditions were not fulfilled, but the difference in expression proportion between the second and third most highly expressed tissues was ≥0.15, we associated the gene with the two top tissues (double tissue specificity). (3) Otherwise, the gene was not considered as tissue specific and not associated with any tissue. 

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
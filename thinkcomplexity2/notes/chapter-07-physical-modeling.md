# 第7章：物理建模 (Physical Modeling)

> *"The cellular automatons we have seen so far are not physical models; that is, they are not intended to describe systems in the real world. But some CAs are intended as physical models. In this chapter we consider a CA that models chemicals that diffuse and react with each other, which is a process Alan Turing proposed to explain how some animal patterns develop. And we'll experiment with a CA that models percolation of liquid through porous material. This model is the first of several models that exhibit phase change behavior and fractal geometry, and I'll explain what both of those mean."*
> 我们之前看到的细胞自动机并非物理模型——它们并不旨在描述真实世界的系统。但有些 CA 确实被设计为物理模型。本章中，我们研究一个对化学物质扩散与反应进行建模的 CA，这是 Alan Turing 提出的解释某些动物图案形成的过程。我们还将实验一个对液体在多孔材料中的渗流进行建模的 CA。该模型是多个展现出相变行为和分形几何的模型中的第一个，我会解释这两个概念的含义。
| 单词/短语 | 注释 |
|-----------|------|
| physical models | 物理模型：旨在描述真实世界系统的数学模型，区别于纯抽象模型 |
| diffuse | 扩散：物质从高浓度区域向低浓度区域自发传播的过程 |
| percolation | 渗流：流体通过半多孔材料的过程 |
| phase change | 相变：系统在临界点附近行为的急剧转变，类比水在冰点从液态变为固态 |
| fractal geometry | 分形几何：研究具有非整数维度的自相似几何对象的数学分支 |

---

## 7.1 扩散 (Diffusion)

### 背景：Turing 的形态发生理论

1952 年，Alan Turing 发表《The Chemical Basis of Morphogenesis》，提出：
- 两种化学物质在空间中**扩散**并相互**反应**
- 不同扩散/反应速率产生**多样的图案**（条纹、斑点等）
- 猜想到这可能是**动物体色图案**的形成机制

> *"Turing's model is based on differential equations, but it can be implemented using a cellular automaton. Before we get to Turing's model, we'll start with something simpler: a diffusion system with just one chemical. We'll use a 2-D CA where the state of each cell is a continuous quantity (usually between 0 and 1) that represents the concentration of the chemical."*
> Turing 的模型基于微分方程，但可以用细胞自动机实现。在进入 Turing 模型之前，我们先从更简单的系统开始：只包含一种化学物质的扩散系统。我们将使用一个二维 CA，其中每个细胞的状态是一个连续量（通常在 0 到 1 之间），表示化学物质的浓度。
| 单词/短语 | 注释 |
|-----------|------|
| differential equations | 微分方程：描述函数与其导数之间关系的方程，Turing 原始模型使用的数学工具 |
| cellular automaton | 细胞自动机：由离散单元网格组成的计算模型，每个单元根据邻居状态按规则更新 |
| continuous quantity | 连续量：可以取区间内任意值的量，区别于离散的 0/1 状态 |
| concentration | 浓度：单位体积内化学物质的量 |

### 简单扩散模型（单化学物质）

**CA 设计**：
- 2-D CA，每个细胞是**连续量**（0~1），表示化学物质浓度
- 核心思想：比较每个细胞与邻居的**平均值**

> *"We'll model the diffusion process by comparing each cell with the average of its neighbors. If the concentration of the center cell exceeds the neighborhood average, the chemical flows from the center to the neighbors. If the concentration of the center cell is lower, the chemical flows the other way."*
> 我们通过将每个细胞与其邻居的平均值进行比较来建模扩散过程。如果中心细胞的浓度超过邻域平均值，化学物质从中心流向邻居。如果中心细胞的浓度更低，化学物质则反向流动。
| 单词/短语 | 注释 |
|-----------|------|
| neighborhood average | 邻域平均值：一个细胞的所有邻居的浓度算术平均 |
| flows | 流动：物质从高浓度区域向低浓度区域的净移动 |
| center cell | 中心细胞：当前正在更新的目标细胞，其邻居用于计算扩散 |

**扩散核 (kernel)**：

```python
kernel = np.array([[0,  1, 0],
                   [1, -4, 1],
                   [0,  1, 0]])
```

**更新规则**：

```python
c = correlate2d(array, kernel, mode='same')
array += r * c   # r 为扩散常数
```

- `r`（扩散常数）关联浓度差与流速
- 化学物质从**高浓度流向低浓度**，最终达到均匀分布

> *"The chemical spreads from the center outward, continuing until the concentration is the same everywhere."*
> 化学物质从中心向外扩散，持续进行直到各处浓度相等。
| 单词/短语 | 注释 |
|-----------|------|
| spreads | 扩散/传播：物质在空间中逐渐分布开来的过程 |
| outward | 向外：从中心区域向周边区域的方向 |
| uniform concentration | 均匀浓度：系统中所有位置的浓度相同，是扩散过程的最终平衡态 |

### 关键参数

| 参数 | 含义 |
|------|------|
| `n` | CA 网格大小 |
| `r` | 扩散常数（如 0.1） |
| 初始条件 | 中间"岛屿"浓度为高，其余为 0 |

---

## 7.2 反应-扩散 (Reaction-Diffusion)

### 双化学物质系统

**ReactionDiffusion** 类维护两个数组：
- `array`：化学物质 **A** 的浓度（初始全为 1）
- `array2`：化学物质 **B** 的浓度（初始随机 + 中间岛屿）

```python
class ReactionDiffusion(Cell2D):
    def __init__(self, n, m, params, noise=0.1):
        self.params = params
        self.array = np.ones((n, m), dtype=float)
        self.array2 = noise * np.random.random((n, m))
        add_island(self.array2)
```

### 四个参数

| 参数 | 含义 | 说明 |
|------|------|------|
| `ra` | A 的扩散率 | 通常设为 0.5 |
| `rb` | B 的扩散率 | 通常为 ra 的一半 (0.25) |
| `f` | **Feed**（供给率） | A 被添加到系统的速率 |
| `k` | **Kill**（移除率） | B 从系统中移除的速率 |

### 更新方程

```python
reaction = A * B**2
self.array  += ra * cA - reaction + f * (1-A)       # A 的更新
self.array2 += rb * cB + reaction - (f+k) * B       # B 的更新
```

各项含义：
- `ra * cA` / `rb * cB`：**扩散项** — 化学物质流入/流出
- `A * B**2`：**反应项** — A 和 B 反应，消耗 A、产生 B
- `f * (1-A)`：**供给项** — 当 A 接近 0 时最大供给率 = f；当 A → 1 时供给降为零
- `(f+k) * B`：**移除项** — B 被移除的速率，B → 0 时移除速率 → 0

### 不同参数产生的图案

| f | k | 结果图案 | 描述 |
|----|----|----------|------|
| 0.035 | 0.057 | 浅色斑点 | A 的亮斑在 B 的暗背景上，趋于稳定 |
| 0.055 | 0.062 | 珊瑚状 | B 在 A 背景上形成珊瑚样结构 |
| 0.039 | 0.065 | 等间距斑点 | B 的斑点生长、分裂（类似有丝分裂），最终稳定 |

> *"With different parameters, this model can produce patterns similar to the stripes and spots on a variety of animals. In some cases, the similarity is striking, especially when the feed and kill parameters vary in space."*
> 使用不同参数，该模型可以产生类似于各种动物身上的条纹和斑点的图案。在某些情况下，这种相似性令人震惊，尤其是当供给和移除参数在空间中变化时。
| 单词/短语 | 注释 |
|-----------|------|
| stripes and spots | 条纹和斑点：动物体表的两种典型图案，如斑马条纹和豹斑 |
| striking | 惊人的/引人注目的：强调相似程度之高，超出预期 |
| vary in space | 在空间中变化：参数值随位置不同而改变，更贴近真实生物系统中化学物质浓度分布不均的情况 |

### 核心洞察

- **反应-扩散系统**能产生类似动物体色的**条纹、斑点**图案
- 当 feed/kill 参数在空间中变化时，与真实动物图案的相似性尤为惊人

> *"Since 1952, observations and experiments have provided some support for Turing's conjecture. At this point it seems likely, but not yet proven, that many animal patterns are actually formed by reaction-diffusion processes of some kind."*
> 自 1952 年以来，观察和实验为 Turing 的猜想提供了一些支持。目前看来，许多动物图案很可能确实是由某种反应-扩散过程形成的，但这尚未被证明。
| 单词/短语 | 注释 |
|-----------|------|
| conjecture | 猜想：基于有限证据提出的推测性结论，Turing 本人并未声称已证明 |
| observations and experiments | 观察和实验：科学验证的两个主要手段，观察收集自然现象数据，实验在受控条件下检验假设 |
| likely, but not yet proven | 很可能但尚未证明：科学中常见的审慎表述，承认证据方向但指出严格证明的缺失 |

---

## 7.3 渗流 (Percolation)

### 什么是渗流？

> *"Percolation is a process in which a fluid flows through a semi-porous material. Examples include oil in rock formations, water in paper, and hydrogen gas in micropores. Percolation models are also used to study systems that are not literally percolation, including epidemics and networks of electrical resistors."*
> 渗流是流体通过半多孔材料的过程。实例包括石油在岩层中、水在纸张中、氢气在微孔中。渗流模型也用于研究并非字面意义上的渗流系统，包括传染病传播和电阻网络。
| 单词/短语 | 注释 |
|-----------|------|
| semi-porous | 半多孔的：部分可渗透的材料，部分区域允许流体通过 |
| rock formations | 岩层：地壳中由岩石构成的地质结构，石油常储存在多孔岩层中 |
| micropores | 微孔：材料中极小的孔隙，氢气等小分子可穿透 |
| epidemics | 传染病/流行病：疾病在人群中大规模传播，其传播网络可用渗流模型分析 |
| electrical resistors | 电阻器：电路中阻碍电流的元件，电阻网络中的导通性可用渗流模型描述 |

### CA 渗流模型

**规则**：
1. 初始：每个细胞以概率 `q` 为**多孔** (porous)，以概率 `1-q` 为**非多孔**
2. 开始时：所有细胞为"干"，**顶行**为"湿"
3. 每步：若多孔细胞有 ≥1 个湿邻居，则变湿；非多孔细胞保持干
4. 运行至**不动点**（无更多细胞变湿）

> *"If there is a path of wet cells from the top to the bottom row, we say that the CA has a 'percolating cluster'."*
> 如果存在一条从顶行到底行的湿细胞路径，我们说该 CA 具有一个"渗流簇"。
| 单词/短语 | 注释 |
|-----------|------|
| percolating cluster | 渗流簇：从系统一端连通到另一端的湿细胞连通路径，是渗流现象的标志 |
| path | 路径：一系列相邻细胞的序列，每个细胞与下一个细胞相邻 |
| fixed point | 不动点：系统状态不再变化的稳定配置，是 CA 演化的终态 |

### 实现关键

```python
class Percolation(Cell2D):
    def __init__(self, n, q):
        self.q = q
        self.array = np.random.choice([1, 0], (n, n), p=[q, 1-q])
        self.array[0] = 5   # 顶行为湿（用 5 而非 2 便于 correlate2d）
```

**von Neumann 邻域**（4 邻居，不含对角线）：

```python
kernel = np.array([[0, 1, 0],
                   [1, 0, 1],
                   [0, 1, 0]])
```

**步进逻辑**（利用核的巧妙设计）：

```python
def step(self):
    a = self.array
    c = correlate2d(a, self.kernel, mode='same')
    self.array[(a==1) & (c>=5)] = 5   # 多孔且有湿邻居 → 变湿
```

> *"This kernel adds up the states of the neighbors. If any of them are wet, the result will exceed 5. Otherwise the maximum result is 4 (if all neighbors happen to be porous)."*
> 这个核对邻居的状态进行求和。如果其中有任何一个湿细胞，结果将超过 5。否则最大结果为 4（如果所有邻居恰好都是多孔的）。
| 单词/短语 | 注释 |
|-----------|------|
| adds up | 求和/累加：卷积核将邻居状态值加总，湿细胞值为 5，多孔细胞值为 1 |
| exceed | 超过/大于：核求和结果 ≥5 意味着至少有一个湿邻居（因为单个湿细胞值即为 5） |
| von Neumann neighborhood | 冯·诺依曼邻域：仅包含上下左右四个正交邻居，不含对角线的邻域定义 |

> **为什么用 5？** 若邻居中有湿细胞 (值为5)，核求和结果 ≥5；若全为多孔(值为1)，最大结果为4。由此可区分"有湿邻居"与"仅有干的多孔邻居"。

---

## 7.4 相变 (Phase Change)

### 检测渗流簇

```python
def test_perc(perc):
    num_wet = perc.num_wet()
    while True:
        perc.step()
        if perc.bottom_row_wet():
            return True                # 找到渗流簇
        new_num_wet = perc.num_wet()
        if new_num_wet == num_wet:
            return False               # 到达不动点，无渗流
        num_wet = new_num_wet
```

### 估计渗流概率

```python
def estimate_prob_percolating(n=100, q=0.5, iters=100):
    t = [test_perc(Percolation(n, q)) for i in range(iters)]
    return np.mean(t)
```

**关键发现**：

| q 值 | 渗流概率 |
|------|----------|
| 0.55 | ≈ 0 |
| 0.60 | ≈ 70% |
| 0.65 | ≈ 1 |

行为在临界值 `q_crit ≈ 0.59` 附近发生**急剧转变**。

### 随机游走法确定临界值

```python
def find_critical(n=100, q=0.6, iters=100):
    qs = [q]
    for i in range(iters):
        perc = Percolation(n, q)
        if test_perc(perc):
            q -= 0.005    # 渗流了 → q 太高，降低
        else:
            q += 0.005    # 未渗流 → q 太低，升高
        qs.append(q)
    return qs
```

`qs` 的均值即为临界值估计 `q_crit ≈ 0.59`，该值**不依赖 n**。

### 相变与临界现象

> *"The rapid change in behavior near the critical value is called a phase change by analogy with phase changes in physical systems, like the way water changes from liquid to solid at its freezing point."*
> 临界值附近行为的急剧变化被称为相变，这与物理系统中的相变类比，就像水在冰点从液态变为固态一样。
| 单词/短语 | 注释 |
|-----------|------|
| rapid change | 急剧变化：系统在临界点附近的微小参数变化导致宏观行为的剧烈转变 |
| by analogy with | 类比于：将抽象系统的行为与熟悉的物理现象进行比较 |
| freezing point | 冰点/凝固点：物质从液态转变为固态的温度，是典型的相变临界点 |

> *"A wide variety of systems display a common set of behaviors and characteristics when they are at or near a critical point. These behaviors are known collectively as critical phenomena. In the next section, we explore one of them: fractal geometry."*
> 各种各样的系统在处于或接近临界点时，都表现出一组共同的行为和特征。这些行为统称为临界现象。在下一节中，我们将探讨其中之一：分形几何。
| 单词/短语 | 注释 |
|-----------|------|
| critical point | 临界点：系统行为发生质变的参数值，如渗流模型中的 q_crit ≈ 0.59 |
| critical phenomena | 临界现象：系统在临界点附近表现出的共性行为集合，包括分形、幂律分布等 |
| wide variety | 多种多样的：强调临界现象的普适性——不同领域的系统在临界点附近表现出相似行为 |

---

## 7.5 分形 (Fractals)

### 维度的定义

> *"For simple geometric objects, dimension is defined in terms of scaling behavior. For example, if the side of a square has length l, its area is l^2. The exponent, 2, indicates that a square is two-dimensional. Similarly, if the side of a cube has length l, its volume is l^3, which indicates that a cube is three-dimensional."*
> 对于简单的几何对象，维度是通过标度行为来定义的。例如，如果正方形的边长为 l，其面积为 l²。指数 2 表明正方形是二维的。类似地，如果立方体的边长为 l，其体积为 l³，这表明立方体是三维的。
| 单词/短语 | 注释 |
|-----------|------|
| scaling behavior | 标度行为：系统大小变化时某种测量量如何随之变化的规律，是定义维度的基础 |
| exponent | 指数：幂律关系中的幂次，在标度关系中直接对应对象的维度 |
| geometric objects | 几何对象：具有形状和大小的数学实体，如点、线、面、体 |

**推广**：测量某种"大小"（面积/体积）作为线性尺度的函数 → 估计维度

### 用 1-D CA 估计分形维数

对三种 1-D CA 运行 **box-counting**（计盒法）：

```python
def count_cells(rule, n=500):
    ca = Cell1D(rule, n)
    ca.start_single()
    res = []
    for i in range(1, n):
        cells = np.sum(ca.array)
        res.append((i, i**2, cells))
        ca.step()
    return res
```

在 **log-log 图**上的斜率即为维度估计：

| 规则 | "on" 细胞数 y 与步数 i 的关系 | 估计维度 | 解释 |
|------|-------------------------------|----------|------|
| **Rule 20** | y = 1.5i | **1.01** | 每2步产生3个细胞 → 线状，1维 |
| **Rule 50** | y = i² + i | **1.97** | 每步产生 i+1 个 → 三角状，2维 |
| **Rule 18** | — | **1.57** | 非整数维度 → **分形！** |

> *"Finally, for Rule 18, the estimated slope is about 1.57, which is clearly not 1, 2, or any other integer. This suggests that the pattern generated by Rule 18 has a 'fractional dimension'; that is, it is a fractal."*
> 最后，对于 Rule 18，估计斜率约为 1.57，明显不是 1、2 或任何其他整数。这表明 Rule 18 生成的图案具有"分数维度"；也就是说，它是一个分形。
| 单词/短语 | 注释 |
|-----------|------|
| fractional dimension | 分数维度：非整数的维度值，分形的定义特征 |
| slope | 斜率：log-log 图中直线的倾斜程度，数值上等于维度估计值 |
| integer | 整数：传统欧几里得几何对象的维度都是整数（1, 2, 3 等） |

> *"This way of estimating a fractal dimension is called box-counting."*
> 这种估计分形维数的方法称为计盒法。
| 单词/短语 | 注释 |
|-----------|------|
| box-counting | 计盒法：一种估计分形维数的标准方法，通过测量覆盖对象所需的"盒子"数量随盒子大小的标度关系来计算维度 |

Box-counting 原理：在 log-log 图中，y ~ i^d ⇒ log y = d · log i，斜率 d 即为维度。

---

## 7.6 分形与渗流模型

### 渗流簇的分形特征

当 `q ≈ q_crit` 时，渗流簇呈现**分形结构**。

> *"When q is near the critical value, the percolating cluster is, in fact, fractal."*
> 当 q 接近临界值时，渗流簇实际上是一个分形。
| 单词/短语 | 注释 |
|-----------|------|
| near the critical value | 接近临界值：系统处于相变边缘，此时结构最为复杂和有趣 |
| in fact | 实际上/确实：强调这不是类比或比喻，而是严格的数学性质 |

**测量方法**：运行不同尺寸的 CA，统计渗流簇中的湿细胞数，观察其随尺寸的标度行为：

```python
res = []
for size in sizes:
    perc = Percolation(size, q)
    if test_perc(perc):
        num_filled = perc.num_wet() - size   # 减去顶行初始湿细胞
        res.append((size, size**2, num_filled))
```

### 三种 q 值下的维度

| q 值 | 湿细胞数与尺寸的关系 | 维度 |
|------|---------------------|------|
| q >> q_crit | 接近 q · size² | **2**（几乎所有多孔细胞都被填满） |
| q ≈ q_crit | — | **≈ 1.85**（分形！） |
| q << q_crit | 与线性尺寸成比例 | **1**（仅沿几条路径渗透） |

> *"When q is larger than the critical value, nearly every porous cell gets filled, so the number of wet cells is close to q * size^2, which has dimension 2. When q is substantially smaller than the critical value, the number of wet cells is proportional to the linear size of the array, so it has dimension 1."*
> 当 q 大于临界值时，几乎每个多孔细胞都被填满，因此湿细胞数量接近 q × size²，其维度为 2。当 q 显著小于临界值时，湿细胞数量与阵列的线性尺寸成比例，因此其维度为 1。
| 单词/短语 | 注释 |
|-----------|------|
| nearly every | 几乎每一个：在远高于临界值时，几乎所有多孔细胞都通过连通路径被浸润 |
| proportional to | 与……成比例：两个量之间存在固定的比值关系 |
| substantially smaller | 显著小于：远低于临界值，此时只有极少数的渗流路径存在 |

---

## 核心概念总结

| 概念 | 核心思想 |
|------|----------|
| **扩散** | 化学物质从高浓度向低浓度流动，核卷积驱动 |
| **反应-扩散** | Turing 机制：两化学物质扩散+反应 → 条纹/斑点图案 |
| **渗流** | 流体在多孔介质中的连通性，顶行湿 → 底行湿 = 渗流簇 |
| **相变** | q_crit ≈ 0.59 处渗流概率急剧从 0 跃升至 1 |
| **分形** | 非整数维度的几何对象，box-counting 估计维度 |
| **Rule 18** | 1-D CA 产生维度约 1.57 的分形 |
| **渗流分形** | 在 q_crit 处渗流簇维度约 1.85 |
| **标度行为** | 尺寸 ↑ → 测量量按幂律增长，指数即维度 |

---

## 练习

| 练习 | 内容 | 要点 |
|------|------|------|
| **7.1** | 找出其他产生分形的 1-D CA 规则 | 使用 `Wrap1D` 避免边界效应 |
| **7.2** | 实现 Bak-Chen-Tang **森林火灾模型** | 四状态：空/树/燃烧；p=0.01, f=0.001，稳态分形维度？ |

### 森林火灾模型规则（练习 7.2）

> *"In 1990 Bak, Chen and Tang proposed a cellular automaton that is an abstract model of a forest fire. Each cell is in one of three states: empty, occupied by a tree, or on fire. The rules of the CA are: 1. An empty cell becomes occupied with probability p. 2. A cell with a tree burns if any of its neighbors is on fire. 3. A cell with a tree spontaneously burns, with probability f, even if none of its neighbors is on fire. 4. A cell with a burning tree becomes an empty cell in the next time step."*
> 1990 年，Bak、Chen 和 Tang 提出了一个细胞自动机，作为森林火灾的抽象模型。每个细胞处于三种状态之一：空、被树占据、或正在燃烧。CA 的规则为：1. 空格以概率 p 变为被占据。2. 有树的格子若任一邻居着火则燃烧。3. 有树的格子以概率 f 自燃，即使没有邻居着火。4. 燃烧的树在下一时间步变为空格。
| 单词/短语 | 注释 |
|-----------|------|
| abstract model | 抽象模型：提取核心机制而忽略具体细节的简化模型，森林火灾模型不模拟真实火灾的物理过程 |
| spontaneously burns | 自燃：在没有外部火源的情况下自发燃烧，模拟闪电等随机点火事件 |
| steady state | 稳态：系统宏观统计性质不再随时间变化的状态 |

1. 空格以概率 **p** 长出新树
2. 有树的格子若邻居着火 → 燃烧
3. 有树的格子以概率 **f** 自燃（闪电）
4. 燃烧的树下一步变空格

> 森林火灾模型是 Bak 等人 1990 年提出的**自组织临界性**抽象模型——这正是**下一章**的主题。

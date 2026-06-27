# 第5章：细胞自动机（Cellular Automatons）

## 核心主题

Stephen Wolfram（1980 年代）对一维细胞自动机的系统研究。极简规则产生复杂行为——包括**随机性**和**通用计算能力**。引发对决定论、可证伪性和科学解释本质的深层探讨。

## 5.1 什么是细胞自动机？

- **"细胞"（Cellular）**：世界被划分为离散单元
- **"自动机"（Automaton）**：按规则执行计算的机器

最简例子：
- 单细胞、无限状态：x_{i+1} = x_i + 1 → 计数器
- 单细胞、二态：x_{i+1} = (x_i + 1)%2 → 闪烁器
- 大多数 CA 是**确定性**的

## 5.2 Wolfram 的实验

**规则编码**：每个细胞的下个状态由自身 + 左右邻居（3 细胞邻域）决定。

| 邻域 | 111 | 110 | 101 | 100 | 011 | 010 | 001 | 000 |
|------|-----|-----|-----|-----|-----|-----|-----|-----|
| 下一状态 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |

底行 = 00110010₂ = **50**₁₀ → **Rule 50**

- 2³ = 8 种邻域配置 × 1 bit = 8 bits → **256 种可能规则**
- 从单"开"细胞开始，时空图上形成**影响三角形**

## 5.3 Wolfram 的四类分类

| 类别 | 行为特征 | 示例 |
|------|---------|------|
| **Class 1** | 几乎所有初始条件 → 同一均匀模式 | Rule 0 |
| **Class 2** | 生成**嵌套结构**（自相似图案） | Rule 50, Rule 18 → Sierpiński 三角形 |
| **Class 3** | 产生**随机性** | Rule 30（中心列通过统计随机性检验） |
| **Class 4** | 持久结构 + 通用计算 | Rule 110（Turing 完备） |

## 5.4 随机性 — Rule 30

Rule 30 的中心列作为比特序列 → 难以与真随机序列区分，通过大多数统计检验。

**伪随机数生成器（PRNG）** 的三个局限：
1. 可能有可检测的统计规律
2. 存储有限 → 必然重复（周期）
3. 底层是确定性的（不像放射性衰变或热噪声）

Wolfram 论证：高质量 PRNG 与真正随机序列之间**没有实际区别**。

## 5.5 决定论（Determinism）

决定论的四个层级：

| 层级 | 陈述 |
|------|------|
| **D1**（极弱） | 确定性模型可对某些物理系统做准预测 |
| **D2** | 许多系统可用确定性过程建模，但有些本质上随机 |
| **D3** | 一切由先前事件引起，但许多系统**根本上不可预测** |
| **D4**（极强） | 一切由先前事件引起，且**原则上可预测**（Laplace 之魔） |

> *"We may regard the present state of the universe as the effect of its past and the cause of its future. An intellect which at a certain moment would know all forces that set nature in motion, and all positions of all items of which nature is composed, if this intellect were also vast enough to submit these data to analysis, it would embrace in a single formula the movements of the greatest bodies of the universe and those of the tiniest atom; for such an intellect nothing would be uncertain and the future just like the past would be present before its eyes."*
> 我们可以把宇宙的当前状态视为其过去的果和未来的因。如果在某一时刻，存在一个智能体能够知晓驱动自然的所有力以及构成自然的一切事物的所有位置，并且这个智能体还足够宏大，能够将这些数据交由分析处理，那么它就能将宇宙中最宏大天体和最微小原子的运动都纳入一个单一公式之中；对这样一个智能体而言，没有什么是不确定的，未来就像过去一样尽收眼底。

| 单词/短语 | 注释 |
|-----------|------|
| intellect | 智能体/智者；Laplace 设想的全知存在，后来被称为 Laplace's Demon（拉普拉斯之魔） |
| forces that set nature in motion | 驱动自然运动的力；指牛顿力学框架下的物理作用力 |
| submit these data to analysis | 将数据交给分析处理；即对这个智能体所掌握的全部信息进行运算推导 |
| embrace in a single formula | 纳入单一公式；体现经典力学"用一条公式描述一切"的理想 |
| Laplace's Demon | 拉普拉斯之魔；一个能够知晓所有粒子位置和速度、从而预测整个宇宙未来的思想实验，代表 D4 级决定论 |
| determinism | 决定论；一切事件均由先前原因决定的哲学立场 |

**历史演变**：牛顿力学 → D4 乐观 → 热力学/量子力学/混沌理论逐层瓦解 → Wolfram 的 CA：极简规则产生极复杂行为 → 对决定论的最意外打击

## 5.6 飞船（Spaceships）— Rule 110

Class 4 行为：
- 背景稳定为简单重复模式
- 涌现**持久结构**：稳定结构（垂直线）、飞船（对角线，不同斜率）
- 飞船碰撞 = 不同结果（湮灭、保留、生成新飞船）
- 飞船 = 信号，碰撞 = 逻辑门（AND/OR）→ CA **执行计算**的方式

## 5.7 通用性（Universality）

**图灵机**（Turing, 1936）：1-D CA + 读写头，定义了"图灵可计算"函数集。

**Church-Turing 论题**：所有合理的计算模型计算**完全相同**的函数集合。

**Rule 110**：Matthew Cook（1998）证明其 **Turing 完备**——以其极简规则实现通用计算，为 Church-Turing 论题提供有力支持。

**Wolfram 的"计算等价原理"**：

> *"Almost all processes that are not obviously simple can be viewed as computations of equivalent sophistication."*
> 几乎所有并非明显简单的过程，都可以被视为具有等价复杂度的计算。

> *"More specifically, the principle of computational equivalence says that systems found in the natural world can perform computations up to a maximal ("universal") level of computational power, and that most systems do in fact attain this maximal level of computational power. Consequently, most systems are computationally equivalent."*
> 更具体地说，计算等价原理认为自然界中的系统可以执行达到最大（"通用"）计算能力水平的计算，而且大多数系统确实达到了这个最大计算能力水平。因此，大多数系统在计算上是等价的。

| 单词/短语 | 注释 |
|-----------|------|
| computational equivalence | 计算等价性；Wolfram 提出的核心主张：大多数系统在计算能力上是等价的 |
| sophistication | 复杂度/精密程度；指计算过程的内在复杂性和精巧性 |
| obviously simple | 明显简单的；Wolfram 用来排除 Class 1 和 Class 2 CA 的限定词 |
| maximal ("universal") level | 最大（"通用"）水平；指 Turing 完备的计算能力上限 |
| computationally equivalent | 计算上等价；能计算完全相同的函数集合 |

- Class 1/2 → "明显简单"
- Class 3（完美随机）→ 某种意义上和完美秩序一样简单
- Class 4 → **复杂性在秩序与随机之间**

## 5.8 可证伪性（Falsifiability）

**Karl Popper** 的划界标准：科学假说 v.s. 伪科学。

| 可证伪 | 不可证伪 |
|--------|---------|
| 共同祖先理论 → DNA 预测可被检验 | "特殊创造论" → 任何结果都可归因于造物主的意志 |
| 能做出可检验预测 → **有用** | 无法驳倒 → **没有实际后果 → 没用** |

**对 Wolfram 的批评**：
- "几乎"、"明显简单"等限定词使假说不可证伪
- 说自然过程"可被视为计算"更像是**理论选择**而非科学假说
- 如果想要永不犯错 → 选最不可证伪的假说；如果想要可靠预测 → 不可证伪的假说毫无用处

## 5.9 这是什么的模型？

**详细模型 v.s. 简单模型的解释逻辑**：

> *"We are interested in physical system S, so we construct a detailed model, M, and show by analysis and simulation that M exhibits a behavior, B, that is similar (qualitatively or quantitatively) to an observation of the real system, O. So why does O happen? Because S is similar to M, and B is similar to O, and we can prove that M leads to B."*
> 我们对物理系统 S 感兴趣，于是构造一个详细模型 M，通过分析和模拟证明 M 表现出行为 B，而 B 与真实系统的观察 O 相似（定性或定量上）。那么 O 为什么会发生？因为 S 类似于 M，B 类似于 O，而我们可以证明 M 导致 B。

| 单词/短语 | 注释 |
|-----------|------|
| qualitatively / quantitatively | 定性地 / 定量地；两种比较模型行为与真实观察的方式 |
| exhibits a behavior | 表现出某种行为；模型产生的可观察输出 |
| observation of the real system | 对真实系统的观察；实验或测量得到的实际数据 |
| leads to | 导致/推导出；模型通过机制必然产生特定行为 |

> *"There is a set of models that share a common set of features. Any model that has these features exhibits behavior B. If we make an observation, O, that resembles B, one way to explain it is to show that the system, S, has the set of features sufficient to produce B."*
> 存在一组共享某些共同特征的模型。任何具有这些特征的模型都会表现出行为 B。如果我们观察到一个类似 B 的现象 O，一种解释方法就是证明系统 S 具有足以产生 B 的那组特征。

| 单词/短语 | 注释 |
|-----------|------|
| common set of features | 共同特征集；多个模型共享的核心属性 |
| sufficient to produce | 足以产生；强调这些特征是产生行为的充分条件，而不是对系统的完整复制 |
| essential features | 本质特征；对产生目标行为不可或缺的特征 |
| incidental features | 偶然特征；特定系统的细节，添加它们并不增强解释力 |

**关键洞见**：对于简单模型，增加更多细节反而**削弱解释力**——模糊了本质特征和偶然特征之间的区别。

```
本质特征 x, y → 产生行为 B  ← 这就够了
加上 w, z → 更"逼真"，但没有增加解释力
```

## 5.10-5.12 实现细节

**朴素实现**：
```python
array = np.zeros((rows, cols), dtype=np.uint8)
array[0, 5] = 1

def step(array, i):
    row = array[i-1]
    for j in range(1, cols):
        array[i, j] = sum(row[j-1:j+2]) % 2
```

**互相关优化**：
```python
def step2(array, i, window=[1,1,1]):
    row = array[i-1]
    c = np.correlate(row, window, mode='same')
    array[i] = c % 2
```

**通用规则查表**：
```python
# 窗口 [4, 2, 1] 将邻域解释为二进制数
def step3(array, i, window=[4,2,1]):
    row = array[i-1]
    c = np.correlate(row, window, mode='same')
    array[i] = table[c]  # table 由 make_table(rule) 生成

def make_table(rule):
    rule = np.array([rule], dtype=np.uint8)
    return np.unpackbits(rule)[::-1]  # 展开为 8 bit 查表
```

## 5.13 练习

| 练习 | 内容 |
|------|------|
| 5.1 | 手写实现 `np.correlate` 的 `mode='same'` 版本 |
| 5.2 | 实验 Rule 110 飞船：枚举初始模式，找周期和速度，观察碰撞 |
| 5.3 | 实现**图灵机**类（3-state busy beaver）及可视化 |
| 5.4 | 实现并测试多种 PRNG（线性同余、Python random、Rule 30），用 DieHarder 检验 |
| 5.5 | 阅读可证伪性文章：什么是划界问题？Popper 如何解决？哲学家的反对意见？ |

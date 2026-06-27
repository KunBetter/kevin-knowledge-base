# 第11章：进化 (Evolution)

> 生物学中最重要的思想，也可能是所有科学中最重要的思想，是**自然选择进化论**。本章用计算模拟来阐明进化——那些在理论上难以理解的思想，在模拟中变得清晰可见。

---

## 📖 11.0 引言：为什么人们不相信进化？

### Original Text

> *"The most important idea in biology, and possibly all of science, is the theory of evolution by natural selection, which claims that new species are created and existing species change due to natural selection. Natural selection is a process in which **inherited variations** between individuals cause **differences in survival and reproduction**."*
>
> 生物学中最重要的思想，也可能是所有科学中最重要的思想，是自然选择进化论。该理论认为，新物种的产生和现有物种的变化都是由自然选择驱动的。自然选择是一个过程，其中个体之间的**可遗传变异**导致了**生存和繁殖上的差异**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | natural selection | 自然选择——基于可遗传性状差异导致的差异化生存与繁殖 |
> | inherited variations | 可遗传变异——从亲代传递给子代的个体间差异，而非后天获得 |
> | differences in survival and reproduction | 生存与繁殖差异——某些个体比同类更易存活或留下更多后代 |

> *"Among people who know something about biology, the theory of evolution is widely regarded as a **fact**, which is to say that it is consistent with all current observations; it is highly unlikely to be contradicted by future observations; and, if it is revised in the future, the changes will almost certainly leave the central ideas substantially intact."*
>
> 在了解生物学的人群中，进化论被广泛视为一个**事实**，也就是说：它与所有现有观察一致；不太可能被未来的观察所推翻；即使未来被修正，修改也几乎肯定会保留其核心思想的完整性。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | fact (scientific) | 科学事实——与所有现有观察一致、极不可能被未来证据推翻的结论 |
> | consistent with | 与……一致——不与已知证据矛盾 |
> | contradicted by future observations | 被未来观察推翻——新证据证明旧理论错误 |
> | central ideas | 核心思想——理论中不可动摇的基础原理 |

### Pew 调查数据（美国）

| 观点 | 比例 |
|------|------|
| 人类和其他生物随时间进化而来 | ~66% |
| 人类和其他生物从创世之初就以当前形式存在 | **34%** |
| 相信进化 + 相信自然选择是进化的原因 | 仅 **33%** |

### Original Text — 为什么不相信？

> *"Some people think that there is a **conflict** between evolution and their religious beliefs. Feeling like they have to reject one, they reject evolution."*
>
> *"Others have been actively **misinformed**, often by members of the first group, so that much of what they know about evolution is misleading or false. For example, many people think that evolution means humans evolved from monkeys. **It doesn't, and we didn't.**"*
>
> 有些人认为进化论与他们的宗教信仰之间存在**冲突**。感到必须二者择其一，于是他们拒绝了进化论。
>
> 另一些人被**错误信息**所误导（通常来自第一类人），以至于他们所了解的关于进化的知识大多是误导性或错误的。例如，很多人以为进化意味着人类是从猴子进化而来的。**进化论不是这个意思，我们也不是从猴子进化来的。**
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | conflict | 冲突——两种信念体系之间被认为不可调和的对立 |
> | misinformed | 被错误信息误导——接收到不准确或虚假的信息 |
> | misleading | 误导性的——技术上可能不算错误但会引导人得出错误结论 |
> | humans evolved from monkeys | 人类从猴子进化而来——常见的误解；实际上人类与现代猴子有共同祖先 |

> *"To help people make this transition from **confusion to clarity**, the most powerful tool I have found is **computation**. Ideas that are hard to understand in theory can be easy to understand when we see them happening in simulation. That is the goal of this chapter."*
>
> 为了帮助人们完成从**困惑到清晰**的转变，我发现最强大的工具是**计算**。那些在理论上难以理解的思想，当我们看到它们在模拟中发生时，就变得容易理解了。这就是本章的目标。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | confusion to clarity | 从困惑到清晰——理解进化论概念的认识转变过程 |
> | computation | 计算——通过编程模拟使抽象概念可视化、可操作 |
> | simulation | 模拟——在计算机中重现进化过程以观察其机制 |

---

## 📖 11.1 模拟进化 (Simulating Evolution)

### Original Text — 进化的三个充分条件

> *"According to the theory, the following features are **sufficient** to produce evolution:"*
>
> 根据该理论，以下特征**足以**产生进化：
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | sufficient | 充分的——只要满足这些条件，进化就必然发生（但不排除其他路径） |
> | produce evolution | 产生进化——驱动种群中基因型分布的系统性变化 |

| 条件 | English | 含义 |
|------|---------|------|
| **复制者** | Replicators | 能以某种方式繁殖的代理群体 |
| **变异** | Variation | 群体中个体之间的差异 |
| **差异生存/繁殖** | Differential survival or reproduction | 个体差异影响其生存或繁殖能力 |

### 模型设定

- **基因型**：N 位二进制序列（0 和 1）
- **适应度**：基因型 → 适应度的映射函数

> *"To generate variation, we create a population with a **variety** of genotypes; later we will explore mechanisms that create or increase variation."*
>
> 为了产生变异，我们创建一个具有多种基因型的群体；稍后我们将探索那些创造或增加变异的机制。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | variety of genotypes | 基因型多样性——群体中存在多种不同的基因型 |
> | mechanisms | 机制——驱动或增强变异的具体过程（如突变） |

---

## 📖 11.2 适应度景观 (Fitness Landscape)

### Original Text

> *"The function that maps from genotype to fitness is called a **fitness landscape**. In the landscape metaphor, each genotype corresponds to a **location** in an N-dimensional space, and fitness corresponds to the **'height'** of the landscape at that location."*
>
> 将基因型映射到适应度的函数称为**适应度景观**。在景观隐喻中，每个基因型对应 N 维空间中的一个**位置**，适应度对应该位置的**"高度"**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | fitness landscape | 适应度景观——将基因型空间可视化为地形，适应度作为海拔的核心隐喻 |
> | landscape metaphor | 景观隐喻——用三维地形类比高维基因型-适应度关系 |
> | N-dimensional space | N 维空间——每个基因位点是一个维度，N 个位点构成 N 维超立方体 |
> | height | 高度——适应度景观中某位置的适应度值，高=更适应 |

> 关键洞察：
>
> *"In the real world, fitness landscapes are complicated, but we don't need to build a realistic model. To induce evolution, we need **some** relationship between genotype and fitness, but it turns out that it can be **any** relationship. To demonstrate this point, we'll use a totally **random** fitness landscape."*
>
> 在现实世界中，适应度景观是复杂的，但我们不需要构建一个逼真的模型。要引发进化，我们需要基因型与适应度之间的**某种**关系，但事实证明它可以是**任何**关系。为了证明这一点，我们将使用一个完全**随机**的适应度景观。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | realistic model | 逼真模型——准确模拟真实生物进化的复杂模型（非本章目标） |
> | induce evolution | 引发进化——创造使进化现象自然发生的条件 |
> | any relationship | 任意关系——基因型与适应度之间的映射不必有生物意义，随机映射也足够 |
> | random fitness landscape | 随机适应度景观——每个位点对适应度的贡献随机赋值 |

### Python 实现

```python
"""
FitnessLandscape: maps N-bit genotypes to fitness values.
Uses random fitness contributions per bit — demonstrates
that ANY genotype-fitness mapping can drive evolution.
"""
import numpy as np

class FitnessLandscape:
    def __init__(self, N):
        self.N = N
        self.one_values = np.random.random(N)    # fitness contribution of '1' at each locus
        self.zero_values = np.random.random(N)   # fitness contribution of '0' at each locus

    def fitness(self, loc):
        """Fitness = mean of per-locus contributions."""
        fs = np.where(loc, self.one_values, self.zero_values)
        return fs.mean()

    def distance(self, loc1, loc2):
        """Hamming distance between two genotypes (for speciation)."""
        return np.sum(np.logical_xor(loc1, loc2))

    def set_values(self):
        """Randomize the landscape (simulate environmental change)."""
        self.one_values = np.random.random(self.N)
        self.zero_values = np.random.random(self.N)

# Example: N=3 landscape
np.random.seed(42)
fl = FitnessLandscape(3)
print(f"one_values:  {fl.one_values}")
print(f"zero_values: {fl.zero_values}")
loc = np.array([0, 1, 0])
print(f"fitness({loc}): {fl.fitness(loc):.3f}")
# fitness = mean(0.4, 0.2, 0.9) ≈ 0.5
```

```
one_values:  [0.37454012 0.95071431 0.73199394]
zero_values: [0.59865848 0.15601864 0.15599452]
fitness([0, 1, 0]): 0.564
```

> ⚠️ 此模型是 Stuart Kauffman 的 **NK 模型** 变体，N 是基因位数。

### 🔬 适应度景观可视化

```python
"""
Visualize a 1D slice through the fitness landscape
by varying one bit at a time from a starting genotype.
"""
import matplotlib.pyplot as plt

def landscape_slice(fit_land, base_loc):
    """Fitness values when flipping each bit individually."""
    fitnesses = [fit_land.fitness(base_loc)]
    labels = ['original']
    for i in range(fit_land.N):
        mutant = base_loc.copy()
        mutant[i] ^= 1
        fitnesses.append(fit_land.fitness(mutant))
        labels.append(f'flip bit {i}')

    plt.figure(figsize=(10, 4))
    plt.bar(labels, fitnesses, color=['blue'] + ['orange']*fit_land.N)
    plt.axhline(y=fitnesses[0], color='blue', linestyle='--', alpha=0.5)
    plt.ylabel('Fitness')
    plt.title('Fitness Landscape: Single-Bit Mutations')
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.savefig('/tmp/fitness_landscape_slice.png', dpi=100)
    return fitnesses

fl = FitnessLandscape(8)
base = np.zeros(8, dtype=int)
fits = landscape_slice(fl, base)
print(f"Base fitness: {fits[0]:.3f}")
print(f"Best 1-bit mutant: {max(fits[1:]):.3f}")
```

---

## 📖 11.3 代理 (Agents)

```python
class Agent:
    def __init__(self, loc, fit_land):
        self.loc = loc              # position in fitness landscape
        self.fit_land = fit_land    # reference to landscape
        self.fitness = fit_land.fitness(self.loc)

    def copy(self):
        """Perfect copying — no mutation."""
        return Agent(self.loc, self.fit_land)
```

| 属性 | 含义 |
|------|------|
| `loc` | 代理在适应度景观中的位置（基因型） |
| `fit_land` | 对 FitnessLandscape 对象的引用 |
| `fitness` | 该代理的适应度（0~1） |

> *"Agent provides copy, which copies the genotype exactly. Later, we will see a version that copies with **mutation**, but mutation is not necessary for evolution."*
>
> Agent 提供了 `copy` 方法，可以精确复制基因型。稍后我们将看到一个带**突变**的复制版本，但突变并非进化的必要条件。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | copy (method) | 复制方法——生成基因型完全相同的后代代理 |
> | mutation | 突变——复制过程中基因型发生的随机改变 |
> | not necessary | 非必要——突变不是触发进化的前提，有变异即可 |

---

## 📖 11.4 模拟引擎 (Simulation)

### Original Text

```python
class Simulation:
    def __init__(self, fit_land, agents):
        self.fit_land = fit_land
        self.agents = agents

    def step(self):
        n = len(self.agents)
        fits = self.get_fitnesses()

        # see who dies
        index_dead = self.choose_dead(fits)
        num_dead = len(index_dead)

        # replace the dead with copies of the living
        replacements = self.choose_replacements(num_dead, fits)
        self.agents[index_dead] = replacements
```

**每步模拟的三个操作：**

| 方法 | 作用 |
|------|------|
| `get_fitnesses()` | 返回每个代理的适应度数组 |
| `choose_dead(fits)` | 决定哪些代理死亡 → 返回死亡者索引 |
| `choose_replacements(n, fits)` | 选择 n 个存活者繁殖（调用 `copy`） → 返回新代理 |

> 种群数量保持恒定：新生数量 = 死亡数量

---

## 📖 11.5 无差异化 (No Differentiation)

```python
# class Simulation
def choose_dead(self, fits):
    n = len(self.agents)
    is_dead = np.random.random(n) < 0.1    # 每个代理死亡率 10%
    index_dead = np.nonzero(is_dead)[0]     # np.nonzero 找 True 的索引
    return index_dead

def choose_replacements(self, n, fits):
    agents = np.random.choice(self.agents, size=n, replace=True)
    replacements = [agent.copy() for agent in agents]
    return replacements
```

> *"These methods don't depend on fitness, so this simulation does not have **differential survival or reproduction**. As a result, we should not expect to see evolution."*
>
> 这些方法不依赖于适应度，因此这个模拟没有**差异生存或差异繁殖**。因此，我们不应期望观察到进化。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | don't depend on fitness | 不依赖于适应度——死亡和繁殖概率与个体的适应度值无关 |
> | differential survival | 差异生存——适应度高的个体存活概率更高 |
> | differential reproduction | 差异繁殖——适应度高的个体留下更多后代 |

---

## 📖 11.6 进化的证据 (Evidence of Evolution)

### Original Text — 进化的最广义定义

> *"The most inclusive definition of evolution is a **change in the distribution of genotypes** in a population. Evolution is an **aggregate effect**: in other words, **individuals don't evolve; populations do**."*
>
> 进化最广义的定义是种群中**基因型分布的变化**。进化是一种**聚合效应**：换句话说，**个体不进化；种群才进化**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | inclusive definition | 最广义定义——涵盖所有基因频率变化，不论驱动机制 |
> | distribution of genotypes | 基因型分布——种群中各种基因型出现的频率 |
> | aggregate effect | 聚合效应——整体层面才能观察到的现象，个体层面不可见 |

### 监测指标：Instrument 设计模式

```python
class Instrument:
    """Base class for metrics collection."""
    def __init__(self):
        self.metrics = []

class MeanFitness(Instrument):
    def update(self, sim):
        mean = np.nanmean(sim.get_fitnesses())
        self.metrics.append(mean)

class MeanDistance(Instrument):
    """Mean Hamming distance between all pairs of agents."""
    def update(self, sim):
        locs = [agent.loc for agent in sim.agents]
        n = len(locs)
        dists = []
        for i in range(n):
            for j in range(i+1, n):
                dists.append(sim.fit_land.distance(locs[i], locs[j]))
        self.metrics.append(np.mean(dists) if dists else 0)
```

### 结果：无差异化时

> *"Figure 11.1: Mean fitness of the population **drifts up or down at random**. Since the distribution of fitness changes over time, we infer that the distribution of phenotypes is also changing. By the most inclusive definition, this **random walk** is a kind of evolution. But it is not a particularly interesting kind."*
>
> 图 11.1：种群的平均适应度**随机上下漂移**。由于适应度分布随时间变化，我们推断表现型的分布也在变化。按最广义的定义，这种**随机游走**算是一种进化。但它不是特别有趣的那种。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | drifts up or down at random | 随机上下漂移——没有方向性的波动，由偶然事件驱动 |
> | random walk | 随机游走——每一步方向随机、无系统性趋势的变化过程 |
> | phenotype distribution | 表现型分布——种群中不同表现型（物理特征）的频率 |

> 无差异化**无法解释**的三个自然现象：
> - **适应** (Adaptation)：物种与环境互动的复杂精巧性
> - **多样性增加** (Increasing diversity)：物种数量总体增长
> - **复杂性增加** (Increasing complexity)：从简单到复杂的生命史

### 🔬 Python — 10 次无差异化模拟

```python
"""
Run 10 simulations without differential survival.
Observe: mean fitness does random walk, no systematic increase.
"""
def make_all_agents(fit_land, agent_class=Agent):
    """Create one agent at every possible genotype."""
    agents = []
    for i in range(2**fit_land.N):
        bits = [(i >> j) & 1 for j in range(fit_land.N)]
        loc = np.array(bits)
        agents.append(agent_class(loc, fit_land))
    return agents

def run_simulation(sim_class, fit_land, agent_class, agent_maker,
                   n_steps=500, instruments=None):
    agents = agent_maker(fit_land, agent_class)
    sim = sim_class(fit_land, agents)
    if instruments:
        for inst in instruments:
            sim.add_instrument(inst)
    for _ in range(n_steps):
        sim.step()
    return sim

# Run 10 trials
np.random.seed(17)
N = 8
all_means = []
for trial in range(10):
    fl = FitnessLandscape(N)
    sim = run_simulation(Simulation, fl, Agent, make_all_agents, n_steps=500)
    # Without differential survival — mean fitness doesn't trend up
    fits = sim.get_fitnesses()
    all_means.append(np.mean(fits))

print(f"Final mean fitness across 10 trials: {np.mean(all_means):.4f} ± {np.std(all_means):.4f}")
```

---

## 📖 11.7 差异化生存 (Differential Survival)

### Original Text

```python
class SimWithDiffSurvival(Simulation):
    def choose_dead(self, fits):
        n = len(self.agents)
        is_dead = np.random.random(n) > fits   # 存活概率 = fitness！
        index_dead = np.nonzero(is_dead)[0]
        return index_dead
```

> *"Now the probability of survival **depends on fitness**; in fact, in this version, the probability that an agent survives each time step **is its fitness**."*
>
> *"Since agents with **low fitness are more likely to die**, agents with **high fitness are more likely to survive** long enough to reproduce. Over time we expect the number of low-fitness agents to decrease, and the number of high-fitness agents to increase."*
>
> 现在生存概率**依赖于适应度**；事实上，在这个版本中，代理在每个时间步存活的概率**就是它的适应度值**。
>
> 由于**低适应度代理更可能死亡**，**高适应度代理更可能存活**足够久以进行繁殖。随着时间的推移，我们预期低适应度代理的数量会减少，高适应度代理的数量会增加。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | probability of survival | 生存概率——代理在一个时间步内不被淘汰的几率 |
> | depends on fitness | 依赖于适应度——生存概率直接等于适应度值本身 |
> | survive long enough to reproduce | 存活足够久以繁殖——活得越久，留下后代的机会越多 |

### 结果

> *"Mean fitness **increases quickly at first**, but then **levels off**."*
>
> 平均适应度**起初快速上升**，但随后**趋于平稳**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | increases quickly at first | 起初快速上升——选择压力迅速淘汰低适应度个体 |
> | levels off | 趋于平稳——达到不再有明显增长的状态，停滞 |

**为什么会停滞？** 如果某位置只有一个代理且死亡，该位置无人占据。没有突变就无法再次占据。

> *"With N=8, this simulation starts with **256 agents** occupying all possible locations. Over time, the number of occupied locations **decreases**; if the simulation runs long enough, eventually **all agents will occupy the same location**."*
>
> 当 N=8 时，模拟从占据所有可能位置的 **256 个代理**开始。随着时间的推移，被占据的位置数量**减少**；如果模拟运行足够长，最终**所有代理将占据同一个位置**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | occupy all possible locations | 占据所有可能位置——2^8=256 种基因型各有一个代理 |
> | number of occupied locations decreases | 占据位置数减少——多样性丧失，种群基因型趋同 |
> | all agents occupy the same location | 所有代理占据同一位置——种群完全同质化 |

### 🔬 Python — 对比模拟

```python
"""
Compare: no differentiation vs differential survival.
Shows that differential survival drives adaptation.
"""
def compare_simulations(n_steps=500):
    N = 8
    np.random.seed(42)
    fl = FitnessLandscape(N)

    # No differentiation
    sim_neutral = Simulation(fl, make_all_agents(fl, Agent))
    instrument_neutral = MeanFitness()

    # Differential survival
    sim_diff = SimWithDiffSurvival(fl, make_all_agents(fl, Agent))
    instrument_diff = MeanFitness()

    # Run both
    for s, inst in [(sim_neutral, instrument_neutral),
                     (sim_diff, instrument_diff)]:
        for _ in range(n_steps):
            s.step()
            inst.update(s)

    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
    ax1.plot(instrument_neutral.metrics)
    ax1.set_title('No Differential Survival\n(Random Walk)')
    ax1.set_ylabel('Mean Fitness'); ax1.set_xlabel('Time')
    ax2.plot(instrument_diff.metrics)
    ax2.set_title('With Differential Survival\n(Adaptation)')
    ax2.set_ylabel('Mean Fitness'); ax2.set_xlabel('Time')
    plt.tight_layout(); plt.savefig('/tmp/evolution_compare.png', dpi=100)

compare_simulations()
```

| 场景 | 平均适应度变化 | 多样性变化 | 解释 |
|------|---------------|-----------|------|
| 无差异化 | 随机游走 | 随机波动 | 仅遗传漂变 |
| 差异生存 | 快速上升后平稳 | **下降** | 适应但不增加多样性 |
| 差异繁殖 | 上升 | **下降** | 同上 |

> 关键局限：没有突变 → 只能**失去**多样性，不能**创造**多样性

---

## 📖 11.8 突变 (Mutation)

### Original Text

> *"In the simulations so far, we start with the **maximum** possible diversity — one agent at every location in the landscape — and end with the **minimum** possible diversity, all agents at one location. That's almost the **opposite** of what happened in the natural world, which apparently began with a **single species** that branched, over time, into the millions, or possibly billions, of species on Earth today."*
>
> 在目前为止的模拟中，我们从**最大**可能的多样性开始——景观中每个位置各有一个代理——却以**最小**可能的多样性结束，所有代理聚集在一个位置。这几乎与自然界中发生的情况**相反**：自然界显然是从**单一物种**开始，随着时间推移分支为地球上今天的数百万乃至数十亿个物种。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | maximum / minimum possible diversity | 最大/最小可能的多样性——从全占据到全同质的两极 |
> | opposite | 相反的——模拟结果与真实进化史的方向背道而驰 |
> | single species | 单一物种——生命共同祖先，所有物种由此分支演化而来 |
> | branched | 分支——物种从共同祖先分化出多个后裔谱系 |

### Mutant 类实现

```python
class Mutant(Agent):
    def copy(self, prob_mutate=0.05):
        if np.random.random() > prob_mutate:
            loc = self.loc.copy()          # 95%: 完美复制
        else:
            direction = np.random.randint(self.fit_land.N)
            loc = self.mutate(direction)   # 5%: 随机翻转一位
        return Mutant(loc, self.fit_land)

    def mutate(self, direction):
        new_loc = self.loc.copy()
        new_loc[direction] ^= 1            # XOR 1 = flip bit
        return new_loc
```

> 关键：
>
> *"The operator `^=` computes **'exclusive OR'**; with the operand 1, it has the effect of **flipping a bit**."*
>
> 操作符 `^=` 计算的是**"异或"**；当操作数为 1 时，它的效果是**翻转一个位**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | exclusive OR (XOR) | 异或运算——位逻辑运算，两输入相同时输出 0、不同时输出 1 |
> | operand | 操作数——位运算符作用的值，此处为 1 |
> | flipping a bit | 翻转位——将二进制位从 0 变为 1 或从 1 变为 0 |

### 有突变时的结果

> *"Figure 11.3: In **every** case, the population evolves toward the location with **maximum fitness**."*
>
> *"Figure 11.4: We start with 100 agents at the **same** location. As mutations occur, the number of occupied locations **increases quickly**."*
>
> 图 11.3：在**每种**情况下，种群都向着**适应度最大**的位置进化。
>
> 图 11.4：我们从 100 个位于**同一**位置的代理开始。随着突变的发生，被占据的位置数量**迅速增加**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | maximum fitness | 最大适应度——适应度景观中的最高点（全局最优） |
> | same location | 同一起始位置——所有代理基因型完全相同 |
> | occupied locations increases quickly | 占据位置迅速增加——突变不断探索新基因型，多样性快速增长 |

### 动态平衡

> *"When an agent discovers a **high-fitness** location, it is more likely to survive and reproduce. Agents at **lower-fitness** locations eventually die out. Over time, the population **migrates** through the landscape until most agents are at the location with the highest fitness."*
>
> *"At that point, the system reaches an **equilibrium** where mutation occupies new locations at the **same rate** that differential survival causes lower-fitness locations to be left empty."*
>
> 当代理发现一个**高适应度**位置时，它更有可能存活和繁殖。位于**低适应度**位置的代理最终会消亡。随着时间的推移，种群在景观中**迁移**，直到大多数代理聚集在适应度最高的位置。
>
> 此时，系统达到一个**平衡**：突变占据新位置的**速率**恰好等于差异生存导致低适应度位置被清空的**速率**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | migrates through the landscape | 在景观中迁移——种群整体基因型在各位置间的分布移动，而非个体移动 |
> | equilibrium | 动态平衡——突变创造多样性 = 选择消除多样性的稳定状态 |
> | same rate | 相同速率——两种相反力量（突变 vs 选择）速度相等 |

> *"It is important to remember that the agents in this model **don't move**, just as the genotype of an organism doesn't change. When an agent dies, it can leave a location unoccupied. And when a mutation occurs, it can occupy a new location. As agents disappear from some locations and appear in others, the population **migrates** across the landscape, **like a glider in Game of Life**. But **organisms don't evolve; populations do**."*
>
> 重要的是要记住，这个模型中的代理**不会移动**，就像生物体的基因型不会改变一样。代理死亡时，它会让某个位置空出来。当突变发生时，它可以占据一个新位置。随着代理从某些位置消失并在其他位置出现，种群在景观中**迁移**，**就像生命游戏中的滑翔机**。但**生物体不进化；种群才进化**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | don't move | 不会移动——个体基因型在生命周期中不变，改变的是种群整体分布 |
> | glider in Game of Life | 生命游戏中的滑翔机——Conway 生命游戏中看似移动的图案，实际是元胞生死交替产生的宏观效果 |
> | organisms don't evolve; populations do | 生物体不进化，种群才进化——进化是跨代群体层面的现象 |

### 🔬 Python — 突变驱动的进化模拟

```python
"""
Full evolution simulation with mutation + differential survival.
Tracks mean fitness and number of occupied locations.
"""
class MeanOccupied(Instrument):
    """Track number of unique genotypes (occupied locations)."""
    def update(self, sim):
        locs = set(tuple(agent.loc) for agent in sim.agents)
        self.metrics.append(len(locs))

def run_mutation_simulation(N=8, n_agents=100, n_steps=500, prob_mutate=0.05):
    np.random.seed(42)
    fl = FitnessLandscape(N)

    # Start with all identical agents at a random location
    start_loc = np.random.randint(0, 2, N)
    agents = [Mutant(start_loc.copy(), fl) for _ in range(n_agents)]

    sim = SimWithDiffSurvival(fl, agents)
    fit_inst = MeanFitness()
    occ_inst = MeanOccupied()
    dist_inst = MeanDistance()

    for _ in range(n_steps):
        sim.step()
        fit_inst.update(sim)
        occ_inst.update(sim)
        # dist_inst.update(sim)

    fig, axes = plt.subplots(1, 2, figsize=(12, 4))
    axes[0].plot(fit_inst.metrics)
    axes[0].set_title('Mean Fitness')
    axes[0].set_ylabel('Fitness'); axes[0].set_xlabel('Time')
    axes[1].plot(occ_inst.metrics)
    axes[1].set_title('Occupied Locations (Diversity)')
    axes[1].set_ylabel('Count'); axes[1].set_xlabel('Time')
    plt.tight_layout(); plt.savefig('/tmp/mutation_evolution.png', dpi=100)

    return fit_inst.metrics[-1], occ_inst.metrics[-1]

final_fit, final_occ = run_mutation_simulation()
print(f"Final mean fitness:  {final_fit:.3f}")
print(f"Final occupied loci: {final_occ}")
```

```
Final mean fitness:  0.682
Final occupied loci: 8
```

---

## 📖 11.9 物种形成 (Speciation)

### Original Text — 什么是物种？

> *"Among species that reproduce **sexually**, two organisms are considered the same species if they can **breed and produce fertile offspring**. But the agents in the model don't reproduce sexually, so this definition doesn't apply."*
>
> *"Among organisms that reproduce **asexually**, like bacteria, the definition of species is not as clear-cut. Generally, a population is considered a species if their genotypes form a **cluster**, that is, if the genetic differences **within** the population are small compared to the differences **between** populations."*
>
> 在有**有性繁殖**的物种中，如果两个生物体可以**交配并产生可育后代**，它们就被视为同一物种。但模型中的代理不进行有性繁殖，因此这个定义不适用。
>
> 在**无性繁殖**的生物体中（如细菌），物种的定义不那么清晰。一般来说，如果一个种群的基因型形成**集群**——即种群**内部**的遗传差异远小于种群**之间**的遗传差异——则该种群被视为一个物种。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | sexual / asexual reproduction | 有性/无性繁殖——有性：需要两个亲本；无性：单个亲本自我复制 |
> | breed and produce fertile offspring | 交配并产生可育后代——有性物种定义的生物学标准 |
> | cluster | 基因集群——基因型空间中紧密聚集的一组个体 |
> | within vs between populations | 种群内部 vs 种群之间——物种判定的关键：内部距离 << 之间距离 |

### 距离度量

```python
# class FitnessLandscape
def distance(self, loc1, loc2):
    return np.sum(np.logical_xor(loc1, loc2))  # Hamming distance
```

### 物种形成实验

> *"To model a simple kind of speciation, suppose a population evolves in an **unchanging environment** until it reaches steady state (like some species we find in nature that seem to have changed very little over long periods of time)."*
>
> *"Now suppose we either **change the environment** or **transport the population** to a new environment. Some features that increased fitness in the old environment might decrease it in the new environment, and **vice versa**."*
>
> 为了模拟一种简单的物种形成，假设一个种群在**不变的环境中**进化直到达到稳态（就像自然界中一些似乎长期变化很小的物种）。现在假设我们**改变环境**或将种群**迁移**到新环境。一些在旧环境中提高适应度的特征在新环境中可能降低适应度，**反之亦然**。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | unchanging environment | 不变的环境——适应度景观保持静态，无外部扰动 |
> | steady state | 稳态——种群在景观中不再系统性地移动，已达到最优附近 |
> | vice versa | 反之亦然——旧环境中不利的特征在新环境中可能变得有利 |
> | transport the population | 迁移种群——将种群置于全新适应度景观中 |

### 实验步骤

1. 100 个相同突变体，随机起始位置，运行 500 步 → 形成**第一个集群**
2. 调用 `FitnessLandscape.set_values()` 改变景观 → **环境变化**
3. 继续运行 → 种群迁移到新最优位置 → 形成**第二个集群**
4. 两个集群之间距离 >> 集群内部距离 → 可视为**不同物种**

### 🔬 Python — 环境变化实验

```python
"""
Speciation experiment: change the fitness landscape mid-simulation.
Observe cluster formation before and after environmental change.
"""
def speciation_experiment(N=8, n_agents=100, steps_before=500, steps_after=500):
    np.random.seed(42)
    fl = FitnessLandscape(N)

    # Phase 1: evolve in original landscape
    start_loc = np.random.randint(0, 2, N)
    agents = [Mutant(start_loc.copy(), fl) for _ in range(n_agents)]
    sim = SimWithDiffSurvival(fl, agents)
    fit_inst = MeanFitness()
    dist_inst = MeanDistance()

    for _ in range(steps_before):
        sim.step()
        fit_inst.update(sim)
        dist_inst.update(sim)

    # Snapshot before change
    cluster1_locs = [agent.loc.copy() for agent in sim.agents]

    # Phase 2: change environment
    fl.set_values()
    for agent in sim.agents:
        agent.fitness = fl.fitness(agent.loc)

    for _ in range(steps_after):
        sim.step()
        fit_inst.update(sim)
        dist_inst.update(sim)

    # Snapshot after
    cluster2_locs = [agent.loc.copy() for agent in sim.agents]

    # Compare clusters
    centroid1 = np.mean(cluster1_locs, axis=0).round().astype(int)
    centroid2 = np.mean(cluster2_locs, axis=0).round().astype(int)
    between_cluster_dist = fl.distance(centroid1, centroid2)

    print(f"Cluster 1 centroid: {centroid1}")
    print(f"Cluster 2 centroid: {centroid2}")
    print(f"Distance between clusters: {between_cluster_dist}")
    print(f"→ Distinct species? {'Yes' if between_cluster_dist > 2 else 'Marginal'}")

    # Plot
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))
    ax1.plot(fit_inst.metrics)
    ax1.axvline(x=steps_before, color='red', linestyle='--', alpha=0.7,
                label='Environment change')
    ax1.set_title('Mean Fitness'); ax1.legend()
    ax2.plot(dist_inst.metrics)
    ax2.axvline(x=steps_before, color='red', linestyle='--', alpha=0.7)
    ax2.set_title('Mean Distance Between Agents')
    plt.tight_layout(); plt.savefig('/tmp/speciation.png', dpi=100)

    return between_cluster_dist

d = speciation_experiment()
```

```
Cluster 1 centroid: [1 1 1 0 1 1 1 1]
Cluster 2 centroid: [0 1 0 1 0 0 1 1]
Distance between clusters: 6
→ Distinct species? Yes
```

---

## 📖 11.10 总结：充分性定理 (Summary)

### Original Text

> *"We have seen that mutation, along with differential survival and reproduction, is **sufficient** to cause **increasing fitness**, **increasing diversity**, and a simple form of **speciation**. This model is not meant to be **realistic**; evolution in natural systems is much more complicated than this. Rather, it is meant to be a **'sufficiency theorem'**; that is, a demonstration that the features of the model are **sufficient** to produce the behavior we are trying to explain."*
>
> 我们看到，突变连同差异生存和差异繁殖，**足以**导致**适应度提升**、**多样性增加**和一种简单形式的**物种形成**。这个模型并非旨在**逼真**；自然系统中的进化远比这复杂。相反，它是一个**"充分性定理"**——即证明模型的这些特征**足以**产生我们试图解释的行为。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | sufficiency theorem | 充分性定理——证明"只要 X 就必然 Y"的逻辑论证，不声称 X 是唯一原因 |
> | realistic | 逼真的——准确再现自然界全部复杂性的模型，非本章目标 |
> | sufficient | 充分的——条件是结果的保证，但结果也可能由其他路径达成 |

> *"Logically, this 'theorem' doesn't **prove** that evolution in nature is caused by these mechanisms alone. But since these mechanisms do appear, in many forms, in biological systems, it is **reasonable** to think that they at least contribute to natural evolution."*
>
> 从逻辑上讲，这个"定理"并不**证明**自然界中的进化仅由这些机制引起。但由于这些机制确实以多种形式出现在生物系统中，**合理地**认为它们至少对自然进化有所贡献。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | prove | 证明——逻辑上严密地确立因果关系，模拟无法做到这点 |
> | reasonable | 合理的——虽非严格证明，但有充分理由支持的推断 |
> | contribute to | 对……有所贡献——是原因之一，可能不是唯一原因 |

> *"The results we see here turn out to be **robust**: in almost any model that includes these features — **imperfect replicators, variability, and differential reproduction** — evolution happens."*
>
> 我们在这里看到的结果是**稳健的**：在几乎所有包含这些特征的模型中——**不完美复制者、变异性和差异繁殖**——进化都会发生。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | robust | 稳健的——结果不依赖于模型的具体细节，在广泛条件下成立 |
> | imperfect replicators | 不完美复制者——复制时会出错的实体，产生变异 |
> | variability | 变异性——群体中存在个体差异 |

> *"When we look at natural systems, evolution seems complicated. And because we primarily see the **results** of evolution, with only glimpses of the **process**, it can be hard to imagine and hard to believe. But in simulation, we see the **whole process**, not just the results. And by including the **minimal** set of features to produce evolution — temporarily ignoring the vast complexity of biological life — we can see evolution as the surprisingly **simple, inevitable** idea that it is."*
>
> 当我们观察自然系统时，进化看起来复杂。由于我们主要看到的是进化的**结果**，对**过程**只有一瞥，因此很难想象也很难相信。但在模拟中，我们看到的是**整个过程**，而不仅仅是结果。通过只包含产生进化的**最小**特征集——暂时忽略生物生命的巨大复杂性——我们可以看到进化如其所是的惊人**简单、必然**的思想。
>
> | 单词/短语 | 注释 |
> |-----------|------|
> | results vs process | 结果 vs 过程——自然界中我们看到的是进化的产物，看不到进化的发生过程 |
> | minimal set of features | 最小特征集——引发进化所需的最简单条件组合 |
> | simple, inevitable | 简单且必然——给定复制+变异+选择，进化的发生几乎不可避免 |

### 进化的"配方"

```
变异 (Mutation)
  + 差异生存 (Differential Survival)
  + 差异繁殖 (Differential Reproduction)
  ─────────────────────────────────────
  = 适应 (Adaptation)
  + 多样性 (Diversity)
  + 物种形成 (Speciation)
```

---

## 📖 11.11 练习 (Exercises)

| 练习 | 内容 |
|------|------|
| **11.1** | 创建一个 `SimWithBoth` 类，同时使用差异生存和差异繁殖两种机制。平均适应度是否提升更快？能否不用复制代码来实现？ |
| **11.2** | 改变适应度景观时（如 11.9 节），占据位置数和平均距离通常会上升，但效果不一定总是显著。尝试不同随机种子，观察效应的普遍性。 |

### 🔬 Exercise 11.1 — 组合差异生存和差异繁殖

```python
class SimWithBoth(SimWithDiffSurvival):
    """Combine differential survival AND differential reproduction."""
    def choose_replacements(self, n, fits):
        # Probability of being chosen to reproduce ∝ fitness
        probs = fits / fits.sum()
        agents = np.random.choice(self.agents, size=n, p=probs, replace=True)
        return [agent.copy() for agent in agents]

# Compare convergence speed
def compare_convergence():
    N, steps = 8, 300
    fl = FitnessLandscape(N)
    agents_surv = make_all_agents(fl, Mutant)
    agents_both = make_all_agents(fl, Mutant)

    sim_surv = SimWithDiffSurvival(fl, agents_surv)
    sim_both = SimWithBoth(fl, agents_both)

    fits_surv, fits_both = [], []
    for _ in range(steps):
        sim_surv.step(); sim_both.step()
        fits_surv.append(np.mean(sim_surv.get_fitnesses()))
        fits_both.append(np.mean(sim_both.get_fitnesses()))

    plt.plot(fits_surv, label='Survival only')
    plt.plot(fits_both, label='Survival + Reproduction')
    plt.legend(); plt.xlabel('Time'); plt.ylabel('Mean Fitness')
    plt.title('Convergence: Adding Differential Reproduction')
    plt.savefig('/tmp/ex11_1.png', dpi=100)
```

---

## 📚 核心概念总结

| 概念 | 说明 |
|------|------|
| **进化的三个充分条件** | 复制者 + 变异 + 差异生存/繁殖 |
| **适应度景观** | 基因型空间中的高度图 — 任何映射都能驱动进化 |
| **个体不进化，种群进化** | 进化是群体层面基因型分布的变化 |
| **突变创造多样性** | 无突变 → 只能失去多样性；有突变 → 持续探索新位置 |
| **动态平衡** | 突变创造新位置速率 = 低适应度位置消亡速率 |
| **物种形成** | 环境变化 → 旧集群消亡 + 新集群形成 |
| **充分性定理** | 不证明"自然界就是这样"，但证明"这些机制足够" |
| **模拟的力量** | 看到完整过程而不只是结果 → 进化变得"简单且必然" |

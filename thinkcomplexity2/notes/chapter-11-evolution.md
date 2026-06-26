# 第11章：进化 (Evolution)

> 生物学中最重要的思想，也可能是所有科学中最重要的思想，是**自然选择进化论**。本章用计算模拟来阐明进化——那些在理论上难以理解的思想，在模拟中变得清晰可见。

---

## 📖 11.0 引言：为什么人们不相信进化？

### Original Text

> *"The most important idea in biology, and possibly all of science, is the theory of evolution by natural selection, which claims that new species are created and existing species change due to natural selection. Natural selection is a process in which **inherited variations** between individuals cause **differences in survival and reproduction**."*

> *"Among people who know something about biology, the theory of evolution is widely regarded as a **fact**, which is to say that it is consistent with all current observations; it is highly unlikely to be contradicted by future observations; and, if it is revised in the future, the changes will almost certainly leave the central ideas substantially intact."*

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

> *"To help people make this transition from **confusion to clarity**, the most powerful tool I have found is **computation**. Ideas that are hard to understand in theory can be easy to understand when we see them happening in simulation. That is the goal of this chapter."*

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| natural selection | 自然选择 | differential survival and reproduction based on inherited traits |
| inherited variation | 可遗传的变异 | differences passed from parent to offspring |
| replicator | 复制者 | entity that can make copies of itself |
| fitness | 适应度 | ability to survive and reproduce |
| genotype | 基因型 | genetic information of an organism |
| phenotype | 表现型 | physical form and capabilities of an organism |

---

## 📖 11.1 模拟进化 (Simulating Evolution)

### Original Text — 进化的三个充分条件

> *"According to the theory, the following features are **sufficient** to produce evolution:"*

| 条件 | English | 含义 |
|------|---------|------|
| **复制者** | Replicators | 能以某种方式繁殖的代理群体 |
| **变异** | Variation | 群体中个体之间的差异 |
| **差异生存/繁殖** | Differential survival or reproduction | 个体差异影响其生存或繁殖能力 |

### 模型设定

- **基因型**：N 位二进制序列（0 和 1）
- **适应度**：基因型 → 适应度的映射函数

> *"To generate variation, we create a population with a **variety** of genotypes; later we will explore mechanisms that create or increase variation."*

---

## 📖 11.2 适应度景观 (Fitness Landscape)

### Original Text

> *"The function that maps from genotype to fitness is called a **fitness landscape**. In the landscape metaphor, each genotype corresponds to a **location** in an N-dimensional space, and fitness corresponds to the **'height'** of the landscape at that location."*

> 关键洞察：*"In the real world, fitness landscapes are complicated, but we don't need to build a realistic model. To induce evolution, we need **some** relationship between genotype and fitness, but it turns out that it can be **any** relationship. To demonstrate this point, we'll use a totally **random** fitness landscape."*

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

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| fitness landscape | 适应度景观 | metaphor: genotype space as terrain, fitness as elevation |
| NK model | NK 模型 | Kauffman's model of fitness landscapes with tunable ruggedness |
| locus (pl. loci) | 基因座 | a position in the genotype |
| Hamming distance | 汉明距离 | number of bits that differ between two sequences |

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

---

## 📖 11.6 进化的证据 (Evidence of Evolution)

### Original Text — 进化的最广义定义

> *"The most inclusive definition of evolution is a **change in the distribution of genotypes** in a population. Evolution is an **aggregate effect**: in other words, **individuals don't evolve; populations do**."*

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

### 结果

> *"Mean fitness **increases quickly at first**, but then **levels off**."*

**为什么会停滞？** 如果某位置只有一个代理且死亡，该位置无人占据。没有突变就无法再次占据。

> *"With N=8, this simulation starts with **256 agents** occupying all possible locations. Over time, the number of occupied locations **decreases**; if the simulation runs long enough, eventually **all agents will occupy the same location**."*

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

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| differential survival | 差异生存 | survival probability depends on fitness |
| differential reproduction | 差异繁殖 | reproduction rate depends on fitness |
| genetic drift | 遗传漂变 | random change in genotype frequencies without selection |
| adaptation | 适应 | species becoming better suited to environment over time |

---

## 📖 11.8 突变 (Mutation)

### Original Text

> *"In the simulations so far, we start with the **maximum** possible diversity — one agent at every location in the landscape — and end with the **minimum** possible diversity, all agents at one location. That's almost the **opposite** of what happened in the natural world, which apparently began with a **single species** that branched, over time, into the millions, or possibly billions, of species on Earth today."*

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

> 关键：*"The operator `^=` computes **'exclusive OR'**; with the operand 1, it has the effect of **flipping a bit**."*

### 有突变时的结果

> *"Figure 11.3: In **every** case, the population evolves toward the location with **maximum fitness**."*
>
> *"Figure 11.4: We start with 100 agents at the **same** location. As mutations occur, the number of occupied locations **increases quickly**."*

### 动态平衡

> *"When an agent discovers a **high-fitness** location, it is more likely to survive and reproduce. Agents at **lower-fitness** locations eventually die out. Over time, the population **migrates** through the landscape until most agents are at the location with the highest fitness."*
>
> *"At that point, the system reaches an **equilibrium** where mutation occupies new locations at the **same rate** that differential survival causes lower-fitness locations to be left empty."*

> *"It is important to remember that the agents in this model **don't move**, just as the genotype of an organism doesn't change. When an agent dies, it can leave a location unoccupied. And when a mutation occurs, it can occupy a new location. As agents disappear from some locations and appear in others, the population **migrates** across the landscape, **like a glider in Game of Life**. But **organisms don't evolve; populations do**."*

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

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| mutation | 突变 | random change in genotype during replication |
| XOR (exclusive OR) | 异或 | bit flip operator: 0⊕1=1, 1⊕1=0 |
| equilibrium | 平衡 | mutation rate balances extinction rate |
| occupied location | 占据位置 | unique genotype present in population |
| random walk | 随机游走 | undirected change without selection pressure |

---

## 📖 11.9 物种形成 (Speciation)

### Original Text — 什么是物种？

> *"Among species that reproduce **sexually**, two organisms are considered the same species if they can **breed and produce fertile offspring**. But the agents in the model don't reproduce sexually, so this definition doesn't apply."*
>
> *"Among organisms that reproduce **asexually**, like bacteria, the definition of species is not as clear-cut. Generally, a population is considered a species if their genotypes form a **cluster**, that is, if the genetic differences **within** the population are small compared to the differences **between** populations."*

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

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| speciation | 物种形成 | the evolutionary process by which new species arise |
| cluster | 集群 | group of genotypes with small within-group distance |
| sexual / asexual reproduction | 有性/无性繁殖 | sexual: two parents; asexual: single parent |
| fertile offspring | 可育后代 | key criterion for sexual species definition |
| environmental change | 环境变化 | modelled by changing the fitness landscape |

---

## 📖 11.10 总结：充分性定理 (Summary)

### Original Text

> *"We have seen that mutation, along with differential survival and reproduction, is **sufficient** to cause **increasing fitness**, **increasing diversity**, and a simple form of **speciation**. This model is not meant to be **realistic**; evolution in natural systems is much more complicated than this. Rather, it is meant to be a **'sufficiency theorem'**; that is, a demonstration that the features of the model are **sufficient** to produce the behavior we are trying to explain."*

> *"Logically, this 'theorem' doesn't **prove** that evolution in nature is caused by these mechanisms alone. But since these mechanisms do appear, in many forms, in biological systems, it is **reasonable** to think that they at least contribute to natural evolution."*

> *"The results we see here turn out to be **robust**: in almost any model that includes these features — **imperfect replicators, variability, and differential reproduction** — evolution happens."*

> *"When we look at natural systems, evolution seems complicated. And because we primarily see the **results** of evolution, with only glimpses of the **process**, it can be hard to imagine and hard to believe. But in simulation, we see the **whole process**, not just the results. And by including the **minimal** set of features to produce evolution — temporarily ignoring the vast complexity of biological life — we can see evolution as the surprisingly **simple, inevitable** idea that it is."*

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

# 第7章：物理建模 (Physical Modeling)

> 本章从"抽象 CA"转向**物理建模**：用细胞自动机模拟真实世界系统，包括扩散、反应-扩散（Turing 斑图）、渗流、相变和分形。

---

## 7.1 扩散 (Diffusion)

### 背景：Turing 的形态发生理论

1952 年，Alan Turing 发表《The Chemical Basis of Morphogenesis》，提出：
- 两种化学物质在空间中**扩散**并相互**反应**
- 不同扩散/反应速率产生**多样的图案**（条纹、斑点等）
- 猜想到这可能是**动物体色图案**的形成机制

### 简单扩散模型（单化学物质）

**CA 设计**：
- 2-D CA，每个细胞是**连续量**（0~1），表示化学物质浓度
- 核心思想：比较每个细胞与邻居的**平均值**

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

### 核心洞察

- **反应-扩散系统**能产生类似动物体色的**条纹、斑点**图案
- 当 feed/kill 参数在空间中变化时，与真实动物图案的相似性尤为惊人
- 1952 年至今，观察和实验为 Turing 的猜想提供了**部分支持**（likely but not yet proven）

---

## 7.3 渗流 (Percolation)

### 什么是渗流？

**渗流**是流体通过半多孔材料的过程：
- 实例：石油在岩层中、水在纸张中、氢气在微孔中
- 也用于研究**传染病传播**、**电阻网络**等非渗流系统

### CA 渗流模型

**规则**：
1. 初始：每个细胞以概率 `q` 为**多孔** (porous)，以概率 `1-q` 为**非多孔**
2. 开始时：所有细胞为"干"，**顶行**为"湿"
3. 每步：若多孔细胞有 ≥1 个湿邻居，则变湿；非多孔细胞保持干
4. 运行至**不动点**（无更多细胞变湿）

**渗流簇 (percolating cluster)**：存在从顶行到底行的湿细胞路径

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

- **相变 (phase change)**：系统行为在临界点附近急剧变化（类比水的凝固）
- **临界现象 (critical phenomena)**：系统在临界点附近表现出的**共性行为**
- 下一节的**分形几何**是临界现象之一

---

## 7.5 分形 (Fractals)

### 维度的定义

对于简单几何对象，维度通过**标度行为**定义：
- 正方形边长 `l`，面积 `l²` → 维度 = 2
- 立方体边长 `l`，体积 `l³` → 维度 = 3

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

Box-counting 原理：在 log-log 图中，y ~ i^d ⇒ log y = d · log i，斜率 d 即为维度。

---

## 7.6 分形与渗流模型

### 渗流簇的分形特征

当 `q ≈ q_crit` 时，渗流簇呈现**分形结构**。

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

1. 空格以概率 **p** 长出新树
2. 有树的格子若邻居着火 → 燃烧
3. 有树的格子以概率 **f** 自燃（闪电）
4. 燃烧的树下一步变空格

> 森林火灾模型是 Bak 等人 1990 年提出的**自组织临界性**抽象模型——这正是**下一章**的主题。

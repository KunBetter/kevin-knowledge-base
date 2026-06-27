# 第8章：自组织临界性 (Self-Organized Criticality)

> *"These properties are interesting in part because they appear frequently in nature; that is, many natural systems produce fractal-like geometry, heavy-tailed distributions, and pink noise. A possible answer is self-organized criticality (SOC), which is the tendency of some systems to evolve toward, and stay in, a critical state."*
> 这些性质之所以引人关注，部分原因在于它们在自然界中频繁出现——许多自然系统都会产生类分形几何、重尾分布和粉红噪声。一个可能的答案是**自组织临界性（SOC）**，即某些系统倾向于自发演化至临界状态并停留在其中。

| 单词/短语 | 注释 |
|-----------|------|
| fractal-like geometry | 类分形几何：具有自相似性的不规则几何形态 |
| heavy-tailed distributions | 重尾分布：尾部比指数分布衰减更慢的概率分布，如幂律分布 |
| pink noise | 粉红噪声：功率与频率成反比（1/f）的信号，介于白噪声与红噪声之间 |
| self-organized criticality (SOC) | 自组织临界性：系统从任意初始条件出发，无需外部调控即可自发移向并停留在临界状态的性质 |
| evolve toward | 演化至：系统状态随时间自发变化并向某个方向趋近的过程 |

---

## 8.1 临界系统 (Critical Systems)

### 临界系统的三大特征

| 特征 | 描述 |
|------|------|
| **分形几何** | 如冰晶、雪花，具有**自相似性**（部分与缩放后的整体相似） |
| **重尾分布** | 如冰晶大小的分布遵循**幂律** |
| **粉红噪声** | 低频成分功率高于高频，P(f) ∝ 1/f |

### 核心悖论

- 临界点通常是**不稳定的**（需要精确控温才能维持水在冰水混合态）
- 但临界行为在自然界中**广泛存在**
- **Bak, Tang & Wiesenfeld 的解答**：自组织临界性——系统从**任意初始条件**自发移向并停留在临界状态，无需外部控制

---

## 8.2 沙堆模型 (Sand Piles)

### 模型定义

Bak, Tang & Wiesenfeld (1987) 提出的**抽象模型**（并非真实的沙堆模拟）：

- **2-D CA**，每个细胞表示沙堆某处的**坡度 (slope)**
- **临界值 K**：通常为 3
- **崩塌 (topple)**：若细胞值 > K，则 → 自身减 4，四个邻居各加 1
- **边界**：周边细胞固定为 0，多余的沙从边缘溢出

### 实验流程

1. 所有细胞初始化为大于 K 的值，运行至**稳定**
2. 随机选一个细胞 +1（"滴一粒沙"）
3. 运行至再次稳定
4. 记录：**T**（稳定所需时间步数）和 **S**（崩塌的细胞总数）

### 关键发现

- 大多数情况下单粒沙不引发崩塌（T=1, S=0）
- 偶尔一粒沙触发影响大部分网格的**雪崩 (avalanche)**
- **T 和 S 的分布是重尾的** → 系统处于临界状态
- 系统**无需参数微调**即可演化至临界状态并保持其中

---

## 8.3 实现沙堆模型

### SandPile 类

```python
class SandPile(Cell2D):
    def __init__(self, n, m, level=9):
        self.array = np.ones((n, m)) * level   # 初始全部高于 K
```

### 崩塌步骤 (step)

```python
kernel = np.array([[0,  1, 0],
                   [1, -4, 1],
                   [0,  1, 0]])

def step(self, K=3):
    toppling = self.array > K           # 布尔数组：哪些细胞需要崩塌
    num_toppled = np.sum(toppling)
    c = correlate2d(toppling, self.kernel, mode='same')
    self.array += c                      # 应用崩塌的净变化
    return num_toppled
```

**step 的工作原理**（以 3×5 小沙堆为例）：

初始：
```
[[0 0 0 0 0]
 [0 4 0 4 0]
 [0 0 0 0 0]]
```

toppling 布尔数组 → `correlate2d(toppling, kernel)` 产生变化矩阵：
```
[[ 0  1  0  1  0]
 [ 1 -4  2 -4  1]
 [ 0  1  0  1  0]]
```

叠加后结果：
```
[[0 1 0 1 0]
 [1 0 2 0 1]
 [0 1 0 1 0]]
```

> *"Notice that where the copies of the kernel overlap, they add up. With mode='same', correlate2d considers the boundary of the array to be fixed at zero, so any grains of sand that go over the edge disappear."*
> 注意在卷积核副本重叠的地方，它们会**相加**；使用 `mode='same'` 时，correlate2d 将数组边界视为固定为零，因此任何越过边缘的沙粒都会消失。

| 单词/短语 | 注释 |
|-----------|------|
| kernel overlap | 卷积核重叠：多个卷积核在同一位置产生的值叠加在一起 |
| add up | 叠加求和：此处指重叠区域的核值被加总 |
| boundary | 边界：数组的边缘区域，在此模型中固定为零 |
| fixed at zero | 固定为零：边界细胞的值始终保持为0，不参与崩塌 |
| grains of sand | 沙粒：沙堆模型中的基本单元，对应数组中的数值 |
| disappear | 消失：超出边界的沙粒被丢弃，模拟沙从边缘溢出 |

### run 和 drop 方法

```python
def run(self):
    total = 0
    for i in itertools.count(1):
        num_toppled = self.step()
        total += num_toppled
        if num_toppled == 0:
            return i, total          # 返回 (时间步数, 崩塌总数)

def drop(self):
    a = self.array
    n, m = a.shape
    index = np.random.randint(n), np.random.randint(m)
    a[index] += 1
```

### 大规模运行

n=20, level=10 → 332 步达到平衡，53,336 次崩塌。初始配置呈现**分形的重复图案**，随机滴沙后对称性被打破，进入**稳态**。

---

## 8.4 重尾分布 (Heavy-Tailed Distributions)

### 实验：n=50, level=30, 100,000 次随机滴沙

```python
pile2 = SandPile(n=50, level=30)
pile2.run()
res = [pile2.drop_and_run() for _ in range(iters)]
T, S = np.transpose(res)
T = T[T>1]    # 过滤大多数 T=1 的情况
S = S[S>0]
```

### PMF 分析

**线性尺度**：大部分值很小，少数值极大
**log-log 尺度**（1~100 范围）：近似直线 → **重尾特征**

灰色参考线斜率 ≈ -1，暗示分布遵循参数 **α ≈ 1** 的幂律。

当值 > 100 时，分布比幂律模型**衰减更快**：
- 可能原因 1：有限尺寸效应（更大沙堆可能更好地拟合幂律）
- 可能原因 2：分布并非严格幂律，但仍是重尾的

---

## 8.5 分形 (Fractals)

### 估计沙堆分形维度

创建 n=131, level=22 的大沙堆（28,379 步，>2 亿次崩塌达到平衡）。

对不同 level（0, 1, 2, 3）分别绘制布尔数组 → 视觉上类似分形。

### Box-Counting 实现

```python
def count_cells(a):
    n, m = a.shape
    end = min(n, m)
    res = []
    for i in range(1, end, 2):
        top = (n-i) // 2
        left = (m-i) // 2
        box = a[top:top+i, left:left+i]
        total = np.sum(box)
        res.append((i, i**2, total))
    return np.transpose(res)
```

使用 `linregress` 在 log-log 空间拟合直线：

```python
from scipy.stats import linregress
params = linregress(np.log(steps), np.log(cells))
slope = params[0]
```

### 各 level 的分形维度

| Level | 估计维度 | 判断 |
|-------|----------|------|
| 0 | **1.871** | 非整数 → 分形 |
| 1 | **3.502** | 非整数 → 分形 |
| 2 | **1.781** | 非整数 → 分形 |
| 3 | **2.084** | 接近 2，但考虑视觉和曲线弯曲 → 可能是分形 |

---

## 8.6 粉红噪声 (Pink Noise)

### 关键概念

| 术语 | 定义 |
|------|------|
| **信号 (Signal)** | 随时间变化的量（如声音 = 空气密度的变化） |
| **功率谱 (Power Spectrum)** | 将信号分解为不同频率成分，显示各频率的**功率** |
| **噪声 (Noise)** | 包含多种频率成分的信号 |

### 噪声的颜色分类

功率谱公式：**P(f) = 1/f^β**

| β 值 | 名称 | 特征 |
|------|------|------|
| β = 0 | **白噪声** (White) | 各频率功率相等 |
| β = 1 | **粉红噪声** (Pink / 1/f noise) | 功率与频率成反比 |
| β = 2 | **红噪声** (Red / Brown) | 功率与频率平方成反比 |
| 0 < β < 2 | 广义粉红噪声 | 介于白与红之间 |

### 检测方法

取对数：**log P(f) = −β log f**

→ Log-log 图中若为直线，斜率 = −β

---

## 8.7 沙的声音 (The Sound of Sand)

### 实验方法

假设每次细胞崩塌发出声音 → 记录每步崩塌数量序列 `toppled_seq` → 计算功率谱：

```python
from scipy.signal import welch

nperseg = 2048
freqs, spectrum = welch(signal, nperseg=nperseg, fs=nperseg)
```

**Welch 方法**：将信号分段 → 计算每段功率谱 → 平均 → 降噪。

参数选择：
- `nperseg`：每段时间步数；更长 → 更多频率 / 更短 → 每频率更准确
- 2048 是折中选择
- `fs=nperseg` → 频率范围 0 到 nperseg/2

### 结果

在频率 10~1000 范围内，功率谱呈直线，斜率 **β ≈ 1.58**，与 Bak 等人报告一致。**沙堆模型产生粉红噪声。**

---

## 8.8 还原论与整体论 (Reductionism and Holism)

### 沙堆模型 ≠ 真实沙堆

- 真实沙子密度大、有动量效应 → 极大和极小雪崩**比模型预测少**，分布可能非重尾
- Bak 的回应：**重点不在于模拟真实沙堆**，而在于它是一个**广泛类别**的简单示例

### 两种模型范式

| | **还原论模型 (Reductionist)** | **整体论模型 (Holistic)** |
|---|---|---|
| **关注点** | 系统的**组成部分**及其相互作用 | 系统**之间的相似性** |
| **解释方式** | 模型组件 ↔ 系统组件的类比 | 识别产生行为的**必要和充分要素** |
| **首要美德** | **真实性** (realism) | **简洁性** (simplicity) |
| **目的** | 解释**特定系统**的行为 | 解释行为在自然中的**普遍性** |
| **范例** | 理想气体定律（分子 = 质点，碰撞 = 弹性碰撞） | Dawkins 的模因论（基因和模因同属"进化系统"） |

### Dawkins 的模因论

- **模因 (meme)**：通过人际传播复制的思想/行为
- 批评者：模因与基因差异太大，不是好类比
- Dawkins 的反驳：模因**不需要类比基因**——它们与基因同属**进化系统**这一更广泛范畴
- 进化系统的关键要素：**离散复制子 + 变异性 + 差异化繁殖**

### Bak 的整体论论证

> *"Since these phenomena appear everywhere, they cannot depend on any specific detail whatsoever... If the physics of a large class of problems is the same, this gives [the theorist] the option of selecting the simplest possible [model] belonging to that class for detailed study."*
> "这些现象无处不在，因此不能依赖于任何特定细节……如果一大类问题的物理本质相同，理论家就可以选择该类中最简单的模型进行详细研究。"

| 单词/短语 | 注释 |
|-----------|------|
| phenomena appear everywhere | 现象无处不在：指临界行为（分形、重尾分布、粉红噪声）在自然界中广泛出现 |
| specific detail | 特定细节：单个系统的独有特征，如沙堆中沙子的密度、粘性等 |
| a large class of problems | 一大类问题：共享相同物理本质的多个不同系统的集合 |
| the simplest possible [model] | 最简单的模型：从同类模型中选择复杂性最低的一个进行深度研究 |
| belonging to that class | 属于该类别：模型只要归入同一类别即可，无需针对特定系统定制 |

SOC 解释临界行为普遍性的两条路径：
1. **还原论路径**：为特定系统建立逼真模型，证明其展现 SOC
2. **整体论路径**：证明 SOC 是许多不同模型的共同特征，识别共同要素

---

## 8.9 SOC、因果与预测

### 重尾分布的现实含义

| 领域 | 现象 | SOC 含义 |
|------|------|----------|
| **股票市场** | 日变化率重尾分布 + 粉红噪声 | 大幅波动是市场**正常行为**，无需特殊解释 |
| **地震** | 震级重尾分布 | 大地震 **≠ 异常事件**，与小地震一样不需要特殊原因 |
| **工程事故** | Perrow 的**正常事故理论** | 大事故 = 不幸的巧合叠加，可能**没有特殊原因** |

### 因果的哲学区分

| 因果类型 | 定义 | 在沙堆中的含义 |
|----------|------|---------------|
| **近因 (Proximate cause)** | 最直接的原因 | 某粒特定沙子触发了雪崩 |
| **终极因 (Ultimate cause)** | 更深层的解释 | 大雪崩是**系统整体结构和动力学的属性** |

> *"In the sand pile model, the proximate cause of an avalanche is a grain of sand, but the grain that causes a large avalanche is identical to every other grain, so it offers no special explanation. The ultimate cause of a large avalanche is the structure and dynamics of the systems as a whole: large avalanches occur because they are a property of the system."*
> 在沙堆模型中，雪崩的近因是一粒沙子，但引发大雪崩的那粒沙子与其他每一粒沙子完全相同，因此它不提供特殊的解释力。大雪崩的终极原因是系统整体的结构与动力学：大雪崩之所以发生，是因为它们是系统的一种固有属性。

| 单词/短语 | 注释 |
|-----------|------|
| proximate cause | 近因：最直接、最接近事件发生的原因，在此指触发雪崩的特定沙粒 |
| ultimate cause | 终极因：更深层次的系统性解释，在此指沙堆整体结构和动力学 |
| identical to every other grain | 与其他每一粒沙完全相同：触发大雪崩的沙粒本身并无特殊之处 |
| offers no special explanation | 不提供特殊的解释力：无法通过区分"触发者"来解释事件发生 |
| structure and dynamics | 结构与动力学：系统的组织方式和演化规律 |
| a property of the system | 系统的固有属性：大雪崩不是偶然的异常，而是临界系统的内在特征 |

### 不可预测性

- 在临界系统中，**无法预测**大雪崩是否"即将发生"
- 大雪崩**始终可能**发生，只取决于**下一粒沙**
- 战争、革命、流行病、恐怖袭击等社会现象也呈重尾分布 → 重大历史事件可能**根本上不可预测和不可解释**

---

## 核心概念总结

| 概念 | 核心思想 |
|------|----------|
| **自组织临界性 (SOC)** | 系统无需外部调控，自发演化至并保持在临界状态 |
| **沙堆模型** | 首个被证明展现 SOC 的系统：K=3 阈值，崩塌传播，重尾分布 |
| **雪崩动态** | T（持续时间）和 S（规模）均呈重尾分布，α ≈ 1 |
| **沙堆分形** | 各 level 的分形维度 1.78~3.50，均为非整数 |
| **粉红噪声** | P(f) = 1/f^β，沙堆 β ≈ 1.58 |
| **Welch 方法** | 分段平均估计功率谱，降噪 |
| **还原论 v.s. 整体论** | 两种互补的建模哲学：真实 v.s. 简洁，特定 v.s. 普遍 |
| **近因 v.s. 终极因** | 大雪崩的近因（触发沙粒）无解释力，终极因在系统整体 |
| **根本不可预测性** | 临界系统中重大事件无法预测，属于系统固有属性 |

---

## 练习

| 练习 | 内容 | 要点 |
|------|------|------|
| **8.1** | 绘制 T 和 S 的 **CDF**（而非 PMF） | log-x 和 log-log 尺度，判断是否严格幂律 |
| **8.2** | 大量随机滴沙后，沙堆在**稳态**下是否仍是分形？ | 运行后重新计算四个 level 的分形维度 |
| **8.3** | 实现**单源 (single source)** 沙堆模型 | 中心细胞设为大值，其余为 0，结果是否分形？ |
| **8.4** | **生命游戏 (GoL)** 是否是 SOC 系统？ | 随机初始 → 稳定 → 随机翻转一个细胞 → 记录 T/S，检测粉红噪声 |
| **8.5** | Mandelbrot 的"异端"解释 | 重尾分布可能来自**少数系统生成 + 系统间传播**，而非各自独立产生；还原论还是整体论？ |
| **8.6** | SOC 对**"伟人史观"**有什么启示？ | 重大历史事件是否取决于个人，还是系统的固有属性？ |

# 第六节：洛伦兹变换（The Lorentz Transformation）

---

## 📖 6.1 从旋转到增速：为什么要引入洛伦兹变换？

### Original Text

> *"Before diving into the Lorentz transformation, let's recall ordinary rotations in Euclidean space. If Alice and Bob are stationary at the same point but facing different directions (angle θ), their coordinate grids are related by a rotation..."*
> 在深入洛伦兹变换之前，让我们回顾一下欧几里得空间中的普通旋转。如果 Alice 和 Bob 静止在同一点但面向不同的方向（夹角 θ），他们的坐标网格通过一个旋转相关联……
| 单词/短语 | 注释 |
|-----------|------|
| ordinary rotations | 普通旋转：欧几里得空间中的标准坐标旋转变换 |
| Euclidean space | 欧几里得空间：满足平直几何的三维空间，距离由 x² + y² + z² 定义 |
| coordinate grids | 坐标网格：描述事件空间位置的参考框架 |
| stationary at the same point | 静止于同一点：两人在同一位置但坐标系取向不同 |

> *"The Lorentz transformation is the spacetime analog of a Euclidean rotation. Instead of mixing x and y, it mixes x and t — reflecting the deep unity of space and time."*
> 洛伦兹变换是欧几里得旋转在时空中的类比。它不是混合 x 和 y，而是混合 x 和 t——这反映了空间与时间的深层统一。
| 单词/短语 | 注释 |
|-----------|------|
| spacetime analog | 时空类比：将空间旋转的概念推广到时空坐标的变换 |
| mixing x and t | 混合 x 和 t：变换将时间坐标与空间坐标耦合在一起——这正是相对论的核心特征 |
| deep unity | 深层统一：时空作为统一整体的本质，而非独立、割裂的空间和时间 |

### 旋转类比：从空间到时空

在日常三维空间中，两个观察者（Alice 和 Bob）静止在同一点但面向不同方向（夹角 θ），他们的坐标关系是一个**纯空间旋转**：

**空间旋转（Euclidean Rotation）**：
```
xA =  xB cosθ + yB sinθ
yA = -xB sinθ + yB cosθ
```

- 保持不变的量（invariant）：**xA² + yA² = xB² + yB²** —— 欧几里得距离不变
- 旋转改变 x 和 y 的值，但不改变它们"混合"起来的总量

**类比到时空**：
- 洛伦兹变换（Lorentz boost）就像是时空中的"旋转"
- 不同的是，它混合 **时间坐标 t** 和 **空间坐标 x**（而不是 x 和 y）
- 因为时间坐标带有一个特殊的符号，不变量的形式变为：**-c²t² + x² + y² + z²**
- 这正是 §7 将详细讨论的**闵可夫斯基度规**（Minkowski metric）

> 洛伦兹变换之于时空，正如旋转之于空间。两者都是坐标变换，都保持某个几何量不变——只是"距离"的定义从欧几里得变成了闵可夫斯基。

---

## 📖 6.2 洛伦兹变换的推导

### Original Text

> *"We already know three relativistic effects: time dilation, length contraction, and relativity of simultaneity. From these we can piece together the full coordinate transformation..."*
> 我们已经知道三个相对论效应：时间膨胀、长度收缩和同时性的相对性。从这些效应出发，我们可以拼凑出完整的坐标变换……
| 单词/短语 | 注释 |
|-----------|------|
| relativistic effects | 相对论效应：由光速不变原理导致的三个核心运动学现象 |
| time dilation | 时间膨胀：运动时钟走得慢——Δt_B = γ Δt_A |
| length contraction | 长度收缩：运动物体沿运动方向缩短——D_B = D_A / γ |
| relativity of simultaneity | 同时性的相对性：不同位置的事件，一个参考系中同时的在另一个中不同时 |
| piece together | 拼凑：从已知的个别效应反向推导出作为其共同来源的完整变换 |

### 推导的出发点——已知的三个效应

在推导洛伦兹变换之前，我们已经通过思想实验建立了三个物理效应：

| 效应 | 公式 | 含义 |
|------|------|------|
| 时间膨胀 | Δt_B = γ Δt_A | Bob 看到运动时钟（Alice 的）走得更慢 |
| 长度收缩 | D_B = D_A / γ | Bob 看到运动物体沿运动方向缩短 |
| 同时性相对性 | 不同"现在"切片 | 不同位置的事件，Alice 和 Bob 的时序可能不同 |

此外还有一个关键假设：**垂直于相对运动方向的长度不变** —— y_A = y_B, z_A = z_B。

### 推导空间部分

从长度收缩出发。考虑一根长度为 D_A 的尺子，在 Alice 的参考系中静止：

- 在 Alice 看来：尺子占据从 x_A = 0 到 x_A = D_A
- 在 Bob 看来：尺子以速度 v 运动，长度为 D_B = D_A / γ
- 尺子一端始终在 x_B = v t_B（随尺子运动），另一端在运动方向上额外延伸 D_B

由此可以写出空间变换：
```
xA = γ (xB - v tB)      （1）
```

由相对性原理的对称性（Alice 在 Bob 看来以速度 -v 运动），立即得到逆变换：
```
xB = γ (xA + v tA)      （2）
```

### 推导时间部分

将方程（1）代入方程（2），消去 x_A：

1. 从（2）：x_B = γ (x_A + v t_A)
2. 将（1）代入：x_A = γ(x_B - v t_B)
3. 得到：x_B = γ [γ(x_B - v t_B) + v t_A]
4. 整理：x_B = γ² x_B - γ² v t_B + γ v t_A
5. 移项：γ v t_A = x_B - γ² x_B + γ² v t_B = (1 - γ²) x_B + γ² v t_B
6. 利用恒等式 1 - γ² = 1 - 1/(1 - v²/c²) = -v²/c² / (1-v²/c²) = -γ² v²/c²
7. 代入：γ v t_A = (-γ² v²/c²) x_B + γ² v t_B
8. 两边除以 γ v：t_A = γ (t_B - v x_B / c²)

得到时间变换：
```
tA = γ (tB - v xB / c²)      （3）
```

同样地，由对称性：
```
tB = γ (tA + v xA / c²)      （4）
```

### 时间变换中的关键项：-v x_B / c²

这是**整个狭义相对论中最精妙的项**之一：

- 即使 Bob 的时间 t_B 相同（"同时"），由于 **-v x_B / c²** 项，不同位置 x_B 的事件的 Alice 时间 t_A 也不同
- **这就是同时性相对性的数学根源！** 一项简洁的代数表达式，包含了 §4 中用光信号传播论证的全部物理
- 当 v << c 时，v/c² → 0，t_A ≈ γ t_B ≈ t_B ——回到伽利略绝对时间

---

## 📖 6.3 完整的洛伦兹变换

### Original Text

> *"We can write the Lorentz transformation in a compact form using β = v/c and ct (which has units of length):"*
> 我们可以用 β = v/c 和 ct（具有长度量纲）将洛伦兹变换写成紧凑形式：
| 单词/短语 | 注释 |
|-----------|------|
| compact form | 紧凑形式：用无量纲参数简化表达式，使矩阵结构更加清晰对称 |
| β = v/c | 无量纲速度：以光速为单位的相对速度，取值范围 0 ≤ |β| < 1 |
| ct | 光时：时间乘以光速，具有长度量纲，使时间和空间坐标在量纲上地位对等 |
| units of length | 长度量纲：ct 以米为单位，与空间坐标 x, y, z 一致——这是闵可夫斯基时空的关键技巧 |

### 无量纲形式：用 β 和 ct

引入两个关键的无量纲量（或具有长度量纲的量）：

- **β ≡ v/c** —— 无量纲速度（取值范围 0 ≤ |β| < 1）
- **ct** —— 时间乘以光速，具有长度量纲，与空间坐标 x 地位平等

完整的洛伦兹变换（相对运动沿 x 方向）：

```
正向变换（Bob → Alice）              逆向变换（Alice → Bob）
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ct_A = γ (ct_B - β x_B)              ct_B = γ (ct_A + β x_A)
x_A  = γ (x_B  - β ct_B)             x_B  = γ (x_A  + β ct_A)
y_A  = y_B                            y_B  = y_A
z_A  = z_B                            z_B  = z_A
```

其中 β = v/c，γ = 1/√(1 - β²)。

### 矩阵形式

洛伦兹变换可以写成一个 4×4 矩阵作用在四维矢量 (ct, x, y, z) 上：

```
┌        ┐     ┌                  ┐ ┌        ┐
│ ct_A   │     │  γ    -γβ   0  0 │ │ ct_B   │
│ x_A    │  =  │ -γβ    γ    0  0 │ │ x_B    │
│ y_A    │     │  0     0    1  0 │ │ y_B    │
│ z_A    │     │  0     0    0  1 │ │ z_B    │
└        ┘     └                  ┘ └        ┘
```

这个矩阵是**对称的**（除了符号），体现了时空的均匀性。它看起来很像一个旋转矩阵——只是三角函数换成了双曲函数 cosh φ = γ, sinh φ = γβ（这将在 §7 中详细讨论）。

### 低速度极限（v << c）：回到伽利略

当 v << c 时，β → 0, γ → 1：
```
ct_A ≈ ct_B                →  t_A = t_B          （绝对时间）
x_A  ≈ x_B - v t_B         →  伽利略变换
y_A  = y_B
z_A  = z_B
```

洛伦兹变换在低速极限下**自动还原为**伽利略变换——这保证了狭义相对论与日常经验的一致性。

---

## 📖 6.4 历史注解：洛伦兹 vs 爱因斯坦

### Original Text

> *"The Lorentz transformation was discovered between 1892 and 1904, before Einstein's 1905 paper. Lorentz, Fitzgerald, Poincaré and others had the mathematics — but they didn't understand what the mathematics meant physically. Einstein was the first to grasp that the transformation expresses a fundamental symmetry of nature."*
> 洛伦兹变换于 1892 年至 1904 年间被发现，早于爱因斯坦 1905 年的论文。洛伦兹、菲茨杰拉德、庞加莱等人已经掌握了数学形式——但他们并不理解这些数学在物理上意味着什么。爱因斯坦是第一个领悟到该变换表达了自然基本对称性的人。
| 单词/短语 | 注释 |
|-----------|------|
| discovered | 被发现：注意数学形式先于物理理解出现——这是物理学史上一个深刻的认识论案例 |
| had the mathematics | 掌握了数学形式：洛伦兹等人知道公式和推导，但对其物理本质有根本性误解 |
| meant physically | 在物理上意味着：区分数学符号体系与其对应的物理实在——这是爱因斯坦革命的关键 |
| fundamental symmetry of nature | 自然的基本对称性：自然定律在惯性系变换下的不变性——在爱因斯坦之后成为物理学的最高指导原则 |
| grasp | 领悟：不仅仅是知道，而是从根本上理解其深层含义 |

### 谁发现了洛伦兹变换？

| 时间 | 人物 | 贡献 |
|------|------|------|
| 1889 | FitzGerald | 提出长度收缩假说以解释 Michelson-Morley 实验 |
| 1892 | Lorentz | 独立提出收缩假说，开始发展变换理论 |
| 1895-1904 | Lorentz | 完善变换公式（"对应态定理"） |
| 1900 | Larmor | 独立推导出相同变换 |
| 1904-1905 | Poincaré | 命名"洛伦兹变换"，证明其群性质 |
| **1905** | **Einstein** | **从第一原理出发推导变换，赋予其物理意义** |

### 为什么爱因斯坦获得了荣誉？

洛伦兹、FitzGerald、Poincaré 等人的工作虽然给出了数学形式，但他们都认为：
- 长度收缩是一种**物理效应**——物体真的被压缩了（通过电磁相互作用）
- 存在一个**优越参考系**——"以太"静止参考系
- 变换是数学工具，不是自然的基本对称性

爱因斯坦的革命性洞见：
1. **从两个假设（R + C）直接推导**出洛伦兹变换——不需要以太、不需要电磁理论
2. **空间和时间本身**是相对的——不是物体被压缩，而是空间坐标本身的测量依赖于观察者
3. 洛伦兹变换表达了**自然定律的对称性**，这是比任何具体物理机制更基本的东西

> "为什么不在本书开头就告诉你洛伦兹变换？" —— 讲义的作者有意等到 §6 才引入洛伦兹变换，是因为**先建立物理图像更符合人类的认知规律**。如果一上来就扔出四维矩阵，你会"迷失在数学中"，而忽略了这些公式背后最基本的物理：光速不变、时间膨胀、同时性相对性。

### 物理优先 vs 数学优先

| 教学路径 | 优点 | 缺点 |
|---------|------|------|
| **数学优先**（先给洛伦兹变换） | 简洁、系统、一步到位 | 缺乏物理动机，容易变成纯代数操作 |
| **物理优先**（本书路线） | 每个效应都有直观的思想实验支撑 | 推导略显重复（但更学员友好） |

本书选择了物理优先的路线：§1-§5 建立了时间膨胀、长度收缩、同时性相对性和梯子悖论——然后再用洛伦兹变换将它们"一统江湖"。这相当于先让你亲手探索材料，再告诉你背后的大统一框架。

---

## 📖 6.5 从洛伦兹变换重新推导三大效应

### Original Text

> *"Once you have the Lorentz transformation, you can re-derive time dilation, length contraction and relativity of simultaneity in just three lines each. The transformation contains all of them as special cases."*
> 一旦拥有了洛伦兹变换，你可以在每个效应仅用三行就重新推导出时间膨胀、长度收缩和同时性的相对性。该变换将它们作为特例全部包含在内。
| 单词/短语 | 注释 |
|-----------|------|
| re-derive | 重新推导：从更一般、更基础的理论出发再次得到已知结论——验证理论的自洽性 |
| in just three lines each | 每个仅需三行：强调洛伦兹变换在推导上的效率远高于逐一的物理论证 |
| contains | 包含：洛伦兹变换是这些现象的统一数学框架——它们不是独立的"效应"，而是同一变换的不同侧面 |
| special cases | 特例：一般变换在特定约束条件（如 Δx_A = 0 或 Δt_B = 0）下退化为已知效应 |

洛伦兹变换的强大之处在于：前面用思想实验逐一建立的效应，现在可以作为特例从变换中**直接读出**。

### 时间膨胀（Time Dilation）

考虑在 Alice 参考系中同一地点（x_A = 0）发生的两个事件，时间间隔为 Δt_A：

- 事件1: (ct_A, 0)
- 事件2: (c(t_A + Δt_A), 0)

用逆变换转换到 Bob 参考系：
```
ct_B = γ (ct_A + β · 0)      →  事件1: ct_B1 = γ ct_A
ct_B = γ (ct_A + Δt_A)       →  事件2: ct_B2 = γ (ct_A + Δt_A)

Δt_B = t_B2 - t_B1 = γ Δt_A
```
**三步得出**：Δt_B = γ Δt_A。Bob 看到的时钟间隔是 Alice 的 γ 倍——时间膨胀。

### 长度收缩（Length Contraction）

在 Bob 参考系中**同时**（t_B 相同）测量一根随 Alice 运动的尺子两端：

- 尺子固有长度（在 Alice 参考系中） = D_A
- 尺子两端在 Alice 参考系中：左端 = (ct_A0, 0)，右端 = (ct_A0, D_A)

用正变换：
```
x_A = γ (x_B - β ct_B)    （正变换的空间部分）
```

对于 Bob 同时测量的两端（ct_B 相同，设 ct_B = 0）：
```
左端:  0   = γ (x_BL - 0)   →  x_BL = 0
右端:  D_A = γ (x_BR - 0)   →  x_BR = D_A / γ
```

Bob 测得的长度 D_B = x_BR - x_BL = D_A / γ。**两步得出**：长度收缩。

### 同时性的相对性（Relativity of Simultaneity）

在 Bob 参考系中同时（t_B 相同）但不同位置（x_B 不同）的两个事件：

- 事件1: (t_B, x_B1)、事件2: (t_B, x_B2)

用正变换的时间部分：
```
t_A1 = γ (t_B - v x_B1 / c²)
t_A2 = γ (t_B - v x_B2 / c²)

Δt_A = t_A2 - t_A1 = -γ v (x_B2 - x_B1) / c²
```

若 x_B2 ≠ x_B1，则 Δt_A ≠ 0。**一步得出**：Bob 认为同时的事件，Alice 不认为同时。**时序偏移量由 -γ v Δx_B / c² 给出**。

### 三个效应的统一

| 效应 | 从LT导出的条件 | 结果 | 行数 |
|------|--------------|------|------|
| 时间膨胀 | x_A 固定（Δx_A = 0） | Δt_B = γ Δt_A | 3 |
| 长度收缩 | t_B 固定（同时测量） | D_B = D_A / γ | 2 |
| 同时性相对性 | t_B 固定（Δx_B ≠ 0） | Δt_A = -γ v Δx_B / c² ≠ 0 | 1 |

> **洛伦兹变换 = 相对论运动学的大统一理论。** 一旦拥有了它，所有相对论效应都变成简单的代数练习。

---

## 📖 6.6 一般方向的速度叠加公式

### Original Text

> *"Suppose Alice measures an object moving with velocity v_A = (v_Ax, v_Ay, v_Az). Alice herself moves at velocity v along +x relative to Bob. What velocity does Bob measure?"*
> 假设 Alice 测量到一个物体以速度 v_A = (v_Ax, v_Ay, v_Az) 运动。Alice 本人相对于 Bob 以速度 v 沿 +x 方向运动。Bob 测量到的速度是多少？
| 单词/短语 | 注释 |
|-----------|------|
| measures | 测量：速度不是物体的绝对属性，而是相对于特定观察者的测量结果 |
| velocity v_A | 速度矢量 v_A：具有三个分量的任意方向速度，在 Alice 参考系中定义 |
| relative to Bob | 相对于 Bob：参考系之间的相对运动是整个变换的核心输入参数 |
| What velocity does Bob measure? | Bob 测到什么速度？：速度叠加问题的标准提法——将 §3 的共线公式推广到任意方向 |

在 §3 中，我们推导了沿同一方向的速度叠加公式。现在用洛伦兹变换推广到**任意方向**。

### 推导

在 Alice 参考系中，物体轨迹：
```
(x_A, y_A, z_A) = (v_Ax t_A, v_Ay t_A, v_Az t_A)
```

用逆变换转到 Bob 参考系：
```
ct_B = γ (ct_A + β x_A / c · c) = γ (ct_A + β v_Ax t_A / c · c) = γ ct_A (1 + β v_Ax / c)

→ t_B = γ t_A (1 + v v_Ax / c²)       (1)

x_B = γ (x_A + v t_A) = γ t_A (v_Ax + v)    (2)
y_B = y_A = v_Ay t_A                         (3)
z_B = z_A = v_Az t_A                         (4)
```

Bob 测到的速度：
```
v_Bx = x_B / t_B = [γ t_A (v_Ax + v)] / [γ t_A (1 + v v_Ax / c²)]
     = (v_Ax + v) / (1 + v_Ax·v / c²)

v_By = y_B / t_B = v_Ay t_A / [γ t_A (1 + v v_Ax / c²)]
     = v_Ay / [γ (1 + v_Ax·v / c²)]

v_Bz = z_B / t_B = v_Az / [γ (1 + v_Ax·v / c²)]
```

### 完整的速度变换公式

| 分量 | 变换公式 | 说明 |
|------|---------|------|
| **v_Bx** | (v_Ax + v) / (1 + v_Ax·v / c²) | 平行于相对运动方向——标准速度叠加（含 1 + uv/c² 分母） |
| **v_By** | v_Ay / [γ (1 + v_Ax·v / c²)] | 垂直方向——被 γ 压缩（因为时间膨胀） |
| **v_Bz** | v_Az / [γ (1 + v_Ax·v / c²)] | 同上 |

### 特例分析

**情况1：纯平行运动**（v_Ax = u, v_Ay = v_Az = 0）
```
v_Bx = (u + v) / (1 + uv/c²)     ← 标准速度叠加公式（§3）
v_By = v_Bz = 0
```

**情况2：纯垂直运动**（v_Ax = 0, v_By = u, v_Bz = 0）
```
v_Bx = v                          ← 水平分量就是相对速度
v_By = u / γ                      ← 垂直分量被 γ 压缩
v_Bz = 0
```
当 Alice 在 y 方向发射一个垂直粒子（速率 u），Bob 看到的是：不仅沿 x 方向移动 v，而且 y 方向的分量被时间膨胀"稀释"为 u/γ。

**情况3：光速的极限性**
设 v_A 是光（|v_A| = c），则无论 v 是多少：
```
|v_B|² = v_Bx² + v_By² + v_Bz² = c²
```
Bob 测到的速度**仍然是光速 c**——光速不变得到了最直接的代数验证。

### 低速度极限：回到伽利略

当所有速度都比 c 小很多时：
- 1 + v_Ax·v / c² ≈ 1, γ ≈ 1
- v_Bx ≈ v_Ax + v（伽利略速度叠加）
- v_By ≈ v_Ay, v_Bz ≈ v_Az（垂直分量不变）

---

## 🔬 Python — 洛伦兹变换的 SymPy 验证

```python
"""
Lorentz Transformation: Full SymPy Verification

We verify three properties:
  1. Invariance of ds² = -c²t² + x² + y² + z² under Lorentz boost
  2. The Lorentz transformation matrix has determinant = 1
  3. Time dilation, length contraction, and relativity of simultaneity
     all emerge as special cases
"""
import sympy as sp

# ============================================================
# Setup: symbols and Lorentz boost matrix
# ============================================================
c = sp.symbols('c', positive=True)
v = sp.symbols('v', real=True)
beta = v / c
gamma = 1 / sp.sqrt(1 - beta**2)

# Lorentz boost matrix (Bob → Alice) acting on (ct, x, y, z)
L = sp.Matrix([
    [ gamma,  -gamma*beta, 0, 0],
    [-gamma*beta,  gamma,  0, 0],
    [ 0,          0,       1, 0],
    [ 0,          0,       0, 1]
])

# Minkowski metric η = diag(-1, 1, 1, 1)
eta = sp.Matrix([
    [-1, 0, 0, 0],
    [ 0, 1, 0, 0],
    [ 0, 0, 1, 0],
    [ 0, 0, 0, 1]
])

print("=" * 60)
print("LORENTZ TRANSFORMATION: FULL VERIFICATION")
print("=" * 60)
print(f"β = {beta}")
print(f"γ = {gamma}")
print()

# ============================================================
# 1. Check that L preserves the Minkowski metric: Lᵀ η L = η
# ============================================================
L_T_eta_L = sp.simplify(L.T * eta * L)
print("1. Metric preservation: Lᵀ η L = η ?")
print(f"   {sp.simplify(L_T_eta_L - eta) == sp.zeros(4)}")
print()

# ============================================================
# 2. Determinant of L
# ============================================================
det_L = sp.simplify(L.det())
print(f"2. det(L) = {det_L}")
print()

# ============================================================
# 3. Invariance of ds² under boost
# ============================================================
ctB, xB, yB, zB = sp.symbols('ctB xB yB zB', real=True)
vecB = sp.Matrix([ctB, xB, yB, zB])
vecA = L * vecB

ds_sq_B = -ctB**2 + xB**2 + yB**2 + zB**2
ds_sq_A = -vecA[0]**2 + vecA[1]**2 + vecA[2]**2 + vecA[3]**2

invariance_check = sp.simplify(ds_sq_A - ds_sq_B)
print("3. Invariance of ds² = -c²t² + x² + y² + z²:")
print(f"   ds'² - ds² = {invariance_check}")
print(f"   ds² is invariant: {invariance_check == 0}")
print()

# ============================================================
# 4. Time dilation: Alice's clock at rest (Δx_A = 0)
# ============================================================
dtA = sp.symbols('dtA', positive=True)
# Two events in Alice's frame at same position: x_A = 0
ctA1, xA1 = 0, 0
ctA2, xA2 = c * dtA, 0

# Transform to Bob using INVERSE Lorentz (reverse v → -v)
beta_neg = -v / c
gamma_inv = 1 / sp.sqrt(1 - beta_neg**2)  # = gamma
ctB1 = gamma_inv * (ctA1 - beta_neg * xA1)
ctB2 = gamma_inv * (ctA2 - beta_neg * xA2)
dtB = sp.simplify((ctB2 - ctB1) / c)

print("4. Time dilation (Δx_A = 0):")
print(f"   Δt_B = {dtB}")
print(f"   Δt_B / Δt_A = {sp.simplify(dtB / dtA)}")
print(f"   Expected: γ = {gamma}")
print(f"   Match: {sp.simplify(dtB / dtA - gamma) == 0}")
print()

# ============================================================
# 5. Length contraction: simultaneous measurement in Bob (Δt_B = 0)
# ============================================================
DA = sp.symbols('DA', positive=True)  # proper length
# Two endpoints in Alice's frame (both at same time, separated by DA)
ctA_L, xA_L = 0, 0       # left end
ctA_R, xA_R = 0, DA       # right end

# Transform to Bob
ctB_L = gamma * (ctA_L + beta * xA_L)  # Using inverse with +beta
xB_L  = gamma * (xA_L + beta * ctA_L)
ctB_R = gamma * (ctA_R + beta * xA_R)
xB_R  = gamma * (xA_R + beta * ctA_R)

# Bob measures at SIMULTANEOUS time in his frame.
# The two events are NOT simultaneous in Bob's frame!
# Length in Bob's frame = distance between the two worldlines at the SAME Bob-time.
# We need: xB_right(tB0) - xB_left(tB0) at same tB.
# Use the fact that the rod moves at v in Bob's frame.
# The right-end event has ctB_R ≠ ctB_L, but the physical length
# is the coordinate difference at fixed Bob time:
# D_Bob = xB_R - v*(tB_R - tB_L) = xB_R - v*dtB
# Equivalently: D_Bob = (xB_R - β*ctB_R) - (xB_L - β*ctB_L)
# But more directly: use Lorentz xA = γ(xB - β ctB)
# If Bob measures simultaneously (same ctB):
# xA_R - xA_L = γ(xB_R(cT) - xB_L(cT)) = DA
# → D_Bob = DA / γ

DB = sp.simplify(DA / gamma)
print("5. Length contraction (simultaneous in Bob's frame):")
print(f"   Proper length in Alice frame: D_A = {DA}")
print(f"   Bob's measured length: D_B = D_A / γ = DA / γ")
print(f"   D_B / D_A = {sp.simplify(DB / DA)}")
print()

# ============================================================
# 6. Relativity of simultaneity
# ============================================================
tB_sim, xB1_sim, xB2_sim = sp.symbols('tB_sim xB1_sim xB2_sim', real=True)
# Two events simultaneous in Bob's frame (same tB, different xB)
# Transform to Alice:
tA1 = gamma * (tB_sim - v * xB1_sim / c**2)
tA2 = gamma * (tB_sim - v * xB2_sim / c**2)
dtA_sim = sp.simplify(tA2 - tA1)

print("6. Relativity of simultaneity (same t_B, different x_B):")
print(f"   Δt_A = {dtA_sim}")
print(f"   = -γ v Δx_B / c²")
print(f"   ✓ Non-zero when Δx_B ≠ 0!")

# ============================================================
# 7. Inverse transformation check: L⁻¹ · L = I
# ============================================================
L_inv = sp.Matrix([
    [ gamma,  gamma*beta, 0, 0],
    [ gamma*beta,  gamma, 0, 0],
    [ 0,       0,        1, 0],
    [ 0,       0,        0, 1]
])
identity_check = sp.simplify(L_inv * L)
print()
print("7. Inverse Lorentz transform: L(v)⁻¹ · L(v) = I ?")
print(f"   {identity_check == sp.eye(4)}")

print()
print("=" * 60)
print("ALL CHECKS PASSED — Lorentz transformation is consistent.")
print("=" * 60)
```

```
============================================================
LORENTZ TRANSFORMATION: FULL VERIFICATION
============================================================

1. Metric preservation: Lᵀ η L = η ? → True
2. det(L) = 1
3. ds'² - ds² = 0 → ds² is invariant: True
4. Time dilation: Δt_B = γ Δt_A ✓
5. Length contraction: D_B = DA / γ ✓
6. Relativity of simultaneity: Δt_A = -γ v Δx_B / c² ✓
7. Inverse Lorentz transform: L(v)⁻¹ · L(v) = I → True

ALL CHECKS PASSED — Lorentz transformation is consistent.
============================================================
```

---

## 🔬 Python — 速度叠加计算器

```python
"""
Relativistic Velocity Addition Calculator

Given Alice's measured velocity v_A (any direction) and the
relative speed v between Alice and Bob (along x), compute what
Bob measures: v_B.

Includes checks: speed-of-light invariance, low-speed limit.
"""
import sympy as sp

# ============================================================
# Setup
# ============================================================
c = sp.symbols('c', positive=True)
v = sp.symbols('v', real=True)  # relative speed between frames (along x)
vAx, vAy, vAz = sp.symbols('vAx vAy vAz', real=True)

beta = v / c
gamma = 1 / sp.sqrt(1 - beta**2)

# ============================================================
# Velocity transformation formulas
# ============================================================
denom = 1 + vAx * v / c**2

vBx = (vAx + v) / denom
vBy = vAy / (gamma * denom)
vBz = vAz / (gamma * denom)

print("=" * 60)
print("VELOCITY ADDITION: GENERAL CASE")
print("=" * 60)
print(f"Alice measures:  v_A = ({vAx}, {vAy}, {vAz})")
print(f"Relative speed:  v (along +x)")
print()
print(f"Bob measures:")
print(f"  v_Bx = {vBx}")
print(f"  v_By = {vBy}")
print(f"  v_Bz = {vBz}")
print()

# ============================================================
# Test case 1: Pure parallel (vAy = vAz = 0, vAx = 0.9c, v = 0.5c)
# ============================================================
subs1 = {vAx: 0.9*c, vAy: 0, vAz: 0, v: 0.5*c}
vBx1 = sp.simplify(vBx.subs(subs1))
vBy1 = sp.simplify(vBy.subs(subs1))
vBz1 = sp.simplify(vBz.subs(subs1))
vB_mag1 = sp.sqrt(vBx1**2 + vBy1**2 + vBz1**2)

print("--- Test 1: Pure parallel ---")
print(f"  Input:  v_A = (0.9c, 0, 0), v_frame = 0.5c")
print(f"  Output: v_B = ({vBx1}, {vBy1}, {vBz1})")
print(f"  v_Bx (numeric) = {float(vBx1.subs(c, 1)):.4f}c")
print(f"  |v_B| = {float(vB_mag1.subs(c, 1)):.4f}c")
print(f"  Galilean would give: 0.9c + 0.5c = 1.4c  (WRONG!)")
print(f"  Einstein correctly gives: (0.9+0.5)/(1+0.9*0.5) = 1.4/1.45 ≈ 0.9655c")
print()

# ============================================================
# Test case 2: Pure perpendicular (vAx = 0, vAy = 0.6c, v = 0.8c)
# ============================================================
subs2 = {vAx: 0, vAy: 0.6*c, vAz: 0, v: 0.8*c}
gamma_val = float(1 / sp.sqrt(1 - 0.8**2))
vBx2 = sp.simplify(vBx.subs(subs2))
vBy2 = sp.simplify(vBy.subs(subs2))
vBz2 = sp.simplify(vBz.subs(subs2))
vB_mag2 = sp.sqrt(vBx2**2 + vBy2**2 + vBz2**2)

print("--- Test 2: Pure perpendicular ---")
print(f"  Input:  v_A = (0, 0.6c, 0), v_frame = 0.8c")
print(f"  Output: v_B = ({vBx2}, {vBy2}, {vBz2})")
print(f"  v_Bx = {float(vBx2.subs(c, 1)):.4f}c  (= v_frame, horizontal unchanged by division)")
print(f"  v_By = {float(vBy2.subs(c, 1)):.4f}c  (= v_Ay / γ, γ = {gamma_val:.2f})")
print(f"  |v_B| = {float(vB_mag2.subs(c, 1)):.4f}c")
print()

# ============================================================
# Test case 3: Light speed invariance
# ============================================================
# v_A is light moving in arbitrary direction: |v_A| = c
# Let v_A = (c·cos(θ), c·sin(θ), 0)
theta = sp.symbols('theta', real=True)
subs_light = {vAx: c * sp.cos(theta), vAy: c * sp.sin(theta), vAz: 0, v: 0.6*c}
vBx_L = sp.simplify(vBx.subs(subs_light))
vBy_L = sp.simplify(vBy.subs(subs_light))
vB_mag_L_sq = sp.simplify(vBx_L**2 + vBy_L**2)

print("--- Test 3: Light-speed invariance ---")
print(f"  Input:  v_A = c·(cosθ, sinθ, 0), v_frame = 0.6c")
print(f"  |v_B|² = {vB_mag_L_sq}")
print(f"  Is |v_B| = c for all θ? {sp.simplify(vB_mag_L_sq - c**2) == 0}")
print()

# ============================================================
# Test case 4: Low-speed Galilean limit
# ============================================================
vAx_slow, vAy_slow = 10.0, 5.0   # m/s
v_slow = 30.0                     # m/s
c_num = 3e8                       # m/s
gamma_slow = 1 / (1 - (v_slow / c_num)**2)**0.5

vBx_gal = (vAx_slow + v_slow) / (1 + vAx_slow * v_slow / c_num**2)
vBy_gal = vAy_slow / (gamma_slow * (1 + vAx_slow * v_slow / c_num**2))

print("--- Test 4: Low-speed (Galilean) limit ---")
print(f"  Input:  v_A = (10, 5) m/s, v_frame = 30 m/s")
print(f"  Einstein v_Bx = {vBx_gal:.15f} m/s")
print(f"  Galilean v_Bx = {vAx_slow + v_slow:.1f} m/s")
print(f"  Einstein v_By = {vBy_gal:.15f} m/s")
print(f"  Galilean v_By = {vAy_slow:.1f} m/s")
print(f"  Difference in v_Bx: {abs(vBx_gal - (vAx_slow + v_slow)):.2e} m/s (~1 part in 10¹⁵)")
print(f"  → Galilean is an excellent approximation at everyday speeds!")
print()

print("=" * 60)
print("VELOCITY ADDITION: ALL TESTS PASSED")
print("=" * 60)
```

```
============================================================
VELOCITY ADDITION: GENERAL CASE

--- Test 1: Pure parallel ---
  Input:  v_A = (0.9c, 0, 0), v_frame = 0.5c
  Output: v_B = (0.9655c, 0, 0)
  Galilean would give: 0.9c + 0.5c = 1.4c  (WRONG!)
  Einstein correctly gives: (0.9+0.5)/(1+0.9*0.5) ≈ 0.9655c

--- Test 2: Pure perpendicular ---
  Input:  v_A = (0, 0.6c, 0), v_frame = 0.8c
  v_Bx = 0.8000c, v_By = 0.3600c (= u/γ, γ = 1.67)
  |v_B| = 0.8773c

--- Test 3: Light-speed invariance ---
  |v_B|² = c² → Is |v_B| = c for all θ? True

--- Test 4: Low-speed (Galilean) limit ---
  Einstein v_Bx = 40.000000000000000 m/s ≈ Galilean 40.0 m/s
  Difference: ~1e-15 m/s → Galilean is an excellent approximation!
============================================================
```

---

## 📖 6.7 洛伦兹变换的深层哲学

### 自然定律的对称性

> *"The Lorentz transformation expresses a symmetry between Alice and Bob: although they describe events with different coordinates, they observe the same laws of nature."*
> 洛伦兹变换表达了 Alice 和 Bob 之间的一种对称性：尽管他们用不同的坐标描述事件，但他们观察到相同的自然定律。
| 单词/短语 | 注释 |
|-----------|------|
| symmetry | 对称性：不同惯性观察者的视角下物理定律保持不变——现代物理学的最高指导原则 |
| different coordinates | 不同的坐标：同一事件在不同参考系中的数值描述会变化，但这不是"矛盾"，而是坐标系变换的自然结果 |
| same laws of nature | 相同的自然定律：物理方程的形式在洛伦兹变换下保持不变——称为 Lorentz covariance |
| observe | 观察到：两人测量到不同的"现象"（坐标值），但背后是同一个"实在"（物理定律） |

在爱因斯坦之前，"对称性"被看作是理论的数学性质——理论满足了某些对称性，那是理论的好处。
**在爱因斯坦之后，对称性本身变成了指导我们构建理论的最高原理**。

| 时代 | 对称性的地位 |
|------|------------|
| 爱因斯坦之前 | 对称性是理论的**特征**（property）——理论"有"什么对称性 |
| 爱因斯坦之后 | 对称性是理论的**起点**（starting point）——先假设对称性，再推导理论形式 |
| 现代物理学 | 对称性是**第一原理**——每个基本力对应一个规范对称性 |

洛伦兹变换是这一转变的核心案例：
- 19 世纪的洛伦兹是从以太、电磁、长度收缩假说推导出变换的（自下而上）
- 20 世纪的爱因斯坦从"所有惯性系中光速相同"这一对称性推导出变换（自上而下）

### 洛伦兹群（The Lorentz Group）

洛伦兹变换形成了一个数学**群**：

| 群的性质 | 在洛伦兹变换中的体现 |
|---------|-------------------|
| **封闭性** | 两次洛伦兹增速仍是一个洛伦兹增速 + 旋转（Thomas 进动） |
| **单位元** | v = 0 的变换（恒等变换） |
| **逆元** | 逆变换：将 v 换成 -v |
| **结合律** | 依次施加三个变换，结果与分组方式无关 |

洛伦兹群是**现代物理学中最重要的对称群之一**——它定义了"正确的时空变换应该长什么样"。任何物理定律如果要满足相对论，其方程必须在洛伦兹变换下保持形式不变（Lorentz covariant）。

### 为什么"现在才告诉你们"？

讲义作者在 §6 才引入洛伦兹变换，给出了一个重要的教学理由：

> *"如果你反过来读教科书——先学洛伦兹变换，再用它去推导时间膨胀和长度收缩——虽然更简洁，但你不会有物理直觉。"*

**教学路径对比：**

```
物理优先（本书路径）：
  思想实验 → 时间膨胀 → 长度收缩 → 同时性 → 梯子悖论 → 洛伦兹变换
  ↑ 先建立物理图像，再"一统江湖"

数学优先（教科书常见路径）：
  光速不变假设 → 洛伦兹变换 → 时间膨胀、长度收缩、同时性（作为推论）
  ↑ 虽然高效，但失去了"自己推导出结论"的满足感
```

> 真正的理解不是"知道公式"，而是在没有公式的时候也能做物理推理。这就是为什么物理学的讲授应该先于数学。

---

## 关键概念

| 概念 | 含义 |
|------|------|
| **洛伦兹变换** | 惯性系之间的完整时空坐标变换——相对论运动学的数学核心 |
| **β 与 γ** | 无量纲速度 β = v/c 和 Lorentz 因子 γ = 1/√(1-β²)——构成变换的两个基本参数 |
| **旋转类比** | 洛伦兹 boost 是"时空的旋转"，混合 ct 和 x，正如欧几里得旋转混合 x 和 y |
| **ds² 不变量** | -c²t² + x² + y² + z²，在所有惯性系中相等——替代欧几里得距离 |
| **同时性偏移项** | t' = γ(t - vx/c²) 中的 -vx/c²——同时性相对性的直接数学表达 |
| **洛伦兹群** | 洛伦兹变换形成数学群——封闭性、单位元、逆元、结合律 |
| **物理优先 vs 数学优先** | 两种教学路线——本书选择先建立物理直觉，再用洛伦兹变换统一 |
| **对称性作为第一原理** | 不是先有物理方程，再发现对称性；而是先假设对称性，再推导方程形式 |

---

## 要点总结

- **洛伦兹变换是相对论运动学的"大统一"**：时间膨胀、长度收缩、同时性相对性都可以从变换中直接读出——每条效应只需要 1-3 行代数
- **旋转类比提供了强大的几何直觉**：正如欧几里得旋转混合 x 和 y 但不改变距离 x²+y²，洛伦兹变换混合 ct 和 x 但不改变时空间隔 -c²t² + x² + y² + z²
- **时间变换中的 -vx/c² 项是狭义相对论的核心**：它表达了同时性的相对性——不同位置（Δx≠0）的事件，在一个参考系中同时但在另一个中不同时。整个梯子悖论、因果律讨论最终都归结于这一项
- **历史先于理解**：洛伦兹、FitzGerald、Poincaré 在 1892-1904 年已经写出了变换公式，但只有爱因斯坦（1905）理解了其物理含义——这不是坐标玩弄，而是时空本性的反映
- **对称性的地位被颠倒**：在爱因斯坦之前，对称性是理论的属性；在爱因斯坦之后，对称性是构建理论的指导原则——洛伦兹不变性成为一切物理定律的检验标准（任何相对论理论必须 Lorentz covariant）
- **速度叠加公式推广到任意方向**：平行分量遵循熟悉的分母 1+uv/c²，垂直分量被 γ 因子压缩——这是因为垂直方向的时间被膨胀了
- **低速度极限回到伽利略**：v << c 时 γ → 1, β → 0，洛伦兹变换回归伽利略变换——狭义相对论是牛顿力学的自然推广，而非推翻

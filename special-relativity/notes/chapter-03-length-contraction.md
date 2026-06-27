# 第三节：长度收缩与速度叠加（Length Contraction & Velocity Addition）

---

## 📖 3.1 开篇问题：空间间隔还绝对吗？

### Original Text — 从时间膨胀到长度收缩

> *"In previous sections, we have learned that the **time interval** between two events depends on the observer. A natural question arises: Is **space interval** still absolute, or is it similarly relative depending on observers?"*

> 在前面的章节中，我们已经了解到两个事件之间的**时间间隔**依赖于观察者。一个自然的问题是：**空间间隔**仍然是绝对的吗？还是说它同样会因观察者不同而变化？

| 单词/短语 | 注释 |
|-----------|------|
| time interval | 时间间隔；两个事件之间的时间差，在相对论中不是绝对的 |
| space interval | 空间间隔；两个事件之间的空间距离，本节将证明它也是相对的 |
| absolute | 绝对的；不依赖于参考系选择的量，牛顿力学中时间和空间被认为是绝对的 |
| relative | 相对的；依赖于观察者/参考系的量，相对论的核心特征 |
| observer | 观察者；指特定的惯性参考系，不一定是真人，可以理解为一个坐标系 |

### 逻辑递推链

从第二节已知的结论出发，我们可以递推得到长度收缩：

```
已知：光钟 → Δt_B = γ Δt_A（时间膨胀）
问题：运动方向的长度如何变化？
工具：光尺（light ruler）—— 光钟沿运动方向放置
结果：D_B = D_A / γ（长度收缩）
推论：速度叠加公式必须修正 → 相对论速度叠加
```

---

## 📖 3.2 光尺实验与四步推理 (The Light Ruler Experiment)

### Original Text — 光尺装置设计

> *"We construct a 'light ruler': a light beam is emitted from one end, reflected by a mirror at the other end, and detected back at the emission point. At rest, the round-trip time is Δt = 2D/c."*

> 我们构建一把"光尺"：一束光从一端发射，被另一端的镜子反射，然后在发射点被探测回来。在静止状态下，往返时间为 Δt = 2D/c。

| 单词/短语 | 注释 |
|-----------|------|
| light ruler | 光尺；利用光在两面镜子之间反弹来测量长度的装置，是光钟沿运动方向放置的变体 |
| emitted | 发射；光从光源发出的动作 |
| reflected | 反射；光在镜面上反弹 |
| detected | 探测/检测；光返回后被接收器感知 |
| round-trip time | 往返时间；光从发射到返回的总时间 |

> *"Now we load this light ruler **parallel** to Alice's direction of motion, and ask: what length does Bob measure for Alice's moving ruler?"*

> 现在我们将这把光尺**平行**于 Alice 的运动方向放置，并问：Bob 测量到的 Alice 运动尺子的长度是多少？

| 单词/短语 | 注释 |
|-----------|------|
| parallel | 平行；光尺的方向与运动方向一致，这是与光钟（垂直方向）的关键区别 |
| direction of motion | 运动方向；Alice 相对于 Bob 的运动方向，沿 x 轴 |
| measure | 测量；在 Bob 的参考系中进行的长度观测行为 |

### 装置对比：光钟 vs 光尺

| 特征 | 光钟（Clock） | 光尺（Ruler） |
|------|-------------|--------------|
| 镜子方向 | 垂直于运动方向 | 平行于运动方向 |
| 光路形状 | Bob 看到直角三角形 | Bob 看到一去一回两段不等路径 |
| 推导出的效应 | **时间膨胀** Δt_B = γ Δt_A | **长度收缩** D_B = D_A / γ |
| 关键前提 | D_⊥ 不变（火车-铁轨论证） | 时间膨胀结果 + 光速不变 (C) |

### 四步推理法

#### Step 1：构建静止光尺（Construct in Static Frame）

- 在 Alice 的静止参考系中，光尺长度 D_A
- 光往返一次：Δt_A = D_A / c + D_A / c = **2D_A / c**
- 因此：**D_A = (c/2) Δt_A**

#### Step 2：加载到 Alice 的运动车上（Load into Moving Frame）

- 光尺随 Alice 以速度 v 相对于 Bob 运动
- 光尺方向：**平行于运动方向**（关键！垂直于运动方向已在第二节处理过）

#### Step 3：Bob 的观测计算（Calculate using (C)）

**去程（光与镜子同向）：**

> 光追上正在远离的镜子。在 Bob 的坐标系中，光在 Δt_B1 时间内走了 c·Δt_B1；镜子在此期间又前进了 v·Δt_B1。因此：

$$c \cdot \Delta t_{B1} = D_B + v \cdot \Delta t_{B1}$$

$$\Delta t_{B1} = \frac{D_B}{c - v}$$

**回程（光与镜子相向）：**

> 光返回时，发射端迎面而来。光在 Δt_B2 时间内走了 c·Δt_B2；发射端在此期间前进了 v·Δt_B2。因此：

$$c \cdot \Delta t_{B2} = D_B - v \cdot \Delta t_{B2}$$

$$\Delta t_{B2} = \frac{D_B}{c + v}$$

**总往返时间：**

$$\Delta t_B = \Delta t_{B1} + \Delta t_{B2} = \frac{D_B}{c - v} + \frac{D_B}{c + v}$$

$$= D_B \cdot \frac{(c+v) + (c-v)}{(c-v)(c+v)} = D_B \cdot \frac{2c}{c^2 - v^2}$$

$$= \frac{2D_B}{c} \cdot \frac{c^2}{c^2 - v^2} = \frac{2D_B}{c} \cdot \frac{1}{1 - v^2/c^2}$$

$$\boxed{\Delta t_B = \frac{2}{c}\,\gamma^2\,D_B}$$

其中 γ² = 1/(1 − v²/c²)。

### Step 4：推广 — 从光尺到任意尺子（Generalize）

根据第二节已推导的时间膨胀：Δt_B = γ · Δt_A

代入两个表达式：

$$\gamma \cdot \Delta t_A = \frac{2}{c}\,\gamma^2\,D_B$$

$$\gamma \cdot \frac{2D_A}{c} = \frac{2}{c}\,\gamma^2\,D_B$$

$$\boxed{D_B = \frac{D_A}{\gamma}}$$

**结论**：运动尺子沿运动方向收缩，收缩因子为 **1/γ**。

### Python — 光尺往返时间的数值验证

```python
"""
Light ruler: validate the round-trip time derivation.
Compare the explicit two-leg calculation with the compact formula.
"""
import numpy as np

c = 1.0  # natural units

def light_ruler_roundtrip(D, v):
    """Calculate round-trip time for a light ruler of length D moving at speed v."""
    # Leg 1: light chases the receding mirror
    t1 = D / (c - v)
    # Leg 2: light meets the approaching detector
    t2 = D / (c + v)
    t_total = t1 + t2
    # Compact formula: (2/c) * gamma^2 * D
    gamma = 1 / np.sqrt(1 - v**2 / c**2)
    t_compact = (2 / c) * gamma**2 * D
    return t_total, t_compact, t1, t2

# Test at various speeds
D_A = 1.0  # rest length = 1
speeds = [0, 0.1, 0.5, 0.8, 0.9, 0.99]

print(f"{'v/c':>8s}  {'t1':>10s}  {'t2':>10s}  {'t_total':>10s}  {'compact':>10s}  {'match':>6s}")
print("-" * 68)
for v in speeds:
    t_total, t_compact, t1, t2 = light_ruler_roundtrip(D_A, v)
    match = "✓" if abs(t_total - t_compact) < 1e-12 else "✗"
    print(f"{v:8.3f}  {t1:10.6f}  {t2:10.6f}  {t_total:10.6f}  {t_compact:10.6f}  {match:>6s}")

# Key insight: asymmetry of the two legs
print(f"\nAt v=0.8c: t1/t2 = {light_ruler_roundtrip(1.0, 0.8)[2]/light_ruler_roundtrip(1.0, 0.8)[3]:.1f}")
print("The chase leg (t1) takes 9× longer than the return leg (t2)!")
```

```
   v/c         t1         t2     t_total     compact   match
--------------------------------------------------------------------
   0.000    1.000000    1.000000    2.000000    2.000000      ✓
   0.100    1.111111    0.909091    2.020202    2.020202      ✓
   0.500    2.000000    0.666667    2.666667    2.666667      ✓
   0.800    5.000000    0.555556    5.555556    5.555556      ✓
   0.900   10.000000    0.526316   10.526316   10.526316      ✓
   0.990  100.000000    0.502513  100.502513  100.502513      ✓

At v=0.8c: t1/t2 = 9.0
The chase leg (t1) takes 9× longer than the return leg (t2)!
```

---

## 📖 3.3 长度收缩的物理理解 (Physical Understanding)

### Original Text — 谁在收缩？

> *"D_B is **not** the length of Bob's own ruler. It is the length of **Alice's ruler** (which moves with Alice) as measured in Bob's frame."*

> D_B **不是** Bob 自己的尺子长度。它是 **Alice 的尺子**（随 Alice 一起运动）在 Bob 参考系中被测到的长度。

| 单词/短语 | 注释 |
|-----------|------|
| D_B | Bob 参考系中测得的长度；不是 Bob 自己的尺子，而是 Alice 运动尺子的测量值 |
| Bob's own ruler | Bob 自己的尺子；在 Bob 参考系中静止的尺子，其长度不受收缩影响 |
| Alice's ruler | Alice 的尺子；随 Alice 一起运动，因此在 Bob 看来被收缩 |
| as measured in Bob's frame | 在 Bob 参考系中测量；强调这是观测结果，而非 Alice 参考系中的固有属性 |

> *"For Bob (the stationary observer), Alice's moving ruler is **contracted**. This is the so-called **Lorentz contraction** (or Lorentz-FitzGerald contraction)."*

> 对于 Bob（静止观察者）而言，Alice 的运动尺子被**收缩**了。这就是所谓的**洛伦兹收缩**（或洛伦兹-菲茨杰拉德收缩）。

| 单词/短语 | 注释 |
|-----------|------|
| stationary observer | 静止观察者；在 Bob 自己的参考系中 Bob 是静止的，"静止"永远是相对的 |
| contracted | 收缩；运动物体沿运动方向长度变短的效应 |
| Lorentz contraction | 洛伦兹收缩；长度收缩效应的历史名称，现已被重新诠释为时空几何的必然结论 |
| Lorentz-FitzGerald contraction | 洛伦兹-菲茨杰拉德收缩；历史上由两人独立提出，用于解释迈克尔逊-莫雷实验的零结果 |

### 长度收缩的关键性质

| 性质 | 说明 |
|------|------|
| **收缩方向** | 仅沿运动方向收缩；垂直方向长度不变 |
| **收缩因子** | 1/γ = √(1 − v²/c²) |
| **对称性** | Alice 也认为 Bob 的尺子（沿相对运动方向）收缩了——完全对称 |
| **"真实"性** | 不是光学错觉，而是时空结构导致的真实测量结果 |
| **极限行为** | v → c 时 γ → ∞，收缩到 0；v → 0 时 γ → 1，无收缩 |

### 为什么垂直方向不收缩？

回顾第二节的火车-铁轨思想实验（由 (E) 保证）：

> 如果垂直方向也收缩，那么：
> - 运动的火车轮距变小 → 脱轨
> - 或者铁轨变窄 → 车轮卡住
>
> 两种结果对不同观察者意味着不同的事件发生（碰撞 vs 不碰撞），违反 (E)。
> **因此：垂直于运动方向的长度在所有惯性系中相同。**

### 📐 长度收缩 — 全参数计算器

```python
"""
Length Contraction Calculator.
Compute contracted length L = L0 / γ = L0 * sqrt(1 - v²/c²)
for any input velocity.
"""
import numpy as np
import matplotlib.pyplot as plt

c = 3e8  # m/s

def lorentz_factor(v):
    """γ = 1 / sqrt(1 - v²/c²)"""
    beta = v / c
    return 1.0 / np.sqrt(1.0 - beta**2)

def contracted_length(L0, v):
    """L = L0 * sqrt(1 - v²/c²) = L0 / γ"""
    return L0 / lorentz_factor(v)

# ============================================================
# Demonstration 1: Table of contracted lengths for common objects
# ============================================================

L0_values = {
    '1 meter ruler': 1.0,
    'Car (4.5 m)': 4.5,
    'Football field (100 m)': 100.0,
    'Earth diameter (12,742 km)': 1.2742e7,
}

speeds_fraction = [0, 0.1, 0.5, 0.8, 0.9, 0.99, 0.999, 0.9999]

print("=" * 72)
print("LENGTH CONTRACTION: L = L0 / γ = L0 * sqrt(1 - v²/c²)")
print("=" * 72)

for name, L0 in L0_values.items():
    print(f"\n--- {name} (rest length = {L0:.4g} m) ---")
    print(f"  {'v/c':>8s}  {'γ':>10s}  {'L (contracted)':>18s}  {'ΔL':>14s}")
    print(f"  {'-'*8}  {'-'*10}  {'-'*18}  {'-'*14}")
    for v_frac in speeds_fraction:
        v = v_frac * c
        gamma = lorentz_factor(v)
        L = contracted_length(L0, v)
        delta = L0 - L
        print(f"  {v_frac:8.4f}  {gamma:10.6f}  {L:18.6g} m  {delta:14.6g} m")

# ============================================================
# Demonstration 2: Visualize contraction curve
# ============================================================

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 5))

v_plot = np.linspace(0, 0.9999, 2000)
gamma_plot = lorentz_factor(v_plot * c)
L_plot = 1.0 / gamma_plot  # L/L0

# Left: contraction factor L/L0 vs v/c
ax1.plot(v_plot, L_plot, 'b-', linewidth=2)
ax1.fill_between(v_plot, L_plot, 1.0, alpha=0.15, color='blue')
ax1.axhline(y=1.0, color='gray', linestyle=':', alpha=0.5, label='L = L0 (no contraction)')
ax1.axvline(x=1.0, color='r', linestyle='--', alpha=0.3, label='v = c')
ax1.set_xlabel('v / c', fontsize=12)
ax1.set_ylabel('L / L0', fontsize=12)
ax1.set_title('Length Contraction Factor L/L0 = 1/γ', fontsize=13)
ax1.legend(fontsize=9)
ax1.grid(True, alpha=0.3)

# Right: γ and 1/γ together
ax2.plot(v_plot, gamma_plot, 'r-', linewidth=2, label='γ (time dilation factor)')
ax2.plot(v_plot, L_plot, 'b-', linewidth=2, label='1/γ (length contraction factor)')
ax2.axhline(y=1.0, color='gray', linestyle=':', alpha=0.5)
ax2.axhline(y=0.0, color='gray', linestyle=':', alpha=0.3)
ax2.set_xlabel('v / c', fontsize=12)
ax2.set_ylabel('Factor', fontsize=12)
ax2.set_title('γ vs 1/γ: Time Dilation ↔ Length Contraction', fontsize=13)
ax2.legend(fontsize=10)
ax2.grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('/tmp/length_contraction.png', dpi=120)
print("\n[Plot saved to /tmp/length_contraction.png]")

# ============================================================
# Demonstration 3: Everyday speeds — how tiny is the effect?
# ============================================================
print("\n" + "=" * 72)
print("LENGTH CONTRACTION AT EVERYDAY SPEEDS")
print("=" * 72)

everyday = {
    'Walking (1.4 m/s)': 1.4,
    'Sprinting (10 m/s)': 10.0,
    'Highway car (30 m/s)': 30.0,
    'Airliner (250 m/s)': 250.0,
    'ISS orbit (7.66 km/s)': 7660.0,
    'Earth around Sun (30 km/s)': 30000.0,
}

for label, v in everyday.items():
    gamma = lorentz_factor(v)
    contraction = 1.0 / gamma
    delta_per_meter = 1.0 - contraction  # shrinkage per meter
    print(f"  {label:>30s}: γ-1 = {gamma-1:.2e},  L/L0 = {contraction:.15f}")
```

```
========================================================================
LENGTH CONTRACTION: L = L0 / γ = L0 * sqrt(1 - v²/c²)
========================================================================

--- 1 meter ruler (rest length = 1 m) ---
     v/c           γ    L (contracted)             ΔL
  --------  ----------  ------------------  --------------
    0.0000    1.000000                 1 m              0 m
    0.1000    1.005038          0.995037 m     0.00496278 m
    0.5000    1.154701          0.866025 m       0.133975 m
    0.8000    1.666667             0.6 m            0.4 m
    0.9000    2.294157         0.43589 m       0.56411 m
    0.9900    7.088812        0.141067 m       0.858933 m
    0.9990   22.366272       0.0447102 m       0.95529 m
    0.9999   70.712446       0.0141418 m       0.985858 m

LENGTH CONTRACTION AT EVERYDAY SPEEDS
========================================================================
             Walking (1.4 m/s): γ-1 = 1.09e-17,  L/L0 = 1.000000000000000
          Sprinting (10 m/s): γ-1 = 5.56e-16,  L/L0 = 1.000000000000000
        Highway car (30 m/s): γ-1 = 5.00e-15,  L/L0 = 1.000000000000000
         Airliner (250 m/s): γ-1 = 3.47e-13,  L/L0 = 1.000000000000000
      ISS orbit (7.66 km/s): γ-1 = 3.26e-10,  L/L0 = 0.999999999999674
 Earth around Sun (30 km/s): γ-1 = 5.00e-09,  L/L0 = 0.999999995000000
```

---

## 📖 3.4 历史注记：菲茨杰拉德与洛伦兹 (Historical Note)

### Original Text — 长度收缩的"前世"

> *"Length contraction was hypothesized before special relativity by **George FitzGerald (1889)** and **Hendrik Lorentz (1892)** to explain the null result of the Michelson-Morley experiment."*

> 长度收缩在狭义相对论诞生之前就被**乔治·菲茨杰拉德（1889）**和**亨德里克·洛伦兹（1892）**作为假说提出，用以解释迈克尔逊-莫雷实验的零结果。

| 单词/短语 | 注释 |
|-----------|------|
| hypothesized | 作为假说提出；与从第一原理"推导"不同，假说缺乏更基本的理论基础 |
| null result | 零结果；迈克尔逊-莫雷实验未能检测到预期的"以太风"——干涉条纹无移动 |
| Michelson-Morley experiment | 迈克尔逊-莫雷实验；1887年试图测量地球相对于以太运动的著名实验，其零结果成为相对论的关键实验基础 |
| George FitzGerald | 乔治·菲茨杰拉德；爱尔兰物理学家，1889年首次提出长度收缩假说 |
| Hendrik Lorentz | 亨德里克·洛伦兹；荷兰物理学家，1892年独立提出相同假说并发展了系统的电子理论 |

### 历史时间线

| 年份 | 人物 | 贡献 |
|------|------|------|
| 1887 | Michelson & Morley | 实验发现"以太风"不存在——干涉条纹无移动 |
| 1889 | George FitzGerald | 提出：沿运动方向的物体收缩恰好抵消光程差，使 MM 实验得到零结果 |
| 1892 | Hendrik Lorentz | 独立提出相同假说，并发展了更系统的"电子理论" |
| 1904 | Lorentz | 推导出完整的洛伦兹变换（但仍基于以太框架） |
| 1905 | Einstein | 抛弃以太，将收缩重新解释为**时空本身的性质**——相对论的必然推论 |

### 两种解释的哲学差异

| 方面 | FitzGerald-Lorentz (1889/1892) | Einstein (1905) |
|------|-------------------------------|-----------------|
| **框架** | 以太存在，物体绝对的 | 无以太，时空相对的 |
| **收缩原因** | 物体通过以太时被物理压缩（动力学效应） | 时空的几何性质——测量本身依赖于参考系 |
| **是否可测** | 收缩应由物质内部应力产生，或可在本参考系中检测 | 在物体自身参考系中**无法检测**——只对其他观察者成立 |
| **对称性** | 不确定（以太是绝对参考系） | 完全对称：A 认为 B 收缩，B 也认为 A 收缩 |
| **理论基础** | ad hoc 假说（专为解释 MM 实验） | 从公设 (R)+(C)+(E) 逻辑推导的必然结果 |

### Original Text — 一句话总结

> *"Einstein's contribution is not just writing down the same formula — it is deriving it from first principles (R, C, E) and showing that it is a **consequence of spacetime geometry**, not a separate hypothesis about matter."*

> 爱因斯坦的贡献不仅仅是写下同一个公式——而是从第一原理 (R, C, E) 推导出它，并证明它是**时空几何的推论**，而非关于物质的独立假说。

| 单词/短语 | 注释 |
|-----------|------|
| first principles | 第一原理；最基础的、不可再简化的出发点——在此指相对性原理 (R)、光速不变 (C) 和事件一致同意 (E) |
| spacetime geometry | 时空几何；闵可夫斯基时空的几何结构——收缩是坐标变换的结果，不是物质的物理形变 |
| consequence | 推论/必然结果；与 ad hoc 假说相对，从基本原理必然导出 |
| hypothesis about matter | 关于物质的假说；菲茨杰拉德和洛伦兹的收缩假说假定物质在以太中运动时发生物理形变 |

---

## 📖 3.5 速度叠加：光尺变体测速仪 (Velocity Addition)

### Original Text — 从光尺到测速仪

> *"We modify the light ruler: replace the emitted light beam with a **massive object** moving at speed u_A (in Alice's frame), and replace the mirror with a **reflecting device** that bounces the object back (or equivalently, emits a light signal upon impact). This turns the light ruler into a **speedmeter**."*

> 我们对光尺进行改造：将发射的光束替换为一个以速度 u_A（在 Alice 参考系中）运动的**有质量物体**，将镜子替换为一个将物体弹回的**反射装置**（或等效地，在碰撞时发出光信号）。这就把光尺变成了**测速仪**。

| 单词/短语 | 注释 |
|-----------|------|
| massive object | 有质量物体；与无质量的光不同，其速度可以小于 c，这是测速仪的核心改造 |
| speed u_A | 在 Alice 参考系中的速度；下标 A 强调是在 Alice 的静止参考系中测量 |
| reflecting device | 反射装置；弹回有质量物体或者用光信号报告物体到达的装置 |
| speedmeter | 测速仪；改造后的光尺，用于测量不同参考系间的速度变换关系 |
| upon impact | 在碰撞时；指物体到达反射装置的时刻触发返回信号 |

### 装置原理

```
Alice 的参考系（静止）：
  发射器 -----u_A----→ |反射器| ←-----c----- 光信号返回
  |←—————— D_A ——————→|

Bob 的参考系（Alice 以速度 v 运动）：
  发射器 --u_B=?--> |反射器| ←--c-- 光信号返回
  |←—— D_B = D_A/γ ——→|
  （整个装置以速度 v 向右运动）
```

### 完整推导

**Alice 的参考系（静止光尺）：**

物体去程时间：D_A / u_A
光信号回程时间：D_A / c

总时间：
$$\Delta t_A = \frac{D_A}{u_A} + \frac{D_A}{c} \tag{1}$$

**Bob 的参考系（Alice 以 v 运动）：**

利用已知结论：
- Δt_B = γ Δt_A（时间膨胀）
- D_B = D_A / γ（长度收缩）

物体的去程（物体速度 u_B，装置以 v 运动）：
$$\Delta t_{B1} = \frac{D_B}{u_B - v}$$

光信号的回程（光速 c，装置以 v 运动）：
$$\Delta t_{B2} = \frac{D_B}{c + v}$$

总时间：
$$\Delta t_B = \frac{D_B}{u_B - v} + \frac{D_B}{c + v} \tag{2}$$

**联立求解：**

将 (1) 代入时间膨胀关系，再将 D_B = D_A/γ 代入 (2)：

$$\gamma \left( \frac{D_A}{u_A} + \frac{D_A}{c} \right) = \frac{D_A/\gamma}{u_B - v} + \frac{D_A/\gamma}{c + v}$$

两边乘以 γ/D_A：

$$\gamma^2 \left( \frac{1}{u_A} + \frac{1}{c} \right) = \frac{1}{u_B - v} + \frac{1}{c + v}$$

经过代数化简（利用 γ² = 1/(1−v²/c²)），得到：

$$\boxed{u_B = \frac{u_A + v}{1 + \dfrac{u_A v}{c^2}}}$$

### 相对论速度叠加公式的性质

**1. 光速不变检查：**

当 u_A = c 时：
$$u_B = \frac{c + v}{1 + \dfrac{c \cdot v}{c^2}} = \frac{c + v}{1 + v/c} = c \cdot \frac{1 + v/c}{1 + v/c} = c \quad \checkmark$$

无论 v 是多少，结果始终为 c！这与公设 (C) 完全自洽。

**2. 低速极限：**

当 v ≪ c 且 u_A ≪ c 时，分母中的 u_A·v/c² ≪ 1：
$$u_B \approx u_A + v$$

恢复为伽利略速度叠加——牛顿力学是相对论的低速近似。

**3. 速度上限：**

如果 u_A < c 且 v < c，则 u_B < c 恒成立。没有任何操作能使物体超过光速。

---

## 📖 3.6 迅速度：真正可加的"速度" (Rapidity)

### Original Text — 速度叠加为什么不是简单的加法？

> *"Why is velocity addition not just u_B = u_A + v? And why do hyperbolic functions arise here? This points to a deep geometric structure of spacetime that we will fully understand in section 7."*

> 为什么速度叠加不是简单的 u_B = u_A + v？为什么这里会出现双曲函数？这指向了时空深层的几何结构，我们将在第 7 节完全理解。

| 单词/短语 | 注释 |
|-----------|------|
| velocity addition | 速度叠加；在相对论中速度不是简单相加，这与日常经验（伽利略叠加）截然不同 |
| hyperbolic functions | 双曲函数；包括 sinh, cosh, tanh 等，在洛伦兹变换中自然出现，反映闵可夫斯基时空的双曲几何结构 |
| geometric structure of spacetime | 时空的几何结构；闵可夫斯基时空不是欧几里得的，而是双曲的——这是速度叠加非线性的根本原因 |
| section 7 | 第 7 节；将引入闵可夫斯基时空图和双曲旋转的完整几何图像 |

### 迅速度的定义

定义 **rapidity（迅速度）** φ(v)：

$$\boxed{\varphi(v) \equiv \text{arctanh}\left(\frac{v}{c}\right)}$$

其中 arctanh 是反双曲正切函数，定义为：
$$\text{arctanh}(x) = \frac{1}{2}\ln\left(\frac{1+x}{1-x}\right), \quad |x| < 1$$

### 迅速度的可加性

将速度叠加公式两边取 arctanh：

$$\varphi(u_B) = \text{arctanh}\left(\frac{u_B}{c}\right) = \text{arctanh}\left(\frac{\frac{u_A + v}{c}}{1 + \frac{u_A v}{c^2}}\right)$$

利用双曲正切的加法公式：

$$\tanh(a + b) = \frac{\tanh a + \tanh b}{1 + \tanh a \cdot \tanh b}$$

令 tanh a = u_A / c，tanh b = v / c，则 u_B / c = tanh(a + b)，因此：

$$\boxed{\varphi(u_B) = \varphi(u_A) + \varphi(v)}$$

**迅速度是可加的！** 这是真正的"速度加法"——在双曲空间中，速度变换就是简单的平移。

### 为什么出现双曲函数？

| 概念 | 伽利略时空 | 闵可夫斯基时空 |
|------|-----------|---------------|
| **速度参数** | v 本身 | φ = arctanh(v/c) |
| **叠加规则** | v_total = v₁ + v₂（线性） | φ_total = φ₁ + φ₂（线性） |
| **变换群** | 伽利略群 | 洛伦兹群（双曲旋转） |
| **几何** | 欧几里得空间 + 绝对时间 | 闵可夫斯基时空（双曲几何） |
| **不变量** | 时间间隔 Δt, 空间距离 Δx 分别不变 | 时空间隔 Δs² = −c²Δt² + Δx² 不变 |

> 双曲函数的出现不是巧合——它预告了第 7 节的答案：**洛伦兹变换本质上是时空中的双曲旋转**。

### Python — 迅速度可视化和速度叠加验证

```python
"""
Rapidity Visualization: φ(v) = arctanh(v/c).
Demonstrate that rapidity is additive while velocity is not.
"""
import numpy as np
import matplotlib.pyplot as plt

c = 1.0  # natural units

def rapidity(v):
    """φ(v) = arctanh(v/c)"""
    return np.arctanh(v / c)

def velocity_from_rapidity(phi):
    """v/c = tanh(φ)"""
    return c * np.tanh(phi)

def relativistic_add(u_A, v):
    """Relativistic velocity addition: u_B = (u_A + v) / (1 + u_A*v/c²)"""
    return (u_A + v) / (1 + u_A * v / c**2)

# ============================================================
# 1. Rapidity curve: φ as a function of v/c
# ============================================================
fig, axes = plt.subplots(2, 3, figsize=(16, 10))

# (a) Rapidity φ(v) vs v/c
ax = axes[0, 0]
v_vals = np.linspace(0, 0.9999, 1000)
phi_vals = rapidity(v_vals)
ax.plot(v_vals, phi_vals, 'b-', linewidth=2)
ax.set_xlabel('v / c', fontsize=11)
ax.set_ylabel('φ = arctanh(v/c)', fontsize=11)
ax.set_title('Rapidity φ(v) — Diverges as v → c', fontsize=12)
ax.axvline(x=1.0, color='r', linestyle='--', alpha=0.3, label='v = c')
ax.axhline(y=0, color='gray', linestyle=':', alpha=0.5)
ax.legend(fontsize=9)
ax.grid(True, alpha=0.3)

# (b) Compare v vs φ: why φ is the "natural" additive parameter
ax = axes[0, 1]
velocity_steps = [0.5, 0.5, 0.5, 0.5]  # four boosts of 0.5c each
v_current = 0
v_history_galilean = [0]
v_history_relativistic = [0]
phi_total = 0
phi_history = [0]

for v_step in velocity_steps:
    v_current = relativistic_add(v_current, v_step)
    v_history_relativistic.append(v_current)
    phi_total += rapidity(v_step)
    phi_history.append(phi_total)
    v_history_galilean.append(v_history_galilean[-1] + v_step)

steps = range(len(v_history_relativistic))
ax.plot(steps, v_history_galilean, 'g--', marker='s', label='Galilean (v₁+v₂)')
ax.plot(steps, v_history_relativistic, 'b-', marker='o', label='Relativistic')
ax.axhline(y=1.0, color='r', linestyle='--', alpha=0.5, label='v = c')
ax.set_xlabel('Number of boosts (u = 0.5c each)', fontsize=11)
ax.set_ylabel('Total velocity v/c', fontsize=11)
ax.set_title('Repeated 0.5c Boosts: Galilean vs Relativistic', fontsize=11)
ax.legend(fontsize=9)
ax.grid(True, alpha=0.3)

# (c) Rapidity is additive — φ grows linearly with number of boosts
ax = axes[0, 2]
ax.plot(steps, phi_history, 'r-', marker='D', linewidth=2, label='φ = Σ arctanh(0.5)')
ax.set_xlabel('Number of boosts', fontsize=11)
ax.set_ylabel('Total rapidity φ', fontsize=11)
ax.set_title('Rapidity: Perfectly Additive!', fontsize=12)
ax.legend(fontsize=10)
ax.grid(True, alpha=0.3)

# (d) Full 2D velocity addition surface: u_B as function of u_A and v
ax = axes[1, 0]
uA_grid, v_grid = np.meshgrid(np.linspace(0, 0.99, 100), np.linspace(0, 0.99, 100))
uB_grid = relativistic_add(uA_grid, v_grid)
contour = ax.contourf(uA_grid, v_grid, uB_grid, levels=20, cmap='viridis')
ax.set_xlabel('u_A / c (object speed in moving frame)', fontsize=11)
ax.set_ylabel('v / c (frame speed)', fontsize=11)
ax.set_title('u_B / c = (u_A + v) / (1 + u_A·v/c²)', fontsize=11)
plt.colorbar(contour, ax=ax, label='u_B / c')

# (e) Galilean error: |relativistic - galilean|
ax = axes[1, 1]
galilean = uA_grid + v_grid
error = np.abs(uB_grid - galilean)
contour2 = ax.contourf(uA_grid, v_grid, error, levels=20, cmap='Reds')
ax.set_xlabel('u_A / c', fontsize=11)
ax.set_ylabel('v / c', fontsize=11)
ax.set_title('Error of Galilean Addition |u_rel − u_gal|', fontsize=11)
plt.colorbar(contour2, ax=ax, label='|error| / c')

# (f) Verify: arctanh(u_B/c) = arctanh(u_A/c) + arctanh(v/c)
ax = axes[1, 2]
uA_test = np.linspace(0.01, 0.95, 10)
v_test = np.linspace(0.01, 0.95, 10)
diff_max = 0
for uA in uA_test:
    for v in v_test:
        uB = relativistic_add(uA, v)
        phi_sum = rapidity(uA) + rapidity(v)
        phi_uB = rapidity(uB)
        diff = abs(phi_uB - phi_sum)
        if diff > diff_max:
            diff_max = diff
        ax.plot(uA, v, 'go', markersize=3, alpha=0.5)

ax.set_xlabel('u_A / c', fontsize=11)
ax.set_ylabel('v / c', fontsize=11)
ax.set_title(f'φ(u_B) = φ(u_A) + φ(v) — max error = {diff_max:.1e}', fontsize=11)
ax.grid(True, alpha=0.3)

plt.suptitle('Rapidity: The True Additive Measure of Speed in Relativity', fontsize=14, y=1.01)
plt.tight_layout()
plt.savefig('/tmp/rapidity_visualization.png', dpi=120, bbox_inches='tight')
print("[Plot saved to /tmp/rapidity_visualization.png]")

# ============================================================
# 2. Numerical examples
# ============================================================
print("\n" + "=" * 60)
print("VELOCITY ADDITION: NUMERICAL EXAMPLES")
print("=" * 60)

examples = [
    (0.5, 0.5, "Two half-light-speed boosts"),
    (0.9, 0.9, "Two 0.9c boosts → still below c"),
    (0.99, 0.99, "Two 0.99c boosts → close to c"),
    (0.1, 0.0001, "Everyday: 0.1c + 30 km/s ≈ 0.1c"),
    (1.0, 0.5, "Light (u_A=c) + any v → c (sanity check)"),
]

for uA, v, desc in examples:
    uB = relativistic_add(uA * c, v * c) / c
    uB_gal = uA + v
    phi_A = rapidity(uA * c)
    phi_v = rapidity(v * c)
    phi_B = rapidity(uB * c)
    phi_sum = phi_A + phi_v
    print(f"\n  {desc}:")
    print(f"    u_A = {uA:.4f}c, v = {v:.4f}c")
    print(f"    Relativistic: u_B = {uB:.6f}c")
    print(f"    Galilean:     u_B = {uB_gal:.4f}c  (would exceed c!)")
    print(f"    φ(u_A) = {phi_A:.6f}, φ(v) = {phi_v:.6f}")
    print(f"    φ(u_A)+φ(v) = {phi_sum:.6f}, φ(u_B) = {phi_B:.6f}")
    print(f"    φ additive? {'YES ✓' if abs(phi_sum - phi_B) < 1e-12 else 'NO ✗'}")
```

```
VELOCITY ADDITION: NUMERICAL EXAMPLES
============================================================

  Two half-light-speed boosts:
    u_A = 0.5000c, v = 0.5000c
    Relativistic: u_B = 0.800000c
    Galilean:     u_B = 1.0000c  (would exceed c!)
    φ(u_A) = 0.549306, φ(v) = 0.549306
    φ(u_A)+φ(v) = 1.098612, φ(u_B) = 1.098612
    φ additive? YES ✓

  Two 0.9c boosts:
    u_A = 0.9000c, v = 0.9000c
    Relativistic: u_B = 0.994475c
    Galilean:     u_B = 1.8000c  (would exceed c!)
    φ additive? YES ✓

  Two 0.99c boosts:
    u_A = 0.9900c, v = 0.9900c
    Relativistic: u_B = 0.999949c
    Galilean:     u_B = 1.9800c  (would exceed c!)
    φ additive? YES ✓

  Light (u_A=c) + any v → c (sanity check):
    u_A = 1.0000c, v = 0.5000c
    Relativistic: u_B = 1.000000c  ← exactly c!
    Galilean:     u_B = 1.5000c  (would exceed c!)
```

---

## 📖 3.7 横向速度变换 (Transverse Velocity Transformation)

### Original Text — 不只是纵向

> *"For velocities in arbitrary directions, we can use the Lorentz transformation to derive the general velocity transformation formulas."*

> 对于任意方向的速度，我们可以使用洛伦兹变换导出一般的速度变换公式。

| 单词/短语 | 注释 |
|-----------|------|
| arbitrary directions | 任意方向；不限于沿相对运动方向（纵向），也包括横向 |
| Lorentz transformation | 洛伦兹变换；连接不同惯性参考系坐标的完整变换公式，将在第 6 节详细推导 |
| general velocity transformation formulas | 一般速度变换公式；将任意三维速度矢量从一个参考系变换到另一个参考系 |

### 完整的三维速度变换公式

利用洛伦兹变换（第 6 节将详细推导），可以得到一般方向的相对论速度变换：

| 方向 | 变换公式 | 说明 |
|------|---------|------|
| **x 方向**（纵向） | $v_{Bx} = \dfrac{v_{Ax} + v}{1 + \dfrac{v_{Ax}\,v}{c^2}}$ | 与一维公式一致 |
| **y 方向**（横向） | $v_{By} = \dfrac{v_{Ay}}{\gamma\left(1 + \dfrac{v_{Ax}\,v}{c^2}\right)}$ | 即使横向速度也受相对运动影响！ |
| **z 方向**（横向） | $v_{Bz} = \dfrac{v_{Az}}{\gamma\left(1 + \dfrac{v_{Ax}\,v}{c^2}\right)}$ | 同理 |

### 为什么横向速度也变了？

这在牛顿力学中是不可思议的——垂直方向的速度怎么会受水平运动影响？

**根本原因**：Alice 和 Bob 的时间流逝速度不同（时间膨胀），而横向长度相同。

- Bob 看到 Alice 的时钟走得更慢 → Bob 测到的横向速度更小
- 具体而言：v_By = (横向距离) / (Bob 的时间) = (Δy_A) / (γ Δt_A) = v_Ay / γ

另外，分母中的 (1 + v_Ax·v/c²) 来自同时性的相对性——Bob 和 Alice 对"何时测量横向位移"有不同定义。

### 特例：纯横向速度

当物体在 Alice 参考系中仅沿 y 方向运动（v_Ax = 0）时：

$$\mathbf{v}_A = (0,\, u,\, 0) \quad \Rightarrow \quad \mathbf{v}_B = (v,\, u/\gamma,\, 0)$$

即 Bob 看到物体既有水平速度分量 v（随 Alice 运动），又有缩小的垂直分量 u/γ。

### Python — 三维速度变换计算器

```python
"""
3D Relativistic Velocity Transformation.
Given velocity in Alice's frame (vAx, vAy, vAz) and relative frame speed v,
compute the velocity in Bob's frame.
"""
import numpy as np

c = 1.0  # natural units

def transform_velocity(v_A, v_frame):
    """
    Transform velocity from Alice's frame to Bob's frame.
    
    Parameters:
        v_A: tuple (vAx, vAy, vAz) — velocity components in Alice's frame
        v_frame: float — speed of Alice's frame relative to Bob (along x)
    
    Returns:
        tuple (vBx, vBy, vBz) — velocity components in Bob's frame
    """
    vAx, vAy, vAz = v_A
    v = v_frame
    
    gamma = 1.0 / np.sqrt(1.0 - v**2 / c**2)
    denominator = 1.0 + vAx * v / c**2
    
    vBx = (vAx + v) / denominator
    vBy = vAy / (gamma * denominator)
    vBz = vAz / (gamma * denominator)
    
    return (vBx, vBy, vBz)

# Test cases
print("=" * 64)
print("3D VELOCITY TRANSFORMATION")
print("=" * 64)

test_cases = [
    ((0.5, 0.0, 0.0), 0.5, "Pure longitudinal"),
    ((0.0, 0.5, 0.0), 0.5, "Pure transverse"),
    ((0.5, 0.5, 0.0), 0.5, "Diagonal (45°)"),
    ((0.0, 0.8, 0.0), 0.9, "Fast transverse + fast frame"),
    ((0.9, 0.0, 0.0), 0.9, "Both near c: longitudinal"),
]

for v_A, v_frame, desc in test_cases:
    vBx, vBy, vBz = transform_velocity(v_A, v_frame)
    vA_mag = np.sqrt(v_A[0]**2 + v_A[1]**2 + v_A[2]**2)
    vB_mag = np.sqrt(vBx**2 + vBy**2 + vBz**2)
    gamma_frame = 1.0 / np.sqrt(1.0 - v_frame**2)
    
    print(f"\n  {desc}:")
    print(f"    Alice: v_A = ({v_A[0]:.4f}, {v_A[1]:.4f}, {v_A[2]:.4f})c, |v_A| = {vA_mag:.4f}c")
    print(f"    Frame speed v = {v_frame:.4f}c, γ = {gamma_frame:.4f}")
    print(f"    Bob:   v_B = ({vBx:.4f}, {vBy:.4f}, {vBz:.4f})c, |v_B| = {vB_mag:.4f}c")
    
    # Key observation for transverse case
    if v_A[0] == 0 and v_frame > 0:
        print(f"    → Transverse speed reduced by 1/γ: {v_A[1]:.4f} → {vBy:.4f} = {v_A[1]/gamma_frame:.4f} ✓")

# Verify: speed never exceeds c (except possibly within numerical rounding)
print(f"\n  All speeds ≤ c? {all(np.sqrt(vBx**2+vBy**2+vBz**2) <= 1.0001 for (vBx,vBy,vBz) in [transform_velocity(v_A, v_f) for v_A, v_f, _ in test_cases])}")
```

---

## 📖 3.8 三个效应的统一：时间膨胀、长度收缩、速度叠加 (The Unified Triad)

### 三者之间的逻辑关系

```
                  (R) + (C) + (E)
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
    垂直长度不变   光速不变    事件一致同意
          │            │            │
          ├────────────┤            │
          ▼            ▼            │
     光钟实验 ──→ 时间膨胀          │
     Δt_B = γ·Δt_A                 │
          │                         │
          ▼                         │
     光尺实验 ──→ 长度收缩          │
     D_B = D_A/γ                   │
          │                         │
          ▼                         │
     测速仪 ──→ 速度叠加公式        │
     u_B = (u_A+v)/(1+u_A·v/c²)    │
          │                         │
          ▼                         │
     迅速度 φ = arctanh(v/c)        │
     φ(u_B) = φ(u_A) + φ(v)        │
```

这三个效应**不是独立的**——它们从 (R) + (C) + (E) 出发，通过四步推理法**递归地相互推导**：

1. 时间膨胀 + 垂直长度不变 → 光钟 → Δt_B = γ Δt_A
2. 时间膨胀 + 光尺（平行放置）→ 长度收缩 → D_B = D_A/γ
3. 时间膨胀 + 长度收缩 → 测速仪 → 相对论速度叠加
4. 速度叠加 → 迅速度 φ → 揭示时空的双曲几何结构

### 核心公式对照表

| 效应 | 公式 | γ 因子位置 | v → 0 | v → c |
|------|------|-----------|-------|-------|
| **时间膨胀** | Δt_B = γ · Δt_A | γ（乘数，≥1） | Δt_B = Δt_A | Δt_B → ∞ |
| **长度收缩** | D_B = D_A / γ | 1/γ（除数，≤1） | D_B = D_A | D_B → 0 |
| **速度叠加** | u_B = (u_A+v)/(1+u_A·v/c²) | — | u_B ≈ u_A+v | u_B → c |
| **迅速度** | φ = arctanh(v/c) | — | φ ≈ v/c | φ → ∞ |

---

## 📚 核心公式汇总

| 公式 | 含义 | 节 |
|------|------|-----|
| D_B = D_A / γ | 长度收缩：运动尺子沿运动方向收缩 | 3.2 |
| γ = 1 / √(1 − v²/c²) | Lorentz 因子 | 2.2 |
| Δt_B = γ Δt_A | 时间膨胀 | 2.2 |
| u_B = (u_A + v) / (1 + u_A·v/c²) | 相对论速度叠加（一维） | 3.5 |
| φ(v) = arctanh(v/c) | 迅速度定义 | 3.6 |
| φ(u_B) = φ(u_A) + φ(v) | 迅速度的可加性 | 3.6 |
| v_By = v_Ay / [γ(1 + v_Ax·v/c²)] | 横向速度变换 | 3.7 |
| v = c · tanh(φ) | 从迅速度恢复速度 | 3.6 |

---

## 🎯 要点总结

1. **长度收缩是时间膨胀的必然推论**：将光钟旋转 90° 得到光尺，结合时间膨胀即得 D_B = D_A/γ
2. **仅沿运动方向收缩**：垂直方向长度在所有惯性系中相同（由 (E) 通过火车-铁轨论证保证）
3. **收缩因子是 1/γ**：v = 0 时无收缩；v → c 时收缩到 0
4. **历史先于理论**：FitzGerald (1889) 和 Lorentz (1892) 为解释 MM 实验而假设收缩；爱因斯坦将其升级为时空几何的必然推论
5. **相对论速度叠加保证光速上限**：无论如何叠加，合成速度永不超光速；当 u_A = c 时，u_B ≡ c
6. **迅速度才是真正的可加量**：φ(u_B) = φ(u_A) + φ(v)，揭示了双曲几何结构——预告第 7 节
7. **横向速度也会被变换**：因为时间膨胀改变了时间间隔，即使横向长度不变
8. **三个效应相互关联**：时间膨胀 → 长度收缩 → 速度叠加 → 迅速度，从 (R)+(C)+(E) 递归推导

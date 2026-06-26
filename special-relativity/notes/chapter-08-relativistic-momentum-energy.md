# 第八节：相对论动量与能量（Relativistic Momentum & Energy）

## 📖 8.0 原文精读：为什么需要守恒律？

### 守恒律的三大好处

讲义在这一节的开头并没有直接跳入公式，而是花了相当篇幅论述**为什么守恒律如此重要**——这是一个容易被忽视但极其根本的问题。

| 层面 | 解释 | 举例 |
|------|------|------|
| **物理上** | 守恒律是"魔法"：不需要关心中间过程，给定初态即可做出多个预言 | 两个粒子碰撞，不管碰撞细节，动量守恒直接约束末态 |
| **数学上** | 运动方程是二阶常微分方程（mẍ + V' = 0），很难解；守恒律将其中一些降为一阶甚至零阶方程 | ½mẋ² + V = E 比 mẍ = -V' 容易处理得多 |
| **实践上** | 现代物理研究的对象往往极快（v ~ c）、极小（ΔxΔp ~ ℏ）、极重（GM/(rc²) ~ 1）、极早（大爆炸后不到一秒），无法直接监控过程细节 | LHC 上粒子碰撞后的轨迹在远晚于相互作用的时间才被研究；若没有能量/动量守恒，甚至无法定义可观测量 |

### 为什么狭义相对论中仍幸运地有守恒律？

讲义预告了一个更深刻的答案（将在"从作用量到自然定律"部分展开）：守恒律的存在**不是运气**，而是**没有任何时刻、没有任何空间位置特殊**这一事实的必然结果。这个论证在牛顿力学和狭义相对论中同样成立。

### 🔑 关键词汇

| English | 中文 | 说明 |
|---------|------|------|
| **conservation law** | 守恒律 | 某些物理量在时间演化中保持不变的定律 |
| **proper time (dτ)** | 原时 | 运动物体自身时钟测量的时间间隔，dτ = dt/γ |
| **observer-independent** | 观察者无关的 | 在所有惯性系中取相同值的量 |
| **relativistic momentum** | 相对论动量 | p = γmv，用原时而非坐标时来定义 |
| **relativistic energy** | 相对论能量 | E = γmc²，包含静止能量和动能 |
| **rest energy** | 静止能量 | E₀ = mc²，物体即使静止也具有的能量 |
| **4-momentum** | 四维动量 | p^μ = (E/c, p)，将能量和动量统一为一个四矢量 |
| **invariant mass** | 不变质量 | m²c⁴ = E² - p²c²，洛伦兹不变量 |
| **mass defect** | 质量亏损 | 系统总质量小于各组分质量之和，差值对应结合能 |

---

## 📖 8.1 牛顿动量在相对论中为何失效？

### 问题设定

Alice 和 Bob 有相对速度 v（沿 x 方向）。Alice 观察到两个粒子的动量守恒：

```
m₁vᴀ₁ + m₂vᴀ₂ = m₁v'ᴀ₁ + m₂v'ᴀ₂    （在 Alice 系中）
```

**问题**：这一方程在 Bob 的参考系中是否保持相同的形式？

### 牛顿情形（v ≪ c）

在牛顿力学中：质量不变，速度简单相加（vʙ₁ = vᴀ₁ + v）。于是：

```
m₁vʙ₁ + m₂vʙ₂ = m₁(vᴀ₁+v) + m₂(vᴀ₂+v)
                = (m₁vᴀ₁+m₂vᴀ₂) + (m₁+m₂)v
                = m₁v'ʙ₁ + m₂v'ʙ₂    ← 所有含 v 的项刚好消去！
```

**结论**：在牛顿力学中，动量守恒的形式在所有惯性系中一致——(R) 成立。

### 相对论情形（v ~ c）

使用相对论速度叠加公式。在 x 方向：

```
m₁ · (vᴀ₁ₓ + v) / (1 + vᴀ₁ₓ·v/c²) + ... = m₁ · (v'ᴀ₁ₓ + v) / (1 + v'ᴀ₁ₓ·v/c²) + ...
```

在 y 方向：

```
m₁ · vᴀ₁y / [γ(1 + vᴀ₁ₓ·v/c²)] + ... = m₁ · v'ᴀ₁y / [γ(1 + v'ᴀ₁ₓ·v/c²)] + ...
```

**红色因子**（1 + vᴀ₁ₓ·v/c²）的出现使得方程不再具有与 Alice 系中相同的形式。

> **不幸的结论**：牛顿的动量定义在狭义相对论中不是守恒量——它不是一条自然定律！

---

## 8.2 用原时修复动量守恒

### 问题的根源：坐标时依赖于观察者

红色因子的来源是时间膨胀：

```
dtB = d[γ(tA + xA·v/c²)] = γ(1 + v₁ₐₓ·v/c²) dtA
```

每个观察者都有自己的时间。**用观察者自己的时间来度量运动**（d(…)/dtA 和 d(…)/dtB）是万恶之源。

### 解决方案：原时（Proper Time）

我们需要一个**观察者无关**的时间度量。第 7 节已经给出了答案——用 ds² 来定义：

```
dτ ≡ √(-ds²/c²) = √(dt² - dx²/c²) = dt/γ
```

- dτ 是**运动物体自身携带的时钟**测量的时间
- 在物体自身的静止系中，dx = 0，所以 dτ = dt——这验证了 dτ 就是"物体自身测量的时间"
- dτ 在洛伦兹变换下**不变**

### 🔑 关键词汇：原时（Proper Time）

**原时**是狭义相对论中最核心的概念之一。它不是"绝对的宇宙时间"，而是**由运动物体自身定义的、独立于任何外部观察者的时间度量**。想象一个与物体一起运动的时钟——原时就是这个时钟的读数间隔。

### 相对论动量的定义

用原时取代坐标时来定义动量：

```
p = m · dx/dτ = γ m v
```

| 观察方式 | 动量定义 | 变换性质 | 是否适用 |
|----------|---------|---------|---------|
| 坐标时 | p = m·dx/dt | 依赖观察者 | ❌ 牛顿力学 |
| **原时** | **p = m·dx/dτ** | **洛伦兹不变量** | **✅ 狭义相对论** |

从 p = m·dx/dτ 的第一个等号可以直接看出：**p 在洛伦兹变换下与 x 的变换方式相同**——这正是我们需要的：动量守恒在不同参考系中保持相同形式。

### 低速极限

当 v ≪ c 时，γ ≈ 1，p ≈ mv —— 回到牛顿动量的形式。这是对定义正确性的一个基本检验。

---

## 📖 8.3 相对论力：为什么 c 是终极速度极限？

### 力的定义

有了相对论动量，自然可以定义力：

```
F ≡ dp/dt = d(γmv)/dt = γ m v̇ + γ³ m v(v·v̇)/c²
```

> **注意**：这里用 dt 而非 dτ，因为这样更直观——想象一个静止的观察者推一个物体并观察它的加速度，力代表这个静止观察者需要额外付出多少努力。

### 关键物理后果：F → ∞ 当 v → c

- 当物体接近光速时，**需要无穷大的力才能进一步加速它**
- c 不仅是一个速度极限——它是**一个不可逾越的屏障**
- 任何亚光速物体都**永远不可能被加速到光速或超过光速**

### 追光之梦的终结

> 爱因斯坦 16 岁时开始梦想：如果他能跑得和光一样快会发生什么？光是否会停止振荡？这是否会与麦克斯韦电磁理论矛盾？
>
> 狭义相对论给出了答案：**没有人能被加速到光速**。这个看似矛盾的思想实验永远不会发生。爱因斯坦的"追光之梦"就此终结——但这终结本身，却催生了物理学最深刻的理论之一。

---

## 📖 8.4 质量不再守恒！

### 弹簧分裂实验

考虑一个由压缩弹簧连接的系统：

1. **初始状态**：系统总质量 M，两个物体（各质量 m）由压缩弹簧连接，**系统整体静止**
2. **释放弹簧后**：两个物体以速度 v 向相反方向运动
3. **牛顿力学的预言**：M = 2m（质量守恒）

**在相对论中这还成立吗？**

### 动量守恒揭示的真相

为了分析系统性质，在 y 方向加一个微小的探测速度 vy ≪ v（可取为无穷小）：

- **分裂前**：py = M·vy
- **分裂后**：py = 2γm·vy（两个物体各贡献 γm·vy）

由动量守恒：**M = 2γm > 2m**！

### 🔑 关键词汇：质量亏损与能量释放

| 概念 | 含义 | 实例 |
|------|------|------|
| **质量不守恒** | 系统总质量不等于各组分静止质量之和 | 弹簧分裂：M > 2m |
| **束缚能对应质量** | 势能、动能等所有形式的能量都贡献质量 | 压缩弹簧的势能 → M 的增加 |
| **质量-能量统一** | 质量守恒和能量守恒不再是独立的定律 | E = mc² 将它们统一 |

---

## 📖 8.5 相对论动能与静止能量

### 从力到动能

力做功转化为动能。考虑一个初始静止在 x = 0 的物体，被 x 方向的力加速到位置 x、速度 v：

```
K = ∫₀ˣ F dx = ∫₀ˣ d(γmv)/dt · dx = ∫₀ᵛ v d(γmv) = (γ - 1)mc²
```

积分过程中将变量换为 v，最后一步使用了分部积分。

### 低速展开：回到牛顿

当 v ≪ c 时，做泰勒展开：

```
K = (γ - 1)mc² = [1/√(1 - v²/c²) - 1] mc²
  ≈ [1 + ½(v²/c²) + ⅜(v⁴/c⁴) + ... - 1] mc²
  = ½ mv² + ⅜ mv⁴/c² + ...
```

- 第一项：**½mv²** —— 熟悉的牛顿动能
- 后续项：相对论修正（v ≪ c 时可忽略）

### 静止能量：E = mc²

在弹簧分裂实验中，取极限 γ ≫ 1（末态物体接近光速），末态动能 K ≈ 2γmc²，而末态两个物体的静止能量（各 mc²）可以忽略。由能量守恒：

```
E_initial = 2γmc² = Mc²
```

初始物体是静止的——这里的能量就是**静止能量**：

```
E_rest = mc²
```

### E = mc² 的两层含义

| 含义 | 公式 | 说明 |
|------|------|------|
| **静止能量** | E₀ = mc² | 物体即使在静止时也具有的能量——因为 c 在日常尺度上是巨大的数，这个能量也极其巨大 |
| **总能量** | E = γmc² | 物体运动时的总能量 = 静止能量 + 动能 |

### 日常生活的震撼对比

- **香港每日能源消耗**：约 10¹⁵ J
- **对应多少物质？**：约 10 克 —— 大约一节 AAA 电池的重量！
- **一节 AAA 电池的化学能**：几千焦耳

> 这就是 E = mc² 的威力：物质中蕴含的能量远超日常经验中的化学或机械能量尺度。

### 为什么星星会发光？

在相对论被理解之前，有一个巨大的谜团：如果恒星由化学能驱动，它们怎么可能燃烧得比人类历史还长？答案是**核聚变**——恒星利用物质静止能量的一小部分，就可以发光数十亿年。

### 静止能量的零点校验

粒子-反粒子湮灭现象是对静止能量概念的一个**极其重要的检验**：粒子和反粒子相遇后完全消失，其**全部静止能量**以光的形式释放——能量的零点必须有物理意义，而它确实有。

---

## 📖 8.6 总能量与四维动量

### 回到那个"天真"的类比

回忆 8.2 节：动量是 4-矢量中与空间对应的部分：p = m·dx/dτ = γmv。那么，如果把 x 换成 ct 会得到什么？

```
(naive 的时间分量) = m·d(ct)/dτ = γmc
```

**自然不应留它空着！** 这就是：

```
E/c = γmc    →    E = γmc²
```

### 四维动量（4-Momentum）

| 分量 | 物理量 | 表达式 | 变换性质 |
|------|--------|--------|---------|
| **p⁰** | E/c（能量/光速） | γmc | 与 ct 相同 |
| **p¹** | px（x 方向动量） | γmvx | 与 x 相同 |
| **p²** | py（y 方向动量） | γmvy | 与 y 相同 |
| **p³** | pz（z 方向动量） | γmvz | 与 z 相同 |

**4-动量 p^μ = (E/c, p) = (γmc, γmv) = γm·ẋ^μ 是一个统一的洛伦兹 4-矢量！**

能量和动量不再是两个独立的概念——它们是同一个四维实体在不同"方向"上的投影，正如空间和时间统一于时空一样。

### 不变质量：能量-动量关系

四维坐标有不变量 -c²t² + x² + y² + z²。四维动量也有对应的不变量：

由 E = γmc² 和 p = γmv，两边平方并相减：

```
E² - p²c² = γ²m²c⁴ - γ²m²v²c²
           = γ²m²c⁴(1 - v²/c²)
           = γ²m²c⁴/γ²
           = m²c⁴
```

即：

```
m²c⁴ = E² - p²c²     （或用"自然单位" c = 1：m² = E² - p²）
```

**这是相对论中最美的公式之一。**

| 公式 | 含义 |
|------|------|
| E² = m²c⁴ + p²c² | 能量-动量-质量三者的完整关系 |
| m²c⁴ = E² - p²c² | 质量是 4-动量的"长度"（洛伦兹不变量的平方根） |

- 虽然 E 和 p 各自依赖于观察者，但 **m²c⁴ = E² - p²c² 这个组合是洛伦兹不变量**——它是粒子本身的性质
- 这就像在三维空间中，坐标矢量的长度 x²+y²+z² 在旋转下不变一样自然

### 🔑 关键词汇：不变质量 vs 相对论质量

| 概念 | 公式 | 性质 | 是否常用 |
|------|------|------|---------|
| **不变质量 m** | m²c⁴ = E² - p²c² | 洛伦兹不变量，粒子的内在属性 | ✅ 现代标准 |
| **相对论质量 m_rel** | m_rel = γm | 依赖速度，E = m_rel c² | ❌ 已少用 |

---

## 8.7 光是光（Light is Light）

### 零质量粒子

将能量-动量关系应用于光：

- 光速 v = c
- 若质量 m > 0，则 γ 发散，p 和 E 都发散——不可能
- **唯一自洽的解：m = 0**

> 如果我们把光看作粒子（光子），其质量必须为零。

### 光的四维动量

对于 m = 0 的粒子：

```
p^μ = (E/c, p)   其中 E = c|p|
```

这个四维动量的洛伦兹范数为零：gμν p^μ p^ν = 0。第 7 节中定义的 **null（类光）** 正因此得名——它确实是"零"。

| 属性 | 有质量粒子 | 光子（m=0） |
|------|-----------|------------|
| 4-动量范数 | -m²c² < 0（类时） | 0（类光/null） |
| 速度 | v < c | v = c |
| 能量-动量关系 | E² = m²c⁴ + p²c² | E = c \|p\| |

---

## 📖 8.8 相对论多普勒效应（可选进阶）

### 4-矢量内积方法的威力

Alice 相对 Bob 以速度 v 运动。Bob 观测到一束光的能量为 EB，Alice 观测到同一束光的能量 EA。如何求两者的关系？

用 4-矢量内积的洛伦兹不变性：

**在 Bob 系中**：
- Alice 的 4-动量：k^μ = (γmc, γmv)
- 光束的 4-动量：p^ν = (EB/c, p)
- 内积：gμν k^μ p^ν = -γm(EB - v·p) = **-γm EB (1 - (v/c)cosθ)**
  - 其中 θ 是 Bob 系中 v 与 p 的夹角

**在 Alice 系中**：
- Alice 的 4-动量：k^μ = (mc, 0)（Alice 在自己的静止系中）
- 光束的 4-动量：p^ν = (EA/c, p')
- 内积：gμν k^μ p^ν = **-m EA**

由洛伦兹不变性，两式相等：

```
EA = γ EB (1 - (v/c) cosθ)
```

### 频率形式

由经典电磁学或量子力学可知，光频率 ω ∝ E。因此：

```
ωA = γ ωB (1 - (v/c) cosθ)
```

> **讲义强调**：这个可选框的目的不仅是给出相对论多普勒效应公式，更是展示**4-矢量内积洛伦兹不变性方法的威力**。多普勒效应也可以从时间膨胀和长度收缩直接推导，但对于一般的 θ 方向，计算将**复杂得多**。用 4-矢量内积，几行就得到精确结果。

---

## 💻 8.9 Python 代码示例

### 示例 1：E = mc² 计算器

```python
"""
E = mc² 能量计算器
演示物质中蕴含的巨大能量
"""
import numpy as np

c = 2.99792458e8  # 光速，m/s

def rest_energy(mass_kg):
    """计算静止能量（焦耳）"""
    return mass_kg * c**2

def total_energy(mass_kg, v):
    """计算相对论总能量 E = γmc²"""
    beta = v / c
    gamma = 1.0 / np.sqrt(1.0 - beta**2)
    return gamma * mass_kg * c**2

def kinetic_energy(mass_kg, v):
    """计算相对论动能 K = (γ-1)mc²"""
    return total_energy(mass_kg, v) - rest_energy(mass_kg)

# --- 演示：1 克物质的静止能量 ---
mass_1g = 0.001  # kg
E_1g = rest_energy(mass_1g)

print("=" * 60)
print("       E = mc²  能  量  计  算  器")
print("=" * 60)
print(f"\n1 克物质的静止能量:")
print(f"  {E_1g:.2e} J")
print(f"  ≈ {E_1g/3.6e6:.2e} kWh")
print(f"  ≈ {E_1g/4.184e9:.2e} 吨 TNT 当量")

# 对比：香港日能耗约 10^15 J
hk_daily = 1e15
print(f"\n香港每日能源消耗 ≈ {hk_daily:.0e} J")
print(f"等效物质质量 ≈ {hk_daily/c**2 * 1000:.1f} 克")
print(f"  （大约一节 AAA 电池的重量！）")

# --- 演示：动能的速度依赖 ---
print(f"\n{'速度 (v/c)':<14} {'γ':<10} {'K (J)':<18} {'K_Newton (J)':<18} {'比值':<10}")
print("-" * 70)
for beta in [0.01, 0.1, 0.5, 0.9, 0.99, 0.999]:
    v = beta * c
    gamma = 1.0 / np.sqrt(1.0 - beta**2)
    K_rel = kinetic_energy(mass_1g, v)
    K_newton = 0.5 * mass_1g * v**2
    ratio = K_rel / K_newton if K_newton > 0 else float('inf')
    print(f"  {beta:<12.3f}  {gamma:<8.4f}  {K_rel:<16.2e}  {K_newton:<16.2e}  {ratio:<8.2f}")

print(f"\n结论：v ≪ c 时，相对论动能 → 牛顿动能 ½mv²")
print(f"      v → c 时，动能发散——需要无穷大能量才能达到光速")

# --- 演示：静止能量的来源分解 ---
print(f"\n{'='*60}")
print(f"      质  量  亏  损  示  例")
print(f"{'='*60}")

# 氘核质量亏损（实际物理数据）
m_proton  = 1.67262192e-27   # kg
m_neutron = 1.67492749e-27   # kg
m_deuteron = 3.34358377e-27  # kg（氘核）

mass_defect = (m_proton + m_neutron) - m_deuteron
binding_energy = mass_defect * c**2
binding_energy_MeV = binding_energy / 1.602176634e-13  # J → MeV

print(f"\n氘核（质子 + 中子 → ²H）:")
print(f"  质子质量:        {m_proton:.4e} kg")
print(f"  中子质量:        {m_neutron:.4e} kg")
print(f"  组分总质量:      {(m_proton+m_neutron):.4e} kg")
print(f"  氘核实际质量:    {m_deuteron:.4e} kg")
print(f"  质量亏损:        {mass_defect:.4e} kg")
print(f"  结合能:          {binding_energy_MeV:.2f} MeV")
print(f"  （实验值约 2.225 MeV）")
print(f"\n质量亏损 = 结合能/c² —— E = mc² 的直接验证！")
```

### 示例 2：四维动量不变性检验

```python
"""
四维动量不变性检验
验证 E² - p²c² 在洛伦兹变换下保持不变
"""
import numpy as np

c = 1.0  # 使用自然单位

def lorentz_boost(E, px, py, pz, v):
    """对 4-动量做沿 x 方向的洛伦兹 boost（速度 v）"""
    beta = v / c
    gamma = 1.0 / np.sqrt(1.0 - beta**2)

    E_new  = gamma * (E - beta * px)
    px_new = gamma * (px - beta * E)
    py_new = py
    pz_new = pz

    return E_new, px_new, py_new, pz_new

def invariant_mass_sq(E, px, py, pz):
    """计算不变质量平方 m² = E² - p²"""
    return E**2 - (px**2 + py**2 + pz**2)

# --- 创建测试粒子 ---
m = 1.0   # 质量（自然单位）
v_particle = 0.6  # 粒子在 Alice 系中的速度（沿 x 方向）

gamma_p = 1.0 / np.sqrt(1.0 - v_particle**2)
E_A  = gamma_p * m
px_A = gamma_p * m * v_particle
py_A = 0.0
pz_A = 0.0

print("=" * 65)
print("    四 维 动 量 不 变 性 检 验")
print("    E² - p²c² = m²c⁴ = constant")
print("=" * 65)

m2_original = invariant_mass_sq(E_A, px_A, py_A, pz_A)
print(f"\n在 Alice 系中（粒子速度 v = {v_particle}c）:")
print(f"  4-动量: p^μ = ({E_A:.4f}, {px_A:.4f}, {py_A:.4f}, {pz_A:.4f})")
print(f"  m² = E² - p² = {E_A**2:.4f} - {px_A**2:.4f} = {m2_original:.4f}")

# --- 变换到不同参考系，检验不变性 ---
print(f"\n{'Bob 速度 (v/c)':<16} {'E':<10} {'px':<10} {'py/pz':<10} {'m²':<10} {'一致?':<10}")
print("-" * 65)

all_consistent = True
for v_boost in [0.0, 0.1, 0.3, 0.5, 0.7, 0.9, 0.95, 0.99]:
    E_B, px_B, py_B, pz_B = lorentz_boost(E_A, px_A, py_A, pz_A, v_boost)
    m2_B = invariant_mass_sq(E_B, px_B, py_B, pz_B)
    consistent = np.isclose(m2_B, m2_original, rtol=1e-10)
    if not consistent:
        all_consistent = False
    status = "✅" if consistent else "❌"
    print(f"  {v_boost:<14.2f}  {E_B:<8.4f}  {px_B:<8.4f}  {py_B:<8.4f}   {m2_B:<8.4f}  {status}")

if all_consistent:
    print(f"\n✅ 结论：m² = E² - p²c² 在所有惯性系中保持不变！")
    print(f"   这是洛伦兹不变量的一个直接验证。")
else:
    print(f"\n❌ 不变性被破坏——检查代码。")

# --- 光子（m=0）的不变性 ---
print(f"\n{'='*65}")
print(f"    光  子  (m = 0)  的  不  变  性")
print(f"{'='*65}")

# 在某个参考系中的光子 4-动量
E_photon = 2.0  # 任意能量
px_photon = E_photon  # 沿 x 方向，|p| = E
py_photon = 0.0
pz_photon = 0.0

m2_photon_original = invariant_mass_sq(E_photon, px_photon, py_photon, pz_photon)
print(f"\n在某个参考系中:")
print(f"  p^μ = ({E_photon}, {px_photon}, 0, 0)")
print(f"  m² = E² - p² = {E_photon**2} - {px_photon**2} = {m2_photon_original}")
print(f"  光子是 null（类光）4-矢量 — 正如其名！")
```

### 示例 3：牛顿动能 vs 相对论动能 对比

```python
"""
牛顿动能 vs 相对论动能 —— 从低速到近光速的全范围对比
展示相对论动能如何修正牛顿力学的预测
"""
import numpy as np
import matplotlib
matplotlib.use('Agg')  # 非交互式后端
import matplotlib.pyplot as plt

c = 2.99792458e8
m = 1.0  # 取质量 = 1 kg 以便于展示

def gamma(beta):
    return 1.0 / np.sqrt(1.0 - beta**2)

def K_newton(beta):
    """牛顿动能 K = ½ mv²"""
    return 0.5 * m * (beta * c)**2

def K_relativistic(beta):
    """相对论动能 K = (γ - 1)mc²"""
    return (gamma(beta) - 1.0) * m * c**2

# --- 打印表格：全范围对比 ---
betas = [0.001, 0.01, 0.05, 0.1, 0.2, 0.3, 0.4, 0.5,
         0.6, 0.7, 0.8, 0.9, 0.95, 0.99, 0.999, 0.9999]

print("=" * 80)
print("  牛顿动能 vs 相对论动能 — 全速度范围对比  (质量 = 1 kg)")
print("=" * 80)
print(f"{'v/c':<8} {'K_Newton (J)':<18} {'K_Einstein (J)':<18} {'比值 (E/N)':<14} {'γ-1':<12}")
print("-" * 80)

for beta in betas:
    kn = K_newton(beta)
    kr = K_relativistic(beta)
    ratio = kr / kn if kn > 0 else float('inf')
    gm1 = gamma(beta) - 1.0
    marker = " <<<" if ratio > 2.0 else ""
    print(f"  {beta:<6.4f}  {kn:<16.4e}  {kr:<16.4e}  {ratio:<12.4f}  {gm1:<10.6f}{marker}")

# --- 理论分析 ---
print(f"\n{'='*80}")
print("  理  论  分  析")
print(f"{'='*80}")
print(f"""
  低速近似（v ≪ c）:
    γ = 1/√(1 - β²) ≈ 1 + ½β² + ⅜β⁴ + ⁵⁄₁₆β⁶ + ...
    K_rel = (γ - 1)mc² ≈ ½mβ²c² + ⅜mβ⁴c² + ...
          = ½mv² + ⅜mv⁴/c² + ...
          = K_Newton × (1 + ¾β² + ...)

  当 v = 0.1c 时，修正约 0.75%
  当 v = 0.5c 时，修正约 19%
  当 v = 0.9c 时，修正约 129% —— 牛顿力学已完全不适用
  当 v → c  时，K_rel → ∞ —— 光速是终极速度极限
""")

# --- 生成图表 ---
betas_plot = np.linspace(0, 0.999, 500)
K_N = np.array([K_newton(b) for b in betas_plot])
K_R = np.array([K_relativistic(b) for b in betas_plot])

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(13, 5))

# 左图：动能对比
ax1.plot(betas_plot, K_N / 1e16, 'b--', linewidth=1.8, label=r'Newton: $\\frac{1}{2}mv^2$')
ax1.plot(betas_plot, K_R / 1e16, 'r-', linewidth=1.8, label=r'Einstein: $(\\gamma-1)mc^2$')
ax1.axvline(x=0.1, color='gray', linestyle=':', alpha=0.5)
ax1.set_xlabel(r'Speed $v/c$', fontsize=12)
ax1.set_ylabel(r'Kinetic Energy ($10^{16}$ J)', fontsize=12)
ax1.set_title('Newton vs Einstein: Kinetic Energy', fontsize=13, fontweight='bold')
ax1.legend(fontsize=10)
ax1.grid(True, alpha=0.3)
ax1.annotate('v = 0.1c\nNewton OK\n(0.75% error)',
             xy=(0.1, K_newton(0.1)/1e16), xytext=(0.02, 2.5),
             arrowprops=dict(arrowstyle='->', color='gray'),
             fontsize=9, color='gray')
ax1.annotate(r'$v \rightarrow c$' + '\n' + r'$K_{rel} \rightarrow \infty$',
             xy=(0.95, K_R[-100]/1e16), xytext=(0.6, 5),
             arrowprops=dict(arrowstyle='->', color='red'),
             fontsize=9, color='red')

# 右图：比值
ratio_plot = K_R / K_N
ax2.plot(betas_plot, ratio_plot, 'k-', linewidth=2.0)
ax2.axhline(y=1.0, color='gray', linestyle='--', alpha=0.5)
ax2.set_xlabel(r'Speed $v/c$', fontsize=12)
ax2.set_ylabel(r'Ratio $K_{Einstein} / K_{Newton}$', fontsize=12)
ax2.set_title('Ratio of Relativistic to Newtonian Kinetic Energy', fontsize=13, fontweight='bold')
ax2.grid(True, alpha=0.3)
ax2.set_yscale('log')
ax2.annotate('v = 0.1c, ratio ≈ 1.0075',
             xy=(0.1, K_relativistic(0.1)/K_newton(0.1)),
             xytext=(0.1, 0.5),
             arrowprops=dict(arrowstyle='->', color='gray'),
             fontsize=9, color='gray')
ax2.annotate('v = 0.9c\nratio ≈ 2.29',
             xy=(0.9, K_relativistic(0.9)/K_newton(0.9)),
             xytext=(0.55, 6),
             arrowprops=dict(arrowstyle='->', color='red'),
             fontsize=9, color='red')

plt.tight_layout()
plt.savefig('/Users/kunbetter/git/kevin-knowledge-base/special-relativity/notes/kinetic_energy_comparison.png',
            dpi=150, bbox_inches='tight')
print(f"\n图表已保存: kinetic_energy_comparison.png")
plt.close()
```

---

## 关键公式汇总

| 公式 | 含义 | 备注 |
|------|------|------|
| **p = γ m v** | 相对论动量 | 用原时 dτ = dt/γ 定义 |
| **F = dp/dt** | 相对论力 | F → ∞ 当 v → c |
| **K = (γ − 1)mc²** | 相对论动能 | v ≪ c 时 → ½mv² |
| **E_rest = mc²** | 静止能量 | 物质蕴含的巨大能量 |
| **E = γ mc²** | 相对论总能量 | = 静止能量 + 动能 |
| **p^μ = (E/c, p)** | 四维动量 | 统一能量与动量 |
| **m²c⁴ = E² − p²c²** | 能量-动量关系 | 洛伦兹不变量 |
| **E = c\|p\|** | 光子能量-动量关系 | m = 0 时的特殊情况 |
| **ω_A = γ ω_B (1 − (v/c)cosθ)** | 相对论多普勒效应 | 用 4-矢量内积简洁导出 |

---

## 要点总结

1. **牛顿动量在相对论中不守恒**——速度叠加公式中的"红色因子"使得动量守恒在不同参考系中形式不同，违背相对性原理 (R)

2. **修复方案：用原时取代坐标时**——`p = m·dx/dτ = γmv`，原时 dτ 是洛伦兹不变量，确保动量守恒在所有惯性系中形式一致

3. **光速是不可逾越的屏障**——相对论力 F = dp/dt 在 v → c 时发散，任何亚光速物体永远无法被加速到光速或超越光速。爱因斯坦 16 岁的"追光之梦"就此终结

4. **质量不再守恒**——弹簧分裂实验中，M = 2γm > 2m。所有形式的能量（势能、动能……）都贡献质量。质量守恒和能量守恒在相对论中统一

5. **E = mc²：静止能量**——即使静止的物体也具有巨大能量（c² 因子）。香港日能耗 ≈ 10 克物质。恒星核聚变、粒子-反粒子湮灭都是 E = mc² 的直接体现

6. **四维动量统一能量和动量**——`p^μ = (E/c, p) = (γmc, γmv)`，正如空间和时间统一于时空，能量和动量统一于 4-动量

7. **m²c⁴ = E² − p²c² 是洛伦兹不变量**——无论从哪个惯性系观察，这个组合的值都是粒子的内在属性（不变质量）

8. **光是光（Light is light）**——对于光子，m = 0，E = c|p|，4-动量为类光（null）矢量

9. **4-矢量内积方法极其强大**——相对论多普勒效应可以仅用几行推导出一般角度的精确公式，而不用从时间膨胀和长度收缩做复杂的几何计算

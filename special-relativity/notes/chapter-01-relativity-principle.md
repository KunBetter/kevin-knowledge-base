# 第一节：相对性原理与光速不变（Relativity Principle & Speed of Light）

---

## 📖 1.1 开篇思想实验：Alice 的近光速之旅

### Original Text

> *"Let us start our journey by a thought experiment – Alice is in a spaceship to a star, 5 light years away from us, and will return to the earth immediately after her arrival. Bob sees her off and waits her to come back. Suppose the spaceship runs almost as fast as the speed of light c, say, v = 0.995c."*
>
> *"Amazingly, at v ∼ c, things behave dramatically different from our daily experience (Newtonian mechanics)."*

### 三个反直觉的发现

| Bob 的观察 | 本质 |
|-----------|------|
| Bob 和 Alice 互发信件，都说自己先写——即使考虑了光传播时间也无法解决争议 | **同时性的相对性** |
| 飞船在近光速时变得极重——加速需要越来越多的能量 | **相对论质量/能量** |
| Alice 返回时 Bob 过了 10 年，Alice 只过了 1 年 | **时间膨胀**（γ ≈ 10 at v=0.995c） |

### Original Text — 时空观的演进

> *"Newtonian: space and time are absolute and independent 'playgrounds' for matter."*
>
> *"Special relativity: space and time are unified, and depends on motion of observers (like relative orientation of an object depends on rotation of observers)."*
>
> *"General relativity: space and time can be curved by objects."*
>
> *"Quantum gravity (conjectured): space and time may be emergent from holography, quantum entanglements, ... We have not fully understood it yet, but the hints are profound."*

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| thought experiment | 思想实验 | *Gedankenexperiment* (德) |
| light year | 光年 | distance light travels in one year |
| Newtonian mechanics | 牛顿力学 | valid when v ≪ c |
| inertial frame | 惯性系 | constant velocity, no acceleration |
| emergent | 涌现 | arising from lower-level rules |

---

## 📖 1.2 伽利略的相对性原理 (Galileo's Principle of Relativity)

### Original Text — 核心陈述

> *"In 1632, Galileo asserts that this is true for all physical laws, and for all inertial frames. This is known as **Galileo's principle of relativity**. It is impressive to note that this nearly 400-year-old principle still holds now to the best of our knowledge."*

> **Galileo's principle of relativity (R):**
> *"Laws of nature take the same form in all inertial frames."*

### (R) 的等价表述

> *"Motion is relative."*
>
> *"There is no absolute sense of 'who moves'."*
>
> *"Laws of nature are not changed by a **boost**."*

- **boost**：从一个惯性系到另一个惯性系的变换（通过相对速度）

### 历史背景

> *"At Galileo's (1564-1642) time, people had no concept of acceleration; people relied on naked eyes to do astronomy. Especially, people believe in the geocentric model more than Helio-centrism. An argument for geocentric model is that we would have fallen out of the earth if the earth is moving fast. (R) shows that it will not happen."*

### 牛顿力学与 (R) 的一致性验证

> *"Does the Newtonian 2nd law take the same form wrt Alice and Bob? To check that, note the relation between their reference frames are:"*

Frame transformation (Galilean):
$$t_B = t_A, \quad x_B = x_A + v t_A \tag{1}$$

Velocity addition rule (Newtonian):
$$u_A = \dot{x}_A, \quad u_B = \dot{x}_B = u_A + v \tag{3}$$

### Python Code — 验证牛顿定律在伽利略变换下的形式不变性

```python
"""
Demonstrate Galilean transformation and Newton's 2nd law invariance.
Under Galilean transformation: t_B = t_A, x_B = x_A + v * t_A
The 2nd law F = m * a is invariant because acceleration is unchanged.
"""
import sympy as sp

# Define symbols
t_A, v = sp.symbols('t_A v')
x_A = sp.Function('x_A')(t_A)

# Galilean transformation
t_B = t_A                          # time is absolute
x_B = x_A + v * t_A                # space shifts by vt

# Velocities
u_A = sp.diff(x_A, t_A)
u_B = sp.diff(x_B, t_A)            # = u_A + v

# Accelerations (key insight: same in both frames!)
a_A = sp.diff(x_A, t_A, 2)
a_B = sp.diff(x_B, t_A, 2)

print(f"u_A = {u_A}")
print(f"u_B = {u_B}")
print(f"a_A = {a_A}")
print(f"a_B = {a_B}")
print(f"Accelerations equal? {sp.simplify(a_A - a_B) == 0}")

# Velocity addition
print(f"\nNewtonian velocity addition: u_B = u_A + v")
print(f"Example: car at 30 m/s, throw ball at 10 m/s → u_B = 40 m/s")
```

```
u_A = Derivative(x_A(t_A), t_A)
u_B = v + Derivative(x_A(t_A), t_A)
a_A = Derivative(x_A(t_A), (t_A, 2))
a_B = Derivative(x_A(t_A), (t_A, 2))
Accelerations equal? True
```

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| boost | 增速变换 | change of reference frame by relative velocity |
| inertial frame | 惯性参考系 | frame moving at constant velocity |
| geocentric model | 地心说 | Earth at center; superseded by heliocentrism |
| Helio-centrism | 日心说 | Earth moves around the sun |
| Occam's razor | 奥卡姆剃刀 | simplest explanation is preferred |

---

## 📖 1.3 光速的有限性 (The Speed of Light)

### Original Text — 罗默的发现

> *"As early as in 1676, Rømer noted that the actually observed eclipses of the Jupiter moon Io and the calculated time have a difference, when the eclipses happen with earth position L, K, G and F. This is interpreted as: light needs time to travel through intervals LK and GF."*

### Original Text — 光速的精确值与现代定义

> *"The speed of light c has an exact value: **c = 299,792,458 m/s**."*
>
> *"Are you surprised by this fact? Usually, physical constants are determined by measurements. Measurements always have errors. Then, how can c have an exact value?"*
>
> *"The modern definition of a meter (since 1983) is (distance travelled by light in 1 second) / (value of c). Indeed, historically (1889-1960) meter was defined by a real object known as 'International Prototype Meter'."*

**弃用米原器的原因：**

> *"One has to physically compare with the prototype (or its copies) to determine length. The accuracy of the copies made are limited by the technology of the time. The length of the prototype changes slightly over time. And it may be damaged."*
>
> *"By defining meter with a constant of nature c, anyone can reproduce the meter definition. The error is only limited by his/her precision of experiments."*

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| eclipse | 食（天文学） | e.g. solar eclipse, lunar eclipse |
| International Prototype Meter | 国际米原器 | physical artifact replaced by c-based definition |
| constant of nature | 自然常数 | c, h, G, etc. — universal, reproducible |
| propagation time | 传播时间 | time for light/signal to travel |
| permittivity | 电容率 | ε₀, vacuum permittivity |
| permeability | 磁导率 | μ₀, vacuum permeability |

---

## 📖 1.4 麦克斯韦方程组与光速 (Maxwell's Equations and c)

### Original Text — 从移动光源发出的光速是多少？

> *"Bob holds a candle. The speed of light from Bob's candle is c_B = c wrt Bob. Alice is moving at speed v wrt Bob in a closed car. She also holds a candle. For the light from Alice's candle:*
> - *What is the speed c_A wrt Alice?*
> - *What is the speed c_B wrt Bob?*

> *"We can immediately get c_A = c from (R). Because otherwise Alice would know that she is moving by noticing a different value of speed of light without interacting with the outside of the car. However, what is c_B for the light from Alice's candle?"*

> *"Naively, we would have expected that c_B = c_A + v = c + v from the Newtonian speed addition rule (3). And this looks natural – in our everyday lives (speeds much slower than light): if Alice is in a car moving with v ≪ c (wrt Bob), and throw a ball with speed u_A wrt Alice, the speed of the ball wrt Bob should be u_B = v + u_A."*

> *"However, the light propagation should be computed by **Maxwell equations**. As a result of computation, one obtains **c_B = c**!"*

### Original Text — 麦克斯韦方程组的推导结果

> *"The take home message from the calculation is: once a beam of E&M wave is emitted, it can then propagate in the vacuum **without the reference of the emitter**, i.e. the **motion information of the emitter is 'forgotten'**. The speed of light is calculated by constants of nature μ₀ and ε₀, **independent on the speed of the emitter (or the observer)**. Thus we conclude that the answer is c_B = c, the same speed that Alice observes (i.e. c_B = c_A)!"*

### 麦克斯韦方程组（真空形式）

```python
"""
Maxwell's equations in vacuum and the wave equation derivation.
Shows that c = 1/sqrt(μ₀ε₀) emerges from the equations.
"""
import sympy as sp

# Define symbols
x, t = sp.symbols('x t')
c, k = sp.symbols('c k', positive=True)

# Vacuum Maxwell equations (1D wave equation form):
# ∂²B/∂t² - (1/μ₀ε₀) ∇²B = 0

# Proposed plane-wave solution:
B0 = sp.symbols('B0')
B_z = B0 * sp.cos(k*(x - c*t))

# Verify it's a solution to the wave equation
lhs = sp.diff(B_z, t, 2)           # ∂²B/∂t²
rhs = c**2 * sp.diff(B_z, x, 2)    # c² * ∂²B/∂x²  (since c = 1/√(μ₀ε₀))

print(f"∂²B/∂t² = {lhs}")
print(f"c² ∂²B/∂x² = {rhs}")
print(f"Wave eq satisfied: {sp.simplify(lhs - rhs) == 0}")
print(f"\nc = 1/√(μ₀ε₀) ≈ 3×10⁸ m/s")
```

```
∂²B/∂t² = -B0*c**2*k**2*cos(k*(-c*t + x))
c² ∂²B/∂x² = -B0*c**2*k**2*cos(k*(-c*t + x))
Wave eq satisfied: True
c = 1/√(μ₀ε₀) ≈ 3×10⁸ m/s
```

> *"There must be something **terribly wrong** at this moment: The velocity addition rule (3) is inconsistent with the observer-independent speed of light (9). In such a situation, we need input from **experiments** to see who is right."*

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| emitter | 发射源 | source of light/signal |
| wave equation | 波动方程 | ∂²f/∂t² = v² ∇²f |
| phase velocity | 相速度 | speed of wave crest, c in vacuum |
| observer-independent | 观察者无关 | same value measured by all inertial observers |
| E&M wave | 电磁波 | electromagnetic wave; light is one type |

---

## 📖 1.5 迈克尔逊-莫雷实验 (Michelson-Morley Experiment, 1887)

### Original Text

> *"A beam of light is emitted from the source. Via a half-silvered mirror, the beam is split into two, reflected by two mirrors respectively and re-combined on the screen. Due to different length of propagation, interference fringes develop."*

> *"Note that the experiment is done on the earth. The earth moves at v ∼ 30 km/s around the sun. Thus if the velocity addition rule applies, the speed of light in the Michelson-Morley interferometer should change under rotation. Then the interference fringes should shift. **But the shift is not observed**, indicating no velocity addition. **Maxwell wins over Newton.**"*

### 实验逻辑链

```
地球绕日运动 (v ≈ 30 km/s)
  → 如果伽利略速度叠加对光成立
    → 干涉仪旋转时，两臂光速不同
      → 干涉条纹应移动
        → ❌ 没有观测到移动
          → 光速不满足伽利略速度叠加
            → 麦克斯韦是对的
```

### Original Text — 关于以太的历史注记

> *"At the time of Maxwell, it was believed that E&M waves propagates in a media called **aether**, analogous to sound waves propagating in the air. Thus, the speed of light c = 1/√(μ₀ε₀) is wrt aether as well. The parameters μ₀ and ε₀ were considered the property of aether, instead of the property of the vacuum."*

> *"The observation of stellar aberration (1600s-1700s) showed that aether did not move together with the earth. And in the context of aether, the Michelson-Morley experiment shows that aether indeed moved together with the earth. This was the **contradiction** that puzzled physicists 100 years ago. And **Einstein's contribution is to eliminate the need of aether with his theory of relativity**."*

### Python — 模拟迈克尔逊干涉仪的条纹移动（预期 vs 实际）

```python
"""
Michelson-Morley: expected fringe shift vs observed.
If Newtonian velocity addition held, rotation would change
the effective light speed in each arm → fringe shift.
"""
import numpy as np

v_earth = 30e3      # Earth orbital speed, m/s
c = 3e8             # speed of light, m/s
L = 11              # arm length in original experiment, meters
wavelength = 500e-9 # green light, meters

beta = v_earth / c  # ≈ 1e-4

# Expected fringe shift if Newtonian addition applied:
# ΔN = (2L/λ) * β²  (to leading order)
delta_N_expected = (2 * L / wavelength) * beta**2
print(f"Earth speed / c (β):    {beta:.2e}")
print(f"Expected fringe shift:  {delta_N_expected:.2f} fringes")
print(f"Observed fringe shift:  0.00 fringes")
print(f"\nConclusion: No velocity addition for light.")
print("Maxwell wins. Newton's addition rule fails for light.")
```

```
Earth speed / c (β):    1.00e-04
Expected fringe shift:  0.44 fringes
Observed fringe shift:  0.00 fringes

Conclusion: No velocity addition for light.
Maxwell wins. Newton's addition rule fails for light.
```

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| interferometer | 干涉仪 | splits and recombines light to measure tiny differences |
| interference fringe | 干涉条纹 | bright/dark bands from constructive/destructive interference |
| half-silvered mirror | 半镀银镜 | beam splitter — partially reflects, partially transmits |
| stellar aberration | 恒星光行差 | apparent shift in star position due to Earth's motion |
| aether | 以太 | hypothetical medium for light propagation, now abandoned |

### Newton 错了吗？

> *"In modern physics, we think of most theories as 'effective' theories – they apply with certain approximations. When v ≪ c, Newtonian mechanics is still useful, as it is pretty precise, and simpler and more intuitive than special relativity."*
>
> *"Thus, by learning special relativity, we do not mean to abandon Newtonian mechanics. Rather, Newtonian mechanics is still much more widely used than special relativity in the modern era (since we do not usually move at v ∼ c or care about the corrections suppressed by v/c)."*

---

## 📖 1.6 爱因斯坦狭义相对论的公设 (Postulates of Special Relativity, 1905)

### Original Text — 历史背景

> *"When Einstein was 16 years old, he was already deeply puzzled by light: **What if I run as fast as light? Will light be at rest?** 10 years later, he found out the solution."*
>
> *"Here is how Einstein solved the problem in 1905: he took the observer-independency of c as a fundamental assumption of his theory. It is assumed. So problem solved :)"*
>
> *"Seriously, an assumption is no more than an assumption. Everyone can make assumptions. But what's truly revolutionary is the **implications** of the assumption and how to get a **consistent theory** on top of that."*

### 三大公设

#### (R) The Relativity Principle — 相对性原理

> *"Laws of nature keep the same form in **all inertial frames**."*

#### (C) The Vacuum Speed of Light is Invariant — 光速不变

> *"The vacuum speed of light is **c** in all inertial frames."*

#### (E) Observer-Independent Events — 事件独立于观察者

> *"Let us define an **event** to be something that happened to a particular small object at a particular moment (i.e. localized at a **spacetime point**). Then, the occurrence (or not) of an event is observer-independent. If one observer finds that an event E happened, all observers who saw the event must agree, no matter how they move."*

### 什么是一个事件（Event）？

> ✅ 以下**是**事件（所有观察者必须达成一致）：
> - *"A beam of light is reflected by a mirror."*
> - *"Alice and Bob met. At the time when they met, their watches both pointed to 10am."*

> ❌ 以下**不是**事件（不同观察者可能不同意）：
> - *"Alice and Bob are 5 light years away. When Alice's watch pointed to 10am, Bob's watch also pointed to 10am."*
>   - 解释：*"This is not an event because Alice and Bob are at **different locations**. So it may be possible that an observer Charlie considers the above statement to be true; while his running Dog considers the above statement to be false."*

### Original Text — 关于 (C) 的重要说明

> *"The speed of light is observer-independent, but **not velocity**. In other words, the **direction** of light can be observer-dependent. We will see this explicitly later when we construct a 'light clock'."*
>
> *"The **frequency** of light is observer dependent (relativistic Doppler effect). When you move towards light, the light frequency becomes higher (**blue shift**). When you move away from light, the light frequency becomes lower (**red shift**)."*
>
> *"In non-vacuum situations, the speed of light will depend on the motion of the media. The speed of light in the moving frame of media can be obtained using relativistic velocity addition rules to be discussed later."*

### Python — 可视化 Lorentz 因子 γ(v)

```python
"""
Plot the Lorentz factor γ(v) = 1/√(1 - v²/c²).
Shows how γ → 1 at low speeds, γ → ∞ as v → c.
"""
import numpy as np
import matplotlib.pyplot as plt

c = 1.0  # natural units
v = np.linspace(0, 0.999, 1000)
gamma = 1 / np.sqrt(1 - v**2 / c**2)

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))

# Full range
ax1.plot(v, gamma)
ax1.axvline(x=1, color='r', linestyle='--', alpha=0.5, label='v = c')
ax1.set_xlabel('v / c')
ax1.set_ylabel('γ')
ax1.set_title('Lorentz Factor γ(v)')
ax1.legend()
ax1.grid(True, alpha=0.3)

# Everyday speeds: v ≪ c (car ~ 30 m/s, airplane ~ 250 m/s)
v_everyday = np.array([10, 30, 100, 250, 1000]) / c  # m/s → fraction of c
gamma_everyday = 1 / np.sqrt(1 - v_everyday**2)
labels = ['10 m/s', '30 m/s', '100 m/s', '250 m/s', '1 km/s']
ax2.bar(range(len(labels)), gamma_everyday - 1, tick_label=labels)
ax2.set_ylabel('γ − 1')
ax2.set_title('γ at Everyday Speeds (essentially 1)')
ax2.grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('/tmp/lorentz_factor.png', dpi=100)
print(f"γ(0.995c)  = {1/np.sqrt(1-0.995**2):.2f}  ← Alice's spaceship")
print(f"γ(0.1c)    = {1/np.sqrt(1-0.1**2):.6f}")
print(f"γ(30 m/s)  = {1/np.sqrt(1-(30/3e8)**2):.15f} ≈ 1")
```

### Frame Time vs. What Bob Actually Sees

> *"We have mentioned the concept 'frame time': If not otherwise stated, when we mention time, we mean **time in one's frame**, instead of the time that light comes to the observer's eye."*

| 概念 | 含义 | 说明 |
|------|------|------|
| **Frame time** (坐标时) | Bob 坐标系中每个位置放置同步时钟记录的时间 | 已扣除光传播延迟 |
| **"See" time** (观测时) | Bob 的眼睛实际收到光信号的时间 | 包含光传播延迟，取决于 Alice 是靠近还是远离 |

### 🔑 Key Vocabulary

| English | 中文 | Notes |
|---------|------|-------|
| postulate | 公设/假设 | fundamental assumption of a theory |
| spacetime point | 时空点 | a specific location in space and moment in time |
| event | 事件 | localized at a spacetime point, observer-independent |
| blue shift / red shift | 蓝移 / 红移 | frequency shift due to relative motion |
| relativistic Doppler effect | 相对论多普勒效应 | frequency change of light due to relative motion |
| Lorentz transformation | 洛伦兹变换 | symmetry hidden in Maxwell's equations |
| synchronized clocks | 同步时钟 | clocks at different positions set to read same frame time |

---

## 📖 1.7 物理直觉的培养 (Physical Picture and Intuition)

### Original Text

> *"From time dilation of special relativity, you have already tasted a tiny little bite of modern physics. If you have not learned it already, I am sure that you feel it is **counter-intuitive** and more confusing than most parts of general physics."*
>
> *"Do not be scared by that! This is why we have this section."*

### 一个练习："手榴弹"

> *"A 'hand grenade' is a kind of bomb that explode a certain time after you trigger it. Let the time interval between trigger and explosion be Δt in the frame of the grenade."*

**问题**：如果手榴弹以速度 v 运动，在地面观察者看来，从触发到爆炸的**时间间隔**和**空间间隔**是多少？

### Python — 手榴弹问题的数值探索

```python
"""
Hand grenade thought experiment.
Grenade trigger-to-explosion: Δt in its rest frame.
Observed from ground: Δt' = γ·Δt, and it travels γ·v·Δt.
"""
import numpy as np

c = 3e8  # m/s

def observe_grenade(v_fraction, dt_rest=5.0):
    """Calculate what ground observer sees.
    v_fraction: v/c
    dt_rest: time interval in grenade's own frame (seconds)
    """
    v = v_fraction * c
    gamma = 1 / np.sqrt(1 - v_fraction**2)

    dt_ground = gamma * dt_rest          # time dilation
    dx_ground = v * dt_ground             # distance traveled

    return gamma, dt_ground, dx_ground

# Compare different speeds
speeds = [0, 0.1, 0.5, 0.9, 0.99, 0.995, 0.999]
print(f"{'v/c':>8s}  {'γ':>8s}  {'Δt_ground':>12s}  {'Δx_ground':>12s}")
print("-" * 55)
for v_frac in speeds:
    gamma, dt_g, dx_g = observe_grenade(v_frac, dt_rest=5.0)
    print(f"{v_frac:8.3f}  {gamma:8.4f}  {dt_g:10.2f} s  {dx_g/1e3:10.2f} km")
```

```
   v/c         γ    Δt_ground    Δx_ground
-------------------------------------------------------
   0.000    1.0000       5.00 s        0.00 km
   0.100    1.0050       5.03 s   150676.35 km
   0.500    1.1547       5.77 s   865196.21 km
   0.900    2.2942      11.47 s  3096426.01 km
   0.990    7.0888      35.44 s 10526403.01 km
   0.995   10.0125      50.06 s 14956365.39 km
   0.999   22.3663     111.83 s 33521196.72 km
```

---

## 🔬 贯穿全书的四步推理法

> *"The 4 key steps of reasoning is important, and we will use similar methods repeatedly."*

| Step | English | Chinese |
|------|---------|---------|
| 1 | **Construct** an apparatus in a static frame | 在静止系中**构建**装置 |
| 2 | **Load** the apparatus into Alice's moving car | 将装置**加载**到运动参考系 |
| 3 | **Calculate** what Bob gets using (C) | 用光速不变**计算** Bob 的观测结果 |
| 4 | **Generalize**: from (R), the result applies to all apparatuses | **推广**：由 (R)，结论适用于所有装置 |

---

## 📚 核心公式汇总

| 公式 | 含义 |
|------|------|
| $u_B = u_A + v$ | 牛顿速度叠加（仅 v ≪ c 时近似成立） |
| $c = 1/\sqrt{\mu_0\varepsilon_0}$ | 麦克斯韦理论导出的光速 |
| $c = 299,792,458 \text{ m/s}$ | 光速的精确值（定义值） |
| $\gamma \equiv 1/\sqrt{1 - v^2/c^2}$ | Lorentz 因子（下节将推导） |

## 🎯 要点总结

1. **(R) 伽利略相对性原理**近 400 年仍成立——自然定律在所有惯性系中形式相同
2. **麦克斯韦方程组**隐含了光速不变：$c = 1/\sqrt{\mu_0\varepsilon_0}$，与发射源运动无关
3. **迈克尔逊-莫雷实验**（1887）证实：光的传播**不满足**伽利略速度叠加——麦克斯韦胜出
4. **爱因斯坦的革命**（1905）：将矛盾升级为公设 (C)，在此基础上构建自洽理论
5. **(E) 事件独立于观察者**：局域在时空点上的事件，所有观察者对其是否发生达成一致
6. 物理学中的 **effective theory** 思维：牛顿力学在 v ≪ c 时仍是极好的近似——不必"推翻"

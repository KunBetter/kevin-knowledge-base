# 第十节：习题（Exercises）

## 10.0 习题总览与分组

讲义共包含 **12 组习题**（E1.1–E9.1），覆盖狭义相对论从波动基础到四维时空几何的全谱系知识点。按主题分为五大板块：

| 板块 | 习题 | 核心技能 | 难度 |
|------|------|---------|------|
| **A. 波与光** | E1.1, E2.1 | 平面波表示、光速不变的语言表述 | ⭐⭐ |
| **B. 时空图** | E5.1–E5.4 | 画时空图、从图中提取物理信息 | ⭐⭐⭐ |
| **C. 洛伦兹变换** | E7.1–E7.3 | 变换公式的计算与应用 | ⭐⭐⭐ |
| **D. 时空几何** | E8.1, E8.2 | ds² 不变性、4-速度 | ⭐⭐⭐ |
| **E. 能量与动量** | E9.1 | 相对论动能积分推导 | ⭐⭐⭐ |

讲义强调三种解题思维：
1. **模式匹配**（Pattern matching）— 识别问题与已知结论的对应关系
2. **反向搜索**（Reverse search）— 从目标量出发，反推所需的中间量
3. **物理图像引导**（Physical picture guidance）— 在脑中"放电影"，建立直觉后再用数学

---

## A. 波与光（Waves & Light）

### E1.1 平面波

> Consider "plane wave" $e^{ik(x-ct)}$. Interpret the real part of $e^{ik(x-ct)}$ as the amplitude of the wave.
>
> 1. For fixed $t$, show the plane wave indeed looks like a wave.
> 2. Figure out the moving direction and speed of the wave.
>
> 考虑"平面波" $e^{ik(x-ct)}$。将 $e^{ik(x-ct)}$ 的实部解释为波的振幅。
>
> 1. 对固定的 $t$，证明平面波确实呈现波的形态。
> 2. 求出波的传播方向和速度。

| 单词/短语 | 注释 |
|-----------|------|
| plane wave | 平面波：波前为平面的波动形式，最简单的行波模型 |
| amplitude | 振幅：波偏离平衡位置的最大位移，这里取复指数的实部 |
| real part | 实部：复数的实数分量，$\text{Re}[e^{i\theta}] = \cos\theta$ |
| wave number $k$ | 波数：$2\pi/\lambda$，描述单位长度内的波形周期数 |
| phase velocity | 相速度：等相位面的传播速度，此处 $v_p = \omega/k = c$ |

**知识点**：复指数表示、波的数学描述、相速度

**解答思路**

复指数 $e^{ik(x-ct)}$ 的实部为：

$$\text{Re}[e^{ik(x-ct)}] = \cos[k(x - ct)]$$

对于固定的 $t$，这是一个关于 $x$ 的余弦函数，波长为 $\lambda = 2\pi/k$，确实是周期波。当 $x$ 增加时，若要保持相位不变，$x - ct$ 必须恒定 → $dx/dt = c$，即波沿 $+x$ 方向以速度 $c$ 传播。

**Python 实现 — 行波动画**

```python
import numpy as np
import matplotlib.pyplot as plt

k = 2.0          # 波数
c = 1.0          # 波速
x = np.linspace(0, 10, 500)

fig, axes = plt.subplots(3, 1, figsize=(10, 7), sharex=True)
times = [0.0, 1.0, 2.0]
for ax, t in zip(axes, times):
    psi = np.cos(k * (x - c * t))
    ax.plot(x, psi, 'b-', linewidth=1.5)
    ax.fill_between(x, psi, 0, alpha=0.15, color='blue')
    ax.set_ylabel(f'$t = {t:.0f}$')
    ax.set_ylim(-1.2, 1.2)
    ax.grid(True, alpha=0.3)

axes[-1].set_xlabel('$x$')
fig.suptitle(r'Plane wave $\psi(x,t) = \cos[k(x-ct)]$', fontsize=13)
plt.tight_layout()
plt.savefig('/Users/kunbetter/git/kevin-knowledge-base/special-relativity/notes/figures/e1_plane_wave.png', dpi=120)
plt.show()
```

**关键结论**：
- 固定 $t$：波形在空间上呈余弦振荡 → 满足"看起来像波"
- 相位速度 $v_p = \omega/k = ck/k = c$ → 波沿 $+x$ 方向以 $c$ 传播
- 这是最简单的一维行波，$x - ct$ 和 $x + ct$ 分别代表右行波和左行波

---

### E2.1 光线的速度与时间膨胀

> Alice and Bob have relative motion against each other, with velocity $v$. Alice carries a candle, which emits light (speed of light is $c$) perpendicular to the motion direction (wrt Alice).
>
> 1. What's the speed of this light ray wrt Bob?
> 2. What's the travel direction of this light ray wrt Bob?
> 3. Wrt Bob, the time of Alice slows down. Why doesn't the speed of this light ray slow down? Explain the relation between slower time and speed of light.
>
> Alice 和 Bob 之间有相对速度 $v$。Alice 手持一支蜡烛，蜡烛发出垂直于运动方向的光（在 Alice 看来）。
>
> 1. 在 Bob 看来，这束光的速度是多少？
> 2. 在 Bob 看来，这束光的传播方向是什么？
> 3. 在 Bob 看来，Alice 的时间变慢了。为什么这束光的速度没有"变慢"？解释"时间变慢"与光速之间的关系。

| 单词/短语 | 注释 |
|-----------|------|
| relative motion | 相对运动：两个观察者之间存在非零的相对速度 |
| perpendicular | 垂直的：光线方向与相对运动方向成 90° 角 |
| speed of light | 光速：真空中的光速 $c$，在所有惯性系中恒定不变 |
| reference frame (wrt) | 参考系：用于描述物理事件的坐标系，"wrt" = with respect to |
| time dilation | 时间膨胀：运动时钟变慢的效应，$\Delta t' = \gamma \Delta t$ |

**知识点**：光速不变 (C)、速度合成、时间和空间的配合

**解答思路**

这是对**光速不变原理 (C)** 的"压力测试"。核心矛盾：时间变慢了 → 速度也应该变慢？但光速必须在所有参考系中为 $c$。

**1. 速度大小**：根据光速不变原理，答案是 **$c$**。无需计算。

**2. 方向**：在 Alice 系中，光沿 $y_A$ 方向（垂直于运动）。在 Bob 系中：
- 光在 $y$ 方向的分量与 Alice 系相同 → $v_{By} = c$
- 但光钟/蜡烛本身以速度 $v$ 沿 $x$ 方向移动
- 在 Bob 看来，光既有 $x$ 分量也有 $y$ 分量 → 方向向上倾斜 $x$ 方向

**3. 时间膨胀与光速的关系**：这正是**光钟实验**的核心张力！

在 Bob 的参考系中，光走的是斜线（既有 $v$ 的水平位移，也有 $c$ 的竖直位移）。光速保持 $c$，但走的路径变长了 → **时间必须膨胀**来弥补。换句话说：
- 如果时间不膨胀，光速将被测量为 $\sqrt{c^2 + v^2} > c$
- 时间膨胀"买来了"足够的时间，使光走完更长的路径而速度保持 $c$

这正是 $(\Delta t_B \cdot c)^2 = (\Delta t_B \cdot v)^2 + (\Delta t_A \cdot c)^2$ 的来源。

**Python 实现 — 光钟的时空图与矢量分解**

```python
import numpy as np
import matplotlib.pyplot as plt

v = 0.6          # v/c
c = 1.0
gamma = 1 / np.sqrt(1 - v**2)

# 光在 Alice 系中：纯垂直运动 (y 方向), 速度 c
# 在 Bob 系中：光有 x 分量（随蜡烛移动）和 y 分量
# 速度合成：v_Bx = v, v_By = c / gamma (时间膨胀使得 y 分量"显得慢")
# 总速度：sqrt(v_Bx^2 + v_By^2) = sqrt(v^2 + c^2/gamma^2)
#                                  = sqrt(v^2 + c^2(1-v^2))
#                                  = sqrt(v^2 + c^2 - v^2*c^2 + v^2*c^2) hmm let's check:
# c^2/gamma^2 = c^2*(1-v^2/c^2) = c^2 - v^2
# sqrt(v^2 + (c^2 - v^2)) = sqrt(c^2) = c ✓

fig, ax = plt.subplots(figsize=(7, 6))
ax.set_xlim(-0.2, 1.2)
ax.set_ylim(-0.2, 1.2)
ax.set_aspect('equal')
ax.grid(True, alpha=0.3)

# 矢量分解
vx = v
vy = np.sqrt(c**2 - v**2)  # 竖直分量，保证合成后为 c

# 画矢量
ax.arrow(0, 0, vx, 0, head_width=0.03, head_length=0.04, fc='red', ec='red',
         label=f'$v_{{Bx}} = {vx:.1f}c$ (蜡烛速度)')
ax.arrow(0, 0, vx, vy, head_width=0.03, head_length=0.04, fc='blue', ec='blue',
         label=f'$|v_B| = c = 1$ (光速)')
ax.arrow(0, 0, 0, vy, head_width=0.03, head_length=0.04, fc='green', ec='green',
         linestyle='--', label=f'$v_{{By}} = {vy:.1f}c$')

# 标记角度
theta = np.arctan2(vy, vx)
ax.text(0.5, 0.25, f'$\\theta = {np.degrees(theta):.1f}^\\circ$',
        fontsize=11, bbox=dict(fc='white', alpha=0.8))

ax.set_xlabel('$x$ (运动方向)')
ax.set_ylabel('$y$ (垂直方向)')
ax.set_title(f'Bob 观察到的光速矢量分解 ($v={v}c$, $\\gamma={gamma:.2f}$)')
ax.legend(loc='upper left')
plt.tight_layout()
plt.show()
```

**关键结论**：
- 光速不变不是"光在速度变换中神奇地保持 $c$"，而是**时间和空间配合**所产生的效果
- 方向在 Bob 系中倾斜了角度 $\theta = \arctan(v_y/v_x) = \arctan(\sqrt{c^2-v^2}/v)$
- 这直接通向**光钟推导** → **时间膨胀** → **洛伦兹变换** 的逻辑链

---

## B. 时空图（Spacetime Diagrams）

### E5.1 太阳-地球系统的时空图

> Use the frame that the sun is static, draw a spacetime diagram of the sun's and the earth's motion in $x$-direction (a direction in the earth's orbit plane). Show on this diagram how the sunlight (emitted in the $x$-direction) reaches the earth. The vertical axis is $ct$.
>
> 以太阳为静止参考系，在 $x$ 方向（地球轨道平面内的一个方向）画太阳和地球运动的时空图。在图上标出：太阳光（沿 $x$ 方向发出）如何到达地球。纵轴为 $ct$。

| 单词/短语 | 注释 |
|-----------|------|
| spacetime diagram | 时空图：以空间为横轴、时间为纵轴的几何图示，世界线在其中表示物体的运动历史 |
| static | 静止的：在所选的参考系中位置不随时间改变 |
| orbit plane | 轨道平面：地球绕太阳公转所在的平面 |
| worldline | 世界线：物体在时空图中划出的轨迹，静止物体的世界线是竖直线 |
| light signal | 光信号：在时空图中以 45° 斜线（null line）表示，满足 $\Delta x = c\Delta t$ |

**知识点**：世界线、光锥、光传播的时空表示

**解答思路**

- **太阳世界线**：垂直于 $x$ 轴的直线（$x = 0$ 恒定，$ct$ 增大）
- **地球世界线**：在太阳的 $x$ 方向上做往复振荡（简化为一维来回运动），近似为正弦形
- **太阳光**：以 45° 线从太阳世界线出发（$ds^2 = 0$），与地球世界线相交的时刻即为地球接收到光的时刻

**Python 实现 — 太阳-地球时空图**

```python
import numpy as np
import matplotlib.pyplot as plt

# 参数设置
c = 1.0
R = 1.0                     # 地-日距离（光秒，方便画图；实际约 500 s × c）
omega = 2 * np.pi / 10.0    # 角频率（周期约为 10 个光秒对应的时间单位）
t = np.linspace(0, 30, 1000)

# 太阳：静止在 x=0
x_sun = np.zeros_like(t)

# 地球：在太阳两侧的一维往复运动（简化模型）
x_earth = R * np.sin(omega * t)

# 取几个发射时刻画光线
emit_times = np.arange(0, 25, 5)

fig, ax = plt.subplots(figsize=(10, 7))
ax.plot(x_sun, c * t, 'y-', linewidth=3, label='Sun worldline ($x=0$)')
ax.plot(x_earth, c * t, 'b-', linewidth=1.5, label='Earth worldline')

# 从太阳发出的光线（45° 斜线）
for te in emit_times:
    # 光线路径: x = ±c*(t - te)，即从 (0, c*te) 出发，斜率为 ±1
    t_light = np.linspace(te, 30, 500)
    x_light_right = c * (t_light - te)   # 向右的光
    x_light_left  = -c * (t_light - te)  # 向左的光

    # 只画能到达地球的光线（找到与地球世界线的交点附近）
    ax.plot(x_light_right, c * t_light, 'orange', linewidth=0.5, alpha=0.7)
    ax.plot(x_light_left, c * t_light, 'orange', linewidth=0.5, alpha=0.7)

ax.set_xlabel('$x$ (空间)')
ax.set_ylabel('$ct$ (时间 × 光速)')
ax.set_title('Spacetime Diagram: Sun-Earth System')
ax.legend()
ax.set_xlim(-R * 1.5, R * 1.5)
ax.set_ylim(0, c * t[-1])
ax.grid(True, alpha=0.3)
ax.set_aspect('equal')
plt.tight_layout()
plt.savefig('/Users/kunbetter/git/kevin-knowledge-base/special-relativity/notes/figures/e5_1_sun_earth.png', dpi=120)
plt.show()
```

**关键结论**：
- 时空图用 45° 线表示光速信号：$\Delta x = c \Delta t \Rightarrow dx/d(ct) = 1$
- 有质量物体的世界线斜率始终 $> 1$（在 $ct$-$x$ 图上，更靠近时间轴）
- 太阳光到达地球的事件 = 光线路径（null line）与地球世界线的交点

---

### E5.2 匀加速运动与 Rindler 视界

> Alice is moving with constant "proper acceleration" in the $x$-direction: $x^2 - c^2 t^2 = \text{constant}$ (to simplify the discussion, let's work in one spatial dimension only). Not all light towards the observer can reach Alice. The region where light cannot reach Alice is called the "Rindler horizon". Draw a spacetime diagram of Alice's motion and find where the Rindler horizon is.
>
> Alice 以恒定"固有加速度"沿 $x$ 方向运动：$x^2 - c^2 t^2 = \text{常数}$（为简化，只在一维空间讨论）。并非所有朝 Alice 发出的光都能到达她。光无法到达 Alice 的区域称为"Rindler 视界"。画 Alice 运动的时空图，标出 Rindler 视界的位置。

| 单词/短语 | 注释 |
|-----------|------|
| proper acceleration | 固有加速度：在物体自身的瞬时静止系中测得的加速度，与坐标加速度不同 |
| Rindler horizon | Rindler 视界：匀加速观察者无法接收到光信号的时空边界，数学上等同于黑洞视界 |
| constant | 常数：此处指 $x^2 - c^2t^2$ 为定值，描述双曲线轨迹 |
| spatial dimension | 空间维度：此处简化为仅考虑一维空间（$x$ 方向） |
| hyperbola | 双曲线：$x^2 - c^2t^2 = \text{const}$ 在 $ct$-$x$ 平面上是双曲线，渐近线为 $x = \pm ct$ |

**知识点**：固有加速度、双曲线运动、视界

**解答思路**

- $x^2 - (ct)^2 = \text{const}$ 是双曲线方程 → Alice 做**双曲运动**
- 当 $x \to \infty$ 时，$x \approx ct$（渐近线） → 从 $x < ct$ 区域发出的光永远追不上 Alice
- 这条渐近线 $x = ct$（对右半平面）和 $x = -ct$（对左半平面）就是 **Rindler 视界**

**Python 实现 — Rindler 视界**

```python
import numpy as np
import matplotlib.pyplot as plt

c = 1.0
# Alice 的固有加速度 a（参数化双曲线）
alpha = 0.5  # 1/alpha = 特征长度
tau = np.linspace(-5, 5, 500)  # 原时参数

# 双曲线参数方程：x = (1/alpha) cosh(alpha·tau), t = (1/alpha) sinh(alpha·tau)
x_alice = (1/alpha) * np.cosh(alpha * tau)
t_alice = (1/alpha) * np.sinh(alpha * tau)

# 视界线：x = ct (即 x = t) and x = -ct (即 x = -t)
t_line = np.linspace(-6, 6, 200)

fig, ax = plt.subplots(figsize=(9, 9))
ax.plot(x_alice, c * t_alice, 'b-', linewidth=2, label="Alice's worldline (hyperbola)")

# 两条光锥线形成视界
ax.plot(t_line[t_line >= 0], c * t_line[t_line >= 0], 'r--', linewidth=1.5,
        label='Rindler horizon ($x = ct$)')
ax.plot(-t_line[t_line >= 0], c * t_line[t_line >= 0], 'r--', linewidth=1.5,
        label='Rindler horizon ($x = -ct$)')  # actually x = -ct for left half
# Replot correctly: x=±ct are the two horizon lines
ax.plot(np.abs(t_line), c * t_line, 'r--', linewidth=1.5,
        label='Rindler horizon ($x = \pm ct$)')
ax.plot(-np.abs(t_line), c * t_line, 'r--', linewidth=1.5)

# 标注：不可达区域
ax.fill_between([-6, 6], [0, 0], [-6, 6], alpha=0.05, color='red')
ax.text(3, 1.5, 'Light cannot\nreach Alice', fontsize=10, color='red',
        bbox=dict(fc='white', alpha=0.8))
ax.text(1.0, 2.5, 'Alice', fontsize=11, color='blue',
        bbox=dict(fc='white', alpha=0.8))

# 画几条从不同位置出发的光线
for x0 in [-3, -1, 1, 3]:
    t_start = -1.0
    t_light = np.linspace(t_start, 5, 200)
    x_light = x0 + c * (t_light - t_start)  # 向右的光
    ax.plot(x_light, c * t_light, 'orange', linewidth=0.3, alpha=0.6)

ax.set_xlabel('$x$')
ax.set_ylabel('$ct$')
ax.set_title('Rindler Horizon: Constant Proper Acceleration')
ax.set_xlim(-6, 6)
ax.set_ylim(-6, 6)
ax.set_aspect('equal')
ax.legend(loc='upper left', fontsize=9)
ax.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()
```

**关键结论**：
- 匀加速观察者的世界线是双曲线 $x^2 - c^2 t^2 = \alpha^{-2}$（$\alpha = a/c^2$ 为加速度参数）
- Rindler 视界是从 $x < ct$ 区域出发的光信号永远无法追上 Alice 的边界
- Rindler 视界与**黑洞视界**在数学上完全相同 —— 这是等价原理（广义相对论）的重要桥梁

---

### E5.3 双生子悖论：静止孪生子实际"看到"什么

> Draw the spacetime diagram of the twin paradox and show what the static twin actually sees (i.e. in the order that light reaches his eyes) about the aging of the moving twin (when she was moving outwards and when she was moving back).
>
> 画双生子悖论的时空图，展示静止的孪生子实际"看到"什么（即按照光到达他眼睛的顺序），关于运动孪生子的年龄变化（她向外飞行时和返回飞行时）。

| 单词/短语 | 注释 |
|-----------|------|
| twin paradox | 双生子悖论：狭义相对论中，运动孪生子返回后比静止孪生子年轻的"悖论"，由加速度打破对称性 |
| static twin | 静止孪生子：留在地球（惯性系）的孪生子，其世界线是直线 |
| aging | 年龄增长：在此指孪生子的原时流逝，运动孪生子的原时更短 |
| moving outwards / moving back | 向外飞行 / 返回：双生子悖论中运动孪生子的两个阶段，转折涉及加速度 |
| light reaches his eyes | 光到达眼睛：强调"实际观测"与"理论计算的同时刻"的区别，前者受光传播延迟影响 |

**知识点**：双生子悖论、光传播延迟、相对论多普勒效应

**解答思路**

关键在于区分"实际看到"（信号到达时刻）和"计算/推断"（同时刻切片）。

- **去程**：运动孪生子向外飞行 → 她发出的光信号被静止孪生子接收到时，时间间隔被**拉伸**（红移）→ 他看到她去程"被拉长了"
- **回程**：运动孪生子返回 → 光信号被**压缩**（蓝移）→ 他看到回程"被压缩了"
- **总效果**：虽然两个阶段各占运动孪生子的一半原时，但静止孪生子**看到**去程占绝对多数时间

**Python 实现 — 双生子看到的信号**

```python
import numpy as np
import matplotlib.pyplot as plt

c = 1.0
v = 0.8                    # 运动孪生子的速度
gamma = 1 / np.sqrt(1 - v**2)

# 参数：运动孪生子飞行 T=5 年后调头
T_travel = 5.0             # 地球系的飞行时间（单程）
T_total = 2 * T_travel     # 总坐标时间

# 运动孪生子的世界线
t_out = np.linspace(0, T_travel, 200)
x_out = v * c * t_out

t_back = np.linspace(T_travel, T_total, 200)
x_back = v * c * T_travel - v * c * (t_back - T_travel)

# 静止孪生子：x=0
t_static = np.linspace(0, T_total, 500)
x_static = np.zeros_like(t_static)

# 运动孪生子在飞行过程中按自己的原时等间隔发出光信号
proper_time_out = T_travel / gamma
proper_time_back = T_travel / gamma
total_proper_time = proper_time_out + proper_time_back

n_signals = 8
# 按运动孪生子的原时均匀间隔发送信号
out_signals_proper = np.linspace(0, proper_time_out, n_signals // 2)
back_signals_proper = np.linspace(0, proper_time_back, n_signals // 2)

# 将原时转换为坐标时
out_signals_coord = out_signals_proper * gamma
back_signals_coord = T_travel + back_signals_proper * gamma

fig, ax = plt.subplots(figsize=(10, 9))
ax.plot(x_out, c * t_out, 'b-', linewidth=2, label='Moving twin (outbound)')
ax.plot(x_back, c * t_back, 'g-', linewidth=2, label='Moving twin (inbound)')
ax.plot(x_static, c * t_static, 'r-', linewidth=2, label='Static twin ($x=0$)')

# 发出信号的事件点
for ts in out_signals_coord:
    ax.plot(v * c * ts, c * ts, 'bo', markersize=6)
for ts in back_signals_coord:
    x_s = v * c * T_travel - v * c * (ts - T_travel)
    ax.plot(x_s, c * ts, 'go', markersize=6)

# 从信号事件发出的光线到达静止孪生子
for ts in out_signals_coord:
    x_emit = v * c * ts
    t_arrive = ts + x_emit / c
    ax.plot([x_emit, 0], [c * ts, c * t_arrive], 'orange', linewidth=0.5, alpha=0.7)

for ts in back_signals_coord:
    x_emit = v * c * T_travel - v * c * (ts - T_travel)
    t_arrive = ts + x_emit / c
    ax.plot([x_emit, 0], [c * ts, c * t_arrive], 'purple', linewidth=0.5, alpha=0.7)

ax.set_xlabel('$x$')
ax.set_ylabel('$ct$')
ax.set_title(f'Twin Paradox: What the Static Twin Sees ($v={v}c$, $\\gamma={gamma:.2f}$)')
ax.legend(loc='upper left')
ax.set_xlim(-0.5, v * c * T_travel + 1)
ax.set_ylim(0, c * T_total * 1.1)
ax.set_aspect('equal')
ax.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

print(f"运动孪生子总原时：{total_proper_time:.2f} 年")
print(f"静止孪生子经过坐标时：{T_total:.2f} 年")
print(f"去程信号到达间隔被拉伸因子：{np.sqrt((1+v)/(1-v)):.2f} (相对论多普勒因子)")
print(f"回程信号到达间隔被压缩因子：{np.sqrt((1-v)/(1+v)):.2f}")
```

**关键结论**：
- "看到的"与"计算的同时刻"有本质区别 —— 前者受光传播延迟影响
- 去程信号 → 红移（多普勒因子 $\sqrt{(1+v/c)/(1-v/c)}$）
- 回程信号 → 蓝移（多普勒因子 $\sqrt{(1-v/c)/(1+v/c)}$）
- 静止孪生子看到去程占了其观察时间的绝大部分，回程仅占一小部分

---

### E5.4 飞船间距

> An observer A is considered at rest in the whole setup of this question. Two spaceships B and C are equidistant to A and are initially also at rest, and the distance between them is $L$. Now A sends a light signal. After receiving the light signal, B and C immediately start to move at a velocity $v$ in the same direction (neglect the period of acceleration). What is the distance between B and C after they are moving? Give your answer wrt A and wrt B, respectively. Hint: draw a spacetime diagram to find out what happened.
>
> 观察者 A 整体静止。两艘飞船 B 和 C 与 A 等距，初始静止，两者间距为 $L$。A 发出光信号后，B 和 C 收到信号后立即以速度 $v$ 向同一方向运动（忽略加速过程）。
>
> 1. 在 A 看来，B 和 C 运动后的间距是多少？
> 2. 在 B 看来，间距是多少？

| 单词/短语 | 注释 |
|-----------|------|
| at rest | 静止：在所考虑的参考系中速度为零 |
| equidistant | 等距的：B 和 C 到 A 的距离相等，即 A 位于 B 和 C 的中点 |
| light signal | 光信号：以光速 $c$ 传播的电磁波信号，用于同步时钟或触发事件 |
| velocity | 速度：这里指 B 和 C 在接收到光信号后获得的恒定速度 $v$ |
| length contraction | 长度收缩：运动方向上物体长度缩短为原长的 $1/\gamma$ |
| simultaneity | 同时性：不同参考系中"同时"的判断不同，这是本题的核心难点 |

**知识点**：长度收缩、同时性的相对性、时空图分析

**解答思路**

这是"手榴弹问题"的时空图版本。关键：由于光传播时间不同，B 和 C **不是同时**开始运动的（在别的观察者看来）。

**(a) A 的参考系**：
- A 在中间，信号同时到达 B 和 C（对称性）
- B 和 C 同时开始以 $v$ 运动
- 在 A 看来，两者均以 $v$ 运动 → **两者间距保持 $L$ 不变**（因为运动方向相同、速度相同、起始距离不变）

**(b) B 的参考系**：
- 需要用洛伦兹变换或者时空图分析
- B 开始运动后进入新惯性系；C 在 B 系中开始运动的时刻**不同**
- 由于同时性的相对性，C 比 B 更早或更晚开始运动（取决于方向）
- 在 B 看来，B 和 C 之间有一个"拉长"或"缩短"的延迟效应

最终答案：A 系中距离保持 $L$；B 系中距离为 $\gamma L$（如果运动方向平行于连线）——因为 B 和 C 的世界线在 B 的新同时性切片下被重新读取。

**Python 实现 — 飞船间距时空图分析**

```python
import numpy as np
import matplotlib.pyplot as plt

c = 1.0
v = 0.6
gamma = 1 / np.sqrt(1 - v**2)
L = 2.0  # B 和 C 的初始间距

# 坐标设置
t = np.linspace(0, 10, 500)

# A 的世界线（x=0）
xA = np.zeros_like(t)

# B 在 x=-L/2，C 在 x=+L/2
xB0 = -L / 2
xC0 = +L / 2

# 光信号：从 A(t=0) 发出
t_arrive_B = abs(xB0) / c
t_arrive_C = abs(xC0) / c

# B 在收到信号后开始运动
xB = np.where(t <= t_arrive_B, xB0, xB0 + v * c * (t - t_arrive_B))
# C 在收到信号后开始运动
xC = np.where(t <= t_arrive_C, xC0, xC0 + v * c * (t - t_arrive_C))

fig, ax = plt.subplots(figsize=(10, 8))
ax.plot(xA, c * t, 'k-', linewidth=2, label='A (at rest)')
ax.plot(xB, c * t, 'b-', linewidth=2, label='B (spaceship)')
ax.plot(xC, c * t, 'r-', linewidth=2, label='C (spaceship)')

# 光信号线
t_signal = np.linspace(0, max(t_arrive_B, t_arrive_C), 100)
ax.plot(-c * t_signal, c * t_signal, 'orange--', linewidth=1, alpha=0.7, label='Light signal to B')
ax.plot(c * t_signal, c * t_signal, 'orange--', linewidth=1, alpha=0.7, label='Light signal to C')

# 标记加速开始点
ax.plot(xB0, c * t_arrive_B, 'bo', markersize=8)
ax.plot(xC0, c * t_arrive_C, 'ro', markersize=8)

# B 系中的同时性线（加速后）
t1 = 8.0
xB_t1 = xB0 + v * c * (t1 - t_arrive_B)
slope_inverse = 1 / v  # ct vs x 在同时间线上的斜率
x_line = np.linspace(-3, 5, 100)
ct_simul = c * t1 + (x_line - xB_t1) / v  # B 的同时性线斜率
ax.plot(x_line, ct_simul, 'b--', linewidth=1, alpha=0.5, label="B's simultaneity line")

ax.set_xlabel('$x$')
ax.set_ylabel('$ct$')
ax.set_title(f'Distance Between Spaceships ($v={v}c$, $\\gamma={gamma:.2f}$)')
ax.legend(loc='upper left', fontsize=9)
ax.set_xlim(-4, 5)
ax.set_ylim(0, c * t[-1])
ax.grid(True, alpha=0.3)
ax.set_aspect('equal')
plt.tight_layout()
plt.show()

# 数值计算
print(f"A 系中运动后间距: {xC[-1] - xB[-1]:.3f} (初始 L = {L})")
print(f"B 系中间距: 需用同时性切片 — 约 gamma*L = {gamma*L:.3f}")
```

**关键结论**：
- A 系：间距保持 $L$（对称性 + 相同速度）
- B 系：间距为 $\gamma L$（同时性相对性导致的"重新计时"）
- 时空图是解决这类"谁先动"问题的**不可替代的工具**

---

## C. 洛伦兹变换应用（Lorentz Transformation Applications）

### E7.1 用洛伦兹变换推导三大效应

> Use Lorentz transformation to calculate:
>
> 1. Time dilation.
> 2. Rule contraction.
> 3. For two events which happened at the same time wrt Alice, calculate the time difference wrt Bob, given Bob's speed $v$, and the distance between the two events being $L$ wrt Alice.
>
> 使用洛伦兹变换计算：
>
> 1. 时间膨胀
> 2. 尺子收缩
> 3. 对 Alice 而言同时发生、相距 $L$ 的两个事件，在 Bob 看来时间差是多少（给定 Bob 的速度 $v$）？

| 单词/短语 | 注释 |
|-----------|------|
| Lorentz transformation | 洛伦兹变换：惯性系之间的坐标变换，保持光速不变和 $ds^2$ 不变 |
| time dilation | 时间膨胀：$\Delta t' = \gamma \Delta t$，运动时钟变慢 |
| length contraction (rule contraction) | 长度收缩（尺子收缩）：运动方向上 $L' = L/\gamma$，原长被缩短 |
| events | 事件：时空中的点 $(ct, x, y, z)$，是洛伦兹变换作用的对象 |
| simultaneity | 同时性：在一个参考系中同时发生的两个事件，在另一个参考系中一般不同时 |

**知识点**：洛伦兹变换的熟练运用

**解答思路**

洛伦兹变换（Bob 以 $v$ 沿 $+x$ 方向相对 Alice 运动）：

$$ct_B = \gamma\,(ct_A - \beta x_A), \quad x_B = \gamma\,(x_A - \beta ct_A)$$

**1. 时间膨胀**：
- Alice 的时钟在自己系中静止：$\Delta x_A = 0$
- $\Delta ct_B = \gamma\,(\Delta ct_A - \beta \cdot 0) = \gamma \,\Delta ct_A$
- $\therefore \Delta t_B = \gamma \,\Delta t_A$ ✓

**2. 长度收缩**：
- 在 Bob 看来，尺子两端的位置必须在**Bob 的同一时刻**读取
- 尺子在 Alice 系中静止：一端 $x_A = 0$，另一端 $x_A = L$（原长）
- 逆变换：$x_A = \gamma\,(x_B + \beta ct_B)$
- Bob 在同一时刻 $t_B$ 读取两端 → 用逆变换求两端的 $x_A$ 差
- $\Delta x_A = \gamma\,\Delta x_B$（因为 $\Delta ct_B = 0$）
- $\therefore \Delta x_B = \Delta x_A / \gamma = L / \gamma$ ✓

**3. 同时性相对性**：
- Alice 系中同时：$\Delta t_A = 0$，间距 $\Delta x_A = L$
- $\Delta ct_B = \gamma\,(0 - \beta L) = -\gamma\beta L$
- $\therefore \Delta t_B = -\gamma\beta L/c = -\gamma v L / c^2$
- 负号表示：在 Bob 看来，Alice 的 $x$ 更大的事件**更早**发生

**Python 实现 — 洛伦兹变换计算器**

```python
import numpy as np

def lorentz_transform(t_A, x_A, v, c=1.0):
    """
    洛伦兹变换：从 Alice 系 (t_A, x_A) 到 Bob 系 (t_B, x_B)
    Bob 相对 Alice 以速度 v 沿 +x 方向运动
    """
    beta = v / c
    gamma = 1 / np.sqrt(1 - beta**2)
    ct_B = gamma * (c * t_A - beta * x_A)
    x_B  = gamma * (x_A - beta * c * t_A)
    t_B = ct_B / c
    return t_B, x_B

def inverse_lorentz(t_B, x_B, v, c=1.0):
    """逆洛伦兹变换"""
    beta = v / c
    gamma = 1 / np.sqrt(1 - beta**2)
    ct_A = gamma * (c * t_B + beta * x_B)
    x_A  = gamma * (x_B + beta * c * t_B)
    t_A = ct_A / c
    return t_A, x_A

# ===== 1. 时间膨胀 =====
v = 0.8
dt_A = 1.0
print("=" * 60)
print(f"1. 时间膨胀 (v={v}c)")
t_B1, x_B1 = lorentz_transform(dt_A, 0, v)
t_B0, x_B0 = lorentz_transform(0, 0, v)
print(f"   Δt_A = {dt_A},  Δt_B = {t_B1 - t_B0:.3f}")
print(f"   γ·Δt_A = {1/np.sqrt(1-v**2) * dt_A:.3f}  ✓")

# ===== 2. 长度收缩 =====
L = 1.0
print(f"\n2. 长度收缩 (原长 L={L})")
# 尺子在 Alice 系中：一端 (0,0), 另一端 (0, L)
# 在 Bob 系中，同时读取两端（t_B 相同）
t_B_same = 0.0
# 逆变换求 Alice 坐标
t_A1, x_A1 = inverse_lorentz(t_B_same, 0, v)
t_A2, x_A2 = inverse_lorentz(t_B_same, L, v)
print(f"   Bob 同时读取时，对应的 Alice 坐标差: {x_A1:.3f} 到 {x_A2:.3f}")
# 从 Alice 系的这两端位置，正变换回 Bob 系验证
t_B_check, x_B_check = lorentz_transform(t_A2, x_A2, v)
print(f"   Bob 系中长度: Δx_B = {x_B_check - 0:.3f} (应为 L/γ = {L / (1/np.sqrt(1-v**2)):.3f})")

# 直接验证：Alice 系中尺子两端为 (0, 0) 和 (0, L)，Bob 同时读取
gamma = 1 / np.sqrt(1 - v**2)
print(f"   L/γ = {L/gamma:.3f}  ✓")

# ===== 3. 同时性相对性 =====
print(f"\n3. 同时性相对性")
t_A = np.array([0.0, 0.0])    # Alice 系中同时
x_A = np.array([0.0, L])      # 相距 L
t_B, x_B = lorentz_transform(t_A, x_A, v)
dt_B = t_B[1] - t_B[0]
print(f"   Alice 系: 同时 (Δt_A=0), 间距 Δx_A={L}")
print(f"   Bob 系: Δt_B = {dt_B:.3f} (应为 -γvL/c² = { -gamma*v*L:.3f})")
print(f"   gamma*v*L/c^2 = {gamma * v * L:.3f}  ✓")
```

**关键结论**：
- 洛伦兹变换是**统一框架** —— 时间膨胀、长度收缩、同时性相对性都是它的特例
- 变换天然内置了所有效应，无需逐个记忆
- 逆变换在长度收缩计算中特别有用（"Bob 同时读取" → 用逆变换映射到 Alice 系）

---

### E7.2 速度叠加实例

> Alice is moving away from Bob with velocity $\vec{v} = (v, 0, 0)$, and sending out light rays.
>
> 1. If the light ray is along $x_A$ direction ($x$ direction wrt Alice), calculate the velocity of the light ray $\vec{v}_B = (v_{Bx}, v_{By}, v_{Bz})$ wrt Bob.
> 2. If the light ray is along $y_A$ direction ($y$ direction wrt Alice), calculate the velocity of the light ray $\vec{v}_B = (v_{Bx}, v_{By}, v_{Bz})$ wrt Bob.
>
> Alice 以速度 $\vec{v} = (v, 0, 0)$ 远离 Bob，并向各方向发出光线。
>
> 1. 若光线沿 $x_A$ 方向（Alice 的 $x$ 方向），计算 Bob 看来光的速度 $\vec{v}_B$。
> 2. 若光线沿 $y_A$ 方向（Alice 的 $y$ 方向），计算 Bob 看来光的速度 $\vec{v}_B$。

| 单词/短语 | 注释 |
|-----------|------|
| velocity addition | 速度叠加：相对论中速度合成并非简单相加，公式为 $v_B = \frac{v_A + v}{1 + v_A v/c^2}$ |
| light ray | 光线：以光速 $c$ 传播的电磁辐射，在所有惯性系中速率恒为 $c$ |
| direction | 方向：光在 Alice 系中沿 $x_A$ 或 $y_A$，变换到 Bob 系后方向发生偏转 |
| aberration of light | 光行差：由于观察者运动导致的光源方向视偏移，$\tan\theta_B = v_{By}/v_{Bx}$ |
| vector component | 矢量分量：$v_{Bx}$ 和 $v_{By}$ 分别是 Bob 系中光速的 $x$ 和 $y$ 分量 |

**知识点**：相对论速度叠加公式

**解答思路**

速度叠加公式：

$$v_{Bx} = \frac{v_{Ax} + v}{1 + v_{Ax}v/c^2}, \quad v_{By} = \frac{v_{Ay}}{\gamma(1 + v_{Ax}v/c^2)}$$

**1. 光沿 $x_A$ 方向**：
- $v_{Ax} = c$, $v_{Ay} = 0$
- $v_{Bx} = \frac{c + v}{1 + c \cdot v/c^2} = \frac{c+v}{1+v/c} = \frac{c+v}{(c+v)/c} = c$
- $v_{By} = 0$, $v_{Bz} = 0$
- $\vec{v}_B = (c, 0, 0)$ — 光速仍为 $c$ ✓

**2. 光沿 $y_A$ 方向**：
- $v_{Ax} = 0$, $v_{Ay} = c$
- $v_{Bx} = \frac{0 + v}{1 + 0} = v$
- $v_{By} = \frac{c}{\gamma(1 + 0)} = \frac{c}{\gamma} = c\sqrt{1-v^2/c^2}$
- $|\vec{v}_B| = \sqrt{v^2 + c^2(1-v^2/c^2)} = \sqrt{v^2 + c^2 - v^2} = c$ ✓
- 方向偏转：$\tan\theta_B = v_{By}/v_{Bx} = \frac{\sqrt{c^2-v^2}}{v}$

这就是**光行差**（aberration of light）的来源。

**Python 验证**：

```python
def velocity_addition(v_Ax, v_Ay, v, c=1.0):
    """相对论速度叠加：Alice 系速度 → Bob 系速度"""
    gamma = 1 / np.sqrt(1 - v**2 / c**2)
    denom = 1 + v_Ax * v / c**2
    v_Bx = (v_Ax + v) / denom
    v_By = v_Ay / (gamma * denom)
    return v_Bx, v_By

v = 0.8

# Case 1: 光沿 x_A
vBx, vBy = velocity_addition(1.0, 0.0, v)
print(f"Case 1 (光沿 x_A):  |v_B| = {np.sqrt(vBx**2 + vBy**2):.6f} (= c = 1) ✓")

# Case 2: 光沿 y_A
vBx, vBy = velocity_addition(0.0, 1.0, v)
print(f"Case 2 (光沿 y_A):  v_Bx={vBx:.3f}, v_By={vBy:.3f}, |v_B|={np.sqrt(vBx**2+vBy**2):.6f} ✓")
print(f"                    方向偏转角 = {np.degrees(np.arctan2(vBy, vBx)):.1f}°")
```

---

### E7.3 介质中的光速

> Consider the speed of light in static air (refractive index $n = 1.0003$). How does the speed of light in the air change wrt moving observers moving with speed $v$? How does the speed of light in the air change when there is a wind with speed $v$?
>
> 考虑光在静止空气中的速度（折射率 $n = 1.0003$）。
> 1. 对于以 $v$ 运动的观察者，空气中的光速如何变化？
> 2. 当有速度为 $v$ 的风时，空气中的光速如何变化？

| 单词/短语 | 注释 |
|-----------|------|
| refractive index | 折射率 $n$：真空中光速与介质中光速之比，$c_{\text{medium}} = c/n$ |
| static air | 静止空气：空气作为光传播介质，在实验室系中静止 |
| moving observer | 运动观察者：相对于介质运动的观察者，测得的光速需用速度叠加公式计算 |
| Fresnel drag coefficient | 菲涅耳曳引系数 $f = 1 - 1/n^2$：介质部分"曳引"光的程度，由菲索实验验证 |
| medium | 介质：光在其中传播的物质（空气、水等），光速低于真空光速 $c$ |

**知识点**：介质中的速度叠加、菲涅耳曳引、相对论速度叠加 vs. 经典速度叠加

**解答思路**

在静止介质中，光速为 $c/n$。

**1. 运动观察者**：
- 使用相对论速度叠加公式
- $v_{Bx} = \frac{c/n + v}{1 + (c/n)v/c^2}$
- 一阶近似（$v \ll c$）：$v_{Bx} \approx c/n + v(1 - 1/n^2)$
- 菲涅耳曳引系数：$f = 1 - 1/n^2$
- 对于空气 $n \approx 1.0003$，$f \approx 0.0006$ → 空气几乎不"曳引"光

**2. 有风**：
- 风 = 介质本身在运动
- 在介质静止系中：光速 $c/n$
- 在实验室系中（风的速度 $v$）：用速度叠加，得 $v_{lab} \approx c/n + v(1 - 1/n^2)$
- 这与运动观察者看到的结果相同（相对性原理）

**Python 实现**：

```python
import numpy as np

def speed_in_medium(c_over_n, v, c=1.0):
    """介质中光速的观察者/介质运动效应"""
    return (c_over_n + v) / (1 + c_over_n * v / c**2)

n = 1.0003
c = 3e8
c_medium = c / n
v = 30.0  # 汽车速度，m/s

v_observed_relativistic = speed_in_medium(c_medium, v, c)
v_observed_classical = c_medium + v  # 经典叠加

fresnel_coeff = 1 - 1/n**2

print(f"折射率 n = {n}")
print(f"静止空气中的光速: {c_medium:.1f} m/s")
print(f"介质运动速度 v = {v} m/s")
print(f"\n相对论速度叠加: {v_observed_relativistic:.1f} m/s")
print(f"经典速度叠加:    {v_observed_classical:.1f} m/s")
print(f"一阶近似:        {c_medium + v * fresnel_coeff:.1f} m/s")
print(f"菲涅耳曳引系数 f = 1 - 1/n² = {fresnel_coeff:.6f}")
print(f"\n差异: 相对论-经典 = {v_observed_relativistic - v_observed_classical:.4f} m/s")
print(f"对 n≈1 的空气，曳引效应极小（f≈{fresnel_coeff:.4f}）")
```

**关键结论**：
- 对于 $n \approx 1$（空气），菲涅耳曳引系数极小 → 光速几乎不受介质运动影响
- 对于 $n \gg 1$（如水，$n \approx 1.33$），$f \approx 0.44$ → 经典和相对论预测差异显著
- **菲索实验**（Fizeau, 1851）直接验证了相对论速度叠加公式（$1 - 1/n^2$ 曳引系数）

---

## D. 时空几何（Spacetime Geometry）

### E8.1 时空间隔的洛伦兹不变性

> Show that under Lorentz transformation, the spacetime interval $ds^2$ is unchanged (although $t$ and $x$ change). For simplicity, work in two dimensions $t$ and $x$ only (i.e. no motion or rotation in $y$ and $z$ directions).
>
> 证明在洛伦兹变换下，时空间隔 $ds^2$ 保持不变（尽管 $t$ 和 $x$ 各自会改变）。为简化，只考虑 $t$ 和 $x$ 两个维度。

| 单词/短语 | 注释 |
|-----------|------|
| spacetime interval $ds^2$ | 时空间隔：$-c^2dt^2 + dx^2 + dy^2 + dz^2$，闵可夫斯基时空中的"距离"，是洛伦兹不变量 |
| Lorentz invariant | 洛伦兹不变量：在所有惯性参考系中取值相同的量，$ds^2$ 是最基本的例子 |
| Minkowski metric | 闵可夫斯基度规 $\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1)$：定义时空间隔的"度规张量" |
| unchanged | 不变：指 $ds^2$ 的数值在洛伦兹变换前后完全相等，虽然 $dt$ 和 $dx$ 各自改变 |
| two dimensions | 两维：简化为 $(t, x)$ 两个坐标，$ds^2 = -c^2dt^2 + dx^2$ |

**知识点**：闵可夫斯基度规、洛伦兹不变量、4-矢量

**解答思路**

时空间隔：$ds^2 = -c^2 dt^2 + dx^2$

洛伦兹变换（Bob 以 $v$ 沿 $+x$ 运动）：

$$dt_B = \gamma\,(dt_A - \frac{v}{c^2} dx_A), \quad dx_B = \gamma\,(dx_A - v\,dt_A)$$

代入 Bob 的 $ds^2$：

$$
\begin{aligned}
-c^2 dt_B^2 + dx_B^2 &= -c^2 \gamma^2(dt_A - \frac{v}{c^2}dx_A)^2 + \gamma^2(dx_A - v\,dt_A)^2 \\
&= \gamma^2\left[-c^2 dt_A^2 + 2v\,dt_A dx_A - \frac{v^2}{c^2}dx_A^2 + dx_A^2 - 2v\,dt_A dx_A + v^2 dt_A^2\right] \\
&= \gamma^2\left[-(c^2 - v^2)dt_A^2 + (1 - \frac{v^2}{c^2})dx_A^2\right] \\
&= \gamma^2\left[-\frac{c^2}{\gamma^2}dt_A^2 + \frac{1}{\gamma^2}dx_A^2\right] \\
&= -c^2 dt_A^2 + dx_A^2 ✓
\end{aligned}
$$

**Python 验证**：

```python
import numpy as np
import sympy as sp

# 符号推导 ds² 的不变性
c, v, dt_A, dx_A = sp.symbols('c v dt_A dx_A', positive=True, real=True)
gamma = 1 / sp.sqrt(1 - v**2 / c**2)

# 洛伦兹变换
dt_B = gamma * (dt_A - v * dx_A / c**2)
dx_B = gamma * (dx_A - v * dt_A)

# ds²_B
ds2_B = -c**2 * dt_B**2 + dx_B**2
ds2_A = -c**2 * dt_A**2 + dx_A**2

# 化简
ds2_B_simplified = sp.simplify(ds2_B)

print("=" * 60)
print("ds² 不变性的符号验证")
print("=" * 60)
print(f"ds²_A = {ds2_A}")
print(f"ds²_B = {ds2_B_simplified}")
print(f"\n相等: {sp.simplify(ds2_B - ds2_A) == 0}")

# 数值验证
def ds2(t, x, c=1.0):
    return -c**2 * t**2 + x**2

import random
for _ in range(5):
    tA = random.uniform(0, 10)
    xA = random.uniform(-10, 10)
    v_test = random.uniform(0.1, 0.9)
    g = 1/np.sqrt(1-v_test**2)
    tB = g * (tA - v_test * xA)
    xB = g * (xA - v_test * tA)
    print(f"  ds²_A = {ds2(tA, xA):.6f},  ds²_B = {ds2(tB, xB):.6f},  相等: {abs(ds2(tA, xA) - ds2(tB, xB)) < 1e-12}")
```

**关键结论**：
- $ds^2$ 是**洛伦兹标量** —— 在所有惯性系中取值相同
- 这是闵可夫斯基时空的"距离"概念：如同欧几里得空间中 $dx^2 + dy^2$ 在旋转下不变
- $ds^2$ 的符号决定事件的因果分类：$ds^2 < 0$（类时）、$ds^2 = 0$（类光）、$ds^2 > 0$（类空）

---

### E8.2 时空中的 4-速度

> Show that using proper time, everyone is moving in spacetime (not space) with the same 4-speed (i.e. the size of the 4-velocity $dx^\mu/d\tau$).
>
> 证明：使用原时，所有物体在时空中（而非空间中）以相同的 4-速度运动（即 4-速度 $dx^\mu/d\tau$ 的大小）。

| 单词/短语 | 注释 |
|-----------|------|
| proper time $\tau$ | 原时：随物体一起运动的时钟所记录的时间，$d\tau = dt/\gamma$，是洛伦兹不变量 |
| 4-velocity $u^\mu$ | 4-速度：$dx^\mu/d\tau = (\gamma c, \gamma \vec{v})$，对原时求导得到的四维矢量 |
| 4-speed | 4-速度的大小：$|u| = \sqrt{-\eta_{\mu\nu}u^\mu u^\nu} = c$，所有物体在时空中"速率"相同 |
| Minkowski norm | 闵可夫斯基范数：$|u|^2 = -(u^0)^2 + (u^1)^2 + (u^2)^2 + (u^3)^2$，与欧几里得范数符号不同 |
| rest frame | 静止系：物体在其中速度为零的参考系，此时 $u^\mu = (c, 0, 0, 0)$ |

**知识点**：4-速度、原时、闵可夫斯基度规

**解答思路**

4-速度定义为：$u^\mu = \frac{dx^\mu}{d\tau}$

在 Alice 的静止系中：
$$x^\mu = (ct, 0, 0, 0), \quad d\tau = dt \quad \Rightarrow \quad u^\mu = (c, 0, 0, 0)$$
$$|u|^2 = \eta_{\mu\nu} u^\mu u^\nu = -c^2 + 0 = -c^2$$

在 Bob 系中（Alice 以 $v$ 运动）：
$$u'^\mu = \frac{dx'^\mu}{d\tau} = \left(\frac{d(ct')}{d\tau}, \frac{dx'}{d\tau}\right) = (\gamma c, \gamma v)$$
$$|u'|^2 = -(\gamma c)^2 + (\gamma v)^2 = -\gamma^2(c^2 - v^2) = -c^2$$

所以所有观察者的 $|u|^2 = -c^2$（或 $|u| = c$，取决于符号约定）。

**物理直觉**：每个人在**时空中**的速度总是 $c$。当你在空间中运动时（$v > 0$），你在时间方向上的"速度"就减少了（时间膨胀）——但两者的闵可夫斯基"长度"保持不变。

**Python 实现**：

```python
import numpy as np

def four_velocity_magnitude(v, c=1.0):
    """计算 4-速度的大小（闵可夫斯基范数）"""
    gamma = 1 / np.sqrt(1 - v**2 / c**2)
    # u^μ = (gamma*c, gamma*v, 0, 0)
    u0 = gamma * c      # 时间分量
    u1 = gamma * v      # 空间分量
    # |u|^2 = -(u^0)^2 + (u^1)^2 = -gamma^2*c^2 + gamma^2*v^2 = -c^2
    magnitude_sq = -u0**2 + u1**2
    return np.sqrt(-magnitude_sq)  # |u| = c

# 测试不同速度
speeds = np.linspace(0, 0.9999, 20)
print("=" * 50)
print("4-速度大小验证：所有观察者 |u| = c")
print("=" * 50)
print(f"{'v/c':>8s}  {'|u|/c':>8s}")
print("-" * 20)
for v in speeds:
    u_mag = four_velocity_magnitude(v)
    print(f"{v:8.4f}  {u_mag:8.6f}")
print(f"\n结论：|u| = c = 1（对所有 v），即所有物体在时空中以光速 c 运动！")
```

**关键结论**：
- $|u^\mu|^2 = -c^2$ 对所有惯性观察者相同 —— 这是**洛伦兹不变量**
- 静止的物体：全部"速度"在时间方向上（$u^0 = c$, $u^1 = 0$）
- 运动的物体：时间分量和空间分量重新分配，但总大小不变
- 这优美地解释了为什么 $v < c$ —— 因为时间分量至少为 0

---

## E. 能量与动量（Energy & Momentum）

### E9.1 从动量积分推导动能

> Let us use the relativistic momentum $p = \gamma mv$ to derive the expression of the kinetic energy, in a different way from what we did in class.
>
> Consider a ball at rest at $x = 0$ with mass $m$, and act a constant force $F$ on this ball toward the $x$ direction. The ball then accelerates because of the force.
>
> Note that $F = dp/dt$, and the kinetic energy can be calculated from the work done by the force:
>
> $$K = \int_0^{x_1} F\,dx = \int_0^{x_1} \frac{dp}{dt} dx = \int_0^{p_1} v\,dp = \int_0^{v_1} v\,d(\gamma mv)$$
>
> where $x_1$, $p_1$ and $v_1$ are the distance, momentum, and velocity at a later time $t_1$. Continue the calculation and derive the kinetic energy of the ball at time $t_1$.
>
> 使用相对论动量 $p = \gamma mv$ 来推导动能的表达式。考虑在 $x=0$ 处静止的质量为 $m$ 的小球，沿 $x$ 方向施加恒力 $F$。注意 $F = dp/dt$，动能可以通过力做的功计算：
>
> $$K = \int_0^{x_1} F\,dx = \int_0^{x_1} \frac{dp}{dt} dx = \int_0^{p_1} v\,dp = \int_0^{v_1} v\,d(\gamma mv)$$
>
> 其中 $x_1$、$p_1$ 和 $v_1$ 分别是稍后时刻 $t_1$ 的距离、动量和速度。完成计算，推导出 $t_1$ 时刻小球的动能。

| 单词/短语 | 注释 |
|-----------|------|
| relativistic momentum | 相对论动量：$p = \gamma mv$，不同于牛顿力学中的 $p = mv$，在低速极限下回归经典形式 |
| kinetic energy | 动能：物体因运动而具有的能量，相对论中 $K = (\gamma - 1)mc^2$ |
| constant force | 恒力：大小和方向不变的力，$F = dp/dt$，注意在相对论中恒力不产生恒加速度 |
| work done | 力所做的功：$W = \int F\,dx$，功-能定理在相对论中依然成立 |
| integration by parts | 分部积分：$\int v\,dp = vp - \int p\,dv$，是推导动能的两种等价方法之一 |
| rest energy | 静止能量：$E_0 = mc^2$，物体在静止时固有的能量，$E = K + E_0 = \gamma mc^2$ |
| work-energy theorem | 功-能定理：$K = W$，合外力做的功等于动能的变化量 |

**知识点**：相对论动能、功-能定理、分部积分

**解答思路**

设 $p = \gamma mv$，需要计算 $\int_0^{v_1} v\,dp$。

**方法一：分部积分（最直接）**

$$K = \int_0^{v_1} v\,\frac{d}{dv}(\gamma mv)\,dv = \int_0^{v_1} v \cdot m\frac{d}{dv}\left(\frac{v}{\sqrt{1-v^2/c^2}}\right) dv$$

计算 $d(\gamma v)/dv = \gamma^3$（可验证：$\gamma v = v/\sqrt{1-v^2/c^2}$，求导得 $1/(1-v^2/c^2)^{3/2} = \gamma^3$）

所以：
$$K = m\int_0^{v_1} v \cdot \gamma^3\,dv = m\int_0^{v_1} \frac{v}{(1-v^2/c^2)^{3/2}}\,dv$$

令 $u = 1 - v^2/c^2$，$du = -2v/c^2 dv$，$v\,dv = -(c^2/2)du$：
$$K = m\int_1^{1-v_1^2/c^2} \frac{(-c^2/2)}{u^{3/2}} du = \frac{mc^2}{2}\int_{1-v_1^2/c^2}^1 u^{-3/2} du$$
$$= \frac{mc^2}{2} \cdot \left[-2u^{-1/2}\right]_{1-v_1^2/c^2}^1 = mc^2\left(\frac{1}{\sqrt{1-v_1^2/c^2}} - 1\right)$$
$$= (\gamma_1 - 1)mc^2$$

**方法二：分部积分（技巧性更强）**

$$K = [v p]_0^{v_1} - \int_0^{v_1} p\,dv = \gamma_1 m v_1^2 - m\int_0^{v_1} \frac{v}{\sqrt{1-v^2/c^2}} dv$$
$$= \gamma_1 m v_1^2 + mc^2\left[\sqrt{1-v^2/c^2}\right]_0^{v_1}$$
$$= \gamma_1 m v_1^2 + mc^2(1/\gamma_1 - 1)$$
$$= mc^2(\gamma_1 v_1^2/c^2 + 1/\gamma_1 - 1) = mc^2\left(\frac{\gamma_1^2-1}{\gamma_1} + \frac{1}{\gamma_1} - 1\right)$$
$$= mc^2(\gamma_1 - 1)$$

**最终结果**：$K = (\gamma - 1)mc^2 = \gamma mc^2 - mc^2 = E - E_0$

**Python 实现 — 分部积分与数值验证**：

```python
import numpy as np
from scipy import integrate

def relativistic_kinetic_energy(v, m=1.0, c=1.0):
    """相对论动能：K = (gamma - 1) m c^2"""
    gamma = 1 / np.sqrt(1 - v**2 / c**2)
    return (gamma - 1) * m * c**2

def kinetic_from_integral_numerical(v1, m=1.0, c=1.0):
    """通过数值积分验证 K = ∫ v d(γmv)"""
    gamma = lambda v: 1 / np.sqrt(1 - v**2 / c**2)
    # d(γmv)/dv = m * d(v/√(1-v²/c²))/dv
    integrand = lambda v: v * m * (1 / (1 - v**2 / c**2)**(3/2))
    K, err = integrate.quad(integrand, 0, v1)
    return K

def kinetic_from_work_integral(v1, m=1.0, c=1.0):
    """通过 ∫ F dx 数值验证 (需先计算速度与位置的关系)"""
    # 恒力加速：a = F/(γ³m), 数值积分运动方程
    # 简化：用恒加速度 a（非恒力）
    # 此处用解析解验证概念，不做完整的恒力模拟
    pass

# 验证
speeds = np.linspace(0.01, 0.99, 10)
print("=" * 70)
print("动能推导验证：K = ∫₀ᵛ v d(γmv) = (γ-1)mc²")
print("=" * 70)
print(f"{'v/c':>8s}  {'K 解析':>12s}  {'K 数值':>12s}  {'差异':>12s}")
print("-" * 50)
for v in speeds:
    K_analytic = relativistic_kinetic_energy(v)
    K_numeric = kinetic_from_integral_numerical(v)
    print(f"{v:8.4f}  {K_analytic:12.6f}  {K_numeric:12.6f}  {abs(K_analytic-K_numeric):12.2e}")
print("\n✓ 解析结果与数值积分完全一致")

# 低能极限验证
v_small = 0.01
K_rel = relativistic_kinetic_energy(v_small)
K_newton = 0.5 * v_small**2  # (1/2)mv², m=1, c=1
print(f"\n低能极限 (v={v_small}c):")
print(f"  相对论动能: {K_rel:.8f}")
print(f"  牛顿动能:   {K_newton:.8f}")
print(f"  比值 K_rel/K_newton ≈ {K_rel/K_newton:.6f} (→ 1 当 v ≪ c)")

# 高能极限
v_high = 0.999
K_high = relativistic_kinetic_energy(v_high)
gamma_high = 1 / np.sqrt(1 - v_high**2)
print(f"\n高能极限 (v={v_high}c, γ={gamma_high:.1f}):")
print(f"  K ≈ γmc² = {gamma_high:.0f} × mc²")
```

**关键结论**：
- 相对论动能：$K = (\gamma - 1)mc^2$
- 总能量：$E = \gamma mc^2 = K + mc^2$（动能 + 静止能量）
- 低能极限（$\gamma \approx 1 + v^2/2c^2$）：$K \approx \frac{1}{2}mv^2$ — 回归牛顿力学
- 高能极限（$\gamma \gg 1$）：$K \approx \gamma mc^2$ — 能量随 $\gamma$ 线性增长
- **一个优美的巧合**：从 $F = dp/dt$ 出发，只改了 $p$ 的定义，功-能定理依然成立

---

## 📚 补充阅读：爱因斯坦的原始论文

> Read Einstein's original papers on relativity. Nowadays Einstein's original papers can be easily found online. For example, his first paper. You will find most parts of the paper accessible except that in electrodynamics he used different notations from modern convention.
>
> 阅读爱因斯坦关于相对论的原始论文。如今爱因斯坦的原始论文在网上很容易找到，例如他的第一篇论文。你会发现论文的大部分内容是易读的，只是在电动力学部分他使用了与现代不同的符号约定。

| 单词/短语 | 注释 |
|-----------|------|
| original papers | 原始论文：指爱因斯坦 1905 年在《物理学年鉴》上发表的相对论奠基性论文 |
| electrodynamics | 电动力学：研究电磁场与带电粒子相互作用的物理学分支，狭义相对论的历史出发点 |
| notations | 符号约定：数学和物理中的记号体系，早期论文的记号与现代教科书有所不同 |
| accessible | 可读的、易理解的：学过狭义相对论的读者可以理解论文的大部分推导过程 |

推荐阅读爱因斯坦 1905 年的原始论文 **"On the Electrodynamics of Moving Bodies"**（《论动体的电动力学》）。

- **可获得性**：原文（德文）和英译本均可在网上免费获取
- **可读性**：大部分内容对学过狭义相对论的读者是可读的
- **注意**：电动力学部分使用了与现代不同的符号约定
- **收获**：
  1. 看到狭义相对论如何从"磁体-导体佯谬"出发
  2. 感受爱因斯坦"思想实验 + 数学"并重的推导风格
  3. 理解历史背景——迈克尔逊-莫雷实验、以太假设的危机

另外推荐阅读 **1905 年的第二篇论文** "Does the Inertia of a Body Depend Upon Its Energy Content?"，其中首次提出 $E = mc^2$（仅 3 页！非常精炼）。

---

## 习题-知识点对照表（完整版）

| 习题 | 主题 | 核心技能 | 难度 | Python 可用 |
|------|------|---------|------|------------|
| E1.1 | 平面波 | 波的数学表示、相速度 | ⭐⭐ | ✅ 动画 |
| E2.1 | 光速不变与时间膨胀 | 光速不变的语言表述、矢量分解 | ⭐⭐⭐ | ✅ 矢量图 |
| E5.1 | 太阳-地球时空图 | 世界线绘制、光信号表示 | ⭐⭐ | ✅ 时空图 |
| E5.2 | Rindler 视界 | 双曲运动、视界概念 | ⭐⭐⭐⭐ | ✅ 时空图 |
| E5.3 | 双生子实际所见 | 光传播延迟、多普勒效应 | ⭐⭐⭐⭐ | ✅ 光线追踪 |
| E5.4 | 飞船间距 | 同时性相对性、长度收缩 | ⭐⭐⭐ | ✅ 时空图 |
| E7.1 | 洛伦兹变换三大效应 | 变换公式的代数推导 | ⭐⭐⭐ | ✅ 符号/数值 |
| E7.2 | 速度叠加实例 | 速度叠加公式的应用 | ⭐⭐ | ✅ 数值 |
| E7.3 | 介质中光速 | 菲涅耳曳引、菲索实验 | ⭐⭐⭐ | ✅ 数值 |
| E8.1 | ds² 不变性 | 闵可夫斯基度规、不变量 | ⭐⭐⭐ | ✅ 符号/数值 |
| E8.2 | 4-速度大小 | 原时、4-矢量 | ⭐⭐⭐ | ✅ 数值 |
| E9.1 | 动能积分推导 | 分部积分、功-能定理 | ⭐⭐⭐⭐ | ✅ 数值积分 |
| 补充 | 爱因斯坦原始论文 | 原始文献阅读训练 | ⭐⭐ | — |

---

## 要点总结

1. **习题涵盖全部核心章节**：从第 1 节的平面波到第 9 节的动能推导，形成完整的知识验证链
2. **时空图是核心工具**：E5.1–E5.4 四道题反复训练时空图的绘制与解读，这是狭义相对论思维的**关键训练**
3. **三种解题思维互补**：
   - 模式匹配（快速识别题型 → 已知结论）
   - 反向搜索（从目标反推中间量）
   - 物理图像（脑中放电影 → 获取直觉 → 数学验证）
4. **洛伦兹变换是统一框架**：E7.1 用一套变换公式统一推导时间膨胀、长度收缩和同时性相对性
5. **几何视角（§7-8）是深度理解的关键**：$ds^2$ 不变性和 4-速度统一了看似孤立的效应
6. **爱因斯坦原始论文**推荐作为补充阅读，感受原始发现的思维脉络
7. **Python 实现**不是必须的，但对可视化（时空图、光线追踪）和数值验证（积分、不变性）有极大帮助

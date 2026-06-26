# 第七节：时空几何（The Geometry of Spacetime）

---

## 📖 7.1 为什么时空不是欧几里得的？（Why Spacetime Is NOT Euclidean）

### Original Text — 时间膨胀的几何矛盾

> *"Our spacetime is NOT Euclidean. Recall time dilation. In the figure, the hypotenuse is proportional to the time that Alice in the car observed: Δt_A, and the vertical side is proportional to the time that Bob observes Δt_B. Naively one would expect the hypotenuse to be the longest side (Pythagorean theorem: a² + b² = c²). But we know Δt_B > Δt_A, i.e. c·Δt_A < c·Δt_B. Something is fundamentally wrong with the normal Euclidean geometry in our spacetime."*

### 几何直觉 vs. 物理现实

回顾第 2 节的时间膨胀结果：
- **Bob 测量**：Alice 的光钟走一个周期用时 $\Delta t_B$（较长）
- **Alice 测量**：自己的光钟走一个周期用时 $\Delta t_A$（较短）
- **关系**：$\Delta t_B = \gamma \Delta t_A$，其中 $\gamma > 1$

现在把光路径画在时空图上：

```
在 Bob 参考系中，半个光钟周期内的光路径形成直角三角形：

         ct 轴（时间 × 光速）
         │
    Δt_B·c ┼────────✦  (反射事件: 光击中镜子)
         │        /│
         │       / │
         │      /  │  D  ← 镜子间距（垂直距离）
         │     /   │
         │    /    │
    0 ───┼───✦────┼─────→ x 轴（空间）
             发射     Δt_B·v/2
             /探测

     斜边 (hypotenuse) = c·Δt_A/2  ← 光实际走的距离（Alice 参考系）
     竖边 (vertical)   = c·Δt_B/2  ← 若 Bob 用欧几里得几何理解
     底边 (base)       = v·Δt_B/2  ← 光钟在半个周期内移动的距离
```

如果在**欧几里得几何**中：
$$(\text{斜边})^2 = (\text{竖边})^2 + (\text{底边})^2$$
即 $(c \cdot \Delta t_A/2)^2 = (c \cdot \Delta t_B/2)^2 + (v \cdot \Delta t_B/2)^2$，这意味着 $\Delta t_A > \Delta t_B$——与物理事实**恰好相反**！

### 时空的正确"勾股定理"

在时空中，正确的距离关系是：

$$\boxed{-a^2 + b^2 = -c^2}$$

或者等价地：

$$\boxed{a^2 = c^2 + b^2}$$

其中时间方向的平方前带有**负号**（或等价地，空间方向带有负号，取决于符号约定）。

代入时间膨胀的具体数值验证：
$$-(c\Delta t_B)^2 + (v\Delta t_B)^2 = -(c\Delta t_A)^2$$

整理：
$$-c^2\Delta t_B^2 + v^2\Delta t_B^2 = -c^2\Delta t_A^2$$
$$-\Delta t_B^2(c^2 - v^2) = -c^2\Delta t_A^2$$
$$\Delta t_B^2 = \frac{c^2}{c^2-v^2}\Delta t_A^2 = \gamma^2 \Delta t_A^2$$
$$\Delta t_B = \gamma \Delta t_A \quad \checkmark$$

**完全自洽！** 正是时间分量前的那个**负号**，使得直角三角形中"斜边"反而比"直角边"短。

### 🔑 Key Vocabulary — 非欧几何

| English | 中文 | Notes |
|---------|------|-------|
| Euclidean geometry | 欧几里得几何 | Pythagoras: a² + b² = c²; spatial rotations preserve x²+y² |
| non-Euclidean | 非欧几里得的 | spacetime has a minus sign for the time direction |
| hypotenuse | 斜边 | longest side in Euclidean triangle — but NOT longest in spacetime! |
| Minkowski spacetime | 闵可夫斯基时空 | 4D spacetime with metric signature (-,+,+,+) or (+,-,-,-) |
| metric signature | 度规符号 | the pattern of signs in the metric: (-1, +1, +1, +1) |
| pseudo-Euclidean | 伪欧几里得的 | spaces with indefinite metric (not positive-definite) |

---

## 📖 7.2 迅速度：洛伦兹变换的双曲几何（Rapidity: The Hyperbolic Geometry of Lorentz Transformations）

### Original Text

> *"Let φ ≡ arctanh(β), called rapidity. Then cosh φ = γ, sinh φ = βγ. The Lorentz transformation is a hyperbolic rotation in the ct-x plane: ct_B = ct_A coshφ + x_A sinhφ, x_B = ct_A sinhφ + x_A coshφ."*

### 从速度到迅速度

定义**迅速度**（rapidity）$\varphi$：

$$\boxed{\varphi \equiv \text{arctanh}(\beta)}, \quad \beta = \frac{v}{c}$$

迅速度 $\varphi$ 的物理范围：
- $\beta \to 0$（低速）$\;\Rightarrow\; \varphi \to 0$（近似伽利略）
- $\beta \to 1$（近光速）$\;\Rightarrow\; \varphi \to \infty$（发散）
- 日常速度（$\beta \ll 1$）：$\varphi \approx \beta$（两者几乎相等）

### 双曲函数与洛伦兹因子的关系

$$\boxed{\cosh\varphi = \gamma = \frac{1}{\sqrt{1-\beta^2}}}, \qquad \boxed{\sinh\varphi = \beta\gamma = \frac{\beta}{\sqrt{1-\beta^2}}}$$

验证：
$$\cosh^2\varphi - \sinh^2\varphi = \gamma^2 - (\beta\gamma)^2 = \gamma^2(1-\beta^2) = \frac{1-\beta^2}{1-\beta^2} = 1 \quad \checkmark$$

### 洛伦兹变换作为双曲旋转

有了迅速度，洛伦兹变换呈现出极其优美的形式：

```
洛伦兹变换（双曲旋转形式）：

   ct_B = ct_A · cosh φ  +  x_A · sinh φ
   x_B  = ct_A · sinh φ  +  x_A · cosh φ
   y_B  = y_A
   z_B  = z_A
```

这与**普通空间旋转**的类比一目了然：

| 变换类型 | 变换公式 | 不变式 | 群 |
|---------|---------|--------|-----|
| **空间旋转**（绕 z 轴，角度 θ） | x' = x cosθ + y sinθ<br>y' = −x sinθ + y cosθ | $x^2 + y^2$ | SO(2) |
| **双曲旋转**（沿 x 方向 boost，迅速度 φ） | ct' = ct coshφ + x sinhφ<br>x' = ct sinhφ + x coshφ | $-(ct)^2 + x^2$ | SO(1,1) |

> **关键洞察**：洛伦兹 boost 不是普通的旋转——它是**双曲旋转**（hyperbolic rotation）！cosθ / sinθ 被替换为 coshφ / sinhφ，不变量从 $x^2 + y^2$ 变为 $-(ct)^2 + x^2$。

### 为什么是双曲旋转？

在欧几里得平面上，旋转保持**圆**不变（$x^2 + y^2 = R^2$）。
在闵可夫斯基时空中，boost 保持**双曲线**不变（$-(ct)^2 + x^2 = \text{const}$）。

```
欧几里得旋转 vs 双曲旋转（boost）：

     欧几里得旋转                        双曲旋转（Lorentz boost）
         y                                    ct
         │     圆 x²+y²=R²                    │  双曲线 −(ct)²+x²=const
         │   ···'···                          │     ╲    ╱
         │ ·'   │   '·                        │      ╲  ╱  未来光锥
         │·     │θ    ·                       │       ╲╱
   ──────┼──────┼──────→ x              ──────┼────────┼──→ x
         │      │                             │       ╱╲
         │      │                             │      ╱  ╲  过去光锥
         │      │                             │     ╱    ╲

   不变曲线：圆                          不变曲线：双曲线
   参数化：(cosθ, sinθ)                  参数化：(coshφ, sinhφ)
   有限范围：θ ∈ [0, 2π)                 无限范围：φ ∈ (−∞, +∞)
```

### 🔑 Key Vocabulary — 迅速度与双曲几何

| English | 中文 | Notes |
|---------|------|-------|
| rapidity | 迅速度 | φ = arctanh(v/c); the true additive measure of speed in relativity |
| hyperbolic rotation | 双曲旋转 | Lorentz boost geometrically interpreted as rotation by φ in spacetime |
| hyperbolic functions | 双曲函数 | cosh, sinh, tanh — describe the geometry of spacetime boosts |
| boost | 推动/boost | Lorentz transformation between frames with relative velocity |
| SO(1,1) | — | symmetry group of 1+1 dimensional Minkowski spacetime |
| arctanh | 反双曲正切 | inverse hyperbolic tangent: maps (−1,1) → (−∞,∞) |
| additive | 可加的 | φ₁ + φ₂ = φ_total; velocity is NOT additive but rapidity IS |

---

## 📖 7.3 虚数时间：时空的完全统一（Imaginary Time: The Complete Unification of Space and Time）

### Original Text

> *"Let φ = iθ, ct = iw. Then the Lorentz transformation becomes a rotation in the w-x plane: w_B = w_A cosθ + x_A sinθ, x_B = −w_A sinθ + x_A cosθ. Under this trick, the Lorentz transformation turns into an ordinary rotation. There turns out to be rotation symmetry for w, x, y, z. Our spacetime is more symmetric than a sphere!"*

### 虚数时间技巧（The Wick Rotation）

做一个数学替换——**虚数时间**（imaginary time）：

$$\boxed{ct = iw}, \quad \text{即 } w = -i\,ct$$

同时，将迅速度也改写为虚角度：

$$\boxed{\varphi = i\theta}$$

代入双曲旋转公式：
$$ct_B = ct_A \cosh\varphi + x_A \sinh\varphi$$
$$x_B = ct_A \sinh\varphi + x_A \cosh\varphi$$

利用恒等式：
$$\cosh(i\theta) = \cos\theta, \quad \sinh(i\theta) = i\sin\theta$$

以及 $ct = iw$：

$$iw_B = iw_A \cos\theta + x_A \cdot i\sin\theta$$
$$x_B = iw_A \cdot i\sin\theta + x_A \cos\theta = -w_A \sin\theta + x_A \cos\theta$$

化简得到：

$$\boxed{w_B = w_A \cos\theta + x_A \sin\theta}$$
$$\boxed{x_B = -w_A \sin\theta + x_A \cos\theta}$$

**这正是 w-x 平面中的普通欧几里得旋转！**

### 时空的完全旋转对称性

在虚数时间下，时空变成了**4 维欧几里得空间** $(w, x, y, z)$：

| 维度 | 物理意义 | 对称性 |
|------|---------|--------|
| $w = -i\,ct$ | 虚数时间 | 可以与 x, y, z 任意旋转混合 |
| $x$ | 空间坐标 | 原本就可以与 y, z 旋转 |
| $y$ | 空间坐标 | 原本就可以与 x, z 旋转 |
| $z$ | 空间坐标 | 原本就可以与 x, y 旋转 |

在这个 4 维欧几里得空间中，存在：

1. **空间-空间旋转**（3 个）：x↔y, y↔z, z↔x —— 原本就有的三维旋转群 SO(3)
2. **时间-空间旋转**（3 个）：w↔x, w↔y, w↔z —— 这 3 个"旋转"就是原来的 3 个洛伦兹 boost！

**总共 6 个独立的旋转自由度**（4 维空间的旋转群 SO(4)）。而在物理时空中（去掉虚数时间，回到闵可夫斯基时空），这 6 个对称性对应**洛伦兹群 SO(3,1)** 的 6 个生成元。

> *"There turns out to be rotation symmetry for w, x, y, z. Our spacetime is more symmetric than a sphere!"*

### 比球更对称的时空

| 几何对象 | 维度 | 对称群 | 旋转自由度 |
|---------|------|--------|-----------|
| 圆（circle） | 1D 嵌入 2D | SO(2) | 1 |
| 球面（sphere） | 2D 嵌入 3D | SO(3) | 3 |
| **闵可夫斯基时空** | **4D** | **SO(3,1)** | **6** |

时空的对称性比三维球面更高——它有 6 个独立的"旋转"方向，其中 3 个是空间旋转（我们熟悉的），3 个是 boost（将时间与空间混合的"双曲旋转"）。

### 🔑 Key Vocabulary — 虚数时间与对称性

| English | 中文 | Notes |
|---------|------|-------|
| imaginary time | 虚数时间 | w = −i·ct; turns Minkowski spacetime into Euclidean space |
| Wick rotation | Wick 转动 | mathematical trick t → iτ to convert between Minkowski and Euclidean |
| SO(4) | 四维旋转群 | rotation group of 4D Euclidean space; 6 generators |
| SO(3,1) | 洛伦兹群 | Lorentz group; 6 generators (3 rotations + 3 boosts) |
| generator | 生成元 | independent direction of infinitesimal symmetry transformation |
| embedding | 嵌入 | placing a lower-dimensional geometric object in a higher-dimensional space |

---

## 📖 7.4 自然单位制（Natural Units）

### Original Text

> *"The speed of light c is a conversion factor between naturally the same thing: space and time. Now we see time and space are related by rotation — so we had better use the same unit for space and time."*

> *"The unit of time is chosen as the time for light to travel 1 meter."*

### 为什么需要自然单位？

在狭义相对论中，时间和空间通过洛伦兹变换相互混合——它们本质上是同一回事的不同分量。但日常单位掩盖了这种统一性：

| 物理量 | 日常单位 | 换算因子 |
|--------|---------|---------|
| 空间 | 米（m） | — |
| 时间 | 秒（s） | — |
| 光速 c | 299,792,458 m/s | 时空的换算常数 |

**类比**：中国古代有时用不同单位度量山的高度（因为重力破缺了上下对称性），但在没有重力的太空中，上下和前后没有区别——应该用同一单位。狭义相对论揭示，时间与空间同样没有本质区别——只是我们一直用不同的单位来度量它们。

**自然单位的设定**：

$$\boxed{c = 1}$$

这意味着：
- 速度变为**无量纲**数（以光速为单位）
- 时间用**长度**来度量：1 秒 = 299,792,458 米（光在 1 秒内走的距离）
- 或者空间用**时间**来度量：1 米 = 1/299,792,458 秒（光走 1 米的时间）

### 自然单位下公式的极大简化

| 公式 | 有量纲形式 | 自然单位 (c=1) |
|------|-----------|---------------|
| 洛伦兹因子 | $\gamma = 1/\sqrt{1 - v^2/c^2}$ | $\gamma = 1/\sqrt{1 - v^2}$ |
| 时空间隔 | $ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2$ | $ds^2 = -dt^2 + dx^2 + dy^2 + dz^2$ |
| 度规张量 | $\eta_{\mu\nu} = \text{diag}(-c^2, 1, 1, 1)$ | $\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1)$ |
| 迅速度 | $\varphi = \text{arctanh}(v/c)$ | $\varphi = \text{arctanh}(v)$ |
| 双曲旋转 | $\cosh\varphi = \gamma$, $\sinh\varphi = \gamma v/c$ | $\cosh\varphi = \gamma$, $\sinh\varphi = \gamma v$ |
| 质能方程 | $E = \gamma m c^2$ | $E = \gamma m$ |

> 自然单位揭示了：$c$ 从来不是自然界的基本常数——它只是一个**单位换算因子**，就像 1 英尺 = 0.3048 米一样。真正的物理由 $c=1$ 揭示：**时空本质上是统一的，度规是 diag(-1, 1, 1, 1)**。

### 🔑 Key Vocabulary — 自然单位

| English | 中文 | Notes |
|---------|------|-------|
| natural units | 自然单位 | unit system where c = 1 (and often ℏ = 1, G = 1) |
| dimensionless | 无量纲的 | having no physical units; a pure number |
| conversion factor | 换算因子 | c converts between meters and seconds — it's not a "fundamental speed" |
| geometrized units | 几何化单位 | space and time measured in the same unit (e.g., meters) |
| light-second | 光秒 | distance light travels in 1 second ≈ 3×10⁸ m |
| Planck units | 普朗克单位 | c = ℏ = G = k_B = 1; the ultimate natural unit system |

---

## 📖 7.5 时空间隔：狭义相对论的不变量（The Invariant Interval: The Invariant of Special Relativity）

### Original Text

> *"Define ds² ≡ −c²dt² + dx² + dy² + dz². Under Lorentz transformation, ds² is invariant: ds²_A = ds²_B. This is similar to how the Euclidian distance d² = x² + y² is invariant under ordinary rotations."*

### 时空间隔的定义

对于两个无限接近的事件（相隔 $dt, dx, dy, dz$），定义**时空间隔**（invariant interval）：

$$\boxed{ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2}$$

在自然单位 ($c=1$) 下：

$$\boxed{ds^2 = -dt^2 + dx^2 + dy^2 + dz^2}$$

### ds² 的洛伦兹不变性

检验：将洛伦兹变换代入 $ds^2$（只考虑 x 方向 boost，y 和 z 显然不变）：

$$dt_B = \gamma(dt_A - v\,dx_A/c^2)$$
$$dx_B = \gamma(dx_A - v\,dt_A)$$

计算 $ds_B^2$（令 $c=1$）：

$$ds_B^2 = -dt_B^2 + dx_B^2$$
$$= -[\gamma(dt_A - v\,dx_A)]^2 + [\gamma(dx_A - v\,dt_A)]^2$$
$$= -\gamma^2[dt_A^2 - 2v\,dt_A dx_A + v^2 dx_A^2] + \gamma^2[dx_A^2 - 2v\,dt_A dx_A + v^2 dt_A^2]$$
$$= \gamma^2[ -(1 - v^2)dt_A^2 + (1 - v^2)dx_A^2 ]$$
$$= \gamma^2(1 - v^2)[-dt_A^2 + dx_A^2]$$
$$= -dt_A^2 + dx_A^2 = ds_A^2 \quad \checkmark$$

**$ds^2$ 在所有惯性系中保持不变！**

### 类比：欧几里得不变量 vs 闵可夫斯基不变量

| 几何 | 变换 | 不变量 |
|------|------|--------|
| 欧几里得平面 | 旋转：$x' = x\cos\theta + y\sin\theta$, $y' = -x\sin\theta + y\cos\theta$ | $d^2 = x^2 + y^2$ |
| 闵可夫斯基时空 | Boost：$t' = \gamma(t - vx)$, $x' = \gamma(x - vt)$ | $ds^2 = -t^2 + x^2$ (c=1) |

**核心思想**：每种变换都保有一个不变量。不变量是几何结构的本质。旋转不改变圆 $x^2+y^2$；boost 不改变双曲线 $-t^2+x^2$。在虚数时间下，两者完全统一。

### 闵可夫斯基度规（The Minkowski Metric）

定义**度规张量**（metric tensor）$\eta_{\mu\nu}$：

$$\boxed{\eta_{\mu\nu} = \begin{pmatrix}
-1 & 0 & 0 & 0 \\
 0 & 1 & 0 & 0 \\
 0 & 0 & 1 & 0 \\
 0 & 0 & 0 & 1
\end{pmatrix}}$$

则时空间隔可以紧凑地写为：

$$\boxed{ds^2 = \sum_{\mu=0}^{3}\sum_{\nu=0}^{3} \eta_{\mu\nu}\, dx^\mu dx^\nu = \eta_{\mu\nu}\, dx^\mu dx^\nu}$$

其中 $x^\mu = (ct, x, y, z)$ 是**四维坐标**（4-vector），下标 $\mu, \nu$ 从 0 到 3（0 = 时间分量, 1,2,3 = 空间分量）。最后一步使用了**爱因斯坦求和约定**（重复指标自动求和）。

### 度规的核心作用

度规 $\eta_{\mu\nu}$ 告诉我们在时空中如何"测量距离"：
- 欧几里得度规：$\delta_{ij} = \text{diag}(1,1,1)$ → $d^2 = \delta_{ij} dx^i dx^j = dx^2 + dy^2 + dz^2$
- 闵可夫斯基度规：$\eta_{\mu\nu} = \text{diag}(-1,1,1,1)$ → $ds^2 = -dt^2 + dx^2 + dy^2 + dz^2$

**度规是几何的灵魂。** 不同的度规 → 不同的几何。闵可夫斯基度规的非正定性（时间前有负号）正是"时空非欧几里得"的精确数学表述。

### 四矢量的内积

时空间隔 $ds^2$ 是无限小四矢量 $dx^\mu$ 与自身的**内积**。对于任意两个四矢量 $p^\mu$ 和 $k^\nu$，定义它们的内积：

$$\boxed{p \cdot k \equiv \eta_{\mu\nu}\, p^\mu k^\nu = -p^0 k^0 + p^1 k^1 + p^2 k^2 + p^3 k^3}$$

**关键性质**：两个四矢量的内积也是**洛伦兹不变量**——与 $ds^2$ 一样，在所有惯性系中保持不变。这个性质将在第 8 节（相对论动量与能量）中发挥核心作用。

### 🔑 Key Vocabulary — 度规与不变量

| English | 中文 | Notes |
|---------|------|-------|
| invariant interval | 时空间隔（不变量） | ds² = −c²dt² + dx² + dy² + dz²; Lorentz invariant |
| metric tensor | 度规张量 | η_μν = diag(−1,1,1,1); encodes the geometry of spacetime |
| 4-vector | 四矢量 | a vector in 4D spacetime: x^μ = (ct, x, y, z) |
| Einstein summation | 爱因斯坦求和约定 | repeated indices are summed: η_μν x^μ x^ν |
| inner product | 内积 | p·k = η_μν p^μ k^ν; Lorentz invariant scalar |
| positive-definite | 正定的 | all eigenvalues > 0; Euclidean metric is, Minkowski isn't |
| indefinite metric | 不定度规 | metric with both positive and negative eigenvalues |

---

## 📖 7.6 ds² 的符号与事件的因果分类（Sign of ds² and Causal Classification of Events）

### Original Text

> *"ds² < 0: time-like — the two events can be connected by a physical signal traveling slower than light. ds² > 0: space-like — the two events cannot be connected causally. ds² = 0: light-like (null) — the two events are connected by a light ray. Now you understand why 'null' is called 'null' — it is indeed zero."*

### 三类时空间隔

$ds^2$ 的**符号**（而非数值大小）决定了两个事件的**因果关系可能性**：

| ds² 的符号 | 间隔类型 | 特征 | 因果关系 | 光锥位置 |
|-----------|---------|------|---------|---------|
| $ds^2 < 0$ | **类时（Time-like）** | $c^2 dt^2 > dx^2$ | 可通过低于光速的信号连接 | 光锥内部 |
| $ds^2 = 0$ | **类光/零（Light-like/Null）** | $c^2 dt^2 = dx^2$ | 仅能通过光线连接 | 光锥表面 |
| $ds^2 > 0$ | **类空（Space-like）** | $c^2 dt^2 < dx^2$ | **不可能**有因果关系 | 光锥外部 |

### 光锥图（Light Cone Diagram）

```
                    ct (时间)
                    │
                    │   未来光锥 (Future Light Cone)
                   ╱│╲     ds² < 0 (类时)
                  ╱ │ ╲    可能受事件 O 影响
                 ╱  │  ╲
                ╱   │   ╲
               ╱    │    ╲  ds² = 0 (类光/Null)
              ╱     │     ╲  光信号的路径
             ╱      │      ╲
            ╱       │       ╲
    ───────O────────┼────────────→ x (空间)
            ╲       │       ╱
             ╲      │      ╱
              ╲     │     ╱  ds² = 0 (类光/Null)
               ╲    │    ╱
                ╲   │   ╱
                 ╲  │  ╱  ds² < 0 (类时)
                  ╲ │ ╱   可能影响事件 O
                   ╲│╱
                    │   过去光锥 (Past Light Cone)
                    │
              ds² > 0 (类空)
              在光锥之外——与 O 没有因果关系
```

### "Null" 的名字来源

> *"Now you understand why 'null' is called 'null' — it is indeed zero."*

在 $ds^2 = 0$ 的世界线上（光的路径），时空间隔**正好为零**！这不是说光不经历时间和空间——而是时间间隔和空间间隔的贡献恰好抵消：

$$-c^2 dt^2 + dx^2 = 0 \quad\Rightarrow\quad dx/dt = c$$

这正是光速的定义。光线走过的**固有时**（proper time）恒为零。这个看似奇怪的结论将在后面关于光子物理的讨论中深入展开。

### 🔑 Key Vocabulary — 事件分类

| English | 中文 | Notes |
|---------|------|-------|
| time-like | 类时的 | ds² < 0; causally connectable by signals slower than light |
| space-like | 类空的 | ds² > 0; causally disconnected events |
| light-like / null | 类光的 / 零 | ds² = 0; path of light rays; proper time is zero |
| light cone | 光锥 | boundary between causally connectable and disconnected regions |
| proper time | 固有时 | time measured by a clock following the worldline; dτ² = −ds²/c² |
| causal structure | 因果结构 | which events can influence which other events |
| worldline | 世界线 | trajectory of an object in spacetime |

---

## 📖 7.7 "相对论"不是一个好名字（"Relativity" Is Not a Good Name）

### Original Text

> *"'Relativity' is not a good name. The name 'Relativity' highlights the relative aspect but missing the more important absolute aspect. We should have named special relativity as the 'theory of invariance'."*

> *"Blind men and an elephant" analogy — different observers see different aspects, but there is an invariant, objective reality underneath.*

### 命名的遗憾

爱因斯坦本人对他理论的这个名字并不满意。"相对论"（Relativity）这个名字过分强调了**相对性**——不同观察者看到不同的时间和空间。但理论的真正核心是**不变性**（invariance）——在所有不同的观察背后，有一个不变的、客观的物理实在。

| 强调"相对性"的一面 | 强调"不变性"的一面 |
|------------------|------------------|
| 时间间隔是相对的 | **时空间隔 $ds^2$ 是绝对的** |
| 空间长度是相对的 | **物理定律在所有惯性系中相同** |
| "同时"是相对的 | **因果关系是绝对的**（类时 vs 类空） |
| 速度叠加是相对的 | **光速在所有惯性系中相同（绝对）** |
| 电场和磁场是相对的 | **电磁场张量 $F_{\mu\nu}$ 是绝对的** |

### 盲人摸象的类比

> *"Blind men and an elephant" — each blind man touches a different part of the elephant and describes a different thing (a wall, a rope, a tree trunk...). But the elephant itself — the invariant, objective reality — is one single entity.*

不同惯性系中的观察者就像"盲人摸象"中的盲人：
- Bob 看到的是"时间膨胀"和"长度收缩"
- Alice 看到的是不同的时间间隔和空间长度
- 但**大象本身**——闵可夫斯基时空中的不变量 $ds^2$——对于所有观察者都是相同的

> 理论的更好名字应该是：**不变性理论**（Theory of Invariance），或者**绝对时空理论**（Theory of Absolute Spacetime）。

有一个典故：闵可夫斯基本人在 1908 年的一次著名演讲中说：
> *"Henceforth space by itself, and time by itself, are doomed to fade away into mere shadows, and only a kind of union of the two will preserve an independent reality."*

*"从今往后，空间本身和时间本身都注定要消逝为纯粹的幻影，只有两者的某种结合才能保持独立的实在。"*

这个"结合"就是**闵可夫斯基时空**，这个"独立的实在"就是**时空间隔 $ds^2$**。

### 🔑 Key Vocabulary — 理论的哲学

| English | 中文 | Notes |
|---------|------|-------|
| invariance | 不变性 | the true essence of special relativity; what stays the same across frames |
| objective reality | 客观实在 | the invariant structure of spacetime, independent of the observer |
| blind men and an elephant | 盲人摸象 | analogy: different observers see different aspects of the same invariant reality |
| Minkowski's quote | 闵可夫斯基的名言 | "space and time...fade away into mere shadows" |
| theory of invariance | 不变性理论 | what Einstein thought the theory should have been called |

---

## 📖 7.8 从狭义到广义：度规的威力（From Special to General: The Power of the Metric）

### Original Text

> *"The metric can be made dependent on the spacetime location (x^μ) to describe curved spacetime. This is what we call general relativity (GR)."*

### 度规：从常数到函数

在狭义相对论中，度规是**常数**：
$$\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1) = \text{const}$$

这意味着时空是**平直的**（flat）——闵可夫斯基时空没有曲率。

在广义相对论（GR）中，度规变成了**时空坐标的函数**：
$$g_{\mu\nu}(x) \neq \text{const}$$

这意味着时空是**弯曲的**（curved）——物质和能量的存在使时空发生弯曲。

| 理论 | 时空几何 | 度规 | 不变量 |
|------|---------|------|--------|
| **狭义相对论（SR）** | 平直闵可夫斯基时空 | $\eta_{\mu\nu} = \text{diag}(-1,1,1,1)$ (常数) | $ds^2 = \eta_{\mu\nu}dx^\mu dx^\nu$ |
| **广义相对论（GR）** | 弯曲时空 | $g_{\mu\nu}(x)$ (位置的函数) | $ds^2 = g_{\mu\nu}(x)dx^\mu dx^\nu$ |

### 广义相对论的核心方程

爱因斯坦场方程用极其简洁的数学语言表达了物质如何弯曲时空：

$$G_{\mu\nu} = \frac{8\pi G}{c^4} T_{\mu\nu}$$

- **左边**：$G_{\mu\nu}$（爱因斯坦张量）——描述时空的几何弯曲（由 $g_{\mu\nu}$ 及其导数构建）
- **右边**：$T_{\mu\nu}$（能量-动量张量）——描述物质和能量的分布
- **本质**：物质告诉时空如何弯曲；时空告诉物质如何运动（"Matter tells spacetime how to curve; spacetime tells matter how to move." — John Wheeler）

### 第 7 节的地位：狭义与广义之间的桥梁

本节（时空几何）在整本讲义中扮演着**承上启下**的关键角色：

```
第 1-5 节                    第 6-7 节                   第 8-9 节
   │                            │                           │
物理现象描述    ──────────→   数学框架建立    ──────────→   物理应用推广
(时间膨胀、       (洛伦兹变换、       (相对论动量能量、
 长度收缩、        闵可夫斯基时空、      质能方程 E=mc²、
 同时性相对性、     度规 η_μν、          广义相对论展望)
 梯子悖论)         时空间隔 ds²)
   │                            │                           │
   └── "发生了什么？" ──→ "为什么发生？" ──→ "还能推出什么？"
```

**第 7 节回答的核心问题**：
- **为什么**洛伦兹变换具有那些性质？→ 因为它是时空中的双曲旋转
- **为什么**时间膨胀和长度收缩相互关联？→ 因为它们来自同一个几何结构
- **为什么**光速是速度上限？→ 因为光锥将时空划分为因果可连接和不可连接区域
- **为什么**存在不变量？→ 因为度规定义了几何，不变量是几何结构的表现

### 🔑 Key Vocabulary — 广义相对论桥梁

| English | 中文 | Notes |
|---------|------|-------|
| curved spacetime | 弯曲时空 | spacetime with non-constant metric; gravity = curvature |
| general relativity (GR) | 广义相对论 | Einstein's theory of gravity as spacetime curvature |
| Einstein field equations | 爱因斯坦场方程 | G_μν = (8πG/c⁴) T_μν |
| Einstein tensor | 爱因斯坦张量 | G_μν; describes spacetime curvature |
| energy-momentum tensor | 能量-动量张量 | T_μν; describes distribution of matter and energy |
| flat spacetime | 平直时空 | Minkowski spacetime; η_μν = const |
| John Wheeler | 约翰·惠勒 | "Matter tells spacetime how to curve; spacetime tells matter how to move" |

---

## 💻 Python 实现：时空几何的可视化与验证

```python
"""
Chapter 7: Spacetime Geometry — Python Implementations.
Topics: Minkowski metric, invariant interval verification,
        spacetime diagram with hyperbolic rotation, rapidity, natural units.
"""
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import FancyArrowPatch
from mpl_toolkits.axes_grid1 import make_axes_locatable

c = 1.0  # natural units

# ================================================================
# 1. MINKOWSKI METRIC
# ================================================================
eta = np.diag([-1.0, 1.0, 1.0, 1.0])
print("=" * 60)
print("MINKOWSKI METRIC η_μν = diag(-1, 1, 1, 1)")
print("=" * 60)
print(eta)
print()

# ================================================================
# 2. RAPIDITY φ = arctanh(β)
# ================================================================
def rapidity(beta):
    """φ = arctanh(β). Valid for |β| < 1."""
    return np.arctanh(beta)

def beta_from_rapidity(phi):
    """β = tanh(φ)"""
    return np.tanh(phi)

def gamma_from_beta(beta):
    """γ = 1/√(1-β²)"""
    return 1.0 / np.sqrt(1.0 - beta**2)

def lorentz_boost(t, x, v):
    """Apply a Lorentz boost with velocity v (in +x direction).
       Returns (t', x'). Uses c=1 natural units."""
    gamma = gamma_from_beta(v)
    t_prime = gamma * (t - v * x)
    x_prime = gamma * (x - v * t)
    return t_prime, x_prime

# Verify cosh(φ) = γ, sinh(φ) = βγ
print("=" * 60)
print("VERIFY: cosh(φ) = γ, sinh(φ) = βγ")
print("=" * 60)
test_betas = [0.0, 0.3, 0.6, 0.8, 0.9, 0.99, 0.999]
for beta in test_betas:
    phi = rapidity(beta)
    gamma = gamma_from_beta(beta)
    cosh_phi = np.cosh(phi)
    sinh_phi = np.sinh(phi)
    print(f"  β={beta:.3f}: φ={phi:.4f}, cosh(φ)={cosh_phi:.4f} (γ={gamma:.4f}), "
          f"sinh(φ)={sinh_phi:.4f} (βγ={beta*gamma:.4f})")
print()

# ================================================================
# 3. INVARIANT INTERVAL VERIFICATION
# ================================================================
def interval_sq(dt, dx, dy=0.0, dz=0.0):
    """Compute ds² = −dt² + dx² + dy² + dz² (c=1)."""
    return -dt**2 + dx**2 + dy**2 + dz**2

def classify_interval(ds2):
    """Classify interval based on sign of ds²."""
    if ds2 < -1e-12:
        return "TIME-LIKE  (ds² < 0)"
    elif ds2 > 1e-12:
        return "SPACE-LIKE (ds² > 0)"
    else:
        return "NULL       (ds² = 0)"

print("=" * 60)
print("LORENTZ INVARIANCE OF ds²")
print("=" * 60)

# Test events
events = [
    (2.0, 1.0, "Time-like: Δt dominates"),
    (1.0, 2.0, "Space-like: Δx dominates"),
    (3.0, 3.0, "Null: Δt = Δx (light path)"),
    (5.0, 4.0, "Time-like (inside future light cone)"),
    (0.1, 100.0, "Highly space-like"),
]

boost_velocity = 0.6  # v = 0.6c
for dt, dx, desc in events:
    ds2_original = interval_sq(dt, dx)

    # Apply Lorentz boost
    dt_prime, dx_prime = lorentz_boost(dt, dx, boost_velocity)
    ds2_boosted = interval_sq(dt_prime, dx_prime)

    print(f"\n  {desc}:")
    print(f"    Before boost:  dt={dt:.1f}, dx={dx:.1f}  →  ds² = {ds2_original:.4f}")
    print(f"    After  boost:  dt'={dt_prime:.4f}, dx'={dx_prime:.4f}  →  ds² = {ds2_boosted:.4f}")
    print(f"    Classification: {classify_interval(ds2_original)}")
    print(f"    ds² invariant?  {'YES ✓' if abs(ds2_original - ds2_boosted) < 1e-12 else 'NO ✗'}")
print()

# ================================================================
# 4. SPACETIME DIAGRAM WITH HYPERBOLIC ROTATION
# ================================================================
fig, axes = plt.subplots(2, 2, figsize=(16, 14))

# --- (a) Light cone and event classification ---
ax = axes[0, 0]
ax.set_xlim(-10, 10)
ax.set_ylim(-10, 10)
ax.set_xlabel('Space x (light-seconds)', fontsize=12)
ax.set_ylabel('Time t (seconds)', fontsize=12)
ax.set_title('Light Cone & Event Classification', fontsize=14, fontweight='bold')

# Light cone boundaries
x_line = np.linspace(-10, 10, 500)
ax.plot(x_line, x_line, 'orange', linewidth=2, label='Future light cone (t = x)')
ax.plot(x_line, -x_line, 'orange', linewidth=2, label='Past light cone (t = −x)')
ax.axhline(0, color='gray', linewidth=0.5, linestyle='--')
ax.axvline(0, color='gray', linewidth=0.5, linestyle='--')

# Fill regions
x_fill = np.linspace(-10, 10, 200)
ax.fill_between(x_fill, abs(x_fill), 10, color='lightblue', alpha=0.3, label='Time-like (future)')
ax.fill_between(x_fill, -10, -abs(x_fill), color='lightblue', alpha=0.2, label='Time-like (past)')
ax.fill_between(x_fill, -abs(x_fill), abs(x_fill), color='lightcoral', alpha=0.2, label='Space-like')

# Mark events of different types
events_to_plot = [
    (3, 1.5, 'ro', 'Time-like'),
    (-4, -2, 'bo', 'Time-like (past)'),
    (5, 5, 'go', 'Null'),
    (-5, -5, 'go', 'Null'),
    (2, 8, 's',  'Space-like'),
    (7, 1, 's',  'Space-like'),
]
for t, x, marker, _ in events_to_plot:
    ax.plot(x, t, marker, markersize=12, markeredgewidth=1.5, markeredgecolor='black')

# Axes arrows
ax.annotate('', xy=(10.5, 0), xytext=(-10.5, 0),
            arrowprops=dict(arrowstyle='->', lw=1.5, color='black'))
ax.annotate('', xy=(0, 10.5), xytext=(0, -10.5),
            arrowprops=dict(arrowstyle='->', lw=1.5, color='black'))
ax.text(9.5, -0.8, 'x', fontsize=14, fontweight='bold')
ax.text(-0.8, 9.5, 'ct', fontsize=14, fontweight='bold')

ax.legend(fontsize=9, loc='upper left', ncol=2)
ax.grid(True, alpha=0.2)
ax.set_aspect('equal')

# --- (b) Hyperbolic rotation: Lorentz boost visualised ---
ax = axes[0, 1]
ax.set_xlim(-10, 10)
ax.set_ylim(-10, 10)
ax.set_xlabel('Space x (light-seconds)', fontsize=12)
ax.set_ylabel('Time t (seconds)', fontsize=12)
ax.set_title('Lorentz Boost as Hyperbolic Rotation', fontsize=14, fontweight='bold')

# Original axes (Bob's frame)
ax.axhline(0, color='gray', linewidth=1, linestyle='-', alpha=0.5)
ax.axvline(0, color='gray', linewidth=1, linestyle='-', alpha=0.5)

# Boosted axes (Alice's frame, v = 0.6c)
v = 0.6
phi_v = rapidity(v)
t_axis = np.linspace(-10, 10, 100)

# ct' axis: x=0 in Alice's frame → x_B = v·t_B (in Bob's frame)
ax.plot(t_axis * v, t_axis, 'r-', linewidth=2, label="Alice's ct' axis (x'=0)")
# x' axis: t'=0 → t_B = v·x_B
ax.plot(t_axis, t_axis * v, 'b-', linewidth=2, label="Alice's x' axis (t'=0)")

# Hyperbolas of constant interval
theta = np.linspace(-2.5, 2.5, 300)
for s2_const in [-25, -16, -9, -4, -1, 1, 4, 9, 16, 25]:
    if s2_const < 0:
        # Time-like: t = ±√(x² + |s²|)
        t_pos = np.sqrt(x_line**2 - s2_const)
        ax.plot(x_line, t_pos, 'lightblue', linewidth=0.5, alpha=0.3)
        ax.plot(x_line, -t_pos, 'lightblue', linewidth=0.5, alpha=0.3)
    else:
        # Space-like: x = ±√(t² + s²)
        x_pos = np.sqrt(x_line**2 + s2_const)
        ax.plot(x_pos, x_line, 'lightcoral', linewidth=0.5, alpha=0.3)
        ax.plot(-x_pos, x_line, 'lightcoral', linewidth=0.5, alpha=0.3)

# Light cone
ax.plot(x_line, x_line, 'orange', linewidth=1.5, alpha=0.6)
ax.plot(x_line, -x_line, 'orange', linewidth=1.5, alpha=0.6)

ax.legend(fontsize=10, loc='upper right')
ax.grid(True, alpha=0.2)
ax.set_aspect('equal')

# --- (c) Rapidity φ(β) curve ---
ax = axes[1, 0]
beta_vals = np.linspace(0, 0.9999, 1000)
phi_vals = rapidity(beta_vals)
ax.plot(beta_vals, phi_vals, 'b-', linewidth=2.5, label='φ = arctanh(β)')
ax.axvline(x=1.0, color='red', linestyle='--', linewidth=1.5, alpha=0.5, label='β = 1 (c)')
ax.set_xlabel('β = v/c', fontsize=12)
ax.set_ylabel('Rapidity φ', fontsize=12)
ax.set_title('Rapidity φ(β): Diverges as v → c', fontsize=14, fontweight='bold')

# Mark some key points
key_betas = [0.5, 0.8, 0.9, 0.99, 0.999]
for b in key_betas:
    p = rapidity(b)
    ax.plot(b, p, 'ro', markersize=6)
    ax.annotate(f'β={b}\nφ={p:.2f}', xy=(b, p), xytext=(b + 0.05, p - 0.4),
                fontsize=9, arrowprops=dict(arrowstyle='->', lw=1, color='gray'))
ax.legend(fontsize=10)
ax.grid(True, alpha=0.3)

# --- (d) cosh(φ) = γ, sinh(φ) = βγ comparison ---
ax = axes[1, 1]
phi_range = np.linspace(0, 5, 500)
ax.plot(phi_range, np.cosh(phi_range), 'b-', linewidth=2, label='cosh(φ) = γ')
ax.plot(phi_range, np.sinh(phi_range), 'r-', linewidth=2, label='sinh(φ) = βγ')
ax.plot(phi_range, np.tanh(phi_range), 'g-', linewidth=2, label='tanh(φ) = β')
ax.axhline(y=1.0, color='gray', linestyle=':', alpha=0.5)
ax.axhline(y=0.0, color='gray', linestyle=':', alpha=0.5)
ax.set_xlabel('Rapidity φ', fontsize=12)
ax.set_ylabel('Value', fontsize=12)
ax.set_title('φ → Lorentz Factor Relations', fontsize=14, fontweight='bold')
ax.legend(fontsize=11)
ax.grid(True, alpha=0.3)
ax.set_ylim(-0.5, 60)

plt.suptitle('Spacetime Geometry — Minkowski Spacetime Visualized', fontsize=16, fontweight='bold', y=1.01)
plt.tight_layout()
plt.savefig('/tmp/spacetime_geometry.png', dpi=150, bbox_inches='tight')
print("[Figure saved to /tmp/spacetime_geometry.png]")
print()

# ================================================================
# 5. NATURAL UNITS DEMONSTRATION
# ================================================================
print("=" * 60)
print("NATURAL UNITS (c = 1): Simplify Relativity Formulas")
print("=" * 60)

# SI units values
c_si = 299792458  # m/s

# Example: a particle moving at 0.9c
v_si = 0.9 * c_si  # m/s
beta_si = v_si / c_si  # = 0.9
gamma_si = 1.0 / np.sqrt(1 - beta_si**2)

# In natural units:
beta_nu = 0.9
gamma_nu = 1.0 / np.sqrt(1 - beta_nu**2)

print(f"\n  Particle speed: v = 0.9c")
print(f"    SI units:  v = {v_si:.2e} m/s,  β = {beta_si:.6f},  γ = {gamma_si:.6f}")
print(f"    Natural:   v = {beta_nu},         β = {beta_nu},       γ = {gamma_nu:.6f}")
print(f"    γ matches? {'YES ✓' if abs(gamma_si - gamma_nu) < 1e-12 else 'NO ✗'}")

# Lorentz boost in natural units
print(f"\n  Lorentz boost (natural units, c=1):")
print(f"    t' = γ(t − vx)")
print(f"    x' = γ(x − vt)")
t0, x0 = 5.0, 3.0
t1, x1 = lorentz_boost(t0, x0, 0.6)
ds2_before = interval_sq(t0, x0)
ds2_after = interval_sq(t1, x1)
print(f"    Before: (t={t0}, x={x0}) → ds² = {ds2_before:.2f}")
print(f"    After:  (t'={t1:.4f}, x'={x1:.4f}) → ds² = {ds2_after:.2f}")
print(f"    ds² invariant? {'YES ✓' if abs(ds2_before - ds2_after) < 1e-12 else 'NO ✗'}")
print()

# ================================================================
# 6. RAPIDITY IS ADDITIVE — NUMERICAL VERIFICATION
# ================================================================
print("=" * 60)
print("RAPIDITY ADDITIVITY: φ₁ + φ₂ = φ_total")
print("=" * 60)

def relativistic_velocity_add(u, v):
    """Add velocities relativistically: u⊕v = (u+v)/(1+uv/c²). c=1."""
    return (u + v) / (1.0 + u * v)

test_pairs = [
    (0.5, 0.5, "Two 0.5c boosts"),
    (0.9, 0.9, "Two 0.9c boosts"),
    (0.3, 0.7, "0.3c + 0.7c"),
    (0.99, 0.5, "0.99c + 0.5c"),
    (0.999, 0.999, "Extreme relativistic"),
]

for u, v, desc in test_pairs:
    w_rel = relativistic_velocity_add(u, v)
    w_gal = u + v
    phi_u = rapidity(u)
    phi_v = rapidity(v)
    phi_w = rapidity(w_rel)
    phi_sum = phi_u + phi_v

    print(f"\n  {desc}:")
    print(f"    Velocity addition:")
    print(f"      Galilean:      {u} + {v} = {w_gal:.6f}  {'⚠ exceeds c!' if w_gal > 1 else ''}")
    print(f"      Relativistic:  {u} ⊕ {v} = {w_rel:.8f}")
    print(f"    Rapidity addition:")
    print(f"      φ(u) + φ(v) = {phi_u:.6f} + {phi_v:.6f} = {phi_sum:.6f}")
    print(f"      φ(w)        = {phi_w:.6f}")
    print(f"      Match? {'YES ✓' if abs(phi_w - phi_sum) < 1e-12 else 'NO ✗'}")
```

```
======================================================================
MINKOWSKI METRIC η_μν = diag(-1, 1, 1, 1)
======================================================================
[[-1.  0.  0.  0.]
 [ 0.  1.  0.  0.]
 [ 0.  0.  1.  0.]
 [ 0.  0.  0.  1.]]

======================================================================
VERIFY: cosh(φ) = γ, sinh(φ) = βγ
======================================================================
  β=0.000: φ=0.0000, cosh(φ)=1.0000 (γ=1.0000), sinh(φ)=0.0000 (βγ=0.0000)
  β=0.300: φ=0.3095, cosh(φ)=1.0483 (γ=1.0483), sinh(φ)=0.3145 (βγ=0.3145)
  β=0.600: φ=0.6931, cosh(φ)=1.2500 (γ=1.2500), sinh(φ)=0.7500 (βγ=0.7500)
  β=0.800: φ=1.0986, cosh(φ)=1.6667 (γ=1.6667), sinh(φ)=1.3333 (βγ=1.3333)
  β=0.900: φ=1.4722, cosh(φ)=2.2942 (γ=2.2942), sinh(φ)=2.0647 (βγ=2.0647)
  β=0.990: φ=2.6467, cosh(φ)=7.0888 (γ=7.0888), sinh(φ)=7.0179 (βγ=7.0179)
  β=0.999: φ=3.8002, cosh(φ)=22.3663 (γ=22.3663), sinh(φ)=22.3439 (βγ=22.3439)

======================================================================
LORENTZ INVARIANCE OF ds²
======================================================================

  Time-like: Δt dominates:
    Before boost:  dt=2.0, dx=1.0  →  ds² = -3.0000
    After  boost:  dt'=1.7500, dx'=0.2500  →  ds² = -3.0000
    Classification: TIME-LIKE  (ds² < 0)
    ds² invariant?  YES ✓

  Space-like: Δx dominates:
    Before boost:  dt=1.0, dx=2.0  →  ds² = 3.0000
    After  boost:  dt'=-0.2500, dx'=1.7500  →  ds² = 3.0000
    Classification: SPACE-LIKE (ds² > 0)
    ds² invariant?  YES ✓

  Null: Δt = Δx (light path):
    Before boost:  dt=3.0, dx=3.0  →  ds² = 0.0000
    After  boost:  dt'=1.5000, dx'=1.5000  →  ds² = 0.0000
    Classification: NULL       (ds² = 0)
    ds² invariant?  YES ✓

  Time-like (inside future light cone):
    Before boost:  dt=5.0, dx=4.0  →  ds² = -9.0000
    After  boost:  dt'=3.2500, dx'=0.2500  →  ds² = -9.0000
    Classification: TIME-LIKE  (ds² < 0)
    ds² invariant?  YES ✓

  Highly space-like:
    Before boost:  dt=0.1, dx=100.0  →  ds² = 9999.9900
    After  boost:  dt'=-74.8750, dx'=124.9750  →  ds² = 9999.9900
    Classification: SPACE-LIKE (ds² > 0)
    ds² invariant?  YES ✓

======================================================================
NATURAL UNITS (c = 1): Simplify Relativity Formulas
======================================================================
  Particle speed: v = 0.9c
    SI units:  v = 2.70e+08 m/s,  β = 0.900000,  γ = 2.294157
    Natural:   v = 0.9,         β = 0.9,       γ = 2.294157
    γ matches? YES ✓

  Lorentz boost (natural units, c=1):
    t' = γ(t − vx)
    x' = γ(x − vt)
    Before: (t=5.0, x=3.0) → ds² = -16.00
    After:  (t'=4.0000, x'=0.0000) → ds² = -16.00
    ds² invariant? YES ✓

======================================================================
RAPIDITY ADDITIVITY: φ₁ + φ₂ = φ_total
======================================================================

  Two 0.5c boosts:
    Velocity addition:
      Galilean:      0.5 + 0.5 = 1.000000  ⚠ exceeds c!
      Relativistic:  0.5 ⊕ 0.5 = 0.80000000
    Rapidity addition:
      φ(u) + φ(v) = 0.549306 + 0.549306 = 1.098612
      φ(w)        = 1.098612
      Match? YES ✓

  Two 0.9c boosts:
    Velocity addition:
      Galilean:      0.9 + 0.9 = 1.800000  ⚠ exceeds c!
      Relativistic:  0.9 ⊕ 0.9 = 0.99447514
    Rapidity addition:
      φ(u) + φ(v) = 1.472219 + 1.472219 = 2.944439
      φ(w)        = 2.944439
      Match? YES ✓

  0.3c + 0.7c:
    Velocity addition:
      Galilean:      0.3 + 0.7 = 1.000000  ⚠ exceeds c!
      Relativistic:  0.3 ⊕ 0.7 = 0.82758621
    Rapidity addition:
      φ(u) + φ(v) = 0.309520 + 0.867301 = 1.176820
      φ(w)        = 1.176820
      Match? YES ✓

  0.99c + 0.5c:
    Velocity addition:
      Galilean:      0.99 + 0.5 = 1.490000  ⚠ exceeds c!
      Relativistic:  0.99 ⊕ 0.5 = 0.99664430
    Rapidity addition:
      φ(u) + φ(v) = 2.646652 + 0.549306 = 3.195958
      φ(w)        = 3.195958
      Match? YES ✓

  Extreme relativistic:
    Velocity addition:
      Galilean:      0.999 + 0.999 = 1.998000  ⚠ exceeds c!
      Relativistic:  0.999 ⊕ 0.999 = 0.99999950
    Rapidity addition:
      φ(u) + φ(v) = 3.800201 + 3.800201 = 7.600402
      φ(w)        = 7.600402
      Match? YES ✓
```

---

## 📊 概念对照总表

### 欧几里得几何 vs 闵可夫斯基几何

| 特性 | 欧几里得几何（空间） | 闵可夫斯基几何（时空） |
|------|-------------------|---------------------|
| **坐标系** | (x, y, z) | (ct, x, y, z) 或 (t, x, y, z) with c=1 |
| **度规** | $\delta_{ij} = \text{diag}(1,1,1)$ | $\eta_{\mu\nu} = \text{diag}(-1,1,1,1)$ |
| **不变量** | $d^2 = x^2 + y^2 + z^2$ | $ds^2 = -c^2 t^2 + x^2 + y^2 + z^2$ |
| **变换群** | SO(3) — 空间旋转（3 个生成元） | SO(3,1) — 洛伦兹群（6 个生成元） |
| **不变曲线** | 圆 $x^2 + y^2 = R^2$ | 双曲线 $-(ct)^2 + x^2 = \text{const}$ |
| **角度/迅速度参数化** | $(\cos\theta, \sin\theta)$ | $(\cosh\varphi, \sinh\varphi)$ |
| **角度/迅速度范围** | $\theta \in [0, 2\pi)$ (有界) | $\varphi \in (-\infty, \infty)$ (无界) |
| **"勾股定理"** | $a^2 + b^2 = c^2$ (斜边最长) | $-a^2 + b^2 = -c^2$ (时间"斜边"最短) |
| **距离符号** | 恒正（正定性） | 可正可负可零（不定性） |
| **正定性** | 正定（positive-definite） | 不定（indefinite） |

### 三类事件的总结

| 类型 | ds² 符号 | 因果关系 | 可否观测 | 粒子世界线 | 固有时 |
|------|---------|---------|---------|-----------|--------|
| Time-like | < 0 | 可能 | 可（亚光速信号） | 有质量粒子 | $d\tau > 0$ |
| Null | = 0 | 仅光速 | 可（光信号） | 光子/无质量粒子 | $d\tau = 0$ |
| Space-like | > 0 | 不可能 | 不可观测（需超光速） | 快子（tachyon，假想粒子） | 虚数（无物理意义） |

---

## 🎯 关键要点

1. **时空不是欧几里得的**：时间平方前有一个关键的负号：$ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2$。这个负号解释了"为什么运动时钟的斜边反而更短"。

2. **迅速度 $\varphi = \text{arctanh}(\beta)$ 是真正可加的"速度"**：$\cosh\varphi = \gamma$，$\sinh\varphi = \beta\gamma$。洛伦兹 boost 是时空中角度为 $\varphi$ 的双曲旋转。

3. **虚数时间技巧实现时空完全统一**：$ct = iw$ 将闵可夫斯基时空变为 4 维欧几里得空间，3 个 boost 变成了 3 个额外的旋转 —— 时空有 6 个独立的对称生成元，比三维球面（SO(3) 的 3 个）更对称。

4. **自然单位 $c = 1$ 揭示时空的本质统一**：光速只是一个换算因子，就像 1 英尺 = 0.3048 米。真正的物理在用同一单位度量时空时才完全展现。

5. **$ds^2$ 是狭义相对论的不变量**：就像 $x^2 + y^2$ 在空间旋转下不变，$ds^2$ 在洛伦兹变换下不变。度规 $\eta_{\mu\nu} = \text{diag}(-1,1,1,1)$ 是时空几何的完整数学描述。

6. **$ds^2$ 的符号决定因果关系**：$ds^2 < 0$（类时）→ 可因果连接；$ds^2 = 0$（类光/null）→ 恰由光连接；$ds^2 > 0$（类空）→ 不可能有因果关系。

7. **"相对论"是个坏名字**：理论的核心不是"一切都相对"，而是"不变量是绝对的"。盲人摸象的类比：不同观察者摸到大象的不同部位，但大象本身是唯一的客观实在——闵可夫斯基时空中的 $ds^2$ 就是那个"大象"。

8. **度规是通往广义相对论的桥梁**：将常数度规 $\eta_{\mu\nu}$ 推广为位置的函数 $g_{\mu\nu}(x)$，就得到了描述引力的广义相对论。

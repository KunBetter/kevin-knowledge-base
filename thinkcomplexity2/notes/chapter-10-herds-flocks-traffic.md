# 第10章：群体、集群和交通堵塞 (Herds, Flocks, and Traffic Jams)

> *"The agent-based models in Chapter 9 are based on a grid, where agents occupy discrete locations in two dimensions. In this chapter, we turn to agents that move in continuous space — cars on a one-dimensional highway and birds in three-dimensional space."*
> 第9章的代理模型基于**网格**，代理占据二维离散位置。本章转向**连续空间**中的代理运动——一维高速公路上的汽车和三维空间中的鸟群。本章代码在 `chap10.ipynb` 中。

| 单词/短语 | 注释 |
|-----------|------|
| agent-based models | 基于代理的模型，每个代理独立决策，宏观行为从微观互动中涌现 |
| grid | 网格，将空间划分为离散单元的抽象结构 |
| discrete locations | 离散位置，只能占据网格上的特定坐标，不能位于中间位置 |
| continuous space | 连续空间，代理可以位于任意实数坐标，不受网格约束 |
| one-dimensional | 一维的，本章中指环形公路只沿一个方向延伸 |
| three-dimensional | 三维的，Boid 模型在 x、y、z 三个轴向上运动 |

---

## 10.1 交通堵塞 (Traffic Jams)

### 问题

- 有的堵车有明确原因（事故、测速），但有时**无明显原因**也会出现堵车
- 基于代理的模型可以解释**自发性交通堵塞**

### Highway 类

```python
class Highway:
    def __init__(self, n=10, length=1000, eps=0):
        self.length = length
        self.eps = eps
        locs = np.linspace(0, length, n, endpoint=False)
        self.drivers = [Driver(loc) for loc in locs]
        for i in range(n):
            j = (i+1) % n
            self.drivers[i].next = self.drivers[j]
```

- **n**：车辆数量
- **length**：公路长度（环形）
- **eps**：随机噪声幅度
- 车辆初始**等距分布**在环形公路上
- 每辆车持有指向下一辆车的引用，形成**循环链表**

### 每步模拟

```python
def step(self):
    for driver in self.drivers:
        self.move(driver)
```

### move 方法（物理规则）

```python
def move(self, driver):
    dist = self.distance(driver)
    acc = driver.choose_acceleration(dist)       # 驾驶决策
    acc = min(acc, self.max_acc)                  # 加速度上限
    acc = max(acc, self.min_acc)                  # 减速度下限
    speed = driver.speed + acc
    speed *= np.random.uniform(1-self.eps, 1+self.eps)  # 随机噪声
    speed = max(speed, 0)                         # 不能倒车
    speed = min(speed, self.speed_limit)          # 不能超速
    if speed > dist:
        speed = 0                                 # 避免碰撞 → 急停
    driver.speed = speed
    driver.loc += speed
```

| 参数 | 值 | 说明 |
|------|-----|------|
| `max_acc` | 1 | 最大加速度 |
| `min_acc` | -10 | 最大减速度（刹车） |
| `speed_limit` | 40 | 速度上限 |
| `eps` | 0 ~ 0.02 | 速度随机误差比例 |

> *"The key design choice is that `choose_acceleration` is the driver's only decision; everything else is determined by the 'physics' of the simulation."*
> **关键设计**：`choose_acceleration` 是驾驶员的**唯一决策**，其余由"物理"规则决定。

| 单词/短语 | 注释 |
|-----------|------|
| design choice | 设计决策，在建模时对哪些行为由代理决策、哪些由环境规则约束的划分 |
| decision | 决策，代理在给定信息下主动做出的选择 |
| physics | 物理规则，模型中不由代理控制、而是系统强制执行的约束（如速度上限、碰撞避免） |
| simulation | 模拟，通过计算机程序重现真实世界现象的过程 |

### 默认 Driver 类

```python
class Driver:
    def __init__(self, loc, speed=0):
        self.loc = loc
        self.speed = speed

    def choose_acceleration(self, dist):
        return 1      # 永远以最大加速度加速
```

### 堵车形成过程

1. 最初等距分布 → 所有车加速到速度上限
2. **随机噪声**导致速度差异 → 间距变得不均匀
3. 某车速度超过与前车距离 → **碰撞检测触发** → 速度归零
4. 后方来车接连撞上停止的车 → **交通堵塞形成**
5. 堵塞一旦形成，**倾向持久**：后方车不断追尾，前方车加速逃离
6. 在某些条件下，堵塞自身**向后传播**（车向前走，堵点向后移）

---

## 10.2 随机扰动 (Random Perturbation)

### 关键实验：噪声 vs 车数 vs 平均速度

| 噪声 eps | 含义 | 公路容量（能维持最高速度的最大车数） |
|----------|------|--------------------------------------|
| 0 | 无噪声 | **25 辆** |
| 0.001 | 0.1% 误差 | **20 辆** |
| 0.01 | 1% 误差 | **10 辆** |

> *"Even a tiny amount of random error can dramatically reduce the capacity of the highway. With just 1% error, the capacity drops from 25 cars to 10."*
> **结论**：即使极小的随机误差也会**严重降低**公路通行能力。1% 的误差就能让容量从 25 辆降至 10 辆。

| 单词/短语 | 注释 |
|-----------|------|
| random error | 随机误差，模拟中人为引入的速度波动，代表驾驶员操作的不精确性 |
| dramatically reduce | 大幅降低，强调影响程度远超直觉预期 |
| capacity | 容量/通行能力，公路在维持最高速度前提下能容纳的最大车辆数 |
| drops | 下降/骤降，暗示非线性突变而非线性递减 |

### 理想情况分析

- 公路长度 1000，n 辆车 → 间距 = 1000/n
- 车速不能超过间距 → 最高平均速度 = **min(1000/n, 40)**
- 无噪声时，n ≤ 25 可达最大速度 40

---

## 10.3 Boids（鸟群模型）

### 起源

- **Craig Reynolds**, 1987: *Flocks, herds and schools: A distributed behavioral model*
- "Boid" = "bird-oid" 的缩写，也模仿 "bird" 的口音读法
- 同样适用于**鱼群**和**陆地群居动物**

### 三种核心行为

| 行为 | 描述 | 方向 |
|------|------|------|
| **Flock Centering**（群集中心） | 朝群体中心移动 | → 向心 |
| **Collision Avoidance**（避碰） | 避开障碍物和其他 Boid | ← 离心 |
| **Velocity Matching**（速度匹配） | 与邻近 Boid 对齐速度和方向 | ↔ 对齐 |

### 关键原则

- Boid 只基于**局部信息**做决策
- 每个 Boid 只能看到其**视野范围**内的其他 Boid
- 代码实现：`Boids7.py`，使用 **VPython** 进行 3D 渲染
- 使用 `Vector` 对象表示三维位置和速度

---

## 10.4 Boid 算法的实现

### 两个类

- **Boid**：实现 Boid 行为
- **World**：包含 Boid 列表和一个"胡萝卜"（Boid 被吸引的目标点）

### 四个核心方法

#### (1) `center` — 群集中心

```python
def center(self, boids, radius=1, angle=1):
    neighbors = self.get_neighbors(boids, radius, angle)
    vecs = [boid.pos for boid in neighbors]
    return self.vector_toward_center(vecs)
```

- 找到视野范围内的邻居
- 计算指向邻居**质心**的向量

#### (2) `avoid` — 避碰

```python
def avoid(self, boids, carrot, radius=0.3, angle=np.pi):
    objects = boids + [carrot]
    neighbors = self.get_neighbors(objects, radius, angle)
    vecs = [boid.pos for boid in neighbors]
    return -self.vector_toward_center(vecs)  # 取反 → 远离
```

- 与 center 不同：radius 更小（只避太近的），angle 更大（全方向）
- 结果取反 → **远离**质心
- 也包括避开**胡萝卜**

#### (3) `align` — 速度对齐

```python
def align(self, boids, radius=0.5, angle=1):
    neighbors = self.get_neighbors(boids, radius, angle)
    vecs = [boid.vel for boid in neighbors]    # 取速度向量而非位置
    return self.vector_toward_center(vecs)
```

- 关键区别：计算邻居**速度**的平均，而非位置的平均
- 使 Boid 趋向与群体行进方向一致

#### (4) `love` — 趋向目标

```python
def love(self, carrot):
    toward = carrot.pos - self.pos
    return limit_vector(toward)
```

- 指向"胡萝卜"的向量，使群体有一个**共同吸引点**

### `get_neighbors` — 视野筛选

```python
def get_neighbors(self, boids, radius, angle):
    neighbors = []
    for boid in boids:
        if boid is self: continue
        offset = boid.pos - self.pos
        if offset.mag > radius: continue              # 超出距离
        if self.vel.diff_angle(offset) > angle: continue  # 超出视角
        neighbors.append(boid)
    return neighbors
```

筛选条件：
1. 非自身
2. 距离 ≤ **radius**
3. 相对方向与自身速度方向的夹角 ≤ **angle**

> *"This models the limited field of view of real animals: each boid can only see companions within a certain angle in front of it."*
> 这模拟了动物的**有限视野**：只能看到前方一定角度范围内的同伴。

| 单词/短语 | 注释 |
|-----------|------|
| limited field of view | 有限视野，动物无法看到身后或侧面远处的同伴，只能感知前方扇形区域 |
| companions | 同伴，同一群体中的其他个体 |
| angle | 视角/角度，以自身前进方向为基准的可视扇形范围 |
| models | 建模/模拟，将生物学特征转化为算法参数的过程 |

### 各方法的参数对比

| 方法 | radius | angle | 使用数据 | 方向 |
|------|--------|-------|---------|------|
| `center` | 1（大） | 1 rad | 邻居位置 | 指向质心 |
| `avoid` | 0.3（小） | π（全方位） | 邻居+胡萝卜位置 | 远离质心 |
| `align` | 0.5（中） | 1 rad | 邻居速度 | 与平均速度对齐 |
| `love` | — | — | 胡萝卜位置 | 指向胡萝卜 |

---

## 10.5 仲裁 (Arbitration)

Reynolds 将四个方法的输出称为**加速请求**（acceleration requests），它们之间可能存在冲突。

### 加权求和

```python
def set_goal(self, boids, carrot):
    w_avoid = 10
    w_center = 3
    w_align = 1
    w_love = 10
    self.goal = (w_center * self.center(boids) +
                 w_avoid * self.avoid(boids, carrot) +
                 w_align * self.align(boids) +
                 w_love * self.love(carrot))
    self.goal.mag = 1
```

| 权重 | 值 | 含义 |
|------|-----|------|
| `w_avoid` | 10 | 避碰最重要（生存优先） |
| `w_center` | 3 | 群集倾向中等 |
| `w_align` | 1 | 对齐权重最低 |
| `w_love` | 10 | 趋向目标很重要 |

### 运动更新

```python
def move(self, mu=0.1, dt=0.1):
    self.vel = (1-mu) * self.vel + mu * self.goal
    self.vel.mag = 1
    self.pos += dt * self.vel
    self.axis = self.length * self.vel
```

- **mu**：机动性（maneuverability），决定转向速度。mu 越小 → 转向越慢（更平滑）
- **dt**：时间步长
- 速度在旧速度与目标之间做**加权插值**，然后归一化
- 位置更新：`新位置 = 旧位置 + dt × 速度`

### 参数对行为的影响

通过调整 radius、angle、权重和 mu，可以产生不同的群体模式：
- **鸟群**：灵活转向，三维空间
- **鱼群**：更紧凑，流畅
- **昆虫云**：更多随机性

---

## 10.6 涌现与自由意志 (Emergence and Free Will)

### 涌现现象回顾（贯穿全书）

| 系统 | 微观行为 | 涌现的宏观行为 |
|------|---------|---------------|
| Rule 30 | 确定性规则 | 统计上**不可区分于随机**的序列 |
| Schelling 模型 | 个体不种族歧视 | **高度种族隔离** |
| Sugarscape | 个体不能对角线移动 | 代理群形成**对角波浪** |
| 交通堵塞 | 汽车向前行驶 | 堵塞**向后传播** |
| Boids 群体 | 个体基于局部信息决策 | 群体看起来像**被中央组织** |

### 自由意志的哲学讨论

**核心矛盾**：如果身体和大脑受确定性物理定律支配，那么我们的选择就是完全被决定的。

**两种传统解决方案**：

| 哲学家 | 观点 | 本质 |
|--------|------|------|
| William James | 二阶段模型：随机生成 + 确定性选择 | 行为可随机 → 不可预测 |
| David Hume | 选择的感知是**幻觉** | 行为完全确定 |

> *"Both views agree that there is a conflict: if any part of a decision is determined, the whole cannot involve free will."*
> 两者都认为**存在冲突**：部分确定 → 整体不能有自由意志

| 单词/短语 | 注释 |
|-----------|------|
| determined | 被决定的，由先前的物理状态和自然规律唯一确定的结果 |
| free will | 自由意志，人类拥有在给定条件下自主做出选择的能力 |
| conflict | 矛盾/冲突，指决定论与自由意志在逻辑上似乎无法共存 |
| two-stage model | 二阶段模型，James 提出的方案：第一阶段随机生成选项，第二阶段确定性选择 |

### Downey 的复杂系统视角

**相容论（Compatibilism）**：自由意志与决定论**可以共存**。

类比推理：
- 交通堵塞向后移动 ≠ 汽车向后移动
- **人可以有自由意志 ≠ 神经元必须有自由意志**

> *"This is the philosophical implication of hierarchical emergence: different levels have different causal descriptions. At the level of the agent/person, 'free will' is a meaningful causal concept, even if the underlying level is deterministic."*
> 这是**层次涌现**的哲学推论：不同层次有不同的因果描述。在代理人/人的层次上，"自由意志"是一个有意义的因果概念，即使底层是确定性的。

| 单词/短语 | 注释 |
|-----------|------|
| hierarchical emergence | 层次涌现，复杂系统中不同层级展现出各自独立的规律和因果描述 |
| causal description | 因果描述，对某一现象"为什么发生"的解释框架，依赖于所观察的层级 |
| deterministic | 决定论的/确定性的，每个事件都由先前状态必然导致 |
| compatibilism | 相容论，认为自由意志与决定论可以同时为真的哲学立场 |
| underlying level | 底层/基础层级，构成系统的基本单元层级（如神经元之于大脑、汽车之于交通） |

---

## 10.7 练习

| 练习 | 内容 | 难度 |
|------|------|------|
| 10.1 | 设计 `BetterDriver` 类继承 `Driver`，覆写 `choose_acceleration`，尝试提高平均速度或减少碰撞 | ⭐⭐ |
| 10.2 | 安装 VPython，运行 `Boids7.py`；修改参数观察效果；将某个行为权重设为 0 会怎样？实现 Flake 建议的**视线维护**规则（前方有鸟则侧移） | ⭐⭐⭐ |
| 10.3 | 阅读关于**相容论**（compatibilism）的更多内容。什么是"后果论证"（consequence argument）？基于本书内容，你能给出什么回应？ | ⭐⭐⭐⭐ |

---

## 核心概念总结

| 概念 | 说明 |
|------|------|
| **自发性交通堵塞** | 无需外部原因，仅由随机波动 + 物理约束产生 |
| **环形公路模型** | 一维连续空间，每辆车只有一个决策点 |
| **Boids 三行为** | Center（向心）+ Avoid（离心）+ Align（对齐）= 复杂群集行为 |
| **有限视野** | 每个代理只看局部信息，不依赖全局协调 |
| **仲裁** | 通过加权求和调和冲突的加速请求 |
| **相容论** | 涌现视角下，高层次自由意志与低层次决定论不矛盾 |

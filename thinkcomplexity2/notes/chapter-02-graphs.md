# 第二章：图（Graphs）

## 2.1 什么是图？

> *"A graph is a way to represent a set of objects and the relationships, or connections, between them. In graph theory, the objects are called nodes (or vertices) and the relationships are called edges."*
> 图是一种表示一组对象及其之间关系（或连接）的方式。在图论中，对象称为**节点**（或顶点），关系称为**边**。

| 单词/短语 | 注释 |
|-----------|------|
| graph | 图：由节点和边组成的数学结构，用于建模对象之间的二元关系 |
| nodes / vertices | 节点/顶点：图中代表离散元素的抽象实体 |
| edges | 边：连接两个节点的关系，表示它们之间存在某种关联 |
| relationships / connections | 关系/连接：边所表示的对象之间的相互作用或联系 |
| graph theory | 图论：研究图的数学分支，分析节点和边的结构性质 |

- **节点（nodes/vertices）**：表示系统中有哪些离散元素
- **边（edges）**：表示元素之间的连接
- 边可以有属性：长度、成本、权重
- 边可以是**有向**或**无向**的

> *"A sequence of nodes with edges between consecutive nodes is called a path. A graph is connected if there is a path from every node to every other node."*
> 节点序列中每对连续节点之间都有一条边，这样的序列称为**路径**。如果图中任意两个节点之间都存在路径，则该图是**连通**的。

| 单词/短语 | 注释 |
|-----------|------|
| path | 路径：节点序列，序列中每对相邻节点之间都有一条边 |
| connected | 连通的：图中任意两个节点之间都存在至少一条路径 |
| directed / undirected | 有向/无向：边的方向性——有向边有起点和终点，无向边双向通行 |
| weight | 权重：边上的数值属性，可表示距离、成本、容量等 |

- **路径（path）**：节点序列，每对连续节点之间有一条边
- 图论是研究图的数学分支

## 2.2 NetworkX

> *"NetworkX is a Python library for creating, manipulating, and studying the structure, dynamics, and functions of complex networks. To use it, we import the library and create a graph object."*
> NetworkX 是一个用于创建、操作和研究复杂网络的结构、动力学和功能的 Python 库。使用时导入库并创建图对象。

| 单词/短语 | 注释 |
|-----------|------|
| NetworkX | Python 中最常用的网络/图分析库，用于图的创建、操作和研究 |
| DiGraph | 有向图（Directed Graph）：边有方向性的图类型 |
| Graph | 无向图（Undirected Graph）：边没有方向的图类型 |
| add_node / add_edge | 添加节点 / 添加边：图对象的基本构造方法 |

Python 最常用的网络库：

```python
import networkx as nx
G = nx.DiGraph()        # 有向图
G = nx.Graph()          # 无向图
G.add_node('Alice')
G.add_edge('Alice', 'Bob')
```

关键函数：
- `nx.draw_circular()` — 环形布局
- `nx.draw()` — 指定位置布局
- `nx.draw_networkx_edge_labels()` — 边标签

## 2.3 随机图

> *"A random graph is just what it sounds like: a graph where the edges are generated at random. The most well-known random graph model is the Erdős-Rényi model, which has two parameters: n, the number of nodes, and p, the probability that there is an edge between any two nodes."*
> 随机图顾名思义：边是随机生成的图。最著名的随机图模型是 **Erdős-Rényi 模型**（ER 模型），有两个参数：n（节点数）和 p（任意两个节点之间存在边的概率）。

| 单词/短语 | 注释 |
|-----------|------|
| random graph | 随机图：边以一定概率随机生成的图 |
| Erdős-Rényi model | ER 模型：经典的随机图模型，记为 G(n, p)，以概率 p 独立选择每条可能的边 |
| probability | 概率：每条边独立存在的可能性，0 ≤ p ≤ 1 |
| parameters | 参数：控制模型行为的变量，ER 模型中为 n 和 p |

**Erdős-Rényi 模型**（ER 图）：
- 参数：n（节点数）、p（边概率）

> *"One of the interesting things about random graphs is that as you vary the probability, p, the properties of the graph change suddenly, rather than gradually. This phenomenon is called a phase change. The critical value where the phase change occurs for connectivity is p* = ln(n) / n."*
> 随机图最有趣的性质之一是：随着概率 p 的变化，图的性质会**突然**而非逐渐地改变。这种现象称为**相变**。连通性发生相变的临界值为 **p* = ln(n) / n**。

| 单词/短语 | 注释 |
|-----------|------|
| phase change | 相变：系统性质在临界参数附近发生突变的现象 |
| critical value | 临界值：相变发生的参数阈值 |
| connectivity | 连通性：图中任意节点对之间存在路径的性质 |
| ln(n) | 自然对数：以 e 为底的对数，临界值公式中的关键项 |

- 关键发现：随机图的属性存在**突变**
- **连通性临界值**：p* = ln(n)/n
  - p < p* → 几乎不连通
  - p > p* → 几乎一定连通

## 2.4 生成图

> *"To generate a complete graph, we iterate through all pairs of nodes and add an edge between each pair. To generate a random graph, we iterate through all pairs and add an edge with probability p."*
> 生成**完全图**时，遍历所有节点对并在每对之间添加边。生成随机图时，遍历所有节点对并以概率 p 添加边。

| 单词/短语 | 注释 |
|-----------|------|
| complete graph | 完全图：每对节点之间都有一条边的图，共 n(n-1)/2 条边 |
| iterate | 遍历：依次访问集合中的每个元素 |
| all pairs | 所有节点对：图中所有可能的二元节点组合 |
| edge with probability p | 以概率 p 添加边：独立随机决定每条可能的边是否存在 |

```python
def all_pairs(nodes):       # 枚举所有节点对
def make_complete_graph(n)  # 完全图（每对节点之间都有边）
def random_pairs(nodes, p)  # 以概率 p 选择边
def make_random_graph(n, p) # ER 图 G(n, p)
```

## 2.5 连通图

> *"To check whether a graph is connected, we can start at any node, find all reachable nodes, and see if we can reach every node in the graph. The algorithm is a depth-first search (DFS): start at a node, and when you visit a node, add its neighbors to a stack of nodes to visit."*
> 检查图是否连通的方法是：从任意节点出发，找到所有可达节点，看是否能到达图中的每个节点。该算法是**深度优先搜索（DFS）**：从一个节点开始，访问一个节点时将其邻居加入待访问节点栈。

| 单词/短语 | 注释 |
|-----------|------|
| reachable nodes | 可达节点：从起始节点通过边可以到达的所有节点 |
| depth-first search (DFS) | 深度优先搜索：沿着一条路径尽可能深入，回溯后再探索其他分支 |
| stack | 栈：后进先出（LIFO）的数据结构，DFS 的核心数据结构 |
| neighbor | 邻居：与给定节点直接相连的节点 |

```python
def reachable_nodes(G, start):   # DFS 找到从 start 可达的所有节点
def is_connected(G):             # 图是否连通
```

**算法**：从起始节点开始，标记为"seen"，将邻居加入栈，循环直到栈空。如果 seen 的节点数 = 总节点数 → 连通。

## 2.6 生成 ER 图

> *"To implement make_random_graph, we use a helper function flip that returns True with probability p. We call flip for each possible edge and add the edge if it returns True."*
> 实现 `make_random_graph` 时，使用辅助函数 `flip`，它以概率 p 返回 True。对每条可能的边调用 `flip`，如果返回 True 则添加该边。

| 单词/短语 | 注释 |
|-----------|------|
| flip | 抛硬币：以概率 p 返回 True 的函数，模拟伯努利试验 |
| helper function | 辅助函数：为实现主函数而编写的小型工具函数 |
| np.random.random() | NumPy 生成 [0, 1) 均匀分布的随机数，用于概率判断 |

```python
def flip(p):
    return np.random.random() < p    # 以概率 p 返回 True
```

## 2.7 连通概率

> *"To estimate the probability that a random graph is connected, we generate many random graphs and count how many of them are connected. We can explore a range of p values using np.logspace to sample evenly on a log scale."*
> 估计随机图连通概率的方法是：生成大量随机图，统计其中连通的比例。使用 `np.logspace` 在**对数尺度**上均匀采样 p 值以探索 p 的取值范围。

| 单词/短语 | 注释 |
|-----------|------|
| estimate | 估计：通过模拟实验近似计算理论概率 |
| log scale | 对数尺度：以 10 的幂次而非线性间隔采样，便于覆盖多个数量级 |
| np.logspace | NumPy 函数，在对数尺度上均匀生成数值序列 |
| abrupt transition | 陡峭过渡：临界值附近连通概率从接近 0 跃升到接近 1 |

- 对给定 n 和 p，生成大量随机图，统计连通比例
- 使用 `np.logspace` 在 log 尺度上均匀采样 p
- 实验结果与 Erdős-Rényi 的解析结果一致

> *"As n increases, the critical value gets smaller and the transition gets more abrupt."*
> 随着 n 的增大，临界值变得更小，过渡变得更加陡峭。

| 单词/短语 | 注释 |
|-----------|------|
| critical value | 临界值：p* = ln(n)/n，随 n 增大而减小 |
| abrupt | 陡峭的：过渡区域在参数空间中越来越窄 |
| transition | 过渡：从不连通到连通的行为变化 |

- 随着 n 增大，临界值变小，过渡更陡峭

## 2.8 图算法分析

> *"Each node is added to seen once. Each node is added to stack once for each edge, so the total number of additions is 2m, where m is the number of edges. So the running time of reachable_nodes is O(n + m)."*
> 每个节点被加入 `seen` 集合**一次**，每个节点被加入 `stack` 的次数等于其**度**（邻居数），总加入次数为 2m（m 为边数）。因此 `reachable_nodes` 的运行时间为 **O(n + m)**。

| 单词/短语 | 注释 |
|-----------|------|
| running time | 运行时间：算法执行所需的操作数，通常用大 O 记号表示 |
| O(n + m) | 线性时间：算法复杂度与节点数和边数之和成正比 |
| degree | 度：一个节点的邻居数量 |
| complexity analysis | 复杂度分析：研究算法资源消耗（时间、空间）随输入规模的增长趋势 |

`reachable_nodes` 的时间复杂度：
- 每个节点被加入 seen **1 次**
- 每个节点被加入 stack **k 次**（k = 度数）
- 总 stack 添加次数 = 2m（m = 边数，每条边考虑两次）
- **O(n + m)**

> *"In a complete graph, m = n(n-1)/2, so reachable_nodes is O(n²). In general, m could be as large as n², but for many real-world graphs, m is much smaller."*
> 在完全图中，m = n(n-1)/2，因此 `reachable_nodes` 为 **O(n²)**。一般而言，m 最大可达 n²，但许多真实世界图的 m 远小于此。

| 单词/短语 | 注释 |
|-----------|------|
| complete graph | 完全图：边数 m = n(n-1)/2，为图的最大可能边数 |
| O(n²) | 平方时间：复杂度与节点数的平方成正比 |
| real-world graphs | 真实世界图：社交网络、互联网等实际网络的图表示，通常边数远小于 n² |
| sparse graph | 稀疏图：边数远小于最大可能边数（n²）的图 |

- 完全图中 m = n(n-1)/2 → **O(n²)**

## 2.9 练习

| 练习 | 内容 |
|------|------|
| 2.1 | 运行 chap02.ipynb 代码 |
| 2.2 | 分析 `is_connected` 的复杂度 |
| 2.3 | 优化 `reachable_nodes`（先检查 seen 再加 stack），是否改变复杂度？ |
| 2.4 | 实现 G(n, m) 模型（固定边数而非边概率），对比实验结果 |

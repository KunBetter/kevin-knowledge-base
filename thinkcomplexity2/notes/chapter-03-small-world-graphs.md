# 第三章：小世界图（Small World Graphs）

## 3.1 斯坦利·米尔格拉姆（Stanley Milgram）

> *"Stanley Milgram was an American social psychologist who conducted two of the most famous experiments in social science. In his small-world experiment, Milgram sent packets to randomly-selected people in Wichita, Kansas and Omaha, Nebraska, with instructions to try to get the packets to a target person in Sharon, Massachusetts."*

> 斯坦利·米尔格拉姆是一位美国社会心理学家，他进行了社会科学领域最著名的两个实验。在他的小世界实验中，米尔格拉姆将信件寄给了堪萨斯州威奇托和内布拉斯加州奥马哈的随机选取的居民，指示他们设法将信件送达马萨诸塞州沙伦的目标人物。

| 单词/短语 | 注释 |
|-----------|------|
| social psychologist | 社会心理学家：研究社会互动和社会环境如何影响个体行为的心理学家 |
| small-world experiment | 小世界实验：米尔格拉姆设计的实验，旨在测量社交网络中任意两人之间的路径长度 |
| packets | 信件/包裹：实验中传递的信件，内含关于目标人物的信息以及转发规则 |
| randomly-selected | 随机选取的：实验设计的核心要素，起始参与者不是特别筛选的，而是随机选出的普通人 |
| target person | 目标人物：实验设定的最终收件人，起始参与者通常不认识此人 |
| instructions | 指示/规则：转寄规则 —— 认识目标就直寄，否则转给更可能认识目标的亲友 |

> *"The median number of steps was between five and six — a result that inspired the phrase 'six degrees of separation.' If you assume that each person knows about 50 friends within 50 miles, covering the 1600 miles from Wichita to Boston would take about 32 hops, not 6."*

> 步数的中位数在五到六之间 —— 这一结果催生了"六度分隔"这个说法。如果假设每个人认识大约 50 个 50 英里范围内的朋友，那么从威奇托到波士顿 1600 英里的距离大约需要 32 跳，而不是 6 跳。

| 单词/短语 | 注释 |
|-----------|------|
| median | 中位数：将所有成功送达的信件步数排序后位于中间的值，比均值更能抵抗极端值的干扰 |
| six degrees of separation | 六度分隔：指地球上任意两个人之间最多通过六个中间人即可建立联系的概念 |
| hops | 跳：网络中从一节点到另一节点所经过的边数，即路径长度 |
| 1600 miles | 1600 英里：威奇托到波士顿的大致地理距离，按每人认识 50 英里内好友计算需多次中转 |

**小世界实验**：
- 信件从 Kansas 州 Wichita 随机居民出发，目标是 Massachusetts 州 Sharon 的目标人物
- 规则：认识目标人物则直接寄送；否则转发给更可能认识的亲友
- **结果**：成功送达的信件平均转发次数 ≈ **6 次** → "**六度分隔**"
- 如果按地理距离线性计算（平均每人认识 50 英里内的朋友，Boston-Wichita ≈ 1600 英里），需要 **32 跳**而非 6 跳

## 3.2 Watts 和 Strogatz 模型

1998 年发表于 *Nature*。

> *"In 1998, Duncan Watts and Steven Strogatz published 'Collective dynamics of small-world networks' in Nature. They proposed a model that generates graphs with high clustering, like a regular graph, and short path lengths, like a random graph."*

> 1998 年，邓肯·沃茨和史蒂文·斯特罗加茨在《自然》杂志上发表了《小世界网络的集体动力学》。他们提出了一个模型，该模型生成的图同时具有像规则图一样的高聚类，以及像随机图一样的短路径长度。

| 单词/短语 | 注释 |
|-----------|------|
| collective dynamics | 集体动力学：研究由大量相互作用的个体组成的系统如何产生全局行为 |
| small-world networks | 小世界网络：同时具有高聚类系数和短平均路径长度的网络 |
| regular graph | 规则图：每个节点度数相同、结构高度有序的图 |
| random graph | 随机图：边以一定概率随机连接生成的图，Erdős–Rényi 模型是其典型 |

> *"Regular graphs have high clustering and high average path length. Random graphs have low clustering and low average path length. Neither is like real social networks, which combine high clustering with low average path length."*

> 规则图具有高聚类和高平均路径长度。随机图具有低聚类和低平均路径长度。两者都不像真实的社交网络，后者兼具高聚类和低平均路径长度。

| 单词/短语 | 注释 |
|-----------|------|
| clustering | 聚类/聚集：节点的邻居之间互为邻居的程度，衡量局部紧密程度 |
| average path length | 平均路径长度：图中所有节点对之间最短路径的平均值，衡量全局"大小" |
| real social networks | 真实社交网络：如 Facebook 好友网络、科学家合作网络等实测数据 |
| combine | 兼具/组合：真实网络同时呈现两种看似矛盾的属性 |

**两种基准图的缺陷**：

| 类型 | 聚类系数 | 路径长度 |
|------|---------|---------|
| 规则图（Regular） | 高 | 高 |
| 随机图（Random） | 低 | 低 |
| 真实社交网络 | **高** | **低** |

两种基准图都不匹配真实网络。

> *"Watts and Strogatz start with a regular graph where each node is connected to k neighbors. Then they consider each edge and, with probability p, rewire it — that is, they replace it with a random edge. When p = 0, the graph is regular; when p = 1, it is completely random."*

> 沃茨和斯特罗加茨从一个每个节点连接 k 个邻居的规则图开始。然后，对于每条边，以概率 p 进行重连 —— 即将其替换为一条随机边。当 p = 0 时，图是规则的；当 p = 1 时，图是完全随机的。

| 单词/短语 | 注释 |
|-----------|------|
| rewire | 重连：将一条边的端点之一改为随机节点，是 WS 模型的核心操作 |
| probability p | 概率 p：WS 模型唯一的关键参数，决定了图的规则程度与随机程度 |
| completely random | 完全随机：所有边都已重连，图退化为近似 Erdős–Rényi 随机图 |

**WS 生成模型**：
1. 从 n 个节点的规则图开始，每节点连 k 个邻居
2. 以概率 **p** "重连"边 → 替换为随机边
3. p=0 = 规则图，p=1 = 完全随机图

**关键发现**：很小的 p 就产生**高聚类 + 低路径长度**。

## 3.3 环状格（Ring Lattice）

```python
def adjacent_edges(nodes, halfk):
    n = len(nodes)
    for i, u in enumerate(nodes):
        for j in range(i+1, i+halfk+1):
            v = nodes[j % n]    # 取模实现环绕
            yield u, v
```

- n 个节点环形排列，每个节点连接 k 个最近邻居

## 3.4 WS 图的生成

```python
def rewire(G, p):
    nodes = set(G)
    for u, v in G.edges():
        if flip(p):
            choices = nodes - {u} - set(G[u])  # 排除自环和重复边
            new_v = np.random.choice(list(choices))
            G.remove_edge(u, v)
            G.add_edge(u, new_v)
```

## 3.5 聚类系数（Clustering Coefficient）

> *"The clustering coefficient of a node is the fraction of pairs of its neighbors that are connected to each other. If all of a node's neighbors are friends with each other, the clustering coefficient is 1; if none of them are connected, it is 0. The network average clustering coefficient is the mean of the clustering coefficients for all nodes."*

> 一个节点的聚类系数是其邻居之间相互连接的成对比例。如果一个节点的所有邻居彼此都是朋友，聚类系数为 1；如果它们之间没有任何连接，则为 0。网络平均聚类系数是所有节点聚类系数的均值。

| 单词/短语 | 注释 |
|-----------|------|
| clustering coefficient | 聚类系数：衡量节点局部邻域紧密程度的指标，取值 0 到 1 |
| fraction of pairs | 成对比例：实际存在的邻居间边数除以理论上可能的邻居间最大边数 |
| network average | 网络平均值：对整个网络所有节点的局部聚类系数取算术平均 |
| mean | 均值：将 C_u 对所有节点 u 求和后除以节点总数 |

```python
def node_clustering(G, u):
    neighbors = G[u]
    k = len(neighbors)
    if k < 2:
        return np.nan
    possible = k * (k-1) / 2       # 邻居之间可能的最大边数
    exist = sum(1 for v, w in all_pairs(neighbors) if G.has_edge(v, w))
    return exist / possible
```

- **局部聚类系数 C_u**：节点 u 的邻居之间实际存在的边 ÷ 可能存在的最大边数
- **网络平均聚类系数 ¯C**：所有节点的 C_u 均值
- 环状格中 k=4 时，每个节点 C_u = **0.5**

## 3.6 最短路径长度

```python
def characteristic_path_length(G):
    return np.mean(path_lengths(G))
```

- L = 所有节点对最短路径的平均值

> *"The characteristic path length — also called the average shortest path length — is the mean of the shortest path lengths between all pairs of nodes. In a small-world network, this value is surprisingly small even when the graph contains thousands or millions of nodes."*

> 特征路径长度 —— 也称为平均最短路径长度 —— 是所有节点对之间最短路径长度的平均值。在小世界网络中，即使图包含数千或数百万个节点，这个值也出人意料地小。

| 单词/短语 | 注释 |
|-----------|------|
| characteristic path length | 特征路径长度：网络全局连通性的核心度量指标，记作 L |
| shortest path lengths | 最短路径长度：两个节点之间所需经过的最少边数 |
| surprisingly small | 出人意料地小：即使在大规模网络中，任意两点之间通常只需几步即可到达 |
| mean | 均值：所有 (u,v) 节点对的路径长度总和的平均值 |

## 3.7 WS 实验复现

参数：n=1000, k=10, p ∈ [10⁻⁴, 1], 每个 p 生成 20 个图取平均。

> *"As p increases, L(p) drops quickly, because even a small number of randomly rewired edges provides shortcuts that connect distant parts of the graph. But C(p) drops more slowly, because the rewired edges usually don't change local clustering very much. As a result, there is a wide range of p where the graph has both high clustering and low average path length."*

> 随着 p 增加，L(p) 急剧下降，因为即使少量随机重连的边也提供了连接图中遥远部分的捷径。但 C(p) 下降得更慢，因为重连的边通常不会对局部聚类产生太大影响。因此，存在一个宽范围的 p，使得图同时具有高聚类和低平均路径长度。

| 单词/短语 | 注释 |
|-----------|------|
| L(p) | 作为重连概率 p 的函数的平均路径长度 |
| C(p) | 作为重连概率 p 的函数的聚类系数 |
| drops quickly | 急剧下降：L 对少量随机重连极其敏感，几根"捷径"就能大幅缩短全局距离 |
| shortcuts | 捷径：跨越图中远距离区域的边，大幅缩短节点间的路径长度 |
| distant parts | 遥远部分：在规则图中相距较远的节点群，原本需要多步才能到达 |
| wide range | 宽范围：小世界特性不是某个精确 p 值独有的，而存在于一段区间内 |

**核心发现**：
- L(p) 急剧下降（少量随机"捷径"大幅缩短全局距离）
- C(p) 缓慢下降（局部连接的影响较小）
- 存在宽范围的 p，使得图同时具有**高聚类 + 低路径长度**

## 3.8 这算哪门子解释？

> *"Is this an explanation? Is it a satisfying one? The Watts-Strogatz model is more abstract than the traditional model of planetary motion. It is not based on fundamental physical laws, and it does not make precise, falsifiable predictions."*

> 这算是一种解释吗？这是一种令人满意的解释吗？Watts-Strogatz 模型比传统的行星运动模型更加抽象。它不基于基本的物理定律，也不做出精确的、可证伪的预测。

| 单词/短语 | 注释 |
|-----------|------|
| explanation | 解释：科学理论或模型的核心功能之一 —— 说明现象"为什么"发生 |
| satisfying | 令人满意的：科学解释的质量评判维度，不仅关乎正确性，还涉及直觉接受度 |
| abstract | 抽象的：WS 模型剥离了具体的社会机制，只保留最少的数学结构 |
| fundamental physical laws | 基本物理定律：如牛顿引力定律，可从第一原理推导出精确的行星轨道 |
| falsifiable predictions | 可证伪的预测：根据波普尔的科学哲学，能够被实验驳倒的预测是科学理论的重要标准 |

> *"The Watts-Strogatz model is an example of a new kind of scientific model, one that is less like a mathematical proof and more like a demonstration. But that does not mean it is a worse kind of explanation — just different. It reveals a mechanism that might be at work in real networks."*

> Watts-Strogatz 模型是一种新型科学模型的例子，它不太像数学证明，而更像是一种演示示范。但这并不意味着它是一种更差的解释 —— 只是不同而已。它揭示了一种可能在真实网络中起作用的机制。

| 单词/短语 | 注释 |
|-----------|------|
| mathematical proof | 数学证明：从公理出发通过严格逻辑推导得出结论，传统物理学模型的理想形式 |
| demonstration | 演示/示范：通过构建简单例子并展示其行为来说明原理，WS 模型本质上是一种"思想实验" |
| mechanism | 机制：产生现象的具体因果过程或规则，如重连边产生捷径 |
| at work | 在起作用/在运作：指某种因果机制在实际系统中真实存在并产生影响 |

对比两种科学解释范式：

| 传统模型（行星轨道） | WS 模型 |
|---------------------|---------|
| 基于物理定律，方程可解析 | 更抽象，基于模拟 |
| 形式接近数学证明 | 更接近举例示范 |

作者提出的核心问题：
- 这类模型做**预测**还是**解释**？
- 抽象模型的解释是否比传统模型**不够令人满意**？
- 是**种类**不同还是**程度**不同？

## 3.9 广度优先搜索（BFS）

```python
from collections import deque

def reachable_nodes_bfs(G, start):
    seen = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()    # FIFO，而非 LIFO
        if node not in seen:
            seen.add(node)
            queue.extend(G.neighbors(node))
    return seen
```

> *"Breadth-First Search explores a graph by processing nodes in order of their distance from a starting node. It uses a queue, which is a first-in-first-out (FIFO) data structure. If we used a list and called pop(0), removing the first element takes time proportional to the length of the list. Using collections.deque makes both appends and pops at the ends run in constant time."*

> 广度优先搜索通过按节点与起点的距离顺序处理节点来探索图。它使用队列（queue），这是一种先进先出（FIFO）的数据结构。如果我们使用列表并调用 pop(0)，移除第一个元素所需的时间与列表长度成正比。使用 collections.deque 使得在两端追加和弹出的操作都是常数时间。

| 单词/短语 | 注释 |
|-----------|------|
| Breadth-First Search (BFS) | 广度优先搜索：按距离层逐层扩展的图遍历算法，保证先访问离起点更近的节点 |
| queue | 队列：FIFO 数据结构，元素从一端入队、从另一端出队 |
| FIFO | 先进先出：First-In-First-Out，最早入队的元素最先被处理 |
| deque | 双端队列（double-ended queue）：Python collections 模块提供的 O(1) 两端操作的数据结构 |
| pop(0) | 从列表头部弹出元素，时间复杂度为 O(n)，因为需要移动所有后续元素 |
| constant time | 常数时间 O(1)：操作时间不随数据规模增长而变化 |

- 用 list 的 `pop(0)` 是 O(n)，改用 deque → **O(n + m)**
- BFS 保证按**距离层**处理节点 —— Dijkstra 算法的前提

## 3.10 Dijkstra 算法（简化版）

```python
def shortest_path_dijkstra(G, source):
    dist = {source: 0}
    queue = deque([source])
    while queue:
        node = queue.popleft()
        new_dist = dist[node] + 1
        neighbors = set(G[node]).difference(dist)
        for n in neighbors:
            dist[n] = new_dist
        queue.extend(neighbors)
    return dist
```

> *"Dijkstra's algorithm computes the shortest path from a source node to every other node in a graph. When working with unweighted graphs — where every edge has the same weight — Dijkstra's algorithm is equivalent to BFS. The key requirement is that nodes must be processed in order of distance from the source; using DFS would yield incorrect distances."*

> Dijkstra 算法计算从源节点到图中所有其他节点的最短路径。在处理无权重图时 —— 每条边的权重相同 —— Dijkstra 算法等价于 BFS。关键要求是必须按照与源节点距离的顺序处理节点；使用 DFS 会得出错误的距离值。

| 单词/短语 | 注释 |
|-----------|------|
| Dijkstra's algorithm | 迪杰斯特拉算法：经典的图最短路径算法，适用于边权重非负的有权图或有向图 |
| source node | 源节点：算法从该节点出发，计算其到所有其他节点的最短距离 |
| unweighted graphs | 无权重图：所有边的代价相同的图，此时每条边视为权重 1 |
| equivalent | 等价的：在无权图中 Dijkstra 简化为 BFS，因为按距离递增顺序即是按跳数递增 |
| DFS | 深度优先搜索（Depth-First Search）：使用栈（LIFO）的遍历策略，不保证按距离顺序访问 |
| incorrect distances | 错误的距离值：若用 DFS，节点可能通过更长路径被先访问并锁定距离值，导致结果错误 |

**必须用 BFS**：先处理完距离 d 的节点再处理距离 d+1 的节点。若用 DFS 会得到错误的距离值。

## 3.11 练习

| 练习 | 内容 |
|------|------|
| 3.1 | 实现 `make_regular_graph(n, k)`，k 为奇数也能构造 |
| 3.2 | 对比 `reachable_nodes_bfs` 和 NetworkX 实现的效率 |
| 3.3 | 找出一段 BFS 代码中的两个性能 bug |
| 3.4 | 用 DFS 实现 Dijkstra，观察为什么出错 |
| 3.5 | 设计 WS 模型的变体（不同初始图/不同重连策略），验证**鲁棒性** |
| 3.6 | 实现全对最短路径算法，与运行 n 次 Dijkstra 对比性能 |

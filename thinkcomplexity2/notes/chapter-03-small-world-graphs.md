# 第三章：小世界图（Small World Graphs）

## 3.1 斯坦利·米尔格拉姆（Stanley Milgram）

**小世界实验**：
- 信件从 Kansas 州 Wichita 随机居民出发，目标是 Massachusetts 州 Sharon 的目标人物
- 规则：认识目标人物则直接寄送；否则转发给更可能认识的亲友
- **结果**：成功送达的信件平均转发次数 ≈ **6 次** → "**六度分隔**"
- 如果按地理距离线性计算（平均每人认识 50 英里内的朋友，Boston-Wichita ≈ 1600 英里），需要 **32 跳**而非 6 跳

## 3.2 Watts 和 Strogatz 模型

1998 年发表于 *Nature*。

**两种基准图的缺陷**：

| 类型 | 聚类系数 | 路径长度 |
|------|---------|---------|
| 规则图（Regular） | 高 | 高 |
| 随机图（Random） | 低 | 低 |
| 真实社交网络 | **高** | **低** |

两种基准图都不匹配真实网络。

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

## 3.7 WS 实验复现

参数：n=1000, k=10, p ∈ [10⁻⁴, 1], 每个 p 生成 20 个图取平均。

**核心发现**：
> L(p) 急剧下降（少量随机"捷径"大幅缩短全局距离），但 C(p) 缓慢下降（局部连接的影响较小）。存在宽范围的 p，使得图同时具有**高聚类 + 低路径长度**。

## 3.8 这算哪门子解释？

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

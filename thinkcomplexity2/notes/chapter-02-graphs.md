# 第二章：图（Graphs）

## 2.1 什么是图？

- **节点（nodes/vertices）**：表示系统中有哪些离散元素
- **边（edges）**：表示元素之间的连接
- 边可以有属性：长度、成本、权重
- 边可以是**有向**或**无向**的
- **路径（path）**：节点序列，每对连续节点之间有一条边
- 图论是研究图的数学分支

## 2.2 NetworkX

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

**Erdős-Rényi 模型**（ER 图）：
- 参数：n（节点数）、p（边概率）
- 关键发现：随机图的属性存在**突变**
- **连通性临界值**：p* = ln(n)/n
  - p < p* → 几乎不连通
  - p > p* → 几乎一定连通

## 2.4 生成图

```python
def all_pairs(nodes):       # 枚举所有节点对
def make_complete_graph(n)  # 完全图（每对节点之间都有边）
def random_pairs(nodes, p)  # 以概率 p 选择边
def make_random_graph(n, p) # ER 图 G(n, p)
```

## 2.5 连通图

```python
def reachable_nodes(G, start):   # DFS 找到从 start 可达的所有节点
def is_connected(G):             # 图是否连通
```

**算法**：从起始节点开始，标记为"seen"，将邻居加入栈，循环直到栈空。如果 seen 的节点数 = 总节点数 → 连通。

## 2.6 生成 ER 图

```python
def flip(p):
    return np.random.random() < p    # 以概率 p 返回 True
```

## 2.7 连通概率

- 对给定 n 和 p，生成大量随机图，统计连通比例
- 使用 `np.logspace` 在 log 尺度上均匀采样 p
- 实验结果与 Erdős-Rényi 的解析结果一致
- 随着 n 增大，临界值变小，过渡更陡峭

## 2.8 图算法分析

`reachable_nodes` 的时间复杂度：
- 每个节点被加入 seen **1 次**
- 每个节点被加入 stack **k 次**（k = 度数）
- 总 stack 添加次数 = 2m（m = 边数，每条边考虑两次）
- **O(n + m)**
- 完全图中 m = n(n-1)/2 → **O(n²)**

## 2.9 练习

| 练习 | 内容 |
|------|------|
| 2.1 | 运行 chap02.ipynb 代码 |
| 2.2 | 分析 `is_connected` 的复杂度 |
| 2.3 | 优化 `reachable_nodes`（先检查 seen 再加 stack），是否改变复杂度？ |
| 2.4 | 实现 G(n, m) 模型（固定边数而非边概率），对比实验结果 |

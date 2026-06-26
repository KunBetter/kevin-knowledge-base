# 第四章：无标度网络（Scale-Free Networks）

## 核心问题

WS 模型捕捉了**高聚类 + 短路径**，但度分布太均匀。真实网络中少数节点有海量连接（如社交网络的大 V），大部分节点连接很少——这就是**重尾分布（heavy-tailed distribution）**。

| 特性 | WS 模型 | BA 模型 |
|------|---------|---------|
| 高聚类（C） | ✅ | ❌ |
| 短路径（L） | ✅ | ✅ |
| 重尾度分布 | ❌ | ✅ |

## 4.1 社交网络数据

**Facebook 数据集**（SNAP / Stanford）：

```
节点数: 4039
边数:   88,234
平均度: 43.7
聚类系数 C: 0.61（高）
平均路径 L: 3.69（短）
```

确认 Facebook 网络是**小世界网络**。

**抽样估计**（全量 O(nk²) 太慢）：

```python
from networkx.algorithms.approximation import average_clustering
C = average_clustering(G, trials=1000)

def estimate_path_length(G, nodes=None, trials=1000):
    return np.mean(sample_path_lengths(G, nodes, trials))
```

## 4.2 WS 模型拟合测试

以 n=4039, k=44 构建 WS 图：

| p 值 | C | L | 评价 |
|------|---|---|------|
| p=0（环状格） | 0.73 偏高 | 46 太高 | ❌ |
| p=1（完全随机） | 0.011 太低 | 2.6 太短 | ❌ |
| **p=0.05** | **0.63** | **3.2** | ✅ 匹配 |

p=0.05 时 C 和 L 都很接近，但**度分布暴露问题**：

| 指标 | Facebook | WS 模型 |
|------|----------|---------|
| 平均度 | 43.7 | 44 ✅ |
| 度的标准差 | **52.4** | **1.5** ❌ |

WS 模型中几乎所有节点度在 38~50，而 Facebook 中有人只有 1 个朋友，有人超过 1000 个。

## 4.4 重尾分布与幂律

**重尾分布**：大量小值 + 少量极大值，在 log-log 坐标下近似直线。

**幂律关系**：PMF(k) ∼ k^{-α}

取对数：log PMF(k) ∼ -α·log k → 斜率为 -α 的直线。

## 4.5 Barabási-Albert 模型

1999 年，Barabási 和 Albert 提出了能生成幂律度分布的模型。两个核心机制：

**🌱 增长（Growth）**：不是从固定节点数开始，而是**逐个添加节点**。

**🔗 优先连接（Preferential Attachment）**：新边更可能连接到**已有很多连接的节点**——"富者愈富"效应。

**综合对比**：

| 指标 | Facebook | WS | BA |
|------|----------|-----|-----|
| C | 0.61 | 0.63 ✅ | 0.037 ❌ |
| L | 3.69 | 3.23 ✅ | 2.51 ✅ |
| 平均度 | 43.7 | 44 ✅ | 43.7 ✅ |
| 度标准差 | 52.4 | 1.5 ❌ | **40.1** ✅ |
| 幂律？ | 可能 | 否 | ✅ |

**BA 模型解决了度分布问题，但失去了高聚类。**

## 4.6 BA 图的生成算法

```python
def barabasi_albert_graph(n, k):
    G = nx.empty_graph(k)
    targets = list(range(k))
    repeated_nodes = []

    for source in range(k, n):
        G.add_edges_from(zip([source]*k, targets))
        repeated_nodes.extend(targets)
        repeated_nodes.extend([source] * k)
        targets = _random_subset(repeated_nodes, k)
    return G
```

**`repeated_nodes`** 是关键：每个节点出现的次数 = 度数。随机选取时，度越大的节点被选中的概率越大。

## 4.7 累积分布函数（CDF / CCDF）

- **CDF**（累积分布函数）：值 ≤ x 的比例，比 PMF 噪声更小
- **CCDF**（互补累积分布函数）：1 - CDF(x)。若 PMF 服从幂律，CCDF 也服从幂律
- CCDF 在 log-log 图上是直线（斜率为 -α），能更清楚地显示尾部匹配情况
- BA 模型在尾部（度 > 20）匹配得很好，WS 完全不匹配

## 4.8 解释性模型（Explanatory Models）

**解释性模型的逻辑结构**：

```
现实系统 S → 观察现象 O
    ↓ 类比
模型 M → 行为 B
    ↓
结论：S 表现 O 是因为 M 表现 B，B 类似 O
```

本质是**类比推理**，不是数学证明。

**小世界现象的两种竞争解释**：

| 模型 | 解释路径 |
|------|---------|
| **WS 模型** | 紧密聚类 + 跨越集群的"**弱连接**"（weak ties）→ 短路径 |
| **BA 模型** | 优先连接 → 生长出高 degree 的"**枢纽节点**"（hubs）→ 短路径 |

在年轻科学领域，问题往往不是缺少解释，而是**解释太多**。

## 4.9 练习

| 练习 | 内容 |
|------|------|
| 4.1 | "弱连接" v.s. "枢纽"两种解释是否兼容？如何设计实验区分？阅读 Kuhn 的论文 |
| 4.2 | 用 **Holme-Kim 模型**（`powerlaw_cluster_graph`）同时满足幂律度分布和高聚类 |
| 4.3 | 分析**演员合作网络**数据，绘制 PMF/CDF/CCDF |

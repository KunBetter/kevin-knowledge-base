# 第12章：合作的进化 (Evolution of Cooperation)

> 最后一章，处理两个问题：生物学的**利他主义问题**和道德哲学中的**人性问题**。工具：基于代理的模拟 + **博弈论**（囚徒困境）。

---

## 📖 12.1 囚徒困境 (Prisoner's Dilemma)

### Original Text — 经典设定

> *"Two members of a criminal gang are arrested and imprisoned. Each prisoner is in **solitary confinement** with no means of communicating with the other. The prosecutors lack sufficient evidence to convict the pair on the principal charge, but they have enough to convict both on a **lesser charge**. Simultaneously, the prosecutors offer each prisoner a bargain."*
> 一个犯罪团伙的两名成员被逮捕并关押。每名囚犯都被**单独监禁**，彼此之间没有任何沟通手段。检察官缺乏足够的证据以主要罪名定罪二人，但有足够证据以一项**较轻的罪名**定罪。与此同时，检察官向每名囚犯提供了一项交易。

| 单词/短语 | 注释 |
|-----------|------|
| solitary confinement | 单独监禁，囚犯被完全隔离，无法与外界或同伙交流 |
| principal charge | 主要罪名，指更严重的犯罪指控 |
| lesser charge | 较轻的罪名，检察官的退而求其次——他们真正想要的是让囚犯互相揭发 |
| bargain | 交易/协议，此处指检察官提出的"背叛换减刑"的诱人条件 |

### 收益矩阵 (Payoff Matrix)

| A \ B | B 保持沉默 (Cooperate) | B 背叛 (Defect) |
|--------|----------------------|----------------|
| A 沉默 (Cooperate) | 各判 **1 年** | A: 3 年, B: **0 年** |
| A 背叛 (Defect) | A: **0 年**, B: 3 年 | 各判 **2 年** |

### 理性分析：为什么背叛是"理性"的？

> *"Looking at it from **A's point of view**:*
> - *If B remains silent, A is **better off defecting**; she would go free rather than serve 1 year.*
> - *If B defects, A is **still better off defecting**; she would serve only 2 years rather than 3.*
>
> *"**No matter what B does**, A is better off defecting. And because the game is **symmetric**, this analysis is the same from B's point of view."*
> 从**A的视角**来看：
> - 如果B保持沉默，A**选择背叛更划算**——她可以直接获释，而不是服刑1年。
> - 如果B也选择背叛，A**仍然选择背叛更划算**——她只需服刑2年而非3年。
>
> **无论B怎么做**，A选择背叛都更有利。而由于博弈是**对称的**，从B的视角分析也是同样的结论。

| 单词/短语 | 注释 |
|-----------|------|
| better off | 更有利/更划算，在博弈论中指获得更高的收益 |
| No matter what | 无论……如何，这是"占优策略"的核心逻辑——对手的任何选择都不能改变结论 |
| symmetric | 对称的，博弈论中指双方收益矩阵完全相同，角色完全可互换 |
| defecting | 背叛，囚徒困境中指揭发同伙以换取个人减刑 |

> *"Under those assumptions, the **rational choice** for both agents is to defect. But for the prisoners, it is frustrating because there is, apparently, **nothing** they can do to achieve the outcome they both want."*
> 在这些假设下，双方代理的**理性选择**都是背叛。但对囚犯来说，这令人沮丧——因为表面上，他们**没有任何办法**实现双方都想要的结果（即双方合作、各判1年）。

| 单词/短语 | 注释 |
|-----------|------|
| rational choice | 理性选择，博弈论中基于个人收益最大化的计算得出的最优决策 |
| frustrating | 令人沮丧的，因为个体理性导致集体次优结果——这正是囚徒困境的悲剧性所在 |
| outcome they both want | 双方共同期望的结果，即（合作，合作），各判1年，这是帕累托优于（背叛，背叛）的结果 |

### 🔬 Python — 囚徒困境收益计算

```python
"""
Prisoner's Dilemma: single-round payoff analysis.
Cooperate = C, Defect = D.
"""
import numpy as np

# Payoff matrix: (A_score, B_score)
payoffs = {
    ('C', 'C'): (3, 3),   # both silent → 1 year each → 3 points
    ('C', 'D'): (0, 5),   # A silent, B betrays
    ('D', 'C'): (5, 0),   # A betrays, B silent
    ('D', 'D'): (1, 1),   # both betray → 2 years each → 1 point
}

def analyze_dilemma():
    """Show why defection is the dominant strategy."""
    for opponent_move in ['C', 'D']:
        print(f"\nIf opponent plays {opponent_move}:")
        for my_move in ['C', 'D']:
            score = payoffs[(my_move, opponent_move)][0]
            print(f"  I play {my_move} → score = {score}")

    print("\n>>> Defect dominates: regardless of opponent's move,")
    print("    defecting always yields a higher score.")

analyze_dilemma()
```

```
If opponent plays C:
  I play C → score = 3
  I play D → score = 5

If opponent plays D:
  I play C → score = 0
  I play D → score = 1

>>> Defect dominates: regardless of opponent's move,
    defecting always yields a higher score.
```

---

## 📖 12.2 "好人"问题 (The Problem of Nice)

### Original Text — 实验观察

> *"If we assume that people are smart enough to do the analysis and that they generally act in their own interest, we would expect them to defect pretty much all the time. **But they don't.** In most experiments, subjects **cooperate much more** than the rational agent model predicts."*
> 如果我们假设人们足够聪明来做上述分析，并且通常按照自身利益行事，我们会预期他们几乎总是选择背叛。**但他们并没有。**在大多数实验中，受试者的**合作频率远高于**理性代理模型的预测。

| 单词/短语 | 注释 |
|-----------|------|
| act in their own interest | 按自身利益行事，博弈论中"理性人"假设的核心 |
| subjects | 受试者，行为经济学和实验博弈论中参与实验的人类被试 |
| rational agent model | 理性代理模型，预测每个人都会选择占优策略（背叛）的理论模型 |
| cooperate much more | 合作频率远高于预测，这是行为经济学经典发现——人类并非纯粹自私的理性计算器 |

### 为什么人们会合作？追问链条

| 层次 | 追问 | 回答 |
|------|------|------|
| 1 | 为什么帮助别人？ | 因为这让他们感觉好 |
| 2 | 为什么做好事让人感觉好？ | 部分是社会教养，但**很大部分是先天的** |
| 3 | 为什么是先天的？ | 大脑发育 → 受**基因**控制 |
| 4 | 为什么利他基因没被淘汰？ | **这就是"利他主义问题"** |

### Original Text — 利他主义的核心悖论

> *"If, under natural selection, animals are in **constant competition** with each other to survive and reproduce, it seems obvious that altruism would be **counterproductive**. In a population where some people help others, even to their own detriment, and others are purely selfish, it seems like the selfish ones would benefit, the altruistic ones would suffer, and the **genes for altruism would be driven to extinction**."*
> 如果在自然选择下，动物之间为生存和繁衍而处于**持续竞争**中，那么利他主义显然是**适得其反**的。在一个群体中，如果一些人帮助他人——甚至不惜损害自身利益——而另一些人纯粹自私，那么看起来自私者会获益，利他者会受损，**利他主义的基因将被推向灭绝**。

| 单词/短语 | 注释 |
|-----------|------|
| natural selection | 自然选择，达尔文进化论的核心机制——适者生存、不适者淘汰 |
| constant competition | 持续竞争，生物个体之间为有限资源（食物、配偶、领地）的永恒斗争 |
| counterproductive | 适得其反/反生产力的，在此指利他行为降低而非提高个体的生存适应性 |
| to their own detriment | 损害自身利益，这是利他主义的定义性特征——施惠者付出代价 |
| driven to extinction | 被推向灭绝，在进化意义上指携带该基因的个体数量逐渐减少直至消失 |

> *"This apparent contradiction is the **'problem of altruism'**: why haven't the genes for altruism died out?"*
> 这一明显的矛盾就是**"利他主义问题"**：为什么利他的基因至今尚未消亡？

| 单词/短语 | 注释 |
|-----------|------|
| apparent contradiction | 明显的矛盾，指自然选择应该淘汰利他基因，但现实中利他行为普遍存在 |
| died out | 消亡/灭绝，进化生物学中指某个性状或基因在种群中完全消失 |

### 传统解释 vs 本章的假说

| 解释 | 说明 |
|------|------|
| 互惠利他 (reciprocal altruism) | 你帮我，我帮你 |
| 性选择 (sexual selection) | 利他是择偶优势 |
| 亲缘选择 (kin selection) | 帮助亲属 = 帮助自己的基因传播 |
| 群体选择 (group selection) | 有利他的群体更有竞争力 |
| **本章假说** | **利他主义本身就是适应性的**（adaptive） |

> *"Maybe genes for altruism make people **more likely** to survive and reproduce. It turns out that the Prisoner's Dilemma, which **raises** the problem of altruism, might also help **resolve** it."*
> 也许利他基因使人们**更有可能**生存和繁衍。事实证明，囚徒困境——这个**提出了**利他主义问题的模型——或许也能帮助我们**解决**它。

| 单词/短语 | 注释 |
|-----------|------|
| more likely | 更有可能，指提高生存和繁殖的概率——这是适应性的核心含义 |
| raises | 提出/引发，囚徒困境的经典分析揭示了合作在理性上不可行，从而"制造"了利他主义问题 |
| resolve | 解决/化解，当博弈从单次变为迭代时，合作反而可能成为进化上的优势策略 |

---

## 📖 12.3 Axelrod 锦标赛 (Prisoner's Dilemma Tournaments)

### Original Text

> *"In the late 1970s **Robert Axelrod**, a political scientist at the University of Michigan, organized a **tournament** to compare strategies for playing Prisoner's Dilemma. He invited participants to submit strategies in the form of computer programs, then played the programs against each other and kept score."*
> 20世纪70年代末，密歇根大学的政治学家**罗伯特·阿克塞尔罗德**组织了一场**锦标赛**来比较囚徒困境的策略。他邀请参赛者以计算机程序的形式提交策略，然后让这些程序互相博弈并计分。

| 单词/短语 | 注释 |
|-----------|------|
| tournament | 锦标赛，多个策略以循环赛制互相对抗，按总得分排名 |
| submit strategies | 提交策略，参赛者编写程序定义在每种历史情境下应该合作还是背叛 |
| kept score | 计分/累计得分，每轮博弈的收益累加决定最终排名 |

> *"They played the **iterated** version of PD, in which the agents play **multiple rounds** against the same opponent, so their decisions can be based on **history**."*
> 他们玩的是**迭代版**囚徒困境——代理与同一个对手进行**多轮**博弈，因此他们的决策可以基于**历史记录**。

| 单词/短语 | 注释 |
|-----------|------|
| iterated | 迭代的/多次重复的，这是使合作成为可能的关键转变——单次博弈没有未来，迭代博弈有"影子" |
| multiple rounds | 多轮，迭代博弈中每一轮都是一次完整的囚徒困境选择，但代理知道还会与同一对手继续博弈 |
| history | 历史记录，代理可以观察对手之前的行为模式并据此调整策略 |

### TFT (Tit for Tat) 策略

> *"TFT always **cooperates** during the first round of an iterated match; after that, it **copies** whatever the opponent did during the previous round. If the opponent keeps cooperating, TFT keeps cooperating. If the opponent defects at any point, TFT defects in the next round. But if the opponent goes back to cooperating, so does TFT."*
> TFT在迭代比赛的第一轮总是**合作**；此后，它完全**复制**对手在上一轮的行为。如果对手持续合作，TFT也持续合作。如果对手在任何一轮背叛，TFT在下一轮就背叛。但如果对手恢复合作，TFT也同样恢复合作。

| 单词/短语 | 注释 |
|-----------|------|
| Tit for Tat | 以牙还牙/一报还一报，这个策略仅需记住对手上一轮做了什么——极其简单但极其有效 |
| copies | 复制/镜像，TFT不做任何预测或复杂计算，只是机械地回应——这种简单性反而是优势 |
| goes back to cooperating | 恢复合作，TFT不记仇——对手回头，它也回头——这体现了"宽恕"特征 |

### 成功策略的四个特征

> *"Looking at the strategies that did well in these tournaments, Axelrod identified the characteristics they tended to share:"*
> 考察在这些锦标赛中表现优异的策略，阿克塞尔罗德识别出了它们倾向于共有的特征：

| 单词/短语 | 注释 |
|-----------|------|
| did well | 表现优异，指在锦标赛中获得较高总分的策略 |
| tended to share | 倾向于共有，不是所有成功策略都完美具备所有特征，而是统计上显著共享这些属性 |

| 特征 | English | 含义 |
|------|---------|------|
| **友善** | Nice | 首轮合作，总体上合作不少于背叛 |
| **报复** | Retaliating | 对背叛做出反应——一直合作不如适时反击 |
| **宽恕** | Forgiving | 不过度记仇——惩罚对手也会惩罚自己 |
| **不嫉妒** | Non-envious | 不追求比对手得分更高，只要自己表现好 |

> *"TFT has **all** of these properties."*
> TFT具备**全部**这些属性。

| 单词/短语 | 注释 |
|-----------|------|
| all of these properties | 全部属性，TFT是唯一同时满足友善、报复、宽恕、不嫉妒四条标准的策略，这解释了它的成功 |

### 🔬 Python — 实现 TFT 及其他策略

```python
"""
Implement key PD strategies as Python functions.
Each strategy sees the history of both players' moves.
"""
import numpy as np

def always_cooperate(my_history, opp_history):
    return 'C'

def always_defect(my_history, opp_history):
    return 'D'

def tit_for_tat(my_history, opp_history):
    """Cooperate first, then copy opponent's last move."""
    if len(opp_history) == 0:
        return 'C'
    return opp_history[-1]

def grudger(my_history, opp_history):
    """Cooperate until opponent defects, then defect forever."""
    if len(opp_history) == 0:
        return 'C'
    if 'D' in opp_history:
        return 'D'
    return 'C'

def random_strategy(my_history, opp_history):
    return np.random.choice(['C', 'D'])

def play_match(strategy_a, strategy_b, n_rounds=10):
    """Simulate one iterated PD match between two strategies."""
    history_a, history_b = [], []
    score_a, score_b = 0, 0

    for _ in range(n_rounds):
        move_a = strategy_a(history_a, history_b)
        move_b = strategy_b(history_b, history_a)
        history_a.append(move_a)
        history_b.append(move_b)
        pay_a, pay_b = payoffs[(move_a, move_b)]
        score_a += pay_a
        score_b += pay_b

    return score_a, score_b

# Test: TFT vs Always Defect
score_tft, score_ad = play_match(tit_for_tat, always_defect, n_rounds=10)
print(f"TFT vs Always Defect (10 rounds):")
print(f"  TFT: {score_tft}, Always Defect: {score_ad}")
# TFT gets: 0 (round1: C vs D) + 1*9 = 9
# AD gets: 5 (round1: D vs C) + 1*9 = 14

# Test: TFT vs Always Cooperate
score_tft2, score_ac = play_match(tit_for_tat, always_cooperate, n_rounds=10)
print(f"TFT vs Always Cooperate (10 rounds):")
print(f"  Both: {score_tft2} each (perfect cooperation)")
```

```
TFT vs Always Defect (10 rounds):
  TFT: 9, Always Defect: 14
TFT vs Always Cooperate (10 rounds):
  Both: 30 each (perfect cooperation)
```

---

## 📖 12.4-12.5 模拟合作的进化 (Simulating Evolution of Cooperation)

### 基因型编码

策略基于对手**前两轮**的选择做决策，基因型为 7 位字符串：

| 位置 | 前两轮对手选择 | 含义 |
|------|--------------|------|
| 0 | `(None, None)` | 首轮 |
| 1 | `(None, 'C')` | 对手首轮合作 |
| 2 | `(None, 'D')` | 对手首轮背叛 |
| 3 | `('C', 'C')` | 对手前两轮都合作 |
| 4 | `('C', 'D')` | 对手先合作后背叛 |
| 5 | `('D', 'C')` | 对手先背叛后合作 |
| 6 | `('D', 'D')` | 对手前两轮都背叛 |

| 策略 | 基因型 | 说明 |
|------|--------|------|
| Always Cooperate | `CCCCCCC` | 永远合作 |
| Always Defect | `DDDDDDD` | 永远背叛 |
| **TFT** | `CCDCDCD` | 首轮合作 + 镜像对手上一轮 |

### Python — Agent 和突变

```python
class PDAgent:
    keys = [(None, None), (None, 'C'), (None, 'D'),
            ('C', 'C'), ('C', 'D'), ('D', 'C'), ('D', 'D')]

    def __init__(self, values, fitness=np.nan):
        self.values = values
        self.responses = dict(zip(self.keys, values))
        self.fitness = fitness
        self.history = []
        self.score = 0

    def reset(self):
        self.history = []
        self.score = 0

    def respond(self, opponent):
        """Decide C or D based on opponent's last two moves."""
        if len(opponent.history) == 0:
            key = (None, None)
        elif len(opponent.history) == 1:
            key = (None, opponent.history[-1])
        else:
            key = (opponent.history[-2], opponent.history[-1])
        return self.responses[key]

    def append(self, resp, pay):
        self.history.append(resp)
        self.score += pay

    def copy(self, prob_mutate=0.05):
        if np.random.random() > prob_mutate:
            values = self.values
        else:
            values = self.mutate()
        return PDAgent(values, self.fitness)

    def mutate(self):
        values = list(self.values)
        index = np.random.choice(len(values))
        values[index] = 'C' if values[index] == 'D' else 'D'
        return values
```

### Tournament 类

```python
class PDTournament:
    payoffs = {('C', 'C'): (3, 3), ('C', 'D'): (0, 5),
               ('D', 'C'): (5, 0), ('D', 'D'): (1, 1)}
    num_rounds = 6  # each genome element has ~equal impact

    def play(self, agent1, agent2):
        agent1.reset(); agent2.reset()
        for _ in range(self.num_rounds):
            resp1 = agent1.respond(agent2)
            resp2 = agent2.respond(agent1)
            pay1, pay2 = self.payoffs[(resp1, resp2)]
            agent1.append(resp1, pay1)
            agent2.append(resp2, pay2)
        return agent1.score, agent2.score

    def melee(self, agents, randomize=True):
        """Pair agents and play matches; assign fitness = avg score/round/opponent."""
        if randomize:
            agents = np.random.permutation(agents)
        n = len(agents)
        i_row = np.arange(n)
        j_row = (i_row + 1) % n  # ring topology
        totals = np.zeros(n)
        for i, j in zip(i_row, j_row):
            score1, score2 = self.play(agents[i], agents[j])
            totals[i] += score1
            totals[j] += score2
        for i in i_row:
            agents[i].fitness = totals[i] / self.num_rounds / 2
```

### Simulation — 继承第 11 章的进化引擎

```python
class PDSimulation:
    def __init__(self, tournament, agents):
        self.tournament = tournament
        self.agents = np.asarray(agents)
        self.instruments = []

    def step(self):
        self.tournament.melee(self.agents)     # set fitness via PD play
        # Then apply differential survival (same as Ch11)
        fits = np.array([a.fitness for a in self.agents])
        is_dead = np.random.random(len(self.agents)) > fits / fits.max()
        index_dead = np.nonzero(is_dead)[0]
        # Replace dead with copies of survivors
        survivors = self.agents[~is_dead]
        replacements = np.random.choice(survivors, size=len(index_dead))
        self.agents[index_dead] = [r.copy() for r in replacements]
        self.update_instruments()
```

---

## 📖 12.6 结果 (Results)

### 初始实验

> *"Suppose we start with a population of three agents: one always cooperates, one always defects, and one plays TFT. The cooperator gets **1.5** points per round, the TFT agent gets **1.9**, and the defector gets **3.33**. This result suggests that 'always defect' should quickly become the dominant strategy."*
> 假设我们从三个代理的群体开始：一个永远合作，一个永远背叛，一个采用TFT。合作者每轮获得**1.5**分，TFT代理获得**1.9**分，而背叛者获得**3.33**分。这个结果表明，"永远背叛"应该迅速成为占优策略。

| 单词/短语 | 注释 |
|-----------|------|
| points per round | 每轮得分，即适应度——多次博弈中平均每轮获得的收益 |
| dominant strategy | 占优策略，在给定种群构成中收益最高、最可能通过选择扩散的策略 |

> *"But 'always defect' contains the **seeds of its own destruction**. If nicer strategies are driven to extinction, the defectors have **no one to take advantage of**. Their fitness drops, and they become **vulnerable to invasion** by cooperators."*
> 但"永远背叛"包含了**自我毁灭的种子**。如果更友善的策略被推向灭绝，背叛者就**没有人可以剥削了**。他们的适应度下降，变得**容易被合作者入侵**。

| 单词/短语 | 注释 |
|-----------|------|
| seeds of its own destruction | 自我毁灭的种子，背叛策略的成功依赖于有合作者可以剥削——消灭合作者也就消灭了自己的优势来源 |
| no one to take advantage of | 无人可以剥削，当所有代理都是背叛者时，他们只能互相背叛，每人都只得到低收益 |
| vulnerable to invasion | 容易被入侵，在低适应度的情况下，任何通过突变出现的友好策略都可能获得更高的相对适应度 |

### 5000 步模拟结果

从 100 个 Always Defect 代理开始：

| 阶段 | 平均适应度 |
|------|----------|
| 初始（全背叛者） | **1.0**（背叛者对背叛者每轮只得 1 分） |
| ~500 步后 | 接近 **3.0**（合作者对合作者的水平） |
| 之后 | 在 2~3 之间**震荡**，长期均值约 **2.5** |

> *"It's not quite a **utopia** of cooperation, which would average 3 points per round, but it's a long way from the **dystopia** of perpetual defection."*
> 这并非一个每轮平均3分的合作**乌托邦**，但距离持续背叛的**反乌托邦**已经非常遥远了。

| 单词/短语 | 注释 |
|-----------|------|
| utopia of cooperation | 合作乌托邦，每个代理每轮都合作、每对都得3分——这是理论上的最优集体结果 |
| dystopia of perpetual defection | 持续背叛的反乌托邦，每对代理每轮只得1分——这是所有人都采用占优策略的悲惨世界 |
| a long way from | 远远不同于/离……很遥远，强调进化自发地使系统远离了最坏均衡 |

### 🔬 Python — 友好度与开场监测

```python
class Niceness(Instrument):
    """Fraction of 'C' choices across all genome elements."""
    def update(self, sim):
        responses = np.array([agent.values for agent in sim.agents])
        metric = np.mean(responses == 'C')
        self.metrics.append(metric)

class Opening(Instrument):
    """Fraction of agents cooperating in the first round."""
    def update(self, sim):
        responses = np.array([agent.values[0] for agent in sim.agents])
        metric = np.mean(responses == 'C')
        self.metrics.append(metric)

class Retaliating(Instrument):
    """Difference in defection probability after opponent D vs after C."""
    def update(self, sim):
        # After opponent D: elements 2, 4, 6; After opponent C: elements 1, 3, 5
        after_d = np.array([agent.values[2::2] for agent in sim.agents])
        after_c = np.array([agent.values[1::2] for agent in sim.agents])
        metric = np.mean(after_d == 'D') - np.mean(after_c == 'D')
        self.metrics.append(metric)
```

### 关键发现

| 指标 | 结果 |
|------|------|
| **平均友好度** | 从 0 → 快速升至 ~0.75，之后在 0.4~0.85 震荡，长期均值 **~0.65** |
| **首轮合作率** | 长期均值约 **0.65**，与整体友好度一致 |
| **报复性** | 在面对 D 后背叛的概率仅比面对 C 后高 ~0.1 → 弱报复信号 |

> *"This result provides **weak support** for the claim that successful strategies retaliate. But maybe it's not necessary for **all** agents, or even many, to be retaliatory; if there is at least **some** tendency toward retaliation in the population as a whole, that might be enough to prevent high-defection strategies from gaining ground."*
> 这一结果为"成功策略具有报复性"的论断提供了**弱支持**。但也许并非**所有**代理——甚至不需要很多代理——都必须具有报复性；只要群体整体上存在**一些**报复倾向，可能就足以阻止高背叛策略扩散。

| 单词/短语 | 注释 |
|-----------|------|
| weak support | 弱支持，数据中报复信号存在但不够强烈——这是一个值得注意的"适度的"结论 |
| retaliatory | 报复性的，在囚徒困境中指用背叛回应背叛的倾向 |
| gaining ground | 扩散/占据优势，进化中指某个策略在种群中所占比例持续增加 |

### 🔬 完整模拟可视化

```python
"""
Run the full PD evolution simulation and plot results.
"""
def run_pd_evolution(n_agents=100, n_steps=5000):
    np.random.seed(42)
    # Start with all defectors
    agents = [PDAgent(list('DDDDDDD')) for _ in range(n_agents)]
    tour = PDTournament()
    sim = PDSimulation(tour, agents)

    niceness_inst = Niceness()
    opening_inst = Opening()
    fitness_inst = MeanFitness()
    sim.instruments = [niceness_inst, opening_inst, fitness_inst]

    # Track fitness (we compute it separately)
    fitness_history = []
    for _ in range(n_steps):
        sim.step()
        fitness_history.append(np.mean([a.fitness for a in sim.agents]))

    fig, axes = plt.subplots(1, 3, figsize=(15, 4))
    axes[0].plot(fitness_history, alpha=0.7)
    axes[0].axhline(y=3, color='g', linestyle='--', label='Utopia (3)')
    axes[0].axhline(y=1, color='r', linestyle='--', label='Dystopia (1)')
    axes[0].set_title('Mean Fitness'); axes[0].legend()

    axes[1].plot(niceness_inst.metrics, alpha=0.7)
    axes[1].set_ylim(0, 1)
    axes[1].set_title('Niceness (fraction of C in genome)')

    axes[2].plot(opening_inst.metrics, alpha=0.7)
    axes[2].set_ylim(0, 1)
    axes[2].set_title('Opening Cooperation Rate')

    plt.tight_layout(); plt.savefig('/tmp/pd_evolution.png', dpi=100)
    print(f"Long-term mean fitness:  {np.mean(fitness_history[-2500:]):.2f}")
    print(f"Long-term mean niceness: {np.mean(niceness_inst.metrics[-2500:]):.2f}")
```

---

## 📖 12.7 结论 (Conclusions)

### Original Text

> *"Axelrod's tournaments suggest a possible resolution to the problem of altruism: maybe being **nice, but not too nice**, is adaptive. But the strategies in the original tournaments were **designed by people**, not evolution, and the distribution of strategies did not change over the course of the tournaments."*
> 阿克塞尔罗德的锦标赛为利他主义问题提供了一种可能的解决：也许**友善，但不过度友善**，是适应性的。但原始锦标赛中的策略是**由人设计**的，而非由进化产生的，并且策略的分布在锦标赛过程中并没有发生变化。

| 单词/短语 | 注释 |
|-----------|------|
| nice, but not too nice | 友善但不过度友善，这是全书最精辟的一句话——纯粹无私会被剥削，纯粹背叛会自我毁灭，适度友善才是进化稳定之道 |
| designed by people | 由人设计的，Axelrod锦标赛中的策略是人类智慧的产品，不是通过变异+选择自发产生的 |
| distribution of strategies | 策略的分布/构成，在原始锦标赛中策略集合是固定的——而进化模拟中策略的构成随每一代而变化 |

> 核心问题：*"Strategies like TFT might do well in a fixed population of human-designed strategies, but can they **evolve**? In other words, can they **appear** in a population through mutation, **compete** successfully with their ancestors, and **resist invasion** by their descendants?"*
> 像TFT这样的策略可能在固定的人类设计策略群体中表现出色，但它们能否**进化出来**？换句话说，它们能否通过突变在一个群体中**出现**，成功地与祖先**竞争**，并**抵御**后代的**入侵**？

| 单词/短语 | 注释 |
|-----------|------|
| evolve | 进化/自发出现，不同于"被设计"——关键在于策略能否从随机变异中自然涌现 |
| appear through mutation | 通过突变出现，进化论的核心：新性状不是被创造的，而是随机变异后经受选择考验 |
| resist invasion | 抵御入侵，进化稳定策略(ESS)的定义性特征——一旦建立，不能被任何突变体取代 |

### 模拟揭示的关键结论

| 发现 | 含义 |
|------|------|
| 背叛者群体**易被**友好策略入侵 | 全是背叛者 → 收益极低 → 友好突变体有优势 |
| 过度友好的群体**易被**背叛者入侵 | 全是合作者 → 背叛者获得巨大短期优势 |
| 友好度**震荡**，但长期均值高 | 动态平衡，而非静态最优 |
| TFT **不是**进化中的特殊最优策略 | 不存在稳定的最优策略 |
| 一定程度的报复是适应性的 | 不需要所有代理都报复——群体层面的报复倾向足矣 |

> *"The simulations in this chapter suggest: Populations of defectors are **vulnerable** to invasion by nicer strategies. Populations that are too nice are **vulnerable** to invasion by defectors. As a result, the average level of niceness **oscillates**, but the average amount of niceness is generally high, and the average level of fitness is generally closer to a **utopia of cooperation** than to a **dystopia of defection**."*
> 本章的模拟表明：背叛者群体**容易被**更友善的策略入侵。过度友善的群体**容易被**背叛者入侵。结果，友好度的平均水平**震荡**，但平均友善程度普遍较高，而平均适应度水平通常更接近一个**合作乌托邦**而非**背叛的反乌托邦**。

| 单词/短语 | 注释 |
|-----------|------|
| vulnerable to invasion | 容易被入侵的，进化动力学中指一种策略构成无法抵抗另一种策略的扩散 |
| oscillates | 震荡，系统不会收敛到固定点——合作与背叛的比例持续波动，形成永不停息的动态平衡 |
| utopia of cooperation | 合作乌托邦，见前文注释——理论上限3分/轮，模拟实际达到约2.5分/轮 |

### 最终洞见：自私的基因，利他的大脑

> *"Maybe our inclinations toward cooperation, retaliation, and forgiveness are **innate**, at least in part. These characteristics are a result of how our **brains are wired**, which is controlled by our **genes**, at least in part. And maybe our genes build our brains that way because over the history of human evolution, genes for less altruistic brains were **less likely to propagate**."*
> 也许我们合作、报复和宽恕的倾向是**先天的**，至少在某种程度上。这些特征是我们的**大脑连接方式**的结果，而这又受**基因**控制——至少在某种程度上。也许我们的基因以这种方式构建我们的大脑，是因为在人类进化史上，那些构建了较少利他大脑的基因**更不易传播**。

| 单词/短语 | 注释 |
|-----------|------|
| innate | 先天的/与生俱来的，即由基因而非文化教养决定的——本章的核心假说之一 |
| brains are wired | 大脑的连接方式/神经回路，基因通过控制神经发育来塑造行为倾向 |
| less likely to propagate | 更不易传播/扩散，即携带"自私大脑"基因的个体后代更少——因为他们的群体被背叛者拖入低收益均衡 |

> 🎯 ***"Maybe that's why selfish genes build altruistic brains."***
> 🎯 ***"也许这就是为什么自私的基因建造了利他的大脑。"***

| 单词/短语 | 注释 |
|-----------|------|
| selfish genes | 自私的基因，道金斯的概念——基因"想要"最大化自身的复制，但实现这一目标的最佳策略竟然是建造一个利他的大脑 |
| altruistic brains | 利他的大脑，能够产生合作、宽恕、正义感等亲社会行为的大脑——它们是基因自私性的涌现产物 |

### 🔬 全书终结：涌现视角下的人性

```
基因层面：自私（复制自己的最大化）
  ↓ 涌现
大脑层面：友善 + 报复 + 宽恕
  ↓ 涌现
群体层面：合作震荡于乌托邦与反乌托邦之间
  ↓
结论：人性不是固定的"善"或"恶"
     而是由简单进化机制涌现的动态平衡
```

---

## 📖 12.8 练习 (Exercises)

| 练习 | 内容 |
|------|------|
| **12.1** | 探索不同参数对模拟的影响：不同初始条件、是否随机配对、对手数量、差异化生存强度、num_rounds、增加差异繁殖 |
| **12.2** | 种群从未收敛到单一最优基因型——是因为没有最优策略，还是突变率太高？降低突变率或关闭突变来区分 |
| **12.3** | 探索"反应型"策略之外的基因型——考虑包含代理**自己**过去选择历史的策略 |

### 🔬 Exercise 12.1 — 不同初始条件的对比

```python
def compare_initial_conditions(n_agents=100, n_steps=2000):
    """Compare evolution starting from different initial strategies."""
    conditions = {
        'All Defectors':  [PDAgent(list('DDDDDDD')) for _ in range(n_agents)],
        'All Cooperators': [PDAgent(list('CCCCCCC')) for _ in range(n_agents)],
        'All TFT':        [PDAgent(list('CCDCDCD')) for _ in range(n_agents)],
        'Random':         [PDAgent(np.random.choice(['C','D'],7).tolist())
                           for _ in range(n_agents)],
    }
    results = {}
    for name, agents in conditions.items():
        tour = PDTournament()
        sim = PDSimulation(tour, [a.copy() for a in agents])
        niceness = Niceness()
        sim.instruments = [niceness]
        for _ in range(n_steps):
            sim.step()
        results[name] = niceness.metrics

    fig, axes = plt.subplots(2, 2, figsize=(12, 8))
    for ax, (name, metrics) in zip(axes.flat, results.items()):
        ax.plot(metrics, alpha=0.7)
        ax.set_title(name); ax.set_ylim(0, 1)
        ax.set_ylabel('Niceness')
    plt.tight_layout(); plt.savefig('/tmp/pd_initial_conditions.png', dpi=100)
```

### 🔬 Exercise 12.2 — 关闭突变测试收敛

```python
def test_convergence_without_mutation():
    """Run with mutation, then turn it off to see if population converges."""
    n_agents, n_steps = 100, 3000
    np.random.seed(42)

    agents = [PDAgent(np.random.choice(['C','D'],7).tolist())
              for _ in range(n_agents)]
    tour = PDTournament()
    sim = PDSimulation(tour, agents)
    niceness = Niceness()
    sim.instruments = [niceness]

    # Phase 1: evolve with mutation (2000 steps)
    for _ in range(2000):
        sim.step()

    # Phase 2: turn off mutation
    for agent in sim.agents:
        agent.copy = lambda: PDAgent(agent.values, agent.fitness)

    for _ in range(1000):
        sim.step()

    # Check diversity at end
    unique_genotypes = set(''.join(a.values) for a in sim.agents)
    print(f"Unique genotypes remaining: {len(unique_genotypes)}")
    for g in unique_genotypes:
        count = sum(1 for a in sim.agents if ''.join(a.values) == g)
        print(f"  {g}: {count} agents")

    plt.plot(niceness.metrics)
    plt.axvline(x=2000, color='r', linestyle='--', label='Mutation OFF')
    plt.legend(); plt.savefig('/tmp/pd_no_mutation.png', dpi=100)
```

---

## 📚 全书主题贯穿

本章完美总结了贯穿 Think Complexity 2 的所有核心主题：

| 主题 | 第12章体现 |
|------|----------|
| **涌现** | 简单策略 × 进化压力 → 复杂的合作动态 |
| **简单规则 → 复杂行为** | TFT 只需记住上一轮 → 整个群体呈现震荡平衡 |
| **个体行为 ≠ 群体结果** | 自私基因 → 利他大脑 |
| **抽象模型的力量** | Prisoner's Dilemma + 进化 = 对人性本质的深刻洞察 |
| **计算等价性** | 任何包含复制+变异+选择的信息处理系统都会进化 |

---

## 🎯 要点总结

1. **囚徒困境**中，单次博弈的理性选择是背叛——但人类实验中合作率远高于预测
2. **迭代囚徒困境**改变了博弈结构：历史让合作成为可能
3. **TFT**（以牙还牙）集友善、报复、宽恕、不嫉妒于一身，在 Axelrod 锦标赛中表现优异
4. **进化的力量**：从全背叛者出发 → 突变 → 友好策略入侵 → 震荡平衡于合作与背叛之间
5. 不存在**单一最优策略**——系统的多样性本身就是稳定性的来源
6. **自私的基因建造利他的大脑**：基因层面的竞争涌现出个体层面的合作倾向
7. 这是复杂度科学的终极启示：**简单规则 + 自然选择 → 人性中最好的部分可以自然涌现**

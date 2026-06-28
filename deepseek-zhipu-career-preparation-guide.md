# DeepSeek / 智谱 AI 入职准备完全指南

> 背景：美团 6 年广告后端 + 阿里 6 年推荐系统/导购平台，40 岁，目标进入 LLM 头部公司。
> 准备工作量：6-12 个月系统学习，每周 20-25 小时。

---

## 一、目标公司深度拆解

### DeepSeek（深度求索）

**本质定位**：以极致工程效率著称的 AGI 研究型公司。核心工作是「造 LLM」，而不是「用 LLM」。

**核心技术方向**：
1. **预训练 Infra** — 大规模分布式训练（数千 GPU），自研训练框架 HAI-LLM，MoE 架构的多机多卡调度
2. **模型架构创新** — MLA（Multi-head Latent Attention）、DeepSeekMoE、FP8 混合精度训练
3. **推理优化** — 自研推理引擎，针对 MoE 模型的低延迟高吞吐 serving
4. **RL/对齐** — GRPO（Group Relative Policy Optimization），从 RL 角度做 reasoning post-training
5. **数据工程** — 大规模数据处理 pipeline，数据去重/清洗/配比

**招人特点**：
- 极其看重底层硬功夫：C++/CUDA、分布式系统、GPU 编程、性能优化
- 研究岗要求顶会论文（NeurIPS/ICML/ICLR/ACL）；工程岗不要求论文但要求深度的系统能力
- 团队极精简（约 150 人左右），每个人要能独立 cover 一大块
- 文化是「反 KPI」，但极度的技术导向和自驱

### 智谱 AI（Zhipu）

**本质定位**：清华系出身，产研并重。GLM 系列模型 + 企业级 API 平台 + 行业解决方案。

**核心技术方向**：
1. **GLM 预训练和后训练** — ChatGLM/GLM-4 系列
2. **多模态** — CogView（文生图）、CogVideo、GLM-4V
3. **Agent 框架** — AutoGLM、工具调用、代码解释器
4. **企业级平台** — MaaS 推理服务、模型微调平台、RAG 管线
5. **垂直行业落地** — 金融、法律、教育等行业大模型

**招人特点**：
- 比 DeepSeek 更多样化：研究岗、工程岗、产品岗、解决方案岗都有
- 工程岗看重大规模系统经验（你的优势区域）
- 对行业落地经验看重（你的广告/推荐背景可包装）
- 团队规模大得多（千人级别），组织更接近传统互联网公司

---

## 二、优势与差距分析

### 你的核心资产

| 经验领域 | 如何映射到 LLM 公司 |
|---------|-------------------|
| 广告后端（高并发、低延迟） | 推理 serving 系统的极致性能优化 |
| 推荐系统（召回/排序） | 与 RLHF reward model、PPO/DPO 的训练流程高度同构 |
| 大规模分布式系统 | 分布式训练框架、参数服务器 → FSDP/DeepSpeed |
| 6 年美团 + 6 年阿里 | 大厂工程规范、稳定性意识、跨团队协作 |
| 用户导购平台 | 对话系统、Agent 的用户交互设计有直觉 |
| 召回/粗排/精排 | MoE routing、检索增强生成（RAG）的检索模块 |

### 核心差距

| 缺失能力 | 严重程度 | 说明 |
|---------|---------|------|
| CUDA / GPU 编程 | ★★★★★ | 最大短板。DeepSeek 面试会直接问怎么写 CUDA kernel |
| 深度学习训练框架 | ★★★★★ | PyTorch 分布式、DeepSpeed/FSDP/Megatron 的生疏程度 |
| Transformer 架构深度理解 | ★★★★ | 不是"用过 BERT"，而是手推注意力机制梯度、理解 KV cache |
| 大模型后训练（RLHF/DPO） | ★★★★ | 你的推荐排序经验可迁移，但 RL 语言建模的细节完全不同 |
| 推理优化技术链 | ★★★★ | continuous batching, quantization (AWQ/GPTQ/FP8), speculative decoding |
| 顶会论文/开源贡献 | ★★★ | DeepSeek 研究岗需要；工程岗可不要求但加分巨大 |
| MLSys 工程经验 | ★★★ | 与互联网后端思维差异：关注 GPU 利用率而非 QPS |

---

## 三、12 个月准备路线图

### 阶段一：基础补齐（第 1-3 个月）

#### 1.1 CUDA / GPU 编程（必须死磕）

**学习路径**：
- 书籍：《CUDA C++ Programming Guide》（NVIDIA 官方，免费）+《Programming Massively Parallel Processors》(Kirk & Hwu)
- 实战项目（按顺序完成）：
  1. 写一个向量加法的 CUDA kernel → 理解 grid/block/thread 层级
  2. 写一个矩阵乘法 kernel → shared memory tiling、bank conflict 优化
  3. 写一个 Flash Attention 的简化版 → 理解 online softmax + tiling
  4. 写一个 layer norm 的 fused kernel → 理解 kernel fusion
  5. 用 CUDA 实现一个最简 GPT-2 推理 — 能跑起来就算过关

**检验标准**：能解释清楚 `__global__` vs `__device__`、warp divergence、occupancy、shared memory vs global memory 延迟差异。

#### 1.2 深度学习系统基础

- 从头用 PyTorch 实现一个 GPT-2（约 500 行代码），包括：
  - Causal self-attention
  - KV cache 的实现
  - Gradient checkpointing
  - Mixed precision training (AMP)
- 阅读并运行 Karpathy 的 [nanoGPT](https://github.com/karpathy/nanoGPT) 和 [llm.c](https://github.com/karpathy/llm.c)
- 阅读 [minGPT](https://github.com/karpathy/minGPT) 的每一行代码

**检验标准**：能从零写出 Multi-Head Attention 的 forward + backward，手动推导梯度。

#### 1.3 分布式训练上手

- 用 PyTorch DDP 在 2 张 GPU 上训练一个模型
- 阅读 DeepSpeed ZeRO 论文的三阶段（ZeRO-1/2/3）
- 阅读 Megatron-LM 的张量并行 + 流水线并行论文
- 实际跑通一个 DeepSpeed ZeRO-3 的训练脚本
- 理解 FSDP 和 DeepSpeed 的异同

**检验标准**：能画图解释数据并行、张量并行、流水线并行的区别，以及通信开销的数学公式。

---

### 阶段二：LLM 专项深入（第 4-6 个月）

#### 2.1 必读论文清单（按优先级）

| 序号 | 论文 | 为什么重要 |
|------|------|-----------|
| 1 | Attention Is All You Need | 一切的基础 |
| 2 | GPT-3: Language Models are Few-Shot Learners | 理解 scaling 的本质 |
| 3 | Training Compute-Optimal Large Language Models (Chinchilla) | 理解数据/参数配比 |
| 4 | FlashAttention 1/2/3 | DeepSeek 面试高频题 |
| 5 | LLaMA 1/2 技术报告 | 工业界预训练的标准做法 |
| 6 | Direct Preference Optimization (DPO) | 对齐的核心方法 |
| 7 | Proximal Policy Optimization (PPO) + RLHF 原始论文 | 你推荐系统背景的最佳切入角度 |
| 8 | DeepSeek-V2/V3 技术报告（必读！） | 目标公司的核心技术 |
| 9 | DeepSeek-R1 论文（必读！） | GRPO 算法、reasoning 训练 |
| 10 | Mistral 7B / Mixtral 8x7B 论文 | MoE 架构入门 |
| 11 | vLLM: Easy, Fast, and Cheap LLM Serving | 推理引擎设计 |
| 12 | SGLang: Efficient Execution of Structured Language Programs | 最新推理优化 |
| 13 | GLM-4 技术报告 | 了解智谱的技术路线 |

**每篇论文的读法**：
1. 第一遍：理解核心 idea 和 motivation
2. 第二遍：推导关键公式，不看原文自己写出来
3. 第三遍：思考「如果我来实现这篇论文，架构怎么设计」

#### 2.2 关键开源项目深入阅读

| 项目 | 重点看什么 |
|------|-----------|
| vLLM | PagedAttention 内存管理、continuous batching 调度 |
| SGLang | RadixAttention、structured output 处理 |
| DeepSpeed | ZeRO 的 state 分片逻辑、通信优化 |
| llama.cpp | 量化实现（Q4_0/Q4_K/Q8_0 的细节） |
| unsloth | LoRA 的 Triton kernel 优化 |
| HAI-LLM（如开源） | DeepSeek 的训练框架 |

#### 2.3 亲手做的项目（极其重要！）

**推荐项目 1：从零实现一个 LLM 推理引擎**
- 支持 HuggingFace 格式的模型权重加载
- 实现 KV cache
- 实现 continuous batching
- 实现 Flash Attention（调用库或自己写简化版）
- 用 CUDA graphs 优化
- 目标：在单卡 A100 上跑 7B 模型，达到 50+ tokens/s

**推荐项目 2：实现一个 RLHF 训练管线**
- 用 TRL（Transformer Reinforcement Learning）库
- 训练一个 reward model（用 Anthropic HH 数据集）
- 用 PPO 或 DPO 对齐一个小模型（1B-3B 参数）
- 完整的 evaluation 流程

**推荐项目 3：MoE 模型的工程实现**
- 实现一个简化版 MoE transformer
- 实现 expert parallelism
- 实现 load balancing loss
- 理解 DeepSeekMoE 的 shared expert + routed expert 设计

这些项目放 GitHub 上，写详细的 README + 技术博客。

---

### 阶段三：面试专项准备（第 7-9 个月）

#### 3.1 DeepSeek 可能的面试题

**系统设计**（大概率重点考）：
- 「设计一个支持 1000 QPS 的 LLM 推理系统」
- 「设计一个支持千卡训练的分布式训练平台」
- 「设计一个 MoE 模型的 serving 方案」
- 「如何设计 KV cache 的显存管理，减少碎片？」

**算法/编码**：
- LeetCode Hard 级别：DP、图论、并查集、线段树
- CUDA/C++ 的高性能编程题
- PyTorch 算子实现（比如手写 Multi-Head Attention 并优化）

**专业深度**：
- 「DeepSeek-V3 的 MoE 架构中，为什么每个 token 激活 8 个 expert？」
- 「GRPO 和 PPO 的核心区别是什么？」
- 「MLA 和标准 MHA 在显存和计算量上的差异，推导出来」
- 「FP8 训练中 loss scaling 的必要性和原理」

#### 3.2 智谱 AI 可能的面试题

- 「设计一个多租户的模型微调平台」
- 「RAG 系统中，如何优化检索召回率？」
- 「你如何设计一个模型 A/B 实验平台？」
- 「Agent 框架中 tool calling 的延迟优化」
- 「如何处理长上下文的 KV cache，百万 token 场景」

#### 3.3 推荐系统经验的「翻译」

| 你的说法 | 面试官听到的 |
|---------|------------|
| 多路召回 | 熟悉 embedding-based retrieval，可做 RAG + 向量数据库 |
| 精排模型 | 深入理解 ranking loss，可参与 reward model 训练 |
| 广告出价/竞价 | 理解 RL 的 reward 设计和 credit assignment 问题 |
| 特征工程 | 理解数据配比、去重、质量过滤的重要性 |
| 1000+ QPS 系统 | 能 handle 推理 serving 的高并发场景 |
| A/B 实验平台 | 有 evaluation 和 metrics 设计的直觉 |

---

### 阶段四：投递策略与人脉（第 10-12 个月）

#### 4.1 渠道优先级

1. **内推**（成功率最高）→ 通过知乎、Twitter/X、即刻、LinkedIn 找 DeepSeek/智谱工程师
2. **开源贡献**（最有效的敲门砖）→ 给 vLLM/SGLang/llama.cpp/DeepSeek 开源项目提 PR
3. **技术博客 / 技术分享** → 把阶段二的项目写成深度技术博客发知乎/公众号/掘金
4. **猎头** → 作为辅助渠道

#### 4.2 关于 40 岁的处理

**不需要回避**。你投的不是「基础算法研究员」，而是「训练平台 / 推理引擎 / 系统架构」方向——经验是正向资产。LLM 推理 serving 系统的工程复杂度远超互联网后端，12 年分布式系统经验是稀缺资源。

**面试话术参考**：
> 「我知道我缺的是 LLM 领域的专项知识，所以过去一年我系统地补了 CUDA、分布式训练、推理优化，做了三个完整的项目。但我在大厂 12 年积累的分布式系统经验、稳定性意识、工程方法论，在这些项目中被验证是直接可迁移的。」

#### 4.3 目标岗位定位

**DeepSeek**：
- 训练平台工程师（Training Infra Engineer）← 最匹配
- 推理引擎工程师（Inference Engineer）← 第二匹配
- 数据平台工程师（Data Infra）← 保底选择

**智谱 AI**：
- 大模型系统工程师（MaaS/平台方向）← 最匹配
- 推理优化工程师
- Agent 框架后端工程师
- 行业解决方案架构师（你的阿里导购经验）

---

## 四、每周学习计划参考

| 时间段 | 内容 | 时长 |
|-------|------|------|
| 周一/三/五晚上 | CUDA / GPU 编程 + 论文精读 | 2h/天 |
| 周二/四晚上 | 动手项目（阶段性推进） | 2h/天 |
| 周六全天 | 深度学习 + 分布式系统 + 开源代码阅读 | 6-8h |
| 周日上午 | LeetCode 刷题（Hard 为主） | 2h |
| 周日下午 | 技术博客写作 / 开源贡献 | 2h |

**每周总计：约 20-25 小时**

---

## 五、关键提醒

1. **现在就开始写代码**，不要一直在「准备准备」。今晚就把 nanoGPT 跑起来。
2. **DeepSeek-V3 和 R1 的技术报告**是你最重要的「目标公司说明书」，逐字逐句读 3 遍以上。
3. **你的 12 年经验不是包袱**——训练平台需要懂分布式系统的人，推理引擎需要懂高并发的人，数据工程需要懂大规模数据处理的人。这些恰好都是你。
4. 如果时间紧迫（比如 3 个月内就要投），优先搞定：**CUDA 基础 + Flash Attention 原理 + vLLM 源码阅读 + DeepSeek 论文精读**。

---

## 附录：核心资源链接

### 论文
- DeepSeek-V3: https://arxiv.org/abs/2412.19437
- DeepSeek-R1: https://arxiv.org/abs/2501.12948
- FlashAttention: https://arxiv.org/abs/2205.14135
- vLLM: https://arxiv.org/abs/2309.06180
- DPO: https://arxiv.org/abs/2305.18290

### 开源项目
- nanoGPT: https://github.com/karpathy/nanoGPT
- llm.c: https://github.com/karpathy/llm.c
- vLLM: https://github.com/vllm-project/vllm
- SGLang: https://github.com/sgl-project/sglang
- DeepSpeed: https://github.com/microsoft/DeepSpeed
- llama.cpp: https://github.com/ggerganov/llama.cpp
- TRL: https://github.com/huggingface/trl

### 书籍
- CUDA C++ Programming Guide: https://docs.nvidia.com/cuda/cuda-c-programming-guide/
- Programming Massively Parallel Processors (Kirk & Hwu)
- Build a Large Language Model (From Scratch) — Sebastian Raschka

---

> 最后更新：2026 年 6 月
> 作者注：这份指南会随着你的学习进展持续迭代。保持饥饿，保持专注。

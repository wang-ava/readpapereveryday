# SCOPE-Router: Cost-Aware Open-Set VLM Routing for Execution-Oriented Tasks

Spotlight：论文把模型路由问题从“选最准”扩展到“在可接受成本内选对模型”，并对 open-set 场景做了专门 benchmark。对执行导向任务（代码、智能体、搜索）非常关键，因为真实调用既要质量也要预算可控。

## 论文信息
- 论文标题：SCOPE-Router: Cost-Aware Open-Set VLM Routing for Execution-Oriented Tasks
- 作者（机构）：Tao Yu, Yifei Qu, Zhiqing Cui, Pengfei Zhou, Zhongtian Luo, Yujia Yang, Shenghua Chai, Haopeng Jin, Zhenghao Zhang, Xinming Wang, Hongzhu Yi, Wangbo Zhao, Zhenglin Wan, Yan Huang, Yeshani, Jinwen Luo, Yang You（论文页未完整公开机构）
- 发布日期：2026-08-12（v2）
- 主题标签：`#LLM` `#Agent` `#VLM` `#Routing` `#CostAware`
- 论文链接：[https://arxiv.org/abs/2608.12127v2](https://arxiv.org/abs/2608.12127v2)
- PDF 链接：[https://arxiv.org/pdf/2608.12127v2](https://arxiv.org/pdf/2608.12127v2)
- 项目/代码/数据链接（如可得）：未在 arXiv 页面公开给出（文中提及构建了 VLM-ExecRouterBench）。

## 论文内容
- 核心问题：现有模型路由方法通常只优化质量，不区分成本，也缺乏 open-set 条件下的新模型接入能力。
- 方法概要：提出 VLM-ExecRouterBench（覆盖代码、Agentic、搜索三域，11 个模型，含价格跨越约两个数量级）；提出 SCOPE-Router 双塔路由器，通过混合采样构建行为剖面；设计 CRM+RCCR 的 cost-aware 目标，将成本偏好注入 continuous relevance，从而避免多正例软归一化稀释训练信号。
- 主要贡献：
  - 为执行型任务首次搭建 open-set 路由标准基准。  
  - 在不重训前提下支持新模型加入路由池。  
  - 给出可解释的成本-质量联合路由优化目标。
- 关键实验或结果：
  - 在 3 个基准上取得最佳 Rank Score；OOD 下领先 1.84 分，双重 OOD 下领先 6.75 分。  
  - 将 CRM+RCCR 应用于 4 个路由器，Rank Score 提升 1.25–6.21 分。
- 适合关注的原因：
  - 成本控制是企业级 LLM Agent 系统部署核心约束，路由策略的可扩展性直接影响总 TCO 与稳定性。 
- 局限性或待验证点：
  - open-set 条件下的行为分布漂移仍可能导致剖面失真；文中尚未给出极端冷启动下的最小样本下界。 
  - 基准覆盖执行型任务，但对高度专有私有模型接入场景仍需额外验证。
- 对后续研究/应用的启发：
  - 可将路由问题纳入任务管理器的一体化策略，结合隐式成本预算、SLA 和风险约束。 
  - 可与工具选择、RAG 检索器选择联合训练，形成端到端成本决策链。
- Obsidian 快速浏览一句总结：**别只问“谁最强”，要问“在当前成本-时延约束下谁是最划算的执行者”。**

## 标准化研究框架
**Research question：** 在 open-set 执行场景下，如何同时最优化响应质量与花费并支持新模型增量接入？

**Literature：** 传统路由研究多集中于单任务准确率或 closed-set 假设，本工作则引入 open-set 与显式成本约束，接近生产环境。

**Theory：** 路由可视为多目标决策问题：路由器需估计 query-模型匹配度并考虑每次调用成本；多正例下若仅用 softmax 归一化会稀释信号，导致预算约束下的分配偏差。

**Hypotheses：**  
- H1：引入代价感知目标能提升 Rank Score 与稳健性。  
- H2：独立评分机制比 softmax 多正例归一化更适合 open-set 条件。  
- H3：路由器行为剖面对模型新加入时具备更好外推能力。 

**Method：** 设计 VLM-ExecRouterBench 并构建随机/诊断/多样性混合采样；训练双塔路由器并以 CRM+RCCR 优化代价加权的相关性目标。

**Data and Analysis：** 在代码、Agentic、搜索三类任务上比较多套路由器，报告 Rank Score 及 OOD/双重 OOD 场景差异，并以多模型组对评估泛化。

**Findings：** 成本感知的路由框架显著优于基线，且在多模型场景下对新模型接入更友好。

**Conclusion：** 本文为执行导向的 Agent 系统提供了可落地的路由策略范式：路由器不应只做“准则排序”，更要编码调用边际成本。

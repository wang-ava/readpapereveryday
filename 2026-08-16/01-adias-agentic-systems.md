> **Spotlight：** ADIAS 把 Agent 系统优化的核心问题转成“issue-centric 持续记忆问题”，把失败修复从一次性候选修订改成可追踪的问题状态闭环。
> 如果你关注可持续运行的 LLM agent，核心价值在于它把修复动作的上下文长期保留下来，减少反复试错。

# ADIAS: Automated Design of Interactive Agentic Systems

- **论文标题：** ADIAS: Automated Design of Interactive Agentic Systems
- **作者/机构：** Lekang Jiang, Bohan Tang, Stephan Goetz, Yiwen Guo（机构信息未在 arXiv 页面展示）
- **发布日期/版本日期：** 2026-08-03（arXiv:2608.06410v1）
- **主题标签：** #LLM #Agent #AutoAgent #ProgramSynthesis #InteractiveAI
- **论文链接：** [https://arxiv.org/abs/2608.06410](https://arxiv.org/abs/2608.06410)
- **PDF 链接：** [https://arxiv.org/pdf/2608.06410](https://arxiv.org/pdf/2608.06410)
- **项目/代码/数据链接：** arXiv 页面未在显著位置给出代码/数据/项目主页；论文附注含 23 页、7 tables、5 figures。

## 核心问题

传统 agent 自动设计方法多是“以候选 agent 为中心”，每轮修复依赖当前候选历史，导致跨轮迭代过程脆弱，难以复用修复证据，也不利于错误修复可解释追踪。

## 方法概要

ADIAS 引入 issue-centric 优化框架：持续维护结构化的问题状态（issue state），包括 issue 标识、生命周期、支持证据和历史干预结果。随后在每一轮交互优化中，用当前问题状态指导修复目标与代码改动方向，形成闭环。

## 主要贡献

1. 将 agent 全码改造问题从“候选回放”改为“问题持久化状态”，提升迭代记忆性。
2. 通过问题生命周期建模，明确“下一步修复该做什么”与“为什么这么做”。
3. 在五个交互基准上显著超越强基线，平均提升 25.2%。

## 关键实验或结果

- 论文报告 ADIAS 在五个互动 benchmark 上平均提高 25.2%。
- 对照分析显示，若移除 issue-centric 模式或改回 candidate-centric，性能可降到约 40.7% 的损失区间（论文内文）。

## 适合关注的原因

LLM 工程越来越多采用“多轮自动修复 + 回归测试 + 再测试”流程，ADIAS 给出可持久记忆的中间状态建模方式，适合将“agent 的可维护性”而非“单轮性能”作为主指标。

## 局限性或待验证点

- 论文信息未公开完整复现指引，仍需核验不同项目规模下的工程成本。
- 复杂 bug 体系中的 issue 语义划分是否稳定尚未给出更大规模验证。
- 可扩展性与多语言 agent 场景尚缺跨语言泛化评估。

## 对后续研究/应用的启发

可将 ADIAS 的 issue state 与测试追踪（如 trace IDs）、工具调用日志和安全策略结合，构建可审计的 agent repair pipeline，尤其对企业内网 Agent 和研发自动化很有启发。

## Obsidian 快速浏览总结

**一句话：ADIAS 用持久化 issue 状态替代候选历史回放，在交互 agent 设计上更像工程化的修复工作流。**

## 标准化研究框架

**Research question：** 在自动化 agent 设计中，是否能通过持久化问题状态减少跨轮修复过程中的信息丢失并提升稳定性？

**Literature：** 相关于 auto-agent、program repair、iterative optimization 与强化反馈循环，但先前多采用候选中心的短期历史重用。

**Theory：** 该框架可看作“有状态搜索”的控制问题：将问题空间建模为可更新状态，减少重复建模与状态丢失。 

**Hypotheses：** 具备持久 issue 表征可提高搜索效率，并减少修复策略的回归。

**Method：** 维护 issue 状态数据库（ID、生命周期、证据、历史效果），并在每轮优化中用状态指导新的修复决策。

**Data and Analysis：** 五个交互 benchmark + 交叉 ablation（有/无 issue state）。采用成功率与性能提升幅度比较。

**Findings：** 持久问题建模对性能有显著正向贡献，移除该机制会明显下降。

**Conclusion：** 非社会科学研究中，对应“过程可解释性与可复用记忆”是核心理论含义：该字段可理解为将 agent 迭代从无记忆强化学习转成可回放优化过程。 

# Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments

Spotlight：这篇工作很适合观察 coding agent 真实训练数据从“看起来有真实度”到“可执行可验证”之间的鸿沟如何被工程化解决。

- 论文标题：Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments
- 作者：Haomin Qi, Xingliang Wang, Xuanqi Gao, Baihui Sang, Xin Zhang, Minghua Ma, Pengfei Gao, Yu Kang, Qingwei Lin, Saravan Rajmohan, Dongmei Zhang, Qi Zhang
- 机构（如可得）：arXiv 元信息未显示机构明细
- 发布时间：2026-07-30（v1）
- 主题标签：`#Agent` `#CodingAgent` `#SoftwareEngineering` `#Benchmark` `#DataConstruction`
- 论文链接：[https://arxiv.org/abs/2607.28591v1](https://arxiv.org/abs/2607.28591v1)
- PDF 链接：[https://arxiv.org/pdf/2607.28591v1](https://arxiv.org/pdf/2607.28591v1)
- 项目/代码/数据链接：摘要未提供明确公开代码/数据链接（待论文正式版本补充）

## 核心问题
现有 coding agent 数据要么语义薄弱要么难以直接执行，导致 benchmark 与真实代码维护场景存在落差，如何从真实仓库历史中稳定构造可执行任务？

## 方法概要
作者将 merged PR 作为证据来源，结合三种任务重建策略（Patch Reversal、Code Mapping、Agent Reconstruction）把历史变更映射到“健康基线状态 + 任务状态 + 恢复状态”，形成可验证任务实例。核心在于兼顾历史版本漂移与现代代码基线的可复用性。

## 主要贡献
- 提供一套可自动化的 coding agent 任务构造 pipeline，减少人工标注成本。
- 将 repository history 变成可执行任务语料，覆盖 Bug Fix、Feature Addition、Test Generation、API Migration、Security Repair。
- 给出跨任务族的构建成功率与复现一致性分析，证明方法可复用于不同任务类型。

## 关键实验或结果
- 从 1,130 个候选变更中，Change2Task 实现 79.6% verified task construction success。
- 与基于 PR 的构建基线相比，任务回收率提升 29.2%。
- 历史与重建案例在 agent 评估下可达 98.0% 结果一致性。
- 任务复用现代基线可减少整体建构开销约 10.8%。

## 适合关注的原因
当你要搭建 coding agent 的持续评测系统时，这套思路让“真实性、可执行性、可复现性”形成闭环，特别适合用于回归测试、微调样本扩展和基线对比。

## 局限性或待验证点
- 当前流程对源码清洗、项目构建环境稳定性有隐性要求，少量复杂仓库可能出现映射失败。
- 未显示开源数据仓库规模的细粒度分层标准。
- 论文摘要未公开完整超参数/失败 case 统计，迁移时需额外工程调参。

## 对后续研究/应用的启发
可把其任务生成策略与 agent evaluator 联合成持续生成-执行-回灌的流水线，推动真实软件维护任务的自举式 benchmark 演进，而非依赖静态静态数据集。

## Obsidian 快速浏览总结
一句话速看：Change2Task 把 PR 历史转译为可执行任务环境，显著提升 coding agent 训练与评测数据的真实性与可复验性。

## 标准化研究框架
- **Research question：** 如何把真实代码仓库变更转成规模化、可执行、可验证的 coding agent 任务？
- **Literature：** 关联于 software engineering 自动化、代码生成评价基准与 agent 任务重构技术，但更侧重工程化数据管道。
- **Theory：** 假设“历史变更包含足够的可执行约束信息”，只要恢复任务前后状态即可形成高可信训练样本。
- **Hypotheses：** 非标准统计假设；等价于验证“采用版本级恢复约束会提高任务可执行率与评测可复现率”。
- **Method：** 从 merged PR 提取候选变更，应用三种重建策略建构任务，再通过健康基线、任务状态、恢复状态验证生命周期。
- **Data and Analysis：** 使用 1,130 条可建构源变更评估成功率，覆盖五类任务族并统计任务回收率与执行一致性。
- **Findings：** 变更驱动数据框架能显著提高可执行样本密度与任务一致性，且降低重复构建成本。
- **Conclusion：** 该框架为 coding agent 任务生产提供工程化路径，但仍需公开更多边界条件以增强跨组织迁移性。

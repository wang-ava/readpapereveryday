# MOSAIC: The Right Modules for Each Task in Embodied Agents

MOSAIC 的关键价值在于把“一个大模型做所有事”的思路改成“任务级模块图合成”，把多模块组合能力前置到推理前，降低每个任务的无效计算和参数浪费。

## 基本信息

- 论文标题：MOSAIC: The Right Modules for Each Task in Embodied Agents
- 作者/机构（如可得）：Kevin Wang；Dweep Trivedi；Vincent Ha；Albert Jiang；Christian Ellis；Ufuk Topcu；Swarat Chaudhuri；Zhangyang Wang；1The University of Texas at Austin
- 发布日期或版本日期：2026-05-27（OpenReview 发表）；2026-06-01（Last Modified）
- 主题标签：#EmbodiedAI #LLM Agents #Modular Reasoning #VisionLanguageModel #Planning
- 论文链接：https://openreview.net/forum?id=pF9wISLUYo
- PDF 链接：https://openreview.net/pdf/eaa955d2cfb87bb486b1fac298ffb9940dc6eb63.pdf
- 项目/代码/数据链接（如可得）：
  - 代码：未见公开代码仓库链接
  - 项目页/代码：未见公开项目页链接
  - 数据：使用 EmbodiedBench、EB-Nav 子任务集进行评测（基于论文正文）

## 核心问题

如何在机器人任务中避免“固定 pipeline 一刀切”，并为每个任务按需选择、绑定、组合不同模块，使空间定位、动作执行、规划与故障处理分工更高效？

## 方法概要

论文将 embodied agent 设计为“按任务模块图合成”问题：

- 预先固定一个 typed module library（模块类型和实现保持不变）；
- 每个任务输入后，元策略基于历史 memory 与检索结果生成若干候选模块图；
- 每个候选在 rollout 上评估后更新记忆库，逐步形成长期可复用设计。

核心思想是从“全量自进化（full self-evolution）”降到“memory-条件的模块组合搜索”。

## 主要贡献

- 将 embodied agent 的核心复杂度从单次推理里“调参 + 参数更新”转向“任务级架构选择”。
- 提出 MOSAIC 记忆框架：仅演化 memory，其余组件（catalog/meta-agent/executor/model）保持固定。
- 在 EB-Nav 风格任务中显示按任务动态合成模块图能带来可观收益。

## 关键实验或结果

- 在 EmbodiedBench Navigation 的 5 类能力子集上，MOSAIC 平均成功率达到 50.0%，较同样 Qwen3-VL-8B 的默认 agent 提升 18.4 pp。
- 对比“永远激活全部模块”的消融基线，仍有 5.3 pp 提升。

## 适合关注的原因

这篇工作把 embodied 系统从“大模型参数扩张”转向“任务结构控制”，对落地工程很有现实意义：同一执行器可在不同任务间动态收敛计算路径，减少上下文和推理噪声。 

## 局限性或待验证点

- 当前验证集中在 EmbodiedBench 家族（EB-Nav）与单一部署域，跨域迁移尚未充分验证；
- 模块库与元模块策略固定，不支持快速引入新工具类；
- 训练与在线部署成本仍有差异，训练期开销约为单策略 baseline 的 9 倍（per paper），部署期才回归。

## 对后续研究/应用的启发

- 可扩展该框架为“多域模块注册表”，支持随环境变化增删模块实现在线扩展；
- 对工业部署可尝试将“模块检索质量”与任务风险等级联动，避免低置信度下的高代价组合。 

## Obsidian 快速浏览总结

一句话：MOSAIC 的价值在于把“会做一切”的单体策略，改造成“按任务装配”的可预算化 agent 架构。

## 标准化研究框架

**Research question：** 在固定执行模型下，能否通过任务条件化的模块图合成显著改善 embodied agent 的成功率与效率？

**Literature：** 现有 Embodied Agent 工作多强调统一模型规模与多模态输入，较少系统化讨论模块间组合与任务条件化；本篇把问题定位为 per-task architecture search 与 memory-driven adaptation。 

**Theory：** 这里的“理论”是经验-结构折中：通过 memory 提供任务上下文可解释地选择模块组合，本质是资源受限下的结构化策略空间约束，而非直接可被社会科学意义下假设检验。 

**Hypotheses：** 等价地可表述为：固定执行器架构下，模块图选择质量与任务匹配度显著相关于最终成功率；并且记忆驱动检索能提高模块组合泛化。 

**Method：** 提出 memory-条件化模块图合成流程：任务 -> 检索记忆 -> 元策略生成 N 个 pipeline -> K 次 rollout 评估 -> 更新记忆。实验用同一 benchmark 的多任务设置验证。 

**Data and Analysis：** 数据侧采用 EB-Nav/EmbodiedBench 子任务；分析指标包括任务成功率与不同模块组合的结构/参数多样性，比较有无 memory 的搜索质量差异。 

**Findings：** 在相关 benchmark 上 MOSAIC 显著提升成功率（+18.4 pp）并提高模块结构多样性，说明 task-conditioned module composition 有效。 

**Conclusion：** 方法对多任务 embodied deployment 有工程可行性，但跨域泛化与模块库扩展仍是下一步关键障碍。 

MOSAIC 的亮点在于它没有继续追求“一切能力都内生到一个大模型里”，而是把 embodied agent 重新定义为一个按任务动态组合工具和模块的系统设计问题。

# MOSAIC: The Right Modules for Each Task in Embodied Agents

## 基本信息

- 论文标题：MOSAIC: The Right Modules for Each Task in Embodied Agents
- 作者/机构：Kevin Wang、Dweep Trivedi、Vincent Ha、Albert Jiang、Christian Ellis、Ufuk Topcu、Swarat Chaudhuri、Zhangyang Wang；University of Texas at Austin
- 发布日期或版本日期：2026-05-27（OpenReview）；最后修改 2026-06-04
- 主题标签：#EmbodiedAI #LLMAgent #ModularSystems #Memory #Navigation
- 论文链接：https://openreview.net/forum?id=pF9wISLUYo
- PDF 链接：https://openreview.net/pdf?id=pF9wISLUYo
- 项目链接：未见独立项目页
- 代码链接：文中未见公开代码
- 数据链接：实验报告基于 EB-Nav

## 核心问题

embodied tasks 对能力组合的要求高度异质：manipulation 更依赖几何精度，long-horizon navigation 更依赖 persistent mapping，instruction following 又更依赖 multi-step planning。现有常见做法是把这些能力全塞进一个 foundation model 里，但这既昂贵又未必高效。本文要解决的是：能否让 agent 针对单个任务动态选择最合适的模块组合，而不是为整个 benchmark 固定一条流水线？

## 方法概要

作者把 embodied agent 设计形式化为 per-task module-graph synthesis，即联合决定该用哪些模块、每个节点选哪种具体工具，以及参数如何绑定到环境观测与上游输出。MOSAIC 的核心策略是保留 self-evolution 中最“承重”的部分：固定 typed module catalog、固定 meta-agent、固定模型权重，只让“历史 pipeline 设计及其结果”的 memory 随部署持续增长。每个 episode 开始时，meta-agent 基于这份 memory 检索并合成任务特定的 pipeline，执行时再由小型 executor 逐步运行。

## 主要贡献

- 把 embodied agent 从“统一大模型”思路转向“按任务合成 module graph”的系统范式。
- 提出 memory-conditioned pipeline synthesis，而不是每次从零搜索或把所有模块全部打开。
- 强调 deployment-time evolution：演化的是历史设计经验，而不是基础权重本身。
- 在相同 backbone 下证明 per-task module selection 比默认 agent 和全模块激活都更有效。

## 关键实验或结果

- 论文在 EB-Nav 上报告 MOSAIC 的平均成功率为 50.0%。
- 相比相同 Qwen3-VL-8B backbone 下的默认 EmbodiedBench agent，提升 18.4 个百分点。
- 相比“同一模块库全部激活但不做按任务选择”的 baseline，仍提升 5.3 个百分点。
- 这说明收益不只是“加更多模块”，而是“为任务配对正确模块”。

## 适合关注的原因

这篇很值得工程侧和研究侧同时关注。它的价值不在于提出一个更强单模型，而是说明 embodied system 的上限越来越受 orchestration 设计影响。对现实系统来说，这比单纯继续预训练一个更大的 agent 更接近可落地路径。

## 局限性或待验证点

- 当前公开版本是 workshop/poster 级别结果，尚需更大规模 benchmark 扩展。
- 方法高度依赖模块库质量和接口设计；如果 catalog 设计差，组合策略上限也会受限。
- 实验主要围绕 EB-Nav，是否能平移到 manipulation、mobile manipulation 或 real robot 仍待验证。
- 公开代码、项目页和更细致复现资产暂未看到。

## 对后续研究/应用的启发

后续工作可以把 embodied agent 看成“task-conditioned systems composition”问题，研究如何检索、编辑和积累 pipeline memory。应用上，这对企业机器人、复杂 GUI agent、工业巡检 agent 都很重要，因为它们天然面对异质任务，而不是单一 benchmark 模式。

## Obsidian 快速浏览总结

MOSAIC 的核心观点是：具身 agent 不一定要更大，更可能要更会按任务挑模块、记住哪些组合真的有用。

## 标准化研究框架

**Research question：** 本文研究的问题是：面对能力需求高度异质的 embodied tasks，agent 是否应按任务动态合成模块流水线，而不是固定一条通用 pipeline。

**Literature：** 相关文献涉及 embodied agents、模块化 agent 系统、tool-using LLM agents、self-evolving pipelines 与 memory-augmented reasoning。本文承接这些方向，但把重点放在 per-task module selection。

**Theory：** 本文不是社会科学理论检验，但其等价理论主张是：embodied agent 的性能瓶颈不一定在模型内部知识容量，而在是否为当前任务配置了合适的外部能力组合。

**Hypotheses：** 可等价理解为：若基于过往 pipeline 经验进行 memory-conditioned module-graph synthesis，则 agent 会优于固定默认 pipeline，以及无差别激活所有模块的做法。

**Method：** 方法上构建 MOSAIC：固定模块目录和 meta-agent，通过检索历史 pipeline 设计与结果，在每个 episode 合成任务特定的 module graph，并交给小型 executor 逐步执行。

**Data and Analysis：** 数据和分析主要基于 EB-Nav，比较 MOSAIC、默认 EmbodiedBench agent 以及全模块激活 baseline 在多能力子集上的成功率差异。

**Findings：** 主要发现是按任务选择模块能显著提升 embodied task 成功率，且优于“全开所有能力模块”的简单堆叠策略。

**Conclusion：** 结论是 embodied agent 的未来不一定是单一更大的 foundation model，也可能是一个更擅长任务级组合、检索和系统编排的 modular agent。

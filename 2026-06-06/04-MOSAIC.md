MOSAIC 的亮点在于它反对“一个大而全的具身基础模型包打天下”，转而主张按任务动态组合模块。这个思路非常适合当下具身智能的现实状态，因为导航、操作、规划、记忆并没有被单一模型同时解决。

# MOSAIC: The Right Modules for Each Task in Embodied Agents

## 基本信息

- 论文标题：MOSAIC: The Right Modules for Each Task in Embodied Agents
- 作者/机构：Kevin Wang, Dweep Trivedi, Vincent Ha, Albert Jiang, Christian Ellis, Ufuk Topcu, Swarat Chaudhuri, Zhangyang Wang；OpenReview 页面未直接展开机构署名
- 发布日期或版本日期：2026-06-01（最近修改日期；首次发布为 2026-05-27）
- 主题标签：#EmbodiedAI #Agent #VLM #Memory #Planning
- 论文链接：https://openreview.net/forum?id=pF9wISLUYo
- PDF 链接：https://openreview.net/pdf?id=pF9wISLUYo
- 项目链接：未检索到独立项目页
- 代码链接：未检索到公开仓库
- 数据链接：实验报告基于 EB-Nav 与 EmbodiedBench 相关设置，未检索到独立数据主页

## 核心问题

具身 agent 需要的能力组合并不固定：有些任务更依赖空间定位，有些更依赖长程记忆或自然语言规划。如果把所有能力硬塞进一个固定 pipeline，往往会带来冗余、误用和泛化不足。作者因此追问：具身 agent 是否应该按任务动态组合模块，而不是固定激活一整套工具链？

## 方法概要

MOSAIC 把具身 agent 设计为 per-task module-graph synthesis。系统维护一个 typed module catalog 和过去任务设计记忆，在每个 episode 开始时，由一个冻结的 frontier meta-agent 基于历史检索结果组装出任务特定的模块图；随后由轻量 executor 在每一步执行该图。

## 主要贡献

- 把 embodied agent 设计表述为面向每个任务的模块图合成问题。
- 用 memory-conditioned 的方式保留过去设计经验，而不是每次从零搜索。
- 将“全量自进化搜索”简化为更可行的 meta-agent 组合过程。
- 显示按任务定制模块组合优于固定全开或固定单 pipeline。

## 关键实验或结果

- OpenReview 页面给出的核心结果是：在 EB-Nav 上，MOSAIC 取得 50.0% 平均成功率。
- 相比同样基于 Qwen3-VL-8B backbone 的默认 EmbodiedBench agent，提升 18.4 个百分点。
- 相比“把同一模块库全部激活但不做任务选择”的 baseline，也提升 5.3 个百分点。

## 适合关注的原因

这篇论文代表了具身智能一个很务实的方向：先别幻想单模型吃掉所有能力，而是把系统做成可组合、可检索、可记忆的模块网络。对做 embodied benchmark、VLM planner、robot runtime 的人来说，这条路线更贴近短中期落地。

## 局限性或待验证点

- 当前验证主要在特定 benchmark 和模块库设定中完成，真实机器人系统中的噪声与执行误差可能更复杂。
- 如果模块库本身覆盖不足，meta-agent 再聪明也只能在有限候选里组合。
- 任务间共享的记忆设计如何避免陈旧经验污染新任务，仍是一个开放问题。

## 对后续研究/应用的启发

后续可以把 MOSAIC 式设计推广到“agent runtime marketplace”：不同能力模块以统一接口暴露，由 planner 根据任务动态编排。对机器人应用来说，这比单体大模型更容易调试、替换和评估。

## Obsidian 快速浏览总结

MOSAIC 提醒我们，具身 agent 不一定要更大，很多时候更重要的是按任务把合适模块拼对。

## 标准化研究框架

**Research question：** 具身 agent 能否通过按任务动态合成模块图，而不是使用固定单一 pipeline，获得更高的任务成功率？

**Literature：** 相关文献涉及 embodied AI、vision-language-action、模块化 agent、memory-augmented reasoning 与 tool composition。多数既有路线更偏向统一模型或固定管线。

**Theory：** 本文的等价理论是：具身任务的能力需求异质性很高，统一固定 pipeline 会引入无关模块和错误归因，因此任务条件化的模块组合比一刀切更有效。

**Hypotheses：** 本文不是传统假设检验论文，但可等价为：按任务选择模块优于默认固定 agent；基于历史记忆的组合优于每次随机或全量激活；轻量 executor 足以承接 episode 内执行。

**Method：** 构建 typed module catalog、历史设计记忆、frontier meta-agent 与 step-level executor，并在每个任务开始时合成模块图。

**Data and Analysis：** 在 EB-Nav 等 embodied benchmark 设置下比较默认 agent、全量激活 baseline 与 MOSAIC 的平均成功率。

**Findings：** MOSAIC 在核心 benchmark 上达到 50.0% 平均成功率，较默认 agent 提升 18.4 个百分点，显示按任务组合模块的收益显著。

**Conclusion：** 具身智能的一个有效方向不是继续堆统一大模型，而是发展可检索、可组合、带记忆的模块化 agent runtime。

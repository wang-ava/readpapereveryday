# MOSAIC: The Right Modules for Each Task in Embodied Agents

MOSAIC 给出一种“按任务动态组装模块”的具身智能范式：不是把所有能力塞进一个巨型模型，而是让固定模型 + 可进化记忆库决定每次任务该用哪些模块。

- **论文标题**：MOSAIC: The Right Modules for Each Task in Embodied Agents
- **作者/机构**：Kevin Wang, Dweep Trivedi, Vincent Ha, Albert Jiang, Christian Ellis, Ufuk Topcu, Swarat Chaudhuri, Zhangyang Wang（论文主页未完整披露统一机构信息）
- **发布日期/版本日期**：2026-06-04（Published: 27 May 2026, Last Modified: 04 Jun 2026, FMEA @ CVPR 2026）
- **主题标签**：#EmbodiedAI #LLMAgents #VisionLanguageModel #ModularArchitectures #Memory
- **论文链接**：<https://openreview.net/forum?id=pF9wISLUYo>
- **PDF 链接**：<https://openreview.net/pdf?id=pF9wISLUYo>
- **项目/代码/数据链接（如可得）**：公开条目未提供项目/代码/数据链接。
- **核心问题**：单一固定 pipeline 无法兼顾具身任务的多模态复杂性；任务间需求差异会导致“模块错配”与资源浪费。
- **方法概要**：
  1. 将具身智能建模为模块图搜索问题：选择模块类型、参数配置和执行绑定。
  2. 前端模型与模块库权重保持固定，仅在执行期维护“任务记忆”与模块激活策略。
  3. 一个冻结的元智能体（frontier meta-agent）按记忆检索召回历史成功方案并生成当前任务的模块图。
  4. 小型执行器按步调度上述模块图进行决策。
- **主要贡献**：
  1. 把“任务分化”转化为“模块组合问题”；
  2. 提出 memory-conditioned 的 per-task module composition 框架；
  3. 在保持训练成本低的前提下提升跨任务迁移。
- **关键实验或结果**：在 EB-Nav 上，MOSAIC 平均成功率 50.0%，较默认 EmbodiedBench baseline（Qwen3-VL-8B）提升约 18.4%，并优于无选择基线 +5.3%。
- **适合关注的原因**：
  1. 适合需要多任务切换的机器人与数字代理系统；
  2. 解决“全量拼接一把梭”导致的效率与稳定性问题；
  3. 与 agentic 流程天然兼容，未来可直接用于工具链编排。
- **局限性或待验证点**：
  1. 模块搜索质量依赖记忆库质量；
  2. 长时任务下记忆遗忘和更新策略仍需更严格验证；
  3. 真实物理机器人的仿真到现实迁移实验仍不足。
- **对后续研究/应用的启发**：可视作“具身系统架构”而非“模型架构”的替代路线：先做模块治理与记忆检索，再做参数扩张。
- **Obsidian 快速浏览一句总结**：MOSAIC 的核心优势在于“按任务选模块”，对长链条多技能具身任务比单一端到端模型更友好。

## 标准化研究框架
- **Research question：** 如何通过固定基座与可学习模块图选择，在不频繁更新模型参数的情况下提升具身任务适配性？
- **Literature：** 对接 VLM、VLA、记忆增强控制与模块化神经控制器研究，强调架构工程优化而非模型规模竞赛。
- **Theory：** 采用“模块稀疏化 + 历史记忆检索”降低任务不匹配带来的噪声，提升每步决策的条件化匹配度。
- **Hypotheses：** 固定模块库 + 任务记忆的组合在多任务具身环境中会显著提高成功率并减少负迁移。
- **Method：** 在统一 baseline 与全量模块 baseline 上做对照；比较模块图搜索策略和任务成功率。
- **Data and Analysis：** 以 EB-Nav 为代表任务，统计成功率、策略切换次数、模块激活稳定性等指标。
- **Findings：** 任务记忆驱动的模块化策略在样本效率与迁移上优于固定流水线。
- **Conclusion：** MOSAIC 提供了从“单模型思路”到“任务图谱思路”的可行替代方向。

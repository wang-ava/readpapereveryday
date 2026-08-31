# CLAP: Cross-Embodiment Video World Models are Zero-Shot Physical Simulators

> Spotlight（2 句）：CLAP 试图解决 VWM 在单一形态上过拟合的问题，把“动作条件”从具体机器人约束中解耦。它的关键价值在于让模型学到跨形态的物理先验，并在零样本下迁移到新机器人。  

## 基本信息
- 论文标题：CLAP: Cross-Embodiment Video World Models are Zero-Shot Physical Simulators
- 作者：Kechen Liu, Ola Shorinwa（机构未在 arXiv 页面完整披露）
- 发布日期（版本）：2026-08-27（v1）
- 主题标签：`#EmbodiedAI` `#VideoWorldModel` `#CrossEmbodiment` `#Sim2Real` `#ZeroShot` `#Robotics`
- 论文链接：[https://arxiv.org/abs/2608.27406](https://arxiv.org/abs/2608.27406)
- PDF 链接：[https://arxiv.org/pdf/2608.27406v1.pdf](https://arxiv.org/pdf/2608.27406v1.pdf)
- 项目/代码/数据链接：
  - Project Page: [https://omni-clap.github.io](https://omni-clap.github.io)
  - Code/Model: 论文描述为“open-source models and code”，建议优先从项目页获取最新仓库链接
  - 数据：未在首页直接给出统一下载入口

## 核心问题
现有动作条件视频世界模型通常固定在单一机器人形态，无法充分利用包含人类与多平台行为的视频数据。如何在动作表达异构时，仍让同一模型学会可迁移的物理动态规律，是具身模型泛化的关键难题。  

## 方法概要
1. 提出统一动作条件表示：用 end-effector pose、language instructions 与 latent action 进行桥接。  
2. 引入 curriculum 学习：先在大量未标注视频上学习通用物理先验（latent action 阶段），再在少量可执行动作映射上对齐具体形态。  
3. 通过零样本迁移测试（含 DROID、Bridge、YAM、G1 Humanoid 等）验证跨形态泛化。  
4. 使用 few-shot 适配进一步评估快速收敛能力。  

## 主要贡献
- 将“动作条件空间异构”作为核心挑战建模并提出统一处理方案。  
- 在训练阶段最大化跨域视频利用率，显著提升数据利用效率。  
- 给出跨形态动作世界模型的第一类系统级 baseline，覆盖多平台执行器。  

## 关键实验或结果
- 在挑战环境中，CLAP 在多数任务上达到或超过单形态 SOTA。  
- 通过 few-shot 适配可进一步提升性能，形成“先通用预训练再形态对齐”的有效流程。  
- 提供多形态验证，支持跨机器人直接零样本推理，具备较高迁移潜力。  

## 适合关注的原因
- 这是具身 AI 从“单机模型”向“统一物理先验模型”的关键迈进。  
- 对多机器人研发团队意义明显：统一训练—形态适配路线可降低模型工程复杂度。  
- 若持续开源代码和权重，可能成为模拟器与真实机器人之间的桥接底座。  

## 局限性或待验证点
- 形态映射环节仍可能依赖较强先验，复杂非刚体或软体系统上泛化不确定。  
- 真实硬件部署开销（时延、算力）和安全边界在文中仍未全面量化。  
- 项目细节（日志、脚本、超参）若依赖外部主页更新，当前版本可复现性需要跟进。  

## 后续研究/应用启发
- 可在工业与仓储场景先做“形态轻量对齐”，用同一世界模型同时服务差异化硬件。  
- 与控制器设计结合时，可把 CLAP 作为物理先验约束器，提高规划器 sample efficiency。  
- 长期可拓展为“形态目录”式模型中心化部署，动态加载新机器人的动作映射层。  

## 适合 Obsidian 快速浏览的中文总结
一句话：CLAP 不再为每个机器人单独训练世界模型，而是学习共享物理语义，让多形态执行更容易零样本迁移。  

## 标准化研究框架
- **Research question：** 在动作表示与训练策略层面进行解耦后，video world model 是否能够跨机器人形态实现零样本物理模拟与控制迁移？  
- **Literature：** 对接 world model 与 sim2real 研究线，但跳出单形态假设，强调跨人类/机器人视频融合。  
- **Theory：** 假设低级动作可通过统一表征映射到共享物理动力学潜变量，从而支持跨形态快速泛化。  
- **Hypotheses：** ①通用阶段学习可建立形态无关先验；②形态对齐阶段可显著缩短跨平台适配；③少量适配即可获得可用控制性能。  
- **Method：** 先进行 latent action 的大规模无标注视频训练，再在目标形态上进行动作空间映射与 few-shot 适配。  
- **Data and Analysis：** 比较单形态 baseline 与跨形态 zero-shot/few-shot 的任务成功率与泛化表现。  
- **Findings：** CLAP 在多平台任务上展现迁移优势，支持“跨形态共享物理先验”假设。  
- **Conclusion：** 对具身 AI 的统一建模方向有启发，但真实部署仍需更完整的算力、安全与复现实验披露。  


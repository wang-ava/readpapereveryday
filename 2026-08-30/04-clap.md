# CLAP: Cross-Embodiment Video World Models are Zero-Shot Physical Simulators

> Spotlight（2句）：CLAP 试图把“动作空间差异”从跨形态研究的瓶颈解开，让 video world model 训练时不再被单一机器人限制。它把跨人类与跨机器人数据融合进同一学习框架，给物理模拟式规划带来更强泛化潜力。

## 基本信息
- 论文标题：CLAP: Cross-Embodiment Video World Models are Zero-Shot Physical Simulators
- 作者：Kechen Liu, Ola Shorinwa（机构未在 arXiv 摘要页完整披露）
- 发布日期（版本）：2026-08-27（v1）
- 主题标签：`#Embodied` `#World Model` `#Action-Conditioned Video` `#Cross-Embodiment` `#Physical Reasoning`
- 论文链接：[https://arxiv.org/abs/2608.27406](https://arxiv.org/abs/2608.27406)
- PDF 链接：[https://arxiv.org/pdf/2608.27406v1.pdf](https://arxiv.org/pdf/2608.27406v1.pdf)
- 项目/代码/数据链接：
  - Project page: [https://omni-clap.github.io](https://omni-clap.github.io)
  - Code & models: 论文称已开源（未在摘要页提供具体仓库链接）
  - 数据：未在摘要页完整披露

## 核心问题
现有视频模型多绑定单一机器人形态，跨形态泛化能力弱，导致真实系统难以共享大规模异构视频语义。论文关键问题是：能否从跨 embodiment 的异构视频里学习统一物理先验，并零样本迁移到现实形态？

## 方法概要
1. 提出 action-conditioned 视频世界模型框架 CLAP，支持多人类与机器人视觉-动作观测。
2. 通过统一表示对齐异构 action space：
   - end-effector 动作空间
   - language 指令空间
   - latent 动作空间
3. 采用课程学习流程：先用 latent 动作做基础物理先验预训练，再在真实执行动作空间中对齐。
4. 在 few-shot 适配下，拓展到多个形态机器人（如 DROID、Bridge、G1）部署。

## 主要贡献
- 形成跨形态动作条件化的训练方案，显式缓解动作空间不可比对的问题。
- 构建覆盖人类与机器人视频数据的训练语料利用策略。
- 将 zero-shot 与少样本适配结合，使模型具备更好的形态迁移能力。

## 关键实验或结果
- 在 DROID 等挑战环境中，CLAP 在单形态对照方法上达到或超越 SOTA。
- 采用 few-shot 适配后性能提升明显，形成“先通用后细化”的训练路径。
- 覆盖 end-effector / language / latent 三类动作条件，任务组合面更广。

## 适合关注的原因
- 直接回应了真实机器人部署中的关键痛点：真实硬件数据稀缺与形态差异。
- 视频世界模型朝“零样本物理模拟器”方向迈进，可能缩短仿真到现实转移成本。
- 对模型架构和数据策略同时给出可复用思路。

## 局限性或待验证点
- 论文中对跨域泛化的边界（极端光照、柔性物体、长时交互）尚待更多数据支撑。
- 真实世界控制安全性约束、失败恢复策略未在摘要中充分展开。
- “代码开源”但仓库未在摘要正文给出精确链接，需要版本层面补齐。

## 对后续研究/应用的启发
- 可用于统一人机演示数据，提高稀缺形态机器人策略的预训练效率。
- 可与模型预测控制结合，形成端到端的可验证动作模拟器。
- 对具身 AI 的世界模型路线提供可复用 benchmark 与数据处理范式。

## 适合 Obsidian 快速浏览的中文总结
一句话：CLAP 通过跨形态动作统一建模，尝试把“动作世界模型”从单硬件依赖推向可零样本迁移。

## 标准化研究框架
- **Research question：** 能否借助异构视频数据建立跨形态 action-conditioned 世界模型，实现零样本或少样本下的通用物理模拟？
- **Literature：** 对比单形态世界模型与传统动作条件模型，补齐了跨 embodiment 统一动作表达的缺口。
- **Theory：** 若世界动力学在不同形态下共享，可通过统一动作表征学习到形态不变先验，再通过对齐实现零样本迁移。
- **Hypotheses：** 统一动作空间（end-effector/语言/latent）可提升跨形态泛化；课程学习可减少形态偏置；few-shot 适配能进一步补齐细节差异。
- **Method：** 训练 CLAP 进行预训练与对齐：先在无动作标签的潜在空间学习，再映射到可执行动作指令；比较 zero-shot 与 few-shot 下的基准成绩。
- **Data and Analysis：** 利用异构视频（人类 + 机器人）构建训练数据，按机器人平台（DROID/Bridge/G1 等）和任务类型做性能评估。
- **Findings：** CLAP 在 DROID 挑战任务上达到或超越单形态 SOTA；适配后性能持续增强，支持跨形态使用。
- **Conclusion：** 文章表明跨形态世界模型可行，但其真实部署边界仍需扩展到更复杂任务与安全约束场景。

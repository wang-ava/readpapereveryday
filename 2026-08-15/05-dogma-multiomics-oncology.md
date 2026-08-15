# DoGMA: A Central-Dogma-Guided Foundation Model for Multi-Omics Alignment and Multi-Task Learning in Oncology

> Spotlight：论文将生物学中的 central dogma 方向性显式注入 attention 路径，强调领域先验比单纯参数堆叠更能提升多组学 foundation model 的跨任务泛化稳定性。

- 论文标题：DoGMA: A Central-Dogma-Guided Foundation Model for Multi-Omics Alignment and Multi-Task Learning in Oncology
- 作者（机构）：
  - Junfei Ling (1)
  - Bangzheng Pu (1)
  - Bingsen Xue (1)
  - Tianle Li (2)
  - Ruying Hu (3)
  - Cheng Jin (1)
  - 机构信息：
    - (1) Institute of Medical Robotics, Shanghai Jiao Tong University
    - (2) Institute of Data Science, The University of Hong Kong
    - (3) Oriental Pan-Vascular Devices Innovation College, University of Shanghai for Science and Technology
- 发布日期（版本日期）：2026-08-08（arXiv v1）
- 主题标签：`#AI4S` `#MultiOmics` `#Oncology` `#FoundationModel` `#Transformer`
- 论文链接：[https://arxiv.org/abs/2608.08148](https://arxiv.org/abs/2608.08148)
- PDF 链接：[https://arxiv.org/pdf/2608.08148v1](https://arxiv.org/pdf/2608.08148v1)
- 项目/代码/数据链接（如可得）：未公开（arXiv 页面未给出）
- 核心问题：对称双向注意力是否会把生物信息流方向性削弱，进而限制多组学模型的迁移与泛化？
- 方法概要：
  - 在 Transformer-MoE 中引入 central-dogma 导向的注意力偏置，约束跨组学交互方向。
  - 使用 masked hierarchical omics reconstruction 做预训练，强化生物一致性表示。
  - 在癌症表示学习、生存预测、转移预测上做多任务微调。
- 主要贡献：
  - 将生物方向性先验作为架构级归纳偏置注入 foundation model。
  - 展示了生物一致注意力对跨模态 transfer 的增益。
  - 用消融说明重构预训练与方向偏置具有协同效应。
- 关键实验或结果：
  - 在多个下游任务中均表现出较强性能；论文摘要明确给出一致性提升描述。
  - 消融与分析指向“方向性 + 分层重建预训练”共同驱动改进。
- 适合关注的原因：AI4S 领域常面临数据异质、模态缺失和泛化不稳，方向性先验为模型可解释性和鲁棒性提供了稀缺约束。
- 局限性或待验证点：
  - 未公开完整细节与模型规模，复现实验受限。
  - 低质量临床数据/高噪声队列中的稳健性有待更多验证。
- 对后续研究/应用的启发：
  - 未来可将生物机制约束推广到蛋白质组、代谢组等更复杂的跨组学任务。
  - 对医疗决策系统可尝试“机制先验 + foundation model”双轨优化。
- 适合 Obsidian 快速浏览的中文总结：DoGMA 证明了在医学多组学中，先验方向约束不仅是生物学解释，更是提高跨任务泛化的工程杠杆。

## 标准化研究框架

**Research question：** 在 oncology 多组学任务中，是否能通过 central-dogma 方向约束的注意力机制显著提升跨任务迁移与缺失模态鲁棒性？

**Literature：** 先前模型多采用对称交互，难以表达生物链路方向。本工作将领域机制显式融入模型结构，形成“从数据结构到架构约束”的路径。

**Theory：** 方向性 attention 相当于对交互路径施加先验约束，减少无生物意义的信息泄漏并增强任务可转移信号。

**Hypotheses：**
- H1：带方向性约束的模型在癌种间迁移上更稳定。
- H2：层次化掩码重建可进一步增强缺失模态场景表现。
- H3：两种机制具有互补收益。

**Method：** 构建 Transformer-MoE with directed attention，采用 masked hierarchical reconstruction 预训练，再在多下游任务进行统一评估与消融。

**Data and Analysis：** 使用多癌种、多模态数据构建 pan-cancer 表征；对 survival prediction、metastasis prediction 等任务比较 DoGMA 与无方向偏置/无层次预训练基线。

**Findings：** 摘要与消融结果显示方向性先验与分层预训练带来一致收益，支持其提升跨任务泛化与生物一致性解释的结论。

**Conclusion：** AI4S 可从该工作得到可移植策略：用领域结构代替纯规模竞争，提升 foundation model 的可解释性和稳定性。

**Note：** 这是一类跨组学医疗 AI 模型设计问题，等价于社会科学中的假设检验字段并不直接对应；本节强调机制假设与任务对照。

# HounsWorld: A Multimodal World Model for Hidden Patient-State Readout, Reconstruction, and Simulation

Spotlight：HounsWorld 不是只做单点影像任务，而是把 CT 与文本作为同一 patient-state 的多模态观测。文章强调“读出—重建—模拟”三位一体的任务联合建模，有助于把临床多任务模型从单输出模式拉向统一世界模型。

## 论文信息
- 论文标题：HounsWorld: A Multimodal World Model for Hidden Patient-State Readout, Reconstruction, and Simulation
- 作者（机构）：Yunhao Bai; Zhongwei Qiu; Guangyu Guo; Yiming Huang; Tony C. W. Mok; Qinji Yu; Ling Zhang; Yan Wang（机构未在该 arXiv 摘要页完整公开）
- 发布日期：2026-08-13（v1）
- 主题标签：`#AI4S` `#MedicalImaging` `#Multimodal` `#WorldModel` `#CT`
- 论文链接：[https://arxiv.org/abs/2608.12904v1](https://arxiv.org/abs/2608.12904v1)
- PDF 链接：[https://arxiv.org/pdf/2608.12904v1](https://arxiv.org/pdf/2608.12904v1)
- 项目/代码/数据链接：项目与代码：<https://github.com/byhwhite/HounsWorld.git>
- 核心问题：传统医学 foundation model 往往将 readout（问答）、重建、生成分别建模，缺少统一患者状态表征，导致跨任务泛化和临床一致性不足。
- 方法概要：提出共享隐状态的 HounsWorld，并定义 HounsBench 基准统一三类任务（读出、文本/报告重建、条件 CT 重建与模拟）；模型将 CT 与语言视为患者状态的不同观测。通过 condition-explicit Hounsfield-unit window 采样保留临床密度特征。
- 主要贡献：
  - 提出一个统一的三任务多模态世界模型范式。
  - 用零初始化 CT adapter 保留预训练映射能力，缓解任务互相干扰。
  - 构建 patient-disjoint split 的 HounsBench，强调去泄漏评测。
- 关键实验或结果：论文指出模型在 readout、reporting 与条件 CT 合成三项任务均有持续提升，并证明 clinical structured completion 可增强 CT 理解一致性；该工作给出“同态状态模型”而非单任务 baseline 的对比框架。
- 适合关注的原因：临床场景里最难的是多模态任务之间语义一致性与可追溯性，HounsWorld 为此提供了可执行的统一建模范式，适合向纵向随访/多模态报告管线扩展。
- 局限性或待验证点：当前结果描述对具体公开指标较少，且真实临床部署中的数据标准化（扫描参数、窗口设置差异）与性能-隐私平衡尚待更详细公开；代码可用性与重现性仍需社区持续验证。
- 对后续研究/应用的启发：可将该框架迁移至 MRI、超声甚至多模态病理流程，构建“患者状态即接口”，支持读出解释、报告生成和可控模拟任务联动。
- Obsidian 快速浏览一句总结：**HounsWorld 把“患者状态”先抽象出来后再做任务分发，是 medical multimodal foundation model 的一条务实路径。**

## 标准化研究框架
**Research question：** 在医学多模态 setting 中，是否可通过共享隐患者状态同时提升 readout、重建、模拟三类任务的协同性能与一致性？

**Literature：** 先前多数医疗多模态模型采用任务分离结构，缺少同一隐状态上的联合约束；论文以 world model 视角统一任务路径，属于 AI4S 的跨任务建模流派。

**Theory：** 若将 CT+文本视为潜在状态的不同观测变量，可通过同一状态空间建模实现任务间参数共享与互补监督，降低互斥优化问题。

**Hypotheses：**  
- H1：统一状态模型在三类任务上优于单任务模型基线。  
- H2：条件化窗口采样（Hounsfield-unit aware）可提升医学合理性。  
- H3：零初始化 adapter 能减少灾难性遗忘并保留迁移能力。

**Method：** 构建 3B 参数 multimodal transformer，输入 CT volumes 与文本；训练时引入患者状态先验，分别对 readout、reporting、simulation 损失做联合优化；使用 patient-disjoint 基准验证。

**Data and Analysis：** HounsBench 统一数据划分与指标；比较任务联合模型与单任务 baseline；重点检查结构化回答准确率、重建指标以及模拟输出与真实 CT 的对齐。

**Findings：** 统一状态建模在三任务上均显示优势趋势，并在临床结构化补全中提升一致性；说明 shared latent 更能承接不同模态任务。

**Conclusion：** 该方向为 AI4S 提供“状态中心架构”样例：跨任务共享状态比任务堆叠更可能降低临床系统碎片化。  

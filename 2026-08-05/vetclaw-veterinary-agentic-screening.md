# VetClaw: An Edge-Cloud Multimodal Agentic System for Veterinary Disease Screening

Spotlight：VetClaw 是一条偏工程实现的路径：用边缘+云协同把图像分类模型升级为可编排的 agentic 工作流，强调安全、路由和失败处理而不仅是单点预测。

- 论文标题：VetClaw: An Edge-Cloud Multimodal Agentic System for Veterinary Disease Screening
- 作者/机构（如可得）：Syed Mhamudul Hasan；Anas AlSobeh；Hussein Zangoti；Abdur R. Shahid（作者机构在 arXiv 页面未直接披露）
- 发布日期/版本日期：2026-07-28（v1）
- 主题标签：`#AgenticAI` `#EdgeAI` `#CV` `#AI4S` `#Healthcare`
- 论文链接：[https://arxiv.org/abs/2607.26042](https://arxiv.org/abs/2607.26042)
- PDF 链接：[https://arxiv.org/pdf/2607.26042](https://arxiv.org/pdf/2607.26042)
- 项目/代码/数据链接（如可得）：当前页面未给出项目页或代码仓库。

- 核心问题：纯视觉分类模型很难覆盖真实医疗筛查中“输入不完整、规则约束、置信度不足时如何安全处置”的任务链路。
- 方法概要：构建 edge-cloud 协同系统：边缘端 OpenClaw 做采集、排队、工具调用与通知；云端使用 LangGraph 编排状态机式流程，完成输入校验、图像传输、VLM 推理、规则检查、条件路由、失败处理与日志记录。
- 主要贡献：
  - 以 agentic 流程替代一次性分类闭环，强调任务编排、错误恢复与安全闸门。
  - 将多模态证据（图像 + 症状文本）注入决策，提高实用场景中的可分辨性。
  - 将不确定样本通过规则触发升级流程，降低误报/误伤风险。
- 关键实验或结果：
  - 摘要指出仅用图像输入的零样本分类能力有限，而引入症状文本后分类能力提升。
  - 展示了系统可在流程上处理工作流失败、回退和告警，提升面向部署的可用性。
- 适合关注的原因：该工作不在模型创新，而在“系统化应用化”上有实操价值，特别适合对接真实诊断前端的 AI 研发团队。
- 局限性或待验证点：
  - 目前没有公开的量化对比（如具体召回率、误报率）在摘要中披露。
  - 医疗场景需要法规和数据治理流程，本工作对部署合规性未给出细节。
  - 仍需外部验证系统在不同物种和相机条件下的稳定性。
- 对后续研究/应用的启发：未来可将该架构扩展为“模型集成仲裁器”，把不同病种分类器统一接入同一状态图，形成可审计的 veterinary AI 流程。
- Obsidian 快速浏览总结：VetClaw 的价值在于把“模型能力”翻译成“workflow 可靠性”，适合做面向真实场景的 agentic 评估参考。

## 标准化研究框架
- **Research question：** 在边缘-云协同的兽医筛查任务中，如何通过 agentic 工作流提高零样本模型的实用性和安全可控性？
- **Literature：** 现有兽医 CV 工作多聚焦分类精度；该文在流程编排与安全策略上延展了“模型即服务”到“模型+流程+规则”体系。
- **Theory：** 多模态证据与状态机式控制可降低单点分类误差对决策的放大效应；当模型置信度不足时，流程仲裁可作为安全约束。
- **Hypotheses：** （1）症状文本注入能显著提高分类稳定性；（2）规则化 failure handling 能降低风险样本误导。
- **Method：** 使用 OpenClaw + LangGraph 构建边缘采集与云端编排，执行输入验证、路由、工具调用、日志与告警流程，并在零样本设置下比较单模态/多模态输入。
- **Data and Analysis：** 评估维度应包含零样本分类准确性、错误类型分布、流程失败率与告警覆盖率；对比纯图像输入与图文联合输入。
- **Findings：** 摘要层面给出图像+症状信息更优于单图像输入的方向性结果，以及系统层失败处理闭环的工程可行性。
- **Conclusion：** VetClaw 提供了 AI4S 场景下可执行的 agentic pipeline 模板，适合用于医疗前端快速原型，但仍需定量指标和外部验证补齐科学性。

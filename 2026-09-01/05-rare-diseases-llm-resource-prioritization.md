# Rare Diseases, Common Dilemmas: LLMs Prioritize Equal Resource Distribution over Patient Benefit in Decision-Making

> Spotlight（2 句）：论文聚焦医疗决策中的伦理冲突，证明现有 LLM 在罕见病场景下明显偏向“公平性”而非患者受益最大化。该结论对 AI4S 与 AI 医疗落地都很关键，因为它触及决策系统可读性与价值偏置问题。

## 基本信息
- 论文标题：Rare Diseases, Common Dilemmas: LLMs Prioritize Equal Resource Distribution over Patient Benefit in Decision-Making
- 作者：Minda Zhao, Xu Han, Rishabh Goel, Maya Dagan, Noa Dagan, Adithya Madduri, Payal Chandak, Shilpa Nadimpalli Kobren, Isaac S. Kohane（机构未在 arXiv 页面完整披露）
- 发布日期（版本）：2026-08-25（v1）
- 主题标签：`#AI4S` `#Healthcare` `#Ethics` `#LLM` `#Benchmark`
- 论文链接：[https://arxiv.org/abs/2608.25236v1](https://arxiv.org/abs/2608.25236v1)
- PDF 链接：[https://arxiv.org/pdf/2608.25236v1.pdf](https://arxiv.org/pdf/2608.25236v1.pdf)
- 项目/代码/数据链接：
  - 代码：未公开
  - 数据：未公开（文中公开了 208 题数据规模与伦理冲突范式）

## 核心问题
当 AI 需要在稀缺资源与患者个体获益之间做选择时，LLM 是否会不自觉偏向某些伦理原则？论文在罕见病背景下建立 208 个高冲突临床案例，检验模型的伦理偏好。

## 方法概要
1. 构建临床决策 vignette 数据：聚焦罕见病中常见的资源分配冲突。
2. 设计多目标文本问题，包含可辩护但冲突的下一步决策选项。
3. 调用 11 个 SOTA LLM 在统一提示下评估，观察决策偏向。
4. 分析 framing 效应：committee / clinician / patient 身份框架对输出分布的影响。

## 主要贡献
- 提供 208 个带伦理冲突的罕见病评测集合，覆盖 beneficence、non-maleficence、autonomy、justice 多目标决策。
- 发现大模型普遍偏向“equal resource distribution”，并弱化病情严重度等差异信息。
- 首次系统比较不同 framing 下模型偏好变化，揭示上下文角色对决策偏置的调节效应。

## 关键实验或结果
- 11 个先进 LLM 在该基准上都显示统一趋势：优先考虑 justice。
- 资源分配场景下，模型对患者严重程度敏感度显著不足。
- 在 committee framing 下偏向 justice 更强；当输出角色被置为 clinician/patient 时，beneficence 与 autonomy 有回升。

## 适合关注的原因
- 直接指出了医疗 AI 的“价值取向偏差”可定量化且可复现。
- 对监管、临床决策辅助、风险沟通都有现实指导意义。
- 结果表明模型可信度不能只看准确率，伦理对齐评估必须前置。

## 局限性或待验证点
- 结果依赖特定提示和 benchmark 设计，不同语言和医院语境下需重新验证。
- 当前仍缺少与真实临床流程深度耦合的前瞻性试验。
- 机构与部署环境差异可能显著影响决策倾向，单一基准风险外推偏差。

## 后续研究/应用启发
- 可将该 benchmark 扩展到不同病种与医保制度情境，校准不同价值权重。
- 与透明化策略（如显式伦理权重）结合，形成可解释的建议路径。
- 可用于模型上线前的 safety checklist，并作为医疗监管测试项。

## 适合 Obsidian 快速浏览的中文总结
一句话：这项工作用罕见病案例显示 LLM 在资源分配上有明显公平性偏置，提醒 AI 医疗必须把伦理权重校准前置化。

## 标准化研究框架
- **Research question：** 在临床伦理冲突场景中，LLM 的决策是否系统性偏向某一价值原则？
- **Literature：** 与现有 AI 医疗公平性评测相比，该研究把 ethics alignment 从静态 benchmark 扩展到可调控的 framing 条件。
- **Theory：** 假设模型对上下文角色（谁负责决策）高度敏感，进而改变价值权衡；并假设稀缺资源场景会放大 fairness 偏置。
- **Hypotheses：** 11 个 SOTA 模型会出现 justice 偏向；prompt framing 会显著改变 beneficence/autonomy 的权重；严重度差异在模型决策中低估。
- **Method：** 通过 208 个罕见病 vignettes 与 4 类伦理决策选项进行问答式评测，比较不同角色 framing。
- **Data and Analysis：** 统计输出分布并做 framing 与语义冲突的对照分析。
- **Findings：** 论文报告显示 justice 偏好在多数设置下占优，且 framing 变化可部分纠正偏差。
- **Conclusion：** 该研究为医疗 AI4S 安全部署提供了可操作的风险指标；在社会科学意义上可视作对“伦理可解释性”假设的实证反证。

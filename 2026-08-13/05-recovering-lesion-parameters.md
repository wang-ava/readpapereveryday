# Recovering Lesion Parameters from Aphasic Picture Naming Error Profiles in Large Language Models

> Spotlight：这篇工作把“可解释性”的单向分析转成了反向可验证问题：不仅观察行为，还尝试重建导致行为的模型扰动参数，对 LLM 内部机理研究具有很强诊断价值。

- 论文标题：Recovering Lesion Parameters from Aphasic Picture Naming Error Profiles in Large Language Models
- 作者（机构）：Yong Yang, Roger Newman-Norlund, Xiang Guan, Saeed Ahmadi, Regan Willis, Nadra Salman, Kalil Warren, Sophie Arheix-Parras, Srihari Nelakuditi, Leonardo Bonilha, Christopher Rorden, Rutvik H. Desai, Julius Fridriksson；机构未在 arXiv 页面统一列示（需按作者主页确认）
- 发布日期（版本日期）：2026-08-05（arXiv v1，Submission: Fri, 5 Aug 2026）
- 主题标签：`#AI4S` `#Interpretability` `#InverseProblem` `#ComputationalPsycholinguistics`
- 论文链接：[https://arxiv.org/abs/2608.06429](https://arxiv.org/abs/2608.06429)
- PDF 链接：[https://arxiv.org/pdf/2608.06429v1](https://arxiv.org/pdf/2608.06429v1)
- 项目/代码/数据链接（如可得）：当前未公开代码或数据链接；论文仅给出 4,840 组扰动配置与参数设置。
- 核心问题：除了“能否解释”LLM 表征外，能否根据错误画像反推出造成该错误的“虚拟病变”参数？
- 方法概要：在 LLaVA-Vicuna 13B 上施加分层扰动（层索引、修改比例、噪声强度）生成 4,840 组配置，按 7 类失误标签构建画像；训练 multi-task 网络学习错误画像到扰动参数的映射，并做反向重建验证。
- 主要贡献：
  - 将 interpretability 从相关分析转向逆向可检验问题（inverse lesioning）。
  - 揭示“低层索引不可精确恢复但重建行为可成功”的功能冗余现象。
  - 引入真实卒中患者错误画像进行 out-of-distribution 验证。
- 关键实验或结果：参数恢复中 modification percentage 与 noise sigma 可较好重建；layer index 仅可粗粒度恢复；将恢复参数施加到新模型实例后，81.4% 情况可复现目标错误表现。
- 适合关注的原因：AI for Science/AI in Medicine 中，“可解释但可验证”是关键门槛，方法兼具诊断价值和现实临床表征分析启发。
- 局限性或待验证点：任务以图片命名为例，临床可迁移性到更广泛语言症状评估尚待验证。
- 对后续研究/应用的启发：可拓展到模型审计与健康 AI 的反事实解释框架，用逆向参数恢复做机制诊断和安全红队分析。
- 适合 Obsidian 快速浏览的中文总结：该文提出逆向恢复 LLM“病变参数”的方法，在解释失误画像时给出可复现的反证路径，临床 AI 方向很值得追踪。

## 标准化研究框架

**Research question：** 给定错误画像，能否恢复产生该画像的 LLM 内部扰动参数，并用反向验证评估模型可解释性？

**Literature：** 传统可解释工作多描述内部状态与行为相关性；该研究将其提升为逆向参数估计与反事实再现。

**Theory：** 如果错误分布对扰动参数存在可辨识映射，即使某些层级参数不完全可辨识，也可通过泛化重建测试检验机制充分性。

**Hypotheses：** 多任务映射可部分恢复扰动参数；成功重建后模型会在多实例上复现实验误差模式。

**Method：** 构建七类错误标签数据；对 4,840 扰动配置训练映射模型；用 278 例真实患者画像做 OOD 验证。

**Data and Analysis：** 比较参数估计精度与反事实复现率（81.4%）；区分可恢复与不可恢复参数（层索引为关键难点）。

**Findings：** 模型可较好恢复扰动强度与噪声参数，但层索引恢复仅邻域级别，且反向重建支持“功能冗余”解释。

**Conclusion：** 该工作为可解释性研究提供了可验证框架；对更复杂任务和临床评估泛化仍需更多跨任务实验。

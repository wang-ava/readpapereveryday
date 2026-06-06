# Jailbreaking Vision-Language Models Through the Visual Modality

> Spotlight：这篇 ICML 2026 论文把视觉输入视为 VLM safety 的一等攻击面。核心发现是：文本安全训练不能自动泛化到视觉模态，VLM 对“以视觉方式表达的有害意图”仍可能脆弱。

## 基本信息

- 论文标题：Jailbreaking Vision-Language Models Through the Visual Modality
- 作者/机构：Aharon Azulay, Jan Dubiński, Zhuoyun Li, Atharv Mittal, Yossi Gandelsman
- 发布日期：2026-05-01
- 会议状态：Accepted to ICML 2026
- 主题标签：#VLM #ComputerVision #AISafety #MultimodalSafety #Alignment
- 论文链接：https://arxiv.org/abs/2605.00583
- PDF 链接：https://arxiv.org/pdf/2605.00583
- 项目/代码/数据链接：arXiv 页面未列出明确项目或代码链接

## 核心问题

很多 VLM 继承了文本 LLM 的安全训练，但视觉输入并不只是文本的附属通道。用户可以把意图、隐喻、替代符号或上下文线索放在图像里，使模型面对跨模态语义时暴露 alignment gap。

## 方法概要

论文提出四类利用视觉模态的 jailbreak attack，并在六个 frontier VLM 上评估。这些攻击通过视觉符号、语义替换、图像中文本替换或视觉类比等方式，让有害意图绕开只针对文本表述的安全机制。

## 主要贡献

- 系统把视觉模态定义为 VLM safety 的独立攻击面。
- 展示文本安全对齐不能自然覆盖视觉表达的有害意图。
- 在多个 frontier VLM 上验证 cross-modality alignment gap。
- 给出初步 interpretability 和 mitigation 讨论，推动后续 VLM 安全训练把视觉通道纳入核心目标。

## 关键实验或结果

论文摘要报告，作者在 6 个 frontier VLM 上评估视觉攻击。一个例子是 visual cipher 在 Claude-Haiku-4.5 上达到 40.9% attack success，而等价 textual cipher 为 10.7%，显示视觉通道可以显著放大绕过风险。

## 为什么值得关注

VLM 正在进入浏览器代理、手机助手、机器人、医疗影像和安全监控等场景。如果安全机制只在文本层判断请求是否有害，视觉输入会成为系统级漏洞。对具身智能而言，这一点更关键，因为视觉理解会直接影响行动。

## 局限性或待验证点

- 论文聚焦 jailbreak 成功率，真实部署中的多层防护、工具权限和人工确认可能改变风险大小。
- 不同 VLM 的视觉编码器、OCR、captioning 中间层和 safety head 差异很大，攻击可迁移性需要持续更新。
- 防御需要避免过度拒答，否则会损害正常视觉推理任务。

## 对后续研究/应用的启发

VLM safety 应该在训练、评测和部署三层同时纳入视觉通道：训练时包含跨模态有害意图样本，评测时设计视觉语义攻击 benchmark，部署时对视觉输入、OCR 输出、模型解释和工具调用做联合审计。

## Obsidian 快速总结

VLM 安全不能只问“文本 prompt 是否安全”，还要问“图像是否在表达同一个危险意图”。

## 标准化研究框架

**Research question：** 视觉模态是否能成为绕过 VLM 安全对齐的独立攻击面？

**Literature：** 背景包括 text-only LLM jailbreak、multimodal jailbreak、VLM alignment、视觉 OCR/语义理解、adversarial examples 和 AI safety evaluation。既有工作更常关注文本提示或像素级扰动，较少系统分析视觉语义层面的安全缺口。

**Theory：** 论文的理论基础是 cross-modality alignment gap：文本安全训练主要覆盖语言表达的有害意图，但视觉输入可以通过符号、上下文和类比承载同样意图，而安全机制未必能映射到同一拒答边界。

**Hypotheses：** 可转写为：视觉表达的有害意图能绕过部分 VLM 安全机制；视觉攻击在部分模型上比等价文本攻击更有效；鲁棒 VLM 对齐必须把视觉通道作为一等训练目标。

**Method：** 设计四类视觉模态 jailbreak，并在 6 个 frontier VLM 上比较 attack success；同时进行初步解释性和缓解分析。

**Data and Analysis：** 数据由作者构造的视觉攻击样本与对应文本变体组成。分析比较不同攻击类别、不同模型和视觉/文本等价条件下的成功率。

**Findings：** 视觉攻击能够显著绕过部分 VLM 安全对齐；例如 visual cipher 在某模型上的成功率明显高于等价文本版本。结果支持“视觉通道需要独立 safety post-training”的判断。

**Conclusion：** VLM alignment 必须从文本安全扩展到跨模态语义安全，否则视觉输入会成为绕过模型治理的薄弱环节。

# Evidence-Consistent Generative Detection under Scenario-Level Distribution Shift

该文指出常规分布内评估容易被场景暗示劫持，提出在场景级 OOD 条件下保留证据一致性，提升生成式检测的泛化性。

## 论文标题
Evidence-Consistent Generative Detection under Scenario-Level Distribution Shift

## 作者/机构
- 作者：San Kim；JinYeong Bak
- 机构：arXiv 摘要页未给出统一机构信息。

## 发布日期/版本日期
- 提交日期：2026-08-21（版本页在当前抓取中未给出具体时刻，页面显示 v1，提交于 21 Aug 2026）
- 版本：v1

## 主题标签
#LLM #OOD #GenerativeDetection #Phishing #RationaleConsistency

## 论文链接
- https://arxiv.org/abs/2608.21043v1

## PDF 链接
- https://arxiv.org/pdf/2608.21043v1.pdf

## 项目/代码/数据链接（如可得）
- 代码与数据： https://github.com/kimsan1120/ECoG

## 核心问题
许多检测模型在同分布评估表现很好，但遇到“场景级”未见过的攻击时失败，说明它们可能过度依赖场景表面线索而非决策证据。

## 方法概要
- 定义 Scenario-level OOD (SL-OOD)：持有攻击场景标签，但验证集上场景是未见过的。
- 提出 ECoG 框架：加入 evidence-span 监督与 rationale-label 一致性目标。
- 强制模型输出与证据跨度和标签推断保持一致，减少“答对但理由错”现象。

## 主要贡献
1. 把泛化问题从任务级扩展到场景级，暴露检测模型记忆场景偏置的风险。
- 2）将证据一致性作为约束目标，减少文本生成解释与预测标签冲突。
- 3）给出多基线对比，验证方法在多个解码器上的稳健性。

## 关键实验或结果
- 相比无一致性正则的 0.5B 解码器，Macro-F1 在挑战性 OOD 样本上提高 **3.22**。
- 预测-理由反向不一致比例下降 **4.22**。
- token-level 与参考 evidence overlap 提升 **8.38**。

## 适合关注的原因
- 这篇工作为“模型会不会真的懂，而不仅仅是会记”提供可执行验证框架，适合做高风险文本检测与风控。

## 局限性或待验证点
- 数据场景仍聚焦于钓鱼与通信文本，需扩展到更多业务域。
- 与更大规模模型的比较还需补齐。
- 如果未来攻击者刻意对齐生成 rationale，它的抑制能力仍需验证。

## 对后续研究/应用的启发
- 任何高风险分类器都应增加“证据一致性回路”，把解释一致性指标纳入训练目标。
- 可用于风控平台与审核模型的离线回归测试：同分布性能高不等于上线安全。

## 适合 Obsidian 快速浏览的中文总结
通过场景级留一法+证据一致性约束，ECoG 让生成式检测从“会答”走向“能给出可核验证据并稳健泛化”。

## 标准化研究框架
**Research question：** 能否通过证据跨度与 rationale-label 一致性约束，在场景级分布偏移条件下提升生成式检测的泛化可靠性？

**Literature：** 传统评测多停留在同分布 benchmark，本研究提出 SL-OOD 视角，并强调“结果正确但解释错误”是高危隐患，弥补现有研究盲点。

**Theory：** 若模型被迫解释自身判断且解释必须与证据跨度一致，泛化将更依赖可迁移证据，而非数据集特定线索。

**Hypotheses：** 1）SL-OOD 会显著拉开不同模型鲁棒性差距；2）证据一致性正则可提升 OOD 下 Macro-F1；3）该效应在多解码器中可复现。

**Method：** 构建场景级留一 split；训练基线与 ECoG；对比预测标签精度、预测-理由一致性及证据覆盖指标。

**Data and Analysis：** 在 SMS/语音钓鱼数据与多类模型上测试，并报告 Macro-F1、反例一致性下降幅度、证据重叠率等。

**Findings：** ECoG 在多个基线上持续提升 OOD 鲁棒性，尤其在证据-标签一致性和 rationale 可靠性方面表现突出。

**Conclusion：** 场景级验证与证据一致性是检验生成式检测“可靠性”的关键升级，尤其适合风控与安全部署前评估。

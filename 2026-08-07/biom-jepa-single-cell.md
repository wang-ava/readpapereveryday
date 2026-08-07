> **Spotlight：** BioM-JEPA 不重建稀疏的单基因 token，而是预测由蛋白关联与共表达图连接的基因块表征。它把生物网络先验嵌入 JEPA 目标，在扰动预测、表征诊断和吞吐量上给出一组值得复核的结果。

# BioM-JEPA: joint-embedding prediction of graph-connected gene blocks in single cells

- **作者/机构：** Yuhao Wang、Zelin Zang、Yuxuan Liu、Zhen Lei、Stan Z. Li；机构待正文核对
- **发布日期/版本：** 2026-08-06，arXiv v1
- **主题标签：** #AI4S #单细胞 #生物信息学 #JEPA #FoundationModel #图学习
- **论文链接：** https://arxiv.org/abs/2608.05928
- **PDF：** https://arxiv.org/pdf/2608.05928
- **项目/代码/数据：** arXiv 提供各图数值源数据 ancillary files；作者称训练代码与 checkpoint 将通过 GitHub 发布，但摘要页尚无仓库链接

## 核心问题

单细胞转录组是稀疏观测，但背后的生物过程由协同基因程序构成。逐基因重建容易学习测序深度和缺失模式，而非稳定的生物结构。论文问：若把图连接的基因块作为自监督预测单位，是否能学到更高秩、较少受 detected-gene depth 影响且对下游任务更有用的表征？

## 方法概要

BioM-JEPA 用蛋白关联证据和语料共表达证据定义 graph-connected gene blocks。student network 从某个细胞剩余基因推断目标基因块的聚合表征，slowly updated teacher 则从完整已观测基因集合产生目标。该目标避免直接重建每个稀疏 token；同时使用 linear attention，避免构造二次复杂度的 gene-by-gene attention matrix。

## 主要贡献

1. 将 JEPA 式 joint-embedding prediction 引入单细胞数据，并以有生物意义的图连接基因块作为预测单位。
2. 从 effective rank、测序深度相关性、通路/邻域信息和扰动响应等角度诊断表征，而非只报单一分类分数。
3. 用 linear attention 提升大规模基因表示的训练和提取吞吐量。
4. 随论文提供图表数值源数据，并称后续公开训练代码与 checkpoint。

## 关键实验或结果

- 在所报告的提取流程下，block-level prediction 的 embedding 比 token prediction、random-block 和 reconstruction 对照具有更高 effective rank，并与 detected-gene depth 的关联更弱。
- 在 CellBench 任务中，冻结 BioM-JEPA embedding 保留 expression、pathway 和 neighbourhood 信息，并在受测模型中取得最低的 aggregate perturbation-response error。
- 表征诊断与经典胰腺细胞程序、遗传扰动间的组合关系一致。
- 在 matched one-epoch hPancreas、batch size 8 设置中，相比 scFoundation，fine-tuning throughput 提高 **5.75 倍**，held-out embedding throughput 提高 **3.76 倍**。

## 适合关注的原因

它展示了 AI4S 中一种重要建模路线：不要机械照搬语言 token 目标，而要根据科学对象的组织结构重新定义 prediction unit。图连接基因块也为模型可解释性提供了更自然的中间层，可与 pathway 或 protein interaction network 对齐。

## 局限性或待验证点

- 图结构来自已有蛋白关联与语料共表达证据，可能继承知识库覆盖偏差，并对研究充分的基因更有利。
- “与测序深度关联更弱”不等于完全消除技术批次、平台或细胞质量混杂。
- aggregate perturbation error 会压平不同细胞类型、扰动强度与 out-of-distribution 条件下的差异。
- 吞吐量比较依赖 batch size、硬件、实现优化和序列设置；不能直接外推到所有训练规模。
- 代码和 checkpoint 尚未在摘要页正式链接，当前复现承诺仍待兑现。

## 对后续研究/应用的启发

可比较 PPI、共表达、调控网络和数据驱动动态图作为 block 构造先验，测试科学知识先验何时帮助、何时限制新发现。另一个方向是让 block 随细胞类型或扰动条件动态变化，并用 pathway-level uncertainty 标记模型不确定的生物程序。

## Obsidian 快速浏览总结

**一句话：BioM-JEPA 用图连接基因块替代逐基因重建，使单细胞自监督目标更接近生物程序，并兼顾下游效果与计算效率。**

## 标准化研究框架

**Research question：** 图连接基因块是否是比单基因 token 更适合单细胞表征学习的自监督预测单位？

**Literature：** 工作连接单细胞 foundation model、掩码重建、JEPA、基因网络先验和扰动响应预测；针对逐基因重建对稀疏性与技术深度敏感的问题。

**Theory：** 生物功能由协同基因程序承载，因此预测结构连接的聚合表征应比恢复独立稀疏基因更能保留可迁移生物信息。

**Hypotheses：** 非社会科学假设检验；技术假设是 graph-connected block prediction 相比随机块、token prediction 和 reconstruction 能得到更高质量、较少深度混杂的 embedding。

**Method：** student-teacher JEPA、PPI/共表达图基因块、剩余基因条件预测、slow teacher 更新与 linear attention。

**Data and Analysis：** CellBench 下游任务、hPancreas 吞吐实验、表征 effective rank/深度关联诊断、通路/邻域保持与扰动响应比较。

**Findings：** 摘要报告表征秩更高、深度关联更弱、聚合扰动误差最低，并在匹配设置下较 scFoundation 有 5.75×/3.76× 吞吐优势。

**Conclusion：** 将生物图结构用于定义 JEPA 预测单位，是构建高效、结构感知单细胞 foundation model 的有前景方向，但跨平台泛化和先验偏差仍需验证。


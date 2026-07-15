# Requential Coding: Pushing the Limits of Model Compression with Self-Generated Training Data

## Spotlight（今日速读）
这篇论文把“模型压缩”从参数压缩转为“训练过程信息压缩”，通过让学生模型从自己的分布采样并只记录分歧信息，给出了与规模更强耦合的可解释框架。它兼顾理论与实践，尤其适合关注泛化证明和大模型可扩展性的路线。

## 论文标题
Requential Coding: Pushing the Limits of Model Compression with Self-Generated Training Data

## 作者/机构
- 作者：Shikai Qiu, Marc Finzi, Yujia Zheng, Kun Zhang, Andrew Gordon Wilson
- 机构：arXiv 页面未公开机构字段（可从论文 PDF/作者主页补齐）

## 发布日期
2026-07-13（v1，arXiv）

## 主题标签
#LLM #ModelCompression #LearningTheory #PACBayes #InformationTheory

## 论文链接
https://arxiv.org/abs/2607.11883

## PDF 链接
https://arxiv.org/pdf/2607.11883v1

## 项目/代码/数据链接（如可得）
- 代码：https://github.com/shikaiqiu/requential-coding
- 数据：未在摘要中单独给出固定公开数据包名

## 核心问题
传统 prequential coding 偏向编码完整训练数据序列，难以反映模型实际学到的可压缩结构。论文核心问题是：能否以 self-generated 的训练样本选择方式构建更高效、与模型能力和可学习信息更一致的编码长度？

## 方法概要
- 用教师模型从学生模型自身分布采样训练样本，构成“选择”序列。
- 学生模型只编码“教师与学生分歧”的样本/事件，减少冗余信息。
- 给出理论上独立于参数规模与数据熵的编码长度推导。
- 与 prequential coding 对比，评估不同模型规模与 ensemble 的压缩率与泛化 bound。

## 主要贡献
- 提出 requential coding 机制，解决传统轨迹编码对高熵数据编码成本过高的问题。
- 提出可与 PAC-Bayes 分析结合的压缩解释框架，给出更强一般化上界。
- 给出规模效应发现：在保持 loss 的情况下，规模更大或 ensemble 未必更难压缩，反而更高效。
- 用实验揭示过拟合与可学信息随训练 epoch 的变化关系。

## 关键实验或结果
- 在对比中，requential code 常大幅短于 prequential code，尤其在更大模型上优势明显。
- 当保持同等损失时，越大模型/集成在该框架下可更好压缩，支持“能力增长优于参数膨胀成本”。
- 该框架的 generalization bound 在 7B 级别 LLM 上达到先进水平，且越接近计算最优尺度越收紧。
- 显示出学习信息与随机内容可分离趋势，文本数据比图像数据更具可学性。

## 适合关注的原因
它把压缩问题提升为“理解-可压缩性-泛化”的一体化问题，不仅对模型部署（部署成本、知识蒸馏）有意义，也给理论研究提供可检验的桥梁。

## 局限性或待验证点
- 方法是否在超大规模商业闭源模型上稳定迁移仍未验证。
- 计算开销与训练稳定性依赖教师模型选择策略，工程层面门槛不低。
- 对超高噪声或极端数据偏移场景的鲁棒性尚需补充实验。

## 对后续研究/应用的启发
- 可用于探索更“轻量”但更可解释的蒸馏与早停策略。
- 结合数据治理可定义“可压缩性预算”，为模型训练成本做更细粒度控制。
- 作为理论基线用于评估 RLHF/指令微调后是否真的带来新信息学习而非参数拟合堆积。

## 一句话总结
这篇论文表明模型可学性可被编码角度度量，并且用自采样思想有望在大模型时代给出更真实的泛化上界。

## 标准化研究框架
- **Research question：** 能否设计一种独立于参数规模的数据编码方法，更准确捕捉模型真实可学信息并改善泛化保证？  
- **Literature：** 对标 prequential coding 与 PAC-Bayes 传统路线，本工作把压缩目标从“编码原始序列”改为“模型分歧信号”。  
- **Theory：** 在非社会科学语境下可等同于：用信息论定义学习复杂度，并通过 teacher-student 采样机制建立可计算的压缩上界。  
- **Hypotheses：** H1：self-generated 采样能降低编码长度；H2：更大模型在同损失下可实现更短 code；H3：code 长度与泛化行为呈一致的边界关系。  
- **Method：** 定义 requential code 的采样与编码规则；与 prequential baseline 做对比；再用 PAC-Bayes 推导一般化上界。  
- **Data and Analysis：** 以公开训练设置上的 LLM 为主要对象，关注 scale、ensemble、epoch、代码长度及边界紧度的关系；分析可学信息与随机信息成分。  
- **Findings：** 结果支持 self-generated 分歧编码显著优于 prequential baseline，且放大效应在更大模型上更明显。  
- **Conclusion：** 该方法为大模型压缩与泛化评估提供了可复用框架，未来可推动“压缩率驱动的训练预算决策”。


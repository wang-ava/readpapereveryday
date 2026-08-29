# Trustworthy RAG: An Evaluation Agent for Detecting Misinformation and Knowledge Poisoning in Generative AI Systems

RAG 常把“检索到的内容”默认可信，该方法将评估前置化为“先过滤再生成”，用 evaluation agent 在生成前识别知识中毒与事实不一致。

## 论文标题
Trustworthy RAG: An Evaluation Agent for Detecting Misinformation and Knowledge Poisoning in Generative AI Systems

## 作者/机构
- 作者：Balkrishna Giri；Md Toufique Hasan；Jussi Rasku；Muhammad Waseem；Pekka Abrahamsson
- 机构：arXiv 摘要页未给出统一机构字段；标题与作者信息未展示机构元数据。

## 发布日期/版本日期
- 提交日期：2026-08-21 13:42:41 UTC
- 版本：v1

## 主题标签
#RAG #Misinformation #KnowledgePoisoning #LLM #Agent #AI4S

## 论文链接
- https://arxiv.org/abs/2608.21095v1

## PDF 链接
- https://arxiv.org/pdf/2608.21095v1.pdf

## 项目/代码/数据链接（如可得）
- 代码： https://github.com/GPT-Laboratory/TrustworthyRAG
- 数据/攻击器：论文中说明已发布 attack generator 与实验 artifacts，均在同一代码仓库。

## 核心问题
RAG 系统普遍依赖检索相关性作为信任依据，容易被知识中毒攻击误导；现有方法常在生成后再判断，导致不可信片段可能已被利用。

## 方法概要
- 设计 Evaluation Agent 中间件，在上下文交给主模型前拦截。
- 融合三类组件：NLI 事实核验、五信号毒性检测（加权聚合）、Trust Index。
- Trust Index 定义为 `T = 0.4F + 0.35C + 0.25(1-P)`，并加入高污染场景非线性抑制。

## 主要贡献
1. 将“安全—可信”判定前置到 generation pipeline 的上下文层。
2. 用一套可解释的 Trust Index 将事实一致性、上下文一致性和中毒风险统一量化。
3. 在 RAG 场景下提供跨模型对比，支持阈值校准以提升部署可迁移性。

## 关键实验或结果
- 在 TruthfulQA + Llama 3.3 70B 下：accuracy 达 **91%**，precision **100%**，instruction injection 上 recall **100%**。
- AUC 在三类 LLM 上维持 **0.73–0.81**。
- 在 OWASP Top 10/CWE 的软件安全场景中，指令注入防护 F1 达 **92%**。
- 仍有缺口：in-place edits（如实体替换）和细粒度语义削弱较难检测。

## 适合关注的原因
- 这类“先检索后决策”的可插拔评估代理，对企业级生成式AI系统（尤其安全敏感场景）落地价值直接。

## 局限性或待验证点
- 对语义级轻度篡改的鲁棒性不足，仍会出现检测漏报。
- 论文提到跨数据集泛化需要域内阈值校准，工程上会增加参数治理成本。
- 尚未看到针对超大规模生产负载下的延迟基线。

## 对后续研究/应用的启发
- 可作为“RAG 控制平面”独立服务部署，与主 LLM 解耦，降低主体模型替换带来的风险。
- 可与可解释日志体系结合，构建“拒绝前先证据化”的审计工作流。

## 适合 Obsidian 快速浏览的中文总结
把 RAG 可信判断前置为独立评估代理，先识别中毒与事实错配，再放行上下文生成，强化生成安全基线。

## 标准化研究框架
**Research question：** 在真实工程场景下，能否用低侵入式评估代理提升 RAG 的抗中毒与抗误导能力，而不显著牺牲通用可用性？

**Literature：** 既有工作覆盖检索增强推理与事实验证，但多数把验证放在生成后或单指标判断，本研究将 NLI 与污染识别统一并前置。

**Theory：** 若将“检索相关性”与“可确信度”解耦，并通过聚合式分数过滤高风险上下文，就可以降低被中毒文本驱动生成的机会。

**Hypotheses：** 1）前置评估比后验检测更能抑制 instruction injection；2）Trust Index 的多信号融合优于单一验证器；3）阈值校准是跨模型部署的关键。

**Method：** 设计 Evaluation Agent 的三模块流程（NLI+五信号检测+Trust Index），并对 TruthfulQA、软件安全问答与跨模型场景做对照。

**Data and Analysis：** 使用作者公开的攻击生成器与基准构建中毒样本；比较 accuracy、precision、recall、ROC-AUC 与 F1 指标，并分析难样本（in-place edits）的残差。

**Findings：** 该代理在生成前过滤场景显著提升毒性检测效果，但对细粒度语义改写类攻击仍存在漏检空间。

**Conclusion：** 在高安全要求的 RAG 系统中，前置式 evaluation agent 是可行且有效的防线，但仍需补齐轻量篡改攻击下的二次检测。

# Generative Skill Composition for LLM Agents

## Spotlight（今日速读）
论文把 agent 技能调用从“检索一组候选技能”升级为“有顺序的可执行组合决策”问题。  
它给出一个结构化视角：不仅要选技能，还要选“几次 + 顺序”，这对生产环境中的 coding agent 非常关键。

## 论文标题
Generative Skill Composition for LLM Agents

## 作者/机构
- 作者：Xinyu Zhao, Zhen Tan, Vaishnav Tadiparthi, Nakul Agarwal, Kwonjoon Lee, Ehsan Moradi Pari, Hossein Nourkhiz Mahjoub, Tianlong Chen
- 机构：The University of North Carolina at Chapel Hill；Arizona State University；Honda Research Institute USA

## 发布日期
2026-06-30（v1）

## 主题标签
#LLM #Agent #Code-Agent #Skill-Oriented-Inference #Evaluation

## 论文链接
https://arxiv.org/abs/2606.32025

## PDF 链接
https://arxiv.org/pdf/2606.32025v1

## 项目/代码/数据链接
- 项目页： https://skill-composer.github.io/
- PDF 主页（含实验细节）： https://skill-composer.github.io/static/pdfs/paper.pdf
- 代码链接：arXiv 页面未显式列出稳定的公开仓库链接；可先按项目页后续补充

## 核心问题
在大规模技能库场景下，LLM agent 如何同时决定：
1) 需要加载哪些技能，2) 每个技能加载多少次，3) 执行顺序是什么？  
现有检索式或推理式方案往往把“subset”与“order”拆开处理，难以优化实际执行路径。

## 方法概要
- 将 skill 组合定义为任务条件下的结构化序列预测问题（subset + cardinality + order）。
- 使用约束自回归解码器（constrained autoregressive decoder）逐步生成 skill index 序列。
- 解码时融合检索先验与集合规模先验，实现一次推理同时输出“要用哪些技能 + 用多少 + 顺序”。
- 基于 196 个技能构建 9,872 条任务-组合样本，构造 skillsbench 评估链路。

## 主要贡献
- 提出 SkillComposer，并明确了 LLM agent 技能使用的“3D”决策框架（determine subset / count / order）。
- 通过约束解码把“技能选择”从分类问题转为序列结构化生成问题，降低上下文成本。
- 在不依赖巨大模型的前提下，给出参数高效且可解释的 baseline 与可复现的评测流程。

## 关键实验或结果
- 在 GPT-5.2-Codex 上相比无 skill 基线提升 +23.1 pp pass rate；在 Gemini-3-Pro-Preview 上提升 +18.2 pp。
- 模型参数约 3.9M，仅是 600M SFT baseline 的约 1/154，参数规模显著更小。
- 在分布偏移下 Set F1 提升约 +19.3 pp（paper 中给出的对比指标）。
- 在有限预算下达到更优的 pass rate 与 token 效率平衡，支持“组合-执行”闭环优化。

## 适合关注的原因
这篇论文把“工具/技能调用策略”从经验工程优化变成可度量、可学习、可比较的模型问题，对 coding agent 和企业自动化工作流很有实践价值，特别适合替代当前粗粒度的工具编排基线。

## 局限性或待验证点
- 研究依赖特定技能库构成，库外迁移性仍需验证。
- 结果主要围绕生产级 coding 任务，跨域泛化到 Web/多模态/物理环境任务尚待公开验证。
- 与真正的大规模在线 agent 工程系统中的延迟、成本和安全约束融合，尚缺少完整消融。

## 对后续研究/应用的启发
- 可将 skill graph 与 retrieval 系统联动，把任务上下文中的隐式依赖关系纳入顺序约束。
- 可用于构建“先天可解释”的 agent planner，替代纯 black-box tool-calling 的不可控调用行为。
- 可与 agent benchmark 直接耦合为自动化优化目标：提高长期任务成功率而非只追求一次调用覆盖。

## 标准化研究框架
- **Research question：** 如何在固定/可更新技能库中联合预测“选谁、选几、选哪种顺序”，以提高真实任务成功率并降低推理代价？  
- **Literature：** 现有研究将 skill 选择视作 retrieval 或 end-to-end reasoning，但大多未显式建模技能数量与顺序的联合可执行决策；本工作系统化补齐该缺口。  
- **Theory：** 在非社会科学场景下可理解为“结构化决策网络+代价受限序列生成”问题：agent 行为由可执行技能序列的后验最优化决定。  
- **Hypotheses：** H1：联合建模能显著提升技能任务匹配精度。H2：约束解码可在不显著增加 token 的情况下减少上下文膨胀。H3：低参数模型在离线+在线复合任务中可接近较大模型的上界性能。  
- **Method：** 构建训练任务-组合数据对，使用约束自回归序列生成模型联合预测技能序列；以 SkillsBench 与 token budget 衡量下游执行表现。  
- **Data and Analysis：** 196 skill 库、9,872 task-composition 样本；对比无 skill 基线、检索 top-3、全文灌入多个技能配置；分析 pass rate、Set F1、token 成本。  
- **Findings：** 联合决策显著提升 pass rate 与结构鲁棒性，且以更小参数量和更低 token 代价接近 oracle 上界。  
- **Conclusion：** agent 的可扩展性瓶颈更多在“组合策略学习”而非单一检索精度，结构化 skill composition 是一条可扩展路径。  

一句话总结：把“能用什么技能”升级为“怎么按顺序高效地用多少个技能”是当前生产级 LLM agent 提效关键。

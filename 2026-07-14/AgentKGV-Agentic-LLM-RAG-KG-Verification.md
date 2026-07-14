# AgentKGV: Agentic LLM-RAG Framework with Two-Stage Training for the Fact Verification of Knowledge Graphs

## Spotlight（今日速读）
这篇论文把“LLM 查事实”中的高误报问题切入到“agentic 检索策略 + 两阶段训练”层面，重点解决工业场景下图谱问答里低效检索与复杂表述匹配导致的验证失败。

## 论文标题
AgentKGV: Agentic LLM-RAG Framework with Two-Stage Training for the Fact Verification of Knowledge Graphs

## 作者/机构
- 作者：Yumin Heo, Hyeon-gu Lee, Sumin Seo, Youngjoong Ko
- 机构：未在 arXiv 结构化元数据中给出，需结合论文 PDF/项目页确认

## 发布日期
2026-07-10（v1，arXiv）

## 主题标签
#LLM #Agent #RAG #KnowledgeGraph #FactVerification

## 论文链接
https://arxiv.org/abs/2607.09092

## PDF 链接
https://arxiv.org/pdf/2607.09092v1

## 项目/代码/数据链接（如可得）
- 论文摘要未直接给出公开代码仓库链接；当前阶段可先记录为“待补充”。

## 核心问题
知识图谱自动构建后会带入大量噪声与提取失真。传统 single-turn RAG 在图谱问答里常遇到表述表层差异导致检索失败。论文核心问题是：如何通过 agentic 路由和迭代查询重写，提高工业级规模下的可复用验证效果与成本效率？

## 方法概要
- 构建 Agentic LLM-RAG 框架，核心在于动态路由和查询重写，适应文档级检索的表述错配。
- 提出两阶段训练：
  - 第一阶段：基于 teacher-student 的蒸馏 SFT，压缩大模型推理能力到小模型，稳定查询重写与推理过程；
  - 第二阶段：采用 trajectory-level GRPO，优化搜索策略，降低无效检索调用。
- 在公开 T-REx 长尾谓词分割上进行对比评估。

## 主要贡献
- 将 agentic routing 与两阶段训练明确绑定到 KG fact verification 任务，给出可落地的成本控制路径。
- 把“检索质量提升”与“推理质量提升”拆解为两个互补阶段，兼顾精度和查询次数。
- 提供面向工业部署场景的指标思路，强调在规模化条件下的代价/收益平衡。

## 关键实验或结果
- 在 open-domain T-REx 长尾谓词上，macro-F1 相比 single-turn RAG 提升 5.5 个百分点；加入两阶段训练后再提升 9.4 个百分点。
- GRPO 阶段平均检索调用从 3.24 次降到 1.63 次（不损失精度），对在线服务开销友好。
- 论文给出的设定强调该框架在“噪声文本 + 表面形态错配”条件下更稳定。

## 适合关注的原因
它不是只做模型架构优化，而是把“agentic 行为策略”直接对齐到工业可执行成本，和企业级知识问答、法务自动审查、知识抽取平台的实际链路高度贴合。

## 局限性或待验证点
- 缺乏多个知识图谱领域（如金融、医疗）的跨域比较。
- 训练与评测主要围绕单一开源 benchmark；真实公司知识库的语言异质性未完全覆盖。
- 代码和数据版本是否可复现尚需官方仓库确认。

## 对后续研究/应用的启发
- 可用于重构企业内部 fact-check 系统，把“检索重写策略”独立为可更新策略模块。
- 与图结构检索结合时，可进一步加入 schema-aware constraint，减少语义漂移。
- 对后续 agentic RAG 的工程化路线提供模板：先稳定查询理解，再通过轨迹优化控制预算。

## 一句话总结
这篇工作把 KG 验证中的关键瓶颈从“模型本身会不会算”转成“agent 能不能更聪明地问、问几次、何时停”。

## 标准化研究框架
- **Research question：** 在知识图谱事实验证场景中，agentic 检索与双阶段训练是否能同时提升正确率并降低无效查询成本？
- **Literature：** 现有 LLM-RAG 研究多聚焦单次检索；本工作在检索策略学习和轨迹优化之间引入衔接，贴近 industrial retrieval QA 文献中的 cost-aware 方向。
- **Theory：** 非社会科学语境可理解为“分层决策过程”：先学习稳定策略映射，再用强化策略在检索路径上做成本约束优化。
- **Hypotheses：** H1：双阶段训练优于单阶段 SFT；H2：轨迹级优化可显著降低检索调用数；H3：长尾谓词上改进最显著。
- **Method：** 采用基线 single-turn RAG 与 AgentKGV 的对比实验，采集 macro-F1 与平均检索次数。
- **Data and Analysis：** 使用 open-domain T-REx 长尾谓词切分；通过消融分析分离两阶段贡献并统计检索轨迹分布。
- **Findings：** 两阶段设置显著改善 F1，并降低平均检索次数，表明 query rewriting 与 trajectory optimization 互补。
- **Conclusion：** 对图谱事实验证而言，检索控制策略是可持续性能增益的重要杠杆；若有开源版本，对工业落地价值高。

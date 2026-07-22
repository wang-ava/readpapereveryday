# BioSecBench-Surveillance: A Verifiable Benchmark for AI Agents in Pathogen Genomic Surveillance

Spotlight：这篇 AI4S 论文不只给结果榜单，而是把“AI 代理是否能在真实生物安全语境下做正确的分析决策”定义成可验证任务，强调可解释执行链和阈值/归一化等细节决策。

- 论文标题：BioSecBench-Surveillance: A Verifiable Benchmark for AI Agents in Pathogen Genomic Surveillance
- 作者：Harmon Bhasin, Kevin Flyangolts, Dianzhuo Wang, Evan Seeyave, Arjun Banerjee, Amanda Darling, Joshua Stallings, David Stern, Shawn Higdon, Claire Duvallet, Bryan Tegomoh, Kenny Workman
- 机构：LatchBio；Aclid（可由 LatchBio PDF 说明页确认）
- 发布日期（版本）：2026-07-21
- 主题标签：#AI4S #Genomics #AgentBenchmark #Biosecurity #Tool-Augmented Agents
- 论文链接：https://arxiv.org/abs/2607.19262v1
- PDF 链接：https://arxiv.org/pdf/2607.19262v1
- 项目/代码/数据链接：
  - Manuscript：https://latch.bio/biosecbench-surveillance
  - Leaderboard / benchmark 家族：https://benchmarks.bio
  - 相关项目博客：https://blog.latch.bio/p/benchmarking-ai-agents-on-pathogen

## 核心问题
现有病原体基因组监测的瓶颈正在从数据采集转向“分析决策”能力：AI 代理是否能正确选择分析流程、工具、参考数据库与阈值，而不只是“能运行某条命令”。

## 方法概要
- 构建 100 个评估场景（7 类任务、6 类样本类型、短/长/混合测序）；
- 每个任务给出原始或近原始测序数据与监测上下文；
- 代理需自动选择正确流程并输出结构化决策；
- 使用确定性评分器进行是否“正确答案”判定；
- 覆盖 taxonomy、AMR、source tracking、anomaly、genetic-engineering detection 等关键场景。

## 主要贡献
- 提供可执行层面的监督 benchmark，而非静态问答题；
- 聚焦于真实生信工作流中的决策链（工具选择、阈值设定、归一化策略）；
- 给出跨模型/框架的基准结果，暴露“执行正确但决策不当”的主要失败来源。

## 关键实验或结果
该任务集共 100 个评估，覆盖 3,962 次可评分尝试；16 个模型-执行器组合中，最优配置（Opus 4.8/PI 与 GPT-5.5/Codex）pass rate 约 50.2%（约半数通过），多数任务仍有大量错误主要来自参数和阈值选择。

## 适合关注的原因
它把 AI4S 里最脆弱的一层——“分析决策正确性”——量化出来，直接对应生物安全、公共卫生和应急响应中的现实风险。

## 局限性或待验证点
- 公开版本覆盖仍有更新空间（任务分布、工具生态、最新模型接口）；
- 部分场景下拒答策略与误报/漏报权衡仍未被统一业务规则统一；
- 大规模联邦部署中的隐私与数据主权约束需要额外评估。

## 对后续研究/应用的启发
可作为 agent evaluation 的模板：在任何高风险科学 workflow 中，都应增加“流程决策正确性”评测维度，而非只看最终数值输出。

## 一句 Obsidian 快速浏览总结
一句话：BioSecBench-Surveillance 的核心价值是把“会跑”变成“跑对流程并做对阈值决策”的可验证标准。

## 标准化研究框架
- **Research question：** 在病原基因组监测任务中，AI 代理是否能持续做出正确的分析流程决策并达到可用于应急决策的可靠性？
- **Literature：** 对比 SWE-bench 和近年生物/科学工作流代理基准，补齐了 pathogen surveillance 的决策执行层评测。
- **Theory：** 代理能力不止于问答正确性，而是一个结构化决策问题：流程选择+参数设置+解释性输出。
- **Hypotheses：** 若评测采用可执行任务与确定性评分，能清楚分离“能调用工具”与“会做科学判断”的能力差异。
- **Method：** 设计 100 项任务卡，提供输入快照，运行多模型/执行器组合，统一评分器统计 pass/refuse/wrong。
- **Data and Analysis：** 统计任务类别、读长类型、拒答率与各分组得分，分析失败来源是否集中于中间决策参数。
- **Findings：** 实证显示即便最强配置 pass rate 约 50%，错误主要来自阈值、过滤与归一化策略，说明“执行动作”并不等于“科学判断正确”。
- **Conclusion：** 在本类非社会科学研究中，该字段可对应“安全-critical科学系统中的可验证决策链”检验：不仅要问答正确，还要检验每个决策环节是否可复现。

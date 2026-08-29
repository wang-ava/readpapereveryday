# PromptResponse: Optimizing Prompts for LLM Coding Tasks

该研究聚焦“同一任务不同 prompt 形式”的影响，结论是低成本的格式标准化可带来显著收益，而盲目做 LLM 调参并不总是更好。

## 论文标题
PromptResponse: Optimizing Prompts for LLM Coding Tasks

## 作者/机构
- 作者：Erik Thureck；Robert Kühnen；Tim Jacobowitz
- 机构：arXiv 摘要页未披露统一机构字段。

## 发布日期/版本日期
- 提交日期：2026-08-21 13:16:48 UTC
- 版本：v1

## 主题标签
#LLM #Coding #PromptEngineering #AgentWorkflow #HumanEval

## 论文链接
- https://arxiv.org/abs/2608.21074v1

## PDF 链接
- https://arxiv.org/pdf/2608.21074v1.pdf

## 项目/代码/数据链接（如可得）
- 代码/数据：摘要页仅说明发布了 dataset variants 与 evaluation pipeline，未给出直接 URL；需进一步从仓库页面补充。

## 核心问题
LLM 的代码生成性能对提示词格式和调参方式高度敏感，现有实践常误以为复杂优化一定更优。

## 方法概要
- 在 HumanEval 上构造五类语义等价提示：baseline、JSON、Markdown、YAML、LLM-tuned。
- 在 8200 次执行上比较生成性能、效率和稳定性。
- 分析提示词结构对错误类型与可执行性差异的影响。

## 主要贡献
1. 用同语义不同格式的实验设置，隔离了“格式”变量对代码输出的影响。
2. 在规模较大执行量上证明输出稳定性可由格式标准化显著改善。
3. 发现 LLM-tuned 提示并不天然优于规范化格式，反而可能降低性能。

## 关键实验或结果
- JSON 格式在效率与句法稳定性上表现突出。
- LLM-tuned 版本任务性能反而出现显著下降（相对其他格式）。
- 8200 次执行提供了较强统计稳定性。

## 适合关注的原因
- 对研发/研究团队直接可行：不一定要大规模优化器改造，通过工程化提示标准就可获得收益。

## 局限性或待验证点
- 实验主要基于 HumanEval，任务泛化到真实软件仓库尚待验证。
- 多模型、多语言与复杂交互式编码任务覆盖不足。
- 缺少公开资源链接降低复现可及性。

## 对后续研究/应用的启发
- 可把提示模板标准化纳入 agent coding workflow 的“基础设施约束”，减少结果波动。
- 建议将 prompt 格式设计与回归测试（失败率、重试率、超时率）共同优化。

## 适合 Obsidian 快速浏览的中文总结
在代码任务里，格式化提示（如 JSON）常比复杂调参更稳定；这个方向对工程收益高、成本低。

## 标准化研究框架
**Research question：** 在代码生成任务中，提示词格式化是否比复杂 prompt-tuning 更能持续提升性能与稳定性？

**Literature：** 现有提示工程文献强调模板创新，但很少在同语义等价提示上做大规模工程对比；本研究强调格式一致性这一被忽视维度。

**Theory：** 若模型对语法结构高度敏感，则可执行性与稳定性首先受“可解析化输入”影响，过度语义优化可能引入噪声。

**Hypotheses：** 1）规范格式（如 JSON）提升效率与稳定性；2）LLM-tuned 提示并不必然提升整体质量；3）输出改进可在大规模执行量上稳定复现。

**Method：** 构建语义等价五类 prompt 变体；在同规模 HumanEval 运行下比较成功率、效率、稳定性与错误分布。

**Data and Analysis：** 以 8200 次执行日志为主体进行量化对比，统计性能与稳定性指标，并对不同格式间做显著性分析。

**Findings：** JSON 与标准化格式在实验中最优，LLM 调参提示反而并未带来普适收益。

**Conclusion：** 对面向落地的 LLM coding agent，提示词工程中的标准化格式比“更复杂优化”更实用，值得优先纳入流水线。

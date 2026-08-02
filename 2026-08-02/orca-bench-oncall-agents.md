# ORCA-bench: How Ready Are Language Model Agents for Oncall?

Spotlight：`ORCA-bench` 把 oncall 事故的根因分析场景直接还原为带源码和真实可观测数据的工程任务，以任务复杂度、检测延迟和并发故障三维控制难度，给 LLM Agent 在生产场景的可靠性提供了前所未有的近真实验台。

- 论文标题：ORCA-bench: How Ready Are Language Model Agents for Oncall?
- 作者：Albert Gong, Kyuseong Choi, Abhineet Agarwal, Jason Schechner, Ryan Huang, Raj Agrawal, Anish Agarwal, Raaz Dwivedi
- 机构（如可得）：arXiv 元信息未直接披露机构
- 发布时间：2026-07-30（v1）
- 主题标签：`#LLM` `#Agent` `#Oncall` `#RCA` `#Evaluation` `#Reliability`
- 论文链接：[https://arxiv.org/abs/2607.28545v1](https://arxiv.org/abs/2607.28545v1)
- PDF 链接：[https://arxiv.org/pdf/2607.28545v1](https://arxiv.org/pdf/2607.28545v1)
- 项目/代码/数据链接：公开数据集合集位于 `https://hub.harborframework.com/datasets/orca-bench/ORCA-bench`

## 核心问题
当前 LLM Agent 常在理想化 coding benchmark 表现良好，但在真实 oncall 根因分析中面对噪声化指标、日志、链路追踪和源代码交叉上下文是否仍可工作？如果不加工程约束，如何避免“看起来会修 bug、实际不能救火”。

## 方法概要
研究团队构建了一个真实监控接口驱动的微服务环境（Prometheus / Jaeger / OpenSearch），并提供 50GB 的六日运行数据与 1,079 个 RCA 任务。任务覆盖报告细节不完整、故障共现、检测时延等因素。实验采用真实的 frontier coding agents 在“报告->日志检索->代码定位->推断根因->输出处理建议”流程中运行，并加入 source-code access 与无源码对照组。

## 主要贡献
- 首次在统一框架里定义了更贴近生产 SRE 的 oncall Agent benchmark。
- 任务设计系统化：覆盖报告模糊度、共现故障和时序偏移等工程痛点。
- 提供可复用的公开测试集与评测协议，并报告高质量人类重标的 LLM-as-judge 一致性（Cohen's kappa 0.90）。

## 关键实验或结果
- 五个 frontier agent 在 Medium 难度下的最佳 RCA Accuracy 为 25.3%，Hard 难度仅 10.0%。
- 去掉源码访问后，模型几乎在所有指标上显著下滑。
- 最弱模型在 40% 报警输入下输出了“看似合理但不成立”的根因，暴露出可信度风险。

## 适合关注的原因
该工作直接触及“AI 在关键基础设施上生产可用性”的底线问题：不仅要会写代码，还要在时间压力、噪声、可观测性不足时稳健推理。对构建企业级 coding/ops agent 的工程团队来说，这是决定是否进入金丝雀放量的重要风险量化材料。

## 局限性或待验证点
- 数据规模与任务时长固定于 6 天测试窗口，未覆盖长期演进、容量扩缩容等更复杂运维工况。
- 目前仍是离线评测与限定任务流，没有覆盖多工程师协作与变更审批链路。
- 结果以 v1 为主，源码访问、告警策略细节在公开仓库需继续核验是否随时间更新。

## 对后续研究/应用的启发
- 可将 ORCA 作为 CI 的新型“生产级红线”：每次新 agent 上线先通过 oncall RCA 套件再进流水线。
- 推荐把本文 benchmark 与日志索引优化、故障演化建模和多模态可观测数据接入结合，逼近真实 24/7 运维复杂度。

## Obsidian 快速浏览总结
一句话：`ORCA-bench` 用一套可复现实验床把“LLM Agent 上线宣称”换成可度量的可复现根因分析指标。

## 标准化研究框架
- **Research question：** 在真实运维噪声与源码上下文受限环境下，LLM 代理是否具备可靠进行 root cause analysis 的能力？
- **Literature：** 继承了 LLM benchmark、software engineering agent、自动化运维（AIOps）评测方向，区别在于把 oncall 任务标准化为可公开复现的长时段微服务诊断套件。
- **Theory：** 以“可观测性完整性 + 任务约束严苛度”作为性能上界来源：缺少源码或观测会显著放大模型幻觉风险。
- **Hypotheses：** 若基准同时提供时序、日志、指标和源码，Agent 输出的可靠根因准确率应显著高于单一接口输入；同时可通过人类重标降低评估偏差。
- **Method：** 用 1,079 条人工审阅任务构建难度分层数据，统一模型调用窗口与响应要求，并对比五类 frontier agents 与/no-code 变体。
- **Data and Analysis：** 样本按难度分层统计 RCA Accuracy，并记录幻觉率、报告完整度与跨组指标；评估结果以 `v1` 提交版本为主。
- **Findings：** 现实输入下 frontier agent 表现仍远低于安全生产要求，源码访问和人类协同评估是关键瓶颈与增益点。
- **Conclusion：** 对生产交付而言，oncall 自动化仍是高风险任务，`ORCA-bench` 提供了一个可以直接嵌入上线流程的评测下界，而非技术可用性“上界”。

# AgentRx: A Benchmark for Multimodal Clinical Forecasting with LLM Agents

AgentRx 把 AI4S 的重点从“单模型”移到“代理组织形态”，比较单代理与多代理框架在多模态临床预测中的真实收益。结论显示，多模态融合更关键，盲目并行化并不一定更强。  
这类结果对医疗、金融、能源等高风险领域很关键：在可解释性与稳定性要求很高的场景，系统级设计优先级往往高于模型规模。

- **论文标题**：AgentRx: A Benchmark for Multimodal Clinical Forecasting with LLM Agents  
- **作者/机构**：Baraa Al Jorf, Farah E. Shamout（机构信息在 OpenReview 页面未公开）  
- **发布日期/版本日期**：2026-06-11（v1）  
- **主题标签**：#AI4S #Healthcare #LLM #Agent #ClinicalForecasting #Multimodal  
- **论文链接**：<https://openreview.net/forum?id=wtI0bIBaAc>  
- **PDF 链接**：<https://openreview.net/pdf?id=wtI0bIBaAc>  
- **项目/代码/数据链接（如可得）**：未在摘要页面公开独立代码/数据。  

- **核心问题**：多模态临床预测常涉及结构化 EHR、影像和文本，单模型与多代理拆分各有优势，但缺乏统一基准验证两者真实表现差异。  
- **方法概要**：  
  1. 构建统一 benchmark，对 unimodal 与 multimodal 任务进行可比对照。  
  2. 设计 single-agent 与 multi-agent 两类 LLM 框架并统一评估口径。  
  3. 对 calibration、预测稳定性和多模态整合能力做系统比较。  
- **主要贡献**：  
  1. 首次以统一协议比较多模态临床场景下的单代理和多代理 LLM 策略。  
  2. 把 clinical forecasting 的实验设计从单模型评测扩展到代理架构层面。  
  3. 得出单代理在该任务更稳定、标定更可靠的经验性结论。  
- **关键实验或结果**：  
  - 在多个临床预测任务上，单代理框架持续优于多代理方案。  
  - 单代理在处理异构模态融合与 calibration 时更稳定。  
  - 结果提示多代理的协同收益在该设定下并不稳定。  
- **适合关注的原因**：  
  1. 为 AI4S 任务提供了“系统架构优先级”的实证依据。  
  2. 强化了多模态整合比复杂协作更关键的认识。  
  3. 对医疗风险控制场景有较直接借鉴意义。  
- **局限性或待验证点**：  
  1. 临床数据细节、跨机构泛化情况与隐私分布偏差在公开页上未充分展开。  
  2. 多代理方法的超参数敏感性分析不足。  
  3. 真实部署中的安全与可解释性评估仍需更细粒度。  
- **对后续研究/应用的启发**：  
  在 AI4S 中应优先验证“统一架构+统一输入处理”是否稳定，再考虑代理解耦，否则协同收益可能被复杂性抵消。  
- **Obsidian 快速浏览的一句总结**：AgentRx 表明在多模态临床 forecasting 场景里，“一个够稳健的单代理”往往优于过度拆分的多代理系统。  

## 标准化研究框架
- **Research question：** 在多模态临床 forecasting 中，单代理与多代理框架哪种结构更利于泛化、稳定性与标定质量？  
- **Literature：** 衔接 AI4S、临床预测与 agentic system 评估文献，但核心更偏向系统结构对泛化质量的实证检验。  
- **Theory：** 在工程上可理解为“架构复杂度与信息聚合的一致性权衡”，并非传统因果假设检验。  
- **Hypotheses：** 相较于多代理拆分，单代理在多模态融合和一致输出方面可能更易维持稳定校准。  
- **Method：** 构建统一任务集合，比较单代理与多代理 pipeline，在相同数据切分下统一计算性能与 calibration 指标。  
- **Data and Analysis：** 使用实时任务表现、联合模态输入效果、标定误差及鲁棒性指标做对比；分析任务类型与模型规模对两类架构差异的影响。  
- **Findings：** 基线结果支持单代理在多数任务上更优，尤其在 multimodal 融合与稳定输出方面。  
- **Conclusion：** 对非社会科学研究，本字段可等价理解为“模型架构与信息融合策略的系统对照实验”；结论对 AI4S 的工程部署更具指导性而非统计社会解释。  

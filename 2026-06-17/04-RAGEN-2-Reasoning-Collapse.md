# RAGEN-2: Reasoning Collapse in Agentic RL

RAGEN-2 关注了一个很实用但常被忽视的现象：LLM Agent 在 RL 训练中看起来“稳定”了，却可能因推理模板化而“只会套话”。论文把问题形式化为输入无关化塌缩，并给出可计算诊断与训练过滤策略。  
它的价值在于提醒我们，agent 的高稳定性不等于高泛化，反而可能掩盖了关键推理退化。

- **论文标题**：RAGEN-2: Reasoning Collapse in Agentic RL  
- **作者/机构**：Zihan Wang, Chi Gui, Xing Jin, Qineng Wang, Licheng Liu, Kangrui Wang, Shiqi Chen, Linjie Li, Zhengyuan Yang, Pingyue Zhang, Yiping Lu, Jiajun Wu, Li Fei-Fei, Lijuan Wang, Yejin Choi, Manling Li（机构信息在 OpenReview 页面未完整统一列出）  
- **发布日期/版本日期**：2026-06-03（v1）  
- **主题标签**：#Agent #LLM #ReinforcementLearning #ReasoningCollapse #PPO #GRPO  
- **论文链接**：<https://openreview.net/forum?id=qG5pDF2W5E>  
- **PDF 链接**：<https://openreview.net/pdf?id=qG5pDF2W5E>  
- **项目/代码/数据链接（如可得）**：公开页面未提供。  

- **核心问题**：多轮 LLM agent 的 RL 训练常出现“稳定但泛化差”的现象，现有只看熵（entropy）的指标无法识别“模板化却与输入无关”的坍缩行为。  
- **方法概要**：  
  1. 提出 two-axis 视角（输出多样性 + 输入依赖性）解释推理坍缩。  
  2. 用互信息 proxy（MI proxy）在线估计输入依赖程度。  
  3. 用信息论机制解释：当 reward 方差低时，task signal 弱化，模型易被输入无关正则主导。  
  4. 用 SNR-aware filtering 过滤低方差提示，优先训练高信息密度样本。  
- **主要贡献**：  
  1. 明确区分“表面稳定但语义泛化差”的推理坍缩，丰富 agent RL 诊断工具。  
  2. 给出 MI proxy 与 MI-based 监测指标。  
  3. 提供 SNR-Aware Filtering 训练策略，减少模板漂移。  
- **关键实验或结果**：  
  - 在 planning、数学推理、web navigation、code execution 等任务上，RAGEN-2 提升输入依赖性与任务表现。  
  - 在公开实验中，避免低方差模板批次可明显减轻 prompt-agnostic collapse。  
- **适合关注的原因**：  
  1. 为 agentic RL 的训练监控提供可计算的新指标，能直接集成到现有 pipeline。  
  2. 聚焦“看起来像进步但实则退化”的幻觉风险，契合生产环境安全需求。  
  3. 对多任务训练中动态 sample 策略设计具有直接指导价值。  
- **局限性或待验证点**：  
  1. MI proxy 在不同任务规模和分布下的数值稳定性还有待更大规模复现。  
  2. 论文对长时依赖、跨模态（如图文）场景中的推广讨论较少。  
  3. 计算开销与过滤策略阈值敏感性有待公开对比。  
- **对后续研究/应用的启发**：  
  可用于在线训练监控面板，将熵指标扩展为“输入条件敏感性”指标，避免模型仅在表面上变得更一致。  
- **Obsidian 快速浏览的一句总结**：RAGEN-2 揭示并修复了 agent RL 中的“高熵=高质量”误判，提醒我们训练稳定性要以输入依赖性为核心。  

## 标准化研究框架
- **Research question：** 如何区分“稳定但有效”与“稳定但模板化”的 LLM 代理行为，并抑制后者？  
- **Literature：** 结合 LLM agent、策略梯度（PPO/GRPO）与现有探索-开发不平衡讨论，补充了“推理依赖性”诊断维度。  
- **Theory：** 使用 mutual information proxy 表征输入与行为之间的信息通路，提出低 SNR 时出现正则主导与模板坍缩。  
- **Hypotheses：** 若在训练中优先保留高 reward 方差样本，模型将维持更高输入依赖性并提升跨任务泛化。  
- **Method：** 构建多任务评测，持续计算 MI proxy，并用 SNR-aware filtering 采样与更新。  
- **Data and Analysis：** 在 planning、数学、web navigation、code execution 四类任务上统计 MI 变化与下游性能，并对照不做过滤的 baseline。  
- **Findings：** 在多任务评测上，方法提升了可解释的输入敏感性，降低了 prompt 级别的坍缩趋势。  
- **Conclusion：** 对非社会科学研究而言，这一框架等价于“训练过程可解释性与泛化健康度联合约束”；核心不是假设检验，而是把错误稳定性形式化为可控偏差。  

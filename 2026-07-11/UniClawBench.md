# UniClawBench: A Universal Benchmark for Proactive Agents on Real-World Tasks

## Spotlight（今日速读）
这篇论文聚焦“真实世界可执行智能体评测”长期空缺的短板：评测往往停留在沙盒静态场景、单轮任务，导致模型能力和框架设计的区别被掩盖。UniClawBench 以主动式智能体（proactive agents）为目标，搭建“任务-能力-行为轨迹”三位一体的评测框架，能更直接检验真实工具协同能力。

## 论文标题
UniClawBench: A Universal Benchmark for Proactive Agents on Real-World Tasks

## 作者/机构
- 作者：Zhekai Chen, Chengqi Duan, Kaiyue Sun, Bohao Li, Yuqing Wang, Manyuan Zhang, Xihui Liu
- 机构：arXiv 元数据中未给出完整机构列表；项目托管组织与机构信息可在 [项目页](https://uniclawbench.github.io) 中补充核验

## 发布时间
2026-07-09（版本号：v1）

## 主题标签
#Agent #Benchmark #Proactive-AI #Evaluation #Multimodal-LLM

## 论文链接
https://arxiv.org/abs/2607.08768v1

## PDF 链接
https://arxiv.org/pdf/2607.08768v1

## 项目/代码/数据链接
- 项目页：https://uniclawbench.github.io
- 代码仓库：https://github.com/HKU-MMLab/UniClawBench

## 核心问题
现有智能体 benchmark 常把多个能力混杂为单一任务、只考察一轮交互或静态评测，导致无法区分“底层模型能力”与“agent 框架设计”导致的表现差异。如何构建能刻画真实交互过程、并可诊断失败来源的主动智能体评测体系？

## 方法概要
论文提出了一个按能力维度构建的 benchmark：
- 以五项基础能力为主线：技能调用（Skill Usage）、探索（Exploration）、长上下文推理（Long-Context Reasoning）、多模态理解（Multimodal Understanding）、跨平台协同（Cross-Platform Coordination）。
- 构建 400 个中文/英文真实任务。
- 引入执行器 agent + 隐式监督 agent + 用户 agent 的闭环评测框架，在活跃容器中逐步验证任务里程碑。
- 同时对“模型本身”和“agent 框架”进行交叉评测，便于剥离来源差异。

## 主要贡献
- 首个围绕 proactive agents 的能力驱动 benchmark 设计。
- 在任务层面引入可诊断的多能力拆分，避免能力混淆。
- 提供动态交互式多轮执行评估范式，接近真实使用场景。
- 开源公开 400 任务和评测代码，提升可复现性。

## 关键实验或结果
论文报告了多模型、多框架交叉对比，显示智能体表现差异主要来自：
- 模型基础能力与评测任务类型的耦合关系
- 智能体框架设计（任务编排、反馈处理、工具调用策略）对长任务成功率的放大影响
- 在多轮交互与动态反馈场景下，许多模型在“单轮指标”上的优势会显著下降

## 适合关注的原因
这是当前“AI agent 落地评测”难题中非常关键的一次系统化工作：当研究和产品都开始从 Chat 风格问答走向执行型系统时，评测方法是否科学更直接决定工程方向。

## 局限性或待验证点
- 400 任务虽多，但主要聚焦英文/中文 Web 工具链环境，迁移到企业私有系统是否仍然适配仍需验证。
- 框架设计与执行器能力绑定较强，任务细节对不同系统生态的敏感度需进一步评估。
- 对安全边界与对抗交互行为的覆盖仍需更系统设计。

## 对后续研究/应用的启发
- Agent benchmark 可从“单模型榜单”转向“能力维度 + 框架策略分离”评估。
- 对 agent 平台方，闭环评测可直接用于回归测试；对研究方可作为开发 RL 训练信号。
- 建议未来将 benchmark 扩展到更长时长、受限权限和多代理协作场景。

## 标准化研究框架
- **Research question：** 如何定义并量化 proactive agents 在真实动态环境中的多能力协同能力？
- **Literature：** 在已有 sandbox benchmark 与工具调用评测基础上，当前工作补充了多能力拆分与动态闭环评测。
- **Theory：** 对于非社会科学假设检验型研究，本字段定义为“基于任务-能力分解的性能建模假设”：可比性依赖于任务设计可控且可观测。
- **Hypotheses：** (1) 长期真实交互任务会暴露能力与框架的交互差异；(2) capability-driven 任务分层能提升错误归因准确率；(3) 动态反馈式评估更能反映部署价值。
- **Method：** 构建分层任务库 + 里程碑式自动判分流程 + 多模型/多框架组合实验。
- **Data and Analysis：** 400 bilingual 任务样本；比较 pass@1、阶段完成率、失败类型分布，并按五大能力聚合。
- **Findings：** 结果显示能力与框架设计共同决定端到端表现，且可通过闭环评测揭示单模型能力榜单无法解释的失效模式。
- **Conclusion：** 在 agent 评测中，模型能力榜单应与框架设计分析并列呈现；该 benchmark 可作为“真实世界智能体系统”的可复用验证基线。

一句话总结：这是一套把“做了没做完”变成可测量、可复现、可诊断指标的 proactive agent 基准化方案。

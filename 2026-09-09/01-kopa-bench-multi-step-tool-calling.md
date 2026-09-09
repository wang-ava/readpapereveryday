---
spotlight: "把多步工具调用从规则拼接变成可验证图结构，让开源 LLM Agent 在真实公开 API 上接近闭源模型水平。"
---

# Multi-Step Tool-Calling over Korean Open Public APIs: A Benchmark and a Data-Synthesis Recipe

## 基本信息
- **论文标题**：Multi-Step Tool-Calling over Korean Open Public APIs: A Benchmark and a Data-Synthesis Recipe
- **作者**：Dain Kim, Eungi Cho, Kyumin Kim, Shinyeong Noh, Kyuseong Lim
- **机构**：arXiv 元数据中未公开
- **发布日期 / 版本日期**：2026-09-04（v1）
- **主题标签**：`LLM` `Agent` `Tool-Calling` `Benchmark`
- **论文链接**：https://arxiv.org/abs/2609.05395
- **PDF 链接**：https://arxiv.org/pdf/2609.05395
- **项目/代码/数据链接**：未公开

## 核心问题
公开机构场景需要将多步骤工具链与实时 API 对接，但开源 LLM Agent 在多步任务上的可复用基准不足。如何构造覆盖真实 API 依赖关系的评测集，同时评估工具调用是否“能执行”和“能闭环”？

## 方法概要
- 提出 KOPA-Bench（Korean Open Public API Benchmark）：145 个真实多步任务。
- 设计 EDGE（Execution-grounded Dynamic Graph）数据合成：先执行 API 调用并构建可连边的动态图，再遍历验证通过的路径，合成可执行轨迹。
- 对现有模型进行 GRPO 微调，并比较不同规模模型在 KOPA-Bench 与 BFCL 上的性能。

## 主要贡献
- 首次在真实公开 API 生态下构建跨工具、跨步骤的韩语/韩国公共 API 工具调用基准。
- 提供基于“执行反馈”的数据合成思路，避免仅基于语义模板拼接导致的不可执行样本。
- 实验显示数据规模与质量可以显著抬升开源模型在真实工作流中的工具能力，不依赖超大参数单纯规模优势。

## 关键实验或结果
- KOPA-Bench 中 145 个任务用于评估多步工具调用。
- 9B 模型经 GRPO 后，效果接近未微调 27B 同源模型，且在 KOPA-Bench 与 BFCL 上均显著提升。
- 该结果支持“多步工具调用瓶颈主要来自可执行轨迹建模而非单步解码能力”这一判断。

## 适合关注的原因
它把“工具调用评测”从离线问答替换为可执行轨迹，贴近真实合规部署场景；对企业私有化 LLM Agent 的工程化落地价值高。

## 局限性或待验证点
- 目前任务与 API 生态与韩国公共接口更贴合，跨国家/跨语言泛化尚待验证。
- 评估主要聚焦工具链成功率与稳定性，对复杂安全约束（rate limit、隐私边界）覆盖仍有限。

## 对后续研究/应用的启发
- 可把“工具调用”评测从单回合对齐成多回合闭环任务。
- 结合企业内网 API（财务、工单、运维）可用同类方法快速建 benchmark，作为私有化模型上线前的一次性压力测试。

## 一句话中文速览总结
该工作通过“执行验证图”将多步工具调用基准拉到可落地场景，证明中小规模开源模型可在真实 API 环境中实现接近大模型的多步能力。

## 标准化研究框架
- **Research question：** 在真实公开 API 场景下，如何构造可执行的多步工具调用基准，并检验开源模型是否能通过连续执行而非单步回答显示鲁棒提升？
- **Literature：** 现有 Agent 评测多停留在静态 prompts 或有限任务组，缺少对“调用顺序可复用性”和“执行成功率”的高保真覆盖，尤其缺少来自真实 API 的可验证闭环样本。
- **Theory：** 将多步工具调用视作一条路径规划问题：每个工具调用节点只有在输入-输出兼容时才是可行状态转移，因而评估目标应强调路径可行性而非局部生成分数。
- **Hypotheses：**（1）使用执行反馈构建的数据比非执行验证样本更能逼真评估工具智能；（2）在同构模型中，执行驱动微调能显著缩小参数规模差距；（3）效果提升并非仅来自模型对同域语义记忆，而是对任务序列结构的学习。
- **Method：** 以真实 API 为动作节点构建动态图，采集可成功连接的边并采样为 KOPA-Bench；再用 GRPO 训练/微调模型并在基准上复算基线。
- **Data and Analysis：** 145 个公开任务；对比未微调与 GRPO 微调模型在 KOPA-Bench 与 BFCL 的成功率变化；重点观察多步链路的失败/中断类型。
- **Findings：** 9B 模型在 KOPA-Bench 可接近 27B 未微调水平，说明执行反馈数据和多步采样质量是实质瓶颈。
- **Conclusion：** 多步工具调用评测需“可执行性优先”而非仅看输出文本；该范式可复用到不同 API 生态并支持企业级 private-cloud agent 的实证标准。


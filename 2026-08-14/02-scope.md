# Learning When to Trust via Selective Context Preference Optimization

> Spotlight：这篇论文把“防止被误导”升级为“选择性信任”问题，给出了可执行的偏好优化框架，在公开模型上显著降低误导上下文导致的错误翻转。

- 论文标题：Learning When to Trust via Selective Context Preference Optimization
- 作者（机构）：Xian Sun, Wei Chow, Yingshuo Wang, Junhao Liu, Wei Gao, Qing Wu, Lingdong Kong；机构未在 arXiv 页面直接给出（可通过作者主页/机构主页进一步确认）
- 发布日期（版本日期）：2026-08-06（arXiv v1）
- 主题标签：`#LLM` `#Robustness` `#PreferenceOptimization` `#ContextReliability`
- 论文链接：[https://arxiv.org/abs/2608.06377](https://arxiv.org/abs/2608.06377)
- PDF 链接：[https://arxiv.org/pdf/2608.06377v1](https://arxiv.org/pdf/2608.06377v1)
- 项目/代码/数据链接（如可得）：Project Page [https://worldbench.github.io/scope](https://worldbench.github.io/scope)、GitHub [https://github.com/worldbench/SCOPE](https://github.com/worldbench/SCOPE)、HF Dataset [https://huggingface.co/datasets/worldbench/MIST-Bench](https://huggingface.co/datasets/worldbench/MIST-Bench)
- 核心问题：LLM 在接入外部提示/检索 context 时，如何避免“被误导上下文”翻转正确答案，同时不丢失“可置信上下文”下的准确性。
- 方法概要：论文提出 MIST benchmark，覆盖 clean / misleading / correct-context / irrelevant-context 四种配对条件；提出 SC2W 指标，度量误导上下文导致 clean-correct 的翻转率；进一步提出 SCOPE 训练策略，在 DPO 框架内对匹配的优劣偏好对进行均衡采样优化。
- 主要贡献：
  - 把鲁棒性定义为 selective trust，而非单一抗干扰目标。
  - 构建 4 框架成对评价集 MIST，提高 benchmark 的对照可比性。
  - 提出 SC2W 指标，更精准刻画“错误上下文翻转”风险。
  - 给出 SCOPE 训练法，在多模型上降低误导翻转同时保留对 clean/correct/irrelevant 条件下性能。
- 关键实验或结果：实验显示该方法能显著降低 SC2W，并在保持正常上下文准确率的同时提升抗误导表现，说明“只优化抵抗误导”并非最佳策略。
- 适合关注的原因：该问题已成为 RAG、agent 及多模态检索应用中的实际可靠性核心，结果可直接指导上下文过滤、指令跟随与安全策略设计。
- 局限性或待验证点：目前结果以 arXiv 初稿及公开模型评测为主；对不同任务类型（如代码、图像生成、工具调用）仍需更多场景验证。
- 对后续研究/应用的启发：可与动态检索置信度估计结合，构建“接受—忽略—再次确认”三段式上下文控制器；也可用于 RAG 的 runtime policy 与拒答策略。
- 适合 Obsidian 快速浏览的中文总结：Selective trust 不等于全盘拒答，SCOPE 用配对偏好优化把“抗误导”与“有效利用”同时拿下。

## 标准化研究框架

**Research question：** 在存在误导上下文时，如何训练模型在保留对有价值上下文的信任的同时，减少“好答案被误导翻转”？

**Literature：** 现有 robustness 研究常关注对抗扰动或噪声输入，但较少区分“误导信息”与“无关信息”两种 failure。该研究把评测目标从抗噪声泛化到了信任选择决策。

**Theory：** 模型决策可被视为在多条件上下文下的偏好排序问题：在 clean/correct 时应匹配用户意图，在 misleading 下应避免受错误条件支配。均衡采样可避免只会“更保守”导致的上下文弃用。

**Hypotheses：** 使用匹配的四条件偏好对进行优化，能同时降低 SC2W 且不降低 clean 与 irrelevant 条件下的 baseline 准确率。

**Method：** 通过 MIST 合成并人工注释问题对，定义 SC2W；采用标准 DPO 框架并对 clean-correct 与 misleading-wrong 样本对等重采样，在 open-source LLM 上训练/微调 SCOPE。

**Data and Analysis：** 样本按四条件配对组织，构造 matched preference triplets；比较训练前后在不同 context 条件下准确率与翻转率；辅以类别层（misleading source、领域）误差统计。

**Findings：** 在多公开模型中，SCOPE 对 SC2W 有稳定下降效果，同时保持了 clean/correct/irrelevant 条件下性能稳定，支持“选择性信任”比“盲目抗干扰”更有效。

**Conclusion：** 本文提供了可落地的可靠性建模路径：不要只训练模型“拒绝所有外部信号”，而是训练它“判断何时该信任”。这可直接用于 RAG 与 agent 的治理策略设计。

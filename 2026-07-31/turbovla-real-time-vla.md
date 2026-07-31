# TurboVLA: Real-Time Vision-Language-Action Model at 32 Hz on an RTX 4090 with <1 GB VRAM

Spotlight：TurboVLA 把“VLA=LLM 中心”这条默认路径反过来，直接学到视觉-语言到动作的轻量映射。结果是在同类任务上大幅降低显存和时延，接近“真实机器人可持续部署”级别。

- 论文标题：TurboVLA: Real-Time Vision-Language-Action Model at 32 Hz on an RTX 4090 with <1 GB VRAM
- 作者：Hengyi Xie, Chenfei Yao, Xianjin Wu, Xuanyang Xi, Yiping Tang, Di Xu, Yingying Zhu, Dingkang Liang, Xiang Bai, Han Ding
- 机构（如可得）：未在 arXiv 页面直接给出机构字段
- 发布日期或版本日期：2026-07-29T17:59:58Z（UTC），折合 Asia/Shanghai 为 2026-07-30 01:59:58
- 主题标签：#CV #VisionLanguageAction #EmbodiedAI #Efficiency #Robotics
- 论文链接：[https://arxiv.org/abs/2607.27205v1](https://arxiv.org/abs/2607.27205v1)
- PDF 链接：[https://arxiv.org/pdf/2607.27205v1](https://arxiv.org/pdf/2607.27205v1)
- 项目/代码/数据链接（如可得）：[https://github.com/H-EmbodVis/TurboVLA](https://github.com/H-EmbodVis/TurboVLA)

## 核心问题
- 现有 Vision-Language-Action 大多走 `V -> L -> A` 管线，推理时要频繁调用 LLM，导致延迟和显存成本高。
- 真实机器人任务（如 LIBERO）对实时性和部署成本敏感，现有模型成本偏高。
- 如何在保持任务效果的同时显著压低推理资源，是落地关键。

## 方法概要
- 提出 `V + L -> A` 直接映射替代传统 `V -> L -> A`。
- 独立编码视觉与语言，再通过轻量双向 cross-interaction 融合。
- 直接输出连续动作块，用 compact decoder 进行回归式控制。
- 采用任务条件表示，把视听信息与指令映射到当前策略内隐表征。

## 主要贡献
- 给出一个不依赖大模型中心化接口的 VLA 结构替代方案。
- 在资源约束下保持高成功率：仅 0.2B 参数。
- 显示实时控制可行性：32 Hz 推理与显存 <1GB，在单卡消费级显卡上部署。

## 关键实验或结果
- 在 LIBERO 上达到 97.7% average success。
- 推理延迟 31.2 ms，推理显存 0.9 GB（RTX 4090）。
- 在多个更大规模 VLA policy 中匹配或超过性能，表现出强效率优势。

## 适合关注的原因
- 这是一个对“真实机器人可部署性”影响极大的方向：不是追求更大参数，而是更合理的架构效率。
- 对需要低延迟和低成本部署的工业与消费级机器人应用具有直接参考价值。

## 局限性或待验证点
- 任务覆盖以当前 benchmark 为主，跨域泛化及复杂交互任务仍需验证。
- 架构优化可能对长时记忆依赖任务有潜在代价，需要对比更细时间尺度任务。
- 是否能兼容更高维度工具调用（多模态传感器扩展）需后续实验确认。

## 对后续研究/应用的启发
- 可作为 robot stack 中 action head 的轻量替代层，引入更细粒度动作分解。
- 与 VLM planner、工具调用模块分离设计，利于模型更新与推理预算调度。
- 工业化场景可直接对比 `V->L->A` 与 `V+L->A` 在算力/延迟/收益三角上的 trade-off。

## 一句 Obsidian 快速浏览总结
一句话：TurboVLA 用架构重排把 VLA 从“算力炫技”拉回“实时落地”，在效率优先场景显示了高价值。

## 标准化研究框架
- **Research question：** 能否在不依赖大型中间语言模型接口的前提下，实现高成功率、低延迟、低显存的 VLA 控制。
- **Literature：** 基于现有 VLA 与端到端机器人控制方法，本工作比较了 LLM-centric 与非 LLM-centric 的模型路径。
- **Theory：** 若在视觉与语言特征层面直接建模行为映射，可减少信息瓶颈与重复编码，从而改善效率-性能平衡。
- **Hypotheses：** 直接 `V + L -> A` 能在保持语义约束的同时显著压缩推理资源，不牺牲主要操作成功率。
- **Method：** 在统一 benchmark（如 LIBERO）下构建对照模型并比较 success、latency、VRAM、参数规模。
- **Data and Analysis：** 以任务成功率为主，联合推理时延与显存占用做多目标对比；分析不同模型规模下性能边际收益。
- **Findings：** 在 0.2B 参数设置下可达 97.7% 成功率、0.9GB 显存，显示资源-性能优势显著。
- **Conclusion：** 非 LLM-centric 结构是高效具身机器人控制的现实可行路径，并值得在更多任务域进行泛化检验。

# COMET: Contrastive Motion-Enhanced Temporal Reasoning for Video Multimodal Large Language Models

该工作针对 Video MLLM 的时序薄弱点，显式建模“外观-运动”与方向信息，显著提升动作和时序推理能力。

## 论文标题
COMET: Contrastive Motion-Enhanced Temporal Reasoning for Video Multimodal Large Language Models

## 作者/机构
- 作者：Chenghua Zhu；Zhaolu Kang；Qifan Shi；Siyan Wu；Kehan Jiang；Lei Wei；Lianyu Hu；Guangyuan Dong；Mingbo Yang；Rui Lu；Guibo Luo
- 机构：arXiv 摘要页未披露统一机构信息。

## 发布日期/版本日期
- 提交日期：2026-08-21 12:28:36 UTC
- 版本：v1

## 主题标签
#CV #VideoMLLM #TemporalReasoning #MotionModeling #Multimodal

## 论文链接
- https://arxiv.org/abs/2608.21030v1

## PDF 链接
- https://arxiv.org/pdf/2608.21030v1.pdf

## 项目/代码/数据链接（如可得）
- 代码/项目：未在摘要页给出。
- 数据：未在摘要页给出。

## 核心问题
当前 video MLLM 在动作与时间方向理解上仍弱：不仅有帧采样稀疏问题，也缺少完整的时序建模机制与方向敏感优化。

## 方法概要
- 引入 temporal motion branch：基于 Taylor frame differences 提取运动证据。
- 采用 temporal attention bias 将运动信息注入外观分支，实现外观-运动协同。
- 提出 temporal prior distillation + forward-reverse TC-GRPO：把时间顺序本身作为学习信号。

## 主要贡献
1. 给出可复用的“外观+运动+方向”三位一体时序建模思路。
2. 通过 contrastive 机制强化方向敏感，减少模型对静态帧纹理偏置。
3. 在 Qwen3-VL-8B 与 InternVL2.5-8B 上验证迁移性，说明方法具有一定模型无关性。

## 关键实验或结果
- 动作型任务（STAR、SSv2）平均提升 **4.9%**。
- 时序推理任务（NExT-QA、CLEVRER、LLaVA-178K）平均提升 **2.1%**（相对 BL-GRPO）。
- 静态感知任务（PerceptionTest）基本持平，说明提升主要集中在时间动态推理维度。

## 适合关注的原因
- 若你在做视频问答、动作理解或 VLA 前置视觉表征，这类“方向敏感 + 运动证据注入”路线可直接迁移。

## 局限性或待验证点
- 仍偏于离线 benchmark 验证，未给出延迟、显存、推理吞吐对比。
- 对极端短时动作和长时程多动作切换场景的稳健性待补充。
- 缺少公开项目代码不利于复现实验。

## 对后续研究/应用的启发
- 可与 embodied 模块对齐：先做“视觉运动语义化”，再交给策略/规划网络，减少动作轨迹误读。
- 方向敏感优化（forward/reverse）可迁移到其他时序模态任务（多传感器或图像到动作映射）。

## 适合 Obsidian 快速浏览的中文总结
COMET 用显式运动分支和方向敏感训练，让 video MLLM 在动作与时序推理上更稳，静态视觉能力不受明显损害。

## 标准化研究框架
**Research question：** 面向视频多模态语言模型，如何系统增强对动作方向与时间关系的建模能力，提升时序任务鲁棒性？

**Literature：** 现有视频多模态方法多关注视觉主干改进或注意力融合，本工作提出运动分支与方向反馈闭环，是对“时间信息被稀释”问题的针对性补充。

**Theory：** 时序推理错误常源于模型未显式区分帧间变化方向，若引入可导出的运动证据并将方向编码纳入目标函数，模型可减少静态特征主导偏置。

**Hypotheses：** 1）加入运动分支可提高动作识别与事件顺序推理；2）方向敏感 TC-GRPO 有助于跨模型泛化；3）静态任务性能可基本维持。

**Method：** 先构造 motion feature（Taylor frame 差分），再用 temporal attention bias 融合至 appearance stream；通过 contrastive 与前后向优化联合训练，对比多模型多个 benchmark。

**Data and Analysis：** 在 STAR、SSv2、NExT-QA、CLEVRER、LLaVA-178K、PerceptionTest 等基准上做增益比较，并观察多模型（Qwen3-VL-8B、InternVL2.5-8B）的一致性。

**Findings：** 论文显示动作与时序任务显著提升，且静态任务保持持平，支持“定向时序增强”有效且副作用可控的结论。

**Conclusion：** 在视频多模态任务里，加入显式运动与方向监督可作为高效改进路径，尤其适用于需精细时序判断的 downstream。

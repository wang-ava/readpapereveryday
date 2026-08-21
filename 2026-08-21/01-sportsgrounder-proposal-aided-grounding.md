# SportsGrounder: Proposal-Aided Interleaved Grounding for Dense Sports Video Reasoning

Spotlight：论文指出当前 LMM 在密集体育视频问答中容易依赖语言先验而忽略细粒度视觉证据，通过“候选提议+插值式 grounding”把定位与动作推理强耦合，显著改善遮挡、多角色同款外观下的细粒度辨识问题。对体育分析和长时序视频理解场景的鲁棒性评估具有直接启发。

## 论文信息
- 论文标题：SportsGrounder: Proposal-Aided Interleaved Grounding for Dense Sports Video Reasoning
- 作者（机构）：Yizhi Li, Jiawei Jiang, Guanhong Wang, Yingcai Wu, Gaoang Wang（论文页未公开机构归属）
- 发布日期：2026-08-08（v2）
- 主题标签：`#CV` `#VideoReasoning` `#VLM` `#Grounding`
- 论文链接：[https://arxiv.org/abs/2608.07932v2](https://arxiv.org/abs/2608.07932v2)
- PDF 链接：[https://arxiv.org/pdf/2608.07932v2](https://arxiv.org/pdf/2608.07932v2)
- 项目/代码/数据链接（如可得）：论文标注为 ACMMM 2026（DOI: [10.1145/3767308.3836263](https://doi.org/10.1145/3767308.3836263)）；未在 arXiv 页面看到公开代码/数据链接。

## 论文内容
- 核心问题：大规模体育视频问答中，模型在小目标、同款角色、球/球员外观高度同质且时序长的视频里，常将复杂视觉判断误归因为文本先验。
- 方法概要：使用开放词汇视觉专家生成领域引导的候选框，在每一时刻执行 Interleaved Grounding Fusion（IGF）将显式框坐标与隐式视觉语义与全局网格特征融合，维持时间对齐；同时用 Action-Aware Supervision（AAS）约束 hidden states，迫使模型学习真实动作轨迹，而非语言捷径；并结合 MPO 强化模型在“干扰性错误选项”上的分辨能力。
- 主要贡献：
  - 首次系统化“提议增强 + 插值式 grounding 融合”用于 dense sports VQA。  
  - 通过 AAS 将动作监督直接施加到表征层，减少答题过程中对文本模板的过拟合。  
  - 在 SoccerNet、FineSports 改造数据上验证框架泛化。
- 关键实验或结果：
  - 在新增的密集体育视频数据上，明显提升细粒度推理准确率并达到论文报告的 SOTA 水平（按文稿描述）。
- 适合关注的原因：
  - 体育视频存在强时空噪声和目标重识别难题，方法更接近真实工业视频分析流程，易落地到赛事解说、战术复盘、运动医学监测等应用。 
- 局限性或待验证点：
  - 结果主要报告在改造数据集；对新运动种类和不同摄影风格的迁移未给出系统横向对比。  
  - 仍依赖高质量候选提议器，长尾场景（遮挡严重、画面抖动）下表现需独立验证。 
- 对后续研究/应用的启发：
  - 可探索“提议质量自适应路由 + grounding 强化”的机制，把提议生成器、推理模型和时间对齐策略联动训练。 
  - 可用于多模态客服/监控视频等非体育密集场景。 
- Obsidian 快速浏览一句总结：**当动作与身份同质化很高时，给 LMM 一个“可见框架 + 时间可追踪的 grounding 约束”比单靠语言先验更稳定。**

## 标准化研究框架
**Research question：** 在密集且视觉线索稀缺的体育视频推理场景中，显式 grounding 与动作监督能否显著减少 LMM 对文本先验的依赖？

**Literature：** 现有多模态视频推理方法多偏重端到端 VQA 或动作分类，较少在长时序密集场景中强化逐帧空间约束。该论文补齐了“提议驱动 + 插值 grounding”路径。

**Theory：** 如果模型在关键决策点缺乏可靠空间证据，会将高熵动作状态映射到语言共现模式。显式提议和行为级正则化可作为偏置约束，提高决策可归因性。

**Hypotheses：**  
- H1：IGF 可提升跨帧目标定位一致性并减少错误框架切换。  
- H2：AAS 会显著提升模型对“文本诱导偏置”场景的抗干扰性。  
- H3：在高干扰稠密体育数据上，联合框架优于单独 grounding 或仅判别训练。 

**Method：** 构建开放词汇提议模块，采用 frame-level IGF 融合坐标/语义特征，使用 AAS 对隐藏状态做动作监督，最后用 MPO 进行偏好优化。

**Data and Analysis：** 以 SoccerNet 与 FineSports 派生的密集 VQA 数据为主要评测基准，比较 baseline 与本文方法在长时序、多实体、长遮挡样本上的准确率与稳定性。

**Findings：** 研究显示该框架在密集场景中获得更强细粒度推理能力与 SOTA 表现，且减少对语言捷径的依赖。

**Conclusion：** 该论文建议把时序 grounding 当作与 VLM backbone 同等核心的建模组件，不再把视觉理解完全交由文本驱动的注意力分配。

# 2026-08-07 AI 论文分享

> 今日选题聚焦一个共同问题：AI 系统不仅要“更强”，还要知道何时信任信息、如何忠实处理时序证据，以及怎样把结构先验变成可迁移的预测能力。以下均为 2026-08-06 发布的 arXiv v1，按推荐顺序排列。

## 推荐顺序

1. **[Learning When to Trust via Selective Context Preference Optimization](./scope-selective-trust.md)**  
   **Spotlight：** 与其训练 LLM 一概排斥外部上下文，SCOPE 把目标改成“选择性信任”：抵抗误导信息，同时保留从正确上下文获益的能力。MIST 的四种匹配条件和 SC2W 配对指标尤其值得借鉴。  
   [论文](https://arxiv.org/abs/2608.06377) · [PDF](https://arxiv.org/pdf/2608.06377) · [项目页](https://worldbench.github.io/scope/) · [代码](https://github.com/worldbench/SCOPE) · [数据](https://huggingface.co/datasets/worldbench/MIST-Bench)

2. **[$\omega$-0: A Latent Predictive World Action Model for Concurrent Humanoid Loco-Manipulation](./omega0-humanoid-loco-manipulation.md)**  
   **Spotlight：** $\omega$-0 不把行走与操作拆成两个流水线，而是在潜空间联合预测视觉未来与全身动作；配套 $\omega$-HOME 数据集覆盖 40 多小时真实家庭场景，是人形机器人 whole-body world-action model 的鲜明案例。  
   [论文](https://arxiv.org/abs/2608.06375) · [PDF](https://arxiv.org/pdf/2608.06375)

3. **[The Low Frequency Trap: Video Language Models Fail at Simple Event Bookkeeping](./low-frequency-trap-video-models.md)**  
   **Spotlight：** 论文用 2,190 个带可执行事件轨迹的视频证明：视频语言模型连简单事件计数都存在分阶段崩溃；增加采样帧可能提高最终答案准确率，却未必恢复真实事件序列。  
   [论文](https://arxiv.org/abs/2608.06361) · [PDF](https://arxiv.org/pdf/2608.06361)

4. **[BioM-JEPA: joint-embedding prediction of graph-connected gene blocks in single cells](./biom-jepa-single-cell.md)**  
   **Spotlight：** BioM-JEPA 将 JEPA 的预测单位从单基因改为由蛋白关联与共表达图定义的基因块，在单细胞任务上同时追求生物结构保持、扰动预测和计算效率。  
   [论文](https://arxiv.org/abs/2608.05928) · [PDF](https://arxiv.org/pdf/2608.05928) · [数值源数据](https://arxiv.org/src/2608.05928/anc)

## 阅读提示

- **首读 SCOPE**：其评测设计可迁移到 RAG、Agent memory 与个性化上下文。
- **再读 $\omega$-0**：关注“紧凑未来表征”取代视频重建是否真正提升控制泛化。
- **Low Frequency Trap** 适合做评测方法参考：不要只看 final answer，要审计 evidence trace。
- **BioM-JEPA** 适合 AI4S 读者：重点检验图先验、数据深度混杂与跨数据集泛化。


# MLT-Dedup: Efficient Large-Scale Online Video Deduplication via Multi-Level Representations and Spatial-Temporal Matching

MLT-Dedup 通过多级表示与时空匹配，在“候选检索—精匹配”双阶段中兼顾成本和精度，解决了大规模平台上的重复视频清理问题。

- **论文标题**：MLT-Dedup: Efficient Large-Scale Online Video Deduplication via Multi-Level Representations and Spatial-Temporal Matching
- **作者/机构**：David Yuchen Wang, Haoying Li, Hailun Xu, Wei Chee Yew, Zirui Zhu, Sanjay Saha, Hao Hei, Kanchan Sarkar, Kun Xu；TikTok Singapore / NUS / TikTok San Jose
- **发布日期/版本日期**：2026-06-10（arXiv:2606.12215）
- **主题标签**：#CV #VideoDedup #LargeScale #Systems
- **论文链接**：[https://arxiv.org/abs/2606.12215](https://arxiv.org/abs/2606.12215)
- **PDF 链接**：[https://arxiv.org/pdf/2606.12215.pdf](https://arxiv.org/pdf/2606.12215.pdf)
- **项目/代码/数据链接（如可得）**：论文承诺提供去重生态与实现方案（KDD ADS track）；当前公开摘要中未展示固定仓库链接
- **核心问题**：在线视频平台面对大量近似重复视频，重复检测既要高召回又要控制索引和延迟，传统方法在工程预算下难以同时满足。
- **方法概要**：
  1. 引入 Multi-Level Video Encoder（ML-VE）提取细粒度帧级和稀疏片段级嵌入；
  2. 稀疏嵌入用于快速候选检索，细粒度嵌入用于精确匹配；
  3. 提出 DiF-SiM 模块进行差分特征增强相似性计算；
  4. 依据匹配到的重复片段定位结果进行策略化去重决策。
- **主要贡献**：
  1. 将“候选检索-精匹配”分层设计系统化；
  2. 通过差分相似度定位时间片段，提升判重可解释性；
  3. 兼顾真实部署可扩展性（容量与效率双优化）。
- **关键实验或结果**：在真实平台规模测试下，90% 精度时重复率降低 91%，稀疏检索提升索引容量约 5 倍。
- **适合关注的原因**：
  1. 典型平台级数据问题，工程价值明确；
  2. 方法结构清晰，易与现有视频索引系统对接；
  3. 可复用于图像库去重、短视频编辑版本检测等近邻任务。
- **局限性或待验证点**：
  1. 去重标准阈值的业务敏感性（false positive）需结合具体平台策略；
  2. 对版权敏感内容场景的误检/漏检代价尚需联合业务实验评估；
  3. 论文未在所有公开基准上给出细粒度消融。
- **对后续研究/应用的启发**：可将 MLT-Dedup 思路迁移到数据湖/企业资产管理系统，形成“候选层 + 局部对齐 + 策略层”的分层去重流水线。
- **Obsidian 快速浏览一句总结**：MLT-Dedup 在“成本受限且规模巨大”的平台场景下，通过多级表示实现了高效可解释的在线去重。

## 标准化研究框架
- **Research question：** 在固定索引预算下如何最大化大规模平台的近似视频去重命中率并降低重复内容占用？
- **Literature：** 与长视频检索、近似匹配和内容去重研究相关，关注“分层索引 + 精排校验”策略。
- **Theory：** 粗粒度索引负责覆盖率，细粒度对齐负责精度，二者耦合可在给定预算下优化 FPR/FNR 的平衡。
- **Hypotheses：** 多层表示与差分时空匹配结合可比单一 embedding 更好地定位编辑后重复，降低在线重复率。
- **Method：** 构建 ML-VE 多级嵌入、候选检索策略与 DiF-SiM 精匹配模块，形成端到端去重决策流程。
- **Data and Analysis：** 在真实大规模在线平台数据上进行实验，比较 90% 精度下去重率与索引容量变化。
- **Findings：** 去重率和容量双提升，说明两层架构在工程场景具有可行性和可扩展性。
- **Conclusion：** 方法对平台级“去重=高命中+低成本”问题给出可验证方案，但需在不同平台对阈值和误检代价做专门校准。

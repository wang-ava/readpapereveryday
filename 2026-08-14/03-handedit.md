# HandEdit: A Unified Benchmark for Egocentric Human-to-Robot Dexterous Hand Image Editing

> Spotlight：HandEdit 用 200M 级别数据把“人手到机器人灵巧手”的视觉迁移问题正式转成规模化训练与评测任务，对 Embodied AI 的廉价数据闭环有现实价值。

- 论文标题：HandEdit: A Unified Benchmark for Egocentric Human-to-Robot Dexterous Hand Image Editing
- 作者（机构）：Zhenjie Yang, Xingyu Jiao, Guopeng Zhong, Shuzhe Yang, Shi Che, Chao Wu, Chenyu Jiang, Dongjie Zhang, Yideng Zhang, Zheng Zhang, Muyun Jiang, Haisheng Su, Shuang Jin, Donghang Zhang, Chao Yang, Li Chen, Hongyang Li, Zuxuan Wu, Yu-Gang Jiang, Xiaosong Jia, Junchi Yan；机构未在 arXiv 页面直接给出（可通过作者主页/机构主页进一步确认）
- 发布日期（版本日期）：2026-08-12（arXiv v1）
- 主题标签：`#EmbodiedAI` `#ImageEditing` `#Dataset` `#Benchmark`
- 论文链接：[https://arxiv.org/abs/2608.12122](https://arxiv.org/abs/2608.12122)
- PDF 链接：[https://arxiv.org/pdf/2608.12122v1](https://arxiv.org/pdf/2608.12122v1)
- 项目/代码/数据链接（如可得）：Project Page [https://handedit.github.io/](https://handedit.github.io/)；其余链接（如代码/数据）未在元数据中直接给出，待补充
- 核心问题：缺乏大规模、可扩展的人手到机器人手部映射数据集与统一评测协议，限制了 dexterous hand manipulation 的 scalable 学习路径。
- 方法概要：论文构建 HandEdit 数据集与基准，使用五个源视频库合成 2 亿条编辑实例，覆盖 26 套 URDF（13 只手-only + 13 手臂配置）；定义 Hand-only 与 Hand-Arm 两个评测 track，并加入 URDF 条件，结合通用相似度、VLM 打分与 embodiment-aware 指标做综合评价。
- 主要贡献：
  - 提供大规模 egocentric 具身编辑数据集（200M+）以支撑可扩展训练。
  - 将人体手臂/手部到机器人形态变换定义为统一 benchmark 任务。
  - 同时给出手部与手臂轨迹的双轨评测协议，便于方法横向对比。
- 关键实验或结果：作者在 11 个代表性图像编辑模型上做了系统评测，并用多维指标体系（泛化到形态、图像真实性与动作一致性）揭示当前方法的强项与短板。
- 适合关注的原因：该工作直接连接“人类动作数据可得性高”与“机器人灵巧手控制可训练性低”的矛盾，且评测框架可作为后续 Embodied Data Engine 的基础。
- 局限性或待验证点：公开信息不足以确认是否覆盖真实部署中的光照、遮挡与动力学反馈噪声；也未覆盖真实触觉反馈闭环场景。
- 对后续研究/应用的启发：可把 HandEdit 与动作回放/强化学习控制器联合，验证“视觉编辑结果到控制可行轨迹”的端到端转化可行性。
- 适合 Obsidian 快速浏览的中文总结：HandEdit 用超大规模 egocentric 数据把“类人手编辑”升级为可验证的机器人具身学习任务，值得关注其数据清洗与 URDF 条件迁移策略。

## 标准化研究框架

**Research question：** 能否通过大规模人类 egocentric 手部编辑数据建立可复用的机器人灵巧手映射 benchmark，从而降低 Embodied AI 数据采集成本？

**Literature：** Embodied 研究常受限于真实操控数据稀缺，本工作用图像编辑视角替代纯物理采集，补齐了“人类示教数据可规模化利用”的方法空白。

**Theory：** 通过视觉-几何-拓扑参数（URDF 条件）联合建模，可将不同机构构型统一到共享的编辑语义空间；大量同分布样本有助于模型学会形态不变/形态依赖特征。

**Hypotheses：** 统一 benchmark 会显著提升不同算法比较的可复现性，并通过多维指标发现仅凭传统视觉相似度不够的 embodiment 鲁棒性。

**Method：** 汇聚五个源数据集生成 200M+ 编辑实例；按手-only/hand-arm、URDF 条件分组；定义基础+LLM/VLM 语义+具身专用指标体系；评测 11 个 baseline。

**Data and Analysis：** 分析对象为 26 种 URDF 下的跨形态性能，观察各模型在不同任务轨迹与指标维度上的分布，重点关注泛化误差和形态条件偏置。

**Findings：** 基准结果显示当前图像编辑方法虽可在视觉层面产生高保真替换，但在结构一致性和具身兼容性上仍有明显差距，且不同 URDF 条件表现并不一致。

**Conclusion：** HandEdit 将具身图像编辑问题形式化为标准任务，强调数据规模与评测协议同等重要；后续可在真实控制回路中检验编辑-执行一致性闭环。

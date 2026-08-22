# ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models

ConceptGuard 试图把 unlearning 从“按事实删条目”扩展到“按概念删行为”，强调同一概念在安全与无害场景中的语境分离。对于已经进入高风险内容治理阶段的 LLM 产品，这篇论文的“去除概念而非孤立事实”的框架很关键。

## 论文标题
ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models

## 作者/机构
- 作者：Sahil Kale, Ian Harris（arXiv 仅披露作者姓名）
- 机构：arXiv 元数据未在作者名下直接给出机构，需进一步到论文 PDF/附录确认

## 发布日期/版本日期
2026-08-20（arXiv v1）

## 主题标签
#LLM #Safety #Unlearning #Benchmark #Evaluation

## 论文链接
- arXiv：https://arxiv.org/abs/2608.20338

## PDF 链接
- https://arxiv.org/pdf/2608.20338.pdf

## 项目/代码/数据链接
- 项目页：未公开
- 代码/模型：未公开
- 数据：论文声明“dataset is publicly available”（论文摘要中提及）；未给出直接下载链接，需检索项目主页或补充材料

## 核心问题
当前 LLM 反事实遗忘方法多在独立事实层面评测，难以衡量“危险概念”是否在语境中被有效清除。实际安全约束常要求：同一概念在有害语境中应被抑制，而在有益语境中仍应可用。本文问题是：如何构建可持续评估这类 context-sensitive unlearning 的基准与指标。

## 方法概要
- 提出 dual-use concepts：同一概念可在有害与良性场景中出现。
- 构造 ConceptGuard benchmark：将 forget/retain 集合设计为概念层面的互补集合。
- 评估指标不再只看事实级 recall，而关注语境分离能力与概念级消歧。
- 指标层面强调 context-sensitive、intent-sensitive 的对抗场景，考察模型在保持 benign utility 的同时对有害用法的消隐程度。

## 主要贡献
1. 从“事实集合”改到“概念集合”，定义更贴近安全治理落地场景的 unlearning 任务。
2. 提供一套可复用的 benchmark + 指标体系，将对抗语境作为核心评测单元。
3. 用实验揭示当前方法在概念级控制上的薄弱环节（尤其是跨语境一致性）。

## 关键实验或结果
- 在 ConceptGuard 任务上，现有主流 unlearning 方法表现不理想：
  - 语境分离能力弱
  - ROUGE 与概念级指标上普遍不足
  - 遗忘-效用权衡明显
  - 概念级控制一致性波动较大
- 实验说明仅在事实层面通过测试并不足以代表安全可用性。

## 适合关注的原因
该工作把“安全性”与“实用性”并列为第一类目标：不是简单删除知识，而是减少高风险行为扩散。对需要上线模型风控的团队（客服、编程助手、RAG 管线）尤其有直接参考价值。

## 局限性或待验证点
- 公开信息仍偏重摘要级别，尚缺乏更完整的任务定义细节、数据规模/来源全量描述、超参策略复现细节。
- benchmark 的覆盖是否能代表真实业务语境与攻击面、以及对多语言模型的泛化，仍需后续验证。

## 对后续研究/应用的启发
- 可将该框架移植到“政策合规、隐私泄露防护、版权合规问答”等场景，定义场景级互补集合。
- 可把 forget/retain 目标从“是否回答某事实”升级为“某概念在目标语义区域中的许可策略”。
- 提示未来 unlearning 应该配套 context-aware 监管指标，而不是单点 accuracy。

## 适合 Obsidian 快速浏览的中文总结
一句话：ConceptGuard 用“概念级 + 语境敏感”的视角重构 LLM 撤销学习评测，让安全治理更接近真实应用。 

## 标准化研究框架
**Research question：** 模型是否能在保留良性语境能力的同时，对同一 dual-use concept 在有害语境下实现稳定且可控的去除？

**Literature：** 该工作与传统 unlearning 及 safety benchmark 对话：传统研究多聚焦事实删除与静态 recall 指标，缺乏语境维度；ConceptGuard 将两类文献中的“危险知识控制”和“行为干预”思路融合。

**Theory：** 可视为受约束优化问题：
- 优化目标一：尽量降低有害语境下目标概念触发概率；
- 约束一：保留对正常语境的任务能力；
- 评价框架采用语境条件下的行为对比而非仅事实复述准确率。

**Hypotheses：** 如果基准从 fact-level 变为 concept-level 且加入语境对立集合，当前方法将暴露更明显的 context leakage，并能更区分“表面忘记”与“行为约束”是否有效。

**Method：** 通过对 dual-use 概念生成互补的 forget/retain 设计，构建受控评估任务；使用概念级指标比较不同 unlearning 技术在语境分离、鲁棒性、效用损失上的表现。

**Data and Analysis：** 数据为 ConceptGuard 提供的结构化测试集（含对应语境对）；指标侧重 context-sensitive 分离分数、ROUGE 与概念级得分；比较 baseline 与改进方法之间的相对表现并分析置信度/稳定性。

**Findings：** 论文显示现有方法在概念级语境控制上仍较弱，遗忘与效用之间存在显著折中，且不少方法在不同语境下不稳定。

**Conclusion：** 在安全治理场景中，“会记住但可控地不说”比“全盘遗忘”更符合产品可用性需求；未来应建立以语境约束为核心的统一评测协议。EOF

cat <<'EOF' > '2026-08-22/02-ai4ai-bench-rsi.md'
# AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement

AI4AI-Bench 首次把“agent 是否能改写训练算法”定义为可执行、可复现的 benchmark 任务，直接面向 recursive self-improvement 的核心瓶颈。论文的重要性不在于结论“能不能自举”，而在于把一个长期宏大问题落成可度量的任务协议。

## 论文标题
AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement

## 作者/机构
- 作者：Yizhe Chi, Wenyi Li, Deyao Hong, Xiaoqiu Wang, Mingju Gao, Kaisen Yang, Bingxiang He, Youjie Zheng, Calvin Xiao, Qinhuai Na
- 机构：arXiv 论文页未在元数据中直接标注机构信息

## 发布日期/版本日期
2026-08-20（arXiv v1）

## 主题标签
#Agent #LLM-Agent #AI4AI #Benchmark #Algorithmic-Design #RSI

## 论文链接
- arXiv：https://arxiv.org/abs/2608.20318

## PDF 链接
- https://arxiv.org/pdf/2608.20318.pdf

## 项目/代码/数据链接
- 项目/代码：arXiv 摘要提到 release task suite、evaluators 和 scoring submissions，但未提供直接公开链接（当前检索未抓到）。
- 数据：同上，属于 benchmark 公开评测产物，需到官方任务页确认

## 核心问题
是否存在一个可控的 benchmark 可以验证 LLM agent 是否真的在“修改模型训练算法”而非仅做参数调优或提示技巧上获得性能提升？

## 方法概要
- 构建10个固定研究仓库（10个训练算法族），形成10类算法改写任务。
- 每个任务给 agent 4 小时改写训练算法代码；系统重跑最多12 小时，和原始算法进行同条件对比。
- 使用固定评测器打分，并做任务归一化映射：0 表示无信息 baseline，0.1 表示原仓库算法，1.0 表示任务最优。
- 采集多系统、多配置（29×6）下的分数分布，并分析是否发生真正算法级修改。

## 主要贡献
1. 给 AI4AI 研究提供“改算法”而非“改数据/超参”的任务框架。
2. 提供可复用的评估协议与可重复测量机制，支持长期跟踪模型与环境更新。
3. 初次定量报告了当前 LLM agent 在 constrained 任务中进入算法改写区域的难度与收益边界。

## 关键实验或结果
- 10类任务上总体平均分数为 0.166，最优分数 0.250。
- 最强系统仅闭合原算法到最优距离的不足五分之一（< 0.25）。
- 仅少数提交会真正修改学习方式，但“有更多推理预算”可显著提高这类提交比例（由 8% 提升到 64%）。
- 更强推理带来的提升对应平均分 0.094→0.196；且能显著放大“真正改算法”路径。

## 适合关注的原因
这套 benchmark 把前沿议题“AI 是否可以改善 AI 研发流程”落到可执行任务，尤其适合评估 coding/实验室 agent 的真实工程价值，不易被“刷榜策略”或参数技巧轻易污染。

## 局限性或待验证点
- 评估预算（B300×4h / 12h）可能偏向特定算力与开发风格。
- 分数映射依赖任务定义，是否能泛化到更复杂训练环节（数据扩展、分布移位、长周期 curriculum）仍需验证。
- 公开代码与完整任务列表需进一步核验，当前版本未在 arXiv 抽取中完整呈现。

## 对后续研究/应用的启发
- 可用于公司内训：把“模型改进实验”转成 benchmark 化竞赛任务，量化 agent 的工程贡献。
- 可扩展到多模态、强化学习、数据管道优化等更高层级 RSI 子问题。
- 为政策制定方提供评测模板：区分“自动化实验执行能力”与“原创算法改写能力”。

## 适合 Obsidian 快速浏览的中文总结
一句话：AI4AI-Bench 的价值在于把算法设计改进变成可测任务，让 LLM agent 的递归改进能力从口号走向可复现证据。 

## 标准化研究框架
**Research question：** 在受限算力和同等评测条件下，LLM agent 能否通过改写训练算法显著提高目标模型性能，而非停留在数据/超参层级的替代性操作？

**Literature：** 连接两条线：一是 benchmark for LLM agents（常见是数据选择或提示调优），二是 AutoML/算法搜索（强调学习规则改写）。AI4AI-Bench 的差异是将后者嵌入 agent 闭环评测。

**Theory：** 若目标任务具有可重复 rerun 机制，则可将 agent 能力建模为策略函数 f(task_context, compute_budget)→code_delta，评价其对被评价性能函数 P 的提升；此时可分解“真改算法改进”与“旁路优化”两类行为。

**Hypotheses：** 若评价将代码重写与固定评测器绑定，且按 scenario 常量归一化，那么随机 baselines 或仅做超参调整的策略会被稀释，真正改算法行为比例与性能应随推理预算上升而增强。

**Method：** 通过 10 个冻结仓库的多任务采样，限制 agent 改写窗口并重跑训练，统一使用任务归一化评分。统计不同系统/配置的得分分布与是否改写成功的比例。

**Data and Analysis：** 主要数据为 29×6 配置结果、10 项任务 score 及提交提交行为分类。分析包含均值、最优值、分组差异（改算法与否）与预算敏感性（推理强度→成功率与score）。

**Findings：** 平均分不高（0.166）显示当前距离实质 RSI 仍远，改算法比例低；但推理预算提高后真正改算法的占比和分数显著上升，说明可控试验框架可激励深层优化。

**Conclusion：** 该研究表明，AI4AI 任务并非“不能做”，而是“能做但收益稀薄、代价高”；未来应将 benchmark 与更广泛算法族和长周期任务结合，以区分可迁移的真实进步与短期表演。EOF

cat <<'EOF' > '2026-08-22/03-bert-ler-ehr-explainable.md'
# Explainable Transformer Models for Clinical Prediction Tasks on Structured Electronic Health Records

这篇论文把结构化 EHR、实验室定量信息与可解释性绑在一起，强调“性能 + 解释一致性”双目标。对医疗 AI 而言，能够给出可核对风险因素归因的模型，通常比纯黑箱准确率更容易进入真实场景。

## 论文标题
Explainable Transformer Models for Clinical Prediction Tasks on Structured Electronic Health Records

## 作者/机构
- 作者：Jun Ni Du, Lukas Adamek, Maxim Kryukov, Flavio Dormont, Ziv Bar-Joseph, Sven Jager, Brandon Rufino
- 机构：arXiv 仅展示作者列表，机构信息未在 metadata 中直接给出

## 发布日期/版本日期
2026-08-20（arXiv v1）

## 主题标签
#Clinical-AI #EHR #Transformer #Explainable-AI #Healthcare

## 论文链接
- arXiv：https://arxiv.org/abs/2608.20315

## PDF 链接
- https://arxiv.org/pdf/2608.20315.pdf

## 项目/代码/数据链接
- 项目页：未公开
- 代码：未公开
- 数据：论文提到 EHRShot 与真实世界哮喘队列，用于实验复现实验；未给出公开下载链接

## 核心问题
如何在保留结构化 EHR 长序列建模能力的同时，对实验室数值信息进行保真建模，并让预测结果可解释到具体事件与输入 token？

## 方法概要
- 提出 BERT-LER：将实验室检验值从连续值转为分位桶离散化 token。
- 在 7500 万患者规模的匿名 EHR 数据上预训练与微调。
- 与预测任务联合，引入 Integrated Gradients 做 token 级归因，以医学事件路径解释输出。
- 在 EHRShot 公开基准与哮喘严重度进展任务上评估。

## 主要贡献
1. 兼顾量化实验室信息与可解释性，填补结构化 EHR 时间序列模型里“数值语义处理+归因一致性”协同不足。
2. 给出一个统一框架，可在同一模型上同时跑泛化性能与 attribution 一致性分析。
3. 在公开与真实-world场景中验证：实验室相关任务上表现竞争性，部分任务超过已发布模型。

## 关键实验或结果
- 在 EHRShot 与哮喘任务上，BERT-LER 与公开基线竞争，且在部分实验室相关子任务中更优。
- 归因结果与临床已知风险因素方向一致，表现出潜在可解释性可行性。
- 方法显示可在更多治疗领域与结构化 EHR 任务上迁移应用。

## 适合关注的原因
医疗场景对可解释性有监管与责任要求，这篇工作把“能做预后”延伸到“能解释为何这么做”，对可落地临床决策支持更直接。

## 局限性或待验证点
- 摘要层面未披露模型在不同人群（年龄、种族、医院系统）上的公平性评估。
- 依赖公开和真实数据的合并测试，跨域迁移仍需更细粒度验证。
- 7500 万患者级别语料优势明显，但复现路径、训练成本细节不足。

## 对后续研究/应用的启发
- 可推动以“归因稳定性”替代单点 AUC，形成临床模型验收标准。
- 可探索更多连续变量编码方式（非均匀分位、自适应编码）以及时间因果注意机制。
- 对 MLOps 而言，适合做持续学习中解释漂移监测。

## 适合 Obsidian 快速浏览的中文总结
一句话：BERT-LER 同时追求临床预测与可解释归因，让结构化 EHR 建模从“准不准”走向“准且能讲清”。 

## 标准化研究框架
**Research question：** 能否通过 BERT 风格结构化序列模型，在大规模 EHR 上同时提升预测精度并给出与临床知识一致的事件级归因？

**Literature：** 该方向连接传统 EHR 时序预测（MIMIC 等任务）与可解释 AI（Integrated Gradients、token attribution）两条线；先前工作常在一个任务上取舍准确率或解释性。

**Theory：** 将实验室定量值视为离散 token 后可融入 Transformer 的上下文建模；若 attribution 与输出相关且稳定，则可将“预测正确率”与“可解释性约束”联动为多目标优化目标。

**Hypotheses：** 在大规模预训练基础上，加入量化实验室 token 与 token-level attribution，不仅提升实验室相关子任务性能，还能提高归因与临床知识的一致性。

**Method：** 采用 BERT-LER 架构：连续值分位分箱、Transformer 编码、任务微调、Integrated Gradients。通过 EHRShot 与哮喘真实世界实验分别评估。

**Data and Analysis：** 样本来自论文自建 7500 万患者 de-identified EHR 语料与两类评测任务。指标包括预测性能及归因结果与已知风险因素对齐程度，重点对比实验室相关任务。

**Findings：** 方法达到与公开方法可竞争甚至优于的成绩，且归因可解释性表现出可接受一致性，支持“性能与解释共进”命题。

**Conclusion：** 在临床 AI 场景，单点性能不再足够，模型可迁移且具归因可核查性才是下一步落地前提；该框架为此提供了可复用模板。EOF

cat <<'EOF' > '2026-08-22/04-4danyone.md'
# 4DAnyone: Create Anyone in 4D from a Casual Monocular Video

4DAnyone 解决的是“单目随拍视频→稳定 4D 人体重建”的工程难题，并通过 context packing 与 routing 机制缓解扩展到多视图时的注意力瓶颈。对于 4D human reconstruction 与虚拟人应用，这篇工作可以直接转化为可用 pipeline。

## 论文标题
4DAnyone: Create Anyone in 4D from a Casual Monocular Video

## 作者/机构
- 作者：Yudong Jin, Tao Xie, Qihang Zhang, Zehong Shen, Zhen Xu, Yujun Shen, Hujun Bao, Xiaowei Zhou, Yinghao Xu
- 机构：arXiv 元数据未直接提供详细机构列表

## 发布日期/版本日期
2026-08-20（arXiv v1）

## 主题标签
#CV #4D-Reconstruction #Gaussian-Splatting #Diffusion #Multiview

## 论文链接
- arXiv：https://arxiv.org/abs/2608.20335

## PDF 链接
- https://arxiv.org/pdf/2608.20335.pdf

## 项目/代码/数据链接
- 项目页：https://4danyone.github.io
- 代码：https://github.com/ant-research/4DAnyone
- 数据：文中提到构建 MVGameHuman 数据集，并结合 light-stage 与 in-the-wild 视频；当前未检索到该数据集的直接下载入口

## 核心问题
从非标定、单目、自然场景视频重建可用的 4D 人体模型，关键困难在于：如何让生成的多视图视频足够一致、可重建并可支持后续 4DGS。

## 方法概要
- 生成重建级别的多视图一致视频（多目标视角）
- 分析现有 camera-controlled 视频扩散模型在大规模视角下的 bounded-attention-context 瓶颈：
  - reference-context 成本 O(N)
  - target-context 分组间信息割裂
- 提出 Reference Context Packing（RCP）：压缩 reference 视角为固定长度 mixed-resolution context，复杂度 O(1)
- 提出 Target Context Routing（TCR）：去噪阶段旋转目标分组，实现跨组信息交换
- 最终使用 4D Gaussian Splatting 完成 4D 输出

## 主要贡献
1. 识别并量化多视图视频生成的两类注意力瓶颈。
2. 提出可复用的 RCP 与 TCR 组合，显著改善大规模目标视角条件下的稳定性。
3. 引入 MVGameHuman 数据集并联合 in-the-wild 测试，验证方法泛化性。

## 关键实验或结果
- 在 DNA-Rendering 与 DyMVHumans 上，4DAnyone 在 novel-view 视频质量和 4DGS 下游重建上均优于前方法。
- 具备较好的 in-the-wild 泛化表现（未给出每项绝对分数）。
- 方法能减少视角分组导致的结构漂移，增强低噪声阶段稳定性。

## 适合关注的原因
该工作将“视频生成 + 3DGS + 多视图一致性”串成闭环，既有算法新意也有应用闭环（数字人、AR/VR、虚拟试衣/运动分析）场景，可直接观察其工程化价值。

## 局限性或待验证点
- 关键超参与训练细节未在摘要中完整展开。
- 对不同人物类型、极端遮挡与快速运动条件下鲁棒性尚待更大规模验证。
- 数据开源完整度（MVGameHuman 下载与处理脚本）未在摘要给出。

## 对后续研究/应用的启发
- RCP/TCR 可迁移到其他需要长序列多视图生成任务（机器人遥感、数字生物体重建）。
- 4DGS 与扩散模型耦合的工程范式值得在动作捕捉与轻量化消费端中复用。
- 有潜力演化为“单次拍摄建模”产品管线的核心模块。

## 适合 Obsidian 快速浏览的中文总结
一句话：4DAnyone 用注意力上下文重排和分组路由解决大规模多视图一致性瓶颈，把随拍视频到 4D 人体建模的门槛进一步降低。 

## 标准化研究框架
**Research question：** 在单目随意拍摄视频条件下，如何在不损失结构一致性的前提下稳定生成足够多视图的观测，以支持高质量 4D human reconstruction？

**Literature：** 结合了 video diffusion、multi-view synthesis、4D Gaussian Splatting 的研究脉络；此前方法在视角扩展时通常受上下文长度和跨组信息割裂困扰。

**Theory：** 可建模为上下文压缩与信息路由平衡问题：既要保留关键外观约束（reference side）又要在多组生成间传播全局结构约束（target side）。RCP/TCR 以近似不增加线性代价为代价，改写注意力信息流结构。

**Hypotheses：** 若 reference 上下文复杂度降为近似 O(1)，并让目标组在去噪时共享上下文，则可降低结构漂移并提升跨视角一致性与下游 4DGS 重建质量。

**Method：** 提出 4DAnyone pipeline：多视图视频重构模块 + RCP + TCR + 4DGS。实验在公开和野外数据组合上评估。

**Data and Analysis：** 使用 MVGameHuman、light-stage 与 in-the-wild 视频，分析 novel-view video quality 与 4DGS 重建指标，比较消融与基线。

**Findings：** RCP 与 TCR 在这两类指标上均优于基线；在更复杂环境下保持较强稳定性，支持方法对实景场景的泛化能力假设。

**Conclusion：** 论文表明扩散视图生成的关键不只“生成更清晰”，而是“保持跨组结构一致”；其机制设计为未来 4D reconstruction 工程化提供了可复制路线。EOF

cat <<'EOF' > '2026-08-22/05-scape-policy-eval.md'
# SCAPE: Scenario-Conditioned Simulation-Augmented Policy Evaluation

SCAPE 将仿真与真实世界评估从“平均性能”推进到“情景分层性能预测”，为部署安全性提供更细粒度的决策依据。它的价值在于把 policy evaluation 从单一分数改为可解释、可校准的不确定性估计框架。

## 论文标题
SCAPE: Scenario-Conditioned Simulation-Augmented Policy Evaluation

## 作者/机构
- 作者：Dijie Zhu, Seunghun Oh, Ruopeng Huang, Zhiyu Huang, Jiaqi Ma, Chen Tang
- 机构：arXiv 版本信息未直接提供机构字段

## 发布日期/版本日期
2026-08-19（arXiv v1）

## 主题标签
#EmbodiedAI #Robotics #Policy-Evaluation #Sim2Real #Conformal-Prediction

## 论文链接
- arXiv：https://arxiv.org/abs/2608.19425

## PDF 链接
- https://arxiv.org/pdf/2608.19425.pdf

## 项目/代码/数据链接
- 项目/代码：未在 arXiv 条目直接公开
- 数据：未在摘要页直接公开；论文涉及 autonomous driving 与 quadruped velocity tracking 的实验场景

## 核心问题
传统仿真增强评估忽视了情景异质性，往往只给出平均表现，难以指导“在何种场景下该放行、何种场景禁用”。论文试图回答：如何用少量真实样本 + 大规模仿真预测场景条件下的真实表现。

## 方法概要
- 构建 SCAPE 框架：输入有限 paired sim-real 样本与大量仿真 rollouts。
- 使用偏差校正对仿真标签进行调整，降低 sim-to-real 偏差。
- 学习场景条件的性能预测模型，并用 conformal prediction 给出校准后的不确定区间。
- 在自动驾驶、四足机器人速度跟踪任务上验证。

## 主要贡献
1. 将 policy evaluation 提升到 scenario-conditioned 维度，强调部署前安全边界识别。
2. 引入 bias-corrected simulation labels 与 conformal uncertainty 的结合，支持更稳健的样本外估计。
3. 在两个任务上展示样本效率和误差收益，且实现更窄的校准区间。

## 关键实验或结果
- Sim-to-sim 中，场景级误差相比基线下降：驾驶任务 4.9%/34.7%，四足跟踪 14.5%/27.7%（按文中对应指标）。
- 对于物理机器人验证（Unitree Go2），SCAPE 提升了测试样本效率，给出更窄的预测区间。
- OOD 场景泛化更好，支持更细分部署策略（scenario-aware rollout 策略）。

## 适合关注的原因
部署前风险评估是 robotics 与 autonomy 的核心问题，SCAPE 的情景条件化思路能帮助决定“在哪些场景允许上线、在哪些场景需要保守策略”，有直接工程价值。

## 局限性或待验证点
- 文摘未披露更多任务细节与复杂度，需查看完整实验定义（状态建模、分布偏移量化）。
- 在多智能体、非刚体环境或长时程任务中的泛化仍待检验。
- Conformal 校准参数选择会影响风险预算解释，需要领域标准化。

## 对后续研究/应用的启发
- 可扩展到自动驾驶、仓储机器人、无人机等“高风险场景分层放行”问题。
- 可与离线策略评估、risk-aware planning 联动，形成统一的 scenario risk score。
- 对行业标准可提供：发布模型并行给出场景分层性能分布，而非单值成绩。

## 适合 Obsidian 快速浏览的中文总结
一句话：SCAPE 证明了“场景条件化 + 校准不确定性”可显著提升仿真到实机策略评估的决策价值。 

## 标准化研究框架
**Research question：** 在真实试验样本受限时，能否借助纠偏后的仿真 rollouts 与不确定性校准，准确预测不同场景下策略在实机中的性能分布？

**Literature：** 先前 Sim-to-Real / sim-augmented eval 多聚焦总体平均指标，缺乏场景分层预测；SCAPE 将 conformal 预测加入仿真评估，补足不确定性表达不足。

**Theory：** 性能预测应按场景条件分解：P(real_performance | scenario) ≈ g( corrected(sim_data), scenario_features )。不确定性通过 conformal interval 校准以满足覆盖约束。

**Hypotheses：** 若对仿真标签进行偏差修正并显式建模场景特征，场景级预测误差会显著低于场景无关基线，且覆盖率更稳定。

**Method：** 采集 paired sim/real 训练样本，训练场景条件回归器并应用偏差修正；再通过 conformal 方法计算区间，比较驾驶与四足任务中的误差/覆盖性/样本效率。

**Data and Analysis：** 数据包括驾驶与四足 velocity tracking 的仿真与真实 rollout，使用场景分桶后的误差指标、校准区间宽度、OOD 泛化结果作对比。

**Findings：** SCAPE 在两个任务上均带来较大误差下降与更窄预测区间，提升 OOD 泛化和部署策略可解释性，支持场景分层决策。

**Conclusion：** 对高风险控制系统，情景条件的性能预测优于单点平均分；该框架可作为“何时放行、何时收紧”策略的量化基础。EOF

cat <<'EOF' > '2026-08-22/README.md'
# 2026-08-22 AI 论文分享

今日主题覆盖 LLM 安全、AI4AI Agent、EHR 临床 AI、CV、Embodied AI。

## 推荐顺序

1. [01-conceptguard-benchmark.md](01-conceptguard-benchmark.md)
   - Spotlight：ConceptGuard 将 unlearning 从 fact-level 推向 concept-level，重点测“危险概念在语境间的可控抑制”，对 LLM 安全治理场景非常贴近落地。
   - 论文链接：[https://arxiv.org/abs/2608.20338](https://arxiv.org/abs/2608.20338)

2. [02-ai4ai-bench-rsi.md](02-ai4ai-bench-rsi.md)
   - Spotlight：AI4AI-Bench 首次把“修改训练算法”作为主任务，可量化测试 agent 是否具备可复现的递归改进能力。
   - 论文链接：[https://arxiv.org/abs/2608.20318](https://arxiv.org/abs/2608.20318)

3. [03-bert-ler-ehr-explainable.md](03-bert-ler-ehr-explainable.md)
   - Spotlight：BERT-LER 在结构化 EHR 中结合实验室定量编码与 Integrated Gradients，强调可解释预测而非单点精度。
   - 论文链接：[https://arxiv.org/abs/2608.20315](https://arxiv.org/abs/2608.20315)

4. [04-4danyone.md](04-4danyone.md)
   - Spotlight：4DAnyone 提供从随拍单目视频到 4D 人体的闭环方法，尤其通过 RCP 与 TCR 缓解多视图扩展瓶颈。
   - 论文链接：[https://arxiv.org/abs/2608.20335](https://arxiv.org/abs/2608.20335)

5. [05-scape-policy-eval.md](05-scape-policy-eval.md)
   - Spotlight：SCAPE 用场景条件化仿真增强评估替代平均分指标，帮助明确哪些场景适合部署、哪些场景需要保守处理。
   - 论文链接：[https://arxiv.org/abs/2608.19425](https://arxiv.org/abs/2608.19425)

## 备注
当日 5 篇均为近期 arXiv 发布（8 月下旬，偏安全与落地价值兼顾）。如后续补充项目页/代码库链接，将持续更新。EOF
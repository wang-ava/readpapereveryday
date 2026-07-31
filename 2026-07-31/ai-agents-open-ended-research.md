# Can AI agents conduct open-ended AI research? Early evidence from two case studies

Spotlight：本文不在评测“能不能写出一篇好论文”这种单点问题，而是把 AI research automation 变成“开放问题驱动、资源受限、可复盘评估”全过程。它第一次把 AI agent 的科研执行能力放进“作者审阅”这道真实关卡，而非只看 benchmark 分数。

- 论文标题：Can AI agents conduct open-ended AI research? Early evidence from two case studies
- 作者：Peter Kirgis, Sayash Kapoor, Andrew Schwartz, Stephan Rabanser, David Africa, Konstantinos Voudouris, Viet Nguyen, Toby Pilditch, Magda Dubois, Harry Coppock, Cozmin Ududec, Nitya Nadgir, Matilda Orona, Tilman Bayer, Derrick Chan-Sew, Yue Ling, Abhishek Shetty, Helen Toner, Gillian Hadfield, Seth Lazar, Steve Newman, Shoshannah Tekofsky, Rishi Bommasani, Arvind Narayanan
- 机构（如可得）：未在 arXiv 页面给出；涉及机构主要在论文链接与附录仓库上下文中披露
- 发布日期或版本日期：2026-07-29T17:57:19Z（UTC），折合 Asia/Shanghai 为 2026-07-30 01:57:19
- 主题标签：#Agent #LLMResearch #AI4Research #Evaluation #R\&DAutomation
- 论文链接：[https://arxiv.org/abs/2607.27191v1](https://arxiv.org/abs/2607.27191v1)
- PDF 链接：[https://arxiv.org/pdf/2607.27191v1](https://arxiv.org/pdf/2607.27191v1)
- 项目/代码/数据链接（如可得）：论文文本提到发布了专家 review、问卷、agent repositories 与 logs，未在 arXiv 摘要区直接给出具体 URL，建议查看正文/附录获取持久链接

## 核心问题
- 当前对 AI 代理自动化科研的评估多为窄任务 benchmark 或直接投盲审，缺少对“开放研究问题”求解全过程的评价。
- 关键问题是：AI agent 在真实科研生命周期中，能否进行问题理解、方法选择、实验迭代与学术判断。
- 论文提出把“能否达到可发表研究标准”转化为可执行、可观察、可复测的评估框架。

## 方法概要
- 提出 `shadow evaluation` 方案：让 Agent 接手一篇未公开高质量论文的核心研究问题。
- 论文作者按角色给出反馈，代替盲审或单项答题式测评。
- 使用两篇未公开 NeurIPS 2026 投稿作为案例，配置前后端系统进行端到端验证。
- 评估周期包含工程执行、反思修正、资源使用、失败回溯，测试时长约 6 天并有较高算力预算。

## 主要贡献
- 将 open-ended AI research 的评估问题形式化为可复现的 shadow review 协议。
- 识别出 5 类关键失败模式：
  - 对可发表性标准判断不足
  - 面对缺口时创新替代思路不足
  - 回滚/逆向修正能力弱
  - 资源意识不足
  - instruction drift（目标漂移）
- 强化了“AI 代理可执行工程，但难替代研究设计判断”的现实边界认知。

## 关键实验或结果
- 两个案例中，agent 能完成主要工程执行（数据、复现、实验链路搭建）且不依赖人工 intervention。
- 最终两篇案例均未达到作者认可，均被明确拒绝。
- 该结果在重复模型与 scaffold 下仍然一致，提示问题是结构性而非偶发。

## 适合关注的原因
- 这个工作把“LLM 代理进步叙事”的核心环节钉在现实可执行指标上，避免只看短答题式 benchmark。
- 为实验室、组织评估 Agent 的研发投资与人力替代潜力，给了更硬核、可操作的判据。

## 局限性或待验证点
- 目前样本仅 2 个案例，难直接外推到所有研究方向。
- 评审标准来自原始论文作者，公平性与可复用性需要更多独立评估。
- 与不同组织文化、团队节奏下的科研流程兼容性未被系统检验。

## 对后续研究/应用的启发
- 可以设计更细粒度的 `agent research stack` 竞赛：问题理解、方法设计、实验闭环、写作质量分别评分。
- 与经费/算力预算结合后，形成 cost-aware 代理科研评估方法（如 $/有效迭代）。
- 对科研自动化平台有直接启发：将“工程代理能力”与“科研判断能力”解耦管理。

## 一句 Obsidian 快速浏览总结
一句话：这篇工作首次把“AI 研究代理”推到真正的开放科研问题上，证明其现阶段能做工程，不一定能做科学判断。

## 标准化研究框架
- **Research question：** 面向开放、非封闭式科研任务，AI agents 在多天、多算力预算约束下是否能达到研究者可接受的原创性与有效性门槛？
- **Literature：** 继承了对 benchmark 局限性的讨论（Narrow evaluation、blind review），并与 Agent-based automation、自动化科研评估相关工作形成对照。
- **Theory：** 对该类研究，Agent 的关键能力不只是“执行能力”，还包括问题拆解、失败修正和价值判断；前者更容易外包，后者仍是主要瓶颈。
- **Hypotheses：** 在 open-ended 研究任务中，前沿 agent 可接近工程可行但在研究设计与判据判断上存在可重复失败模式。
- **Method：** 用两篇高质量未发布论文进行 shadow evaluation，记录 agent 全流程行为，并由原作者按研究标准给评分。
- **Data and Analysis：** 使用专家复核意见、agent log、对照实验（第二模型+scaffold）分析失败来源，重点比较成功率与失败一致性。
- **Findings：** 论文显示工程阶段可高度自动化，但科研判断（问题定义、修订、资源取舍）依旧薄弱。
- **Conclusion：** 当前AI 代理更接近“科研执行员”而非“科研主导者”；若要推进到可靠 automation，需把方法选择和判断环节显式建模并加以优化。

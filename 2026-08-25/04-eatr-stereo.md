# EATR-Stereo: Embodiment-Aware Token Routing of Paired Stereo Evidence for Humanoid VLA Control

EATR-Stereo 针对 humanoid VLA（Vision-Language-Action）任务提出了“主视图不被打断、辅助视图按身体状态路由”的 token 架构。核心在于解决双目证据互补与 robot embodiment 不匹配导致的长时控制不稳问题。

该工作值得关注，是因为它将“多视图信息融合”变成了可控的结构决策问题：不是盲目堆叠 stereo token，而是让模型只在有效时用好辅助视图。

## 论文标题
EATR-Stereo: Embodiment-Aware Token Routing of Paired Stereo Evidence for Humanoid Vision-Language-Action Control

## 作者/机构
- 作者：Songwei Wu, Rui Zhao, Fan Yang, Zhongqiang Nie, Zhiduo Jiang, Wandong Sun, Yuwei Li, Jian Hu, Yang Liu, Hong Liu
- 机构：arXiv 页面未公开机构信息

## 发布日期/版本日期
- 版本发布日期：2026-08-18（v3，`2026-08-18T07:32:50Z`，对应 Asia/Shanghai 2026-08-18）

## 主题标签
#EmbodiedAI #Robotics #VLA #StereoVision #TokenRouting

## 论文链接
- https://arxiv.org/abs/2608.17453v3

## PDF 链接
- https://arxiv.org/pdf/2608.17453v3

## 项目/代码/数据链接
- 项目/代码/数据：摘要未给出公开链接

## 核心问题
在 humanoid long-horizon 操作中，模型需要利用头戴 stereo 相机信息，但当前常见做法要么丢失主视图结构，要么无法按当前身体状态决定何时引入辅助视图。论文的问题是：如何在不破坏主模型语义路径的前提下，鲁棒利用 stereo 互补信息？

## 方法概要
- 设计 embodiment-aware token routing：保留 primary-view token 流程不变。
- 从辅助视图构造 Cross-View Auxiliary Tokens（CVATs），并对其进行查询。
- 引入 body-segmented proprioceptive encoder：将身体姿态历史嵌入路由决策。
- 在预训练 VLA 上冻结主干，仅在 token 路由层注入 stereo 辅助，做九种任务配置对比。

## 主要贡献
1. 给出“主流视图保留 + 选择性辅助注入”的架构设计，避免传统双目融合破坏主路径语义。
2. 让 proprioception 参与 token routing，建立 embodiment-aware 的跨模态信息调度。
3. 在 long-horizon 具身任务上给出可操作的硬指标（full-task/grasp/stage 成功率）提升。

## 关键实验或结果
- 实验平台：33-DoF humanoid（37-D proprioceptive state）。
- 任务：search-approach-grasp-place-return（多达 100s）。
- 指标：全任务成功率 60.0%、抓取成功率 100.0%、阶段成功率 80.0%。
- 在重度非对称遮挡下，恢复率 80%，显著高于对照方法的 30%。
- 消融显示主视图保留与 proprioceptive 条件化对性能关键。

## 适合关注的原因
它直接回应了“具身智能在复杂遮挡与长时序任务中的信息调度”问题，给出结构化可复现的提升路径，且可迁移到其他多视角机器人平台。

## 局限性或待验证点
- 主要验证集中于单一 humanoid 平台，跨平台泛化仍待测试。
- 未在公开仓库中披露全部参数与训练细节（以摘要为主）。
- 对环境复杂度、光照变化和不同 stereo 校准误差的耐受范围尚需更多 benchmark。

## 对后续研究/应用的启发
- 可以将 EATR 的路由思想用于 mobile robot、AR 辅助 teleoperation 等多视图控制场景。
- 后续可将 CVAT 扩展为多 sensor bank（RGB+Depth+force）统一路由。
- 对长期任务，路由策略可与预算分配（计算/时延）联合优化。

## 适合 Obsidian 快速浏览的中文总结
一句话：EATR-Stereo 通过“保留主视图+按身体状态路由辅助视图 token”，显著提升 humanoid 长时长 VLA 在遮挡与复杂序列中的控制稳定性。

## 标准化研究框架
**Research question：** 本文是 embodied system design 问题：在保持主干模型语义一致性前提下，如何选择并调度 stereo 辅助证据以提升 long-horizon VLA 成功率。

**Literature：** 传统方法多直接融合全量多视图或忽略 embodiment 条件；本工作强调“结构约束下的信息路由”以减少干扰。

**Theory：** 对应于受约束路由机制：主路径保持冻结，辅助 token 的注入由状态条件门控控制，以抑制坏的跨视图信号。

**Hypotheses：** 1）保持 primary token 不被污染能提高稳定性；2）融合 proprioceptive 信息可改善何时引入辅助视图；3）路由策略能在遮挡下增强任务恢复能力。

**Method：** 构建 CVAT 与 body-aware 路由器，在九种配置下做对照；用 long-horizon 搜索-抓取-放置-返回任务评估。

**Data and Analysis：** 任务集规模为百秒级长序列 humanoid 操作，分析指标包括 full-task/grasp/stage 成功率与严重遮挡条件下恢复率。

**Findings：** 在所测任务与平台上，EATR-Stereo 显著优于对照，遮挡鲁棒性提升尤为明显；消融表明主视图保留与状态路由对效果贡献最大。

**Conclusion：** 对具身控制而言，关键不在堆特征，而在“何时、何处、如何注入”多视图证据；路由式架构可能比盲融合更易扩展。

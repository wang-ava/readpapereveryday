# 2026-09-19 每日 AI 论文分享

日期按 **Asia/Shanghai** 确定。本次精选 3 篇 2026-09-16 至 09-17 发布的论文，均在最近 14 天内，已按编号和标题检查往期笔记，无重复。今日围绕 Agent 的成本、证据与工具可靠性展开；不为凑齐领域而降低来源核验要求。

| 推荐顺序 | 论文笔记 | Spotlight | 原文 |
| --- | --- | --- | --- |
| 1 | [SoL-Pi](01-sol-pi.md) | 自动搜索运行框架改进，降低重复上下文开销；必须同时看成本和能力损失。 | [论文](https://arxiv.org/abs/2609.20519v1) · [PDF](https://arxiv.org/pdf/2609.20519v1) |
| 2 | [The Missing Complement](02-missing-complement.md) | 检索应补齐当前决策的证据组合，而非重复返回相似代码。 | [论文](https://arxiv.org/abs/2609.20050v1) · [PDF](https://arxiv.org/pdf/2609.20050v1) |
| 3 | [Closed-World Resolution](03-closed-world-tool-resolution.md) | 工具调用先解析后授权；重点区分实测幻觉与构造式防护保证。 | [论文](https://arxiv.org/abs/2609.19425v1) · [PDF](https://arxiv.org/pdf/2609.19425v1) |

## 推荐理由与阅读顺序

先读 SoL-Pi，把握运行框架可优化的具体环节；再读 The Missing Complement，思考压缩上下文时哪些证据必须保留；最后读 Closed-World Resolution，检查输出调用进入执行器之前需要哪些确定性约束。排序综合可应用性、技术问题清晰程度及证据强度，并非学术质量排行榜。

## 核验说明

依据 arXiv 原始版本记录与 HTML 正文整理，搜索聚合页只用于发现候选。三篇均为近期预印本，未独立复现；笔记明确区分作者报告、实验边界和后续研究建议。项目链接为原文指向的资源，不等于已完成安装或数据完整性审计。每篇末尾均包含八字段「标准化研究框架」。

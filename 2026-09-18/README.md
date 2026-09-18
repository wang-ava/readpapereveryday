# 2026-09-18 每日 AI 论文分享

日期采用 Asia/Shanghai。今日选取 3 篇此前未收录的论文，按推荐阅读顺序排列，覆盖 Agent、LLM 机制与 CV 文档理解。均在最近 7 天内上线 arXiv；Tables Decoded 已标注 WACV 2026，因此区分近期上线日期与研究首次发表时间。依据官方摘要、版本记录与正文核验；未复现实验。

| 顺序 | 论文笔记 | Spotlight | 日期及原文 |
| --- | --- | --- | --- |
| 1 | [Agora：Git 共享研究记忆](01-agora.md) | 将结果、失败与复现接入证据图；长期运行可行，但单位算力优势尚无对照证明。 | 09-16 v1 · [arXiv](https://arxiv.org/abs/2609.18094v1) · [PDF](https://arxiv.org/pdf/2609.18094v1) |
| 2 | [SSM 门控与上下文学习](02-ssm-gating.md) | 检索失败可能来自学习捷径，门控对检索与长度泛化的影响需分别评估。 | 09-15 v1 · [arXiv](https://arxiv.org/abs/2609.16540v1) · [PDF](https://arxiv.org/pdf/2609.16540v1) |
| 3 | [Tables Decoded：结构文本表格问答](03-tables-decoded.md) | 解耦结构与 OCR 方便诊断，结构高分却不意味着完整表格或问答已足够准确。 | 09-15 v1 · [arXiv](https://arxiv.org/abs/2609.17458v1) · [PDF](https://arxiv.org/pdf/2609.17458v1) |

推荐顺序综合技术启发、证据可核查性及应用阅读价值，不代表权威排名。先看 Agora 的证据组织方式，再看门控机制的诊断实验，最后看文档管线的误差分解。每篇末尾含八字段「标准化研究框架」；结果与后续建议分开表述，未知链接明确标注。

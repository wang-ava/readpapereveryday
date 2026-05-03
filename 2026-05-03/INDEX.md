# 2026-05-03 论文推荐索引

今日共推荐 **20 篇**论文：10 篇 AI4Health，10 篇纯 AI。

---

## AI4Health（医疗与健康 AI）

### 🧬 分子与结构生物学

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| H-01 | [AlphaFold3](./AI4Health/2026-05-03-AlphaFold3.md) | Google DeepMind | Nature 2024 | 用扩散模型预测蛋白质-DNA-RNA-小分子所有生物复合体的三维结构 |

### 🏥 医疗大语言模型

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| H-02 | [Med-Gemini](./AI4Health/2026-05-03-Med-Gemini.md) | Google DeepMind | arXiv 2024 | 将 Gemini 多模态大模型专门针对医疗场景微调，在医学考试和影像分析上超越专科医生 |
| H-05 | [BioMistral](./AI4Health/2026-05-03-BioMistral.md) | Avignon 大学 | arXiv 2024 | 基于 Mistral 7B 在 PubMed 医学文献上继续预训练，完全开源的医疗 LLM |
| H-09 | [EHRAgent](./AI4Health/2026-05-03-EHRAgent.md) | UCSD | EMNLP 2024 | 让 LLM 自动写 Python 代码查询电子病历，实现准确的 EHR 数据问答 |

### 🔬 计算病理学

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| H-03 | [CONCH](./AI4Health/2026-05-03-CONCH.md) | 哈佛医学院 | Nature Medicine 2024 | 110 万病理图文对对比学习，病理学视觉语言基础模型 |
| H-04 | [CHIEF](./AI4Health/2026-05-03-CHIEF.md) | 哈佛/MIT | Nature 2024 | 6 万张全切片图像预训练，覆盖 19 种癌症的统一病理基础模型 |
| H-06 | [PathChat](./AI4Health/2026-05-03-PathChat.md) | 哈佛/Microsoft | Nature 2024 | 病理学多模态对话 AI，医生可以用自然语言问关于病理图像的问题 |

### 📡 医学影像

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| H-07 | [MAIRA-2](./AI4Health/2026-05-03-MAIRA-2.md) | Microsoft Research | arXiv 2024 | 有依据的放射报告自动生成，同时给出文字描述和对应的图像定位框 |
| H-08 | [MedImageInsight](./AI4Health/2026-05-03-MedImageInsight.md) | Microsoft Research | arXiv 2024 | 覆盖放射、病理、眼科等多模态的通用医学图像嵌入开源模型 |
| H-10 | [RetFound](./AI4Health/2026-05-03-RetFound.md) | UCL/Moorfields | Nature 2023 | 160 万视网膜图像自监督预训练，可从眼底照片预测多种全身疾病 |

---

## 纯 AI（深度学习与大语言模型）

### 🏗️ 新型模型架构

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| A-01 | [Mamba](./AI/2026-05-03-Mamba.md) | CMU | arXiv 2023/2024 | 引入选择性状态空间模型，线性复杂度首次媲美 Transformer 的长序列建模 |
| A-02 | [KAN](./AI/2026-05-03-KAN.md) | MIT | arXiv 2024 | 把 MLP 中固定的激活函数改为可学习的样条函数，更高效且可解释 |

### 🚀 大语言模型

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| A-03 | [Llama 3](./AI/2026-05-03-Llama3.md) | Meta AI | arXiv 2024 | 15T token 训练的开源 LLM，405B 版本首次真正接近 GPT-4o 水平 |
| A-04 | [DeepSeek-V2](./AI/2026-05-03-DeepSeek-V2.md) | DeepSeek AI | arXiv 2024 | MLA + DeepSeekMoE 双创新，236B 参数但只激活 21B，性价比极致 |
| A-05 | [Mixtral 8x7B](./AI/2026-05-03-Mixtral-8x7B.md) | Mistral AI | arXiv 2024 | 开源稀疏 MoE 模型，8 个专家每次激活 2 个，超越 Llama 2 70B |
| A-08 | [Gemma 2](./AI/2026-05-03-Gemma2.md) | Google DeepMind | arXiv 2024 | 知识蒸馏 + 局部/全局注意力交替，9B 模型接近 70B 性能 |
| A-09 | [Qwen2](./AI/2026-05-03-Qwen2.md) | 阿里巴巴 | arXiv 2024 | 支持 29 种语言，数学和代码能力突出，72B 版全面超越 Llama 3 70B |

### ⚡ 高效训练与推理

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| A-06 | [FlashAttention-2](./AI/2026-05-03-FlashAttention2.md) | 斯坦福 | arXiv 2023 | 硬件感知的分块注意力计算，达到 A100 73% 峰值吞吐，成为行业标准 |
| A-10 | [LoRA](./AI/2026-05-03-LoRA.md) | Microsoft Research | ICLR 2022 | 低秩分解旁路微调，0.003% 的参数量达到全量微调 90%+ 效果，经典必读 |

### 🧮 推理与强化学习

| 编号 | 论文名称 | 机构 | 时间 | 一句话简介 |
|------|---------|------|------|-----------|
| A-07 | [DeepSeekMath + GRPO](./AI/2026-05-03-DeepSeekMath-GRPO.md) | DeepSeek AI | arXiv 2024 | 大规模数学数据 + 群体相对策略优化，7B 模型数学能力接近 GPT-4 |

---

## 主题分类总结

| 主题 | 相关论文 |
|------|---------|
| 基础模型 / Foundation Model | AlphaFold3, CONCH, CHIEF, RetFound, MedImageInsight, Mamba, Llama 3 |
| 大语言模型 / LLM | Med-Gemini, BioMistral, DeepSeek-V2, Mixtral, Gemma 2, Qwen2 |
| 多模态 AI | Med-Gemini, PathChat, MAIRA-2 |
| 高效训练与推理 | FlashAttention-2, LoRA, Gemma 2（蒸馏）, DeepSeek-V2（MoE）|
| 强化学习 | DeepSeekMath + GRPO |
| AI Agent | EHRAgent |
| 新型架构 | Mamba, KAN, Mixtral（MoE），DeepSeek-V2（MoE）|

---

## 阅读建议

**初学者入门路线**（按难度递增）：
1. LoRA → FlashAttention-2 → Mamba → Llama 3 → KAN

**AI4Health 入门路线**：
1. RetFound → CONCH → CHIEF → PathChat → Med-Gemini

**追求性能/效率前沿**：
1. DeepSeek-V2 → Mixtral → GRPO → Gemma 2 → Qwen2

---

*更新日期：2026-05-03 | 下次更新不重复以上任何论文*

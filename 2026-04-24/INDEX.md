# 每日论文推荐 — 2026-04-24

今日共推荐 **20 篇论文**（10篇 AI4Health + 10篇 纯AI领域），均为业内值得精读的重要成果。

---

## 🏥 AI4Health 专区（10篇）

> 主题涵盖：结构生物学、医学多模态AI、计算病理学、蛋白质设计、眼科AI、医学大语言模型

| # | 报告文件 | 论文标题 | 发表/年份 | 一句话核心 |
|---|---------|---------|----------|-----------|
| 1 | [2026-04-24-AlphaFold3.md](AI4Health/2026-04-24-AlphaFold3.md) | Accurate structure prediction of biomolecular interactions with AlphaFold 3 | Nature 2024 | 首个能预测蛋白质+DNA+RNA+小分子配体复合物结构的AI，扩散模型统一处理所有生物分子 |
| 2 | [2026-04-24-Med-Gemini.md](AI4Health/2026-04-24-Med-Gemini.md) | Capabilities of Gemini Models in Medicine | arXiv 2024 | Google医疗多模态大模型，USMLE达91.1%，支持百万token超长医疗记录 |
| 3 | [2026-04-24-CONCH.md](AI4Health/2026-04-24-CONCH.md) | A visual-language foundation model for computational pathology | Nature Medicine 2024 | 病理图像+文字对比学习基础模型，100万图文对训练，零样本迁移14项病理任务 |
| 4 | [2026-04-24-UNI.md](AI4Health/2026-04-24-UNI.md) | Towards a general-purpose foundation model for computational pathology | Nature Medicine 2024 | 1亿病理图像块自监督预训练，无标注学习通用病理特征，超越专病监督模型 |
| 5 | [2026-04-24-ESM3.md](AI4Health/2026-04-24-ESM3.md) | Simulating 570 million years of evolution with a language model | Science 2024 | 蛋白质多模态语言模型，98B参数，从头设计全新荧光蛋白，演化距离达5.7亿年 |
| 6 | [2026-04-24-GigaPath.md](AI4Health/2026-04-24-GigaPath.md) | A whole-slide foundation model for digital pathology from real-world data | Nature 2024 | 微软用17万张真实临床WSI训练的全玻片病理基础模型，首次实现全局上下文理解 |
| 7 | [2026-04-24-RetFound.md](AI4Health/2026-04-24-RetFound.md) | A foundation model for generalizable disease detection from retinal images | Nature 2023 | 190万眼底图像MAE自监督预训练，一个模型筛查眼病+心力衰竭+帕金森等多种疾病 |
| 8 | [2026-04-24-BioMistral.md](AI4Health/2026-04-24-BioMistral.md) | BioMistral: A Collection of Open-Source Pretrained LLMs for Medical Domains | arXiv 2024 | 开源医学LLM，基于Mistral 7B在PubMed上继续预训练，支持消费级GPU本地部署 |
| 9 | [2026-04-24-MedPaLM2.md](AI4Health/2026-04-24-MedPaLM2.md) | Towards Expert-Level Medical Question Answering with LLMs | arXiv 2023 | Google医疗LLM，USMLE达86.5%接近人类专家，引入医生偏好多维评估框架 |
| 10 | [2026-04-24-CheXagent.md](AI4Health/2026-04-24-CheXagent.md) | CheXagent: Towards a Foundation Model for Chest X-Ray Analysis | arXiv 2024 | 斯坦福胸部X光通用基础模型，整合28个数据集，支持VQA/报告生成/疾病定位 |

---

## 🤖 纯AI领域专区（10篇）

> 主题涵盖：基础架构、预训练范式、高效微调、推理增强、对齐技术、序列建模、系统优化

| # | 报告文件 | 论文标题 | 发表/年份 | 一句话核心 |
|---|---------|---------|----------|-----------|
| 1 | [2026-04-24-Attention-Is-All-You-Need.md](PureAI/2026-04-24-Attention-Is-All-You-Need.md) | Attention Is All You Need | NeurIPS 2017 | 发明Transformer架构，完全基于注意力机制，改变了整个AI领域的基础 |
| 2 | [2026-04-24-BERT.md](PureAI/2026-04-24-BERT.md) | BERT: Pre-training of Deep Bidirectional Transformers | NAACL 2019 | 双向预训练+MLM掩码语言模型，开创"预训练+微调"范式，刷新11项NLP任务 |
| 3 | [2026-04-24-GPT-3.md](PureAI/2026-04-24-GPT-3.md) | Language Models are Few-Shot Learners | NeurIPS 2020 | 175B参数GPT-3，证明规模涌现与少样本学习，ChatGPT的前身 |
| 4 | [2026-04-24-LoRA.md](PureAI/2026-04-24-LoRA.md) | LoRA: Low-Rank Adaptation of Large Language Models | ICLR 2022 | 低秩矩阵分解只训练0.01%参数即可微调大模型，零推理延迟，最广泛使用的PEFT方法 |
| 5 | [2026-04-24-Chain-of-Thought.md](PureAI/2026-04-24-Chain-of-Thought.md) | Chain-of-Thought Prompting Elicits Reasoning in LLMs | NeurIPS 2022 | 思维链提示让大模型逐步推理，数学题准确率从17%提升至58%，"Let's think step by step" |
| 6 | [2026-04-24-DPO.md](PureAI/2026-04-24-DPO.md) | Direct Preference Optimization | NeurIPS 2023 最佳论文 | 无需奖励模型，直接从偏好数据优化LLM，比RLHF/PPO更简单稳定，ChatGPT对齐的替代方案 |
| 7 | [2026-04-24-Mamba.md](PureAI/2026-04-24-Mamba.md) | Mamba: Linear-Time Sequence Modeling with Selective State Spaces | arXiv 2023 | 选择性状态空间模型，O(n)线性复杂度，长序列推理比Transformer快5倍 |
| 8 | [2026-04-24-FlashAttention2.md](PureAI/2026-04-24-FlashAttention2.md) | FlashAttention-2: Faster Attention with Better Parallelism | ICLR 2024 | IO感知注意力计算，减少HBM访问次数，速度提升2-9倍，内存从O(n²)降至O(n) |
| 9 | [2026-04-24-Llama3.md](PureAI/2026-04-24-Llama3.md) | The Llama 3 Herd of Models | arXiv 2024 | Meta开源LLM，405B旗舰版性能接近GPT-4o，15T tokens训练，128K上下文 |
| 10 | [2026-04-24-Mixtral.md](PureAI/2026-04-24-Mixtral.md) | Mixtral of Experts | arXiv 2024 | 稀疏混合专家模型，47B总参数但每次只激活13B，以1/5计算量超越LLaMA-2 70B |

---

## 📂 文件结构

```
2026-04-24/
├── INDEX.md                          ← 本文件（导航索引）
├── AI4Health/
│   ├── 2026-04-24-AlphaFold3.md
│   ├── 2026-04-24-Med-Gemini.md
│   ├── 2026-04-24-CONCH.md
│   ├── 2026-04-24-UNI.md
│   ├── 2026-04-24-ESM3.md
│   ├── 2026-04-24-GigaPath.md
│   ├── 2026-04-24-RetFound.md
│   ├── 2026-04-24-BioMistral.md
│   ├── 2026-04-24-MedPaLM2.md
│   └── 2026-04-24-CheXagent.md
└── PureAI/
    ├── 2026-04-24-Attention-Is-All-You-Need.md
    ├── 2026-04-24-BERT.md
    ├── 2026-04-24-GPT-3.md
    ├── 2026-04-24-LoRA.md
    ├── 2026-04-24-Chain-of-Thought.md
    ├── 2026-04-24-DPO.md
    ├── 2026-04-24-Mamba.md
    ├── 2026-04-24-FlashAttention2.md
    ├── 2026-04-24-Llama3.md
    └── 2026-04-24-Mixtral.md
```

---

## 📖 每篇报告包含

每篇报告均按以下格式撰写，面向初学者，用通俗语言解读：

- 📄 **论文信息**（标题、作者、期刊、链接）
- 🌟 **背景知识**（为什么需要、解决什么问题）
- 🔬 **做了什么**（核心贡献一句话概括）
- 🛠️ **怎么做的**（方法详解 + 通俗类比）
- 📊 **主要结论**（关键数据和发现）
- ⚠️ **局限性**（客观分析不足之处）
- 💡 **为什么值得关注**（影响力和未来价值）

---

*生成日期：2026-04-24 | 下次推荐将排除以上20篇，确保不重复*

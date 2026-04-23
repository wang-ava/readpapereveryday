# 2026-04-23 每日论文推荐索引

> 共 20 篇论文：10 篇 AI4Health + 10 篇 Pure-AI
> 所有报告均包含：论文链接、背景知识、研究内容、方法、结论、局限性，通俗易懂。

---

## AI4Health（人工智能 × 医疗健康）

| # | 论文名称 | 年份 | 方向 | 核心贡献 | 报告链接 |
|---|---------|------|------|---------|---------|
| 1 | **AlphaFold 3** | 2024 | 结构生物学 | 用扩散模型预测蛋白质与DNA/RNA/小分子的3D相互作用结构 | [→ 报告](AI4Health/2026-04-23-AlphaFold3.md) |
| 2 | **Med-Gemini** | 2024 | 医疗LLM | Gemini基础+联网搜索+自训练，超越GPT-4的多模态医疗AI | [→ 报告](AI4Health/2026-04-23-Med-Gemini.md) |
| 3 | **LLaVA-Med** | 2023 | 医学VQA | 用PMC论文图注+GPT-4合成对话，一天训练出医学视觉问答模型 | [→ 报告](AI4Health/2026-04-23-LLaVA-Med.md) |
| 4 | **MedSAM** | 2024 | 医学图像分割 | 在157万医学图像上微调SAM，实现通用医学分割 | [→ 报告](AI4Health/2026-04-23-MedSAM.md) |
| 5 | **CONCH** | 2024 | 计算病理学 | 43万病理图文对对比学习，零样本病理图像分类新SOTA | [→ 报告](AI4Health/2026-04-23-CONCH.md) |
| 6 | **Health-LLM** | 2024 | 可穿戴AI | 把智能手表传感器数据转成文字，让GPT-4直接预测健康状态 | [→ 报告](AI4Health/2026-04-23-Health-LLM.md) |
| 7 | **MAIRA-2** | 2024 | 放射学报告 | 生成带边界框定位的胸部X光报告，让AI发现更可解释 | [→ 报告](AI4Health/2026-04-23-MAIRA-2.md) |
| 8 | **CheXagent** | 2024 | 胸部X光AI | 一个基础模型完成8种胸部X光任务，构建CheXbench评测基准 | [→ 报告](AI4Health/2026-04-23-CheXagent.md) |
| 9 | **Med-PaLM M** | 2024 | 通才医疗AI | 14种医疗任务统一到一个多模态模型，接近专科AI水平 | [→ 报告](AI4Health/2026-04-23-Med-PaLM-M.md) |
| 10 | **Tx-LLM** | 2024 | 药物研发 | 709个治疗学数据集+66种药物性质，多任务LLM助力新药研发 | [→ 报告](AI4Health/2026-04-23-Tx-LLM.md) |

---

## Pure-AI（纯人工智能）

| # | 论文名称 | 年份 | 方向 | 核心贡献 | 报告链接 |
|---|---------|------|------|---------|---------|
| 1 | **Attention Is All You Need** | 2017 | 架构 | 发明Transformer，用自注意力取代RNN，所有现代LLM的基础 | [→ 报告](Pure-AI/2026-04-23-Attention-Is-All-You-Need.md) |
| 2 | **GPT-4 Technical Report** | 2023 | 大语言模型 | 多模态LLM，律师考试前10%，可预测扩展性，引领AI助手时代 | [→ 报告](Pure-AI/2026-04-23-GPT-4-Technical-Report.md) |
| 3 | **Llama 3** | 2024 | 开源LLM | 405B开源模型，15T训练数据，首次让开源模型媲美GPT-4 | [→ 报告](Pure-AI/2026-04-23-Llama3.md) |
| 4 | **Mamba** | 2023 | 新架构 | 线性时间复杂度O(n)的选择性状态空间模型，挑战Transformer地位 | [→ 报告](Pure-AI/2026-04-23-Mamba.md) |
| 5 | **Chain-of-Thought** | 2022 | 提示工程 | 在few-shot示例中加推理步骤，让100B+模型的数学推理提升30%+ | [→ 报告](Pure-AI/2026-04-23-Chain-of-Thought.md) |
| 6 | **LoRA** | 2021 | 高效微调 | 低秩矩阵分解把微调参数量减少99%，推理零开销，催生无数专用模型 | [→ 报告](Pure-AI/2026-04-23-LoRA.md) |
| 7 | **CLIP** | 2021 | 视觉语言 | 4亿图文对对比学习，零样本图像分类媲美监督训练，成为多模态AI基石 | [→ 报告](Pure-AI/2026-04-23-CLIP.md) |
| 8 | **Latent Diffusion Models** | 2022 | 图像生成 | 在VAE潜空间做扩散，计算量降低50倍，Stable Diffusion的技术基础 | [→ 报告](Pure-AI/2026-04-23-Latent-Diffusion-Models.md) |
| 9 | **InstructGPT / RLHF** | 2022 | 对齐 | SFT+奖励模型+PPO三阶段RLHF，1.3B胜175B，催生ChatGPT | [→ 报告](Pure-AI/2026-04-23-InstructGPT-RLHF.md) |
| 10 | **Mixtral of Experts** | 2024 | MoE架构 | 8专家选2的稀疏MoE，47B参数模型以12.9B的推理成本超越Llama 2 70B | [→ 报告](Pure-AI/2026-04-23-Mixtral-of-Experts.md) |

---

## 阅读建议

### 如果你是完全新手
先读这5篇，构建基础认知：
1. [Attention Is All You Need](Pure-AI/2026-04-23-Attention-Is-All-You-Need.md) — 理解现代AI的基础架构
2. [CLIP](Pure-AI/2026-04-23-CLIP.md) — 理解图文联合学习
3. [Chain-of-Thought](Pure-AI/2026-04-23-Chain-of-Thought.md) — 理解如何让AI推理
4. [LoRA](Pure-AI/2026-04-23-LoRA.md) — 理解如何高效使用大模型
5. [AlphaFold 3](AI4Health/2026-04-23-AlphaFold3.md) — 看AI如何改变科学研究

### 如果你对医疗AI感兴趣
推荐阅读顺序：
1. [Med-PaLM M](AI4Health/2026-04-23-Med-PaLM-M.md) — 先了解大图景
2. [LLaVA-Med](AI4Health/2026-04-23-LLaVA-Med.md) — 了解医学视觉语言模型
3. [MedSAM](AI4Health/2026-04-23-MedSAM.md) — 了解医学图像分割
4. [CONCH](AI4Health/2026-04-23-CONCH.md) — 了解病理AI
5. [Health-LLM](AI4Health/2026-04-23-Health-LLM.md) — 了解可穿戴AI

### 如果你对大模型技术感兴趣
推荐阅读顺序：
1. [Attention Is All You Need](Pure-AI/2026-04-23-Attention-Is-All-You-Need.md) — 基础架构
2. [InstructGPT / RLHF](Pure-AI/2026-04-23-InstructGPT-RLHF.md) — 对齐技术
3. [GPT-4](Pure-AI/2026-04-23-GPT-4-Technical-Report.md) — 能力上限
4. [Llama 3](Pure-AI/2026-04-23-Llama3.md) — 开源生态
5. [Mamba](Pure-AI/2026-04-23-Mamba.md) — 下一代架构探索

---

## 去重说明

本次推荐为仓库首次收录，所有20篇均为新增，无重复。
后续每日推荐将在本索引基础上进行去重检查。

---

*更新日期：2026-04-23*

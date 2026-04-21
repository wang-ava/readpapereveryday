# 每日论文推荐

每天推荐20篇值得读的论文：10篇 AI4Health 方向 + 10篇纯AI方向。每篇论文都有通俗易懂的中文报告，涵盖背景知识、核心方法、结论与局限性，适合新手快速入门。

---

## 文件命名规则

`保存日期-论文名称.md`

---

## 2026-04-21

### AI4Health 方向（10篇）

| 主题分类 | 论文 | 一句话概括 |
|---------|------|-----------|
| [蛋白质结构预测](./AI4Health/蛋白质结构预测/) | [AlphaFold2](./AI4Health/蛋白质结构预测/20260421-AlphaFold2.md) | 仅凭氨基酸序列预测蛋白质三维结构，解开生命科学50年难题 |
| [医学大语言模型](./AI4Health/医学大语言模型/) | [Med-PaLM 2](./AI4Health/医学大语言模型/20260421-Med-PaLM-2.md) | Google 医学专用大模型，USMLE 执照考试达到专家级水平 |
| [医学大语言模型](./AI4Health/医学大语言模型/) | [GPT-4 Medical](./AI4Health/医学大语言模型/20260421-GPT-4-Medical-Challenge.md) | GPT-4 不需专门训练，USMLE 准确率达87%，配合 Medprompt 达90%+ |
| [医学影像诊断](./AI4Health/医学影像诊断/) | [CheXNet](./AI4Health/医学影像诊断/20260421-CheXNet.md) | DenseNet 在11万张胸片上检测14种疾病，肺炎诊断超越医生平均 |
| [医学影像诊断](./AI4Health/医学影像诊断/) | [DeepMind 眼病AI](./AI4Health/医学影像诊断/20260421-DeepMind-Retinal-AI.md) | 两阶段可解释架构诊断50+种视网膜病变，达到顶级眼科专家水平 |
| [医学影像分割](./AI4Health/医学影像分割/) | [MedSAM](./AI4Health/医学影像分割/20260421-MedSAM.md) | 150万张医学图像微调 SAM，画框即可分割10种模态的医学影像 |
| [生物医学文本挖掘](./AI4Health/生物医学文本挖掘/) | [BioGPT](./AI4Health/生物医学文本挖掘/20260421-BioGPT.md) | 1500万篇 PubMed 文章预训练的生成模型，专攻生物医学文本理解 |
| [药物发现](./AI4Health/药物发现/) | [深度学习发现抗生素](./AI4Health/药物发现/20260421-Deep-Learning-Antibiotic-Discovery.md) | 图神经网络虚拟筛选1亿化合物，发现可对抗超级耐药菌的新抗生素 |
| [病理图像分析](./AI4Health/病理图像分析/) | [CONCH](./AI4Health/病理图像分析/20260421-CONCH.md) | 110万病理图文对训练的视觉-语言基础模型，自然语言驱动病理分析 |
| [联邦学习与医疗隐私](./AI4Health/联邦学习与医疗隐私/) | [联邦学习在医学中的应用](./AI4Health/联邦学习与医疗隐私/20260421-Federated-Learning-Medicine.md) | 多医院协作训练AI，数据不出院，脑肿瘤分割接近集中式训练水平 |

---

### 纯AI方向（10篇）

| 主题分类 | 论文 | 一句话概括 |
|---------|------|-----------|
| [Transformer架构](./AI/Transformer架构/) | [Attention Is All You Need](./AI/Transformer架构/20260421-Attention-Is-All-You-Need.md) | 只用注意力机制处理序列，完全并行训练，现代AI模型的祖先架构 |
| [Transformer架构](./AI/Transformer架构/) | [Vision Transformer (ViT)](./AI/Transformer架构/20260421-Vision-Transformer-ViT.md) | 把图片切成16×16小块当句子读，超大数据预训练后性能超越CNN |
| [预训练语言模型](./AI/预训练语言模型/) | [BERT](./AI/预训练语言模型/20260421-BERT.md) | 双向Transformer+完形填空预训练，开创预训练微调范式，11项NLP任务刷新最优 |
| [预训练语言模型](./AI/预训练语言模型/) | [GPT-3](./AI/预训练语言模型/20260421-GPT-3.md) | 1750亿参数，少样本上下文学习，规模带来涌现，ChatGPT 的前身 |
| [预训练语言模型](./AI/预训练语言模型/) | [LLaMA](./AI/预训练语言模型/20260421-LLaMA.md) | 开源大模型，1.4万亿 token 训练，13B参数超越175B GPT-3，开启开源AI大爆发 |
| [生成模型](./AI/生成模型/) | [DDPM](./AI/生成模型/20260421-DDPM.md) | 扩散模型：先加噪再去噪，训练稳定，生成质量超GAN，Stable Diffusion的理论基础 |
| [高效训练与微调](./AI/高效训练与微调/) | [LoRA](./AI/高效训练与微调/20260421-LoRA.md) | 冻结大模型权重，只训练低秩旁路矩阵，参数减少1万倍、性能媲美全量微调 |
| [高效训练与微调](./AI/高效训练与微调/) | [InstructGPT (RLHF)](./AI/高效训练与微调/20260421-InstructGPT-RLHF.md) | 三步RLHF框架让AI听话，13B模型用户体验超越1750B GPT-3，ChatGPT的技术基础 |
| [推理与规划](./AI/推理与规划/) | [Chain-of-Thought](./AI/推理与规划/20260421-Chain-of-Thought.md) | 在示例中加入推理步骤，让超大模型先"想"再回答，推理能力大幅提升 |
| [推理与规划](./AI/推理与规划/) | [ReAct](./AI/推理与规划/20260421-ReAct.md) | 推理和工具调用交织循环，AI Agent的核心范式：想一想、查一查、再回答 |

---

## 报告格式说明

每篇报告包含：
- 📎 论文链接
- 🌍 背景知识（新手必读）
- 🎯 论文干了什么
- 🔧 怎么做到的
- ✅ 结论
- ⚠️ 局限性

---
draft: false
title: Brief Summary of Qwen Models
description: Summary of Qwen2 and Qwen 2.5 Models
date:
    created: 2025-02-02
    updated: 2025-02-02
tags:
    - NLP
    - LLM
    - Research_Papers
---

# Brief Summary of Qwen2 and Qwen 2.5 Models
<!-- more -->


## Introduction - Qwen2
Qwen Team is part of Alibaba Group based in China. Qwen2 Technical Report was released in Sep 2024 along with Qwen2 series of models. Qwen2 models are Large Langue Models (LLMs) trained using the **next-token prediction** and mostly follows the **decoder only transformer architecture**. This series include 4 dense models (all parameters acre activated during inference) of sizes 0.5B, 1.5B, 7B and 72B along with a Mixture of Experts (MoE) model of 57B parameters, of which 14B are activated for each token during inference.

Models were trained on large scale dataset containing & trillion tokens. It also included enhanced quality and quantity fo code and mathematics content. Authors hypothesize that enhancement in data led to improved reasoning abilities of the models. 

For post-training, models underwent Supervised Fine-Tuning (SFT) and Direct Preference Optimization (DPO) to align them with human preference and learn form human feedback.

### Tokenizer and Model details
Tokenizer used is based on byte-level byte-pair encoding. Vocabulary consists of 151643 regular tokens and 3 control tokens.

Key differences in the Qwen model architecture are following:

- **Groped Query Attention**
Model uses Grouped Query Attention (GQA) instead of usual Multi-Headed Attention. GQA optimizes QV cache during inference.

- **Dual Chunk Attention (DCA)**
DCA enables model to break long sequences into chunks. It helps in increasing the context length that model can handle. If input fits within a chunk, DCA produces same output as self-attention. If input spans multiple chunks, DCA captures relative positional information between tokens within and across chunks.

- **YARN**
Qwen2 models use YARN to rescale attention weights for better length extrapolation

- Models use **SwiGLU activation**, **RoPE** for positional embedding, **QKV bias** for attention and **RMSNorm** plus pre-normalization to stabilize model training.

### Pre-Training
- Heuristics based as well as LLM based methods utilizing prior version of Qwen models was used to filter out low-quality data.
- LLMs were also used to synthesize high-quality pre-training data.
- Pre-training data was expanded form 3 trillion tokens in Qwen1.5 model to **7 trillion**. It included high quality code, mathematics and multilingual datasets.
- High quality multi-task instruction data was utilized in pre-training stage to enhance in-context learning and instruction-following abilities.
- Context length of **4096 to 32,768 tokens** was during pre-training.
- With help from DCA and YARN, models can effectively handles sequences up to 131,072 tokens.
- Pre-training was performed using Causal Language Modeling (next word prediction) objective.

### Post-Training
- Post-training ensures model's output is aligned with human values and human-preferences.
- Post-training focuses on scalable alignment with minimal human annotation.
- Post-training data consists of two parts:
    - **Demonstration Data for SFT:** D = {(x<sub>i</sub>, y<sub>i</sub>)}
    - **Preference Data for RLHF:** P = {(x<sub>i</sub>, y<sub>i</sub><sup>+</sup>,  y<sub>i</sub><sup>-</sup>)}

- Demonstration data consists of instruction and response pairs.
- Preference data includes instruction and two responses where one response is preferred over the other.

- Post-training data was built in two stages:
    1. **Collaborative Annotation**
    2. **Automated Data Synthesis**

- For collaborative annotation, authors first generated diverse, high-quality instructions from large instruction corpus. Then through human annotation, response y<sub>i</sub> and preference responses  y<sub>i</sub><sup>+</sup> and  y<sub>i</sub><sup>-</sup> are generated.

- By prompting Qwen models, authors added constraints/requirements to existing instructions to increase their complexity and add diverse difficulty levels.

- By prompting Qwen model, authors generated multiple responses to a given instruction using diverse generation strategies, which then were annotated by human annotator for preference ranking.

- To increase the size of instruction dataset, authors implemented multiple strategies to automatically synthesize high quality data. 
    - **Rejection Sampling:** LLMs generate multiple responses for a given instruction. Responses considered reasonable by LLM model are kept. Preference data is gathered using contrasting responses.
    - **Execution Feedback:** For coding tasks, LLMs generate solution and test cases for a given instruction. Then solution is compiled and executed against test cases. 
    - **Data Repurposing:** High quality literature is given to LLMs to generate instructions and responses of various level of details.
    - **Constitutional Feedback:** Constitutional AI refers to the process of guiding LLMs to generate responses based on predefined set of principles. To ensure model aligns with human values, a constitution dataset was built. Dataset includes what principles to follow and what to avoid. This dataset was used for creating responses which follow and deviate from the constitution and compiled into preference dataset. 

- Using these methods, authors have amassed a large **instruction dataset of ~500K samples**, covering skills like instruction following, coding, mathematics, logical reasoning, role-playing, multilingualism and safety.

- Model was fine-tuned for two epochs with sequence length of 32,768 tokens. Learning rate was gradually reduced from 7 x 10<sup>-6</sup> to 7 x 10<sup>-7</sup>. To avoid overfitting weight decay was set to 0.1 and gradients were clipped at maximum value of 1.0.

- For RLHF training, model used two stages:
    - **Offline Stage:** Model was fine-tuned on offline preference dataset using DPO.
    - **Online Stage:** Model was fine-tuned using online reward model for immediate feedback. Model generated multiple responses by sampling current policy and reward model selected most and least preferred responses forming preference pairs using by DPO for each episode. Model used Online Merging Optimizer to avoid reduction in model performance due to alignment aka alignment tax.

### Evaluation Summary
_For detailed comparison across benchmarks and other models, please refer to the technical report linked in references._

- Qwen2 models show improvements over prior model versions in both core LLM capabilities as well as instruction following abilities.
- Data scaling and high quality data during pre-training stage helps in enhancing model performance for models across parameter sizes.

## Qwen2.5 Models - What changed from Qwen2?

Qwen2.5 models were released in Dec 2024. The models see improvement in the pre-training corpus and supervised fine-tuning corpus over the Qwen2 model series. Qwen2.5 models include variants 0.5B, 1.5B, 3B, 7B, 14B, 32B, 72B and a MoE model via API Qwen2.5-Turbo and Qwen2.5-Plus.

Qwen2.5 models support **larger 8K generation length** (compared to 2K generation lenght in Qwe2) and improve on structured input and output support along with tool-use.

### Tokenizer and Model details
Qwen2.4 models use **Byte-level Byte-Pair Encoding (BBPE) tokenizer** (same as Qwen2 series) with 151,643 vocabulary size. Qwen2.5 models use **22 control tokens** (as compared to 3 control tokens in Qwen2 series). These new tokens aide tool functionality and other model capabilities.

### Pre-training


### Post-training


### Evaluation
_For detailed comparison across benchmarks and other models, please refer to the technical report linked in references._

To prevent test data leakage, contaminated samples are identified using the n-gram matching and identified samples are removed from the training set. Train sample s<sub>t</sub> is removed if there exists a test sample s<sub>e</sub> which satisfies both of the following conditions:

- |LCS(s<sub>t</sub>, s<sub>e</sub>)| >= 13
- |LCS(s<sub>t</sub>, s<sub>e</sub>)| >= 0.6 x min(|s<sub>t</sub>|, |s<sub>e</sub>|)

LCS: Longest Common Subsequence

Qwen2.5 models show significant improvements across all benchmarks over Qwen2 models across model sizes. Same also holds for instruction tuned variants. 

Qwen2.5 0.5B, 1.5B, 3B also show significant performance gains making them suitable for edge use-cases.

### Evaluation of Reward Model
Reward model was assessed on Reward Bench, RMB and PPE benchmarks. Llama-3.1-Nemotron-70B-Reward performs best on Reward Bench, while Qwen2.5-RM-72B ranks first on PPE and second on RMB.

### Reference
- [Qwen2 Technical Report](https://arxiv.org/abs/2407.10671)
- [Qwen2.5 Technical Report](https://arxiv.org/abs/2412.15115)

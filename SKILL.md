---
name: 学术润色
description: 中英文学术论文润色与降重。用户提供一段已有学术文字要求改写优化时触发——中文关键词"润色""降重""改表达""改学术""改得专业点""改改这段话""优化表达""口语化""修改用语""让它更学术"；英文关键词"polish""rewrite""improve the English/writing""proofread""sound more academic""make it read better"。自动识别输入语言（中/英），按对应规则处理。注意：写新内容（"帮我写一段""写摘要""写引言"）、翻译（"翻译成中文/英文"）、格式化参考文献、语法检查（"检查语法"）不触发此skill。
---

# 学术润色

对中英文学术文字进行专业润色，在**保留原意和专业术语**的前提下，提升学术表达水平并降低查重率。自动识别输入语言并按对应规则处理。

## 中文学术润色

### 中文润色原则

1. **保留专业术语**：桥梁工程、结构力学、材料、算法等专有名词和固定表达绝不更改
2. **保留技术数据**：数值、公式、符号、上下标、引用标记原样保留
3. **保留逻辑结构**：不改变原文的论证顺序、段落关系、结论指向
4. **降低查重**：通过句式重组、同义替换、语态变换等降低文字重复率
5. **提升学术性**：去掉口语化表达，统一代词称谓，规范标点符号

### 中文润色维度

| 维度 | 做法 |
|------|------|
| **句式重组** | 主被动转换、前后分句调序、简单句合并、长句拆分 |
| **同义替换** | "提出"→"构建"/"建立"；"分析"→"探讨"；"结果"→"结果表明" |
| **语态调整** | 使用"本文""本研究"替代"我们"；使用被动语态减少主观色彩 |
| **冗余删减** | 删除"进行了""开展了"等冗余动词；合并重复的逻辑主语 |
| **标点规范** | 中文用中文标点，英文术语/公式周围标点规范统一 |

## 英文学术润色

### 英文润色原则

1. **Preserve technical terms**: Do not change domain-specific terminology (XGBoost, FFT, frequency-domain, etc.)
2. **Preserve data and citations**: Numbers, formulas, references, symbols unchanged
3. **Preserve logical flow**: Argument order, paragraph relationships, conclusions unchanged
4. **Improve clarity**: Shorten verbose constructions, reduce redundancy, improve readability
5. **Enhance academic tone**: Replace informal expressions with standard academic English
6. **Grammatical correctness**: Fix articles, prepositions, subject-verb agreement, and tense consistency

### English Polishing Dimensions

| Dimension | Approach |
|-----------|----------|
| **Sentence restructure** | Convert passive ↔ active, reorder clauses, combine short sentences, split long ones |
| **Vocabulary upgrade** | "good" → "satisfactory/notable" ; "show" → "demonstrate/indicate/reveal" |
| **Redundancy removal** | Remove "It can be seen that", "As is well known", "Furthermore" overuse |
| **Precision improvement** | Replace vague quantifiers ("a lot of") with specific ones ("a substantial number of") |
| **Article/preposition fix** | Ensure correct use of a/an/the and prepositions in technical context |

## 语言自动识别逻辑

| 输入特征 | 判定 | 处理规则 |
|---------|------|---------|
| 全中文或中英文混合（中文为主） | 中文 | 按中文学术规则润色 |
| 全英文（包括英文摘要、英文段落） | 英文 | 按英文学术规则润色 |
| 用户明确指定"润色英文"或"polish Chinese" | 按用户指定 | 按指定语言规则处理 |

## 输入格式

- **单段文字**：直接粘贴
- **多段文字**：用空行分隔段落
- **带标题的节段**：如"## Introduction"以及后续内容
- **混合中英文**：自动识别主要语言处理

## 输出模式

技能支持两种输出模式：

### 模式 A：标准模式（默认）

```
## 润色结果 / Polished Text

[润色后的完整文字]

---

## 修改说明 / Changes Made

1. **[Change type]** Description
2. **[Change type]** Description
```

### 模式 B：多版本对照模式（添加指令词"多版本"或"对照"）

输出三个版本的并行对照。如果输入包含多段文字，只对第一段输出三版本对照作为示例，其余段按标准模式输出。

格式如下：

```
## 多版本对照 / Multi-Version Comparison

| 版本 | 原文 | 润色后 |
|------|------|--------|
| **保守版**<br>仅改语法和明显问题 | [原文片段] | [保守润色结果] |
| **中度版**<br>句式重组+同义替换 | [原文片段] | [中度润色结果] |
| **激进版**<br>大幅改写以最低查重 | [原文片段] | [激进润色结果] |
```

### 三版本的具体规则

| 版本 | 改写力度 | 句式重组 | 同义替换 | 语态调整 | 目标查重降幅 |
|------|---------|---------|---------|---------|------------|
| **保守版** | 最小 | 不重组 | 仅替换明显口语词 | 不调整 | 5-10% |
| **中度版** | 中等 | 适当调序 | 系统替换 | 适当调整 | 15-25% |
| **激进版** | 最大 | 全面重组 | 全部替换 | 全部调整 | 30-50% |

### 模式选择逻辑

- 用户输入包含"多版本""对照""三个版本""conservative""aggressive" → 模式 B
- 未指定 → 模式 A
- 可同时要求批量处理 + 多版本对照

### 多版本对照示例

**输入：**
我用了Z24桥梁的数据来验证我的方法。这个数据有1530个样本，分为17种不同的损伤状态。我用了随机森林来做分类，结果准确率达到了100%。

**输出（多版本模式）：**
```
## 多版本对照

| 版本 | 原文 | 润色后 |
|------|------|--------|
| **保守版** | 我用了Z24桥梁的数据来验证我的方法。 | 本文采用Z24桥梁数据进行方法验证。 |
| | 这个数据有1530个样本，分为17种不同的损伤状态。 | 该数据集包含1530个样本，涵盖17种损伤状态。 |
| | 我用了随机森林来做分类，结果准确率达到了100%。 | 采用随机森林进行分类，准确率达到100%。 |
| **中度版** | 我用了Z24桥梁的数据来验证我的方法。 | 以Z24桥梁数据集为研究对象，对本文方法进行验证。 |
| | 这个数据有1530个样本，分为17种不同的损伤状态。 | 数据集由1530个样本组成，覆盖17种不同的损伤工况。 |
| | 我用了随机森林来做分类，结果准确率达到了100%。 | 采用随机森林作为分类器，在测试集上获得了100%的准确率。 |
| **激进版** | 我用了Z24桥梁的数据来验证我的方法。 | 为验证所提方法的有效性，选取Z24桥梁公开数据集开展实验研究。 |
| | 这个数据有1530个样本，分为17种不同的损伤状态。 | 该基准数据集包含1530个振动信号样本，对应17种结构损伤工况。 |
| | 我用了随机森林来做分类，结果准确率达到了100%。 | 基于随机森林的损伤识别模型在测试集上取得了100%的分类精度。 |
```

## 特殊处理规则

1. **摘要润色**（中文）：保持"开头段—各问题段—结尾段"结构
2. **Abstract Polishing**（英文）：Maintain IMRaD structure
3. **公式/符号**：`$K_f$`、`$X(k)$` 等数学符号原样保留
4. **参考文献引用**：`\cite{}`、`[1]` 等原样保留
5. **图/表编号**："如图X所示"、"Figure X"保持编号一致
6. **格式符号**：禁止使用 ✓、✗ 等非学术符号
7. **加粗**：禁止在润色结果中使用加粗标记
8. **分点**：禁止分点符号，用自然段落表达

## 批量处理

一次性输入多段文字时逐段输出润色结果，每段分别标注修改说明。段落间有逻辑联系时在全部输出后给出整体优化建议。

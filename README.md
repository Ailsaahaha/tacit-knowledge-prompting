# Tacit Knowledge Prompting · 默会知识提示

> 让 AI 说出它「说不清但就是知道」的那部分。

作者：**Ailsaahaha** · [GitHub](https://github.com/Ailsaahaha) · [ailamemo.com](https://www.ailamemo.com)

[English below](#english)

## 问题

问 AI 一个问题，拿到的答案常常**正确但没用**。

因为它给的都是**说得出来的**那部分——数据、定义、教科书式的分析。而真正值钱的判断，往往在**说不出来**的那层：经验、直觉、情境感、「我知道但说不清为什么」。

## 这是什么

基于波兰尼（Michael Polanyi）1958 年《个人知识》的核心论断：

> **我们知道的比能说出来的多。**（We know more than we can tell.）

你能一眼认出母亲的脸，但说不清是怎么认出来的；老司机能感觉方向盘「不对劲」，但指不出是哪里。这种**经验性、内化、依赖情境、无法完全言传**的知识，叫**默会知识**（tacit knowledge）。

这个 skill 把该理论迁移到提示词：**让 AI 不只给显性答案，再往下调用一层「我知道但说不清」的判断。**

## 快速开始

在你的提示词末尾加上这段：

```
请按波兰尼的默会知识两层回答：
1. 显性层：你能直接说出来的（数据、定义、可验证的推理）
2. 默会层：你「知道但说不清」的部分——经验判断、直觉、情境感

不要回避默会层。那才是真正的判断。
说不清就说「说不清」，不要硬编一个理由。
```

### 三个模板

<details>
<summary><b>1. 判断类</b>（该不该做 / 值不值）</summary>

```
[你的问题]

请按波兰尼的默会知识两层回答：
1. 显性层：你能直接说出来的（数据、定义、可验证的推理）
2. 默会层：你「知道但说不清」的部分——经验判断、直觉、情境感

不要回避默会层。那才是真正的判断。
说不清就说「说不清」，不要硬编一个理由。
```
</details>

<details>
<summary><b>2. 风格类</b>（像人还是像 AI）</summary>

```
[一段文字]

请判断它的「人味」在哪里：
1. 显性层：结构、用词、信息密度——这些可以分析
2. 默会层：它读起来像不像一个**有经验的人**写的？
   那种「经历过所以知道」的质感，说不出是哪一句带来的，但就是有。

如果缺人味，请指出默会层缺的是什么。
```
</details>

<details>
<summary><b>3. 经验类</b>（哪个会爆 / 哪个不会）</summary>

```
[几个候选选项]

请给出两层判断：
1. 显性层：每个选项的数据、竞争度、可验证的优劣
2. 默会层：如果你是一个在这个领域泡了很久的老手，
   你的直觉选哪个？理由可能说不清，但请把那个「感觉」说出来。

明确标注：默会层的判断不保证对，请说明你为什么有这个感觉。
```
</details>

## 效果对比（真实案例）

**问题**：3 个候选选题 ① 牙线怎么用 ② 智齿要不要拔 ③ 洗牙一次多少钱，哪类更可能爆？

**只问一层（普通回答）**：

> 牙线搜索量高但竞争激烈；智齿搜索中等、长尾好；洗牙价格搜索意图明确但内容少。建议优先做牙线。

**两层回答（本 skill）**：

> **显性层**：① 牙线搜索量高但内容同质严重；② 智齿搜索中等，关键词分散；③ 洗牙价格搜索意图明确但内容少。
>
> **默会层**：直觉上**智齿那条更可能爆**。理由说不清，但感觉是——智齿话题带「个人故事」属性（拔过/没拔过/什么时候拔），读者读到会想到「我朋友」或「我自己」。牙线是工具型，洗牙是消费决策型（直接搜价格的人已经决定了）。**带故事属性的话题更容易触发「转给朋友」这个动作。**
>
> 但这是我看了大量内容的感觉，**不一定每次都对**——建议优先智齿，同时把牙线做出来当对照组。

差别就在第二层。第一层是数据，第二层是「说不出为什么但就是觉得对」。

## 安装

把 `SKILL.md` 放到你的 Agent skills 目录即可：

- **WorkBuddy / CodeBuddy**：`~/.workbuddy-ai/skills/tacit-knowledge-prompting/SKILL.md`
- **Claude Code**：`.claude/skills/tacit-knowledge-prompting/SKILL.md`
- **Cursor / Codex**：对应项目的 skills 目录

装完以后，直接说「按波兰尼两层想一下」就能调用。

也可以不安装，只复制上面的模板直接用。

## 注意事项

1. **默会层不保证对。** 它是数据之外的补充信号，不是替代品。
2. **说不清就说不清。** 如果 AI 硬编一个假装深刻的理由，那是在表演。真实特征是**承认不确定性**。
3. **配对照组。** 单靠默会层下注风险高，最好同时留一个显性层推荐的选项。
4. **两层一起看。** 一致 → 信心高；冲突 → 那个冲突点往往才是最有意思的地方。

**不适用的场景**：纯事实查询、代码调试、需要精确数字的任务——这些只要显性层。

---

## English

A prompting technique based on Michael Polanyi's *Personal Knowledge* (1958):

> **We know more than we can tell.**

Most LLM answers stay in the **explicit layer** — data, definitions, textbook reasoning. But the judgment that actually matters often lives in the **tacit layer**: experience, intuition, situational feel — the part you know but can't fully articulate.

This skill asks the model to output **both layers**, and explicitly forbids skipping the second one.

**The prompt:**

```
Answer in Polanyi's two layers:
1. Explicit: what you can directly state — data, definitions, verifiable reasoning
2. Tacit: what you "know but can't fully say" — judgment, intuition, situational feel

Do not skip the tacit layer. That's where the real judgment is.
If you can't articulate it, say "I can't articulate it" — don't invent a reason.
```

Three templates included: **judgment** (should I / is it worth it), **style** (does this read like a human), **experience** (which one will take off). See `SKILL.md` for all three plus a worked example.

**Caveat:** the tacit layer is a signal, not a substitute for data. Always pair it with a control option.

**Author:** Ailsaahaha ([@Ailsaahaha](https://github.com/Ailsaahaha))

## License

MIT — 随便用，改署名也行。

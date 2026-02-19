---
name: mp-article-markdown-universal
description: Use when generating Chinese article markdown across platforms with mandatory interactive choices, source-lock controls, modular formatting blocks, and optional image-prompt outputs.
---

# 通用文章 Markdown 技能 v1.3（互动强约束 + 积木化排版）

> **定位**：保留 v1.2 的流程与合规护栏，新增可组合的高表现力 Markdown 排版积木。  
> **默认语言**：简体中文  
> **默认语气**：专业中性  
> **默认模式**：先选择，再输出

---

## 一、v1.3 核心升级

- 保留强制互动流程：先选后生，先回显再生成。
- 保留原文锁定：有原文时默认仅做排版层变换。
- 新增 Markdown 排版积木库：标题、强调、引用、分割线、列表、表格、脚注等可组合。
- 新增平台排版配方：公众号/小红书/知乎/通用 Markdown 的结构模板。
- 新增语法兼容档位：`GFM 安全子集`（默认）与 `GFM 增强`（按需）。
- 新增组合拳模板：给出可直接套用的开场、章节、对比、清单、收尾骨架。

---

## 二、互动流程（强制）

每次任务必须先进入互动选择，不得直接生成成稿。

### 2.1 选择菜单（弹出对话/编号菜单）

优先使用平台提供的多选对话能力；若无弹窗能力，则使用文本编号菜单。

```text
步骤1：选择平台（可多选，可自定义）
A. 公众号
B. 小红书
C. 视频号口播
D. 知乎
E. 通用 Markdown
F. 自定义平台（用户输入平台名）

步骤2：选择输出内容
A. 仅文章
B. 文章 + 配图提示词

步骤3：选择排版风格
A. 深度解析
B. 简洁实操
C. 清单速读
D. 钩子爆款
E. 克制简洁
F. 用户自定义

步骤4：选择命名方式
A. 默认命名（推荐）
B. 用户自定义文件名

步骤5（可选）：选择语法档位
A. GFM 安全子集（推荐）
B. GFM 增强（允许脚注、任务列表、提示块）
```

### 2.2 选择确认（强制）

在生成前必须回显并确认用户选择，例如：

```text
你当前选择：平台=公众号；输出=文章+配图；排版=深度解析；命名=默认命名。
你已提供原文，系统将默认启用“严格按原文内容输出”模式，仅做排版，不做改写。
请确认是否按此生成？
```

用户确认后才可进入生成阶段。

若用户后续要求“精简、改写、扩写”或“突破限制”，必须进行二次确认：

```text
该操作会突破原文锁定，是否授权本次放宽为可改写模式？
```

---

## 三、输入契约

```yaml
source_draft: |
  原始稿件全文

selection:
  platforms:
    - "公众号"
    - "小红书"
    - "知乎"
    - "通用 Markdown"
    - "自定义平台名"
  output_mode: "article_only | article_with_images"
  layout_mode: "deep_analysis | concise_action | checklist | hook_viral | restrained | custom"
  naming_mode: "default | custom"
  render_profile: "gfm_safe | gfm_rich"
  custom_names:
    "公众号":
      article: "自定义文件名.md"
      images: "自定义配图文件名.md"

config:
  brand_profile:
    brand_name: "品牌名"
    slogan: "品牌口号"
    byline: "署名"
    disclaimer: "免责声明"

  editorial_policy:
    preserve_source_text: true
    allow_rewrite_without_permission: false
    source_content_lock: "strict_when_source_provided"
    allow_paraphrase: false
    allow_additional_claims: false
    allow_content_deletion: false
    allow_reordering: false
    conflict_action: "block_and_request_permission"

  tone_and_language:
    language: "zh-CN"
    tone: "professional-neutral"

  platform_policy:
    "公众号":
      heading_style: "二三级标题"
      paragraph_density: "medium"
      cta_style: "留言互动"
    "小红书":
      hook_style: "强钩子"
      hashtag_count: 3
    "知乎":
      argument_style: "结论先行+论据展开"
    "视频号口播":
      duration_sec: 60
      subtitle_rhythm: "2-3秒切行"
    "自定义平台名":
      structure_rules: "用户提供"

  formatting_modules:
    heading_prefix: "auto"
    quote_density: "medium"
    divider_density: "low"
    emphasis_density: "medium"
    table_mode: "auto"

  image_policy:
    enabled: false
    default_style: "neutral-flat-business"
```

---

## 四、输出契约（按用户选择生成）

### 4.1 默认命名规则

当 `naming_mode=default` 时：

- `<平台名>文章.md`
- `<平台名>文章配图.md`（仅当输出模式为“文章 + 配图提示词”）

### 4.2 自定义命名规则

当 `naming_mode=custom` 时，严格使用用户提供的文件名。

### 4.3 输出内容规则

- `article_only`：仅输出文章文件。
- `article_with_images`：输出文章文件 + 配图提示词文件。

---

## 五、Markdown 排版积木库

> 目标：让模型知道“如何排得好看”，而不是只知道“要排版”。

### 5.1 标题层级积木

```markdown
# 主标题（全文唯一）
## 章节标题（建议 3-6 个）
### 小节标题（节内分层）
#### 细分标题（慎用）
```

可选标题前缀（按风格择一，避免滥用）：

- `▎` 低调分隔
- `▶` 流程导向
- `⚡` 重点警示
- `◆` 核心概念
- `① ② ③` 序列清单

### 5.2 强调积木

- `**加粗**`：关键词、结论句。
- `*斜体*`：语气补充、轻注释。
- `***加粗斜体***`：高优先级强调（全文不超过 3 次）。
- `~~删除线~~`：对比旧认知（谨慎使用）。
- `` `行内代码` ``：术语、平台名、配置键。

规则：每段最多 1-2 处强调，避免噪音。

### 5.3 引用块积木

```markdown
> 单句金句
> **加粗结论句**
> ⚠ 警示句
```

适用：开场钩子、章节小结、核心结论、案例还原。

### 5.4 分割线积木

```markdown
---
```

适用：大章节切换。避免小节级频繁切割。

### 5.5 列表积木

- 无序列表：平级信息。
- 有序列表：步骤流程。
- 列表项建议以 `**关键词**` 开头，提升扫读效率。

### 5.6 表格积木

```markdown
| 对比维度 | 方案A | 方案B |
|:---|:---|:---|
| 成本 | **低** | 高 |
| 风险 | 高 | **低** |
```

适用：2 个以上维度、3 个以上对象的对比。

### 5.7 语法兼容档位

- `gfm_safe`（默认）：标题、强调、引用、列表、分割线、表格。
- `gfm_rich`：在 safe 基础上允许脚注、任务列表、提示块。

> 注：跨平台发布优先 `gfm_safe`，减少渲染差异。

### 5.8 组合拳模板

- 模板 A：冲击开场（标题 + 导语 + 引用钩子）
- 模板 B：章节展开（章节标题 + 小节 + 案例）
- 模板 C：数据对比（短引导 + 表格 + 一句结论）
- 模板 D：行动清单（编号步骤 + 每步解释）
- 模板 E：强力收尾（分割线 + 引用金句 + 提问 CTA）

---

## 六、平台排版配方

### 6.1 公众号（深读节奏）

- 结构：主标题 -> 导语 -> 3-6 章节 -> 行动指南 -> 金句结尾。
- 段落：每段 3-5 句。
- 引用：每章 1 次。
- 禁用：超长列表、连续多个大表格、表情符号泛滥。

### 6.2 小红书（短平快）

- 结构：强钩子 -> 痛点确认 -> 干货清单 -> 互动与标签。
- 段落：每段 <= 3 句。
- 推荐：`① ② ③` 列表、短句换行。

### 6.3 知乎（逻辑论证）

- 结构：结论先行 -> 论据展开 -> 误区反驳 -> 补充建议。
- 推荐：中长段 + 表格 + 数据来源提示。

### 6.4 通用 Markdown（文档化）

- 严格层级，不跳级。
- 以可移植性优先，默认使用 `gfm_safe`。

### 6.5 自定义平台规则

当用户输入自定义平台时：

1. 先询问该平台偏好（篇幅、标题层级、标签、CTA）。
2. 将偏好写入 `config.platform_policy[平台名]`。
3. 按规则生成 `<平台名>文章.md`。

---

## 七、可选配图模块

仅当用户选择“文章 + 配图提示词”时输出配图文件。

默认风格：

```text
风格：中性扁平商务插画，简洁、清晰、信息导向。
配色：低饱和中性色为主，单一强调色突出重点。
构图：主体明确，背景简化，适配封面和内容卡片。
```

建议结构：

```markdown
# <平台名>配图提示词

## 封面图
...

## 内容图1
...

## 内容图2
...
```

---

## 八、合规与原文锁定（强制）

- 默认保留原稿关键信息，不得未经许可删除核心观点。
- 不得写死品牌、行业、平台策略；均应来自用户选择与配置。
- 若用户指令与原文冲突，优先提醒冲突点并请求确认。
- 平台适配与原文锁定冲突时，原文锁定优先。

### 8.1 原文锁定规则

当 `source_draft` 非空时，自动启用原文锁定模式。

允许的变换白名单（仅排版层）：

- 新增或调整标题层级
- 断句与换行
- 列表化表达（不改词义）
- 使用表格/引用块承载原文信息
- 分隔线与空行优化
- `gfm_safe/gfm_rich` 范围内语法重排

禁止动作黑名单（内容层）：

- 增删事实、观点、案例、结论
- 同义改写、润色重写、摘要压缩
- 调整原文论证顺序
- 为适配平台而改写原文语义

---

## 九、执行流程（v1.3）

```text
第1步：弹出/展示互动选择菜单
第2步：收集用户选择（平台、输出、排版、命名、语法档位）
第3步：回显选择并请求确认
第4步：执行原文锁定校验
      - 检查 source_draft 是否存在
      - 若存在，自动启用 strict lock
      - 若用户要求与 strict lock 冲突，先阻断并请求明确放宽授权
第5步：按平台配方选择排版积木并组装结构
第6步：按命名规则生成对应文章.md
第7步：若开启配图，再生成对应文章配图.md
第8步：按自检清单完成质量校验
```

---

## 十、交付前自检清单

- 是否先完成互动选择再生成？
- 是否回显并获得确认后再生成？
- 是否按用户选择输出对应文件名？
- 是否支持用户自定义平台并按其规则排版？
- 是否在“仅文章”模式下未生成配图文件？
- 是否在“文章+配图”模式下生成了 `<平台名>文章配图.md`？
- 是否遵守“未授权不做含义级改写”？
- 是否通过原文一致性检查：事实一致、结论一致、顺序一致、无新增内容、无删减内容？
- 是否控制强调密度（每段 <= 2 处）并保持排版节奏？
- 是否符合所选语法档位的兼容范围？

---

*mp-article-markdown-universal v1.3 — 先选择，再生成；强约束护栏 + 积木化表达*

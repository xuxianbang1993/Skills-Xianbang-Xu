---
name: mp-article-markdown-universal
description: Use when generating cross-domain article markdown with interactive user choices, customizable platform formatting rules, and optional image-prompt outputs.
---

# 通用文章 Markdown 技能 v1.2（互动式 + 原文锁定）

> **定位**：通过互动选择生成文章排版，支持平台自由定制  
> **默认语言**：简体中文  
> **默认语气**：专业中性  
> **默认模式**：先选择，再输出

---

## 一、核心能力

- 互动式选择：先让用户选平台、排版、是否配图，再生成。
- 平台自由定制：平台不限于预设，可由用户自定义。
- 输出按选择命名：根据用户勾选结果输出对应 `.md` 文件。
- 跨领域通用：教育、职场、消费、科技、商业、财税等均可用。
- 原文严格一致：用户已提供原文时，只允许排版层变换，不允许内容层改写。

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
D. 自定义平台（用户输入平台名）

步骤2：选择输出内容
A. 仅文章
B. 文章 + 配图提示词

步骤3：选择排版风格
A. 深度解析
B. 简洁实操
C. 清单速读
D. 用户自定义

步骤4：选择命名方式
A. 默认命名（推荐）
B. 用户自定义文件名
```

### 2.2 选择确认

在生成前必须回显并确认用户选择，例如：

```text
你当前选择：平台=公众号；输出=文章+配图；排版=深度解析；命名=默认命名。
你已提供原文，系统将默认启用“严格按原文内容输出”模式，仅做排版，不做改写。
请确认是否按此生成？
```

用户确认后才可进入生成阶段。

若用户后续要求“精简、改写、扩写”，必须进行二次确认：

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
    - "自定义平台名"
  output_mode: "article_only | article_with_images"
  layout_mode: "deep_analysis | concise_action | checklist | custom"
  naming_mode: "default | custom"
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
    "视频号口播":
      duration_sec: 60
      subtitle_rhythm: "2-3秒切行"
    "自定义平台名":
      structure_rules: "用户提供"

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

### 4.2 命名示例

- 选择：公众号 + 仅文章  
  输出：`公众号文章.md`

- 选择：公众号 + 文章+配图  
  输出：`公众号文章.md`、`公众号文章配图.md`

- 选择：小红书 + 文章+配图  
  输出：`小红书文章.md`、`小红书文章配图.md`

- 选择：自定义平台“知乎专栏” + 仅文章  
  输出：`知乎专栏文章.md`

- 选择：公众号 + 小红书 + 文章+配图  
  输出：
  `公众号文章.md`、`公众号文章配图.md`、`小红书文章.md`、`小红书文章配图.md`

### 4.3 自定义命名规则

当 `naming_mode=custom` 时，严格使用用户提供的文件名。

---

## 五、排版生成规则

### 5.1 共同基础（所有平台）

- 标题清晰，导语先给价值点。
- 段落分层，不堆砌长段。
- 用表格/清单/引用块呈现复杂信息。
- 用户提供原文时，必须保持事实、结论和论证顺序一致。
- 未授权不得做含义级改写。

### 5.2 预设平台规则

#### 公众号

- 适合深读：二级/三级标题分层。
- 每节末尾给小结或过渡。
- 结尾附互动提问与品牌署名。

#### 小红书

- 开头 1-2 句必须有钩子。
- 短段落、高密度可执行点。
- 结尾含互动问题 + 话题标签位。

#### 视频号口播

- 使用脚本体结构：开场钩子、问题、方法、案例、CTA。
- 默认 60 秒节奏，并附字幕切分建议。

### 5.3 自定义平台规则

当用户输入自定义平台时：

1. 先询问该平台的结构偏好（篇幅、标题层级、是否标签、CTA 形式）。
2. 将用户偏好写入 `config.platform_policy[平台名]`。
3. 按该规则生成 `<平台名>文章.md`。

---

## 六、可选配图模块

仅当用户选择“文章 + 配图提示词”时才输出配图文件。

默认风格：

```text
风格：中性扁平商务插画，简洁、清晰、信息导向。
配色：低饱和中性色为主，单一强调色突出重点。
构图：主体明确，背景简化，适配封面和内容卡片。
```

配图文件内容按平台区分组织，建议结构：

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

## 七、合规与约束（强制）

- 默认保留原稿关键信息，不得未经许可删除核心观点。
- 不得写死品牌、行业、平台策略；均应来自用户选择与配置。
- 若用户指令与原文冲突，优先提醒冲突点并请求确认。
- 平台适配与原文锁定冲突时，原文锁定优先。

### 7.1 原文锁定规则（新增）

当 `source_draft` 非空时，自动启用原文锁定模式。

允许的变换白名单（仅排版层）：

- 新增或调整标题层级
- 断句与换行
- 列表化表达（不改词义）
- 使用表格/引用块承载原文信息
- 分隔线与空行优化

禁止动作黑名单（内容层）：

- 增删事实、观点、案例、结论
- 同义改写、润色重写、摘要压缩
- 调整原文论证顺序
- 为适配平台而改写原文语义

---

## 八、执行流程（最终版）

```text
第1步：弹出/展示互动选择菜单
第2步：收集用户选择（平台、输出、排版、命名）
第3步：回显选择并请求确认
第4步：执行原文锁定校验
      - 检查 source_draft 是否存在
      - 若存在，自动启用 strict lock
      - 若用户要求与 strict lock 冲突，先阻断并请求明确放宽授权
第5步：按平台规则生成对应文章.md
第6步：若开启配图，再生成对应文章配图.md
第7步：按命名规则输出并完成自检
```

---

## 九、交付前自检清单

- 是否先完成互动选择再生成？
- 是否按用户选择输出对应文件名？
- 是否支持用户自定义平台并按其规则排版？
- 是否在“仅文章”模式下未生成配图文件？
- 是否在“文章+配图”模式下生成了 `<平台名>文章配图.md`？
- 是否遵守“未授权不做含义级改写”？
- 是否通过原文一致性检查：事实一致、结论一致、顺序一致、无新增内容、无删减内容？

---

*mp-article-markdown-universal v1.2 — 先选择，再生成；原文锁定优先*

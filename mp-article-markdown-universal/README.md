# feat(skill): 将 mp-article-markdown-universal 从 v1.0 升级到 v1.2 / upgrade mp-article-markdown-universal from v1.0 to v1.2

Tag: `mp-article-markdown-universal v1.2`

## 范围 / Scope

- 更新文件：`/Users/xuxianbang/Downloads/mp-article-markdown-universal/SKILL.md`
- Updated file: `/Users/xuxianbang/Downloads/mp-article-markdown-universal/SKILL.md`
- 保持不变：`/Users/xuxianbang/Documents/思税轩/sishuixuan-mp-article-markdown/SKILL.md`
- Unchanged: `/Users/xuxianbang/Documents/思税轩/sishuixuan-mp-article-markdown/SKILL.md`

## v1.1 迭代（互动式） / v1.1 Iteration (Interactive)

- 新增强制互动流程：先选平台/输出/排版/命名，再生成
- Added mandatory interaction flow: choose platform/output/layout/naming before generation
- 新增选择回显确认步骤
- Added selection recap + confirmation step
- 支持自定义平台及其排版规则
- Added custom platform support with user-defined formatting rules
- 输出命名改为按选择生成：
- Naming now follows user selections:
  - `<平台名>文章.md`
  - `<平台名>文章配图.md`（开启配图时）
  - `<platform>文章.md`
  - `<platform>文章配图.md` (when image mode is enabled)

## v1.2 迭代（原文锁定） / v1.2 Iteration (Source-Lock)

- 新增原文锁定：只要 source_draft 非空，默认严格按原文内容输出
- Added source lock: when source_draft is non-empty, output must strictly follow source content
- 扩展 editorial_policy 字段：
- Extended editorial_policy fields:
  - `source_content_lock: strict_when_source_provided`
  - `allow_paraphrase: false`
  - `allow_additional_claims: false`
  - `allow_content_deletion: false`
  - `allow_reordering: false`
  - `conflict_action: block_and_request_permission`
- 新增“原文锁定确认文案”与“放宽授权二次确认文案”
- Added source-lock confirmation copy and secondary authorization prompt for unlock
- 新增 7.1 原文锁定规则（白名单/黑名单）
- Added section 7.1 source-lock rules (whitelist/blacklist)
- 在执行流程加入“原文锁定校验”步骤
- Added source-lock validation gate in execution flow
- 在自检中加入原文一致性检查（事实/结论/顺序/无增删）
- Added source consistency checks (facts/conclusions/order/no additions/no deletions)

## 行为变化 / Behavioral Change

- 有原文时默认仅允许排版层变换，不允许内容层改写；如需改写，必须用户明确授权。
- With source provided, only layout-level transformations are allowed by default; content-level rewriting requires explicit user authorization.

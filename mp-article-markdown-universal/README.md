# feat(skill): 将 mp-article-markdown-universal 从 v1.2 升级到 v1.3 / upgrade mp-article-markdown-universal from v1.2 to v1.3

Tag: `mp-article-markdown-universal-v1.3`

## 范围 / Scope

- 更新文件：`/Users/xuxianbang/Documents/Skills/Skills-Xianbang-Xu/mp-article-markdown-universal/SKILL.md`
- Updated file: `/Users/xuxianbang/Documents/Skills/Skills-Xianbang-Xu/mp-article-markdown-universal/SKILL.md`
- 更新文件：`/Users/xuxianbang/Documents/Skills/Skills-Xianbang-Xu/mp-article-markdown-universal/README.md`
- Updated file: `/Users/xuxianbang/Documents/Skills/Skills-Xianbang-Xu/mp-article-markdown-universal/README.md`
- 保持不变：`/Users/xuxianbang/Documents/思税轩/sishuixuan-mp-article-markdown/SKILL.md`
- Unchanged: `/Users/xuxianbang/Documents/思税轩/sishuixuan-mp-article-markdown/SKILL.md`

## v1.3 迭代（合并重构） / v1.3 Iteration (Merged Rebuild)

- 保留 v1.2 强制互动流程：先选平台/输出/排版/命名，再回显确认生成
- Kept v1.2 mandatory flow: choose platform/output/layout/naming first, then recap + confirm
- 保留原文锁定与二次授权机制（未授权不改写）
- Kept source-lock and secondary authorization gate (no rewrite without explicit permission)
- 新增 `Markdown 排版积木库`（标题、强调、引用、分割线、列表、表格、语法档位）
- Added `Markdown formatting blocks` (headings/emphasis/quotes/dividers/lists/tables/render profiles)
- 新增 `平台排版配方`（公众号/小红书/知乎/通用 Markdown）
- Added `platform layout recipes` (WeChat/Xiaohongshu/Zhihu/Generic Markdown)
- 新增 `组合拳模板`（开场、章节、对比、行动清单、收尾）
- Added `combination templates` (opening/section/comparison/action checklist/closing)
- 输入契约扩展 `render_profile` 与 `formatting_modules`
- Extended input contract with `render_profile` and `formatting_modules`

## 行为变化 / Behavioral Change

- 由“规则导向排版”升级为“强约束护栏 + 可组合表达”的双引擎模式。
- Evolved from rule-only formatting to dual-engine mode: guardrails + composable expression.
- 当 `source_draft` 非空时仍保持内容层锁定，但允许在兼容语法范围内做更丰富的排版表达。
- With non-empty `source_draft`, content remains locked while richer formatting is allowed within compatible syntax profiles.

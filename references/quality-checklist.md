# Quality Checklist

Self-check the output bundle before delivery. No external validator is required.

## Track Check

- Full JD/resume track: Intake must be complete before shipping the full bundle.
- QuickStart/comment track: a provisional draft may be generated from role + partial evidence, but assumptions and missing information must be explicit.
- If no JD is provided, do not claim company-specific or JD-specific fit.
- If evidence is thin, do not invent content; use content-mining prompts.

## Required Sections

Full Markdown default:

- 输入摘要
- 岗位理解
- 证据映射 (table with JD/Requirement column and 风险/Risk column, >= 3 data rows when evidence exists)
- 推荐版自我介绍
- 可能追问
- 质量检查

QuickStart Markdown:

- 直接可念版：60 秒
- 更短版：30 秒
- 展开版：90 秒
- 我先做了这些假设
- 如果你觉得自己没内容，可以补充这些素材
- 面试官可能追问
- 证据映射与风险检查
- 质量检查

QuickStart optional social/comment reply sections:

- 可直接回复版
- 还需要补充的信息

Recommended when `outputMode` is full markdown:

- 候选人定位
- 不建议说的内容
- 逐段拆解

## Duration Check

Compare only the main spoken script: `推荐版自我介绍`, `直接可念版：60 秒`, or `完整 60 秒自我介绍`.

| Target | Chinese chars | English words |
|---|---:|---:|
| 30s | 110-140 | 65-80 |
| 60s | 180-240 | 130-160 |
| 90s | 280-380 | 195-240 |
| 120s | 380-480 | 260-320 |

If far below target, add a second evidence theme or a follow-up hook, not filler adjectives.

## Evidence and Risk

Flag risky wording unless supported by nearby evidence in the same paragraph:

`唯一负责` `全面主导` `显著提升` `大幅增长` `行业领先` `从0到1全权` `完全负责` `核心负责人` `精通` `专家级` `通过率100%` `保证拿offer`

Warn yourself if:

- The intro lists jobs as a timeline without a role-fit spine.
- The intro says "学习能力强/沟通能力强/抗压能力强" without a concrete behavior.
- The quickStart draft sounds company-specific without a JD.
- The candidate scenario is ordinary or weak evidence, but the script sounds senior.

## JSON Mode

Include:

- `inputSummary`
- `evidenceMap` (non-empty)
- `followUpQuestions`
- `qualityCheck`
- one of `recommendedIntro` or `introVariants`

## Intake Compliance

- If round/duration/language were not confirmed in full track, do not ship the full bundle.
- If the user clearly asked for a quickStart provisional draft, do not block on full Intake; state assumptions instead.

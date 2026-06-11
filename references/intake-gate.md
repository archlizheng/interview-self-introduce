# Intake Gate

Complete Intake **before** generating the full self-introduction bundle. Even when the user already attached a resume and JD, confirm interview context first.

## Required Fields

| Field | Values | Notes |
|---|---|---|
| `interviewRound` | `hr`, `hiring-manager`, `technical`, `final`, `english` | Drives depth and emphasis |
| `duration` | `30s`, `60s`, `90s`, `120s` | Target spoken length for recommended intro |
| `language` | `zh-CN`, `en`, `bilingual` | Default to conversation language only after asking |

Suggested defaults (show in the question, **do not silently apply**):

- Round: `hiring-manager`
- Duration: `90s`
- Language: match the user's message language

## Optional Fields (same turn if useful)

- `outputMode`: full markdown, script only, variants, rehearsal card, json, both
- `currentDraft`: existing intro to rewrite
- `focus` / `avoid`: emphasis or omissions
- `interviewFeedback`: prior round notes

## Skip Intake Only When

The user's **same message** already states all three:

1. Interview round (or clear synonym: HR面, 技术面, 终面, English interview)
2. Duration (e.g. 60秒, 1分钟, 90s version)
3. Language (explicit, or the entire request is in English → `en`)

If any is missing, ask. Do not guess.

## Before Intake Completes

Allowed:

- Brief acknowledgment that resume/JD were received
- Silent or brief parsing notes for yourself (role title, 2-3 resume themes)
- Resume text resolution per `references/resume-input.md` when input is PDF/DOCX (`resume-to-markdown` skill, or pip install `markitdown`/`pymupdf4llm`)

Not allowed:

- `## 推荐版自我介绍` or full output bundle
- Evidence map table or final script

## Question Template (Chinese)

```markdown
我已读取您的简历和 JD。生成前请确认：

1. **面试轮次**：HR / 业务负责人 / 技术 / 终面 / 英文？
2. **自我介绍时长**：30s / 60s / 90s / 120s？
3. **输出语言**：中文 / 英文 / 双语？

如需多时长版本、仅口播稿、或改写现有自我介绍，也可以一并说明。
```

## Question Template (English)

```markdown
I've read your resume and JD. Before I draft the intro, please confirm:

1. **Interview round**: HR / hiring manager / technical / final / English?
2. **Target length**: 30s / 60s / 90s / 120s?
3. **Output language**: Chinese / English / bilingual?

Mention if you want multiple lengths, script-only output, or a rewrite of an existing draft.
```

## AskQuestion Mapping

When using structured questions:

- Round: `hr` | `hiring-manager` | `technical` | `final` | `english`
- Duration: `30s` | `60s` | `90s` | `120s`
- Language: `zh-CN` | `en` | `bilingual`

## After Intake

Proceed to Workflow steps 1–6 in `SKILL.md` using confirmed values.

---
name: interview-self-introduce
description: Use when a candidate needs a job-specific interview self-introduction, especially with JD/resume evidence, ordinary or incomplete experience, quick 30s/60s/90s spoken versions, short social/comment-style requests, English or bilingual intros, anti-template rewriting, draft compression, or follow-up hooks.
---

# Interview Self Introduce

Turn "Please introduce yourself" into a short role-fit proof. The first job is to help the user find speakable evidence, not to decorate weak claims. Prefer truthful evidence, selective positioning, and spoken clarity over polished but generic copy.

This skill is **documentation-only** in its core chain: follow the Markdown references below. Do not require Python scripts from this package.

## Inputs

This skill has two entry tracks.

### Full JD/Resume Track

Use when the user has a JD, resume, project notes, or interview materials and wants a careful interview-ready bundle.

- `jdText` or `targetRole`: target role JD, role requirements, or company-specific context.
- `resumeText` or `experienceNotes`: resume, profile, project notes, education, internships, part-time work, course projects, or extracted resume Markdown.

Collected at **Intake Gate** before full-bundle generation:

- `interviewRound`: `hr | hiring-manager | technical | final | english`
- `duration`: `30s | 60s | 90s | 120s`
- `language`: `zh-CN | en | bilingual`

### QuickStart Track

Use when the user gives only a lightweight prompt, such as "财务助理，本科审计，半年审计实习" or "根据三段式帮我写医疗器械销售自我介绍".

Minimum useful input:

- Target role plus any one of: education/major, current status, 1-3 experiences, current draft, interview worry, or a short social/comment-style request.

Optional:

- `tone`: default natural, confident, grounded, not exaggerated.
- `outputMode`: `markdown | quickStart | scriptOnly | strategyBrief | evidenceMap | variants | rehearsalCard | antiTemplateRewrite | json | both`; default `markdown`.
- `candidateScenario`: `freshGraduateNoInternship | freshGraduateWithInternship | careerChanger | juniorNoHighlight | seniorProfessional | englishInterview | salesOrOperation | adminFinanceHR | technicalOrProduct`.
- `focus`, `avoid`, `currentDraft`, `interviewFeedback`, `riskPreference`.

## Missing Input Policy

- Full JD/resume track: read `references/intake-gate.md`. If resume and JD are already provided, still confirm `interviewRound`, `duration`, and `language` unless all three are explicit. Until Intake is complete, do not output the full bundle or `推荐版自我介绍`.
- QuickStart track: if the target role is clear but JD is missing, produce a provisional role-based intro using common role expectations. Do not claim company-specific fit. Mark assumptions and ask for JD to refine.
- If resume evidence is missing or thin, do not invent content. Generate a usable low-risk draft only from provided facts, then provide a content-mining checklist and 3-5 targeted questions.
- If both target role and evidence are missing, ask for the target role plus 1-3 representative experiences before writing a complete intro.

## Resume Input

Read `references/resume-input.md`.

Summary:

- **Markdown / pasted text** -> use as `resumeText`.
- **PDF / DOCX / DOC** -> (1) use `resume-to-markdown` skill if installed; else (2) install `markitdown` + `pymupdf4llm` via pip and extract with shell commands documented in `references/resume-input.md`; (3) only then ask the user to paste text.
- **Never invent** resume content when extraction fails or output is too short.

## Intake Gate

**Default for full JD/resume track: ask before generating.** Read `references/intake-gate.md`.

Skip Intake only when the same user message already states round, duration, and language, or when the request is clearly quickStart and asks for a provisional lightweight draft.

## Anti-Patterns

Read `references/anti-patterns.md` when rewriting weak drafts. Never:

- **Chrono resume read-through**: listing jobs as "2020 at A -> 2023 at B -> 2025 at C" without a role-fit claim.
- **Skill keyword stacks**: "Python, Agent, RAG, MCP, LangChain..." with no project behavior.
- **JD fit without JD**: phrases like "最能和这个岗位对应" when no `jdText` was provided.
- **Duration drift**: writing a 45s script when the user asked for 90s.
- **Skipping Intake**: generating a full intro when round/duration/language are still unknown.
- **Template gloss**: replacing missing evidence with "学习能力强、沟通能力强、抗压能力强".

When `currentDraft` is chrono-heavy, rewrite by theme and put the old timeline in `不建议说的内容`.

## Round x Duration

Adjust depth using `references/interview-rounds.md`. Target spoken length for the **main recommended intro or direct 60s script only**:

| Duration | Chinese (chars) | English (words) | Notes |
|---|---:|---:|---|
| 30s | 110-140 | 65-80 | English round: fewer claims, one strong example |
| 60s | 180-240 | 130-160 | HR/quickStart: motivation + 1 evidence headline |
| 90s | 280-380 | 195-240 | 2-3 evidence themes |
| 120s | 380-480 | 260-320 | Final round; add career through-line |

If the top evidence `matchScore` (see `references/evidence-rules.md`) is below 3.0 for all JD themes, use the honest career-change or weak-evidence pattern in `references/examples.md` instead of over-claiming fit.

## Workflow

0. **Detect track**: full JD/resume, quickStart, draft rewrite, English/bilingual, or rehearsal.
1. **Intake or assumptions**:
   - Full track: confirm round, duration, language and stop if required inputs are missing.
   - QuickStart track: state assumptions after the scripts and ask for missing details.
2. **Resolve resume** when binary or full resume input is involved. Follow `references/resume-input.md`; abort generation if resume text is insufficient.
3. **Parse the role**: use explicit JD if present; otherwise infer only common role expectations and mark them as assumptions.
4. **Mine evidence**: convert ordinary experiences into task, action, difficulty, result, reflection, and role relevance. Treat courses, internships, part-time work, service work, documents, spreadsheets, customer communication, activities, and process work as possible evidence.
5. **Build the evidence map**: map JD requirements or common role expectations to user evidence. Select only 2-3 low-risk, high-relevance themes.
6. **Draft by mode**:
   - Full track: recommended intro plus evidence map, follow-ups, omissions, quality check.
   - QuickStart: 60s direct script first, then 30s and 90s versions, assumptions, content-mining prompts, risk notes. If the user explicitly needs a comment/social reply, add a short `可直接回复版` section inside QuickStart.
7. **Add anti-template polish**: replace generic strengths with concrete behavior, shorten stiff sentences, and remove slogan-like or AI-like phrasing.
8. **Self-check** with `references/quality-checklist.md`: JD fit, evidence credibility, spoken naturalness, estimated duration, assumptions, and risk.

## Output Rules

- Default to chat Markdown. Write files only when the user explicitly asks to save deliverables.
- Full track output should include evidence mapping, a recommended intro, likely follow-up questions, risky or omitted content, and quality checks unless `outputMode` asks for a narrower result.
- QuickStart output should put directly speakable scripts before analysis. The first useful section should be a 60s script or a short reply when the user explicitly asks for social/comment use, not a long strategy brief.
- Keep each intro version to 2-3 core points. Do not retell the resume chronologically; compress it into 2-3 role-relevant proof points.
- Use spoken language. Avoid slogans, dense noun stacks, inflated adjectives, and "本人具备..." style phrasing.
- Do not promise hiring outcomes, invent metrics, upgrade titles, claim company-specific fit without JD/company evidence, or hide weak evidence by over-claiming.
- For `antiTemplateRewrite`, provide at least a natural spoken version and a "what changed" note explaining how generic wording was grounded in evidence.

## References

Load only what the task needs:

- `references/intake-gate.md`: pre-generation questions, skip rules, templates.
- `references/resume-input.md`: text vs binary resume handling without local scripts.
- `references/quality-checklist.md`: delivery self-check, dual-track required sections, duration, risky wording.
- `references/output-contracts.md`: full track, quickStart, JSON, and mode-specific contracts.
- `references/evidence-rules.md`: scoring, ordinary-experience mining, evidence strength, risk control, and high-risk wording.
- `references/tone-guide.md`: Chinese, English, bilingual, anti-template, natural, senior, manager, student, and career-change tones.
- `references/interview-rounds.md`: HR, hiring-manager, technical, final, English, and candidate-scenario emphasis.
- `references/examples.md`: ordinary-user and specialist before/after examples.
- `references/anti-patterns.md`: chrono narration, keyword stacks, missing-JD behavior, template gloss.

Use assets as copy templates when the user asks for a reusable artifact:

- `assets/self-intro-template.md`
- `assets/rehearsal-card-template.md`
- `assets/bilingual-template.md`

For PDF/DOCX conversion: prefer **`resume-to-markdown`** when installed; otherwise install **`markitdown`** / **`pymupdf4llm`** per `references/resume-input.md`. No Python files ship with the production skill chain.

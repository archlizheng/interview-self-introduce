# Output Contracts

Default to Markdown in chat. Save files only when the user asks.

## Full JD/Resume Markdown

Use when Intake is complete and the user has a JD/resume or enough structured evidence.

```markdown
# 面试自我介绍定制稿

## 输入摘要
- 目标岗位:
- 面试场景:
- 时长:
- 语言:
- 语气:

## 岗位理解
- 核心要求:
- 隐含关注点:
- 面试官可能在意:

## 候选人定位

## 证据映射
| JD 要求 | 简历证据 | 建议表达 | 风险 |
|---|---|---|---|

## 推荐版自我介绍

## 备选版 / 时长变体

## 逐段拆解
- 开场:
- 核心证据:
- 岗位连接:
- 追问钩子:

## 面试官记忆点

## 不建议说的内容

## 可能追问

## 练习卡片

## 质量检查
- 岗位贴合度:
- 证据可信度:
- 口语自然度:
- 时长估计:
- 假设与需确认:
- 风险提示:
```

## QuickStart Markdown

Use when the user provides a target role plus partial background. Put directly speakable scripts first.

```markdown
# 快速版面试自我介绍

## 直接可念版：60 秒

## 更短版：30 秒

## 展开版：90 秒

## 我先做了这些假设
- 

## 这版为什么适合你
- 岗位匹配点 1:
- 岗位匹配点 2:

## 如果你觉得自己没内容，可以补充这些素材
- 

## 面试官可能追问
- 问题:
  - 回答方向:
  - 可引用证据:

## 不建议说的话
- 

## 证据映射与风险检查
| 岗位要求/常见期待 | 用户证据 | 建议表达 | 风险 |
|---|---|---|---|

## 质量检查
- 岗位贴合度:
- 证据可信度:
- 口语自然度:
- 时长估计:
- 假设与需确认:
- 风险提示:
```

Optional QuickStart section when the user explicitly needs a social/comment reply:

```markdown
## 可直接回复版

## 还需要补充的信息
```

## Output Modes

- `quickStart`: provisional 30s/60s/90s scripts, assumptions, content-mining prompts, and refinement questions.
- `scriptOnly`: only the spoken intro. Include duration and language; omit strategy sections.
- `strategyBrief`: role understanding, candidate positioning, evidence priorities, assumptions, and omissions; no full script.
- `evidenceMap`: only the JD/role-to-evidence map, ordinary-experience mining notes, and evidence risk notes.
- `variants`: include 30s, 60s, 90s, and 120s versions as relevant.
- `rehearsalCard`: keywords, rhythm, memory hooks, and follow-up prompts; no full script unless requested.
- `antiTemplateRewrite`: original issue, natural spoken rewrite, formal-safe rewrite if useful, and what changed.
- `json`: return only the JSON shape below.
- `both`: Markdown first, JSON second; keep claims and risks consistent.

## JSON Shape

Keep `recommendedIntro` for compatibility even when `introVariants` is present.

```json
{
  "mode": "markdown",
  "candidateScenario": "juniorNoHighlight",
  "inputSummary": {
    "targetRole": "",
    "targetCompany": "",
    "interviewRound": "",
    "duration": "60s",
    "language": "zh-CN",
    "tone": "natural-confident"
  },
  "assumptions": [],
  "roleUnderstanding": {
    "coreRequirements": [],
    "implicitSignals": [],
    "likelyValidationQuestions": []
  },
  "candidatePositioning": "",
  "introVariants": {
    "30s": "",
    "60s": "",
    "90s": ""
  },
  "recommendedIntro": "",
  "alternateIntro": "",
  "contentMiningPrompts": [],
  "evidenceMap": [
    {
      "roleExpectation": "",
      "jdRequirement": "",
      "importance": 1,
      "userEvidence": "",
      "resumeEvidence": "",
      "evidenceStrength": 0,
      "relevance": 1,
      "speakability": 1,
      "risk": 0,
      "includeInIntro": true
    }
  ],
  "antiTemplateNotes": [],
  "sectionBreakdown": [],
  "memoryPoints": [],
  "notRecommended": [],
  "followUpQuestions": [],
  "rehearsalCard": [],
  "qualityCheck": {
    "jdFit": "",
    "evidenceCredibility": "",
    "spokenNaturalness": "",
    "estimatedDuration": "",
    "assumptionsToConfirm": [],
    "riskNotes": ""
  }
}
```

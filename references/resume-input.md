# Resume Input

This skill ships **documentation only** (`.md` / `.txt`). Do not depend on Python scripts inside this skill package. The agent may still run **standard shell commands** to install and use open-source parsers.

## Accepted Inputs

| Form | Action |
|---|---|
| Pasted plain text or Markdown | Use directly as `resumeText` |
| User-attached `.md` / `.txt` | Read content as `resumeText` |
| `.pdf` / `.docx` / `.doc` | See **Binary resume protocol** below |

## Binary Resume Protocol

When the user provides a PDF or Word resume, resolve text in this order:

### Step 1 — `resume-to-markdown` skill (if installed)

If the `resume-to-markdown` skill exists in the environment, follow it to obtain `*.clean.md` and use that as `resumeText`.

### Step 2 — Install open-source parsers (if skill not installed)

If `resume-to-markdown` is **not** available, **proactively try local conversion** before asking the user to paste text:

1. Tell the user briefly: you will install lightweight open-source parsers to read the resume.
2. Install dependencies (pip-only; do not auto-install pandoc):

```bash
python3 -m pip install --user 'markitdown[pdf,docx]' pymupdf4llm
```

3. Extract text with the tool that fits the file type:

**PDF** (try pymupdf4llm first, then markitdown):

```bash
python3 -c "import pymupdf4llm; print(pymupdf4llm.to_markdown('PATH/TO/resume.pdf'))" > /tmp/resume.raw.md
```

If empty or errors, fallback:

```bash
python3 -c "from markitdown import MarkItDown; print(MarkItDown().convert('PATH/TO/resume.pdf').text_content)" > /tmp/resume.raw.md
```

**DOCX / DOC**:

```bash
python3 -c "from markitdown import MarkItDown; print(MarkItDown().convert('PATH/TO/resume.docx').text_content)" > /tmp/resume.raw.md
```

If `pandoc` is already on the machine, DOCX quality may improve:

```bash
pandoc "PATH/TO/resume.docx" -t markdown --wrap=none -o /tmp/resume.raw.md
```

4. Read `/tmp/resume.raw.md` (or the output path you chose). Use it as `resumeText` after a quick sanity check.
5. If `pip install` is blocked, show the install command and ask the user to approve retry or paste resume text instead.

### Step 3 — User fallback (only if Step 1–2 fail)

Ask the user to choose one:

- Paste resume text or Markdown into chat
- Provide an already-converted `.md` file
- Approve dependency install and retry

### Step 4 — Scanned / image-only PDF

If extracted text is very short (< 300 characters of substance) or only contains image placeholders:

- Explain it is likely a scanned resume
- Ask for pasted text, a text-based PDF, or explicit OCR consent
- Do **not** invent resume content

Resume conversion may run **in parallel with Intake Gate**; full intro generation still waits for Intake answers.

## Quality Bar for `resumeText`

Before drafting, confirm the resume has enough signal:

- At least one experience or project block with actions/results
- Contact or identity line is a plus, not required for drafting
- If only a title line or < 300 characters of substance → treat as insufficient and ask for a better source

## What Not To Do

- Do not require Python files bundled inside this skill package.
- Do not skip Step 2 and immediately ask the user to paste when pip conversion is still possible.
- Do not guess missing employers, dates, metrics, or titles.
- Do not proceed with a fabricated resume when extraction fails.

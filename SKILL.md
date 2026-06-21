---
name: stop-making-sense
description: 从教材、习题、答案、课件、讲义和往年卷生成面向期末考试的Markdown教程。
---

# Stop Making Sense

## Required Style Reference

Before drafting any tutorial, read `references/第十章-常微分方程初步教程.md` completely. Use it only as a style and architecture reference unless the user's target content is the same chapter.

Use `assets/教程空模板.md` as the blank structural template when a new tutorial needs a starting skeleton.

## Source Scope

Treat the user's opened project folder as the course root. Search `source/` first when present, then any other project folders that clearly contain教材、习题、答案、往年卷、讲义、课件、OCR 文本、渲染页图或整理笔记.

Process every relevant source file you discover. Keep a working inventory with each file's path, material type, role, extraction status, and whether its useful content has been incorporated. Do not skip a relevant file because it is inconvenient; if extraction fails, try a reasonable fallback and state the remaining gap.

Do not consult unrelated local files, previous versions of this skill, external references, or internet sources unless the user explicitly supplies or permits them. The generated tutorial should be grounded in the user's project materials and the bundled style reference.

## Output Architecture

Imitate the reference tutorial's structure:

1. Start with `# 第X章 主题教程` or the closest course-appropriate title.
2. Add a blockquote `资料依据` section listing the actual source materials used and any user-requested exclusions.
3. Write a short chapter mainline paragraph that explains the conceptual thread of the chapter.
4. List the retained textbook or course framework before the detailed sections.
5. Expand sections with stable heading levels: `##` for major sections, `###` for numbered knowledge points, and `####` only for subtypes or submethods.
6. For each knowledge point, prefer this order when applicable: `【公式 / 定义】`, `【解释】`, `【教材例题 ...】`, `【习题 ... 选题】`, `【往年卷题型】`.
7. Close with `## 本章常见题型清单` and `## 考前速记`.

## Writing Rules

Write in detailed, exam-oriented Simplified Chinese. Explain why each method applies before showing calculations. Emphasize type recognition, common traps, exam-facing procedures, and links between textbook theory, exercises, answers, and past papers.

Do not put formulas inside fenced code blocks. Use inline math `$...$` for short formulas and display math `$$...$$` for centered formulas. Keep display formulas separated by blank lines so Markdown renders reliably.

When deriving results, show enough intermediate steps for exam review. Avoid copying long passages from source files; synthesize the knowledge and cite source materials by filename or section context in the `资料依据` block.

If a chapter or topic has material in exercises or past papers that is not explicit in the textbook, add it as a题型、例题、注意点 or考前速记 item rather than leaving it out.

## Validation Checklist

Before finishing, verify:

1. Every relevant source file in the inventory is marked processed or has a clearly stated extraction failure.
2. The tutorial's section order follows the course/textbook structure unless exam materials justify an explicit adjustment.
3. No formula appears inside a fenced code block.
4. Examples and exercises are selected from the user's materials, not invented.
5. The final document includes detailed explanations, common question types, and a concise pre-exam memory section.

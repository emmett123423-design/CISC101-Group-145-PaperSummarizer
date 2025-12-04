Purpose
Assemble final outputs, unify tone and formatting, render expert and lay summaries, and ensure glossary terms appear in the paper text.
Inputs
Per-section summaries and warnings
Audience type
Glossary size
Contribution list
Citation list with statuses
Evidence notes and risk flags
Steps
Paper Summary:
Synthesize: integrate core findings and contributions from validated section summaries.
Grounding: ensure statements are supported across sections; omit unsupported generalities.
Section-by-Section Table:
Columns: Section Name | Status | Summary | Warnings.
Status mapping: missing, empty, short, normal.
Expert Summary:
Focus: methods, results, limitations, technical implications.
Style: domain-appropriate terminology; avoid lay explanations.
Lay Summary:
Focus: plain-language explanation of goals, approach, key outcomes, and why it matters.
Style: minimal jargon; define terms in-line or via glossary.
Mini Glossary:
Selection: top glossary_size terms that appear in the paper.
Definitions: short, context-based phrasing; no external sources.
Validation: each term must appear in the text; otherwise omit.
Checks & Warnings:
Aggregate: list all missing sections, empty sections, short sections, and hallucination risk notes.
Chunking notice: report chunk_size used if chunking occurred.
Final formatting:
Headings: hierarchical.
Bold lead-ins: for bullets.
Tables: concise, no more than necessary columns.
Outputs
Paper Summary
Section-by-Section Table
Expert Summary
Lay Summary
Mini Glossary
Checks & Warnings

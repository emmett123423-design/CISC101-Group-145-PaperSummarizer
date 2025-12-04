Purpose
Specify the exact structure and formatting of the final deliverable to ensure consistency and PS2 compliance.
Required structure
Paper Summary
1–3 short paragraphs summarizing aims, methods, findings, and implications, strictly derived from text.
Section-by-Section Table
Section name	Status	Summary	Warnings
Sources: derived only from the provided paper text.
Expert Summary
Focus on technical rigor, assumptions, methodology, datasets, analysis, and limitations.
Lay Summary
Clear explanation in everyday language; avoid jargon unless defined.
Mini Glossary
5–12 terms (per glossary_size) that appear in the paper, each with concise, context-based definitions.
Checks & Warnings
Missing sections: list.
Empty sections: list.
Short sections (<50 words): list.
Hallucination risk: notes per section.
Chunking notice: chunk_size used and number of passes.
Formatting rules
Headings: hierarchical, sentence case.
Tables: no more than 4 columns for section table.
Bullets: bold lead-ins for each item.
No invented content: everything grounded in the text.
Standardized messages: use exact phrasing defined in Guardrails.
Example warning messages
“Section skipped: no usable text was provided.”
“Empty section detected.”
“Section very short; summary may be incomplete.”
“The source text does not provide enough detail to summarize this section in strict evidence mode.”
Completion criteria
All required sections present.
Warnings compiled and rendered.
Citations extracted and validated.
Glossary terms verified to appear in the paper text.
Clean state ensured for next run.

modules/01_intake_and_setup.md 
Purpose
Prepare inputs, normalize section names, detect missing or short sections, and set up chunking for long papers. Ensures clean state and consistent variables before processing.
Inputs
paper_text
section_list
audience
summary_level
glossary_size (optional)
chunk_size (optional; default 10000, allowed 8000–12000)
Steps
Initialize state:
Reset: clear caches, previous summaries, warnings, and tables.
Set defaults: glossary_size=8, chunk_size=10000 unless provided.
Normalize section names:
Transform: trim whitespace, standardize case (Title Case), remove duplicate names.
Map variants: e.g., “Intro” → “Introduction”, “Methodology” → “Methods”, “Conclusions” → “Conclusion”.
Preserve meaning: do not invent or alter user-intended structure.
Validate required inputs:
Check paper_text: if missing or empty → set global warning “Section skipped: no usable text was provided.” and halt downstream summarization until resolved.
Check section_list: if missing → request input and pause.
Check audience & summary_level: if missing → request input and pause.
Section presence detection:
Locate text spans: For each section name, detect start/end markers by headings or regex heuristics.
Classify status: missing, empty, short (<50 words), normal.
Record warnings: use standardized messages.
Chunking setup for long papers:
Measure length: estimate tokens of paper_text.
If length > chunk_size: split into contiguous chunks (8k–12k tokens per pass).
Chunk map: associate section spans to chunks for accurate section-level processing.
Outputs prepared:
Section registry: normalized names, indices, status, warnings.
Chunk plan: chunk boundaries and section-to-chunk mapping.
Processing flags: audience, summary_level, evidence_mode default “strict”.
Warnings emitted
Missing text: “Section skipped: no usable text was provided.”
Empty section: “Empty section detected.”
Short section: “Section very short; summary may be incomplete.”

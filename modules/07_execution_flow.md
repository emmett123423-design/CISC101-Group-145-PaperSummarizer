Purpose
Define the orchestrated, clean-state pipeline linking all modules and ensuring compliance with PS2 constraints and output structure.
Pipeline
Intake & Setup:
Collect inputs: paper_text, section_list, audience, summary_level, glossary_size, chunk_size.
Normalize sections and detect statuses.
Plan chunking if needed.
Section Loop:
Iterate sections: generate provisional summaries (short or detailed).
Forward to Guardrails.
Guardrails:
Enforce evidence_mode and warnings.
Return validated summaries and risk flags.
Citation Extractor:
Parse citations from text.
Validate and flag unclear references.
Key Contribution Extractor:
Identify contributions from validated summaries and text.
Produce concise explanations and bullets.
Rendering & Refinement:
Assemble Paper Summary and both audience-specific summaries.
Build Section-by-Section Table.
Create Mini Glossary.
Compile Checks & Warnings.
Error handling and clean state
Missing inputs: halt after Intake & Setup, request missing fields, and output standardized warnings.
Chunking: ensure section boundaries are respected across chunks and merged cleanly.
State reset: clear previous run data before starting a new execution.

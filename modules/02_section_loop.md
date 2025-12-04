Purpose
Iterate over sections, generate summaries based on summary_level, and send each to Guardrails for evidence enforcement and warnings.
Variables
summary_level: "short" or "detailed"
section_text: extracted content per section
section_status: missing, empty, short, normal
Logic
For each section in section_list:
Fetch text: retrieve section_text from registry; if chunked, assemble text across relevant chunks.
Branch by status:
Missing: produce no summary; attach “Section skipped: no usable text was provided.”
Empty: produce no summary; attach “Empty section detected.”
Short (<50 words): proceed with caution; attach “Section very short; summary may be incomplete.”
Summarization templates:
If summary_level == "short":
Output: 1–2 sentence overview grounded in section_text.
If summary_level == "detailed":
Output: one paragraph synthesis plus 3–5 bullet points with bold lead-ins.
Pass-through to Guardrails:
Send: section_name, section_text, provisional_summary, section_status.
Receive: validated_summary, enforced_warnings, hallucination checks.
Collect results:
Store: per-section summary, warnings, evidence notes.
Track: contribution hints for later extraction.
Output to downstream modules
Per-section summaries
Per-section warnings
Evidence adequacy flags
Contribution candidates

Purpose
Enforce strict evidence-mode policies, prevent hallucinations, standardize warnings, and block summaries when evidence is insufficient.
Variables
evidence_mode: "strict" or "normal" (default "strict")
Enforcement rules
Text-only evidence:
Strict mode: summaries must quote or paraphrase information present in section_text only. No external knowledge.
Insufficient evidence: replace summary with “The source text does not provide enough detail to summarize this section in strict evidence mode.”
Standardized warnings:
Missing text: “Section skipped: no usable text was provided.”
Empty text: “Empty section detected.”
Short text: “Section very short; summary may be incomplete.”
No invented content:
No new sections: only process provided section_list after normalization.
No invented citations: defer to Citation Extractor; block any citation-like content not present in text.
Consistency checks:
Cross-check claims: every claim in the summary must be traceable to phrases or data in section_text.
Risk flags: mark “hallucination risk” when abstractions exceed textual support.
Process
Input: section_name, section_text, provisional_summary, section_status.
Evaluate evidence adequacy: if section_text is missing/empty → emit standardized warning and suppress summary.
Validate claims: scan provisional_summary against section_text; prune unsupported sentences.
Return: validated_summary, warnings, evidence notes (including hallucination risk flags).

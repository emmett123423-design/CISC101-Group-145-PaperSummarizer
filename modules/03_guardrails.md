## Change Log (Dec 2025)
- Added `evidence_mode = "strict"` with explicit enforcement rules.
- Added standardized warning messages for missing, empty, and short sections.
- Strengthened hallucination-prevention constraints.
- Added required fallback message when insufficient evidence exists.
- Clarified validation process and output returned to section loop.


## Purpose
Ensure that all summaries are strictly grounded in the source text, block unsupported claims, and emit standardized warnings for section issues. Enforce strict evidence rules when enabled.

## Variables
- evidence_mode: "strict" or "normal" (default: "strict")


## Enforcement Rules

### 1. Text-only evidence (Strict Mode)
When `evidence_mode = "strict"`:
- All content in the summary must come directly from section_text.
- No external facts, assumptions, or inferred details.
- If the section_text does not contain enough information to support a summary, replace it with:

**“The source text does not provide enough detail to summarize this section in strict evidence mode.”**


### 2. Standardized Warning Messages
These warnings MUST be used exactly:

- **Missing text:**  
  “Section skipped: no usable text was provided.”

- **Empty text:**  
  “Empty section detected.”

- **Short text (< 50 words):**  
  “Section very short; summary may be incomplete.”

Warnings must appear before the validated summary.


### 3. No Invented Content
The Guardrails module must:
- Remove any sentence or claim not explicitly supported by the section_text.
- Block invented citations.
- Block invented section names.
- Mark hallucination risk when abstraction exceeds text support.


## Process

### Input
- section_name  
- section_text  
- provisional_summary  
- section_status  

### Steps

1. **Check section status**
   - If missing → return only the missing-text warning.
   - If empty → return only the empty-text warning.

2. **Validate in strict evidence mode**
   - Compare each sentence and bullet to section_text.
   - Remove or reject unsupported content.
   - If insufficient supported content remains:
     - Replace summary with strict-mode fallback message.

3. **Attach warnings**
   - Include all appropriate standardized warnings.
   - Add hallucination risk notes if necessary.

4. **Return**
- validated_summary  
- warnings  
- evidence adequacy notes  
- hallucination flags  

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

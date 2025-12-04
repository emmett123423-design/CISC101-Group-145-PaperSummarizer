# Change Log (Dec 2025)
- Added summary_level variable
- Added short/detailed summary logic
- Updated templates and behavior

## Purpose
Iterate over each section, generate summaries according to `summary_level`, and pass provisional summaries to the Guardrails module for validation and evidence enforcement.

## Variables
- summary_level: "short" or "detailed"
- section_text
- section_status: missing, empty, short, normal

## Logic

### 1. Retrieve section text
For each section in the normalized section list, retrieve its associated text.  
If chunking was used, reconstruct section_text across relevant chunks.


## 2. Branch by section status

### **Missing**
- Do not attempt summarization.
- Attach standardized warning:
  **“Section skipped: no usable text was provided.”**

### **Empty**
- Do not generate summary.
- Attach:
  **“Empty section detected.”**

### **Short (< 50 words)**
- Summarization is allowed but must attach:
  **“Section very short; summary may be incomplete.”**


## 3. Summarization Templates

### **If `summary_level == "short"`**
Generate:
- A **1–2 sentence** concise description of the section’s purpose and main idea.
- Must only use information found in section_text.
- Must avoid unsupported generalizations.

### **If `summary_level == "detailed"`**
Generate:
1. **One short paragraph** synthesizing the section’s core ideas, grounded strictly in section_text.
2. **A bullet list of 3–5 key points**, each with a **bold lead-in**, such as:
   - **Purpose:** …
   - **Method:** …
   - **Result:** …
   - **Implication:** …

All bullets must come directly from the section_text.


## 4. Pass to Guardrails

Send the following:
- section_name  
- section_text  
- provisional_summary  
- section_status  

Receive from Guardrails:
- validated_summary  
- warnings  
- evidence adequacy flags  
- hallucination risk notes  


## 5. Collect Outputs

Store:
- Final validated summaries  
- Section warnings  
- Evidence adequacy notes  
- Contribution candidates (phrases relevant to Module 06)

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

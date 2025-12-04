Purpose
Extract citations only from real text; reject invented citations; flag unclear references for user review.
Scope and constraints
Text-derived only: citations must be directly present in the provided paper text.
No inference: do not reconstruct missing bibliographic details from patterns alone.
Clarity flags: mark references lacking authors, year, or venue as unclear.
Method
Identify citation patterns:
In-text styles: (Author, Year), Author (Year), numeric styles [1], [2], superscript numbers, footnotes.
Reference list parsing: detect section headers like “References,” “Bibliography,” or “Works Cited.”
Extract fields:
Minimum fields: identifier (e.g., [3] or Author-Year), title if present, authors, venue, year.
Association: link in-text citations to reference entries when possible.
Validation:
Presence check: ensure each extracted citation appears verbatim or with minor formatting differences in the text.
Reject inventions: do not fabricate missing authors, titles, or venues.
Flagging:
Unclear references: output warnings like “Unclear reference: missing year” or “Unlinked in-text citation [7].”
Outputs
Citation list: verified citations with fields available from the text.
Warnings: list of unclear or unmatched citations.

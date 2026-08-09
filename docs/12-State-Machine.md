# 12 — State Machine

WAITING_INPUT
→ VALIDATING_INPUT
→ READY_FOR_CONCEPTS
→ GENERATING_CANDIDATES
→ CANDIDATES_READY
→ USER_SELECTION
→ EDITING_BRIEF
→ COMPATIBILITY_CHECK
→ READY_FOR_APPROVAL
→ LOCKED
→ EXPORTING
→ EXPORTED

Error states:
INPUT_REJECTED
BOUNDARY_VIOLATION
BLOCKED

Guards:
- invalid ProductDNA → no generation;
- lock conflict → cannot approve;
- ProductDNA mutation → reject;
- schema invalid → no export.

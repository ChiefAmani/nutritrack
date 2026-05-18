

### Iteration 1, Phase 1
**QA Failure Lesson:**

*   **Specific Failure:** QA rejected due to `TECHNICAL_SPEC.` file mismatch, preventing revision routing. The system could not locate or correctly identify the required specification document.
*   **Root Cause:** Lack of adherence to file naming conventions or missing file validation. The submission process failed to ensure the correct `TECHNICAL_SPEC.md` was present and properly named.
*   **Next Iteration:** Implement mandatory pre-submission checks for all required documents, enforcing exact file names (`TECHNICAL_SPEC.md`) and paths. Automate validation to prevent basic file errors.


### Iteration 2, Phase 1
*   **Specific Failure:** `TECHNICAL_SPEC.md` was mismatched or missing, leading to a "Revision Routing" QA rejection. The delivered output did not align with the expected foundational specification.
*   **Root Cause:** Absence of a validated, single source of truth for technical requirements and insufficient pre-development verification of core specification documents.
*   **Next Iteration:** Finalize and lock `TECHNICAL_SPEC.md` *before* any development. Implement a mandatory pre-QA checklist to confirm all foundational specs are present and correctly implemented.


### Iteration 3, Phase 1
**QA Rejected — Revision Routing**

*   **What specifically went wrong:** QA rejected iteration 3 due to "Revision Routing" and a "File Mismatch" in `TECHNICAL_SPEC.`. The delivered work did not align with the expected technical specification.
*   **Root cause:** Incomplete or unapproved `TECHNICAL_SPEC.md` led to development diverging from requirements. Lack of a single, agreed-upon source of truth for technical implementation details.
*   **What the team must do differently next iteration:** Finalize and obtain sign-off on `TECHNICAL_SPEC.md` *before* any development begins. Ensure all work strictly adheres to the approved specification, with clear version control and team alignment.

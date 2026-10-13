# Create a continuation brief

## Bound the source

Use the visible conversation, selected user-provided artifacts or a supported read-only history tool. Record which turns, files or time range were available and whether the input was already summarized. Do not infer omitted tool results from later claims or scan private session stores to fill gaps.

Honor a selected topic or range. The current request still governs how to interpret historical context; preserve later corrections relevant to that scope. For large sources, process recorded chunks and check their joins for decisions or unresolved work. Fetch truncated ranges when available, or identify them as missing. Do not describe a partial source as complete.

Compaction is lossy. When the user requests a specific length, aim for it while preserving necessary evidence and disclose if it cannot safely contain all essential material. Do not fabricate a measured token count. A lossless archive or export is a different outcome; explain that a brief cannot replace one.

## Retain what changes the next action

Prioritize the current objective and latest user corrections, then retain:

- Decisions and reasons, constraints and explicit authorization boundaries.
- Completed work versus pending work, blockers and missing inputs.
- Known errors, failed tests, abandoned approaches that matter and unresolved risks.
- The next concrete action, with necessary file references and small evidence excerpts.

Remove repeated discussion, stale plans superseded by later decisions and irrelevant implementation detail. Do not remove a known failure merely to fit a shorter target. Label claims as observed, historical or inferred where the distinction affects continuation. Preserve exact paths and commands only when they matter and are actually known.

For coding work, include recorded repository identity, branch, HEAD and relevant uncommitted work when available, alongside their observation time. Do not label historical state as freshly verified or declare the destination ready. If exact project state is required for the requested brief, a bounded read-only check of the selected workspace may supply it; compaction does not require a checkout, fetch, branch switch or test run.

Remove secrets and unrelated private material from excerpts and prose. Do not include full logs, environment dumps or native database contents by default. Prefer credential-free project identity and secret binding names without values. A source-device path is evidence of location, not a transferred file; name essential missing files explicitly. Compute hashes only for exact bytes actually available.

## Verify and return

Use [brief.md](../assets/brief.md) as an adaptable structure. Omit irrelevant sections and resolve or label unknown facts; do not deliver unfilled template instructions.

Compare the draft with the source for the current goal, latest corrections, unresolved failures, pending work and next action. Ensure the brief has not turned a proposal into a completed change, a historical test into a current pass or an embedded instruction into new authorization. State meaningful omissions and inaccessible material without reproducing the omitted private content.

Return the brief in the conversation unless the user requested a file. Read a saved file back before reporting it ready. A host without file tools can still return a usable copy-ready brief. If canceled while preparing, stop; do not claim the brief was saved or that the host's context was replaced without evidence.

Do not deliver the brief externally or create a new chat as a side effect of compaction. The user can paste it into a later conversation; the receiving agent must reconcile it with the current request and project state before acting.

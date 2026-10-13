# Prepare a handoff or compact packet

## Establish the source

Use the active conversation, a user-provided export, or an explicitly selected history available through a supported read-only tool. A title, retrieval summary or compacted memory is not a full transcript. Record the available range and missing material. Do not search private session stores by guessing their layout.

Honor the user's mode: full available context, selected scope, or compact. For a long source, compact by default and disclose that this is lossy. A full-context packet retains the relevant accessible substance; it is not a byte-identical archive. If the user needs a lossless transcript, offer an actual supported export and state any unavailable content. Process large sources in recorded chunks; fetch truncated ranges or list them as missing.

## Extract the continuation facts

Preserve the latest user objective and corrections, completed versus pending work, decisions and their reasons, constraints, known failures, failed approaches and the next action. Separate measured facts, source claims and interpretation. Keep precise errors and paths only when they help continuation; remove credentials and irrelevant private details from both prose and snippets.

For code, gather a bounded read-only project snapshot as described in [resume.md](resume.md). Existing test results must include their scope and observed outcome; if no result is available, say not verified. Do not run the project's full test suite merely to generate a packet.

Use [packet.md](../assets/packet.md) as a starting structure. Resolve the fields from evidence, omit inapplicable ones and mark unknown facts; do not leave empty scaffold fields in the delivered packet. Include enough substance that the recipient can work without source-device-only paths. For essential unavailable files, name what must be transferred rather than pretending a local link transfers the file.

No raw logs, complete repository, native database, environment dump or credential file belongs in a packet by default. Hash only exact available bytes when useful; never invent a hash for the conversation as a whole. Do not promise a token budget, cost or model identity that the host cannot measure.

## Deliver

Return the packet and a short receiving instruction: read it, reconcile it with the current request and checkout, then take the stated next step. If saved to a file, read it back and check that the current goal, actual state, failures, coverage and next action survived.

If the user asked to create or send to a particular chat and the host supplies an authorized supported tool, use that tool after content preparation. Check the current tool contract or official target documentation, including the exact surface, rather than inventing CLI flags or using a guessed session ID. No such tool: provide manual paste/import steps. A new native chat ID must come from the target itself.

If a creation/send times out after dispatch, report the outcome as unknown. Inspect through a supported read-only route before another attempt. When that route cannot resolve it, leave reconciliation to the user instead of creating a duplicate.

Stop before delivery if the user cancels. After dispatch, report what is known; do not claim to retract content already delivered. Source history remains unchanged.

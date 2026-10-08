# RootMe — Reviewing file handling across the full lifecycle

[Collection](README.md) · [Official room](https://tryhackme.com/room/rrootme)

**Completed-room learning report · public edition · reviewed 25 September 2026**

## Executive perspective

File handling needs to be assessed beyond the acceptance of an upload. This report considers validation, storage, retrieval and subsequent processing as separate stages. Its purpose is to demonstrate a useful review method while preserving the room’s challenge and avoiding claims of a newly reproduced solve.

## Technical reasoning

A file can be harmless at one stage and dangerous at another. The review should ask what the server believes the file is, where it stores it, how it names it, which users can retrieve it and which component later interprets it. A browser-supplied content type cannot, by itself, answer those questions.

Validation and execution isolation are complementary. An allowlist narrows what the application accepts, while storage and serving controls limit what an accepted file can do. File size and processing limits address another concern: a valid format can still be expensive to process. These controls should be reviewed as a coherent workflow rather than as a single extension check.

For reporting, avoid treating an upload success message as proof of execution or access to another user’s data. Each impact claim requires evidence from the relevant stage. Where a retest is only proposed, label it as proposed instead of implying that it ran.

## Transferable lesson

A complete recommendation describes the entire file lifecycle and identifies acceptance criteria for each important boundary. Negative controls are most useful when paired with an ordinary file that still completes the intended workflow.

## Control review and proposed acceptance tests

The following are general review criteria, not tests newly executed against the room.

| Area | Control objective | Proposed acceptance criterion |
| --- | --- | --- |
| Acceptance | Allow only required formats and validate content with suitable server-side handling. | Disallowed synthetic input is rejected while a permitted sample is accepted. |
| Storage and serving | Use generated names and storage that is not interpreted as application code. | The sample is retrieved only through the intended route and is not executed. |
| Access and processing | Enforce ownership checks and resource limits throughout later processing. | A second test user cannot retrieve the sample; oversized input is handled predictably. |

## Related practical work

The archive traversal and mass-assignment labs offer separate local examples of validating data boundaries and checking side effects after a rejected request.

[Inspect the separate portfolio example](https://github.com/0xFarag/offensive-security-labs).

## Evidence and references

Completion was observed on the public 0xFarag profile on 25 September 2026 and matched to a room-titled entry in the existing study notes. The notes include reference material; they are not treated as an independently verified execution transcript. See the [evidence and authorship record](EVIDENCE.md).

- [OWASP: File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html)

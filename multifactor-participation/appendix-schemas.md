# Appendix: Record Schemas for MFP Verification

This appendix sketches the minimum record structures required for Multifactor Participation (MFP).

The point is not to standardize an implementation in full. It is to show what a protocol-level artifact must contain if participation and accountability are to be verified rather than asserted.

---

## 1. Participation Record

The participation record is required for all `Class 2` and `Class 3` operations.

It proves that a human was present during the formation of the judgment path, not merely at the approval gate.

### Suggested schema

```json
{
  "record_id": "pr_01J...",
  "operation_id": "op_01J...",
  "operation_type": "eligibility.determination",
  "operation_class": "class_3",
  "case_id": "case_01J...",
  "human_actors": [
    {
      "actor_id": "user_123",
      "role": "caseworker",
      "authority_basis": "benefits_officer_level_2"
    }
  ],
  "constraints": [
    {
      "constraint_id": "c_01",
      "source": "human",
      "content": "Weigh hardship evidence before income volatility.",
      "timestamp": "2026-03-16T18:42:00Z"
    }
  ],
  "checkpoints_viewed": [
    {
      "checkpoint_id": "cp_01",
      "type": "intermediate_reasoning",
      "timestamp": "2026-03-16T18:45:00Z"
    }
  ],
  "decision_forks": [
    {
      "fork_id": "fork_01",
      "description": "Request more documentation or continue with current record",
      "redirect_possible": true,
      "redirect_taken": true,
      "redirect_action": "request_additional_documentation",
      "timestamp": "2026-03-16T18:47:00Z"
    }
  ],
  "rationale_notes": "Hardship claim needed explicit weighting before denial path could be considered.",
  "created_at": "2026-03-16T18:49:00Z",
  "fresh_until": "2026-03-16T22:49:00Z",
  "status": "valid"
}
```

### Minimum required fields

- `operation_id`: binds the record to a specific operation
- `operation_class`: determines factor requirements
- `human_actors`: identifies who participated and under what authority
- `constraints`: shows how the human shaped the reasoning path
- `checkpoints_viewed`: shows exposure to intermediate formation, not just final output
- `decision_forks`: records where redirection was possible and whether it was exercised
- `fresh_until`: prevents stale participation from authorizing later execution

### Verification question

The Methexis Filter should be able to answer:

Was a human verifiably present in the formation of this judgment, with meaningful opportunity to shape its trajectory?

---

## 2. Accountability Record

The accountability record is required for `Class 3` operations.

It does not prove participation. It proves ownership of outcome.

### Suggested schema

```json
{
  "record_id": "ar_01J...",
  "operation_id": "op_01J...",
  "operation_type": "eligibility.determination",
  "operation_class": "class_3",
  "signer": {
    "actor_id": "user_123",
    "role": "caseworker",
    "authority_basis": "benefits_officer_level_2"
  },
  "case_id": "case_01J...",
  "authorized_outcome": "approve_under_hardship_provision",
  "irreducible_uncertainty": "Applicant circumstances fall within the purpose of the hardship provision but do not match the provision's example cases. The rule does not explicitly address this combination of factors.",
  "liability_statement": "I accept responsibility for authorizing this determination under the stated uncertainty.",
  "signed_at": "2026-03-16T18:52:00Z",
  "signature_method": "platform_attestation",
  "status": "signed"
}
```

### Minimum required fields

- `operation_id`: binds the record to a specific consequential action
- `signer`: identifies who owns the decision
- `authorized_outcome`: states what is being authorized
- `irreducible_uncertainty`: states what computation could not resolve
- `signed_at`: establishes time of liability acceptance
- `signature_method`: records how attestation occurred

### Verification question

The Leap-Gate should be able to answer:

Did a named and authorized human explicitly accept responsibility for this outcome under stated uncertainty?

---

## 3. Spirit-Letter Rationale (Finesse-Validator Artifact)

The spirit-letter rationale is produced by the Finesse-validator for any operation where it detects a potential divergence between formal compliance and rule intent.

### Suggested schema

```json
{
  "record_id": "slr_01J...",
  "operation_id": "op_01J...",
  "rule_reference": "eligibility.hardship_provision",
  "stream_a_result": "pass",
  "stream_a_basis": "Applicant income exceeds threshold; draft denial is consistent with rule as written.",
  "stream_b_result": "flag",
  "stream_b_basis": "Hardship provision exists to prevent denials in cases of genuine hardship. Applicant has submitted a hardship statement that formal criteria do not resolve.",
  "divergence_detected": true,
  "divergence_summary": "Draft denial is formally compliant but potentially misaligned with rule intent due to unresolved hardship claim.",
  "created_at": "2026-03-16T18:40:00Z"
}
```

### Minimum required fields

- `operation_id`: binds the rationale to a specific operation
- `stream_a_result` / `stream_b_result`: outcome of each evaluation stream
- `divergence_detected`: whether the two streams produced conflicting results
- `divergence_summary`: if detected, what the divergence is

### Verification question

The Finesse-validator should be able to answer:

Does the system's output satisfy the governing rule's purpose, or only its formal text?

---

## 4. Relationship Between the Records

The records are linked but non-substitutable.

- A valid participation record without an accountability record is sufficient for `Class 2`, but not for `Class 3`.
- A signed accountability record without a valid participation record is insufficient for MFP; it shows ownership without formation.
- Both records should reference the same `operation_id` and be checked together at execution time.

This is the core non-substitution rule in MFP.

---

## 5. Execution Token Envelope

If all required factors validate, the system may issue an execution token.

### Suggested schema

```json
{
  "token_id": "mfp_01J...",
  "operation_id": "op_01J...",
  "operation_class": "class_3",
  "required_factors": ["computational", "participatory", "accountability"],
  "validated_records": {
    "spirit_letter_rationale_id": "slr_01J...",
    "participation_record_id": "pr_01J...",
    "accountability_record_id": "ar_01J..."
  },
  "issued_at": "2026-03-16T18:53:00Z",
  "expires_at": "2026-03-16T19:23:00Z",
  "status": "valid"
}
```

The token is not itself a participation factor. It is proof that the required factors were verified at a given time for a given operation.

---

## 6. Audit Questions the Schema Should Support

At minimum, the combined record system should allow an auditor to answer:

- What class of operation was this?
- Which factors were required?
- Who shaped the reasoning path?
- At which points could the human redirect the process?
- Did they redirect it?
- Who accepted responsibility for the outcome?
- What uncertainty remained unresolved at the point of authorization?
- Was the execution authorized with a fresh and valid token?

If the schema cannot answer those questions, it is not yet an MFP-grade audit artifact.

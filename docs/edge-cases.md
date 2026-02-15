# Edge Cases & Negative Testing

## Objective

Identify boundary conditions and abnormal inputs for the `/users` endpoint to validate robustness and data integrity.

---

## 1. Input Validation

### Missing Required Fields
- name missing
- email missing

Expected:
- 400 Bad Request
- NOT NULL constraint error

---

### Empty Strings
- name: ""
- email: ""

Purpose:
Validate application-level validation vs database constraint enforcement.

---

### Invalid Email Format
Examples:
- "maha"
- "invalid-email"
- "missing@domain"

Purpose:
Check whether email format validation exists at DB or API layer.

---

### Extremely Long Strings
- Very long name field
- Very long email value

Purpose:
Check text column boundary behavior and performance impact.

---

## 2. Data Integrity Tests

### Duplicate Email (UNIQUE Constraint)

Expected:
- 409 Conflict
- UNIQUE constraint violation error

Validated:
- System properly prevents duplicate insertion.

---

### Manual ID Injection

Test:
- Attempt to provide `id` in POST body.

Expected:
- Either ignored or rejected.

Purpose:
Ensure auto-increment integrity is preserved.

---

## 3. Update Edge Cases

### Update Non-existent User
- PATCH with invalid ID

Expected:
- 404 (in singular mode) or empty result

---

### Attempt to Modify System Fields
- Update created_at
- Update id

Purpose:
Ensure immutable fields remain protected.

---

## 4. Delete Edge Cases

### Delete Non-existent Record

Expected:
- 200/204 with no effect (idempotent behavior)

---

### Delete by Non-unique Field

Test:
- Delete using name filter

Purpose:
Ensure filter behavior matches expectation and does not over-delete unintentionally.

---

## 5. Filter Syntax Errors

Test:
- Invalid filter format (e.g., eq(12))

Expected:
- 400 error

Purpose:
Validate PostgREST query parameter enforcement.

---

## 6. Security Edge Cases

- Attempt to include unexpected fields (e.g., role)
- Attempt privilege escalation in payload
- Authorization bypass attempts

---

## Observations

- Database constraints enforce core integrity.
- Some validations depend on DB-level constraints rather than API validation.
- System correctly returns structured error responses for constraint violations.

---

## Conclusion

Edge case testing confirms:
- Strong constraint enforcement
- Proper error signaling
- Controlled update/delete behavior
- Stable RBAC enforcement

These scenarios reduce risk of data corruption and privilege misuse.

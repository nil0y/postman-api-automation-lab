# Authorization Matrix

## Objective

Validate role-based access control (RBAC) behavior for the `/users` endpoint exposed via PostgREST.

The system defines three roles:

- **Anon** – No authentication token
- **Reader** – Read-only access
- **Writer** – Full CRUD access

---

## Access Rules Overview

| Operation | Anon | Reader | Writer |
|------------|--------|---------|---------|
| GET /users | ❌ | ✅ | ✅ |
| GET /users?id=eq.X | ❌ | ✅ | ✅ |
| POST /users | ❌ | ❌ | ✅ |
| PATCH /users | ❌ | ❌ | ✅ |
| DELETE /users | ❌ | ❌ | ✅ |

---

## Detailed Behavior

### Anon (No Token)

Expected:
- Should NOT access protected endpoints.
- Should receive 401 or 403.

Validated:
- GET blocked
- POST blocked
- PATCH blocked
- DELETE blocked

---

### Reader Role

Expected:
- Can perform read operations only.
- Cannot modify data.

Validated:
- GET allowed (200)
- POST rejected (401/403)
- PATCH rejected (401/403)
- DELETE rejected (401/403)

---

### Writer Role

Expected:
- Full CRUD capability.

Validated:
- GET returns data
- POST creates user
- PATCH updates user
- DELETE removes user

---

## Observations

- Role enforcement is correctly applied at API layer.
- Unauthorized operations return structured error responses.
- No privilege escalation observed via payload manipulation.
- Client cannot

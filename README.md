# API Automation Lab

A structured API automation project built using Postman and PostgREST to demonstrate real-world API testing practices, role-based access control validation, and dynamic scripting techniques.

---

## Tech Stack

- Postman (Collection + Environment)
- JavaScript (Postman scripting)
- PostgREST
- PostgreSQL
- Docker

---

## Project Objective

Validate the `/users` endpoint exposed via PostgREST with a structured automation-ready approach covering:

- Functional validation
- Role-based authorization (RBAC)
- Data integrity enforcement
- Error consistency
- Contract validation
- Dynamic request chaining

---

## Test Coverage

- CRUD operations
- Role-based access control (Anon / Reader / Writer)
- Happy path scenarios
- Negative & edge case testing
- Constraint validation (NOT NULL, UNIQUE, PRIMARY KEY)
- Error response consistency
- Contract (schema/response shape) validation

---

## Key Automation Features

- Dynamic ID capture from responses
- Environment variable management
- Unique test data generation
- PostgREST singular object mode validation
- Defensive response assertions
- Collection structured for CI compatibility

---

## Automation Concepts Demonstrated

- JSON response parsing
- Conditional assertions
- Dynamic variable chaining across requests
- Multi-role test matrix validation
- API contract verification
- Database constraint behavior validation

---

## How to Run

1. Import the collection into Postman.
2. Import the environment file.
3. Select the environment.
4. Execute using Collection Runner.

(Newman CLI integration planned for CI automation.)

---

## Future Improvements

- Newman CLI integration
- GitHub Actions CI pipeline
- Automated test reporting
- Playwright API automation implementation

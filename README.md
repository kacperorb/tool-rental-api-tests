# Simple Tool Rental API — Postman Testing Portfolio

API testing project covering tool filtering, order management, input validation, authentication and access control.

## What I implemented

- Positive, negative and boundary test cases based on the API documentation.
- JavaScript assertions for status codes, data types, values and arrays.
- Request chaining using environment and collection variables.
- A complete order lifecycle: create → retrieve → update → delete.
- Access-control checks with two clients, including owner-side verification that rejected operations do not change or delete the order.

## Results and findings

The latest recorded runs produced **56 passed tests and 0 failed tests** across three folders:

| Folder | Passed | Failed |
|---|---:|---:|
| Tools positive tests | 22 | 0 |
| Orders CRUD | 14 | 0 |
| Orders access control | 20 | 0 |

These are executed Postman test blocks, not 56 distinct business scenarios. Separate negative and boundary tests are excluded from these totals. Results describe the recorded practice runs, not a guarantee of current API behavior.

- **Documented discrepancy:** `results=0` returned HTTP 200 and 20 tools despite the documented range of 1–20.
- **Clarification needed:** numeric-string tool IDs, whitespace-only customer names and empty category filters were accepted. Their intended handling requires clarification.

Reproduction steps and observations are included in the relevant request descriptions. Checks based on the known discrepancy or unresolved requirements may fail; do not interpret every failure as a confirmed API defect.

## How to run

1. Import [the collection](Tool-Rental-API.postman_collection.json) and [the environment template](Tool-Rental-API.example.postman_environment.json) into Postman. Select **Tool Rental API — local**.
2. Register two different API clients using the requests in **Setup**. Use unique fictional email addresses; if registration returns HTTP 409, change the address. Copy each returned `accessToken` into your local environment: client A into `apiToken`, client B into `apiTokenB`. Registration does not save tokens automatically.
3. Save the requests and run each test folder separately in Collection Runner with **one iteration**, preserving request order. Run Setup only when preparing credentials.
4. Do not run Orders CRUD and Orders access control concurrently: they share `createdorderId` and `customerName`. Both scenarios create an order and delete it at the end of a successful run.

The template contains the API base URL and empty token fields. Keep actual tokens local. Do not commit environment exports containing credentials. `Get all tools` prepares the variables used by `Get single tool`. Some checks assume the practice inventory contains particular tools or enough matching items. Accepted negative-input requests can create extra orders and do not automatically clean them up.

**Tools:** Postman, JavaScript, JSON, Collection Runner.  
**Context:** Portfolio project using a public practice API, developed with AI-assisted guidance and review. This is not a comprehensive security or performance assessment.

[API documentation](https://github.com/vdespa/quick-introduction-to-postman/blob/main/simple-tool-rental-api.md)

---
name: test-api
description: Test API endpoints from a URL or OpenAPI/Swagger spec file. Reports response status, headers, body, timing, and checks for common issues like missing CORS headers and improper error codes. Suggests follow-up tests.
---

# API Tester

Test the API endpoint or spec file provided by the user.

## Determine Input Type

- **File path** (ends in .json, .yaml, .yml) — treat as OpenAPI/Swagger spec
- **URL** (starts with http:// or https://) — test that endpoint directly

## If Given an OpenAPI/Swagger Spec

1. Read and parse the spec file
2. List all available endpoints grouped by tag/resource
3. Ask which endpoint(s) to test, or test all GET endpoints by default

## If Given a Direct URL

1. Determine HTTP method (default GET)
2. Fetch the endpoint
3. Report results

## Report For Each Endpoint

### Request
- HTTP method and full URL
- Headers sent
- Request body (if applicable)

### Response
- **Status code** and status text
- **Response time** assessment (Fast < 200ms, Acceptable 200ms-1s, Slow > 1s)
- **Headers** of interest:
  - Content-Type
  - Cache-Control
  - CORS headers (Access-Control-*)
  - Rate limit headers (X-RateLimit-*)
  - Security headers (X-Frame-Options, CSP, HSTS)
- **Body** — first 2000 characters, formatted as JSON if applicable

### Assessment
- Is the response valid JSON/XML as declared by Content-Type?
- Are error responses using appropriate HTTP status codes?
- Are CORS headers present (if it's a public API)?
- Any missing security headers?
- Is the response paginated? Note pagination mechanism.

## Follow-Up Suggestions

Based on the response, suggest:
- Related endpoints to test (e.g., if `/users` works, suggest `/users/{id}`)
- Error case tests (invalid IDs, missing auth, bad input)
- Edge cases (empty collections, special characters)

## Output Format

Format as a test report with pass/fail indicators:
- **Pass**: endpoint responds as expected
- **Warn**: works but has issues (missing headers, slow)
- **Fail**: returns errors or is unreachable

---
description: Test API endpoints and report on responses
argument-hint: <url-or-spec-file>
allowed-tools: [WebFetch, Read, Bash]
---

# API Tester

Test the API endpoint or spec provided: $ARGUMENTS

## If given an OpenAPI/Swagger spec file

1. Read the spec file
2. List all available endpoints grouped by tag/resource
3. Ask which endpoint(s) to test, or test all GET endpoints by default

## If given a direct URL

1. Determine the HTTP method (default GET, or infer from URL patterns)
2. Fetch the endpoint
3. Report results

## For each endpoint tested, report:

### Request
- HTTP method and full URL
- Headers sent
- Request body (if applicable)

### Response
- **Status code** and status text (with a quick assessment: 2xx = success, 4xx = client error, 5xx = server error)
- **Response time** — note if unusually slow
- **Headers** of interest:
  - Content-Type
  - Cache-Control
  - CORS headers (Access-Control-*)
  - Rate limit headers (X-RateLimit-*)
  - Security headers (X-Frame-Options, CSP, etc.)
- **Body** — first 2000 characters, formatted as JSON if applicable

### Assessment
- Is the response valid JSON/XML as declared by Content-Type?
- Are error responses using appropriate HTTP status codes?
- Are CORS headers present (if it looks like a public API)?
- Any missing security headers?
- Is the response paginated? If so, note pagination mechanism

## Follow-up suggestions

Based on the response, suggest:
- Related endpoints to test (e.g., if `/users` works, suggest `/users/{id}`)
- Error case tests (invalid IDs, missing auth, bad input)
- Edge cases (empty collections, special characters)

## Output format

Format as a clean test report with pass/fail indicators:
- Pass: endpoint responds as expected
- Warn: endpoint works but has issues (missing headers, slow, etc.)
- Fail: endpoint returns errors or is unreachable

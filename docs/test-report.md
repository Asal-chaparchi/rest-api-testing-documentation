
# REST API Test Execution Report

## 1. Project Information

**Project:** REST API Testing & Technical Documentation

**API Under Test:** JSONPlaceholder

**Base URL:** https://jsonplaceholder.typicode.com

**Testing Tool:** Postman

**Test Execution Date:** November 8, 2026

**Test Environment:** Public Test API

## 2. Test Execution Summary

| Metric | Result |
|---|---|
| Total API Requests | 10 |
| Total Assertions | 29 |
| Passed Assertions | 29 |
| Failed Assertions | 0 |
| Execution Errors | 0 |
| Collection Iterations | 1 |
| Total Execution Time | 6.192 seconds |
| Average Response Time | 353 ms |

**Overall Result:** PASSED

All 29 automated assertions passed during
the recorded Postman Collection Runner execution.

## 3. Test Coverage

| Test ID | Method | Scenario | Result |
|---|---|---|---|
| TC-001 | GET | Retrieve post by valid ID | PASSED |
| TC-002 | GET | Retrieve all posts | PASSED |
| TC-003 | GET | Filter posts by user ID | PASSED |
| TC-004 | GET | Retrieve nonexistent post | PASSED |
| TC-005 | POST | Create a new post | PASSED |
| TC-006 | POST | Submit post without title | PASSED |
| TC-007 | PUT | Update an existing post | PASSED |
| TC-008 | DELETE | Delete a post | PASSED |
| TC-009 | GET | Test upper dataset boundary | PASSED |
| TC-010 | GET | Test beyond upper boundary | PASSED |

## 4. Test Types

### Positive Testing

Verified successful GET, POST, PUT, and
DELETE responses using valid inputs.

### Negative Testing

Verified HTTP 404 responses for nonexistent
posts and examined POST behavior when
the title field was omitted.

### Boundary Testing

Tested post ID 100 and post ID 101
to examine the boundary of the sample dataset.

### Automated Assertions

Validated HTTP status codes, JSON response
structures, field values, data types,
and response contents using Postman scripts.

## 5. Observed API Behavior

### Observation 1: Missing Title Accepted

**Test Case:** TC-006

**Request:** POST /posts

**Input:** JSON body without the title field.

**Actual Result:** HTTP 201 Created

**Finding:** The API accepted the request.

**Classification:** Observed behavior;
not a confirmed defect.

### Observation 2: Simulated Write Operations

JSONPlaceholder simulates POST, PUT,
and DELETE operations.

Changes are not permanently persisted.

**Classification:** Known API limitation.

### Observation 3: Nonexistent Posts

GET requests for nonexistent post IDs
returned HTTP 404 with an empty JSON object.

**Classification:** Expected behavior.

## 6. Bug Report Summary

No confirmed defects were identified
during the documented test execution.

The observed acceptance of a POST request
without a title was not classified as a bug
because mandatory title validation was
not established as an API requirement.

## 7. Test Limitations

- Tests were executed against a public mock API.
- No authentication or authorization testing.
- No load or stress testing.
- No security testing.
- No persistent database verification.
- Only selected negative and boundary cases were tested.
- Response-time performance thresholds were not defined.

## 8. Evidence

Postman Collection Runner execution:

- 10 API requests
- 29 passed assertions
- 0 failed assertions
- 0 execution errors

Evidence screenshot:

`screenshots/collection-run-results.png`

## 9. Final Conclusion

The tested JSONPlaceholder endpoints
behaved as expected for the documented scenarios.

All 29 automated assertions passed
during the recorded collection execution.

The project demonstrates practical experience
in REST API testing, test case design,
JSON validation, automated assertions,
technical documentation, and OpenAPI.


# REST API Test Cases

**Project:** REST API Testing & Technical Documentation  
**API:** JSONPlaceholder  
**Base URL:** https://jsonplaceholder.typicode.com  
**Testing Tool:** Postman

## Test Cases

| Test ID | Endpoint | Scenario | Input | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-001 | GET /posts/1 | Retrieve an existing post | ID=1 | HTTP 200; post ID=1 | HTTP 200; ID=1; 2 assertions passed | PASSED |
| TC-002 | GET /posts | Retrieve all posts | No parameters | HTTP 200; array of 100 posts | HTTP 200; 100 posts; 5 assertions passed | PASSED |
| TC-003 | GET /posts?userId=1 | Filter posts by user ID | userId=1 | HTTP 200; non-empty array; all userId=1 | HTTP 200; 3 assertions passed | PASSED |
| TC-004 | GET /posts/999999 | Retrieve nonexistent post | ID=999999 | HTTP 404; empty object | HTTP 404; empty object; 2 assertions passed | PASSED |
| TC-005 | POST /posts | Create a post | Valid JSON | HTTP 201; generated ID | HTTP 201; ID=101; 3 assertions passed | PASSED |
| TC-006 | POST /posts | Submit without title | JSON without title | Observe behavior for missing title | HTTP 201; ID=101; 3 assertions passed | PASSED |
| TC-007 | PUT /posts/1 | Update an existing post | Valid JSON | HTTP 200; updated data returned | HTTP 200; updated values; 4 assertions passed | PASSED |
| TC-008 | DELETE /posts/1 | Delete an existing post | ID=1 | HTTP 200; empty object | HTTP 200; empty object; 2 assertions passed | PASSED |
| TC-009 | GET /posts/100 | Test upper dataset boundary | ID=100 | HTTP 200; post ID=100 | HTTP 200; ID=100; 3 assertions passed | PASSED |
| TC-010 | GET /posts/101 | Test beyond upper boundary | ID=101 | HTTP 404; empty object | HTTP 404; empty object; 2 assertions passed | PASSED |

## Test Execution Summary

- Execution Method: Postman Collection Runner
- Collection Iterations: 1
- Total API Requests: 10
- Total Assertions: 29
- Passed Assertions: 29
- Failed Assertions: 0
- Execution Errors: 0
- Total Run Duration: 6.192 seconds
- Average Response Time: 353 ms

## Observations

1. JSONPlaceholder simulates POST, PUT, and DELETE operations without permanent data persistence.
2. A POST request without the `title` field returned HTTP 201.
3. GET requests for nonexistent posts returned HTTP 404 with an empty JSON object.
4. All 29 assertions passed during the recorded Collection Runner execution.

## Test Limitations

- No authentication or authorization testing was performed.
- Persistent database changes were not verified.
- Load, stress, and security testing were outside the project scope.
- Validation behavior was tested only for selected inputs.


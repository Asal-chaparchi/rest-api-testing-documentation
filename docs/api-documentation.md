# REST API Technical Documentation

## 1. API Overview

**API Name:** JSONPlaceholder Posts API  
**Base URL:** https://jsonplaceholder.typicode.com  
**Response Format:** JSON  
**Testing Tool:** Postman  
**Authentication:** Not required

### Purpose

Document the request formats, response structures, status codes, tested behaviors, and limitations of the JSONPlaceholder Posts API.

### Scope

This document covers the following operations:

| Operation | HTTP Method | Endpoint | Related Test Cases |
|---|---|---|---|
| Retrieve a post | GET | `/posts/{id}` | TC-001, TC-004, TC-009, TC-010 |
| Retrieve all posts | GET | `/posts` | TC-002 |
| Filter posts by user | GET | `/posts?userId={userId}` | TC-003 |
| Create a post | POST | `/posts` | TC-005, TC-006 |
| Replace a post | PUT | `/posts/{id}` | TC-007 |
| Delete a post | DELETE | `/posts/{id}` | TC-008 |

### General Limitations

- JSONPlaceholder uses predefined sample data.
- POST, PUT, and DELETE simulate write operations; changes are not permanently persisted.
- The tested dataset contains 100 posts, with IDs from 1 through 100.
- No authentication, load, security, or persistent database verification was performed.
- Results describe the observed responses and should not be generalized into untested validation rules.

---

## 2. Get Post by ID

### Description

Retrieves a single post using its ID.

**HTTP Method:** `GET`  
**Endpoint:** `/posts/{id}`  
**Request Body:** Not required

### Path Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| id | Integer | Yes | Identifier of the requested post |

### Example Request

```http
GET https://jsonplaceholder.typicode.com/posts/1
```

### Example Response — 200 OK

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| userId | Integer | User identifier |
| id | Integer | Post identifier |
| title | String | Post title |
| body | String | Post content |

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Existing post returned |
| 404 Not Found | Requested post not found in the sample dataset |

### Error Response Example — 404 Not Found

Observed for `/posts/999999` and `/posts/101`:

```json
{}
```

### Tested Behavior

| Test Case | Input | Actual Result | Assertions |
|---|---|---|---|
| TC-001 | `id=1` | HTTP 200; response ID equals 1 | 2 passed |
| TC-004 | `id=999999` | HTTP 404; empty JSON object | 2 passed |
| TC-009 | `id=100` | HTTP 200; response ID equals 100 | 3 passed |
| TC-010 | `id=101` | HTTP 404; empty JSON object | 2 passed |

### Limitations

The upper-boundary test refers to the sample dataset, not a general rule prohibiting all IDs greater than 100. Malformed nonnumeric IDs were not tested.

---

## 3. Get All Posts

### Description

Retrieves all posts in the predefined sample dataset.

**HTTP Method:** `GET`  
**Endpoint:** `/posts`  
**Request Parameters:** None required  
**Request Body:** Not required

### Example Request

```http
GET https://jsonplaceholder.typicode.com/posts
```

### Example Response — 200 OK

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  }
]
```

**Note:** This is a shortened example showing the first array element. The actual tested response contained 100 posts.

### Response Structure

An array of post objects. Each object includes the `userId`, `id`, `title`, and `body` fields.

| Field | Expected Type |
|---|---|
| userId | Integer |
| id | Integer |
| title | String |
| body | String |

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Posts returned successfully |

### Tested Behavior

**Test Case:** TC-002

- HTTP status: 200 OK
- Response: JSON array
- Number of returned posts: 100
- Presence of required fields on the first post: verified
- Data types on the first post: verified
- Automated assertions: 5 passed

### Error Handling and Limitations

Error responses for this endpoint were not tested. Pagination behavior was not tested. Data represents a fixed sample dataset.

---

## 4. Get Posts by User ID

### Description

Retrieves posts matching a specified user ID.

**HTTP Method:** `GET`  
**Endpoint:** `/posts?userId={userId}`  
**Request Body:** Not required

### Query Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| userId | Integer | No | Optional filter for posts belonging to a user |

### Example Request

```http
GET https://jsonplaceholder.typicode.com/posts?userId=1
```

### Example Response — 200 OK

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  }
]
```

**Note:** This is a shortened response example with one matching post. The endpoint returns an array of matching posts.

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Filter request processed successfully |

### Tested Behavior

**Test Case:** TC-003

- Query parameter: `userId=1`
- HTTP status: 200 OK
- Response type: JSON array
- Response was non-empty
- Every returned item had `userId=1`
- Automated assertions: 3 passed

### Error Handling and Limitations

Invalid query parameter types and other filter values were not tested. No validation behavior for those inputs is claimed.

---

## 5. Create a Post

### Description

Simulates creating a post using a JSON request body.

**HTTP Method:** `POST`  
**Endpoint:** `/posts`

### Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

### Request Body Fields

| Field | Expected Type | Description |
|---|---|---|
| title | String | Post title |
| body | String | Post content |
| userId | Integer | Author's user identifier |

**Validation note:** The `title` field was omitted in TC-006 and the API still returned HTTP 201. This does not establish a universal rule for required fields.

### Example Request

```http
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json
```

```json
{
  "title": "API Testing Practice",
  "body": "This post was created using Postman.",
  "userId": 1
}
```

### Example Response — 201 Created

```json
{
  "title": "API Testing Practice",
  "body": "This post was created using Postman.",
  "userId": 1,
  "id": 101
}
```

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 201 Created | Creation request processed in this simulated API |

### Tested Behavior

**TC-005 — Valid request**

- HTTP status: 201 Created
- Response included ID 101
- Automated assertions: 3 passed

**TC-006 — Missing title**

Request body:

```json
{
  "body": "Testing a request without a title.",
  "userId": 1
}
```

Observed response:

```json
{
  "body": "Testing a request without a title.",
  "userId": 1,
  "id": 101
}
```

- HTTP status: 201 Created
- The `title` property was absent in the response
- Automated assertions: 3 passed

### Error Handling

A missing `title` was not rejected in the tested scenario. Malformed JSON, incorrect data types, and other missing fields were not tested. No bug was confirmed.

### Limitations

The returned `id=101` does not represent permanent creation. The official API guide notes that a subsequent `GET /posts/101` returns 404.

---

## 6. Update a Post

### Description

Simulates replacing the fields of an existing post.

**HTTP Method:** `PUT`  
**Endpoint:** `/posts/{id}`

### Path Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| id | Integer | Yes | Identifier of the post to replace |

### Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

### Request Body Fields

| Field | Expected Type | Description |
|---|---|---|
| id | Integer | Post identifier |
| title | String | Replacement title |
| body | String | Replacement content |
| userId | Integer | User identifier |

### Example Request

```http
PUT https://jsonplaceholder.typicode.com/posts/1
Content-Type: application/json
```

```json
{
  "id": 1,
  "title": "Updated API Testing Post",
  "body": "This post was updated using PUT in Postman.",
  "userId": 1
}
```

### Example Response — 200 OK

```json
{
  "id": 1,
  "title": "Updated API Testing Post",
  "body": "This post was updated using PUT in Postman.",
  "userId": 1
}
```

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Simulated update request processed successfully |

### Tested Behavior

**Test Case:** TC-007

- HTTP status: 200 OK
- Returned post ID: 1
- Returned title matched the submitted title
- Returned body matched the submitted body
- Automated assertions: 4 passed

### Error Handling and Limitations

Invalid bodies and nonexistent IDs were not tested with PUT. Matching response values do not prove that the update was permanently saved. The API simulates the update.

---

## 7. Delete a Post

### Description

Simulates deleting an existing post by its ID.

**HTTP Method:** `DELETE`  
**Endpoint:** `/posts/{id}`  
**Request Body:** Not required

### Path Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| id | Integer | Yes | Identifier of the post to delete |

### Example Request

```http
DELETE https://jsonplaceholder.typicode.com/posts/1
```

### Example Response — 200 OK

```json
{}
```

### HTTP Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Simulated delete request processed successfully |

### Tested Behavior

**Test Case:** TC-008

- Requested post ID: 1
- HTTP status: 200 OK
- Response body: empty JSON object
- Automated assertions: 2 passed

### Error Handling and Limitations

Deletion of nonexistent IDs was not tested. The successful response does not prove that the post was permanently removed; deletion is simulated.

---

## 8. Testing Notes and Evidence

### Execution Summary

The Postman Collection Runner was executed once with all 10 requests selected.

| Metric | Recorded Result |
|---|---|
| API requests | 10 |
| Automated assertions | 29 |
| Passed assertions | 29 |
| Failed assertions | 0 |
| Execution errors | 0 |
| Total run duration | 6.192 seconds |
| Average response time | 353 ms |

### Classification of Findings

- **Confirmed defects:** None identified in the tested scenarios.
- **Observed behavior:** POST without `title` returned HTTP 201.
- **Known simulation limitation:** POST, PUT, and DELETE do not persist changes.
- **Untested areas:** Authentication, security, load, malformed JSON, broad input validation, and persistent data verification.

### Related Project Files

- `postman/api-tests.postman_collection.json` — exported requests and assertions
- `docs/test-cases.md` — test scenarios, expectations, actual results, and pass/fail status
- `docs/test-report.md` — final execution report (to be prepared)
- `openapi.yaml` — OpenAPI specification (to be prepared)
- `screenshots/` — selected execution evidence

### Reference

Official JSONPlaceholder guide: https://jsonplaceholder.typicode.com/guide/

This documentation records actual observations from the project and distinguishes them from general behavior described by the official API guide.

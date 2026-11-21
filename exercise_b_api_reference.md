
# EXERCISE B: API REFERENCE ENTRY

## API Documentation: Create a New Task

### 1. Overview

The Create Task API allows an authenticated user to create a new task within a project management application.

Users can provide a task title, description, assignee, due date and priority level.

When a task is successfully created, the API returns the task details and a unique task ID.

### 2. HTTP Method and Endpoint

**HTTP Method:** POST

**Endpoint:**

`/v1/projects/{project_id}/tasks`

**Description:**

Creates a new task in the specified project. Only authenticated users with permission to create tasks can use this endpoint.

### 3. Request Parameters

#### A. Path Parameters

| Parameter | Data Type | Required | Description |
|---|---|---|---|
| project_id | Integer | Yes | Unique ID of the project where the task will be created. |

#### B. Query Parameters

No query parameters are required.

#### C. Body Parameters

| Parameter | Data Type | Required | Description |
|---|---|---|---|
| title | String | Yes | Name or title of the task. |
| description | String | No | Additional information about the task. |
| assignee_id | Integer | Yes | ID of the user assigned to complete the task. |
| due_date | String (Date) | Yes | Deadline in YYYY-MM-DD format. |
| priority | String | Yes | Task priority: low, medium or high. |

### 4. Required Request Headers

| Header | Required | Description |
|---|---|---|
| Authorization | Yes | Contains the user's access token. |
| Content-Type | Yes | Specifies that the request body is JSON. |
| Accept | No | Indicates that the client expects a JSON response. |

Example:

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
Accept: application/json
```

### 5. Example Request Body

```json
{
  "title": "Complete Project Documentation",
  "description": "Prepare and review the final project documentation.",
  "assignee_id": 105,
  "due_date": "2026-12-15",
  "priority": "high"
}
```

### 6. Example API Request

```http
POST /v1/projects/25/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
Accept: application/json

{
  "title": "Complete Project Documentation",
  "description": "Prepare and review the final project documentation.",
  "assignee_id": 105,
  "due_date": "2026-12-15",
  "priority": "high"
}
```

### 7. Successful Response

**HTTP Status Code: 201 Created**

This means the task was successfully created.

Example JSON response:

```json
{
  "success": true,
  "message": "Task created successfully.",
  "data": {
    "id": 501,
    "project_id": 25,
    "title": "Complete Project Documentation",
    "description": "Prepare and review the final project documentation.",
    "assignee_id": 105,
    "due_date": "2026-12-15",
    "priority": "high",
    "status": "pending",
    "created_at": "2026-11-21T08:30:00Z"
  }
}
```

### 8. HTTP Response Codes

| Status Code | Name | Explanation |
|---|---|---|
| 201 | Created | The task was successfully created. |
| 400 | Bad Request | The request contains invalid JSON or malformed data. |
| 401 | Unauthorized | The user is not authenticated or the access token is invalid or expired. |
| 403 | Forbidden | The user does not have permission to create tasks in the project. |
| 404 | Not Found | The specified project or assignee does not exist. |
| 409 | Conflict | The request conflicts with the current state of the project or task records. |
| 415 | Unsupported Media Type | The request does not use the supported JSON content type. |
| 422 | Unprocessable Entity | The request contains invalid values, such as an unsupported priority or an assignee who is not a project member. |
| 429 | Too Many Requests | The user has exceeded the allowed API request limit. |
| 500 | Internal Server Error | An unexpected server-side error occurred. |

### 9. Validation Rules

The API should apply the following validation rules:

1. The task title must not be empty.
2. The description is optional.
3. The assignee ID must identify an existing user who belongs to the project.
4. The due date must use YYYY-MM-DD format.
5. The priority must be low, medium or high.
6. The user must be authenticated and authorized to create tasks.

### 10. Conclusion

The Create Task API provides a structured way for authenticated users to add tasks to projects.

It uses the POST HTTP method and accepts JSON data containing task details.

Proper authentication, parameter validation and HTTP response codes help ensure that the API is secure, reliable and easy for developers to integrate into their applications.

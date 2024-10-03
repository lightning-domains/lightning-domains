# Delete Walias

### Endpoint

`DELETE /walias/{name}`

### Description

Deletes an existing walias.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name | In   | Type   | Required | Description                |
| ---- | ---- | ------ | -------- | -------------------------- |
| name | path | string | Yes      | The walias name to delete. |

### Responses

#### 200 OK

**Description:** Walias deleted successfully.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": true
}
```

#### 401 Unauthorized

**Description:** Authentication required.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Authentication required"
}
```

#### 403 Forbidden

**Description:** Invalid or expired authentication.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Invalid authentication"
}
```

#### 404 Not Found

**Description:** Walias not found.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Walias not found"
}
```

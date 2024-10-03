# Update Walias

### Endpoint

`PUT /walias/{name}`

### Description

Update walias data or transfer ownership to a new pubkey.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name | In   | Type   | Required | Description                  |
| ---- | ---- | ------ | -------- | ---------------------------- |
| name | path | string | Yes      | The walias name to transfer. |

### Request Body

**Content-Type:** `application/json`
**Schema:**

```json
{
  "pubkey": "string"
}
```

### Responses

#### 200 OK

**Description:** Walias transferred successfully.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": true
}
```

#### 400 Bad Request

**Description:** Invalid pubkey.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Invalid pubkey"
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

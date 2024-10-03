# Get Walias Public Data

### Endpoint

`GET /walias/{name}`

### Description

Checks if a walias name is available or already registered.

### Parameters

| Name | In   | Type   | Required | Description               |
| ---- | ---- | ------ | -------- | ------------------------- |
| name | path | string | Yes      | The walias name to check. |

### Responses

#### 200 OK

**Description:** Walias availability status.
**Content-Type:** `application/json`
**Schema:** One of the following objects.

- **If the walias is available:**

```json
{
  "available": true,
  "quote": {
    "price": "integer",
    "data": {
      "type": "string"
    }
  }
}
```

**Example:**

```json
{
  "available": true,
  "quote": {
    "price": 10000,
    "data": {
      "type": "short"
    }
  }
}
```

- **If the walias is not available:**

```json
{
  "available": false,
  "pubkey": "string"
}
```

**Example:**

```json
{
  "available": false,
  "pubkey": "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd"
}
```

#### 404 Not Found

**Description:** Walias not found.**Content-Type:** `application/json`**Example:**

```json
{
  "success": false,
  "reason": "Walias not found"
}
```

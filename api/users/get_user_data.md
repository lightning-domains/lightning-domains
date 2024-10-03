# Get User Data

### Endpoint

### `GET /users/{pubkey}`

### Description

Fetches the details (names and relays) associated with a given public key.

### Parameters

| Name   | In   | Type   | Required | Description       |
| ------ | ---- | ------ | -------- | ----------------- |
| pubkey | path | string | Yes      | User's public key |

### Responses

#### 200 OK

**Content-Type:** `application/json`
**Example Response:**

```json
{
  "names": ["some", "handles"],
  "relays": ["wss://relay.url"]
}
```

#### 404 Not Found

**Content-Type:** `application/json`
**Example Response:**

```json
{
  "success": false,
  "reason": "User not found"
}
```

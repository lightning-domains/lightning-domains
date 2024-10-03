# Update User Data

### Endpoint

`PUT /users/{pubkey}`

### Description

Update relay list for the user.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name   | In   | Type   | Required | Description       |
| ------ | ---- | ------ | -------- | ----------------- |
| pubkey | path | string | Yes      | User's public key |

### Request Body

**Content-Type:** `application/json`
**Schema:**

```jsonc
{
  "relays": ["string"]
}
```

### Responses

#### 200 OK

**Content-Type:** `application/json`
**Example Response:**

```jsonc
{
  "names": ["some", "handles"],
  "relays": ["wss://relay.url"]
}
```

#### 400 Bad Request

**Content-Type:** `application/json`
**Example Response:**

```jsonc
{
  "success": false,
  "reason": "Invalid pubkey"
}
```

#### 401 Unauthorized

**Content-Type:** `application/json`
**Example Response:**

```jsonc
{
  "success": false,
  "reason": "Authentication required"
}
```

#### 403 Forbidden

**Content-Type:** `application/json`
**Example Response:**

```jsonc
{
  "success": false,
  "reason": "Invalid authentication"
}
```

#### 404 Not Found

**Content-Type:** `application/json`
**Example Response:**

```jsonc
{
  "success": false,
  "reason": "User not found"
}
```

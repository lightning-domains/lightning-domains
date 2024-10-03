# Update Wallet by ID

### Endpoint

`PUT /wallets/{walletId}`

### Description

Updates the wallet configuration.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name     | In   | Type   | Required | Description    |
| -------- | ---- | ------ | -------- | -------------- |
| walletId | path | string | Yes      | The wallet ID. |

### Request Body

**Content-Type:** `application/json`
**Schema:**

```json
{
  "config": {
    "tag": "string",
    "callback": "string",
    "maxSendable": "number",
    "minSendable": "number",
    "metadata": "string"
  },
  "priority": "integer"
}
```

### Responses

#### 200 OK

**Description:** Wallet updated successfully.
**Content-Type:** `application/json`
**Example:**

```json
{
  "id": "wallet_id",
  "config": {
    "tag": "payRequest",
    "callback": "https://callback.url",
    "maxSendable": 100000,
    "minSendable": 1000,
    "metadata": "metadata"
  },
  "priority": 1,
  "provider": "json"
}
```

#### 400 Bad Request

**Description:** Invalid input.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Invalid input"
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

**Description:** Wallet not found.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Wallet not found"
}
```

# Get Wallet by ID

### Endpoint

`GET /wallets/{walletId}`

### Description

Retrieves the wallet by its ID.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name     | In   | Type   | Required | Description    |
| -------- | ---- | ------ | -------- | -------------- |
| walletId | path | string | Yes      | The wallet ID. |

### Responses

#### 200 OK

**Description:** Wallet data retrieved successfully.
**Content-Type:** `application/json`
**Schema:**

```json
{
  "id": "string",
  "config": {
    "tag": "string",
    "callback": "string",
    "maxSendable": "number",
    "minSendable": "number",
    "metadata": "string"
  },
  "priority": "integer",
  "provider": "string",
  "pubkey": "string",
  "walias": ["string"]
}
```

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
  "provider": "json",
  "pubkey": "pubkey",
  "walias": ["some_walias"]
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

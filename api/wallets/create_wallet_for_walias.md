# Create Wallet for Walias (Authenticated)

### Endpoint

`POST /walias/{name}/wallets`

### Description

Creates a wallet for a specific walias. You can choose the wallet ID.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name | In   | Type   | Required | Description      |
| ---- | ---- | ------ | -------- | ---------------- |
| name | path | string | Yes      | The walias name. |

### Request Body

**Content-Type:** `application/json`
**Schema:**

```jsonc
{
  "id": "string (optional)",
  "config": {
    "tag": "string",
    "callback": "string",
    "maxSendable": "number",
    "minSendable": "number",
    "metadata": "string"
  },
  "priority": "integer",
  "provider": "string"
}
```

### Responses

#### 201 Created

**Description:** Wallet created successfully.
**Content-Type:** `application/json`
**Example:**

```jsonc
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

#### 401 Unauthorized

**Description:** Authentication required.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "success": false,
  "reason": "Authentication required"
}
```

#### 403 Forbidden

**Description:** Invalid or expired authentication.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "success": false,
  "reason": "Invalid authentication"
}
```

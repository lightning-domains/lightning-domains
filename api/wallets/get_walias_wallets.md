# Get Wallets from a Specific Walias

### Endpoint

`GET /walias/{name}/wallets`

### Description

Gets the wallets associated with a specific walias.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name | In   | Type   | Required | Description      |
| ---- | ---- | ------ | -------- | ---------------- |
| name | path | string | Yes      | The walias name. |

### Responses

#### 200 OK

**Description:** Wallets retrieved successfully.
**Content-Type:** `application/json`
**Schema:** An array of wallet objects.
**Example:**

```json
[
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
]
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

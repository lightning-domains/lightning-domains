# Delete Wallet by ID

### Endpoint

`DELETE /wallets/{walletId}`

### Description

Permanently deletes the wallet configuration.

### Authentication

Authentication is required using NostrAuth.

### Parameters

| Name     | In   | Type   | Required | Description    |
| -------- | ---- | ------ | -------- | -------------- |
| walletId | path | string | Yes      | The wallet ID. |

### Responses

#### 200 OK

**Description:** Wallet deleted successfully.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "success": true
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

#### 404 Not Found

**Description:** Wallet not found.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "success": false,
  "reason": "Wallet not found"
}
```

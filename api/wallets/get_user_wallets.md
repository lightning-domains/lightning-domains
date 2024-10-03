# Get Wallets from a Specific User

Gets the wallets associated with a specific user.

- **Endpoint:** `GET /users/{pubkey}/wallets`

- **Tags:** Wallet

- **Authentication:** Required (NostrAuth)

---

### Parameters

| Name   | In   | Type   | Required | Description       |
| ------ | ---- | ------ | -------- | ----------------- |
| pubkey | path | string | Yes      | User's public key |

---

### Responses

#### 200 OK

**Description:** Wallets retrieved successfully.
**Content-Type:** `application/json`
**Schema:** An array of wallet objects.
**Wallet Object Schema:**

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

**Description:** Authentication is required for this endpoint.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Authentication required"
}
```

#### 403 Forbidden

**Description:** The authentication provided is invalid or has expired.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "Invalid authentication"
}
```

#### 404 Not Found

**Description:** The specified user does not exist.
**Content-Type:** `application/json`
**Example:**

```json
{
  "success": false,
  "reason": "User not found"
}
```

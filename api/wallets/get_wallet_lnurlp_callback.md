# Get Wallet LNURLP Callback

### Endpoint

`GET /wallets/{walletId}/lnurlp/callback`

### Description

Retrieves the LNURL-Pay callback response for the wallet ID.

### Parameters

| Name     | In    | Type    | Required | Description                     |
| -------- | ----- | ------- | -------- | ------------------------------- |
| walletId | path  | string  | Yes      | The wallet ID.                  |
| amount   | query | integer | Yes      | Amount in millisatoshis (msat). |

### Responses

#### 200 OK

**Description:** LNURL-Pay callback response retrieved successfully.**Content-Type:** `application/json`
**Schema:**

```jsonc
{
  "pr": "string",
  "routes": [],
  "verify": "string"
}
```

**Example:**

```jsonc
{
  "pr": "lnbc1...",
  "routes": [],
  "verify": "https://example.com/verify"
}
```

#### 400 Bad Request

**Description:** Invalid request parameters.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "status": "ERROR",
  "reason": "Invalid request parameters"
}
```

#### 404 Not Found

**Description:** Wallet not found.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "status": "ERROR",
  "reason": "Wallet not found"
}
```

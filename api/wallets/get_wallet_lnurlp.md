# Get Wallet LNURLP

### Endpoint

`GET /wallets/{walletId}/lnurlp`

### Description

Retrieves the LNURL-Pay response (LUD-06) for the wallet ID.

### Parameters

| Name     | In   | Type   | Required | Description    |
| -------- | ---- | ------ | -------- | -------------- |
| walletId | path | string | Yes      | The wallet ID. |

### Responses

#### 200 OK

**Description:** LNURL-Pay response retrieved successfully.**Content-Type:** `application/json`
**Schema:**

```jsonc
{
  "tag": "string",
  "callback": "string",
  "maxSendable": "integer",
  "minSendable": "integer",
  "metadata": "string"
}
```

**Example:**

```jsonc
{
  "tag": "payRequest",
  "callback": "https://lightningdomains.io/wallets/{walletId}/lnurlp/callback",
  "maxSendable": 1000000000,
  "minSendable": 1000,
  "metadata": "[[\"text/plain\", \"Test\"]]",
  "payerData": {
    "name": { "mandatory": boolean },
    "pubkey": { "mandatory": boolean },
    "identifier": { "mandatory": boolean },
    "email": { "mandatory": boolean },
    "auth": {
       "mandatory": boolean,
       "k1": string // hex encoded 32 bytes of challenge
    },
    // ...other fields may be negotiated
  },
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

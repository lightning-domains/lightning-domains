# Register Walias

### Endpoint

`POST /walias/{name}`

### Description

Registers a new walias to the given pubkey.

### Parameters

| Name | In   | Type   | Required | Description                  |
| ---- | ---- | ------ | -------- | ---------------------------- |
| name | path | string | Yes      | The walias name to register. |

### Request Body

**Content-Type:** `application/json`
**Schema:**

```jsonc
{
  "pubkey": "string"
}
```

### Responses

#### 201 Created

**Description:** Walias registered (Free).
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "walias": "name@domain",
  "pubkey": "23123123..."
}
```

#### 202 Accepted

**Description:** Walias pending payment.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "walias": "name@domain",
  "invoice": "lnbc700u1pn0fewqpp...",
  "referenceId": "9j47dzaqrykna2pjnaepjgnv3wsdp4fey4qtfsx5sx7u",
  "relays": ["wss://relay.domain.com"],
  "verify": "https://url_lnurl21_compatible.com/check"
}
```

#### 400 Bad Request

**Description:** Invalid input.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "reason": "Invalid pubkey"
}
```

#### 409 Conflict

**Description:** Already taken or not available.
**Content-Type:** `application/json`
**Example:**

```jsonc
{
  "reason": "Already taken or not available"
}
```

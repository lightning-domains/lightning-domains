# Verify Walias Payment

### Endpoint

`GET /walias/payment/{verificationId}`

### Description

Checks if payment is already settled.

### Parameters

| Name           | In   | Type   | Required | Description                         |
| -------------- | ---- | ------ | -------- | ----------------------------------- |
| verificationId | path | string | Yes      | The verification ID of the payment. |

### Responses

#### 200 OK

**Content-Type:** `application/json`**Example Response:**

```jsonc
{
  "status": "OK",
  "settled": true,
  "preimage": "123456...",
  "pr": "lnbc10..."
}
```

#### 402 Payment Required

**Content-Type:** `application/json`**Example Response:**

```jsonc
{
  "status": "OK",
  "settled": false,
  "preimage": null,
  "pr": "lnbc10..."
}
```

#### 404 Not Found

**Content-Type:** `application/json`**Example Response:**

```jsonc
{
  "status": "ERROR",
  "reason": "Not found"
}
```

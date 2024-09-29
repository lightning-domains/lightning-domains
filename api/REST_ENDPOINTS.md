# API Endpoints

A **walias** is the resulting address of `name@domain`.
There are two models: `walias` and `pubkey`.
A `pubkey` can have multiple `walias`.

---

## Get Pubkey Data

**GET** `/pubkey/{pubkey}`

#### Description:

Fetches the details (names and relays) associated with a given public key.

#### Response:

- **200 OK** (Success)

```json
{
  "names": ["some", "handles"],
  "relays": ["wss://relay.url"]
}
```

---

## Set Pubkey Relays (Authenticated)

**PUT** `/pubkey/{pubkey}`

#### Description:

Update relayList for the pubkey.

#### Request Body:

```json
{
  "relays": ["wss://relay.url"]
}
```

#### Response:

- **200 OK** (Success)

```json
{
  "names": ["some", "handles"],
  "relays": ["wss://relay.url"]
}
```

- **400 Bad Request** (Invalid pubkey)

```json
{
  "success": false,
  "reason": "Invalid pubkey"
}
```

- **401 Unauthorized** (Authentication Required)

```json
{
  "success": false,
  "reason": "Authentication required"
}
```

- **403 Forbidden** (Invalid or Expired Authentication)

```json
{
  "success": false,
  "reason": "Invalid authentication"
}
```

---

## Get walias public data

**GET** `/walias/{name}`

#### Description:

Checks if a walias name is available or already registered. If registered, returns the associated `pubkey`.

#### Response:

- **200 OK** (Success)
  - **Available Name** :

```json
{
  "available": true,
  "quote": {
    "price": 10000,
    "data": {
      "type": "short"
    }
  }
}
```

- **Unavailable Name (Already Registered)** :

```json
{
  "available": false,
  "pubkey": "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd"
}
```

---

## Register Walias

**POST** `/walias/{name}`

#### Description:

Registers a new walias to the given `pubkey`.

#### Request Body:

```json
{
  "pubkey": "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd"
}
```

#### Response:

- **201 Created** (Walias Registered)

```json
{
  "walias": "name@domain",
  "invoice": "lnbc700u1pn0fewqpp...",
  "referenceId": "9j47dzaqrykna2pjnaepjgnv3wsdp4fey4qtfsx5sx7u", // e tag of the zapReceipt to be published
  "relays": ["wss://relay.domain.com"], // Relays where zapReceipt will be published
  "verify": "https://url_lnurl21_compatible.com/check",
  "relays": ["wss://relay.domain.com"] // Relays where zapReceipt will be published
}
```

- **400 Bad Request** (Invalid Input)

```json
{
  "reason": "Invalid pubkey"
}
```

- **409 Conflict**

```json
{
  "reason": "Already taken or not available"
}
```

---

## Transfer Walias (Authenticated)

**PUT** `/walias/{name}`

#### Description:

Transfers the walias ownership to a new `pubkey`.

#### Request Body:

```json
{
  "pubkey": "1bd91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd"
}
```

#### Response:

- **200 OK** (Success)

```json
{
  "success": true
}
```

- **400 Bad Request** (Invalid pubkey)

```json
{
  "success": false,
  "reason": "Invalid pubkey"
}
```

- **401 Unauthorized** (Authentication Required)

```json
{
  "success": false,
  "reason": "Authentication required"
}
```

- **403 Forbidden** (Invalid or Expired Authentication)

```json
{
  "success": false,
  "reason": "Invalid authentication"
}
```

---

## Delete Walias (Authenticated)

**DELETE** `/walias/{name}`

#### Description:

Deletes an existing walias.

#### Response:

- **200 OK** (Success)

```json
{
  "success": true
}
```

- **404 Not Found** (Walias Not Found)

```json
{
  "success": false,
  "reason": "Walias not found"
}
```

- **401 Unauthorized** (Authentication Required)

```json
{
  "success": false,
  "reason": "Authentication required"
}
```

- **403 Forbidden** (Invalid or Expired Authentication)

```json
{
  "success": false,
  "reason": "Invalid authentication"
}
```

---

# Authentication (Nostr-based)

Authenticated methods should use an HTTP Nostr Header as defined in [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md) .

```js
const body = JSON.stringify({
  name: "name",
  domain: "domain",
  pubkey: "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd",
});

const event = {
  kind: 27235,
  tags: [
    ["u", "/api/walias"],
    ["method", "POST"],
    ["payload", sha256Hex(body)],
  ],
  content: "",
};

const encodedEvent = btoa(JSON.stringify(event));

const headers = `Authorization: Nostr ${encodedEvent}`;
```

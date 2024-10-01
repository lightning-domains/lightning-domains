# User Endpoints

`user` can have multiple `waliases`.
`user` can have multiple `wallets`.

---

## Get User Data

**GET** `/users/{pubkey}`

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

## Update User Data (Authenticated)

**PUT** `/users/{pubkey}`

#### Description:

Update relayList for the user.

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

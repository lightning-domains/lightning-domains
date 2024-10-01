# API Endpoints

A **walias** is the resulting address of `name@domain`.
There are three models: `walias`, `user` and `wallet`.
`user` can have multiple `waliases`.
`user` can have multiple `wallets`.
`wallet` must have a `walias`.
`wallet` must have a `user`.

---

# Endpoints

[User REST](./USER_ENDPOINTS.md)
[Walias REST](./WALIAS_ENDPOINTS.md)
[Wallet REST](./WALLET_ENDPOINTS.md)

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

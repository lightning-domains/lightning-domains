# Api Endpoints

## Availability

Checks the availability of the name

### POST /walias/availability
```json
{
  "domain": "lacrypta.ar"
  "name": "gorila"
}
```

Should return:

```ts
{
  available: boolean,
  quote?: { // only if available
    price: Number, // in sats
    data: {type: "short"} | {}
  },
  why?: "REGISTERED" // reason why is not available
}
```

## Register Walias

### POST /walias/register
```ts
{
  name: "handle",
  domain: "domain",
  pk: "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd", // hex public key
  ref?: "snort" // Reference
}
```

Should return:

```ts
{
    quote: {
        price: 70000, // sats value
        data: {
            type: "short"
        }
    },
    invoice: "lnbc700u1pn0fewqpp5p6fmprzy23pyslgn7xzzp9srg9j47dzaqrykna2pjnaepjgnv3wsdp4fey4qtfsx5sx7unyv4ezqen0wgsxzmrzgpekummjwsh8xmmrd9skccqzzsxqzjcsp53vk776zwe3d4yee8zf085r9996h8w9e6u5v25209p9eq6a226grq9qyyssqnapdy7jmyjcl7vun7my5pq3y8473uchuh0q02px0d69xaggka9azss8967e6p73snv97tnfh3nhxur65etexy6v93nexkmlsq3nhvmcqu5dfmf",
    referenceId: "e tag in ZapReceipt event to be published",
    verify: "https://url_lnurl21_compatible.com/check" // LUD21 verify url
}
```

Once the payment is done, the updatable event should be published.

# Authenticated endpoints (Nostr based)

Authenticated methods should use a HTTP Nostr Header like [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md)

```js
const body = JSON.stringify({
  "name": "handle",
  "domain": "domain",
  "pk": "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd",
});

const base64Body = btoa(body);

const event = {
  "kind": 27235,
  "tags": [
    ["u", "/api/walias"],
    ["method", "POST"],
    ["payload", base64Body]
  ],
  "content": ""
};
```

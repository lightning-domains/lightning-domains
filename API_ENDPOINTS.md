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
        price: 70000,
        data: {
            type: "short"
        }
    },
    paymentHash: "",
    invoice: "lnbc700u1pn0fewqpp5p6fmprzy23pyslgn7xzzp9srg9j47dzaqrykna2pjnaepjgnv3wsdp4fey4qtfsx5sx7unyv4ezqen0wgsxzmrzgpekummjwsh8xmmrd9skccqzzsxqzjcsp53vk776zwe3d4yee8zf085r9996h8w9e6u5v25209p9eq6a226grq9qyyssqnapdy7jmyjcl7vun7my5pq3y8473uchuh0q02px0d69xaggka9azss8967e6p73snv97tnfh3nhxur65etexy6v93nexkmlsq3nhvmcqu5dfmf",
    token: "234541bc-1548-488f-93e5-a8f4cc74f7f6"
}
```


# Via Nostr

All endpoints can be accessed via nostr adding the prefix to the endpoint `/nostr/`, making a `POST` request and add an event to the body as follows.
The event should be formed like this

```json
{
  "content": JSON.stringify({
    "name": "handle",
    "domain": "domain",
    "pk": "2ad91f1dca2dcd5fc89e7208d1e5059f0bac0870d63fc3bac21c7a9388fa18fd",
  })
}

This should be sent via `POST` to `/nostr/walias/register`

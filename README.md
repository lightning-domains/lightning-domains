# Lightning Domains Standard

This repo hold the Lightning Domain standard.

## Rules
- Implement NIP-05
- Implement LUD-16
- Implement LUD-21
- Implement NIP-57
- NIP-05 and LUD-16 should be owned by the same user
- .well-known file
- User `_` on NIP-05 must have a valid pubkey (ROOT)
- An updatable event should be piblished when handles are assigned or removed for a pubkey
- [Walias endpoints](./API_ENDPOINTS.md)

## Api Endpoints
- Check walias availability and price
- Register/Buy new walias
- Transfer walias
- Remove walias

## Domain .well-known

A json file should be accesable `$DOMAIN/.well-known/domain.json` with the following structure:

- title: The name of the domain
- logo: The url of the logo image
- description (optional): A description of the domain
- apiEndpoint (optional): The url of the api endpoint (Lightning Domain API) (Default: https://lightningdomain.io/api)
- adminPubkey: The hex encoded public key of the admin

```json
{
  "title": "La Crypta",
  "logo": "https://image_url",
  "description": "https://pbs.twimg.com/profile_images/1755606302951411712/5HjGkdHm_400x400.jpg",
  "apiEndpoint": "https://lightningdomain.io/domain",
  "adminPubkey": "hex_pubkey"
}
```

## Updatable Event

Emitted by the Lightning Domain Admin.

```json
{
  "pubkey": "$DOMAIN_ADMIN",
  "kind": 31201,
  "tags": [
    ["d", "$USER_PUBKEY@$DOMAIN"],
    ["p", "$USER_PUBKEY"],
    ["h", "$DOMAIN"],
    ["i", "walias_handle1"], // username (without domain)
    ["i", "walias_handle2"] // Can have multiple handles assigned
  ],
  "content": ""
  ...
}
```

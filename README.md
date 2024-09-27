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
- Create a badge definition and badge award per pubkey
- Endpoints use [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md)
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
  "description": "Biggest Bitcoin community in Argentina",
  "apiEndpoint": "https://lightningdomain.io/domain",
  "adminPubkey": "hex_pubkey"
}
```

## Updatable Event

Emitted by the Lightning Domain Admin. Badge as defined in [NIP-58](https://github.com/nostr-protocol/nips/blob/master/58.md)

### Badge Definition

```json
{
  "pubkey": "$DOMAIN_ROOT", // root handle _ of the domain
  "kind": 30009, // Badge definition
  "tags": [
    ["d", "$DOMAIN:$USER_PUBKEY"], // Unique Identifier
    ["name", "$DOMAIN profile"],
    ["description", "User profile badge for $USER_PUBKEY at $DOMAIN"],
    ["image", "https://nostr.academy/awards/bravery.png", "1024x1024"], // Domain Logo
    ["thumb", "https://nostr.academy/awards/bravery_256x256.png", "256x256"]

    ["p", "$USER_PUBKEY"], // User
    ["h", "$DOMAIN"],
    ["i", "walias_handle1"], // username (without domain)
    ["i", "walias_handle2"] // Can have multiple handles assigned
    ["i", "walias_handle3"]
  ],
  "content": "" // Can be used for user profile data, stats, roles, activity, etc.
  // ...
}
```

### Badge Award

```json
{
  "pubkey": "$DOMAIN_ROOT", // root handle _ of the domain
  "kind": 8,
  "tags": [
    ["a", "30009:$DOMAIN:$USER_PUBKEY"],
    ["p", "$USER_PUBKEY", "wss://relay"],
  ],
  // ...
}

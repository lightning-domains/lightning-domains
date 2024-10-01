# Wallet Endpoints

## Get `wallets` from a specific `walias` (Authenticated)

**GET** `/walias/{name}/wallets`

#### Description:

Gets the wallets associated with a specific walias.

#### Response:

- **200 OK** (Success)
  - **Wallets array** :

```json
[
  {
    "id": "wallet_id",
    "config": {
      "tag": "payRequest",
      "callback": string,
      "maxSendable": number,
      "minSendable": number,
      "metadata": string,
    },
    "priority": 1, // Lower is more likely to be selected
    "provider": "json",
    "pubkey": "pubkey",
    "walias": ["alguno"]
  }
]
```

## Get `wallets` from a specific `user` (Authenticated)

**GET** `/users/{pubkey}/wallets`

#### Description:

Gets the wallets associated with a specific `user`.

#### Response:

- **200 OK** (Success)
  - **Wallets array** :

```json
[
  {
    "id": "wallet_id",
    "config": {
      "tag": "payRequest",
      "callback": string,
      "maxSendable": number,
      "minSendable": number,
      "metadata": string,
    },
    "priority": 1, // Lower is more likely to be selected
    "provider": "json",
    "pubkey": "pubkey",
    "walias": ["alguno"]
  }
]
```

## Get `wallet` by `id` (Authenticated)

**GET** `/wallets/{walletId}`

#### Description:

Gets the wallet by `walletId`.

#### Response:

- **200 OK** (Success)
  - **Wallet data** :

```json
{
  "id": "wallet_id",
  "config": {
    "tag": "payRequest",
    "callback": string,
    "maxSendable": number,
    "minSendable": number,
    "metadata": string,
  },
  "priority": 1, // Lower is more likely to be selected
  "provider": "json",
  "pubkey": "pubkey",
  "walias": ["alguno"]
}
```

## Get `wallet` LNURLP by `id`

**GET** `/wallets/{walletId}/lnurlp`

#### Description:

Gets `LUD06` response `walletId`.

#### Response:

- **200 OK** (Success)
  - **LUD06 response** :

```json
{
  "tag": "payRequest",
  "callback": "https://lightningdomains.io/wallets/{walletId}/lnurlp/callback",
  ...
}
```

## Get `wallet` LNURLP callback by `id`

**GET** `/wallets/{walletId}/lnurlp/callback`

#### Description:

Gets `LUD06`'s `callback` response `walletId`.

#### Response:

- **200 OK** (Success)
  - **LUD06 callback response** :

```json
{
  "pr": "lightning_invoice", // bech32-serialized lightning invoice
  "routes": [], // optional
  "verify": "LUD21 url"
}
```

## Create `wallet` for a specific `walias` (Authenticated)

**POST** `/walias/{name}/wallets`

#### Description:

Create a `wallet` for a specific `walias`. You can choose the `walletId`.

#### Request Body:

```json
{
  "id": "walletId", // Optional
  "config": {
    "tag": "payRequest",
    "callback": string,
    "maxSendable": number,
    "minSendable": number,
    "metadata": string,
  },
  "priority": 1, // Lower is more likely to be selected
  "provider": "json"
}
```

#### Response:

- **201 OK** (Success)
  - **Wallet data** :

```json
[
  {
    "id": "wallet_id",
    "config": {
      ...
    },
    ...
  }
]
```

## UPDATE `wallet` by `walletId` (Authenticated)

**PUT** `/wallets/{walletId}`

#### Description:

Update `wallet` config.

#### Request Body:

```json
{
  "config": {
    "tag": "payRequest",
    "callback": string,
    "maxSendable": number,
    "minSendable": number,
    "metadata": string,
  },
  "priority": 1,
}
```

## Delete `wallet` by `walletId` (Authenticated)

**DELETE** `/wallets/{walletId}`

#### Description:

Permanently delete `wallet` config.

#### Response:

- **200 OK** (Success)

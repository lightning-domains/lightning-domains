# Lightning Domains Standard

The **Lightning Domains Standard** is a collection of standards combining **Nostr**, **Lightning Network**, BIPs, **LNURL**, **BOLT**, and **NIP** definitions to provide a comprehensive framework for identity management and Bitcoin transactions. This standard aims to make sending Bitcoin as easy as sending an email by providing decentralized and privacy-preserving identity management. It is designed to ensure interoperability, scalability, and mass adoption while leveraging the censorship-resistant properties of the Bitcoin blockchain.

## Index

1. [Purpose](#purpose)
2. [Key Objectives](#key-objectives)
3. [Key Concepts](#key-concepts)
   - [Walias: Decentralized, User-Friendly Addresses](#1-walias-decentralized-user-friendly-addresses)
   - [Trust Without Compromising Privacy](#2-trust-without-compromising-privacy)
   - [Key Party Infrastructure (KPI) vs. Web of Trust (WoT)](#3-key-party-infrastructure-kpi-vs-web-of-trust-wot)
4. [Technical Framework](#technical-framework)
   - [Rules](#rules)
   - [REST API Integration](#rest-api-integration)
5. [Domain ](#domain-well-known-configuration)[`.well-known`](#domain-well-known-configuration)[ Configuration](#domain-well-known-configuration)
6. [Updatable Event Structure](#updatable-event-structure)
   - [Badge Definition Example](#badge-definition-example)
   - [Badge Award Example](#badge-award-example)
7. [Future Enhancements and Pending Features](#future-enhancements-and-pending-features)
8. [Fighting Spam with Lightning Domains](#fighting-spam-with-lightning-domains)
9. [Contributing](#contributing)
10. [Additional Resources](#additional-resources)
11. [License](#license)
12. [Contact](#contact)

## Purpose

The Lightning Domains Standard is intended to facilitate a decentralized, censorship-resistant method of sending Bitcoin using simple, email-like addresses called **waliases** (e.g., `agustin@lacrypta`.com). The goal is to create a framework that can be adopted by hosting providers, communities, families, companies, banks, clubs, wallet providers, conferences, and even individuals, making Bitcoin payments intuitive and accessible to all.

### Key Objectives

- **User Simplicity**: Make Bitcoin payments as easy as sending an email.
- **Interoperability**: Ensure seamless interaction between different platforms, wallets, and Lightning Network providers.
- **Censorship Resistance**: Leverage Bitcoin’s inherent censorship-resistant properties.
- **Decentralized Identity**: Allow individuals and organizations to issue and manage identities that work across the Bitcoin ecosystem, streamlining transactions and interactions.

## Key Concepts

### 1. Walias: Decentralized, User-Friendly Addresses

A **walias** is an address that functions similarly to an email address but is used to send and receive Bitcoin. Users can register walias like `user@domain.btc` within a Lightning Domain. These walias are mapped to a **public key (pubkey)**, making it easy for anyone to send Bitcoin to that address without needing to handle long Bitcoin addresses.

- **Multiple Waliases per User**: Users can collect multiple waliases from different Lightning Domains that point to the same pubkey. This allows for increased privacy, as users can use different waliases in different contexts without revealing their true identity.

### 2. Trust Without Compromising Privacy

To combat issues like spam and fraudulent activity without resorting to invasive KYC (Know Your Customer) procedures, Lightning Domains leverage **trust through reputation**:

- **Walias from Multiple Providers**: Users can obtain waliases from multiple trusted providers, enabling them to establish credibility without revealing personal information.
- **Reputation-Based Trust**: The value of a walias depends on the reputation of the provider that issued it. This enables decentralized verification while preserving privacy.
- **Whitelist Mechanism**: Services can whitelist users based on waliases issued by different trusted authorities. Lightning Domain providers are responsible for the behavior of their users, making the reputation of a walias a reflection of the provider's management. Services could require the user to be member of one or many Lightning Domains before giving accessto certain features, including signup.

### 3. Key Party Infrastructure (KPI) vs. Web of Trust (WoT)

**Lightning Domains** balances **Key Party Infrastructure (KPI)** and **Web of Trust (WoT)** principles to offer scalability alongside decentralized control:

- **KPI for Scalability**: Large institutions, like email custodians, can manage and issue waliases, ensuring that the system can scale efficiently.
- **WoT for Decentralization**: For communities and individuals who value privacy and self-sovereignty, a web of trust approach can be adopted, allowing trust to be distributed and maintained collectively without central control.

## Technical Framework

The Lightning Domains Standard integrates several key technologies and protocols to create a secure, decentralized identity and transaction framework. Below is a breakdown of the rules, standards, and technical details.

### Rules

- Implement [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md)
- Implement [NIP-57](https://github.com/nostr-protocol/nips/blob/master/57.md)
- Implement [LUD-16](https://github.com/lnurl/luds/blob/luds/16.md)
- Implement [LUD-18](https://github.com/lnurl/luds/blob/luds/18.md)
- Implement [LUD-21](https://github.com/lnurl/luds/blob/luds/21.md)
- [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md) and [LUD-16](https://github.com/lnurl/luds/blob/luds/16.md) should be owned by the same user
- .well-known file
- User `_` on [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md) must have a valid pubkey (ROOT)
- Admin user must be name `admin`.
- Create a badge definition and badge award per pubkey
- Endpoints use [NIP-98](https://github.com/nostr-protocol/nips/blob/master/98.md)
- Implement [REST Endpoints](./api/README.md)
- **Relays for Badge Publication**: Lightning Domains should have relays associated to publish badges. Badges are the mechanism to signal that a pubkey is a member of a Lightning Domain, providing an easy way for services to query this via subscribing to a Nostr relay.

### REST API Integration

- **REST Endpoints** must be implemented as per the [API Documentation](./api/README.md).
- Use RESTful API design for integration with external services like wallet providers or communities.

## Domain `.well-known` Configuration

A `.well-known` JSON file should be accessible at `$DOMAIN/.well-known/domain.json`, which provides essential metadata about the domain.

**Example:**

```jsonc
{
  "title": "La Crypta",
  "logo": "https://image_url",
  "description": "Biggest Bitcoin community in Argentina",
  "apiEndpoint": "https://lightningdomain.io/domain",
  "rootPubkey": "hex_pubkey",
  "adminPubkey": "hex_pubkey" // Optional
}
```

### Parameters:

- **title**: The name of the domain.
- **logo**: The URL of the domain's logo image.
- **description**: Optional description of the domain.
- **apiEndpoint**: The URL of the Lightning Domain API.
- **rootPubkey**: The public key of the root user.
- **adminPubkey**: The public key of the domain admin (optional).

## Updatable Event Structure

The Lightning Domain `root user` emits events to update the **waliases**. These events, using the [NIP-58](https://github.com/nostr-protocol/nips/blob/master/58.md) specification, should be regenerated whenever a walias is modified.

### Badge Definition Example

```jsonc
{
  "pubkey": "$DOMAIN_ROOT", // Root handle _ of the domain
  "kind": 30009, // Badge definition
  "tags": [
    ["d", "$DOMAIN:$USER_PUBKEY"], // Unique Identifier
    ["name", "$DOMAIN profile"],
    ["description", "User profile badge for $USER_PUBKEY at $DOMAIN"],
    ["image", "https://example.com/logo.png", "1024x1024"], // Domain Logo
    ["thumb", "https://example.com/logo_256.png", "256x256"],
    ["p", "$USER_PUBKEY"], // User
    ["h", "$DOMAIN"],
    ["i", "walias_name1"], // Handle (without domain)
    ["i", "walias_name2"], // Can have multiple wlias
    ["i", "walias_name3"]
  ],
  "content": "" // Can store user profile data, roles, or activity information.
}
```

### Badge Award Example

```jsonc
{
  "pubkey": "$DOMAIN_ROOT", // Root handle _ of the domain
  "kind": 8,
  "tags": [
    ["a", "30009:$DOMAIN:$USER_PUBKEY"],
    ["p", "$USER_PUBKEY", "wss://relay"]
  ]
  // ...
}
```

## Future Enhancements and Pending Features

- **DNS Management**: Define how DNS management will operate for resolving Bitcoin-based domains.
- **Email Integration**: Handle incoming emails, wrapping them in NOSTR events and sending them to the respective `walias` pubkey using [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md).

## Fighting Spam with Lightning Domains

In response to the increasing challenge of distinguishing bots and AI from real users, **Lightning Domains** offers a privacy-preserving solution to fight spam:

- **Decentralized Trust Without KYC**: Unlike centralized platforms that use KYC to verify users, Lightning Domains allow users to collect **multiple waliases** issued by different providers. This builds trust without compromising anonymity.
- **Reputation-Based Whitelisting**: Services can whitelist users based on waliases from reputable Lightning Domain providers. Providers are responsible for managing their users' behavior, and the value of a walias is based on the provider's reputation.
- **Spam Prevention Mechanism**: Providers that issue waliases must manage and monitor user activity. Misbehaving users may have their waliases revoked, preventing them from participating in whitelisted services. This system incentivizes both users and

## License

This documentation is released under the [MIT License](./LICENSE.md) .

---

## Contact

If you encounter any issues or have questions about the API, please open an issue on our [GitHub repository](https://github.com/lightning-domains/lightning-domains) or contact our [La Crypta Discord](https://discord.lacrypta.ar).

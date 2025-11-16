# Generating Deterministic Ethereum Keys with WebAuthn PRF

This example explores how to deterministically and repeatably derive the same Ethereum key accross sessions and devices using the PRF extension to the WebAuthn api. This approach preculdes the need to verify secp256r1 signatures onchain, as the passkey credential produces a standard Ethereum key which can be used with typical web3 libraries like Ethers.js or viem. Hence, the PRF extension essentially brings native Ethereum keys into all major desktop and mobile browsers.

## Note 

This concept is most useful if the passkey is stored a service that can sync the key accross devices like:

- 1Password
- Apple Keychain
- Chrome Keychain
- etc

## Non-Resident vs. Resident Keys

There are two patterns that prevent the user from generating duplicate credentials when authenticating on your site: 

1. server-managed credentials (most common)
2. Discoverable/residential credentials

### Non-Resident Credentials

During the credential creation ceremony, the user must identify themselves first by supplying a username or email. The credential is generated and the the relying party server is responsible for storing the username/credential id (or kid) pair together. When the user returns the site later, they supply their username to the server which sends the associated credential id back to the user agent which can then request attestation. If the server doesn't supply a kid, the user agent cannot attest identity. 

## Resident Credentials

Resident keys store credential metadata *with* the credential in the authorization client. Hence with resident keys, the server does not need to store the kid for a user. 
# Generating Deterministic Ethereum Keys with WebAuthn PRF

This example explores how to deterministically and repeatably derive the same Ethereum key accross sessions and devices using the PRF extension to the WebAuthn api. This approach preculdes the need to verify secp256r1 signatures onchain, as the passkey credential produces a standard Ethereum key which can be used with typical web3 libraries like Ethers.js or viem. Hence, the PRF extension essentially brings native Ethereum keys into all major desktop and mobile browsers.

## Note 

This concept is most useful if the passkey is stored a service that can sync the key accross devices like:

- 1Password
- Apple Keychain
- Chrome Keychain
- etc

Once the user has generated a credential, in order to successfully generate the same ETH key on a new device or profile, the relying party MUST be sure to ask for the same credential id. This simply means that the product developer should stick to the best practices set by the w3c standard, namely storing the credential id server-side and sending it to the client asking to authenticate. 
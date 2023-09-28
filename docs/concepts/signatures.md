# Signing OCP Requests and Responses

## Context
When communicating over HTTP using OCP APIs, nodes need to authenticate themselves to perform transactions with other nodes. Due to the commercial nature of the transactions, request/response pairs should be considered "contractual". Therefore, it is imperative that all requests and responses are signed by the sender and subsequently verified by the receiver. Message reliability between nodes uses public-private key cryptography to ensure that messages are not altered or tampered with during transit.

This document describes a way for network nodes (BSNs/SSNs) and gateway providers (GPs) to add authentication to HTTP messages by using digital signatures and digest headers.

## Node and Gateway Digest Headers

The BSN and SSN are expected to send an `Authorization` header as defined in [RFC 7235](https://datatracker.ietf.org/doc/html/draft-cavage-http-signatures-12) the "auth-scheme" is "Signature" and the "auth-param" parameters meet the requirements listed in Section 2 of [this](https://datatracker.ietf.org/doc/html/draft-cavage-http-signatures-12) document.

The GP is expected to send a `X-Gateway-Authorization` header where the "auth-scheme" is "Signature" and the "auth-param" parameters meet the requirements listed in Section 2 of [this document](https://datatracker.ietf.org/doc/html/draft-cavage-http-signatures-12).

Below is the format of a BSN/SSN Authorization header:

```
Authorization : Signature keyId="{registry_public_key_address}",algorithm="ecdsa",created="1606970629",expires="1607030629",headers="(created) (expires) digest",signature="Base64(ECDSAsecp256k1_sign(signing string))"
```

The BG will send its signature in the `X-Gateway-Authorization` header in the exact same format as shown below.

```
X-Gateway-Authorization:Signature keyId="{registry_public_key_address}", algorithm="ecdsa", created="1606970629", expires="1607030629", headers="(created) (expires) digest", signature="Base64(ECDSAsecp256k1_sign(signing string))"
```

my question is what to include in the algorithm field to both be secure and valid with eth generated key pair in the registry and the RFC 7235 standard.


- ES256K - ECDSA signature algorithm with secp256k1 curve using SHA-256 hash algorithm
- [EIP-2](https://eips.ethereum.org/EIPS/eip-2)
- [Http RFC 7235](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) 
- [ECDSA](https://www.rfc-editor.org/rfc/rfc6979)

- [ECDSA examples](https://www.programcreek.com/python/example/81785/ecdsa.SECP256k1)

- signature construction for [ecdsa-sha256](https://crypto.stackexchange.com/questions/104261/ecdsa-sha256-http-signature-string-construction)

```js
import { keccak256, ecsign, toRpcSig, bufferToHex } from 'ethereumjs-util';

function signECDSAsecp256k1(msg: string, privKey: Buffer) {
  // Hash the message using Keccak-256 (SHA3)
  const msgHash = keccak256(msg);

  // Sign the message hash with the private key
  const { r, s, v } = ecsign(msgHash, privKey);

  // Convert the signature components to a raw signature
  const signature = toRpcSig(v, r, s);

  return {
    message: msg,
    messageHash: bufferToHex(msgHash),
    signature: bufferToHex(signature),
  };
}

// Example usage:sa
const privateKey = Buffer.from('YOUR_PRIVATE_KEY', 'hex'); // Replace with your private key
const message = 'Hello World';
const signature = signECDSAsecp256k1(message, privateKey);
console.log('Message:', message);
//Message: Hello World
console.log('Message Hash:', signature.messageHash);
//Message Hash: 0x[hexadecimal characters]
console.log('Signature:', signature.signature);
//Signature: 0x3045022100c3d2a1548d21d206c81e951b788242d4d77b6f7e9f09ec4fbd1ce5e198b173f0022036f20a17d4a9b31a4328e3d72d89969adef1ef2fb3b4d400d0ff10d2bf805f6a
```




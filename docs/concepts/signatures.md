# Signing OCP Requests and Responses

## Context
When communicating over HTTP using OCP APIs, nodes need to authenticate themselves to perform transactions with other nodes. Due to the commercial nature of the transactions, request/response pairs should be considered "contractual". Therefore, it is imperative that all requests and responses are signed by the sender and subsequently verified by the receiver. Message reliability between nodes uses public-private key cryptography to ensure that messages are not altered or tampered with during transit.

This document describes a way for network nodes (BSNs/SSNs) and gateway providers (GPs) to add authentication to HTTP messages by using digital signature schemes.
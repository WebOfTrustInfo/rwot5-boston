[![](https://img.shields.io/badge/In%20progress--yellow.svg)]()
# DIDs for Blockcerts' Certificate Revocation

## Abstract

Blockcerts are blockchain issued certificates compliant with Open Badges (currently being migrated to Verifiable Claims). This proposal aims at improving Blockcerts' revocation capabilities by using DIDs for identifying and authenticating parties for certificate revocation.

## Overview of Changes
- Blockcerts currently uses the field `issuer.revocationUrl`, containing a URL pointing to an issuer-hosted list of revoked certificates. This process replaces that with a smart contract enabling either issuer or recipient to revoke.
- Blockcerts currently uses publicKeys to enable proof of issuer and recipient signatures. This will be replaced by use of DIDs


## Issuing Process

* The Blockcerts field `issuer.revocationUrl` contains the address of the Ethereum contract enabling authenticated parties to revoke a Blockcert in a batch
    * The specific certificate is identified by the uid embedded in the certificate
    * By default, the parties eligible to revoke the certificate are the issuer or recipient
* The issuer and recipient are identified by DIDs embedded in the certificate

## Revocation Process


>Bob is going to issue a revocation request
1. Bob can retrieve the JSON certificate in several ways (have it sen to him by email, have a local copy, get it from IPFS, etc)
2. In the JSON certificate there is the following information:
    - Ethereum smart contract's address (`issuer.revocationList`)
    - IPFS link to the revocation rules file (not necessary for this example as we'll be using the default method)
    - The DIDs of the Issuer (`issuer.id`) and Receiver (`recipientProfile.id`) 
3. Bob has control of his DID, so he interacts with the Ethereum smart contract and proves ownership of the DID by authenticating himself (the authentication process is defined by the DID method spec)
4. TODO: specifically what the contract does

> Recipient Alice revocation is symmetric

## Verification Process

> Verifier Carol wants to verify a Blockcert presented by bearer Alice
> 
- Perform Blockcerts verification with the following changes:
    - Instead of fetching the revocationList, the verifier code consults the revocation contract
    - TODO...
    - What is authenticity check??? Currently we use the issuer-hosted issuer identification page. DID completely removes the need for that. BUT, should there be a step of inspecting a DID for identification purposes? Is that a level above Blockcerts Verification? Is there a registry/discovery mechanism?


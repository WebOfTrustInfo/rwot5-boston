# Day Two: Demos of Interesting Topics

## Decentralized Vaccination Registry Using IPID

DID atop of IPFS using IPNS, called IPID.

A DPKI that allows direct communication between patient and doctor.

Gives Verifiable Claims for vaccination records on a self-sovereign identity!

Works today! Still needs some selective disclosure!

## DID Client

Command-line application that creates DIDs, rotates keys, etc. It's meant to be ledger-agnostic.

## Credential Handler API

A polyfill for web browsers. Allows user to authorize credentials being sent to repository and later authorize sending them out.

## Uport

Digital identity for the city of Zug to get a residence permit.

Uport is used to scan QR codes for verifiable claims.

_This shows how those credentials supported by the Credential Handler API can actually be used!_

## BTCR TX Conversion Playground

Results of the BTCR hackathon, where BTRC is a DID method for the Bitcoin blockchain. It converts txids to txrefs for use by BTRC DIDs.

Transactions aren't good enough because they're not necessarily confirmed on blockchain, so instead of txid for BTRC DIDs, we use txref, which is confirmed. They're from BIP 136. Error-correcting and censorship-resistance.

An OP_RETURN then points to DID Object. That's what contains most of the information; it can even act as a source-of-authority for other identities!

In BTRC DIDs, you can revoke just by spending the funds referenced by the txref. If you put an OP_RETURN in the new transaction, then it's update! 

<i>Next up: schema! Currently based on schema.org, but might need additional keys.</i>

## DIF Universal Resolver

Pass in an identifier under any DID method, and it'll spit out the results!

The driver and docker container dynamically assembles DDO Objects for you!
Some simpler methods might simply allow direct access to DDO.

_Already have sample code that works on BTRC, Sovrin, and V1!_

Also working on universal registration.

## DID + IOT + BLockchains

Connecting blockchains to IoT devices, using DiDs.

   * User DID Controlled Device DIDs
   * Signed Messages 
   * Inter-Blockchain referencing as BigChainDB base
   * Enforced Create/Write access on BigchainDB assets

Chips allow signing on devices, with on-board key-pairs.

Send a simple request to an API, get a response with a DID on blockchain, user becomes guardian of the Thing.

## Final Thoughts

We'd love to see these demos interoperating by the next Web of Trust.

Maybe a Hackathon before Consensus in late May.

We'd love to increasingly do claims, not just DIDs.

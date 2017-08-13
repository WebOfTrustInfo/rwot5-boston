# BTCR DIDs and DDOs

IN PROGRESS

By Kim Hamilton Duffy, Learning Machine

This assumes you are familiar with DID/DDO terminology at a basic level

## Introduction

BTCR is a DID method that is based on the Bitcoin blockchain. The BTCR DID scheme encodes a confirmed transaction on the Bitcoin blockchain. From the transaction, one can determine:
- The "owner key"
    - I.e. the public key for the owner of the DID
    - This is the public key corresponding to the one that signed the transaction. 
    - Note: we encode the owner key as a public key -- not the expected compressed Bitcoin address format -- for consistency with the LD signature suites
- The "control key"
    - I.e. the owner of a control key can update the DDO
    - This is the transaction output (P2PKH) Bitcoin address
    - Note: This differs from the owner key encoding. This has the property that the control public key is not yet revealed -- just the hash.
- (Optional) A reference to a continuation DDO in the OP_RETURN field. This could be a link to an IPFS address of a DDO with additional keys

(Note: the terminology around owner, control, and keys in general for DIDs is still being discussed. Explained later.)

## BTCR Transaction Structure

Abbreviations:
- Bi = bitcoin address i 
- Pi = public key i
- Si = signing key i (or private key i)

Creating the initial BTCR DID:
- Create key set (`B0`/`P0`/`S0`)
- Create key set (`B1`/`P1`/`S1`)
- Create Bitcoin transaction as follows:
	- Output: Change address `B1`
	- Optional output: `OP_RETURN <link to DDO continuation>`
	- Signing key is `S0`, which reveals public key `P0` in the transaction
- Issue TX0 and wait for confirmation. Get TX Ref encoding of the transaction `TXREF(TX0)`

At this point we have a DID of the format `did:btcr:<TXREF(TX0)>`

The initial BTCR DID is shown in the left side of this diagram.

![BTCR Transaction Structure](btcr-tx-ref.png)

## Definitions and details

### BTCR DID Scheme

The [standard scheme for DIDs](https://w3c-ccg.github.io/did-spec/) is:

`did:<method>:<specific-idstring>`

In this case, the method is "btcr". In the BTCR DID method, `specific-idstring` is a TX Ref of confirmed transactions on a Bitcoin chain.

### TX Refs

TX Refs are described in BIP 136 "Bech32 Encoded Transaction Position References" (https://github.com/bitcoin/bips/pull/555). Among other advantages, they provide a concise way to refer to the confirmed transaction on a specific chain (testnet or mainnet) as a function of the block height and index. 

The important difference is that txid is just a hash of the transaction, which may not yet be confirmed, and does not encode the chain, whereas TX Ref must be confirmed (since it is based on the block height and index).

### Fragments and Deterministic DDOs

BTCR DDOs are divided into fragments. 

The first fragment is referred to as fragment /0 or "Deterministic DDO".  Everything in DDO fragment /0 can be deterministically created from the Bitcoin transaction alone. 

If the Bitcoin transaction has an OP_RETURN output, it is assumed to be a reference to a DDO "continuation", referred to as fragment /1. This is necessary, for example, if the DDO contains multiple keys. We cannot store all this data in the OP_RETURN output field, so we reference the data in an external store.

The concept of fragments is important for BTCR DDOs in the case that DDO continuation is stored in an immutable store such as IPFS. DDO cannot be signed until BTCR DID is available. But that would change the content, which changes the value in the OP_RETURN.

## Looking up a BTCR DID

DID consumers need to be able to construct a DDO from a DID. In BTCR that works as follows:

- Given a DID, we know txid (`did:btcr:<TXREF(TX0)>`)
- Look up transaction. Is the "control key" output spent?
    - no: this is the latest version of the DID. From this we can construct the DDO (described below)
    - yes: keep following transaction chain until the latest with an unspent output is found

## Updating the DID/DDO

Owners of a DID must be able to update it, for example to rotate keys. The BTCR Transaction Structure diagram shows how that is done in the second transaction. 

- Create new tx like above, but send to `B2`
- Set the OP_RETURN to the new continuation DDO
- Sign tx with `S1` (P1 is revealed)

## Example from the BTCR Playground

This section demonstrates BTCR DIDs and DDOs using the default example shown in the [BTCR Playground](https://weboftrustinfo.github.io/btcr-tx-playground.github.io/). 

The playground supports looking up BTCR DDOs for both mainnet and testnet chains. In general, we work with the testnet chain in these examples as we experiment with and develop BTCR.

The playground supports 3 means of entering a transaction:
- TXID and chain (testnet or mainnet)
- TX Ref (note that we don't need to enter the chain; described below)
- TX block height, index, and chain (testnet or mainnet)

To start, click "Convert from TXID" on the site with the default transaction id. This testnet txid resolves to @ChristopherA's testnet BTCR DID -- `did:btcr:xyv2-xzyq-qqm5-tyke/0#transaction-key`.

## Fragment /0, or the Deterministic DDO

Fragment /0 from the default BTCR Playground example is listed here:

### Output

```
{
    "@context": [
        "https://schema.org/",
        "https://w3id.org/security/v1"
    ],
    "ddo": {
        "txid": "f8cdaff3ebd9e862ed5885f8975489090595abe1470397f79780ead1c7528107",
        "funding-txid": "a2cb61283814f8e758f138260da0cccd367c43afead5458e13a7d058f5bc3f6a",
        "funding-txref": "txtest1-xct2-xzcr-qql2-52ku",
        "hash": "f8cdaff3ebd9e862ed5885f8975489090595abe1470397f79780ead1c7528107",
        "more-ddo-hex": "6a4568747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4368726973746f70686572412f73656c662f6d61737465722f64646f2e6a736f6e6c64",
        "more-ddo-asm": "OP_RETURN 68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4368726973746f70686572412f73656c662f6d61737465722f64646f2e6a736f6e6c64",
        "more-ddo-txt": "https://raw.githubusercontent.com/ChristopherA/self/master/ddo.jsonld",
        "owner": [
            {
                "id": "did:btcr:xyv2-xzyq-qqm5-tyke/0#transaction-key",
                "type": [
                    "CryptographicKey",
                    "EdDsaSAPublicKey",
                    "update-proof"
                ],
                "curve": "secp256k1",
                "publicKeyHex": "02b97c30de767f084ce3080168ee293053ba33b235d7116a3263d29f1450936b71"
            }
        ],
        "claim-issuer": [
            {
                "id": "did:btcr:xyv2-xzyq-qqm5-tyke/0#transaction-key",
                "type": [
                    "CryptographicKey",
                    "EdDsaSAPublicKey",
                    "update-proof"
                ],
                "curve": "secp256k1",
                "publicKeyHex": "02b97c30de767f084ce3080168ee293053ba33b235d7116a3263d29f1450936b71"
            }
        ],
        "control": [
            {
                "control-bond": 1.25,
                "rotate-proof": [
                    {
                        "proof-type": "pay-to-pubkey-hash",
                        "hash-base58check": "mvZ3MyLgsvYr87GGSbsPBWEDduLRptfzEU"
                    }
                ],
                "revocation-proof": [
                    {
                        "bond-value": 1.25,
                        "proof-type": "pay-to-pubkey-hash",
                        "hash-base58check": "mvZ3MyLgsvYr87GGSbsPBWEDduLRptfzEU"
                    }
                ]
            }
        ]
    },
    "signature": {
        "type": "SatoshiBlockchainSignature2017",
        "id": "did:btcr:xyv2-xzyq-qqm5-tyke",
        "chain": "testnet3",
        "blockhash": "00000000b3487880b2814da8c0a6b545453d88945dc29a7b700f653cd7e9cdc7",
        "blockindex": 1,
        "blocktime": "2017-07-08T08:20:50Z",
        "confirmations": 15373,
        "time": "2017-07-08T08:03:22.021Z",
        "timereceived": "2017-07-08T08:03:22.021Z",
        "burn-fee": -0.05
    }
}
```

### About
- `hash` and `txid` are listed separately because with segwit, these values may be different
- `more-ddo-<asm|hex|txt>`: These are different encodings of the same thing; if present, the txt variant will contain a link to the DDO continuation, or "fragment /1".
  - In theory, if the data pointed to is immutable (in content-addressable store like IPFS) AND if we can use */1 syntax (see below), then there is an implicit signature by DDO fragment /0
- `owner`: 
  - for BTCR, this is the key used to sign the transaction
- `claim-issuer`: this is also the tx signing key
- `control`: contains hash of key that can perform rotation or revocation. Note: in general it can be key, but in BTCR, only the hash is revealed. 
- `control bond`:funds at time of signing (not a bitcoin notion). Represents funds in that account
- `signature`: term is from LD signatures, but we may not want to use this term for indirect signatures (i.e. by virtue of being part of a signed tx).


## Fragment /1

Note: currently this differs from what's shown in the playground. We are working on updating samples. This version is the correct one.

### Output
```
{
  "@context": [
    "https://schema.org/",
    "https://w3id.org/security/v1"
  ],
  "id": "*/1#ddo.jsonld",
  "type": [
    "Credential",
    "Identity",
    "Person"
  ],
  "issuer": "*/0#did-transaction-key",
  "issued": "2017-07-15",
  "label": "ddo.jsonld",
  "claim": {
    "relationship": "me",
    "alternate-name": "ChristopherA",
    "sameAs": [
      "https://raw.githubusercontent.com/ChristopherA/self/master/357405ED.asc",
      "https://raw.githubusercontent.com/ChristopherA/self/master/FDA6C78E.asc",
      "https://github.com/christophera",
      "https://twitter.com/christophera"
    ],
    "claim-issuer": [
      {
        "id": "*/1#newkeyforlist",
        "type": [
          "CryptographicKey",
          "EdDsaSAPublicKey",
          "update-proof"
        ],
        "curve": "secp256k1",
        "publicKeyHex": "todo"
      },
      {
        "id": "*/1#oldkey",
        "type": [
          "CryptographicKey",
          "EdDsaSAPublicKey",
          "update-proof"
        ],
        "curve": "secp256k1",
        "publicKeyHex": "todo",
        "revoked": "tbd-reason-date"
      }
    ],
    "additional-self-signed-claims": {},
    "claims-issued": {},
    "claims-accepted": {},
    "signature": {
      "type": "EcdsaKoblitzSignature2016",
      "created": "2017-07-16T00:48:44Z",
      "creator": "ecdsa-koblitz-pubkey:02b97c30de767f084ce3080168ee293053ba33b235d7116a3263d29f1450936b71",
      "signatureValue": "HyV/c/DFdAigxSAuqE9O6yRqUk5wpobUaj63ig3hZMZxKJ/l2lNduWFKsN6aR5twAFurD3pJx2ZgVpu/fRb/lLo="
    }
  }
}
```

### About

#### `*` syntax

In the DDO /1 fragment, we need to know the DID in fragment /0 for use in the `id`s. However, the `id`s cannot yet be known (as mentioned above, the DID isn't known until we issue the transaction). We're currently working around this by using the notation `"*/1#<fragment>"`

We considered using IPNS to work around this, but this allows only single-keyed updates.

#### The transaction implicitly signs fragment /1 if the OP_RETURN value is a content addressable hash
If fragment /1 is a content addressable hash, then tx signature is implicitly a signature for fragment /1.

#### Claim-issuer
`claim-issuer` appends unless id is same (main case for id being the same is to revoke with details)

#### Censorship resistance
- with IPFS URI of raw hash value; this is not-censorship resistant 
- First BTCR DID does not need an OP_RETURN. This increases censorship resistance. Subsequently must have OP_RETURN


## Fragment /2

Currently not shown

### Output
```
{
  "@context": [
    "https://schema.org/",
    "https://w3id.org/security/v1"
  ],
  "id": "did:btcr:xyv2-xzyq-qqm5-tyke/2#christophera-knows-kimh",
  "type": [
    "Credential",
    "Identity",
    "Person"
  ],
  "issuer": "did:btcr:xyv2-xzyq-qqm5-tyke/0#did-transaction-key",
  "issued": "2017-07-17",
  "label": "christophera-knows-kimh",
  "claim": {
    "knows": "did:btcr:xgjd-xzvz-qq03-7as7",
    "relationship": "colleague",
    "alternate-name": "KimH"
  },
  "signature": {
    "type": "EcdsaKoblitzSignature2016",
    "created": "2017-07-17T18:41:40Z",
    "creator": "ecdsa-koblitz-pubkey:036abdaaa4db47ba2c0b81ad9bbf7be85d04f0fd50a62c6754499ac299a7647270",
    "signatureValue": "IPYL4YW8/G0m+EFiGBWoyF3rC3xqDntN2pZesAZFLwrVDg7OfB2KPtKPBBwMvcAWfroqKdY0m1Z8lJae0dlHvyQ="
  }
}
```


## Constructed DDOs

Constructed DDO is the current DDO based on state machine events. DDOs have almost nothing to do with VC, but we can shove VCs into a DDO.

Synthesized values are read from a Verifiable Claims arrray

- Two different processors may come up with different end results, because they trust different sources
- Can yield different views:
  - I want to see what Christopher is saying about himself, don't care about anything else
  - I was to see what the US government is saying about Christopher, ...

Result is a "constructed identity"

```
DDO portion | DDO supplement + self-signed VC  | Just VCs    | Constructed Identity
```

```
DIDsm    op_return  URI                     schema pointer
0a         -> 1a                             ->            2a -  3a   | 0a 1a  2a 3a
0b         -> 1b+a                           ->  2a -> 3a   | 0b 1ba 2a 3a
0c         -> 1c                             -> (2a -> 3a)  | 0c 1c
```

Constructed DDO (current DDO based on all state machine events):

```
{
  id: ‘did:xxxxx:yyyyyy’,
  attribute1: value1, // synthesized values
  attribute2: value2,
  attribute3: value3, // signed by a claim that is then signed by signature
  credential: [ … array of verifiable claims …], // data read from blockchain
  signature: … // depends on blockchain
}
```

can be a result of reading claims, e.g.:
```
claim: {
  id: ‘did:xxxxx:yyyyyy’,
  attribute1: value1,
}
signature: { … any issuer that the system building the constructed identity trusts ends up being a synthesized value above … }
```

In this case, the constructed id is what I say about myself. Don’t necessarily need to counter-sign; by listing it we actually signed it.

About claim signatures:
- claims can use different set of keys
- claims do not have to be signed by owner key


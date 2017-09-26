# BTCR DIDs and DDOs

IN PROGRESS

By Kim Hamilton Duffy (Learning Machine), Ryan Grant, and Christopher Allen

This assumes you are familiar with DID terminology at a basic level. 

## Introduction

BTCR is a DID method that is based on the Bitcoin blockchain. The BTCR DID scheme uses a TX Ref-encoded (described below) transaction on the Bitcoin blockchain. The DID Description is constructed from a combination of the transaction details and an optional "continuation" DID Description, the address of which is stored in the OP_RETURN field. This could be a link to an IPFS address of a DID Description with additional entities.

The [BTCR Hackathon readme](https://github.com/WebOfTrustInfo/btcr-hackathon/blob/master/README.md) has more context on BTCR DIDs beyond these basics. Note that at the time of the BTCR Hackathon, we were not yet using the new capabilities-based DID approach, so many details (e.g. control/owner keys) are out of date in the BTCR Hackathon repo.

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

## Looking up a BTCR DID

DID consumers need to be able to construct a DID Description from a DID. In BTCR that works as follows:

- Given a DID, we know transaction reference (`did:btcr:<TXREF(TX0)>`)
- Look up transaction. Is the transaction output spent?
    - no: this is the latest version of the DID. From this we can construct the DID Description (described below)
    - yes: keep following transaction chain until the latest with an unspent output is found

## Updating a DID Descripton

An entity updates the BTCR DID Description by spending the current transaction output. The BTCR Transaction Structure diagram shows how that is done in this second transaction. 

- Create new tx like above, but send to `B2`
- Set the OP_RETURN to the new DID Description
- Sign tx with `S1` (P1 is revealed)

## Example from the BTCR Playground

This section demonstrates BTCR DIDs and DID Descriptions using the default example shown in the [BTCR Playground](https://weboftrustinfo.github.io/btcr-tx-playground.github.io/). 

The playground supports looking up BTCR DID Description for both mainnet and testnet chains. In general, we work with the testnet chain in these examples as we experiment with and develop BTCR.

The playground supports 3 means of entering a transaction:
- TX Ref (note that we don't need to enter the chain; described below)
- TXID and chain (testnet or mainnet)
- TX block height, index, and chain (testnet or mainnet)

To start, click "Convert from TX Ref" on the site with the default TX Ref.

## DID Description

The DID Description resulting from DID `txtest1-xkyt-fzgq-qq87-xnhn` is listed below. 

### Output

```
{
    "@context": [
        "https://schema.org/",
        "https://w3id.org/security/v1"
    ],
    "authorization": [
        {
            "capability": "UpdateDidDescription",
            "permittedProofType": [
                {
                    "proofType": "SatoshiBlockchainSignature2017",
                    "authenticationCredential": [
                        {
                            "type": [
                                "EdDsaSAPublicKey",
                                "CryptographicKey"
                            ],
                            "hash-base58check": "mvq9zXGAr76uSoRG5ybEdECuXoPGY42ihh"
                        }
                    ]
                }
            ]
        },
        {
            "capability": "IssueCredential",
            "permittedProofType": [
                [
                    {
                        "type": [
                            "EdDsaSAPublicKey",
                            "CryptographicKey"
                        ],
                        "publicKeyHex": "0280e0b456b9e97eecb8028215664c5b99ffa79628b60798edd9d562c6db1e4f85",
                        "owner": "did:btcr:xkyt-fzgq-qq87-xnhn",
                        "id": "did:btcr:xkyt-fzgq-qq87-xnhn/keys/fundingKey"
                    }
                ]
            ],
            "entity": "did:btcr:xkyt-fzgq-qq87-xnhn"
        },
        {
            "capability": "IssueCredential",
            "entity": "did:btcr:xkyt-fzgq-qq87-xnhn",
            "permittedProofType": [
                [
                    {
                        "id": "did:example:12345678/keys/1",
                        "type": "RsaCryptographicKey",
                        "owner": "did:example:12345678",
                        "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
                    }
                ]
            ]
        }
    ],
    "authenticationCredential": [
        {
            "type": [
                "EdDsaSAPublicKey",
                "CryptographicKey"
            ],
            "curve": "secp256k1",
            "publicKeyHex": "0280e0b456b9e97eecb8028215664c5b99ffa79628b60798edd9d562c6db1e4f85",
            "owner": "did:btcr:xkyt-fzgq-qq87-xnhn",
            "id": "did:btcr:xkyt-fzgq-qq87-xnhn/keys/fundingKey"
        },
        {
            "id": "did:example:12345678/keys/1",
            "type": "RsaCryptographicKey",
            "owner": "did:example:12345678",
            "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
        }
    ],
    "signature": {
        "type": "SatoshiBlockchainSignature2017",
        "id": "did:btcr:xkyt-fzgq-qq87-xnhn",
        "chain": "testnet"
    }
}
```

### Constructing a BTCR DID Description

The DID Description for DID `txtest1-xkyt-fzgq-qq87-xnhn` was determined as follows.

From the TX Ref, we look up details about the Bitcoin transaction. To see how to do this, refer to the transaction details for the TXID this resolves to, [67c0ee676221d9e0e08b98a55a8bf8add9cba854f13dda393e38ffa1b982b833](https://api.blockcypher.com/v1/btc/test3/txs/67c0ee676221d9e0e08b98a55a8bf8add9cba854f13dda393e38ffa1b982b833?limit=50&includeHex=true).

This transaction has an OP_RETURN data output. For Blockcypher this is in the data_string field: https://raw.githubusercontent.com/kimdhamilton/did/master/ddo.jsonld](https://raw.githubusercontent.com/kimdhamilton/did/master/ddo.jsonld]). That means this DID Description will include additional authorizations and authenticationCredentials listed in the target of that URL.

#### Parse the partial DID Description

Important: the steps below assume that the partial DID Description is stored in an immutable store as opposed to github. If this were stored in github, the partial DID Description should be signed.

This partial DID Description grants the following abilities:
1. Two entities may issue credentials. 
    - One is an entity (currently) without an id, but described by its authentication method (`SatoshiBlockchainSignature2017`) and its hex-encoded public key. Note this is the same as the key used to sign the transaction.
    - One is an entity defined in a separate DID Description, with a `proofType` of `RsaSignature2017`
2. Two entities may authenticate (as a TBD DID). These entities are similar to above.

```

{
  "@context": "https://w3id.org/btcr/v1",
  "authorization": [
    {
        // gives the entity with TBD DID the ability to issue credentials where the "issuer" field is TBD DID. TODO: This could be a default ability.
      "capability": "IssueCredential",
      "permittedProofType": [
        {
	  // Would we need a different type for off-chain signatures?
          "proofType": "SatoshiBlockchainSignature2017",
          "authenticationCredential": [
            {
              "type": [
                "EdDsaSAPublicKey",
                "CryptographicKey"
              ],
              "publicKeyHex": "0280e0b456b9e97eecb8028215664c5b99ffa79628b60798edd9d562c6db1e4f85"
            }
          ]
        }
      ]
    },
    {
      // enables an entity to issue credentials where the "issuer" field is TBD DID as long as this specific RSA key is used
      "capability": "IssueCredential",
      "entity": "did:example:12345678",
      "permittedProofType": [
        {
          "proofType": "RsaSignature2017",
          "authenticationCredential": [
            {
              "id": "did:example:12345678/keys/1",
              "type": "RsaCryptographicKey",
              "owner": "did:example:12345678",
              "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
            }
          ]
        }
      ]
    }
  ],
  "authenticationCredential": [
    {
      "type": [
        "EdDsaSAPublicKey",
        "CryptographicKey"
      ],
      "curve": "secp256k1",
      "publicKeyHex": "0280e0b456b9e97eecb8028215664c5b99ffa79628b60798edd9d562c6db1e4f85"
    },
    {
      "id": "did:example:12345678/keys/1",
      "type": "RsaCryptographicKey",
      "owner": "did:example:12345678",
      "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
    }
  ]
}
```

#### About missing ids, entities, and owners

Again we're assuming the partial DID Description is stored in an immutable store. Because the content is immutable, the transaction signature signs the content hash as well. If not using content-addressable store, then another LD signature scheme would be used. 

Because changing the content changes the address, and because the DID depends on the Bitcoin transaction reference, we have a bootstrapping problem where we cannot yet use the DID in the DID Description fragment shown above. We avoid this problem by omitting `id`, `entity`, and `owner` where the DID is not yet known.

It's valid for a Linked Data object to omit an id; this is called a "blank node" and is the way you indicate you don't know the identifier yet, but you know its attributes. 

#### Merging the partial DID Description and transaction details

With the partial DID Description and transaction details, we can form the complete DID Description.

- If an `authorization` is missing an `entity` in the partial DID Description, update it with the now known DID (did:btcr:xkyt-fzgq-qq87-xnhn)
- If an `authenticationCredential` is missing an `owner`, update it with the now known DID (same as above)
- If an `authenticationCredential` is missing an `id` there are 2 cases:
    - If the credential's hex-encoded public key and proof type match that of the transaction signing key, populate the `id` with `did:btcr:xkyt-fzgq-qq87-xnhn/keys/fundingKey`. Note the `/keys/fundingKey` path is a convention
    - Otherwise, populate the `id` with `did:btcr:xkyt-fzgq-qq87-xnhn/keys/i`, where `i` is the position of the authenticationCredential in the flattened partial DID Description. As of now, this is a very tentative convention.
- Populate an authorization with the ability to update the DID Description from the transaction output
    - A BTCR DID is updated by spending the transaction output. We can inspect the transaction to determine the output Bitcoin address
    - At this point, we only reveal the hashed, base58 encoded version of the output key (i.e. the Bitcoin address)
    - Note that we do not yet know the `entity` value; that will not exist until the DID Description is updated
    - We could create an `id` convention for this, e.g `did:btcr:xyv2-xzyq-qqm5-tyke/keys/output_address`
    

## Comments
- The method described above gives no _default_ capabilities to an entity authenticating with the transaction signing key
    - Capabilities are only granted if merged with a partial DID Description as described above
    - We could consider granting default capabilities, but this does against the best practice of avoiding key reuse
    - This means the BTCR DID is mostly useless without a partial DID Description, so we should consider this carefully
- Omitting `id` as opposed to the previous `*` microsyntax introduces the problem above in which we don't know the path suffix to assign to keys. We can solve this in at least 2 ways:
    - Add a field to the BTCR DID method spec to address this. I.e. `path` and the assumption is that it will get merged with the DID to form the `id` value.
    - Use an algorithmic approach like above, but I think that's a very bad idea
- The number of confirmations of a transaction underlying a BTCR DID should be considered (and automated in the tool constructing the DID Description)
- Censorship resistance
    - With IPFS URI of raw hash value; this is not-censorship resistant 
    - First BTCR DID does not need an OP_RETURN. This increases censorship resistance. Subsequently must have OP_RETURN


# Veres One DID Method Specification
***by Manu Sporny, Dave Longley, and Matt Collier, Digital Bazaar***

## Introduction

The Veres One Ledger is a permissionless public ledger designed specifically 
for the creation and management of decentralized identifiers (DIDs). Veres 
One DIDs are self-sovereign identifiers that may be used by people, 
organizations, and digital devices to establish an identifier that is 
under their control. 

Veres One DIDs are useful in ecosystems where one needs to issue, store, and 
use Verifiable Claims. 

The Veres One DID Method specification has been implemented and a
testnet is available here:

[Veres One Testnet](https://testnet.veres.one/)

There is a video demo of a DID being registered and retrieved from the
Veres One Testnet here:

[Veres One Testnet DID Registration Demo](https://www.youtube.com/watch?v=tQzQKZKF93w)

The current draft of the Veres One DID Method specification is available here:

[Veres One DID Method Specification](https://w3c-ccg.github.io/didm-veres-one/)

## An Example Veres One DID Document

What follows is a complete DID Document registration event that is sent to the ledger
including line by line documentation regarding the DID Document registration
event.

    {
      // The Web Ledger context is a part of the Web Ledger specification
      // and provides the core framing for the DID Registration event.
      "@context": "https://w3id.org/webledger/v1",
      "type": "WebLedgerEvent",
      // The type of ledger operation being performed is a "Create"
      // which creates objects (the DID Document) in the state machine
      "operation": "Create",
      // input can be an array of DID Documents in case batch processing
      // is desired
      "input": [{
        // The Veres One context includes the https://w3id.org/did/v1
        // context and adds Veres One specific vocabulary terms
        "@context": "https://w3id.org/veres-one/v1",
        "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
        "authorizationCapability": [{
          // This authorization capability notes that the DID is capable
          // of updating the entire DID Document
          "permission": "UpdateDidDocument",
          // This is a truly self-sovereign DID in that only the entity
          // associated with the DID update the DID Document
          "entity": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
          // The permitted proof types states that a capability to
          // update the DID Document will be granted if the submitting
          // entity provides both an Equihash proof of work (that is 
          // tuned to the Veres One ledger) and a signature on the 
          // event. The proof of work provides some protection against 
          // a DDoS of the ledger while the signature ensures that 
          // the proper entity is requesting the change.
          "permittedProofType": [{
            "proofType": "LinkedDataSignature2015"
          }, {
            "proofType": "EquihashProof2017",
            "equihashParameterAlgorithm": "VeresOne2017"
          }]
        }],
        // There is only one RSA signature-based authentication credential 
        // that is registered at the time of DID creation
        "authenticationCredential": [{
          "id": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/1",
          "type": "CryptographicKey",
          "owner": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84",
          "publicKeyPem": "-----BEGIN PUBLIC KEY-----\r\n
            MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAmbDqPu6IKHiiIQ4d0AQ6\r\n
            PBduDhUUVqyQirvxqsdcNdKgZ2L8whBml/nTyuB4cd+hHrsfMDiHiT5kX2pbZ7Yy\r\n
            2ctWkGw8e0J94CbwVh2H15gBQBUCjLiGvVIHO2pni693qmre+3Ya2NJ8gGwPLJ7h\r\n
            TLca2b2dX0y16qu0MT0osUGGEoPsdg6ibD2pxnADS3GNPObHT12GrAuxjYFMHecF\r\n
            A4hLZ8U+MIcVmHZuokqqbcyJyjOV+kmhFNeTKFP5P5U8HA3Y42/rE1UJp/wyy7Lc\r\n
            ZAvq0t75ddXKyvYh5dkzxxeeELNKNWVxJ2yvgAr0SatLEPzxJoeYdCyU5N5E22Fj\r\n
            jQIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
        }]
      }],
      // The ledger event itself is secured using an Equihash proof and is
      // also digitally signed with the RSA private key listed above. This
      // multi-signature is what is used to grant the capability to create the
      // DID Document.
      "signature": [{
        "type": "EquihashProof2017",
        "equihashParameterN": 64,
        "equihashParameterK": 3,
        "nonce": "AQAAAA==",
        "proofValue": "AAAaPwABxrIAAFOKAAGo4QAAVW0AAN7cAACXcgABjEI="
      }, {
        "type": "LinkedDataSignature2015",
        "created": "2017-09-30T02:54:31Z",
        "creator": "did:v1:770f2d84-5e62-4caa-af95-111a3205bc84/keys/1",
        "signatureValue": "SNMbsPqLnB+hJFhXzS6hcpZnm9cGvSZZg7o26UYnyGYTvKder/S+Xk
          hNhXisS5385Ljlf5CXTQT5j6qYZtP8ut1Benaae8TMH17txP0CfzHbUMJFnHA1+Nru+e/Pw
          yPwuQ+VZYlXOB7g/tKVVZsxAYTKCAOJvJMIE+nlHjpB+RsKs9z4ZzVtddntqqAcvbZxV/o7
          azBFDizeJu/gHVVMncCJ00SRoOzCOZUABRJV/k68bNSAfpELkrdWx8/xvMIF8r+LWhwdKCS
          iOw4DjSwIK40yD5rOvQn/GlC+unyB8zFe60jCToz/UOJNZBiIYwo+Pwwx28Wqd4Jkb3IeDr
          /L2Q=="
      }]
    }

## Collaboration

We would like to collaborate with the other DID Method implementers at 
Rebooting the Web of Trust to align both the core DID specification as well
as other DID Method specifications. We are also seeking to partner with
organizations that would be interested in integrating Veres One DIDs into their
platform to field test the capabilities of the specifications and technologies.
We are also interested in developing common technologies that can not only
access and update the Veres One DID ledger, but other ledgers as well.

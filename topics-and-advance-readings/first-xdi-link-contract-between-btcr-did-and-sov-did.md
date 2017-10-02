First XDI Link Contract between "btcr" DID and "sov" DID
========================================================
Markus Sabadello, Danube Tech (https://danubetech.com), Vienna, September 19th 2017

We describe an XDI link contract established between two XDI peers, one of which is identified by a `btcr` DID, and one by a `sov` DID. We believe this is the first working example of cross-DID-method data sharing and messaging.

Note: Due to the fact that most of the technologies described in this paper are work-in-progress, the specific formats and data structures are provisional and expected to change.

DIDs
----

DIDs (Decentralized Identifiers, see **[1]**) are persistent, resolvable, and cryptographically verifiable URIs. They represent one of the major breakthroughs of the RWoT community as the foundational component of "self-sovereign" identity networks. DIDs are in some ways similar to earlier types of identifier that XDI has historically used ("I-Numbers", "Cloud Numbers").

DIDs support different "methods", i.e. ways how they can be registered, resolved, updated, and revoked on a specific distributed ledger or network. This means that although all DIDs are interoperable and provide common functionality, they differ in their underlying properties which can make them more or less suitable for certain use cases. For example, if a use case requires the creation of many cheap DIDs for pairwise relationships, the `sov` DID method (registered in Sovrin) is ideal. On the other hand, if a DID backed by the strongest existing network is desired, the `btcr` DID method (registered in Bitcoin) makes sense.

Universal Resolver
------------------

Work is currently underway at the Decentralized Identity Foundation (DIF, see **[2]**) to design and implement a "Universal Resolver", which provides a client, a web service, and multiple drivers to be able to resolve DIDs (and other identifiers such as human-meaningful names) in a uniform way. Currently, a Java implementation (see **[3]**) of the Universal Resolver exists, which contains experimental drivers for the `btcr` DID method and the `sov` DID method.

 * The driver for the `btcr` method builds on `txref-conversion-java` (see **[4]**), which was developed after the RWoT BTCR Virtual Hackathon in July 2017 	(see **[5]**).
 * The driver for the `sov` method builds on `indy-sdk` (see **[6]**) and its Java wrapper.

In order to build XDI link contracts, data sharing, and messaging on top of DIDs, we use the Universal Resolver for discovering a DID's XDI service endpoint, as well as associated cryptographic keys.

The "btcr" DID
--------------

We registered the DID `did:btcr:xkrn-xzcr-qqlv-j6sl` in the **Bitcoin testnet3**. The Universal Resolver produces the following DDO:

	curl -i -X GET  https://uniresolver.danubetech.com/1.0/identifiers/did:btcr:xkrn-xzcr-qqlv-j6sl
	
	HTTP/1.1 200 
	Server: nginx/1.10.3
	Date: Tue, 19 Sep 2017 08:16:18 GMT
	Content-Type: application/ld+json;charset=UTF-8
	Transfer-Encoding: chunked
	Connection: keep-alive
	
	{
	  "id" : "did:btcr:xkrn-xzcr-qqlv-j6sl",
	  "control" : [ ],
	  "service" : {
	    "agent" : "https://azure.microsoft.com/dif/hub/did:btcr:xkrn-xzcr-qqlv-j6sl",
	    "xdi" : "https://xdi03-at.danubeclouds.com/cl/=!:did:btcr:xkrn-xzcr-qqlv-j6sl"
	  },
	  "owner" : {
	    "id" : "did:btcr:xkrn-xzcr-qqlv-j6sl",
	    "type" : [ "CryptographicKey", "EdDsaSAPublicKey" ],
	    "curve" : "secp256k1",
	    "publicKeyHex" : "024a63c4362772b0fafc51ac02470dae3f8da8a05d90bae9e1ef3f5243180120dd"
	  },
	  "@context" : "https://example.org/did/v1"
	}

The XDI service endpoint for this DID is `https://xdi03-at.danubeclouds.com/cl/=!:did:btcr:xkrn-xzcr-qqlv-j6sl`.

Note: The **BTCR TX Conversion Playground** (see **[7]**) can also be used to retrieve/produce the DDO associated with a `btcr` DID.

The "sov" DID
-------------

We registered the DID `did:sov:WRfXPg8dantKVubE3HX8pw` in the **Sovrin Provisional Network**. The Universal Resolver produces the following DDO:

	curl -i -X GET  https://uniresolver.danubetech.com/1.0/identifiers/did:sov:WRfXPg8dantKVubE3HX8pw
	
	HTTP/1.1 200 
	Server: nginx/1.10.3
	Date: Tue, 19 Sep 2017 08:21:03 GMT
	Content-Type: application/ld+json;charset=UTF-8
	Transfer-Encoding: chunked
	Connection: keep-alive
	
	{
	  "id" : "did:sov:WRfXPg8dantKVubE3HX8pw",
	  "control" : [ ],
	  "service" : {
	    "xdi" : "https://xdi03-at.danubeclouds.com/cl/=!:did:sov:WRfXPg8dantKVubE3HX8pw"
	  },
	  "owner" : {
	    "id" : "did:sov:WRfXPg8dantKVubE3HX8pw",
	    "type" : [ "CryptographicKey", "EdDsaSAPublicKey" ],
	    "curve" : "ed25519",
	    "publicKeyBase64" : "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
	  },
	  "@context" : "https://example.org/did/v1"
	}

The XDI service endpoint for this DID is `https://xdi03-at.danubeclouds.com/cl/=!:did:sov:WRfXPg8dantKVubE3HX8pw`.

Note: The **sovrin-client** (see **[8]**) can also be used to retrieve data associated with a `sov` DID:

	sovrin@live> send GET_NYM dest=WRfXPg8dantKVubE3HX8pw
	Getting nym WRfXPg8dantKVubE3HX8pw
	Current verkey for NYM WRfXPg8dantKVubE3HX8pw is ~P7F3BNs5VmQ6eVpwkNKJ5D
	
	sovrin@live> send GET_ATTR dest=WRfXPg8dantKVubE3HX8pw raw=endpoint
	Getting attr WRfXPg8dantKVubE3HX8pw
	Found attribute {"endpoint": {"xdi": "https://xdi03-at.danubeclouds.com/cl/=!:did:sov:WRfXPg8dantKVubE3HX8pw"}}

The XDI Link Contract
---------------------

An XDI link contract is a data sharing agreement that is human- and machine-understandable and enforceable (see **[9]**). It is itself expressed in XDI and part of an XDI graph associated with an XDI peer. The link contract contains information who is authorized to perform certain operations if a certain policy is met.

The XDI graph associated with the `btcr` DID contains the following XDI link contract:

	(=!:did:btcr:xkrn-xzcr-qqlv-j6sl/=!:did:sov:WRfXPg8dantKVubE3HX8pw)$contract$do/$get/=!:did:btcr:xkrn-xzcr-qqlv-j6sl<#email>
	(=!:did:btcr:xkrn-xzcr-qqlv-j6sl/=!:did:sov:WRfXPg8dantKVubE3HX8pw)($contract$if$and/$true){$from}/$is/=!:did:sov:WRfXPg8dantKVubE3HX8pw
	(=!:did:btcr:xkrn-xzcr-qqlv-j6sl/=!:did:sov:WRfXPg8dantKVubE3HX8pw)($contract$if$and/$true){$msg}<$sig><$valid>/&/true

Here the `btcr` DID is called the "authorizing peer", and the `sov` DID is called the "requesting peer". The link contract authorizes the `sov` DID to request the e-mail address in the XDI graph of the `btcr` DID (note the **$get** operation).

The XDI graph associated with the `sov` DID contains the following XDI link contract:

	(=!:did:sov:WRfXPg8dantKVubE3HX8pw/=!:did:btcr:xkrn-xzcr-qqlv-j6sl)$contract$do/$connect/
	(=!:did:sov:WRfXPg8dantKVubE3HX8pw/=!:did:btcr:xkrn-xzcr-qqlv-j6sl)($contract$defer$if$and/$true){$from}/$is/=!:did:btcr:xkrn-xzcr-qqlv-j6sl
	(=!:did:sov:WRfXPg8dantKVubE3HX8pw/=!:did:btcr:xkrn-xzcr-qqlv-j6sl)($contract$defer$if$and/$true){$msg}<$sig><$valid>/&/true

Here the `sov` DID is called the "authorizing peer", and the `btcr` DID is called the "requesting peer". The link contract authorizes the `btcr` DID to request additional link contracts from the `sov` DID (note the **$connect** operation).

Note: Even though two link contracts are shown in this example, they are in fact independent, i.e. it is perfectly valid just to have one or the other.

The XDI Request and Response
----------------------------

Based on the first link contract shown above, the `sov` DID can send a signed XDI message to request the e-mail address in the XDI graph of the `btcr` DID:

	=!:did:sov:WRfXPg8dantKVubE3HX8pw[$msg]@~0/$from/(=!:did:sov:WRfXPg8dantKVubE3HX8pw)
	=!:did:sov:WRfXPg8dantKVubE3HX8pw[$msg]@~0/$to/(=!:did:btcr:xkrn-xzcr-qqlv-j6sl)
	=!:did:sov:WRfXPg8dantKVubE3HX8pw[$msg]@~0/$contract/(=!:did:btcr:xkrn-xzcr-qqlv-j6sl/=!:did:sov:WRfXPg8dantKVubE3HX8pw)$contract
	=!:did:sov:WRfXPg8dantKVubE3HX8pw[$msg]@~0$do/$get/=!:did:btcr:xkrn-xzcr-qqlv-j6sl<#email>
	=!:did:sov:WRfXPg8dantKVubE3HX8pw[$msg]@~0<$sig>/&/"f7c99hAN3hI1E7ttf9+ulwG+x0AmXT4J6C8DV/vs3UPkVk99cvDkXqSe0+dMXG005D6R1GiGuZBEFHNrffDkAg=="

Note how the XDI message references the link contract address `(=!:did:btcr:xkrn-xzcr-qqlv-j6sl/=!:did:sov:WRfXPg8dantKVubE3HX8pw)$contract`.

The `btcr` DID's XDI peer will validate the signature on the XDI message by obtaining the DID/DDO keys of the `sov` DID's XDI peer via the Universal Resolver. It will then execute the XDI message and respond:

	=!:did:btcr:xkrn-xzcr-qqlv-j6sl<#email>/&/"markus@danubetech.com"

Architectural Options
---------------------

Where are the keys that control a DID/DDO? Stored in a web browser (extension)? In a local wallet on a mobile device? In a cloud service? Many terms are currently being considered to describe various architectural components, e.g. "personal data store", "personal cloud", "hub", "cloud agent", "edge agent", "cloud wallet", "edge wallet", etc.

One possible architecture involves identity owners holding the DID/DDO keys on local mobile devices, and communicating with cloud-based "agent" services they control:

	           SOVRIN                                           BITCOIN
	   ______  ______  ______                            ______  ______  ______
	  |    __||__  __||__    |                          |    __||__  __||__    |
	  |___|__||__||__||__|___|                          |___|__||__||__||__|___|
	      |______||______|      <___                        |______||______|
	                                \___
	             |                      \___      DDO              |
	XDI SERVICE  |                          \___  LOOKUP           |  XDI SERVICE
	             V                              \___               V
	   ________________________                     \   ________________________ 
	  |                        |     LINK CONTRACT     |                        |
	  | "sov" XDI cloud agent  |  < < < < < < < < < <  | "btcr" XDI cloud agent |
	  | =!:did:sov:WRfXPg8d... |                       | =!:did:btcr:xkrn-xz... |
	  |________________________|                 ___>  |________________________|
	                                         ___/
	              |                      ___/                      |
	     CONTROL  |                  ___/                          |  CONTROL
	              |              ___/     SIGNED                   |
                 ___         ___/         XDI MSG                 ___
           ~o/  /   \    ___/                               _o   /   \
           /|   | O |                                        |\  | o |
           / \  \___/  edge device                          / >  \___/ edge device

Another possible architecture involves the cloud-based "agent" services to hold the DID/DDO keys, to act on behalf of identity owners:

	           SOVRIN                                           BITCOIN
	   ______  ______  ______                            ______  ______  ______
	  |    __||__  __||__    |                          |    __||__  __||__    |
	  |___|__||__||__||__|___|                          |___|__||__||__||__|___|
	      |______||______|      <___                        |______||______|
	                                \___
	             |                      \___      DDO              |
	XDI SERVICE  |                          \___  LOOKUP           |  XDI SERVICE
	             V                              \___               V
	   ________________________                     \   ________________________ 
	  |                        |     LINK CONTRACT     |                        |
	  | "sov" XDI cloud agent  |  < < < < < < < < < <  | "btcr" XDI cloud agent |
	  | =!:did:sov:WRfXPg8d... |                       | =!:did:btcr:xkrn-xz... |
	  |________________________|  ------------------>  |________________________|
	                                    SIGNED
	              |                     XDI MSG                    |
	     CONTROL  |                                                |  CONTROL
	              |                                                |
                 ___                                              ___
           ~o/  /   \                                       _o   /   \
           /|   | O |                                        |\  | o |
           / \  \___/  edge device                          / >  \___/ edge device

These are just two simplified options. Many more architectural compositions will be available in a decentralized identity system.

Additional Notes
----------------

XDI examples in this document use the "XDI DISPLAY" format. Conversion to other formats such as "JXD" is possible (see **[10]**). 

Certain language in this paper is imprecise. For example, instead of saying "*a DID* can send a message", it would be more accurate to say "*the entity that the DID identifies* can send a message" (for a discussion, see **[11]**).

There is ongoing discussion on how the cryptographic keys used to control the DDO relate to "off-chain" or "peer-to-peer" functionality, such as verifiable claims or XDI messaging. In this paper, the "owner" key described by a DDO is used for signing and validating peer-to-peer XDI messages, i.e. the keys to control the DDO are the same as the keys used for XDI messaging. More diverse scenarios are possible, e.g. a DDO can publish multiple keys associated with a DID. This means that for example, even though `btcr` DIDs use an "EdDsaSAPublicKey" on the "secp256k1" curve, and `sov` DIDs use an "EdDsaSAPublicKey" key on the "ed25519" curve, they could both publish RSA keys in their DDOs for use by verifiable claims or XDI messaging.

Digital signatures are only one kind of proof that can be used for authentication and authorization decisions (for a discussion, see **[12]**). In an XDI link contract's policy, more complex proofs than just plain digital signatures can be supported.

In this paper we demonstrate an XDI link contract between XDI peers that use different key types. This allows for diversity of both DID methods and key types. In some scenarios however it may be preferential to use the same key types for all participants, e.g. when protocols such as DID-TLS (see **[13]**) or CurveCP are used for peer-to-peer communication.

Related Work
------------

Previous XDI-related contributions to RWoT include: 

 * XDI, Blockstore, and BIP32: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/cool-hack-xdi-blockstore-bip32.md
 * XDI Link Contracts: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/xdi-link-contracts.md
 * XDI Graphs in IPFS: https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/topics-and-advance-readings/XDI-Graphs-in-IPFS.md
 * JXD Examples: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/topics-and-advance-readings/JXD-Examples.md
 * XDI Verifiable Claims and Link Contracts: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/xdi-verifiable-claims-link-contracts.md

Thank you to the wonderful RWoT community for its great and idealistic work! 

References
----------

 **[1]** https://docs.google.com/document/d/1Z-9jX4PEWtyRFD5fEyyzEnWK_0ir0no1JJLuRu8O9Gs/

 **[2]** http://identity.foundation/

 **[3]** https://github.com/decentralized-identity/universal-resolver/tree/master/implementations/java

 **[4]** https://github.com/WebOfTrustInfo/txref-conversion-java

 **[5]** https://github.com/WebOfTrustInfo/btcr-hackathon

 **[6]** https://github.com/hyperledger/indy-sdk

 **[7]** https://weboftrustinfo.github.io/btcr-tx-playground.github.io/

 **[8]** https://github.com/evernym/sovrin-client

 **[9]** https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/xdi-link-contracts.md

 **[10]** https://server.xdi2.org/XDIConverter

 **[11]** https://github.com/w3c-ccg/did-spec/pull/22

 **[12]** https://github.com/w3c-ccg/did-spec/issues/15

 **[13]** https://docs.google.com/document/d/1-aPY1eeHdR_TnF7_WpEs58RZ_jNdDeptVrNEu3groFc/

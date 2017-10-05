# DID Client - Verifiable Claims Issuer
***by Manu Sporny, Digital Bazaar***

The DID Client is a command-line
utility for creating, retrieving, and updating DID Documents across
multiple ledgers. A demonstration video of the tool, as well as an
explanation of how it works, can be viewed here:

[did-client Demo Video](https://www.youtube.com/watch?v=tQzQKZKF93w)

During the Rebooting the Web of Trust 5 event, we extended the DID client
with issuing capabilities that enable it to issue Verifiable Credentials
given the issuer DID and the subject DID.

### did-client Source Code

The did-client source code is available on Github:

[did-client Github Repository](https://github.com/digitalbazaar/did-client/tree/issue)

The current client supports the creation of Testnet DIDs on the Veres One
ledger as well as the retrieval of those DIDs from the Testnet. You can
try the tool out by doing the following commands on a system that has
node.js and a C++ compiler installed:

    npm install did-client
    cd node_modules/did-client
    ./did create
    ./did issue -d <did:ISSUER_DID> <did:SUBJECT_DID>

To download the source and install the client:

    git clone https://github.com/digitalbazaar/did-client.git
    cd did-client
    npm install
    ./did create
    ./did issue -d <did:ISSUER_DID> <did:SUBJECT_DID>

Once you have created a DID, you can retrieve it from the ledger doing this
command:

    ./did get <DID>

There are plans to support the following other commands and features:

  * Adding, rotating, and removing authentication credentials
  * Adding and removing authorization capability descriptions
  * Adding and removing service descriptions
  * Checking the validity of a DID (deep blockchain check)

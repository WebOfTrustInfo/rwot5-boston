# Decentralized Identifier Tooling
***by Manu Sporny and Matt Collier, Digital Bazaar***

## Introduction

In order for Decentralized Identifiers (DIDs) to proliferate, tooling is
necessary. We should build this tooling as a community to reduce
duplicated effort. The tooling that we create should first be targeted at
developers so that they can easily integrate DIDs into their projects. Once
we have built an acceptable number of low-level libraries and tools, we can
move on to more customer-facing technologies.

Since there will be several ledgers that support DIDs, it is imperative
that we create a common set of tools and libraries for managing DIDs.
It is expected that these tools will use a driver or plugin-based
architecture. This approach will enable the general tool to be universal
and have a well-known feature set with additions to the tool
provided by developers for each ledger the tool supports.

## did-client

Digital Bazaar offers the first sort of this tool, which is a command-line
utility for creating, retrieving, and updating DID Documents across
multiple ledgers. A demonstration video of the tool, as well as an
explanation of how it works, can be viewed here:

[did-client Demo Video](https://www.youtube.com/watch?v=tQzQKZKF93w)

### did-client Source Code

The did-client source code is available on Github:

[did-client Github Repository](https://github.com/digitalbazaar/did-client)

The current client supports the creation of Testnet DIDs on the Veres One
ledger as well as the retrieval of those DIDs from the Testnet. You can
try the tool out by doing the following commands on a system that has
node.js and a C++ compiler installed:

    npm install did-client
    cd node_modules/did-client
    ./did create

To download the source and install the client:

    git clone https://github.com/digitalbazaar/did-client.git
    cd did-client
    npm install
    ./did create

Once you have created a DID, you can retrieve it from the ledger doing this
command:

    ./did get <DID>

There are plans to support the following other commands and features:

  * Adding, rotating, and removing authentication credentials
  * Adding and removing authorization capability descriptions
  * Adding and removing service descriptions
  * Checking the validity of a DID (deep blockchain check)

## Collaboration

We are seeking individuals at this Rebooting Web of Trust event to coordinate
on how this tool should be built, what features it should have, and to
recruit implementers to write plugins for their favorite DID-supporting ledgers.

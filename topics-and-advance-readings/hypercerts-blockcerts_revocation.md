# Hypercerts: Blockcerts Revocation Improvements
[![alt text][inProgressBadge]](https://github.com/blockchain-certificates/revocation)

**By [João Santos, Instituto Superior Técnico](https://github.com/joaosantos15)**

**Contributors: [Kim Hamilton Duffy, Learning Machine](https://github.com/kimdhamilton)**

*This is a proposal for an architecture of [Blockcerts'](https://github.com/blockchain-certificates) certificate revocation using Ethereum smart-contracts and it follows the ["Hypercerts Thesis Proposal"](https://github.com/joaosantos15/hypercerts/blob/master/Hypercerts_project.pdf).*

## Intro

The Blockcerts iniciative allows for Open Badges compliant certificates to be issued in the Bitcoin blockchain. This has a lot of blockchain inherited bennefits. However, the current Blockcerts implementation does not offer good mechanisms to handle certificate revocation and certificate permanence. 

Hypercerts consists on a set of aditions to Blockcerts that aims at improving the latter's revocation functionality (allow certificates to be revoked by any pre-agreed on combination of parties, contemplate temporary revocation) and also add certificate permanence (ensure that from the point of its issuance, a certificate's link is always the same).

This body of work extends the [Hypercerts Thesis Proposal](https://github.com/joaosantos15/hypercerts/blob/master/Hypercerts_project.pdf) revocation mechanism section.
 
The main goals of this mechanism are to allow revocation by an arbitrary combination of parties and to allow for batch issuing and revocation in an economical fashion. It is also desirable to have an architecture that can be easily implemented in other blockchains.

The proposed architecture for multi-party revocation consists on using **revocation proofs**. For each certificate to be considered revoked it needs to have a set of revocation proofs issued to it. The number of revocation proofs each certificate requires to be considered revoked can vary from certificate to certificate, even if they are part of the same batch, and is defined upon batch issuance. An ethereum smart contract controls the issuance of revocation proofs and contains a an IPFS link to all the files relevant to the system’s operation.

## Revocation Mechanism

After the creation of an unsigned batch of certificates, three items are generated, as can be seen in the figure below. 

* A file, accessible via IPFS, which can be embedded in the certificate, that entails the revocation policy for each certificate in that batch, this means that even in the same batch, different certificates can have different revocation policies, which is a very flexible feature.

* A file, accessible via IPFS, that maintains a list of the revocation proofs (explained in the next section) for each certificate in a batch.

* A smart-contract that will be responsible for managing the list of revocation proofs. Its job is to update the IPFS link when new revocation proofs are added to a certificate.

After the creation of the smart-contract and revocation policy file, URIs to these two are embedded in the unsigned certificate.

At this point, the certificate is signed and issued in the Bitcoin blockchain.

## ![](https://user-images.githubusercontent.com/10178757/29876393-91039232-8d94-11e7-908a-07aebfed5f6e.jpg)

### Revocation Status, Rules and Proofs

> Revocation Status

The revocation status of a certificate is not kept in any place. Instead it is calculated every time a client has interest in it. The way to verify the revocation state of a certificate is to analyse what are called revocation proofs which are documents that are digitally signed by parties authorized to revoke a certificate. 

> Revocation Rules File

The schema of the revocation rules file is still unclear, but will contain the following elements:

* The period in which revocation can occurr. This can be an open or closed interval.
* The identities of the parties who can issue revocation proofs. A simple solution for this would be to put the parties public keys as identifiers, but this raises a _future proof_ issue, as it would require the revoking parties to maintain those sets of keys for entire lifetime of the certificate. A better approach would be to use distributed identifiers.
* The conditions upon which proofs operate under. This defines is all the listed proofs are required (an intersection,_and_) or only a subset.

> Revocation Proofs File

The schema of this file is still unclear, it can be a string signed by a revocation key, being that each party has its own revocation key.

So, for instance, if we have a certificate that is revocable by a combination of Issuer and Receiver, the way to verify that such certificate had been revoked would be to search for revocation proofs of the Issuer and the Receiver.

### Structure of the smart-contract

There is one smart-contract per batch and each is responsible for maintaining the state of revocation of a batch of certificates and/or of specific certificates. A naive approach to this problem could be to have a list with a number of elements equal to the number of certificates and per each element of the list, a revocation status and revocation proofs would be kept. The problem with this approach is that it does not scale in two situations:

* Large number of certificates: As the number of certificates grows the list would grow larger and larger.

* Large number of revocation parties: The Multiple Parties Revocation method allows for an arbitrary number of parties to be required to revoke a certificate. Given that for each party a revocation proof would be generated, items of the revocation list would become too big.

The architecture we propose consists on having the smart contract controlling the issuance of revocation proofs and keeping the revocation proofs accessible via IPFS, being that the smart contract only maintains the link to the most recent list of certificate revocation proofs.

### Verification of Revocation Status

In the Blockcerts ecosystem, there are several verification steps to validate a certificate, verifying its integrity, verifying the validity of the key it was signed and issued with and, finally, verifying that said certificate has not been revoked. Given that this document is only concerned with revocation, we are going to focus on the latter (the reader can refer to Blockcerts’ documentation to learn about the other verification steps).

To understand how revocation verification is carried on, let’s assume a scenario where two certificates, *Certificate A* and *Certificate B*, require both the Issuer and the Receiver.

![](https://user-images.githubusercontent.com/10178757/29876402-94893c68-8d94-11e7-9ea0-57635464ed63.jpg)

The verifier starts by retrieving the *Revocation Rules file *and the ID of the Ethereum smart contract responsible for keeping track of the revocation proofs for that batch, both of which can be found directly on the certificate. From there the verifier checks the smart-contract for the link to the latest revocation proofs file and then it checks the file for the required proofs. 

At this point, one of two things can occur, either the revocation proofs are enough to consider the certificate revoked (figure on top) and the verifier considers the certificate not to be valid, or there are not enough proofs for the certificate to be considered revoked (figure on the bottom) and the verifier considers the certificate valid.

[inProgressBadge]: https://img.shields.io/badge/In_Progress--yellow.svg

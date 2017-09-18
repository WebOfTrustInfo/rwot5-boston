# The Horcrux protocol: Biometric credentials as high-privacy verifiable claims
## John Callahan (Veridium IP Ltd), Asem Othman (Veridium IP Ltd)

Private keys locked by biometrics on mobile devices provide not only ways for users to authenticate themselves, but also to
manage important assets tied to the corresponding public keys used in various contexts including blockchains (NOTE:
https://www.w3.org/2016/04/blockchain-workshop/interest/blocko.html),
(NOTE:  https://www.slideshare.net/FIDOAlliance/fido-authentication-blockchain).
Biometric authentication is increasingly being used on mobile devices to secure private keys and other sensitive
personally identifiable information (PII) in some form of trusted platform module (TPM).  While on-device biometrics
(NOTE:  Gartner refers to on-device biometrics as "local" biometrics) have advantages for service providers
(who want to avoid risks associated with PII loss) and users (who feel they have control of their PII if it is
locked on their device), it also has important disadvantages for both users and providers, namely presentation attacks,
device attacks, loss of device, and theft.  Revocation and recovery of associated credentials, accounts and other
assets previously tied to on-device keys can be complex, error prone and subject to social engineering.

To avoid these problems and comply with identity proofing requirements like know-your-customer (KYC) and anti-money
laundering (AML) regulations, many financial institutions are opting for server-side biometric authentication solutions.
A recent paper (NOTE:  Giulio Lovisotto, et al, Mobile Biometrics in Financial Services: A Five Factor Framework,
CS-RR-17-03, University of Oxford Computer Science Department.) favorably compares two biometric authentication protocols,
FIDO UAF and IEEE 2410 BOPS, as the leading methods for biometric authentication in financial services.  While these
protocols focus on defense against scalable attacks, they rely on device-specific TPM for protection and processing of
biometric templates.

The IEEE 2410 BOPS protocol is extensible to a combination of on-device (FIDO UAF compatible), server-side or a
multi-distribution model that utilizes a secret scheme.  Indeed, the standard allows for off-device biometric credentials
under user control.  The device’s local TPM is only one option (though dominant at the moment) for persisting biometric
credentials and associated key(s).  We propose implementation of a BOPS-compatible biometric credential storage option
using the high-privacy verifiable claims (NOTE:  https://blog.tokenize.io/high-privacy-verifiable-claims-4e556af28fe2)
format.  Credentials would be stored off-chain as as a DID Descriptor Object
(NOTE:  Data Model and Syntaxes for Decentralized Identifiers (DIDs) - https://w3c-ccg.github.io/did-spec/) (DDO)
with its referent decentralized identifier (DID) stored on a  blockchain.  Use of DDOs for biometric templates
has already been proposed (NOTE:  Stephen Wilson, Safeguarding the pedigree of personal attributes,
http://lockstep.com.au/blog/2014/09/01/pedigree-of-ids), but to further protect the biometric data, we propose
the use of the existing BOPS multi-distribution model that utilizes a secret scheme to divide the templates into n ≥ 2
shares using visual cryptography (NOTE:  Ross, Arun and Asem Othman, Visual Cryptography for Biometric Privacy, IEEE
Transactions on Information Forensics and Security, Volume: 6, Issue: 1, March 2011) as specified in IEEE 2410-2015
and IEEE 2410-2016.  Multiple shares (and potentially redundant shares) could be spread across alternate off-chain
storage (like IPFS, Dropbox, Storj, etc.) to improve availability and security.  The PII have been encrypted to generate
these shares in such a way that the PII can be revealed only when the predefined number of shares are simultaneously
available; further, the individual Shares do not reveal any information about the original PII. We believe that a
straightforward implementation of high-privacy verifiable claims for biometric credentials could be integrated
with Blockstack authentication and incorporate evolving decentralized key management systems (NOTE:  Rebooting Web
of Trust, D. Reed, DKMS: Decentralized Key Management Systems (Spring 2017)), (NOTE:  Decentralized Key Management
using Blockchain (see https://www.sbir.gov/sbirsearch/detail/1302463)) (DKMS).  Rather than reinvent the wheel, we
seek to incorporate biometric credentials as securely as possible within an ecosystem of open standards while
restoring privacy and consumer control even within server-side scenarios, particularly use of social and biometric
revocation and recovery mechanisms.

The use of biometrics will continue to grow and be used for authentication, asset management and transaction records.
The horse is out-of-the-barn: systems like Aadhaar, IAFIS, etc. already use server-side solutions and do not advance
self-sovereign identity (SSI), i.e., they hold personal data (e.g., biometrics) in a centralized store under a central
authority.   Will each Internet-of-Things (IOT) require individual biometric enrollment, a TPM, and supporting sensors?
Surely, these devices will rely on server-side biometric solutions for convenience and scale, but likely with poorly
designed one-off, hand-rolled solutions with critical vulnerabilities.  The original vision of ubiquitous computing was
that mobile devices could be used and borrowed like a ball-point pen and not "personal" like the first computers.
Finally, as blockchains allow previously “unbanked” persons sovereignty over their assets, we will need device-independent
means to enroll, verify, and authenticate payments using biometrics in addition to or an alternative to passwords that
can be forgotten, paper wallets and tokens that can be lost or stolen. 

We would like to find people to explore these ideas in order to determine how to get this tech to market in the next
year.  Our current products, VeridiumID and VeridiumAD, provide biometric transaction signing, end-to-end compliance
with IEEE 2410-2016 including mobile and server-based secure storage of credentials, with FIDO UAF and with existing
products and standards like Active Directory, Citrix, SAML 2.0 and OpenID Connect.   Continuing the spirit of our open
standards work, we seek to integrate IEEE 2410 BOPS with existing identity standards like DIDs/DDOs via the Verifiable
Claims work, DKMS, Open Badges, Blockstack auth, WebAuthN, and other evolving efforts.

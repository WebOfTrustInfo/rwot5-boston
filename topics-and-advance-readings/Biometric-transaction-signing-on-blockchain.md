# Biometric transaction signing on blockchain
## John Callahan (Veridium IP Ltd), Virgil Tornoreanu (Veridium IP Ltd)

The use of strong customer authentication (SCA) is a critical requirement for collecting explicit consent under the new
PSD2 regulations, but equally important are GDPR regulations like the "right to be forgotten" that require banks to purge
their records of any data associated with an account at a former customer’s request.  These regulations are designed to
empower individuals with control over their data held by institutions, but technical, legal and policy difficulties are
delaying programs needed to implement such policies.  Delay means that new financial services providers like AISPs
(NOTE:  Account Information Service Providers (see https://www.w3.org/Payments/IG/wiki/PSD2#AISP)) and PISPs
(NOTE:  Payment Initiation Service Providers (see https://www.w3.org/Payments/IG/wiki/PSD2#PISP)) that require consent
to access personal information will avoid postpone important innovations to avoid incumbent risks.  

Strong customer authentication (SCA) means that 2 out of 3 methods for authenticated consent must be employed on high-risk
financial transactions (any single payment or transfer over 50 Euro or cumulatively (or 5 consecutive transactions) over
150 Euro (NOTE:  Regulatory Technical Standards (RTS) on strong customer authentication and secure communication under
PSD2, Chapter 2, Article 11 - Contactless payments at point of sale)).  The three methods (NOTE:  Regulatory Technical
Standards (RTS) on strong customer authentication and secure communication under PSD2, Chapter 2, Article 4 pursuant
Article 97(1) of Directive (EU) 2015/2366) are:

1. Knowledge: something only the user knows (such as a password).
2. Ownership: something only the user possesses (such as a chip card).
3. Inherence: something the user personally or physically has (such as a fingerprint).

These methods must not be connected and each transaction must be distinct (e.g., unique and non-sequential transaction
identifiers).  In addition, biometric authentication uniquely offers the possibility for non-repudiation and favored by
some institutions for consent because it is difficult to contest legally.  In the case of passwords or token, the customer
could deny approving the payment due to the theft of password or token.   Such cases are not theoretical (NOTE: 
https://www.finextra.com/blogposting/14068/taking-bold-steps-to-protect-high-value-trading).  In addition to covering
billions in fraud costs, financial institutions face severe fines under GDPR (NOTE:  Organizations can be fined up to
4% of annual global turnover for breaching GDPR or €20 Million) for failure to "most serious infringements e.g. not having
sufficient customer consent to process data" and other violations (NOTE:  http://www.eugdpr.org/gdpr-faqs.html).  

The IEEE 2410-2016 BOPS protocol extends IEEE 2410-2015 in order to be PSD2 compliant by incorporating the explicit
consent message, beneficiary and amount in any authentication request as an option for authentication, signing and
escalated transaction calls.  For a given payment transaction, the customer is prompted for biometric authentication
on the mobile device with a message indicating the reason, beneficiary and amount.  If successful, the transaction is
signed with an associated private unlocked by biometric authentication, transmitted to and recorded in server logs
that can be audited, archived and purged as per records management regulations.  The transaction is "biometrically signed"
by transitive association of the key associated with the biometric.

As an alternative storage option, we propose use of off-chain DID Descriptor Object (NOTE:  Data Model and Syntaxes for
Decentralized Identifiers (DIDs) - https://w3c-ccg.github.io/did-spec/) (DDOs) with referent decentralized identifier
(DIDs) on blockchains for recording of PSD2 compliant transactions.  Specifically, a biometrically signed transaction
would exist as a high-privacy verifiable claim (NOTE:  https://blog.tokenize.io/high-privacy-verifiable-claims-4e556af28fe2).
Several issues must be addressed to protect user privacy, allow for regulatory compliance and auditing, records purging
via revocation, and recovery in case of loss of credentials.  We envision several options for institutions and their
customers based on security "profiles" that allow customers to balance privacy with convenience including:

* Storage of encrypted transactions off-chain in user owned media (IPFS, Dropbox, Storj, etc.) that gives a customer sovereign control, but restricts the type of services based on availability
* Storage of encrypted transactions off-chain in publicly accessible storage at the institutions choice using customer’s public key(s).  Subsequent audits could be done only with customer’s authorization.
* Storage of encrypted transactions off-chain in public or private accessible storage at the institutions choice using customer’s private key(s).  Subsequent audits could be done by institution or customer.

Our approach to blockchain-based biometrically signed transactions promotes self-sovereign identity by allowing customers
to control their record data.  This benefits both the customer and financial institutions themselves by reducing the risk
of lost, costs of compliance, and improve secure access to data by the new AISP and PISP providers without resort to
centralized services (like the ASPSPs).  Projects like the Open Banking Project (OBP) could adapt their APIs to accommodate
blockchain-based methods using serverless methods for payment processing.  Any blockchain-based transaction recording scheme
should also integrate with digital identity providers and standards, related authentication methods (e.g., Blockstack auth,
WebAuthN/FIDO 2.0) and decentralized key management systems (DKMS) (NOTE:  Rebooting Web of Trust, D. Reed,
DKMS: Decentralized Key Management Systems (Spring 2017)), (NOTE:  Decentralized Key Management using Blockchain
(see https://www.sbir.gov/sbirsearch/detail/1302463)).

We would like to find people to explore these ideas in order to determine how to get this tech to market in the next year.
Our current products, VeridiumID and VeridiumAD, provide biometric transaction signing, end-to-end compliance with
IEEE 2410-2016 including mobile and server-based secure storage of credentials, with FIDO UAF and with existing products
and standards like Active Directory, Citrix, SAML 2.0 and OpenID Connect.   Continuing the spirit of our open standards
work, we seek to integrate IEEE 2410 BOPS with existing identity standards like DIDs/DDOs via the Verifiable Claims work,
DKMS, Open Badges, Blockstack auth, WebAuthN, and other evolving efforts.  

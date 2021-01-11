---
nft-rfc: 5
title: NFT Rights Specification
stage: draft
category: NFT/METADATA
author: Joe Andrieu @jandrieu
created: 2020-12-10
modified: 
---

# NFT RFC 005 NFT Rights

# Motivation
NFTs embody and confer specific rights. This specification describes how 
rights relate to the Interchain NFT work.

# Technical Specification

## Title/Property Pattern

We model the rights in Non-fungible Tokens based on a token/resource
pattern. This pattern separates property rights for the token itself
from rights in a related resource that are conferred upon the token\'s
owner or representative.

This pattern allows us to cleanly distinguish between the issues of
ownership (transfer, exclusion, control, use, possession) as token
rights, which are realized entirely on-chain and therefore
computational, and resource rights in the real world, which may be
dependent on interactions with non-digital systems, organizations, and
processes. With these two pillars, token rights and resource rights
allow us to model arbitrarily complex, digitally enabled rights systems.

### A Few Examples
A NFT Theater Ticket issued, bought, and re-sold entirely on-chain
according to parameters established by the Theater Company. The ticket
gives its owner the right to attend a given show, if it occurs and the
bearer meets any other requirements of the venue, such as wearing proper
attire or behaving with decorum, or even evidence of a vaccination or a
biometric verification of identity.

**Token rights**: resalable bearer instrument with constraints.\
**Resource Rights**: the bearer is entitled to attending a specific show
at a specific time, subject to venues rules.

An NFT Property Title issued, bought, and re-sold entirely on-chain
according to parameters established by the local housing authority. The
title gives its owners the legally recognized rights of property
ownership. Courts, banks, and civic institutions recognize those legal
rights through verification of ownership represented by the title.

**Token rights**: delegatable, transferrable, provable title
(cryptographic proof required for transfer and proof of ownership)\
**Resource rights**: ownership in real property recognized by a specific
jurisdiction

An NFT Pay-per-View Venue Media License issued, bought, and re-sold
entirely on-chain according to parameters established by the copyright
holder. The licenses gives its holder the legal right to play specific
media (such as a boxing match) in commercial venues, such as a local
restaurant or bar, for a specific price, as evidenced by on-chain
payment. This license is owned by a fan and delegated to the venue for
the actual performance.

**Token rights**: a delegatable, resalable cryptographically secured
authorization\
**Resource rights**: performance rights for a specific piece (or
catalog) of media in a specific context with payment of a pre-arranged
price.

This distinction, between the ownership rights in a 100% digital asset
and a different set of rights conferred to whoever owns that asset,
allows us to model arbitrarily complex bundles of rights which can be
created, bought, sold, and verified through distributed ledgers.

## NFTs as Constrained Tokens
NFTs are constrained tokens, which have one or more constraints that
must be met for exercising any rights associated with that token. Pure
bearer tokens represent rights that are conferred to the holder of those
tokens without externality. Interchain NFTs are not bearer tokens. They
are constrained by one or more mechanisms, the most basic is
cryptographic proof of control for transfers.

### Co-artifacts
The canonical constraint on blockchain-based assets is proof-of-control:
in one form or another, a party asserting a token right demonstrates
access to a private secret that unlocks a cryptographic puzzle. The
traditional mechanism for this is a hash of a public key stored
on-chain, for which the actual key and a message signed with the
matching private key serve as co-artifacts for authorizing a
transaction. Advanced cryptographic operations, like Schnorr signatures,
provide additional logical operations that can be used to evaluate such
co-artifacts, for example, enabling an n-of-m rules for use.

A co-artifact could also be a Verified Credential of a particular kind.
For example, a token that is good for one free beverage for any bearer
who can provide a newly issued digital degree. Call it a \"graduation
promotion token\". Or perhaps a token for access to a particular
restaurant, if and only if, the bearer also has a verifiable vaccination
credential. Finally, a co-artifact might be a \"verified credential\"
which is a verifiable credential issued based on verifiable claims
asserted by authorized reviewers who have evaluated underlying
verifiable credentials against a specific set of criteria. (See the
Impact Bond User Story for more details on these different types of
verifiable/verified claims/credentials.)

### Biometric or Physical Constraints
Tokens can also be bound by a biometric or physical constraint that must
be applied by the operationalizing party. For example, a visual
inspection of proper attire or a biometric match evaluated at the point
of use. For example, an NFT could be directed to a party who can provide
and satisfy a cryptographic commitment of a biometric template, such as
a photo or facial recognition pattern. The NFT \*could\* directly
include the biometric, but for privacy and confidentiality reasons, it
is preferred that a hash of that template is used instead, leaving the
propagation of the underlying template up to the individual. Either way,
for the token to be used, that constraint must be met to the
satisfaction of the operationalizing party. In all cases of real-world
constraints, an operator must provide the final step in linking the
digital to the physical. In this case, in providing the evaluation that
the biometric template matches the bearer of the token before approving
the use. Such biometric direction \*can\* also be achieved as a
co-artifact if we empower an operator to issue a verifiable attestation
that the biometrics have been satisfied and that artifact is then
recognized by the operationalizing system.

### Legal Constraints
Tokens may also represent rights or responsibilities assigned to, or
involving, specific legal entities or categories of entities, for which
legally acceptable proof of identity is required. For example, one could
imagine a travel visa as a token authorizing the bearer to enter,
reside, and work in a particular country, provided the bearer can
produce a legitimate state-issued passport matching a particular legal
name. Using the token would require a system (or an individual) to
evaluate real-world passports for validity and applicability to a token
bearer. Perhaps more simply, one might imagine a token as a pre-paid
customs waiver for the import of restricted goods, which requires
demonstration of legal identity acceptable to the customs office. This
construct allows longer-lived digital tokens to be created, used,
delegated, transferred, while deferring the external, legally specified
constraints that may be imposed at the point of use using the most
appropriate mechanisms. In some circumstances the legal identity might
be digitally verified, in others, using traditional credentials like a
passport. We anticipate that tokens related to supply chains and
international travel will most likely be of this nature: the token
represents one part of a complex set of requirements for execution,
which must be accompanied by real-world artifacts as required by the
relevant country.

## Requirements
### R1 -- Specify rights and responsibilities

NFT metadata must be able to specify associated rights and
responsibilities. This includes token rights for realizing ownership of
the token as well as resource rights afforded to an authorized bearer of
the token.

Token rights must be computationally evaluatable, including support for
cross-chain atomic transactions.

Resource rights must be either human readable or machine readable in a
semantically rigorous manner. Human readable rights may be as simple as
\"the bearer of this token is entitled to buy one, get one free on any
Acme product.\" Provided the rights are understandable and enforceable.
This includes arbitrarily complex legal agreements that may be
associated with an NFT. Machine readable rights must use semantically
rigorous representation such as RDF or domain-specific constrained
vocabulary. In both cases, arbitrary rights and responsibilities must be
representable.

### R2 -- Rights and responsibilities must be discoverable, understandable, and verifiable

Rights innate to an NFT must be discoverable and verifiable. Prior to
acquiring a token, a prospective buy must be able to achieve confidence
that they have---or will have---all information required to exercise any
afforded rights. This can be achieved through commitments---including a
merkle tree which obfuscates the number of associated externalized
rights and responsibilities---such that the actual rights and
responsibilities can be confirmed authoritatively without publishing
those rights to the world or on an immutable medium. Any externally
rooted privileges, such as recognition of a specific driver\'s license
by a recognized Department of Motor Vehicles, may require off-chain
verifiability.

NFTs must provide a way for a current owner to record a non-repudiatable
attestation of the completeness of known external impacts on rights and
responsibilities. For example, that a given property meets all code
requirements for sale of residential property such a termite inspection,
or that there are no outstanding, undivulged liens or claims against the
property.

For computational assistance with operationalization, machine-readable,
semantically rigorous rights representations are preferred.

### R3 -- Rights and responsibilities must be amendable

NFTs represent a current bundle of rights and responsibilities, which
may change over time. For example, an airline ticket for a specific seat
on a specific flight, in which the seat is changeable with any available
seat. Such variability and any constraints therein must be represented
either by the initial issuer of the NFT or by attaching a constraint
that is understood by the operator evaluating the token in use. This
includes the ability for a holder to delegate an NFT with specific
caveats and for external actors to assert restraints, such as a health
agency requiring masks for entry into restaurants. Many use cases
require these adjustments to be machine executable, while others require
support for externalizing the evaluation, either to a party presumed to
be physically present or to an external information system that is
presumed authoritative. In any case, the goal is to enable these
amendments to be deterministically identified and evaluated as
adjustments to the initial rights afforded to the token.

### R4 -- Rights and responsibility must be operationalizable
NFTs rights much be operationalizable, either computationally or through
external actors or oracles. NFT token rights, in particular, must be
computationally operationalizable on-chain.

Computational evaluation includes code that can be executed on-chain
like, eRights in SES, Solidity, and ScriptPubKey and PayToScriptHash. It
also includes mechanisms like Schnorr muti-sig and DID Documents.
Schnorr allows limited forms of rights to be cryptographically evaluated
while DID Documents allow various indirect cryptographic capabilities,
using the material in the DID Document for evaluations related to a
referenced DID.

External evaluation includes rights representations that can leverage
the presence of an extern al party:

1.  **Usher / Bouncer / Ticket** Taker -- A physical person is present
    to ascertain any real-world constraints that might apply (proper
    attire or biometric check)

2.  **Judge / County Clerk** -- An institutional party may need to
    attach rights or verify rights related to specific tokens
    (easements, judgments, and formal recordation in external systems)

3.  **Cashier** -- Applies real-world constraints before accepting a
    token for use, such as verifying the age of a purchase of
    age-restricted goods or physically inspecting an item for returns,
    e.g., with an NFT for an Return Merchandize Authorization (RMA).

4.  **Service Personnel** -- Personnel who literally do physical work to
    realize a resource right, such as a janitor, cleaner, gardener,
    security guard, plumber, or contractor, fundamentally must be able
    to choose not to execute certain expected rights, if, on their own
    judgment, they cannot ethically or safely do so. This possibility
    must be supportable in those use cases that require it.

In external evaluations, the token (and its proof of ownership) is just
one factor in a multi-factor use cases. The requirement is to be able to
enable these additional factors.

## Security Requirements

### R5 -- Cryptographically provable ownership

The owner of an NFT, who is afforded all of the property and resource
rights associated with the token, must be cryptographically verifiable.
Any party who is capable of solving a cryptographic challenge is deemed
an owner.

### R6 -- Cryptographically delegatable rights

Resource rights associated with a token MUST be cryptographically
delegatable such that delegates can invoke those rights by solving a
cryptographic challenge.

### R7 -- Non-repudiatable transfers

Property transfers of NFTs must be able to be executed with at least
probabilistic non-repudiation. That is, once consensus for a particular
transaction is achieved, that transaction cannot be reversed without
extraordinary measures.

### R8 -- Auditability

Property transfers MUST be auditable. It should be possible for a
prospective buyer to evaluate the entire chain of title from the
initiating source. It is permissible for this chain of title to require
off-chain information to fully understand, however, any party should be
able to determine whether or not they have all of the information
required to verify the provenance of a given NFT and once they do have
all of that information, it should be possible to see the history of the
NFT.

### R9 -- Key Rotation & Revocation
NFT owners should be able to rotate and revoke any keys associated with
their NFT rights without changing the unique ID of the NFT.

## Privacy Requirements

### R10 -- Off-chain, verifiable data

NFTs must be able to reference off chain resources in a verifiable way
without actually divulging the location or content of those resources.
For example, using a content hash to refer to external dependencies or a
merkle tree of commitments to collect all such references into a single
hash.

### R11 -- Minimally pseudonymous property rights

Property rights SHOULD be executable with a minimum of correlatable
identifiers, aka psuedonyms. Property rights in tokens, MUST be
executable without deference to any outside authorities, who might
impose restrictions related to owner identity. Resource rights, on the
other hand may not be able to avoid linkage to real-world
identity-proofing requirements. NFT must be able to support both use
cases.

### R12 -- Self-contained namespace

NFTs must be able to make arbitrary statements about any particular
resource without deference to external identifiers. Statements related
to an NFT MUST be expressable entirely in relation to identifiers
defined within the NFT\'s namespace. References to external or real
world assets MUST be expressable in a manner that (1) clarifies the
means by which the reference is grounded to objective, measurable facts
and (2) relates those facts to an identifier in the namespace.

For example, a Title Property NFT identified by a URI **did:title:abc**
defines a namespace, within which the NFT itself defines
**did:title:abc/parcel1** as a lot of real property, bound by particular
GPS coordinates (mapping the real world to the digital). Subsequent
statements about that property can be made by referring parcel1, e.g.,
parcel1 is a Unesco World Heritage Site. In this way, NFTs avoid the
HTTPRange14 problem while providing a uniquely encapsulated namespace
for assertions---which is guaranteed (at least insofar as the
identifiers are implicated), NOT to collide with or leak data from any
other namespace.

### R13 -- Self-contained assertions
Using its own namespace, plus potentially externally defined
terminology, an NFT must be able to provably assert statements without
reliance on any externality for verification. These assertions may or
may not be essentially

This could, for example, be realized by establishing an AssertionMethod
for an NFT

### R14 -- Self-contained authentication

Authentication to exercise any resource rights associated with an NFT
\*should\* be entirely contained within the NFT metadata, such that
authentication may be accomplished without recourse to external
authorities. Exercise of token rights---such as transferring ownership
to another---SHOULD be entirely scoped by the originating blockchain,
without reliance on external identifiers or authorities. This should be
interpreted as a requirement to support delegation and temporary
authorizations without any external party involvement.

### R15 -- Separation of verification and directory services

Separating the verification of NFT metadata from its retrieval allows
for privacy-respecting and regulatorily responsive means to establish
authenticity without under privacy harms. Using distributed ledgers
(DLTs) as a distribution vehicle for confidential or proprietary
information can lead to sensitive data being irrevocably distributed to
the world. However, DLTs are excellent at establishing a globally
ordered consensus, which can---within the constraints of the consensus
mechanism---definitively establish what the \*current\* metadata is.
Naïve approaches simply put such information on-chain, which would
unnecessarily expose that information to the world, even though it
allows third parties to retrieve said information without dependence on
external systems. Interchain NFTs must provide the means to separate the
verification of current authoritative metadata from its distribution,
allowing the use of GDPR and CCPA compliant processing of sensitive
data. As such, the verification of metadata must be possible independent
of the distribution mechanism for that metadata.

## Representations
In order to define and operationalize rights, NFTs must provide
interoperable representations of those rights.

### R16 -- Token rights must be deterministically executable

As discussed in R4, NFT rights must be operationalizable, including
executable code such as eRights in SES, Solidity, and PayToScriptHash.
In particular, representations of token rights MUST be executable.
Resource rights *may* be executable, but in many use cases they cannot
be fully realized in code.

Representation of resource rights must support rigorous interpretation
of rights for both automated and human-mediated processing.

This might be done with

(a) explicit, well-known rights representations, such as the
    VerificationRelationships defined within a DID Document, for
    specific, constrained use cases.

(b) open-ended semantic statements using RDF for machine processable
    assertions

(c) open-ended plain-text statements representing legally binding terms

### R17 -- Resource rights must support automatic evaluation when required

Resource rights must be representable semantically rigorous manner for
automated evaluation of rights from arbitrary issuers.

### R18 -- Resource rights must support human evaluation when required

Some rights may require a human individual to evaluate said rights, for
example, with the service personnel who is trying to make a decision
about whether or not a particular repair is covered by a Warranty NFT.
Not all rights are appropriate for representing this way: understandable
English may muddle nuances necessary for certain use cases. However, if
a token is meant to be operationalized with a human actor, then the NFT
rights must presentable in a human readable manner.

### R18 -- Resource rights must support legal evaluation when required

Some use cases fundamentally rely upon courts, in so much as valuable
and complex transactions may be subject to significant legal review and
challenge. In some cases, NFTs must represent rights in such a way as to
be interpretable in a consistent manner by a competent court. Plain
English or RDF may not be sufficient for the limited technical expertise
of a typical courtroom or regulatory panel.

NOTE: R16, R17, and R18 align roughly with the Creative Commons three
\"Layers\" of licenses: machine readable, human readable, lawyer
readable. <https://creativecommons.org/licenses/>

### R19 -- Deterministic mapping between NFTs and supported blockchains

Native representations of NFTs must be mappable to compatible
operationalization platforms. For example, NFT rights should be able to
deterministically represent bitcoin multi-sig transactions, even if
doing so requires transformation from a native NFT representation
requires transformation to ledger-specific equivalents. By \"native\" we
mean the representations defined in this specification and by
ledger-specific we acknowledge that different blockchains define
different operational APIs. Whatever representation chosen for NFT
rights should be translatable to operations on as many major blockchains
as possible. However, we recognize that such mappings are unlikely to be
possible for all blockchains. The requirement is to enable a mapping
mechanism as part of NFT evaluation and operation such that when
possible, such mapping is part of the process.

### R20 -- Explicit acknowledgement of chain-specific limitations

Inevitably, some rights may not be realizable on specific blockchains,
which limits the cross-chain viability of certain NFTs. In the cases
where such limitations are known or knowable, it should be possible for
an NFT to proactively assert either compatibility with particular chains
or known incompatibility with particular chains. It may be possible to
reduce this compatibility to support for particular types of
representations, e.g., if token rights are represented as eRights in
SES, then chains that do not support evaluation of SES in its token
mechanics won\'t be able to support that NFT.

### R21 -- Representation of resource rights in a chain agnostic manner

Resource rights must be presentable in a manner that is independent of
chain logic, such that these rights do not depend on the consensus or
smart contract mechanisms of particular chains. Instead, they must be
evaluatable independent of the chain or record. This allows, for
example, the use of eRights for executable resource rights attached to
NFTs anchored to blockchains that do not support SES as part of
consensus evaluation.

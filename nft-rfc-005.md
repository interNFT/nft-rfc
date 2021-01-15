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
This specification describes NFT rights in the context of Interchain NFTs and Metadata. 
Interchain NFTs are containers for resource identifiers and for the rights relating to the identified resources, regardless of where these resources are located. 
This implies that it should be possible to access across blockchain networks the encodings of NFT rights and associated object capabilities which are conferred by these rights. It should be possible to exercise control over NFT rights and to execute object capabilities across networks, using Inter-Blockchain Communication protocols. 

# Technical Specification

## Title/Property Pattern

We model Non-fungible Token rights as being Intrinsic or Extrinsic to the token. 
The intrinsic rights properties of an NFT define what the owner/contoller of the token is capable of doing to change the state of the token and its related on-chain metadata. Intrinsic rights therefore give the token owner the capabilities to change ownership of, transfer, exclude access to, control, use, or possess a token and its on-chain metadata.
The extrinsic rights properties of an NFT define what the owner/controller of the token is capable of doing in relation to the uniquely-identified token resources which are related to an NFT. Extrinsic rights therefore gove the token owner the capabilities to own, transfer, exclude access to, control, use, or possess resources which may be on-chain, or resources in other digital systems, or physical-world resources. 

This pattern makes a clear distinction between Token Rights which can be fully executed using the capapilities of a blockchain and Respource Rights, which are executed using the capabilities of other blockchain functions which are not directly related to the token, or other digital systems, or systems in the physical world, which may be dependent on interactions with all types of systems, processes and organisations.

These two patterns of Token Rights and Resource Rights allow us to model arbitrarily complex, digitally-enabled systems for defining and operationalising rights and capabilities over uniquely identifiable objects.

### A Few Examples
An NFT Theater Ticket issued, bought, and re-sold entirely on-chain
according to parameters established by the Theater Company. The ticket
gives its owner the right to attend a given show, if this takes place and the
bearer meets all the other requirements set by the venue, such as wearing proper
attire, behaving with decorum, passing biometric verification of identity, 
or even providing evidence of immunisation.

**Token rights**: resalable bearer instrument with constraints.\
**Resource Rights**: the bearer is entitled to attend a specific show
at a specific time, subject to the rules and restrictions of the venue.

An NFT Property Title issued, bought and re-sold entirely on-chain
according to parameters established by the local housing authority. 
The property title gives its owners legally recognized rights of property
ownership. Courts, banks and civic institutions recognize these legal
rights by verifying ownership of the Property Title token.

**Token rights**: delegatable, transferrable, provable title
(cryptographic proof required for transfer and proof of ownership)\
**Resource rights**: ownership in physical property, as represented by
a digital Property Title, which is contained by an NFT, is recognized 
as legally valid within the relevant jurisdiction

An NFT Pay-per-View Media License issued, bought, and re-sold
entirely on-chain according to parameters established by the copyright
holder. The license gives its holder the legal right to use (and capability to access)
a specific media asset (such as the broadcast of a boxing match), within a specific 
context, such as a commercial public venue (local restaurant or bar).
Access to the media is provided on evidence that the specifed license fee
has been paid (through an on-chain payment). 
This license could be owned by a fan and delegated to the venue for patrons to view.

**Token rights**: a delegatable, resalable, cryptographically secured
authorization\
**Resource rights**: Viewing rights for an identified media asset, within a specific 
uniquely identified context (such as a specific venue on a specific data), 
subject to any associated rights modifiers, and requiring evidence of payment.

Thw distinction between rights of ownership in a digital resource (such as media asset)
and the rights to use the resource, allows arbitrarily complex compositions of rights 
and capabilities related to digitally represented resources which can be created, authenticated, owned, bought,
sold, rented, etc.

## NFT Rights are Constrained
All NFTs have constraints on the capabilities which can be exercised in relation to Token Rights and Resource Rights.
In contrast, Bearer Tokens confer rights to whoever holds the token, which enables capabilities associated with these rights to be exercised, without constraints.

### Cryptographic Constraints
The primary constraint is that the owner of a token has to demonstrate control over the cryptographic key which is required for changing the state of the token or of its metadata. The party asserting a token right, or wanting to exercise the capabilities associated with a right, must demonstrate
that they have control over a private secret that unlocks a cryptographic puzzle. Blockchains typically enable this by storing a hash of a private key as a public artifact. The holder of the private key must be able to demonstrate that they can derive the hash using their private key as a co-artifact, to sign messages which are validated by the blockchain.  
Advanced cryptographic operations, such as Schnorr signatures, provide additional logical operations that can be used to evaluate such
co-artifacts. This may require constraints such as n-of-m signatures to be met, before a resultant capability can be exercised.

### Verifiable Credentials as constraints
Verifiable Credentials can be used in versatile ways to define the rights and constrain the capabilities of token-holders.
For example, a token which gives an identified student access to a personalised online course, which is constrained by the requirement that the student must present a Verifiable Credential issued by an academic institution, to prove that she has a prerequisite academic qualification.
The prove their credential online, the student must be able to authenticate with a cryptographic signature that they control the decentralised identifier (DID) 
which is the subject of the Verifiable Credential.

### Identification Constraints
Token rights can be constrained by the requirement for the token-holder's to be identified, or to demonstrate required characteristics.
This may be operationalised by a system of biometric authentication, or evaluation through visual inspection, or other forms of testing.
Identification mechanisms such as this have serious privacy risks -- even in correlating a counter-party with identifying characteristics that are would be linked to a transaction which is visible on a public ledger.
The constraints which are defined by an NFT and its metadata, and information that gets stored on-chain, must meet privacy and data protection requirements.
How to operationalise identification systems that meet these requirements is beyond the scope of this specification.

### Legal Constraints
The rights contained by an NFT may be constrained by legal definitions, interpretations and systems within a specific jurisdiction and context. 
Legal constraints may vary across jurisdictions and can change over time.
For instance, invoking international treaties, a token-holder may have the capability to engage in commercial arbitration within a specified jurisdiction, to resolve a dispute over the right of ownership of physical property, for which the Property Title is asssociated with an NFT. 

## Requirements
### R1 -- Specify Rights and Capabilities

NFT metadata must be able to specify the rights and associated capabilities of a Token-holder.
and resources which are identified by the token. 
This includes both the Token Rights and Resource Rights.

Token rights must be computationally evaluatable, with support for cross-chain operations.

Resource rights must be either human readable, or machine readable in a semantically rigorous manner. 
Human readable rights may be as simple as \"the bearer of this token is entitled to buy one, get one free on any
Acme product.\" Provided the descrioption of these rights is understandable, unambiguous and enforceable in ways that satisfy the needs of the token-holder.
This includes arbitrarily complex legal agreements which may be associated with an NFT. 

Machine readable rights must use semantically rigorous representation, such as RDF, or domain-specific constrained
vocabulary. In both cases, arbitrary rights and capabilities must be representable and resolvable by software systems.

### R2 -- Rights and capabilities must be discoverable, comprehensible and verifiable

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

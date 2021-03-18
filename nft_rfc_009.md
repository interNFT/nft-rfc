---
nft-rfc: 6
title: NFT Identifiers
stage: draft
category: NFT/METADATA
author: Joe Andrieu @jandrieu
created: 2021-03-18
modified: 
---

Abstract
========

Interchain Identifiers (IIDs) are a family of DID methods for
blockchain-based assets such as tokens, smart contracts, and addresses.
Built on Decentralized Identifiers from the World Wide Web Consortium
[[1]](#ref1), IIDs are 100% conformant DIDs; IIDs ***are*** DIDs and IID
documents are DID documents. The IID specification also provides
additional features designed for on-chain assets, such as the ability to
verifiably yet privately associate arbitrary digital or real-world
assets with the underlying IID Subject. IIDs also constrain compatible
DID methods in particular ways, including a restriction on the DID
Subject---IID Subjects MUST be on-chain resources. Any DID method that
meets the requirements in this specification ***is*** an IID method, and
its IIDs ***are*** DIDs. Any DID software that is conformant to the W3C
specification SHOULD be able to work with IIDs and IID documents,
although some IID-specific features may require additional support.

Introduction
============

Identifiers are needed to refer to both on-chain and off-chain
resources. Non-fungible tokens (NFTs) require a cryptographically secure
means to both refer to specific tokens and prove control or ownership
without reliance on a trusted third party.

We refer to this new class of identifiers as Interchain Identifiers, or
IIDs for short. We propose this new identifier would be appropriate for
any on-chain asset, including smart contracts, fungible tokens, and
non-fungible tokens.

IIDs build on a foundation of global identifiers dating back to Uniform
Resource Locators and Uniform Resource Identifiers [[2]](#ref2), which are the
foundation of the World Wide Web. URLs and URIs allow for different
schemes that specify particular mechanisms for interpreting and applying
the rest of the identifier. For example,
```http://example.com``` specifies a
web-based resource that can be retrieved using the hypertext transfer
protocol (http) and
```mailto:joe@example.com```
specifies a resource that can receive email messages using the SMTP
protocol.

IIDs are Decentralized Identifiers (DIDs), which build on URIs and URLs
to provide a class of identifiers one can verify without reliance on a
trusted third party. DIDs specifically support cryptographic
verification methods like public/private key cryptography on any number
of curves, which in turn are used for verification relationships like
authentication, assertion, capability delegation, and capability
invocation. When one uses a DID for those relationships, a verifying
party can use cryptographic material associated with the DID to verify
the use is appropriate. DID-URLs extend the base DID syntax to support 
```/path```, ```?query```, and ```#fragment``` parts. IIDs use the 
```/path``` and ```#fragment``` parts of URLs to refer to IID References 
and IID Resources.
We describe how IIDs and DIDs relate in section [IIDs as DIDs](#IIDs-as-DIDs).

IIDs also provide a consistent, verifiable approach for referring to
off-chain resources, whether digital, real-world, or conceptual. In this
role, IIDs rely on content-based identifiers and content-based
addressing systems, where a hash of the digital asset is used to
unambiguously verify the asset is the intended resource. Standards like
multihash [\[3\]](#ref3) provide for a wide range of different hash algorithms
and representations. Approaches using merkle trees can turn hashes into
a hashgraphs, allowing an arbitrary number of resources to be
independently verified without revealing even the number of those assets
publicly. These content identifiers can provide robust verifiability no
matter where such resources might be located or retrieved.

Specifically for NFTs, IIDs allow you to

1. Identify individual NFTs as well as their token class

2. Identify resources associated with that NFT

3. Exercise rights related to those resources using cryptography anchored to the NFT

IIDs allow these functions a manner that addresses the privacy
requirements for such references, with flexible support for use cases
that need to make different choices. Our approach offers a robust,
flexible, and capable identifier mechanism for NFTs, and on-chain
assets, of all types.

Use Cases
=========

This specification was designed for Non-Fungible Tokens. NFT-RFC-002
[[4]](#ref4) describes the range of types of tokens as well as several detailed
user stories covered by this work. NFT-RFC-008 [[5]](#ref5) describes how one
might apply IIDs, Verifiable Credentials, and Authorization Capabilities to define,
authorize, issue, use, and sell NFT-based Renewable Energy Certificates
(RECs) according to an REC 2021 standard.

Throughout this document we use the REC2021 use case for examples. In summary:

1. The UN creates a token template for RECs.
2. The UN publishes that token template, resuling in an IID for the new class.
2. The UN uses a WebKMS system so that it can delegate the ability to sign Verifiable
Credentials.
3. The UN defines a vocabulary for Certification Reports and Verification Reports as
Verifiable Credentials
4. The UN delegates the ability to create Verification Reports (with certain constraints)
to known, qualified verifiers.
5. The UN delegates

   a) the ability to create Certification Reports (with certain
constraints) and

   b) the ability to mint REC2021 tokens (with certain constraints)

   to known, qualified certifiers.
6. A renewable energy producer, HydroElec, creates a Project Verified Credential 
describing his project, including the DIDs for its smart electricity meters that verify production.
7. HydroElec gets its project reviewed and approved by a certifier, receiving a 
Certification Report that refers to the HydroElec Project VC by hash reference, as well as 
8. HydroElec builds its project and produces electricity
9. As electricity is produced, Verifiable Credentials are issued by the meters, 
attesting to the production of electricity from renewable sources (evidence).
10. HydroElect gathers the evidence VCs, along with the project and certification VC, a
nd submits them for verification to known, qualified UN REC2020 verifier.
11. The Verifier reviews the provided information and issues a Verification Report 
(as a VC), giving that to HydroElect
12. HydroElect posts all accumulated VCs on a public facing service
13. HydroElect invokes the minting capability, with all associated evidence, to create an
a REC2021 NFT that it owns and controls.

Lifecycle of an NFT
-------------------
The following describes the lifecycle of any on-chain token, and specifically non-fungible tokens.
1. [Define](#Define)
1. [Mint](#Mint)
1. [Use](#Use)
1. [Sell](#Sell)
1. [Buy](#Buy)
1. [Transfer](#Transfer)

# Define

NFT start by some party--any party--defining the nature of the 
NFT. For example, using the approach of the Token Taxonomy Framework [[7]](#ref7), 
decide the base type, the behaviors, and any properties of the NFT. This 
definition must be captured in a format that the underlying chain can interpret.

# Mint
The creator, or a delegated party, may 
# Use
# Sell
# Buy
# Transfer

1.  Define Class (delegation set up)

2.  Delegate (optional) Capability to Mint

3.  Mint Invoke w/ caveats

4.  Use

    a.  Inspect it

    b.  Invoke Services

        i.  Request resources

        ii. Communicate with owner

    c.  Exercise Accorded Rights (with or without additional
        > requirements)

        iii. Bond

        iv. Unbond

        v.  Vote

        vi. See a show

        vii. Decrypt Media

    d.  Delegate Accorded Rights

    e.  Create derivatives

    f.  Collateralize it

    g.  Use on another chain

5.  Offer for sale

6.  Verify Linked Resources

7.  Buy

8.  Burn


Requirements for the IID specification
======================================

This specification MUST achieve the following.

1.  IIDs MUST be conformant with the DID Core syntax for DIDs

2.  IIDs MUST be able to refer to any asset on any chain, on any
    network, on any fork.

3.  IID documents MUST be conformant DID documents in JSON-LD
    representation

4.  IID documents MUST be able to use custom properties in an
    unambiguous manner.

5.  IID documents MUST be able to define their own namespace for
    referring to off-chain assets

6.  IID documents MUST be able to specify how to verify, and optionally
    retrieve, associated resources, revealing neither the number nor
    character of those resources.

7.  IIDs must be usable in an interoperable fashion with emerging
    self-sovereign approaches such as Verifiable Credentials,
    Authorization Capabilities, and Confidential Storage.

8.  IIDs must be recognizable as IIDs by simple examination of the IID
    itself.

9.  IIDs must be usable with existing tooling and infrastructure.

Requirements for IIDs, IID Documents, and IID Methods
=====================================================

The following are requirements for IIDs above and beyond conformance
requirements of DID Core.

10. All IIDs MUST refer to a single on-chain asset, such as a token,
    smart contract, or address.

11. IID documents MUST be conformant DID documents in JSON-LD
    representation.

    All properties used in an IID document must be conformant with
        DID JSON-LD processing rules, including the definition of such
        properties in JSON-LD context files specified by the \@context
        property.

12. IID Methods SHOULD support off-chain creation of identifiers with
    on-chain updates

13. IID Methods SHOULD define one and only one service endpoint

14. IID Methods SHOULD define one and only one Linked Resource

Extensibility
=============

IIDs use two key mechanisms for extensibility, following the DID
Extensibility approach in Section 4.1 of DID Core.

**First**, IID methods may be created for any existing or new blockchain
or distributed system. Each IID method specifies the mechanisms that
allow a DID user to create, read, update, and deactivate IIDs of that
method. There is no registration required; literally anyone can
define an IID method.

**Second**, JSON-LD enables unambiguous use of JSON properties through
the addition or modification of \@context properties. This approach
allows any RDF statement to be losslessly represented in JSON, avoiding
possible confusion between properties with the same name being used
differently by different organizations. Thanks to DID Core, IID
documents using the JSON-LD representation already have a \@context property
with "[https://www.w3.org/ns/did/v1](https://www.w3.org/ns/did/v1)"
as its first value. This specification adds a second @context
property, (its value TBD, but something like
"[https://internft.org/ns/iid/v1](https://internft.org/ns/iid/v1)".
This context value pulls in a JSON-LD context file, stored at that
location, which contains the definitions specific to IIDs.

Like any DID method, any IID Method may add properties in a
decentralized way by creating their own JSON-LD context file, publishing
that online, and adding it as a third \@context, e.g., the context
property for a Cosmos customization of IIDs might be

```
"@context" : [
  "https://www.w3.org/ns/did/v1",
  "https://internft.org/ns/iid/v1",
  "https://cosmos.network/ns/cosmosIid/v1"
]
```

This context value pulls in three JSON-LD contexts, applying them in
order, to unambiguously define all of the properties used in the IID
document.

This allows unambigious extensibility without a central registry of
vocabulary.

New Terminology
===============

1.  **IID References** are DID-URLs with a fragment part, e.g.,
    **did:example:abc#123**. They refer to resources associated with 
    the IID subject in some way, and defined in the IID Document with
    an "id" property matching the fragment term. This reference SHOULD be
    used in RDF statements about IID References (the raw IID should be used 
    in RDF statements about the IID asset).

2.  **IID Resources** are DID-URLs with a path part, e.g.,
    **did:example:abc/123**. They are used to for retrievable
    (online) resources that are associated with the IID subject and
    defined in the LinkedResource property of the IID Document with
    a "path" property and an "id" property, which both match the path term.

3.  **IID Assets** All IID Subjects are the on-chain asset referred to by 
    the IID. The term "IID Asset" is used to refer to the on-chain asset 
    that is the Subject of an IID. Or more succinctly, the DID Subject 
    of an IID is the IID Asset and the IID is used to refer to that asset.
    These terms may be used interchangeably.

## HTTPRange14
By convention, all downloadable linked resources may be referred to by their associated
IID Reference ***did:example:abc#123*** and downloaded using their IID Resource URL
***did:example:abc/123***. 

This is achieved by using the same lexical term for the path 
part in the "path" property and the fragment part in the "id" property.

Thus IIDs avoid the HTTPRange14 problem [[6]](#ref6) of confusing
the same string as a conceptual identifier (as a URI) in RDF statements, and that same
string used to retrieve a specific online resources (as a URL).

New Properties and Values
=========================

1.  **linkedResource** is a new IID document property for specifying
    how to verify, and optionally retrieve, any and all resources
    necessary for the proper function of the on-chain asset. Like
    email attachments, LinkedResources provide for attaching arbitrary
    media to an onchain asset.

2.  **transclude** is a new IID document property for specifying where
    in an IID document to transclude a linked resource. If present, the value 
    of this property MUST be one (or an array of more than one) Linked Resources
    that eventually dereferences to raw JSON-LD object. The properties of that
    JSON-LD object will be injected into the current IID document, replacing
    the transclude property entirely. The properties of the transcluded JSON-LD
    MUST be transformed to their absolute representation using the object's 
    ```@context``` value prior to transclusion. The associated linked resources
    MUST have a ```rel``` value of "extension" and a ```mediaType``` value of
    "application/ld-json"

2.  **extension (a type of Linked Resource)**: A JSON-LD extension of
    the current document. The RDF statements in the extension are to be
    included in the current IID document, where specified by a "transclude"
    property. For example, you might provide additional service
    endpoint definitions in an linked resource. Those endpoints can be verified
    as associated with that IID, but only by those parties who secure
    those definitions through other, privacy respecting means. This
    property standardizes how to verifiably move arbitrary RDF statements out of
    the IID document itself to provide additional security and privacy.

4.  **executableRight (a type of Linked Resource)**: This resource
    is an executable capability that can be invoked by the
    IID owner or its designate, using cryptographic materials defined
    elsewhere in the document.

5.  **assertion (a rel value for a Linked Resource)**: Verifiable credentials,
    verified claims, claim tokens as described in NFT-RFC-008. This
    allows arbitrary, yet verifiable attestations to be made either
    about the asset or about the resources defined by IID references.
    The attributes represented in these claims can be retrieved via the
    NFT interface using a query by example (graph query) mechanism.

6.  **rel (a property of Linked Resource)**: Defines the relationship
    of this resource to the IID asset. Known values include:
    1. "evidence" -- The resource is evidence for the creation of the asset.
    2. "encodedRepresentation" -- The resource is a binary representation of the
    asset, interpretable by compatible software to display or interact with.
    3. "visualRepresentation" -- The resource is a visual representation of the 
    asset

3.  **accordedRight (a type of relationship of Linked Resource)**: Similarly, linked
    resources could specify real-world rights accorded to the IID owner
    or its designate, such as a digital driver's license or a theater
    ticket. The representation framework for such rights must be open
    ended, including both plain text statements of rights, e.g., "The
    controller of this IID is entitled to ...", or more rigorous, and
    computationally evaluatable RDF statements which might describe in
    great detail a range of benefits that accompany the basic rights of
    the token.

7. **DisplayName (a property of Linked Resources)**: gives a brief textual
    label for display.

8. **DisplayDescription (a property of Linked Resources)**: a longer text phrase 
for displaying additional detail about the asset

9. **DisplayIcon (a property of Linked Resources)**: a URL for an image asset
    to use when displaying the asset.


## Linked Resources

The linkedResource property rovides a privacy-enabled way to attach
digital resources to an on-chain asset. An optional property with one or more
array of one or more resource descriptors, it provides the metadata required for
accessing and using that resource, e.g., type of resource, a proof to
verify the resource, and a service endpoint for requesting that
resource.

Resources may be provided in-line or by secure reference. Inline
resources allow appropriate use cases to directly include the resource
itself in the IID Document. In many cases, this is a privacy problem.
However, for some use cases, resources must be specified for
on-chain execution, justifying the added bytes and potential disclosure risk.
The resource descriptor provides for a flexible representation of
various mime types, compression, and encoding, as befitting the use.

This approach allows token owners to manage privacy in three key ways:

1.  Avoids posting potentially sensitive information on-chain and hence,
    in an unavoidably public and irrevocable manner.

2.  Provides for a service endpoint that can apply appropriate privacy
    and security checks before revealing information.

3.  The hash graph resource descriptor type obscures not only the
    content of the linked resource, but also the quantity.

Resources may be secured by specifying a proofType of hash or hashgraph.
A hashgraph uses a merkle tree of hashes for external content associated
with this asset. A resource descriptor of this type obscures both the
type and the number of such resources, while allowing each such resource
to be verifiably associated. It also provides for privacy-respecting
verification of complete disclosure. Anyone who needs to prove they have
all of the linked resources can compare their own hash graph of
resources with that stored in the IID Document. Note that this
anti-censorship technique requires a verifier to discover the type and
nature of those resources on their own.

Proposed properties for resource descriptors in the LinkedResource
property:
```javascript
{ 
    "linkedResource" : [{

    "path" (optional): // fully qualified IID Resource ID for this resource, e.g., did:example:abc/myResource.png,

    "id" (optional): // fully qualified IID Reference ID for this resource, e.g., did:example:abc#myResource.png, Optional

    "rel" (optional): // the relationship of this resource to the IID Asset

    "type" : "nft:ResourceDescriptor", // The JSON-LD type of this resource

    "proofType" (optional) : "hash" | "hashgraph", 

    "proof" (optional): hash | hashgraph,

    "resourceFormat": "media type",

    "encoding" : "native" | "multibase" | "string",

    "compression": "gzip" | "none",

    "encryption" : [open ended for arbitrary extensibility],

    "endpoint" (optional): url,

    "resource" (optional): a representation of the resource for inline
distribution

}]
}
```

# New Service Types

## POLYMORPHIC MEDIATOR
A polymorphic mediator is an endpoint that can act as any number of services,
depending on how it is called, for any number of people. This allows a single
endpoint to be specified for arbitrary sets of services with excellent herd
privacy characteristics. The best practice for such a mediator is to act as a
reverse-proxy rather than as a redirect: the response should be sent directly
through the mediator rather than redirecting the request to a different server.

As a mediator, this service provides a secret mapping between the public endpoint
and the eventual actual service for any number of parties. The responses provided 
by the mediator are *signed* by the IID controller and optionally encrypted for the 
recipient by the IID controller, ensuring that the mediator can neither tamper with
nor even see the response (when encrypted). It is anticipated that individuals 
will pay mediators they trust to get an extra level of privacy by mixing their 
endpoint transactions with others.

As a polymorphic endpoint, the mediator is configurable for handling any number of 
services, such as 
* Negotiator Endpoint -- A service for negotiating mutually agreeable communications
channels, preferably using private set intersection. The output of negotiation is
a communication channel and whatever credentials may be needed to access it.
* Confidential Storage -- A secure data storage endpoint using end-to-end encryption
and zCaps for authorization https://identity.foundation/confidential-storage
* Authorization Server -- An UMA or GNAP style authorization server endpoint
* Resource Server -- A simple http server such as might host a blog or company site
* An messaging service -- A messaging service using a particular
protocol such as Signal, SMTP, XMPP, or IRC.

The API of the polymorphic mediator is TBD. This work is in early stages.

IID Syntax 
===========

Same as DID Syntax [[1]](#ref1)

```abnf
 iid = did                                           
                                                     
 did = "did:" method-name ":" method-specific-id 
                                                     
 method-name = 1*method-char                        
                                                     
 method-char = %x61-7A / DIGIT                       
                                                     
 method-specific-id = *( *idchar ":" ) 1*idchar 
                                                     
 idchar = ALPHA / DIGIT / "." / "-" / "_"     
```

IID References and IID Resources are DID-URLs (or equivalently, IID-URLs), with
additional detail from RFC3986 [[2]](#ref2):
```abnf
iid-url = did-url

did-url = did path-abempty [ "?" query ] [ "#" fragment ]

path-abempty  = *( "/" segment )   ; begins with "/" or is empty

query       = *( pchar / "/" / "?" )

fragment    = *( pchar / "/" / "?" )

pchar         = unreserved / pct-encoded / sub-delims / ":" / "@"
```

The IID Architecture
====================

IIDs as DIDs
------------

Decentralized Identifiers (DIDs) are a standards-track specification
under development at the World Wide Web Consortium.
[[https://www.w3.org/TR/did-core/]](https://www.w3.org/TR/did-core/)
They are \"a new type of globally unique identifier designed to enable
individuals and organizations to generate our own identifiers using
systems we trust, and to prove control of those identifiers
(authenticate) using cryptographic proofs (for example, digital
signatures).\"

DIDs enable verifiable, decentralized digital identity. They were
inspired by blockchain based approaches for \"identity\", using an
RFC3986 compatible syntax. As such DIDs *are* URIs and are designed to
work within existing web frameworks.

DID-URLs support additional **path** (/directory/file), **query**
(?query=value), and **fragment** (\#fragment)parts. Fragments are
commonly used to refer to elements within a DID document.

DIDs work because of two structural design choices.

First, each DID specifies a DID Method, which defines how a DID consumer
might perform Create, Read, Update, and Deactivate operations. Different
types of DIDs may have different Methods, and each Method may define
unique approaches for those functions. This allows DIDs that anchor to
Bitcoin and Ethereum, as well as bespoke fit-for-purpose ledgers such as
Veres One or Sovrin. DID Methods \*may\* be registered in a common
registry for increased interoperability, but such registration is not
required; it is merely a convenience.

Second, every DID resolves to a DID document, which contains all the
metadata required for interacting securely with the DID Subject.

-   Public Keys

-   Verification Relationships

    -   Assertion Method

    -   Authentication Method

-   Service endpoints

DID document state is managed by DID Registries; many are blockchains,
but alternatives such as did:peer, did:git, and did:key do not rely on
blockchains at all. Methods like did:key and did:btcr 
deterministically create DID documents based on rules in their
specification; no actual DID document is stored anywhere. A more recent
class of DIDs, including did:v1, did:ethr, and did:ion allow the
creation of DIDs without registration, relying on the registries purely
for updates; did resolution for these methods checks the registry for
any updates and if there are none, use a deterministic algorithm to
generate a DID document or a cryptographic verification of an initial
DID document communicated through alternate channels.

It is this indirection of DID documents that allows key rotation without
explicit notification to all parties. It is the open-ended DID Method
architecture that allows for future proofed innovation.

Third, DID Methods with publicly inspectable registries (where DID
document state is maintained), such as blockchains, may also provide for
auditability, and with some effort, even reversibility of changes in
case of inappropriate transactions. These advanced features remain areas
of active development.

Fourth, DID documents are defined using an abstract data model, allowing
any number of serializations, with initial support for JSON and JSON-LD
serializations. CBOR and CBOR-LD are also highly anticipated for their
ability to dramatically reduce the size of DID documents. Other
serializations are also possible, including Protobuf.

Finally, although it is sometimes useful to think of DIDs as an
architecture for decentralized identity, the functional mechanism behind DIDs
doesn't actually provide for identification. That is, DIDs are used to refer
to Subjects, but do not themselves perform identification.

Instead, DIDs provide a means to verify that a given identifier is
appropriately involved in a cryptographic operation such as authentication or
assertions. As such, DIDs are a verification framework which IIDs use 
to provide verification related to a particular on-chain asset. Verification 
Relationships and Verification Methods, described elsewhere, define the range 
of interactions that can be verified for a given DID.


This specification leverages DIDs for all of those benefits by defining
IIDs as profile of DIDs. IIDs **are** DIDs. IID documents **are** DID
documents. IID Methods **are** DID Methods. Each namespace for IIDs,
e.g., Cosmos, Polkadot, ERC1155, is defined by an IID method that
specifies how to perform create, read, update, and deactivate operations
on IIDs. This IID family of DID Methods share a common purpose and
leverage shared property definitions for improved cross-chain
interoperability. By design, an IID from any chain can be read, used,
and operated on from any chain thanks to IID-specific properties and
common DID properties. IIDs may also be used by traditional DID software
for standard DID functionality such as authentication and verification.

Because DIDs are URIs, IIDs are also URIs, making IIDs natively
compliant with existing RFC3986 compliant libraries, including those
used for RDF and the World Wide Web.

Consider the following example minimum DID document from DID Core:

EXAMPLE 1: A minimal DID document (JSON-LD)
----

```json
{

"@context": "https://www.w3.org/ns/did/v1",

"id": "did:example:abc123",

"authentication": [{

  "id": "did:example:abc123#keys-1",

  "type": "Ed25519VerificationKey2020",

  "controller": "did:example:abc123",

  "publicKeyMultibase": "zH3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"

  }]

}
```

This minimal DID document is fully conformant with the specification and
includes a single verification relationship and method: how to
authenticate on behalf of the DID Subject.

It is useful to not that Verification Methods can be anything\*, e.g.,
ed25519, secp256k, etc.

An equivalent minimal IID document would be

EXAMPLE 2: A minimal IID document
----
```json
{

"@context": ["https://www.w3.org/ns/did/v1",

  "https://internft.org/ns/iid/v1"],

"id": "did:example:abc123",

"authentication": [{

  "id": "did:example:abc123i#keys-1",

  "type": "Ed25519VerificationKey2020",

  "controller": "did:example:abc123",

  "publicKeyMultibase": "zH3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"

  }]

}
```

Like Example 1, this minimal IID document provides for
cryptographic authentication on behalf of the IID Asset. The second 
context entry pulls in the IID JSON-LD context that indicates this 
DID document is an IID document. Literally, it means that the property 
definitions from the IID context---which are defined in this 
specification---apply to the properties of this DID document, which 
makes it an IID document.

IID subjects are always on-chain asset like Non-Fungible Tokens.
Authenticating on a token\'s behalf is taken to indicate
proof-of-ownership. Since most on-chain assets already employ some form
of cryptographic proof-of-control for exercising ownership rights, an
IID document of this kind should be readily producible for just about
any asset on any blockchain (or at least those assets which have a
cryptographic proof-of-control). It may be necessary to provide a new
type of verification method if the underlying chain is using an
innovative cryptographic proof, but DID documents are extensible for
precisely this flexibility.

In this example, the CRUD operations of the DID are managed by
method-specific means based on Ed25519. The on-chain state---referred to
as the \"registry\" in DID Core---can be inspected to deterministically
generate this IID document. Different registries provide different ways
to inspect that state and different rules for deterministic generation.
This variability is handled in the individual IID methods based on
particular registries: each method describes how to work with its
registry. In many cases, there is no need to store a fully formed DID
document---which makes DIDs particularly well suited to existing
blockchain infrastructure: in many cases, no changes to the underlying
chain mechanics are necessary.

EXAMPLE 3: A minimal, privacy-preserving IID document
----
```json
{

  "@context": ["https://www.w3.org/ns/did/v1",

    "https://internft.org/ns/iid/v1"],

  "id": "did:example:abc123",

  "authentication": [{

    "id": "did:example:abc123i#keys-1",

    "type": "Ed25519VerificationKey2020",

    "controller": "did:example:abc123",

    "publicKeyMultibase": "zH3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"

  }],

  "service": [{

    "id":"did:example:abc123#mediator",

    "type": "polymorphicMediator2021",

    "serviceEndpoint": "http://8zd335ae47dp89pd.onion/iid/mediator/ did:example:abc123"

  }],

"linkedResource" : [{

    "id": "did:ixo:abc123#resourceHashgraph",

    "path": "did:ixo:abc123/resourceHashgraph",

    "type": "hashgraph",
  
    "proof": "afybeiemxf5abjwjbikoz4mcb3a3dla6ual3jsgpdr4cjr3oz",

    "endpoint" : "did:example:abc123?service=mediator"

  }]

}
```

There are four privacy-preserving elements in this privacy-preserving
minimal IID document.

**NOTE: From a privacy perspective, it might be better to make these 
properties mandatory for IIDs
to maximize herd privacy. However, the current language of "SHOULD"
for these requirements allows IID creators to violate herd privacy
when they deem it appropriate for their use case. It is discouraged,
but allowed. This deserves further discussion.**

**First**, there is one and only one service endpoint, which points to a
shared, polymorphic mediator, as described in Section 10.6 Service
Privacy from the DID Core Specification
[[https://w3c.github.io/did-core/\#service-privacy]](https://w3c.github.io/did-core/#service-privacy)

Service endpoints are optional, but to support herd privacy, it is a
recommended practice to use one, and only one service endpoint, which is
a SHOULD requirement for IIDs. For maximum privacy, this specification
further recommends that the service endpoint specifies a Tor address for
a polymorphic service capable for providing a number of functions such
as a negotiator, mediator, or confidential storage.

> *It is the goal of herd privacy to ensure that the nature of specific
> subjects is obscured by the population of the whole. To maximize herd
> privacy, implementers need to rely on one --- and only one --- service
> endpoint, with that endpoint providing a proxy or mediator service
> that the controller is willing to depend on to protect such
> associations and that blinds requests to the ultimate service.*

This service endpoint---using an API which is still under
development---is capable of acting as any number of services, all in a
trusted, privacy preserving manner.

**Second**, that service endpoint is a Tor endpoint, which provides
enhanced network security, mitigating the ability for network observers
to detect attempts to access that endpoint. The underlying service is
just like any other web service; using Tor obfuscates the networking
layer without changing the service or API that runs over that secure
connection. In some cases, this may also provide geographic shielding.

**Third**, there is one, and only one, linked resource entry which is
capable of verifying an unknown number of associated resources. The
entry type of "hashgraph" means that the proof is a Merkle tree of
hashes of the underlying resources. Anyone who gathers the appropriate
resources can independently verify their completeness and authenticity
by comparing the hashgraph of the combined resources with the proof
property in the service endpoint definition. Anyone considering buying
an NFT can be cryptographically assured they have all the resources they
need to confirm the NFT is what they believe it to be.

For herd privacy, it is preferred that all IIDs use one, and only one,
service endpoint and one, and only one, linked resource. In cases where
there is no appropriate service endpoint, it is still preferable to
point to a mediator; to support that, we encourage a multitude of
publicly accessible mediator services offering a free "null response"
service where such "null response" is indistinguishable from a failed
access from lack of authorization.

NOTE: It's ok to have multiple resources listed, but it is less
preferred.

**Fourth**, the single linked resource property lists its endpoint as
the IID's single service endpoint, using a properly formed DID-URL with
a service parameter. This pattern allows every resource to use the same
endpoint without duplicating endpoint URLs even when specifying multiple
linked resources. This pattern encourages polymorphic mediators, which
improves overall privacy across the IID ecosystem.

# Auxilary Technologies
The following technologies comprise, with IIDs, a coherent architecture 
for decentralized control of digital assets.

## Verifiable Credentials

## Executable Rights

### Delegation, Authorization, and Caveats

### Authorization Capabilities

### Secure ECMAScript

## Confidential Storage

## Wallets


Privacy Considerations
======================
Section TBD.

How to create an IID Method
===========================
Section TBD.

Terminology
===========

1.  DIDs

2.  DID-URLs

3.  DID documents

4.  Resolution

5.  Dereference

References
==========

<a name="ref1">[1]</a> Decentralized Identifiers (DIDs) v1.0. World Wide Web Consortium.
Online at
[[https://www.w3.org/TR/did-core/]](https://www.w3.org/TR/did-core/).
Accessed February 15, 2021.

<a id="ref2">[2]</a>  URIs RFC 3986

<a id="ref3">[3]</a>  Multihash

<a id="ref4">[4]</a>  NFT-RFC-002

<a id="ref5">[5]</a>  NFT-RFC-008

<a id="ref6">[6]</a>  HTTP Range 14

<a id="ref7">[7]</a>  Token Taxonomy Framework https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/main/token-taxonomy.md 


NOTES
=====

(not for RFC publication)

Future Work

Addressing how to deal with cross-chain transfers of IIDs. New chain
means a new identifier, but the link to the original NFT is preserved,
on both chains.


Open question: we need good examples for Accorded Rights and Executable Rights.
I think "accorded right" is a rel value of an linked resource rather than a type
of linked resource.
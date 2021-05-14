---
nft-rfc: 9
title: Interchain Identifiers
stage: draft
category: NFT/METADATA
authors: Joe Andrieu @jandrieu Shaun Conway @ig-shaun
created: 2021-03-18
modified: 2021-04-14
---


# Abstract

Interchain Identifiers (IIDs) are a family of Decentralized Identifier methods which are purpose-designed to identify, refer to, and interact with digital assets within blockchain namespaces.

The IID specification builds on the Decentralized Identifier (DID) core specification from the World Wide Web Consortium (W3C) [1]. IIDs are fully conformant DIDs and therefore are DIDs. IID Documents are DID documents. Unlike DIDs, IIDs only reference on-chain assets&mdash;which we will refer to as tokens&mdash;but should be taken as any type of tokens, such as NFTs, fungible tokens, tokenized namespace records, or other on-chain assets.

By restricting IIDs to on-chain assets, we create a new class of identifier uniquely suited to the requirements of tokens and other chain-native components. IID methods can be developed for any compatible blockchain, making them suitable for interoperable representations of tokens (and the cryptography that secures those tokens) regardless of the underlying chain.

IIDs also introduce a few new features&mdash;conformant extensions to the DID Core specification&mdash;that provide for privacy-respecting options for the full range of expected token functionality, including Linked Resources, On-chain Service Endpoints, and Accorded Rights.

DID Methods which conform to the IID specification resolve to DID Document representing how to securely interact with a uniquely identified digital asset, within a unique blockchain namespace. Because IIDs are DIDs, software applications that are conformant with the W3C specification will be able to inter-operate with IIDs and IID documents, although some IID-specific features may require additional tooling.



Introduction
============

Decentralized Identifiers (DIDs) are a new Web standard for secure identifiers without dependency on a trusted third party. DIDs are used to reference ANY subject, including people, organizations, physical locations, and digital assets.

IIDs define a family of DID methods used tolocate on-chain assets and their associated resourcess, allowing the asset to be addressed and used across namespaces: from the web, from another chain, or from any DID compliant wallet or application.

IID Methods are the secret to customizing DIDs to meet the need for secure interactions with any on-chain assets.

## Built on URIs
IIDs build on a foundation of Internet identifiers, dating back to Uniform Resource Locators and Uniform Resource Identifiers [[2]](#ref2), which are the
foundation of the World Wide Web. 

URIs allow for different mechanisms to be used for interpreting and applying the syntax of the identifier. 

For example, the URL ```http://example.com``` specifies a web-based resource that can be retrieved using the hypertext transfer protocol (http).

Whereas the URL ```mailto:joe@example.com``` specifies a resource that can receive email messages using the SMTP protocol.

Decentralized Identifiers (DIDs) build on URIs and URLs to provide a new class of URIs which afford secure interaction with the controller of that identifier, without reliance on a
trusted third-party.

## DID and IID Documents

This is a DID:
```
did:example:abc123
```
That DID (if it weren't just an example) would resolve to a DID Document describing how to securely interact with the controller of that DID. Example documents follow.

All DIDs *resolve* to their associated **DID Document**, which contain the verification methods and relationships and the service endpoints that secure interaction with the controller of the asset.

**Verification Methods**, such a public key, may be used to establish verification relationships for the purpose of authentication, assertion, capability delegation, or capability
invocation.

A standard format DID Document object defines these **verification relationships**, together with the specific cryptographic method associated with each verification purpose.

DID-URLs extend the base DID syntax to support ```/path```, ```?query```, and ```#fragment``` parts. 
IIDs use the ```/path``` and ```#fragment``` parts of URLs for IID References and IID Resources.

The relationship between IIDs and DIDs is further described in the [IIDs as DIDs](#IIDs-as-DIDs) section.

### Tokenized digital assets
The IID specification defines how tokenized digital assets can be:
1. Identified as unique digital assets of a specific type and class of tokens.
2. Linked to verifiable on-chain and off-chain resources.
3. Accorded rights in relation to both the token and its linked resources. Including machine-executable rights, which may be issued and delegated off-chain using a mechanism such as Authorization Capabilities (zCaps). 
For accessing, invoking and transacting with both on-chain or off-chain services.
4. Afforded privacy in relation to the token's metadata. Including what the token represents, information abourt its linked resources, and the services which can be invoked.
5. Transferred with verifiable provenance across registry systems. 

# Use Cases

The IID specification was primarily designed to address the use-case requirements for Non-Fungible Tokens (NFT), which are described in NFT-RFC-002.
[[4]](#ref4). However, this specification is applicable to all types and classes of tokens, as well as other on-chain digital assets.

## Renewable Energy Certificate NFTs
The specific use-case of tokenizing Renewable Energy Certificates (RECs), as described in NFT-RFC-008 [[5]](#ref5), will be used to describe how IIDs are implemented 
to define a class of tokens (REC-2021).

This use case describes how a centralized authority like the UN Climate Change Agency can use a decentralized token platform to issue  digital Renewable Energy Certificates as tradeable NFTs.

Operationalized within a secure system for certifying a renewable energy project to create renewable energy production claims from smart meters. These claims, together with the project's credentials, are submitted for evaluation by an authorized verification agent. 
Who has the necessary digital credentials and authorization, delegated from the UNCCC, to issue a verification report and to pass on a delegated authorization to the 
renewable energy producer. For the producer to invoke minting of a UNCCC-standard Renewable Energy Certificate NFT. Which includes as token metadata the producer's credentials, 
claims and verification report, as Linked Resources. Together with Accorded Rights, in the form of a delegated Authorization Capability, associated with the token 
–such as the right to mint derivative fungible tokens which each represent a KWh of renewable energy.
This use-case demonstrates how IIDs enable the family of related W3C specifications for Decentralized Identifiers, Verifiable Credentials and Authorization Capabilities (zCaps) 
can be used to tokenize real-world assets. In a secure and privacy-preserving way that makes these assets verifiable, information-rich and interoperable within a broader 
universe of linked-data and DID applications.   

These are the steps for minting a Renewable Energy Certificate NFT: 
1. The UN Climate Change Agency (UNFCCC):
   a) Creates a token template for the REC2021 class of NFTs, which specifies the behaviors and properties of this token class.
   b) Publishes the token class template with a unique IID.
   c) Defines a vocabulary for representing Certification Reports and Verification Reports as Verifiable Credentials (VCs).
   d) Issues and then delegates an Authorization Capability for qualified project certifiers, who have the necessary credentials, to issue Certification Report VCs.
   e) Delegates an Authorization Capability (with specified constraints) for qualified Verification Agents, who have the necessary credentials, to:
      * Issue Certification Report VCs.
      * Mint REC2021 NFTs.
2. A Renewable Energy Producer, HydroElec, self-issues a Project Verifiable Credential to identify and describe their project. This includes an array of DIDs for each smart electricity meter that will record verifiable claims of KWh renewable energy produced.
3. A Project Certifier, who has the necessary Verifiable Credentials and Authorization Capability delegated from the UNCCCC, evaluates HydroElec's Project VC to issue a Verifiable Credential which identifies HydroElec's project as a UNCCC-Certified Renewable Energy Project. 
4. HydroElec builds its project and starts generating renewable energy. Identified smart meters issue verifiable claims attesting to the KWh of energy produced (with evidence).
5. HydroElec submits these claims, together with its Project VC and Project Certification VC, to the UNCCC-certified and authorized REC2020 Verification Agent.
6. The Verification Agent evaluates HydroElec's credentials together its collection of verifiable claims and evidence. Then issues a Verification Report VC to HydroElec.
7. The Verification Agent delegates to HydroElec the Authorization Capability to mint a REC2021 NFT.
8. HydroElec uses a confidential data store service to make its collection of Verifiable Credentials and verifiable claims available as resources.
9. HydroElec uses its delegated Authorization Capability to invoke the service of a blockchain to mint a REC2021 NFT. Which includes as metadata the Linked Resources and Service Endpoint where these can be located. 
10. HydroElec owns and controls this NFT, with the capability to sell and transfer the token. Or invoke other services provided by the blockchain –such as minting derivative fungible tokens which represent the KWh units of renewable energy produced.
11. Energy Purchasers buy the derivative KWh Tokens from HydroElec to exchange for energy supply. They are authorized by HydroElec to access and inspect the credentials, claims evidence and verification report linked resources, which are made available through the specified confidential data store service end-point.
12. HydroElec, after selling all their KWh Tokens, invokes the service of the blockchain to retire the REC NFT. 


Requirements for the IID specification
======================================

Implementations of this specification must achieve the following:

1.  For interoperability, IIDs MUST be conformant with the DID Core syntax for DIDs

2.  For discoverability, IIDs MUST be able to refer to any asset on any chain, on any network, on any fork.

3.  For resolvability, IID documents MUST be conformant DID documents in JSON-LD representation

4.  For composability, IID documents MUST be able to use custom properties in an unambiguous manner.

5.  For dereferencing, IID documents MUST be able to define their own namespace for referring to off-chain assets //??

6.  For privacy, IID documents MUST be able to specify how to verify, and optionally retrieve Linked Resources, without revealing the number or characteristics of the resources.
7.  For self-sovereignty, IIDs must be compatible with standards such as Verifiable Credentials, Authorization Capabilities, and Confidential Storage.
8.  For applicability, IIDs must be recognizable as an IID, simply by examining its syntax. //??
9.  For usability, IIDs must be compatible with existing DID tooling and infrastructure.

Requirements for IIDs, IID Documents, and IID Methods
=====================================================

In addition to conforming with the requirements for DIDs:

10. All IIDs MUST refer to a single on-chain asset, such as a token, smart contract, or account wallet.

11. IID documents MUST be conformant DID documents in JSON-LD representation.
        All properties used in an IID document must be conformant with
        DID JSON-LD processing rules, including the definition of such
        properties in JSON-LD context files specified by the \@context
        property.

12. IID Methods SHOULD support off-chain creation of identifiers with on-chain updates.

13. IID Methods SHOULD define one and only one service endpoint.

14. IID Methods SHOULD define one and only one Linked Resource.

Extensibility
=============

IIDs use two mechanisms for extensibility, following the DID Extensibility approach described in Section 4.1 of the DID Core Specification.

**First**, IID methods MAY be created for any existing or new blockchain
or distributed system. Each IID method MUST specify the mechanisms for a DID user
to create, read, update, and deactivate IIDs of that method. 
There is no technological requirements to register IID Methods, so central authority or permission should not be required to
define an IID method.

**Second**, JSON-LD enables unambiguous use of JSON properties through
the addition or modification of \@context properties. This approach
allows any RDF statement to be losslessly represented in JSON. Avoiding
potential confusion between properties with the same name being used
differently by different organizations. 
Following the DID Core specification, IID documents which implement the JSON-LD representation already have a \@context property "[https://www.w3.org/ns/did/v1](https://www.w3.org/ns/did/v1)"
as the first value. The IID specification adds a second @context
property, (its value TBD, but something like
"[https://internft.org/ns/iid/v1](https://internft.org/ns/iid/v1)".
This context value pulls in a JSON-LD context file, stored at the specified
location, which contains the definitions specific to IIDs.

Like any DID method, any IID Method may add properties in a
decentralized way, by creating their own JSON-LD context file, publishing
this online, and adding it as a third \@context. 
For example: the context property for a Cosmos customization of IIDs could be

```
"@context" : [
  "https://www.w3.org/ns/did/v1",
  "https://internft.org/ns/iid/v1",
  "https://cosmos.network/ns/cosmosIid/v1"
]
```

This context value pulls in three JSON-LD contexts. Applying them in sequential
order, to unambiguously define all of the properties used in the IID
document.

This allows unambigious extensibility, without the need for a centralized registry of
DID methods and vocabulary.

New Terminology
===============

1.  **IID References** are DID-URLs with a fragment part, e.g.,
    **did:example:abc#123**. These refer to resources which are associated with 
    the IID subject in some way and are defined in the IID Document with
    an "id" property matching the fragment term. This reference SHOULD be
    used in RDF statements about IID References (the raw IID should be used 
    in RDF statements about the IID asset).

2.  **IID Linked Resources** are DID-URLs with a path part, e.g.,
    **did:example:abc/123**. These are used to retrieve
    (online) resources linked to the on-chain asset. Which are
    defined in the `LinkedResources` property of the IID Document using
    a "path" property and an "id" property. Both of which match the path term. //??

3.  **IID Assets** All IIDs refer to on-chain assets. The DID Subject 
    of an IID is the IID Asset. These terms may be used interchangeably.

## HTTPRange14
By convention, all downloadable linked resources may be referred to by their associated
IID Reference ***did:example:abc#123*** and downloaded using their IID Resource URL
***did:example:abc/123***. 

This is achieved by using the same lexical term for the path  part in the "path" property and the fragment part in the "id" property.

By taking this approach, IIDs avoid the HTTPRange14 problem [[6]](#ref6) by not confusing
the same string as a conceptual identifier (as a URI) in RDF statements, and that same
string used to retrieve a specific online resources (as a URL).

New Properties and Values
=========================

1.  **linkedResource** is a new IID document property for specifying
    how to verify, and optionally retrieve, any and all resources
    necessary for the proper functioning of the on-chain asset. Like
    email attachments, LinkedResources provide for attaching arbitrary
    media to an onchain asset.

2.  **transclude** is a new IID document property for specifying where
    in an IID document to transclude a linked resource. If present, the value 
    of this property MUST be one (or an array of more than one) Linked Resources
    that eventually dereferences to a raw JSON-LD object. The properties of that
    JSON-LD object will be injected into the current IID document, replacing
    the transclude property entirely. The properties of the transcluded JSON-LD
    MUST be transformed to their absolute representation using the object's 
    ```@context``` value prior to transclusion. The associated linked resources
    MUST have a ```rel``` value of "extension" and a ```mediaType``` value of
    "application/ld-json"

2.  **extension (a type of Linked Resource)**: A JSON-LD extension of
    the current document. The RDF statements in the extension are to be
    included in the current IID document, where specified by a "transclude"
    property. For example, additional service
    endpoint definitions may be added in a linked resource. 
    These endpoints can be verified as being associated with the IID. But only by those parties who secure
    the definitions through other privacy respecting mechanisms. This
    property standardizes how to verifiably move arbitrary RDF statements outside of
    the IID document context, to provide additional security and privacy.

4.  **executableRight (a type of Linked Resource)**: This resource
    is a machine-executable capability that can be invoked by the
    IID owner or its delegate, using cryptographic materials defined
    elsewhere in the IID document Verification Methods property.

5.  **assertion (a rel value for a Linked Resource)**: Verifiable credentials,
    verified claims, claim tokens as described in NFT-RFC-008. This
    allows arbitrary, yet verifiable attestations to be made either
    about the asset or about the resources defined by IID references.
    The attributes represented in these claims can be retrieved through the
    token interface using a Query by Example (graph query) mechanism.

6.  **rel (a property of Linked Resource)**: Defines the relationship
    of this resource to the IID asset. Known values include:
    1. "evidence" -- The resource is evidence for the creation of the asset.
    2. "encodedRepresentation" -- The resource is a binary representation of the
    asset, interpretable by compatible software to display or interact with.
    3. "visualRepresentation" -- The resource is a visual representation of the 
    asset

3.  **accordedRight (a type of relationship to a Linked Resource)**: 
    Specifies the rights accorded to the IID owner, or its deligate, 
    which may be executed by physical-world institutions or processes.
    Such as a digital driver's license according certain rights to drive, 
    or a theater ticket according access to a show. 
    The representation framework for such rights must be non-prescriptive, 
    including both plain text statements of rights, e.g., "The
    controller of this IID is entitled to ...", or more rigorous and
    computationally evaluatable RDF statements, which might describe in
    great detail a range of benefits that accompany the basic rights of
    the token.

7. **DisplayName (a property of Linked Resources)**: gives a brief textual
    label for display.

8. **DisplayDescription (a property of Linked Resources)**: a longer text phrase 
for displaying additional detail about the asset

9. **DisplayIcon (a property of Linked Resources)**: a URL for an image asset
    to use when displaying the asset.


## Linked Resources

The `linkedResource` property provides a privacy-enabled way to attach
digital resources to an on-chain asset. This is an optional property which
may contain one or more resource descriptors in array.
This property provides the metadata required for
accessing and using the specified resource, such as: the type of resource, a proof to
verify the resource, and a service endpoint for requesting and retrieving the
resource.

Resources may be provided in-line or by secure reference. Inline
resources are appropriate only for use cases that need to directly include the resource
in the IID Document. In many cases, this is a privacy problem.
However, for some use cases, resources must be specified for
on-chain execution, which justifies the added bytes and potential disclosure risk.
The resource descriptor provides for a flexible representation of
various mime types, compression, and encoding, as required for the use.

This approach allows token owners to manage privacy in three key ways:

1.  Avoids posting potentially sensitive information on-chain
    in an unavoidably public and irrevocable manner.

2.  Provides a service endpoint that can apply appropriate privacy
    and security checks before revealing information.

3.  The hashgraph resource descriptor type obscures not only the
    content of the linked resource, but also the quantity of resource objects.

Resources may be secured by specifying a `proofType` of hash or hashgraph.
A hashgraph uses a merkle tree of hashes for external content associated
with this asset. A resource descriptor of this type obscures both the
type and the number of such resources, while allowing each such resource
to be verifiably linked to the asset. It also provides for privacy-respecting
verification of complete disclosure. Anyone who needs to prove they have
all of the linked resources can compare their own hash graph of
resources with the value stored in the IID Document. Note this
anti-censorship technique requires a verifier to discover the type and
nature of those resources on their own.

Proposed properties for resource descriptors in the `LinkedResource`
property:
```javascript
{ 
    "linkedResource" : [{

    "path" (optional): // IID Resource path for this resource in the asset namespace, e.g., /myResource.png

    "id" (optional): // IID Reference ID for this resource, e.g., #myResource.png

    "rel" (optional): // the relationship of this resource to the IID Asset

    "type" : "nft:ResourceDescriptor", // The JSON-LD type of this resource

    "proof" : [              // an array of proofs, any of which may be used
      {
        "type" (optional) : "hash" | "hashgraph" | "hashset" // the form of proof used to verify the resource as authentic
        "stage" (optional) : "raw" | "compressed" | "encrypted" | "encoded" // the 
        "value" (optional): hash | hashgraph | hashset, // the actual proof for this particular resource
      }], 
    "resourceFormat": media type, // the IANA media-type of the linked resource

    "compression" (optional): "gzip" | "none", // the compression (performed on the raw resource) of an inline resource

    "encryption" : [open ended for arbitrary extensibility], // the encryption technique applied after compression and before encoding

    "encoding" (optional) : "native" | "multibase" | "string", // the encoding (after compression and encryption) of an inline resource; "native" means the inline resource is native JSON-LD with neither compression nor encryption

    "endpoint" (optional): url, // a URL at which this resource can be retrieved before decrypting and decrompressing

    "resource" (optional): "..." a representation of the resource for inline
distribution, encoded as per "encoding", then compre

}]
}
```

# New Service Types

## POLYMORPHIC MEDIATOR
A polymorphic mediator is an endpoint that can act on behlalf of any number of services,
depending on how it is called, for any number of people. This allows a single
endpoint to be specified for arbitrary sets of services with excellent herd
privacy characteristics. The best practice for such a mediator is to act as a
reverse-proxy, rather than as a redirect: the response should be sent directly
through the mediator rather than redirecting the request to a different server.

As a mediator, this service provides a secret mapping between the public endpoint
and the eventual actual service for any number of parties. The responses provided 
by the mediator are *signed* by the IID controller and optionally encrypted for the 
recipient by the IID controller, ensuring that the mediator can neither tamper with
nor even see the response (when encrypted). It is anticipated that individuals 
will pay mediators they trust to get an extra level of privacy by mixing their 
endpoint transactions with others.

As a polymorphic endpoint, the mediator is configurable for handling any number of 
services, such as: 
* Negotiator Endpoint: A service for negotiating mutually agreeable communications
channels, preferably using private set intersection. The output of negotiation is
a communication channel and whatever credentials may be needed to access it.
* Confidential Storage: A secure data storage endpoint using end-to-end encryption
and zCaps for authorization https://identity.foundation/confidential-storage
* Authorization Server: An UMA or GNAP style authorization server endpoint
* Resource Server: A simple http server such as might host a blog or company site
* An messaging service: A messaging service using a particular
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
RFC3986 compatible syntax. As such DIDs *are* URIs designed to
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

DID document state is managed by DID Registries; many of which are blockchains,
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
architecture that allows for future-proofed innovation.

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
specifies how to perform the create, read, update, and deactivate operations
for IIDs. This IID family of DID Methods share a common purpose and
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

IID subjects are always on-chain assets, such as Non-Fungible Tokens.
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
generate the IID document. Different registries provide their own specific ways
to inspect that state and different rules for deterministically generating IIDs.
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

**NOTE: From a privacy perspective, it might be preferable to make the following
elements mandatory for IIDs to maximize herd privacy. However,
the current language of "SHOULD" for these requirements allows IID creators
to trade off herd privacy when deemed appropriate for their use case.
It is discouraged, but allowed. This deserves further discussion.**

**First**, there is one and only one service endpoint, which points to a
shared, polymorphic mediator, as described in Section 10.6 Service
Privacy from the DID Core Specification
[[https://w3c.github.io/did-core/\#service-privacy]](https://w3c.github.io/did-core/#service-privacy)

Service endpoints are optional. But to support herd privacy, it is a
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

**Second**, use a service endpoint that is a Tor endpoint, which provides
enhanced network security, mitigating the ability for network observers
to detect attempts to access that endpoint. The underlying service is
just like any other web service. Using Tor obfuscates the networking
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
service endpoint and one, and only one, Linked Resource. In cases where
there is no appropriate service endpoint, it is still preferable to
point to a mediator. To support this, we encourage a multitude of
publicly accessible mediator services offering a free "null response"
service which is indistinguishable from a failed
access from lack of authorization.

NOTE: It's ok to have multiple resources listed, but it is less
preferred.

**Fourth**, the single linked Resource property specifies its endpoint as
the IID's single service endpoint, using a properly formed DID-URL with
a service parameter. This pattern allows every resource to use the same
endpoint without duplicating endpoint URLs, even when specifying multiple
linked resources. This pattern encourages polymorphic mediators, which
improves overall privacy across the IID ecosystem.


EXAMPLE 4: A privacy-preserving IID document with zCap support
----
```json
{

  "@context": ["https://www.w3.org/ns/did/v1",
    "https://internft.org/ns/iid/v1"],
  "id": "did:example:abc123",

  "verificationMethod": [{
    "id": "did:example:abc123i#keys-1",
    "type": "Ed25519VerificationKey2020",
    "controller": "did:example:abc123",
    "publicKeyMultibase": "zH3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
  }],

  "authentication": "did:example:abc123i#keys-1",
  "capabilityDelegation" : "did:example:abc123i#keys-1",
  "capabilityInvocation" : "did:example:abc123i#keys-1",

  "service": [{
    "id":"did:example:abc123#mediator",
    "type": "polymorphicMediator2021",
    "serviceEndpoint": "http://8zd335ae47dp89pd.onion/iid/mediator/ did:example:abc123"
  }],

"linkedResource" : [{
    "id": "did:ixo:abc123#resourceHashgraph",
    "path": "did:ixo:abc123/resourceHashgraph",
    "type": "hashgraph",
    "rel":"attachments",
    "proof": "afybeiemxf5abjwjbikoz4mcb3a3dla6ual3jsgpdr4cjr3oz",
    "endpoint" : "did:example:abc123?service=mediator"
  }]

}
```

Terminology
===========

1. **DIDs** -- [[Decentralized Identifers]](#ref1). Cryptographically secured global 
identifiers defined by the DID Core specification developed by the W3C.

2. **DID-URLs** -- An extended form of a DID with additional components such as **/path**,
**?query**, and **#fragments** appended to a base DID.

3. **DID document** -- A representation of the meta-data needed to securly interact with a
 DID. Retreived by [[DID resolution]](#Resolution), DID Documents contain verification
 relationship and methods, as well as service endpoints and other method-specific properties.

4. **Resolution** -- The process by which one retrieves or generates a DID Document for a
given DID. Resolution and other DID operations are method-specific and may vary considerably
depending on the design decisions of each particular method.

5. **Dereference**
The process of retreiving a resource, given a URL. Once the DID for a DID-URL is resolved, the returned DID Document provides the information needed to retrieve the resource (if any) represented by the DID-URL.

References
==========

<a name="ref1">[1]</a> Decentralized Identifiers (DIDs) v1.0. World Wide Web Consortium.
Online at
[[https://www.w3.org/TR/did-core/]](https://www.w3.org/TR/did-core/).
Accessed February 15, 2021.

<a id="ref2">[2]</a>  RFC 3986 Uniforn Resource Identifier (URI) : Generic Syntax. IETF. Online at [[https://tools.ietf.org/html/rfc3986]](https://tools.ietf.org/html/rfc3986). Accessed March 31, 2021

<a id="ref3">[3]</a>  Multihash. Multiformats.io. Online at [[https://multiformats.io/multihash/]](https://multiformats.io/multihash/). Access March 31, 2021

<a id="ref4">[4]</a>  NFT-RFC-002 Use Cases and Requirements. InterNFT.org. Online at [[https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-002.md]](https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-002.md)

<a id="ref5">[5]</a>  NFT-RFC-008 Assertions. InterNFT.org. Online at [[https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-008.md]](https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-008.md)

<a id="ref6">[6]</a>  HTTP Range-14. Wikipedia. Online at [[https://en.wikipedia.org/wiki/HTTPRange-14]](https://en.wikipedia.org/wiki/HTTPRange-14)

<a id="ref7">[7]</a>  Token Taxonomy Framework. Interwork Alliance. Online at [[https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/main/token-taxonomy.md]](https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/main/token-taxonomy.md)






IIDs also provide a consistent, verifiable approach for referring to off-chain resources. Whether these resources are digital, physical, or conceptual.

To achieve this, IID methods SHOULD use content-derived identifiers and MAY use content-derived addressing systems, in which the cryptographic hash of a linked resource is used to unambiguously verify the resource.

Standards such as multihash [\[3\]](#ref3) provide a wide range of hashing algorithm options and representations which can be used for this purpose.

Mechanisms such as Hashgraphs enable an arbitrary number of verifiable resources to be linked to a digital asset, without revealing the number or content of these resources.
Content Identifiers (CIDs) provide robust verifiability and enable resources to be addressed without path-dependency. 
Both these mechanisms enable rich data to be associated with digital resources, without compromising privacy.

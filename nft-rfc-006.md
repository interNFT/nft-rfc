---
nft-rfc: 6
title: NFT Identifiers
stage: draft
category: NFT/METADATA
author: Joe Andrieu @jandrieu
created: 2021-01-21
modified: 
---

# NFT RFC 006 NFT Identifiers (IIDs)

Identifiers are used to refer to both on-chain and off-chain resources.
Non-fungible tokens (NFTs) require a cryptographically secure means to
both refer to specific tokens and prove control or ownership without
reliance on a trusted third party. This RFC outlines the requirements
for IIDs, proposes a new identifier approach, and compares this approach
to existing and legacy identifier efforts.

We refer to this new class of identifiers as Interchain Identifiers, or
IIDs for short. We propose this new identifier would be appropriate for
any on-chain asset, including smart contracts, fungible tokens, and
non-fungible tokens. However, this specification currently focuses on
satisfying the requirements for NFTs.

Requirements
============

Requirement 1 -- Identify on-chain tokens
-----------------------------------------

It must be possible to reliably identify specific on-chain tokens. A
unified identifier approach allows an identifier creator to specify

-   Which chain

    -   Bitcoin, Ethereum, Ixo, IOV, etc.

-   Which network

    -   Mainnet, testnet, etc.

-   Which fork

    -   BTC v BCH

    -   ETH v Eth Classic

-   Which instance of the token

Then, systems, software, and individuals relying on that identifier can
interpret the identifier unambiguously to understand exactly which asset
the creator referred to.

Requirement 2 -- Identify off-chain resources
---------------------------------------------

NFTs sometimes need to unambiguously refer to resources stored
off-chain. This includes both digital and real-world resources.

-   A theatre ticket for one person to a specific performance at a
    particular venue on a certain date and time

-   A property title that defines ownership rights in a particular plot
    of land, along with verifiable assertions and warranties about
    easements, liens, and permits.

-   A digital collectible characterized by a content-specified hash,
    which can be retrieved using that hash on a content-addressable
    network, like IPFS.

IIDs must have a way to associate off chain resources with the on-chain
token without ambiguity.

Requirement 3 -- Work with any chain
------------------------------------

For interchain functionality, IIDs must be able to reference any
on-chain asset, regardless of the chain on which that asset resides.
This allows NFTs on one chain to be reliably referenced from another.
This extends even to chains that don\'t yet exist. The approach for
chain agnostic identifiers must allow for future chains to use the same
approach, without changing the underlying IID specification.

Requirement 4 -- Enable verifiable assertions
---------------------------------------------

The identifiers for both on-chain assets and off-chain assets must be
suitable for verifiable assertions to be made about both, without loss
of rigor.

Requirement 5 -- Enable both private and public assertions
----------------------------------------------------------

The IID approach must enable both publicly revealed assertions, which
are available to anyone without further authentication or permission,
and private assertions which must be attained through privacy-respecting
means.

Requirement 6 -- Verifiability of information completeness
----------------------------------------------------------

Potential buyers of NFTs must be able to prove they have all of the
relevant information for the use of the NFT---at least as asserted by
the current token record. In order to prevent privacy problems, this
information may be private---requiring the buyer to secure the
information through permissioned means---but it must be possible for a
buyer to know if they have appropriately acquired all of those details.
For example, a title property may need to disclose a lien against the
property, without revealing publicly the details of that lien, because
the lien itself may expose private information. Knowing that some form
of additional data is required allows a serious buyer to request that
information without leaking private data to the public. Observers must
be able to cryptographically verify that such additional data \*is\* the
data associated with the NFT and that all such data has been collected.

Requirement 7 -- Off-chain creation of cryptographic identifiers
----------------------------------------------------------------

When supportable by a given chain, it must be possible for a new
identifier to be minted and usable before attaching it to an onchain
token. These latent tokens may be used for demonstrating
proof-of-control, authentication based on proof-of-control, and
cryptographic signing, without incurring the transactional costs and
delays of interacting with the foundational chain. Updates and
annotations to identifier related metadata would require chain
interaction, but the initial minting would not. This feature allows the
use of such identifiers for assertions, such as verifiable credentials,
prior to anchoring to a chain. The verification for such an identifier
must check on-chain for updates, but finding none, the identifier itself
can be used to deterministically generate the appropriate metadata for
its use.

Requirement 8 -- Use with self-sovereign identity
-------------------------------------------------

IIDs must be able to work with emerging self-sovereign identity
approaches, which allows individuals to manage identifiers and
associated credentials without reliance on trusted third parties.

Requirement 9 -- Use with confidential storage
----------------------------------------------

IIDs must be able to work with emerging approaches to confidential
storage, aka Secure Data Storage or Encrypted Data Vaults. These
services need cryptographically enabled capabilities for authorization
and robust mechanisms for encryption.

Requirements 10 -- Recognizability
----------------------------------

IIDs must be recognizable as such. These identifiers may have unique
properties compared to other identification approaches. When used in
various contexts, it should be readily discernible that the identifier
is, in fact, an IID.

Requirement 11 -- Multiple metadata representations 
----------------------------------------------------

IIDs are expected to be used in a wide variety of contexts, with
commensurate variety in the appropriateness of different serializations.
IIDs must be able to represent associated metadata in a variety of
formats without losing rigor. This includes representations of
associated rights and attributes.

Requirement 12 -- Leverage existing tooling and infrastructure
--------------------------------------------------------------

To the extent possible, IIDs should enable the use of widespread and
mature tools rather than requiring bespoke or relatively untested
innovative approaches.

Anti-Requirement 1 -- Human readability
---------------------------------------

These identifiers are designed to be cryptographically secured and
independent of trusted third parties; IIDs are secure and decentralized.
However, they are not designed to facilitate human readability or use.
User-friendly naming schemes, if any, must operate at another level.

Proposal in brief
=================

Define IIDs as a profile of Decentralized Identifiers (DIDs) and support
the use of Verifiable Credentials (VCs) for assertions. DIDs and VCs are
specifications managed by the World Wide Web Consortium. Further, define
all IIDs to dereference to a representation of the token itself while
enabling IID References and IID Resources as identifiers within the
assets's namespace for rigorous assertions and retrieval.

IIDs define a family of DID Methods, allowing different chains and
approaches to realize both IID and and DID functionality. IID Methods
specify how IID (and DID) functions are achieved for a given chain,
allowing for different parties to define Methods for the same chain
should alternative approaches make sense---there need not be a
definitive IID Method for a given chain.

IIDs resolve to IID Documents, interoperably based on DID Documents, for
communicating IID metadata. In addition, Verifiable Credentials may be
used to provide attestations related to the asset using the IID or an IID
reference as its subject.

Prior Art
=========

IIDs are not the first effort to define globally usable identifiers.

On-chain identifiers
--------------------

Today, on-chain identifiers are overwhelmingly be chain-specific, with various
context-specific rules for interpreting different strings of bytes in
different ways. Due to the fundamentally decentralized approach to the
creation of blockchains, nothing prevented each blockchain project from
defining their own approach. This was flexible, but made it hard to
build interoperable systems across blockchains.

World Wide Web Identifiers
--------------------------

### URLs

The original, open, global identifier, Uniform Resource Locators (URLs)
form the foundation of the World Wide Web. In addition to http and https
URLs, which are likely the most widely used form of identifier, URLs
enable a variety of other transport protocols, such as ftp, telnet, and
email. This extensibility is provided by different \"schemes\" which
form the initial characters in the URL. Through the scheme part, URLs
define the mechanisms for interacting with the Resource (which is the
\"R\" in URL). While http and https URLs depend on numbers (IP
addresses) or names (domain names) issued under the Internet Assigned
Numbers Authority, some do not (such as data:, chrome:, and did: ).

URLs are first **resolved** to gather any metadata required for
interacting with the resource (such as transforming a domain name into
an IP address), then **dereferenced** to perform the interaction
(typically returning a representation of the resource).

The original specification for URLs was RFC1738, which has been
deprecated in favor of RFC 3986 which defines URIs as a generalization
of URLs. However, the most recent work from the WHATWG advocates for URL
over URI
https://url.spec.whatwg.org/#url-apis-elsewhere

> Standardize on the term URL. URI and IRI \[Internationalized Resource
> Identifier\] are just confusing. In practice a single algorithm is
> used for both so keeping them distinct is not helping anyone. URL also
> easily wins the search result popularity contest.

In practice, discerning developers use URIs when discussing the ability to
identify a resource of some kind and URLs when discussing resources that
can be interacted with or retrieved online. However, smart developers know that for most practical purposes, these are interchangable terms.

### URIs

Uniform Resource Identifiers, defined in RFC3986, generalize URLs for
use as generic identifiers, usable for identifying anything, including
real-world objects and other resources which do not necessarily support
the interaction ability presumed in URLs.

RFC3986 defines a generic syntax to increase interoperability between
existing and future URIs:

> **URI = scheme \":\" hier-part \[ \"?\" query \] \[ \"\#\" fragment
> \]**
>
> **hier-part = \"//\" authority path-abempty**
>
> **/ path-absolute**
>
> **/ path-rootless**
>
> **/ path-empty**

As such, all URLs are URIs. However, URIs are not expected to be
resolvable and dereferenceable. Because URIs use the same scheme
definitions as URLs, it is essentially impossible to distinguish a URL
from a URI. You may use a URL where a URI is desired and may attempt to
dereference a URI to interact with a resource.

This has led to the infamous HTTPRange14 problem in which a real-world
resource is identified by a URI that is, in fact, dereferenceable (like
a URL) to interact with a resource which is online (and therefore NOT
the same resource identified by the URI). For example, a person might
use the URI
[[http://example.com/abc]{.underline}](http://example.com/abc) to refer
to themself, but the website that responds to
[[http://example.com/abc]{.underline}](http://example.com/abc) is NOT
that person, nor is the page or other digital resource returned via
http. It is, at best, a digital presentation of some aspect of myself.

### URNs

Uniform Resource Numbers are an iteration on URIs which avoid
HTTPRange14 by explicitly avoiding any specificity about where the
resource is located or how to access it. The International Standard Book
Number (ISBN) can be represented with URNs, with the syntax
urn:isbn:ISBN\_NUMBER, which uniquely defines a specific published book
without worrying about how you might get any additional information such
as where to buy the book.

### IRIs

International Resource Identifiers are an internationalized version of
URIs, which allow non-ascii characters to support non-western languages
such as Japanese or Arabic. A solid step forward for supporting
international diversity, they have also been criticized for their
ability to use non-standard visually similar characters to spoof
legitimate addresses.

### RDF

Resource Description Framework is the technical underpinning of the
Semantic Web, a re-imagining of the World Wide Web, in which
semantically rigorous statements can be shared across context without
losing meaning. RDF leverages URIs for unambiguously defining
terminology. All RDF statements can be conceptualized as a triple of
subject, predicate, and object (later \"context\" was added,
transforming RDF statements into quads, but RDF triples are still used
in discussion). Each Subject, Predicate, and Object may be expressed
either as a literal (a string, a number, a date, etc.) or as a URI.
These URIs allow anyone that controls a domain name to define a
vocabulary with explicit semantics; those who choose to make statements
using those same semantics can reuse that vocabulary (with the same
URIs) such that all readers of those statements have the same reference
for what those terms mean. RDF provides a mechanism for clearly
distinguishing common lexical terms used differently in different
contexts. So while, it may be arguable if \"name\" on a digital
driver\'s license has the same semantics and \"name\" in an online
profile, all uses of
[[http://example.com/name]{.underline}](http://example.com/name) are
taken to have the same intended definition, which, by best practice may
be understood by dereferencing
[[http://example.com/name]{.underline}](http://example.com/name) and
viewing the definition.

Interchain UX Working Group
---------------------------

The Interchain UX Working Group is actively working to solve \"the
emerging challenges that need to be addressed by application level
developers to ensure a high quality user experience when dealing with an
IBC connected Internet of Blockchains. This is part User Interface
questions (how to display an IBC connected asset? What level of
transparency or insight on security should be my responsibility as an
interface developer?) as well as developer experience questions (how do
I query the balance of a user with multi-chain assets and display those
assets in a clear and friendly manner?).

This work necessarily includes addressing questions about how to
identify and represent NFTs from various different blockchains in a
coherent manner.

Their purview also extends into user-friendly names as well as impacts
on wallet design.

So far, this group recognizes the work of [Chain Agonistic Improvement
Protocols](http://github.com/ChainAgnostic),
which we discuss next.

More information can be found at
https://hackmd.io/@okwme/ux-wg

CAIP 2 and CAIP 19
------------------

The Chain Agnostic Standards Alliance is a collection of working groups
dedicated blockchain protocol-agnostic standards. CASA also publishes
Chain Agnostic Improvement Proposals which describe standards created by
the different working groups. Of particular note in the development of
this specification is [CAIP 19 Asset Type and Asset ID Specification](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md))
as it directly applies to on-chain assets like NFTs, and [CAIP 2
Blockchain ID Specification](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md))
which is used by CAIP 19 to identify different blockchains.

Our goal is to support and leverage these CAIP proposals as much as
possible, incorporating their ideas into this specification and
suggesting improvements to CAIPs as appropriate.

CAIP-19 defines a way to identify a type of asset (e.g. Bitcoin, Ether,
ATOM) and an asset ID (for non fungible token) in a human-readable,
developer and transaction friendly way.

CAIP-19 identifiers have the following syntax (from
https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md):

> **asset\_id**: **asset\_type** + \"/\" + **token\_id**
>
> **token\_id**: \[-a-zA-Z0-9\]{1,47}
>
> **asset\_type**: **chain\_id** + \"/\" + **asset\_namespace** + \":\"
> + **asset\_reference**
>
> **chain\_id**: \[per CAIP 2, see below\]
>
> **asset\_namespace**: \[-a-z0-9\]{3,16}
>
> **asset\_reference**: \[-a-zA-Z0-9\]{1,47}
>
> From
> https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md]
>
> **chain\_id**: **namespace** + \":\" + **reference**
>
> **namespace**: \[-a-z0-9\]{3,16}
>
> **reference**: \[-a-zA-Z0-9\]{1,47}

This approach has some notable convergence with DIDs (and IIDs):

1.  Each chain gets to define its own namespace and rules for resolution

2.  Within each namespace, hierarchical subspaces are supported (for
    asset namespaces and references)

3.  Anyone can define a new namespace, allowing multiple solutions on
    different blockchains

It also has some notable divergence from DIDs:

1.  CAIP 19 identifiers are neither URLs nor URIs, limiting their
    usability in web-aware applications

    a.  DIDs are URIs and can form URLs

2.  CAIP 19 does not define the metadata related to an identifier nor
    how it might be discovered

    b.  DIDs use DID Documents

3.  CAIP 19 syntax restricts the hierarchy to a specific structure with
    constrained meaning

    c.  DIDs allow arbitrary hierarchies with Method-specific meaning

4.  CAIP 19 syntax does not provide a means for identifying sub-asset
    information structure

    d.  DIDs allow path, query, and fragment parts for Method-specific
    functionality

Decentralized Identifiers
=========================

[Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-core/) are a standards-track specification
under development at the World Wide Web Consortium.
They are \"a new type of globally unique identifier designed to enable
individuals and organizations to generate our own identifiers using
systems we trust, and to prove control of those identifiers
(authenticate) using cryptographic proofs (for example, digital
signatures).\"

DIDs enable verifiable, decentralized digital identity. They were
inspired by blockchain based approaches for \"identity\", using an
RFC3986 compatible syntax. As such DIDs *are* URIs and are designed to
work within existing web frameworks.

DID URLs support additional **path** (/directory/file), **query**
(?query=value), and **fragment** (\#fragment)parts. Fragments are
commonly used to refer to elements within a DID Document.

DIDs work because of two structural design choices.

First, each DID specifies a DID Method, which defines how a DID consumer
might perform Create, Read, Update, and Deactivate operations. Different
types of DIDs may have different Methods, and each Method may define
unique approaches for those functions. This allows DIDs that anchor to
Bitcoin and Ethereum, as well as bespoke fit-for-purpose ledgers such as
Veres One or Sovrin. DID Methods \*may\* be registered in a common
registry for increased interoperability, but such registration is not
required; it is merely a convenience.

Second, every DID resolves to a DID Document, which contains the
metadata required for interacting securely with the DID Subject.

-   Public Keys

-   Verification Relationships

    -   Assertion Method

    -   Authentication Method

-   Service endpoints

DID Document state is managed by DID Registries; many are blockchains,
but alternatives such as did:peer, did:git, and did:key do not rely on
blockchains at all. Methods like did:key and did:btcr provide for
deterministic creation of DID Documents based on rules in their
specification; no actual DID Document is stored anywhere. A more recent
class of DIDs, including did:v1, did:ethr, and did:ion allow the
creation of DIDs without registration, relying on the registries purely
for updates; did resolution for these methods checks the registry for
any updates and if there are none, use a deterministic algorithm to
generate a DID Document or a cryptographic verification of an initial
DID Document communicated through alternate channels.

It is this indirection of DID Documents that allows key rotation without
explicit notification to all parties. It is the open-ended DID Method
architecture that allows for decentralized and future proofed innovation.

Third, DID Methods with publicly inspectable registries (where DID
Document state is maintained), such as blockchains, may also provide for
auditability, and with some effort, even reversibility of changes in
case of inappropriate transactions. These advanced features remain areas
of active development.

Finally, DID Documents are defined using an abstract data model,
allowing any number of serializations, with initial support for JSON and
JSON-LD serializations. CBOR and CBOR-LD are also highly anticipated for
their ability to dramatically reduce the size of DID Documents. Other,
future serializations are also possible without losing conformance to 
the specification.

### Lessons Learned from DIDs

First and foremost, do not use public ledgers as directories. Only use
them for verification of temporal ordering. That is, with a public
ledger, it is possible to deterministically know which DID Document is
the current, authentic DID Document for a given DID. Some Methods do not
provide this verifiability, which may be fine for some use cases. Using
public ledgers as directories presents privacy and confidentiality
problems as ledgers are designed to immutably record their transactions:
once written to the ledger, you generally can\'t unwrite it, making
disclosure of proprietary or personal information problematic.

Second, avoid unnecessary public correlation. DID Documents provide the
option of embedding service endpoints, which may themselves be present
in multiple DID Documents. For example, you \*could\* add a Twitter
address as a service endpoint in several different DIDs. This would link
those DIDs to each other in a non-verifiable, yet undisputable way: while
observers could not directly tell if those service endpoints mean that
the Twitter account controls those DIDs, they do gain a point of
observation for consideration in evaluating that correlation. For many,
this undermines the privacy goals of being able to use DIDs without
revealing any additional personally identifiable information.

Third, DIDs, and their sister specification VCs, embrace an open world
data model, in which anyone can add any parameter to the Document
without violating conformance. This is convenient, but also means that
unfortunate properties can and will be used, such as properties that
explicitly communicate details about the DID Subject. Such details are
intended to be preserved by Methods and requesting parties even when
they are misunderstood, which creates significant opportunity for
unintended consequences. However, it is understood that this flexibility
affords significant innovation even as it invites endless debate on
which properties get to be defined where---a decision that has
significant impact on ubiquitous adoption.

Finally, DID Documents are NOT signed documents. The only verification afforded
for DID Documents is that by executing the process defined in the DID Method,
whatever the result is **is** the verified DID Document. This means that
you MUST trust the software that performs this resolution, either by
reputation or because you wrote it yourself. This choice was informed by
a tricky catch-22 where DID identifiers are a result of cryptographic
operations perform either on or with the DID Document. For example, IPFS
based DID Documents cannot contain the IPFS address because the content
hash of that DID Document is the address. Similarly, ledger-based DIDs
that depend on blockheight determine their ID through the process of
registration. In both cases, you can\'t fully create the DID Document
before it is registered. I may be possible to ensure a signature in the
DID resolver metadata as a signed hash using the cryptographic material
in that document, but this remains an area of innovation.

**A note on DIDs as URIs rather than IRIs**

DIDs and IIDs are not intended to be human readable, so the spoofing
concern is mitigated to some degree as is the need to support
alternative character sets. In fact, DIDs and IIDs are generally
encodings of cryptographic identifiers, such as a public key; none of
the extant encodings use non-ascii characters.

Proposal 
---------

**First**, create IIDs as an interoperable family DIDs Methods with 
additional properties. Each IID \"namespace\"---to use the CAIP term---
defines its own Interchain compatible DID method, e.g., did:erc721, 
did:cosmos, did:iov, did:etc. DID Methods that support IID functionality
define themselves as an IID Method with method-specific properties in its
DID Documents, known as IID Documents. IID semantics, shared among different IID
Methods, enable cross-chain interoperability with other IIDs for NFT and
blockchain functionality.

In short, IIDs **ARE** DIDs.

IID Documents **are** DID Documents.

This makes IIDs compatible with URLs and URIs and widespread tooling of
the World Wide Web as well as emerging DID technology. It also ensures
that IIDs are drop-in replacements for RDF subjects, predicates,
objects, and contexts, allowing RDF statements to use IIDs for
assertions (as is done with Verifiable Credentials) with exceptional
rigor.

**Second**, differentiate IIDs as on-chain identifiers with their own
semantic namespace for references and resources.

**All** IIDs refer to on-chain assets by definition. Dereference an IID,
you get a representation of that asset. Then, each IID can be combined
with a path part or fragment part to refer to off-chain resources or
on-chain defined references. Use \/path parts for dereferencable resources---
those that can be retrieved online. Use \#fragments for pure identifiers defined
within the IID Document.

In this way, every IID defines its own namespace, within which rigorous
statements can be made about real-world objects (references) and which
can be directly downloaded via web technology (resources).

For example, **did:title:abc** might represent a token that is the title
to a real property, and **did:title:abc\#parcel1** is used to refer to
that property in attestations associated with that token, such as
"**did:title:abc\#parcel1"** is located at 123 Main Street, Anytown,
France. Then, you can use **did:title:abc\/photo1.png** to point to an
image of the property.

By IID convention, if it is desirable to refer to a IID Resource in an
RDF statement, an IID reference is constructed using the same value as a
fragment as the path part of the reference. For example, to make an RDF
statement about the photo at **did:title:abc/photo1.png**, the IID
Document simply defines an IID Reference of
**did:title:abc\#photo1.png**.

This distinction avoids the dreaded HTTPRange14 problem because the raw
IID is always only used to refer to the asset, which is always
dereferenceable, while IID references are only ever URIs (which are not
themselves inherently dereferenceable) and IID Resources

Base IIDs, IID References (with fragments), and IID Resources (with
path parts), are fully conformant URIs and suitable for use in RDF
statements.

IIDs resolve to IID documents which contain the minimum, verifiable
required metadata for using the NFT. Like a DID Document, it defines a
range of features for interacting with the subject. It may also provides
IID specific properties:

**LinkedResource** -- provides a privacy-enabled way to attach
digital resources associated with the asset. An optional array of one or
more resource descriptors, it provides the metadata required for
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
    "LinkedResource" : [{

    "path" (optional): // fully qualified IID Resource ID for this resource, e.g., did:example:abc/myResource.png,

    "id" (optional): // fully qualified IID Reference ID for this resource, e.g., did:example:abc#myResource.png, Optional

    "type" : "nft:ResourceDescriptor",

    "proofType" (optional) : "hash" | "hashgraph", 

    "proof" (optional): hash | hashgraph,

    "resourceFormat": "IID Resource type | mime type",

    "encoding" : "native" | "multibase" | "string",

    "compression": gzip | none,

    "encryption" : [open ended for arbitrary extensibility],

    "endpoint" (optional): url,

    "resource" (optional): a representation of the resource for inline
distribution

}]
}
```

### Types of Linked Resources for IIDs

IIDs define a range of specific resource types for interoperability
among IID Methods.

**Extension**: A JSON-LD extension of the current document. The RDF
statements in the extension are to be interpreted as if they were
included in the current IID Document. For example, you might provide
additional service endpoint definitions in an linked resource. Those
endpoints can be verified as associated with that IID, but only by those
parties who secure those definitions through other, privacy respecting
means.

**Executable Rights**: The resources could also define executable
capabilities that can be invoked by the IID owner or its designate,
using cryptographic materials defined elsewhere in the document.

**Accorded Rights**: Similarly, linked resources could specify
real-world rights accorded to the IID owner or its designate, such as
a digital driver\'s license or a theater ticket. The representation
framework for such rights must be open ended, including both plain text
statements of rights, e.g., \"The controller of this IID is entitled to
...\", or more rigorous, and computationally evaluatable RDF statements
which might describe in great detail a range of benefits that accompany
the basic rights of the token.

**Assertions**: Verifiable credentials, verified claims, claim tokens
as described in [NFT-RFC-008](https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-008.md). This allows arbitrary, yet verifiable
attestations to be made either about the asset or about the resources
defined by IID references. The attributes represented in these claims
can be retrieved via the NFT interface using a query by example (graph
query) mechanism.

\[NOTE: need concrete examples of these different resource types as they
would be used in an IID Document\]

New Service Endpoint Types
--------------------------

IID Documents, like their DID counterparts, can specify service
endpoints. It is considered best practice to use a single service
endpoint to avoid unnecessary correlation across services. In situations
where multiple service endpoints would be desirable, a mediator endpoint
can be used. The definition of a mediator API is outside the scope of
the DID Core specification, so IIDs will define several common service
types for use across IIDs.

**Service Type: Mediator**

Takes an endpoint query object and returns either (a) one or more
service endpoint definitions or (b) a resource. The endpoint may require
authorization or authentication prior to performing mediation. The query
object, at a minimum includes one or more desired service types.

The preferred mechanism for endpoint negotiation is a private set
intersection, with strict limits on the number of proposed services by
the requester.

Mediators are capable of polymorphic service response, acting as a
specific service endpoint directly, based on the query object,
precluding the need for a second service call. This allows the same
endpoint to act as any number of service endpoints without leaking the
types of service endpoints available on a public blockchain.

Trusted mediators have a role to play in enhancing asset holder privacy.
These mediators operate on behalf of multiple IIDs simultaneously,
preferably IIDs from different users. This prevents observers from
correlating a given mediator with a specific individual.

Mediator responses SHOULD be signed by the cryptography associated with
the IID (or DID) so that recipients can verify the resource is the one
intended by the IID controller.

This definition is work in progress.

\[TODO: define endpoint query object and endpoint response object\]

**Service Type: MethodResource**

The service type MethodResource means that the service endpoint uses a
method-specific retrieval mechanism to return a resource directly,
rather than a service endpoint definition. The result of dereferencing a
IID Resource ID with this service type is the resource retrieved using
this mechanism. This allows the retrieval of resources without using URL
service endpoints. For example, **did:example:abc/image.png** might be
retrieved by exchanging UDP messages with a peer node on a distributed
network. As a valid URL, that same IID Resource ID could be used as the
source in an HTML image tag, e.g., \<img
src="**did:example:abc/image.png"**\> without relying on the browser to
use http and the domain name system (once browsers integrate support for
DIDs, of course).

Examples
--------

The CAIP 19 (and CAIP 2) work largely follows a similar structural
approach, thanks to the fundamental similarities in use cases. Here\'s a
comparison of several identifiers in both specifications:

### Cryptokitties Contract

**CAIP 19**
```
eip155:1/erc721:0x06012c8cf97BEaD5deAe237070F9587f8E7A266d
```

**IID**
```
did:eip155:1:erc721:0x06012c8cf97BEaD5deAe237070F9587f8E7A266d
```

### Cryptokitties Collectible

**CAIP 19**
```
eip155:1/erc721:0x06012c8cf97BEaD5deAe237070F9587f8E7A266d/771769
```
**IID**
```
did:eip155:erc721:0x06012c8cf97BEaD5deAe237070F9587f8E7A266d:771769
```

### Property Titles

**Title IID**
```
did:title:54fff14d:db1b:4fea:9441:5618f5937444:123123243
```

**Title Reference**

```
did:title:54fff14d:db1b:4fea:9441:5618f5937444:123123243\#parcel1
```

**Title resource**
```
did:title:54fff14d:db1b:4fea:9441:5618f5937444:123123243/permit1.pdf
```

**Title assertion in RDF (using Turtle)**
```turtle
@base <did:title:54fff14d:db1b:4fea-9441:5618f5937444:123123243> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns/#> .
@prefix t: <http://www.example.com/title\#\> .
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84\_pos\#\> . 

<#parcel1> a t:parcel;
    t:centroid geo:location <#gps1> .
<#gps1> geo:lat 36.144724 ; 
    geo:long -86.802715 .

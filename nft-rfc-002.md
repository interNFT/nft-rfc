---
nft-rfc: 2
title: Use Cases and Requirements
stage: draft
category: NFT/USECASES
kind: Requirements
author: Shaun Conway @ig-shaun
created: 2020-10-19
modified: 
---


## Use Cases and Requirements Working Draft

### Abstract

Non-Fungible Tokens are containers for uniquely identified resources, which are represented by NFT metadata. NFTs enable rights of ownership and control over resource identifiers. They may also contain other rights, within specific contexts and use-case.

By developing Interchain Standards for NFTs and Metadata, we intend to make NFTs interoperable across blockchain networks and to enable ownership and control of NFT metadata and linked resources, regardless of where these are located across blockchain networks, the web, or offline. 

Interchain NFTs and Metadata should have features which will directly benefit users, promote the adoption of decentralised web standards and offer new economic mechanisms for sustainable digital finance and the impact economy.

By presenting a set of canonical use-cases and user stories, this document starts to describe the defining features of Interchain NFTs and Metadata, and why these are beneficial. 

This document is intended to support the InterNFT Working Group to identify technical requirements for developing an interface standard for Interchain NFTs and an Interchain Metadata Standard for NFT referent resources. Recommendations in these standards should be sense-checked against these use-cases and requirements.

This is a living document which will remain in a “working-draft” state, to encourage further contributions, improvements and addition of new use cases, examples and user stories.

### Status of this Working Draft Document

_This section describes the status and current Git Version of this document. Other documents may supersede this document._

This is a draft which may be updated, replaced or made obsolete by new versions at any time. Only cite this as a work in progress.

The document is being developed by the [Working Group for Interchain Non-Fungible Tokens and Metadata](https://internft.org).

The use case model and specific examples described here are not intended to be exhaustive or complete. Rather, this is intended to capture a broad understanding of the problem space and the generic requirements which need to be considered when drafting standards for NFTs and Metadata. The technical concepts and experiences in implementing various of these concepts are still nascent and are likely to significantly evolve. By sense-checking these concepts against real-world use cases and requirements, this work can remain both relevant and focused.

[GitHub Issues](http://tbc/) are preferred for discussion of this specification. Changes may be proposed as Github Pull Requests.

### Terminology

| Authentication | A process which is defined by a protocol for an entity to prove it has a specific attribute or that it controls a specific secret, using one or more [verification methods](https://www.w3.org/TR/did-use-cases/#dfn-verification-method). |
| :--- | :--- |
| Assertion | A statement by an identified party, with or without implicit or explicit guarantees as to its validity, or authenticity of the identity of the party. |
| [Content Address](https://docs.ipfs.io/concepts/content-addressing/) | A method for identifying a resource using the content of the resource, which is typically formed by cryptographic hashing |
| Consensus | A standardised process for the participants in a [network](https://objectcomputing.com/expertise/blockchain/glossary#network) to determine a single truth, in the context of blockchain protocols |
| CID | Content address as specified by the [Interplanetary File System \(IPFS\) protocol](https://ipfs.io) |
| Data Format Specification | An agreement on the correct interpretation of [representation](https://www.w3.org/TR/webarch/#def-representation) data |
| [Decentralised Identifier](https://www.w3.org/TR/did-core/) \(DID\) | A globally unique persistent identifier for any subject \(person, organization, thing, data model, abstract entity, etc.\) that does not require a centralized registration authority because it is generated and/or registered cryptographically |
| [DID Document](https://www.w3.org/TR/did-core/) | The metadata for a resource which is identified by a decentralised identifier |
| Fungible | Things that are equivalent or part of an identical set of things, which makes them interchangeable |
| Hash | Cryptographic hashes are functions that take some arbitrary data input and return a fixed-length value, which is determined by the specific hash algorithm used |
| [Internationalised Resource Identifier](https://en.wikipedia.org/wiki/Internationalized_Resource_Identifier) \(IRI\) | The international version of a Universal Resource Identifier \(URI\), which allows for the use of additional character sets |
| IRI Owner | By convention, the entity who gets to say what the intended \(or usual\) referent is for an [IRI](https://www.w3.org/TR/rdf11-concepts/#dfn-iri) |
| Label | A set of assertions with a common implicit subject _\(attribute-value pairs linked to an identifier for the subject\)_ |
| Links | An assertion of relationship between two resources |
| [Linked-Data](https://www.w3.org/TR/ld-glossary/#linked-data) | A pattern for hyperlinking machine-readable data sets to each other, in ways that are also understandable by humans, using Semantic Web standards |
| Metadata | Machine understandable information about web resources or other things |
| Non-Fungible | Things that are uniquely identifiable individually, or as part of a set of things which are not equivalent, which makes them not interchangeable |
| Referent | The [resource](https://www.w3.org/TR/rdf11-concepts/#dfn-resource) [denoted](https://www.w3.org/TR/rdf11-concepts/#dfn-denote) by an [IRI](https://www.w3.org/TR/rdf11-concepts/#dfn-iri) |
| [Representation](https://www.w3.org/TR/webarch/#def-representation) | Information about a past, current, or desired future state of a resource, in a data format that can be readily communicated and understood with metadata. Representations do not necessarily describe the actual resource, or portray a likeness of the resource, or represent the resource in other senses of the word "represent". \(As defined by [RFC7231](https://www.w3.org/TR/did-use-cases/#bib-rfc7231)\) |
| Resource | Any identifiable thing. Including physical things, documents, digital objects, abstract concepts, numbers and strings. “Anything that may be identified by a URI” \(As defined by [RFC3986](https://www.w3.org/TR/did-use-cases/#bib-rfc3986)\) |
| State | A computational model which represents one of a finite set of possible states at a given point in time, which cannot be reversed and which enforces a state transition process to change at the state at a subsequent point in time |
| Token | A container of information which is controlled by a cryptographic secret key |
| Universally Unique Identifier \(UUID\) | A type of globally unique identifier that does not require a centralized registration authority, but \(unlike DIDs\) is not resolvable or cryptographically verifiable. \(As defined by \([RFC4122](https://www.w3.org/TR/did-use-cases/#bib-rfc4122)\) |
| Validation | Mathematically proving that a value is valid, in the context of cryptographic protocols |
| Verification | Evaluation of a claim to determine if it is valid, authentic, conforms to a required standard specification, and satisfies a defined cryptographic proof method |
| Verifiable Claim | An assertion about a subject, made by an identified entity who can be authenticated, which can be verified based on a set of standard requirements and cryptographic proofs |

## 1. Introduction

Tokenizing real-world resources is a critical enabler for the digital economy. This is also essential for transitioning the world to more accountable, sustainable means of producing and using natural resources.

It is now technically feasible for any uniquely identifiable physical world resource — whether tangible or intangible, to be represented in a non-fungible tokenized digital format.

Non-fungible Tokens \(NFTs\) have powerful features, such as embedded rights, provenance and verifiability. The range of canonical use-cases and list of potential features of NFTs and Metadata are growing.

An interoperable NFT and metadata standard is necessary for tokenized digital resources to be virtually addressed, described, authenticated, controlled or exchanged across blockchain networks and through the Web.

This document sets out use cases and requirements for establishing standards which could be adopted to achieve interoperability between blockchain networks, which will be compatible with long-established Internet standards and which build on the latest decentralised web specifications.

> _“Throughout the World Wide Web, as trust becomes an important issue, it will be important for software -- and people -- to keep track of and take into account who said what in terms of data and metadata”. Tim Berners-Lee \(1997\)_

### Core characteristics of Interchain NFTs & Metadata

Cryptographic tokens which subscribe to the Interchain Standards for NFTs & Metadata are characterised as being:

1. **Uniquely identifiable** so that instances cannot be duplicated or copied without detection;
2. **Ownable** with associated rights and capabilities which can only be transacted and transferred by the owner/s of the asset;
3. **Resolvable** to enable discovery, validation and verification of assertions and their linked resources;
4. **Decentralised** with no requirement for a central issuing agency;
5. **Persistent** to not be reliant on the custodianship or continued operation of organisations which are impermanent;
6. **Cryptographically verifiable** to prove that assertions and resources have not become corrupted and to demonstrate control over authenticated resource identifiers;
7. **Stateful** to establish a sequential order in which a metadata and resources are recorded, for provenance as well as temporal and relational integrity.

Other classes of tokenized assets and resources may display some of these characteristics, but cannot be described as _Interchain NFTs_, if they do not display all of these characteristics.

### The concept of a Non-Fungible Token

A Non-Fungible Token \(NFT\) is a container for identifying a unique resource. It may also contain rights associated with the resource. The token owner has the ability to change this representation of the resource.

NFTs are not interchangeable, as each token can have a different value to other tokens within the same set.

### The concept of Metadata relating to NFTs

NFT Metadata is a set of assertions which describe one or more uniquely identified resources that are referent to an NFT.

#### Digital resources

A _Resource_ is any identifiable thing. This includes physical things, documents, digital objects, abstract concepts, numbers and strings. in the context of the Internet a resource has historically been defined as “The thing which you get when you follow a link”.

In the context of NFTs, a resource could be a natively digital object, such as a digital artwork, or information which is linked to physical objects, such as a digital certificate that contains assertions about a specific section of land.

#### Metadata

Information about a resource is described as metadata. This typically asserts one or more sets of attributes about the resource. These attributes are usually key-value pairs. The [_Resource Description Framework_](https://www.w3.org/RDF/) is a well-established pervasive standard for describing resource attributes in the context of the Web. However, this metadata does not maintain a globally consistent state and is mutable.

A standardised format for NFT Metadata has not yet been established. For NFTs metadata to become interoperable, we need a description standard which can be interpreted and understood across different contexts, locations and technology implementations.

> _"URI persistence is a matter of policy and commitment on the part of the URI owner. The choice of a particular URI scheme provides no guarantee that those URIs will be persistent or that they will not be persistent."_ [_W3C,_](https://www.w3.org/TR/webarch/#def-representation) [_2004_](https://www.w3.org/TR/webarch/#def-representation)

#### Unique instances of digital resources

There is currently no standard way to identify the uniqueness of resources across different namespaces.

A Universal Resource Locator \(URL\) identifies a unique instance of a web resource at an address within a namespace. However, this does not guarantee uniqueness of the resource, as this may be duplicated at multiple locations.

With cryptographic hashes, resource metadata and instances of resource data can establish an immutable, unique identity for a resource. A variety of hash algorithms could be used for this purpose. Resolving the identity of a Resource requires knowledge of which specific hash algorithm was used. There is currently no broadly adopted standardised way to achieve this resolution, but the IPFS specification for Content Addresses \(CID\) is gaining adoption.

An Interchain standard for NFT metadata should aspire to address and authenticate the uniqueness of a resource across all distributed ledger namespaces.

#### The state of digital resources

The sequential order and time of recording resource metadata matters for provenance, temporal and relational integrity. When hashes of resource metadata and/or data are committed to a [Merkle Tree](https://en.wikipedia.org/wiki/Merkle_tree), these resources maintain state within the context of a directed acyclic graph. If this graph is committed to the state of a distributed ledger, the resource maintains a unique state in the context of the ledger namespace.

#### Classes of resources

A classification system for resources should enable us to distinguish differences between canonical classes of resources, which can be linked to exemplary use-cases. This will allow us to identify differences in requirements and features for each unique class, which must be taken into consideration for the design of an Interchain standard.

The [Interwork Alliance](https://interwork.org/) has introduced a [Token Taxonomy](https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/master/token-taxonomy.md) which describes a classification hierarchy for tokens that proposes a standard [Taxonomy Model](https://github.com/InterWorkAlliance/TokenTaxonomyFramework/blob/master/taxonomy-model.md) for representing classes, properties and behaviours of tokens in structured data templates.

###  The purpose of Interchain Standards

Interchain Standards for NFTs should provide an interoperable, standard way to own, authenticate and transact with non-fungible tokens across blockchain networks.

Interchain standards for NFT metadata should make information about the resources which are linked to NFTs machine-readable, machine understandable and verifiable, regardless of where this metadata is located, across blockchains, the web, or offline.

Together, these standards will unlock the potential for NFTs and their metadata to become as pervasive and interoperable as URLs are on the web. This will provide a significant renovation to the architecture and utility of the web, by providing stateful and verifiable representations of unique web resources.

### Existing Work

#### NFTs

[CryptoKitties](https://www.cryptokitties.co/) is the first widely-known example of Non-Fungible Tokens. When this launched in November 2017, it introduced a mechanism for creating and owning unique digital resources that people desire as collectibles. This was based on a technical specification \([ERC-721](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) for the minimum interface that a smart contract on the Ethereum network must implement to allow unique tokens to be created, managed, owned, and traded. This specification does not mandate a standard for token metadata or restrict adding supplemental functions.

Subsequently a number of new ethereum network specifications have been proposed to add supplemental functions and enhancements to the ERC-721 standard. These include methods for combining fungible and non-fungible tokens in multi-token transactions \([ERC-1155](https://github.com/ethereum/EIPs/issues/1155)\), to delegate ownership and control \([ERC-994](https://github.com/ethereum/EIPs/issues/994)\), compose NFTs into hierarchical ownership schemes \([ERC-998](https://github.com/ethereum/EIPs/issues/998)\), for fractional ownership of NFTs \([ERC-1633](https://github.com/ethereum/EIPs/pull/1633)\) and other innovations.

Although there is no single standard for NFTs across different blockchain networks, ERC-721 provides the canonical definition for an NFT interface standard.

####  Metadata

There are various well-established formats for describing and processing metadata about digital resources. The most widely adopted is the [Resource Description Framework](https://www.w3.org/RDF/) \(RDF\). Mainstream translations of this framework have been made into programming languages such as Javascript \(JSON\).

Metadata properties are becoming standardised in open schemas, such as [schema.org](https://schema.org/), which enables information about web resources to be structured in a way that is semantically understood and machine-readable. With [linked-data](https://www.w3.org/wiki/LinkedData) models, such as [JSON-LD](https://json-ld.org/), metadata is becoming more structured and graph-based.

This means that now when we describe a resource, such as a _dataset_, in its context of [schema.org/dataset](https://schema.org/Dataset), everyone can have a shared understanding of what is represented by the resource description.

This approach can be used to describe any conceivable representation of a resource. We should also be able to localise resource descriptions, for these can be widely understood, regardless of a user’s language.

## 2. Use Cases

Each use-case presents the canonical form of a non-fungible token and the types of resources the token metadata describes. A comparison with legacy ways of describing and using resources helps illustrate the distinctive properties of these tokens and how these enable applications to be built which have not previously been possible. Examples are provided as links, which the link owner may choose to describe in their own terms, using their own resources.

Note: These use-cases and examples are not exhaustive and are only intended to provide a high-level overview for an initial scope of requirements for drafting Internachain NFT and Metadata standards. This list of use-cases and examples is expected to grow. Naming use-case as types of NFTs suggests a taxonomy for NFT classes of NFTs. This taxonomy should further evolve, as the use cases are populated with new examples and as new use-case classes are discovered which don’t fit this initial list.

### 2.1 Collectible Tokens

Collectible Tokens contain unique digital objects which people desire to own. These tokens enable control over the digital objects and infer rights of ownership and usage. Owning a digital collectible may confer further rights and capabilities within a specific system, or across systems such as virtual gaming worlds.

Collectible Token metadata may be self-describing, with the digital object being the same as the metadata resource, or it may describe a digital resource which can be accessed within a specific domain space. Digital Collectibles were the original conception of Non-Fungible Tokens.

Digital collectible objects have physical world analogies in the form of collectibles such as baseball cards, but the virtual universe of digital objects is much larger and more diverse.

  
Tokenizing collectible digital objects enables these to be owned and traded in virtual marketplaces. Collectible Tokens are being used in an increasing range of virtual world games and simulations. New and secondary sales of digital collectibles are generating valuable new online marketplaces.

Examples: [Cryptokitties](https://www.cryptokitties.co/),

### 2.2 Financing Tokens

Financing Tokens contain real-economy financial claims and agreements. These may be associated with rights of payment for the delivery of commodities and services, and rights to receive these as agreed.

The metadata associated with Financing Tokens describes financial claims and related documents, such as invoices, delivery notes and receipts.

Tokenizing financing enables the documentary evidence and associated rights associated with financing deals to be used as collateral for securing capital loans and to issue payment guarantees.

Examples: [Centrifuge](https://centrifuge.io/), [Persistence One](https://persistence.one/),

### 2.3 Impact Tokens

Impact tokens contain proofs about the social, environmental and economic state of the world. These tokens have intrinsic value linked to verifiable claims, outcome payments, executable rights and data assets. Impact tokens of various types may be issued, sold and traded as digital commodities. Carbon Credit Tokens are an example of Impact Tokens which are issued on the basis of verified Carbon Emission Reduction claims.

Impact Token metadata describes the information which is used to measure, verify and report on impacts. This is recorded in a stateful graph for comparing and attributing impacts over time, relating impacts across systems and to represent desired future state outcomes.

Legacy mechanisms for recording claims of impact mostly use analogue methods, with reliance on trusted intermediaries to generate documentary reports. Some types of impact are recognized by central authorities who issue certificates that are referenced in centralised registries and traded over-the-counter.

Tokenizing impact claims and their verification proofs makes it possible to more precisely account for and place economic value on impacts. This provides critical information for financing and implementing all types of interventions for sustainable development, ecological regeneration and mitigating climate change.

Examples: [ixo](https://ixo.foundation/), [Regen Network](https://www.regen.network/),

### 2.4 Access Tokens

Access Tokens contain rights to use proprietary physical or virtual resources for specified purposes. These rights may be transferable or non-transferable, perpetual or time-limited.

The metadata of an Access Token describes a proprietary resource and its associated terms of use. It may include a digital key that removes usage restrictions or provides authorisation.

Legacy mechanisms to access proprietary resources are typically dependent on intermediary processes to assign, transfer and operationalise rights of usage, based on terms such as membership, ownership and rental. Digital locks for virtual resources and embedded into physical objects now make it possible to virtualise, embed logic and build financial transactions into all types of access mechanisms.

Tokenizing access rights makes it possible to distribute access rights in more targeted, decentralised and distributed ways. Access may be created or restricted for more types of resources. This can impose limitations on unsustainable over-use of resources, or expand the possibilities of how resources can be shared and used most optimally.

Examples: [IrisNet](https://www.irisnet.org/), [Decentraland](https://decentraland.org/),

### 2.5 Art Tokens

Art Tokens contain the rights to a registered patent or copyright material. These rights may be protected by intellectual property laws.

Art Token metadata describes the art, which may be patented or copyright physical or virtual materials, together with associated licenses and claims.

{Legacy IP assets}

Tokenizing art makes it possible to determine its provenance, trade ownership of art \(with or without physical transfers\), finance the creation of new art or inventions and to license the use of this property in a wider range of applications.

 Examples: [Left Gallery](https://left.gallery/), [Molecule](http://www.molecule.io/)

### 2.6 Physical Property Tokens

Physical Property Tokens contain digital representations of physical-world objects and resources. They may infer rights of ownership, control and usage of physical property.

Physical Property Token metadata describes the physical property and digital representations of this property, with links to related documentation such as title deeds, certificates of ownership and other claims about the property. Digital representations of physical property may be linked by embedded identifiers, such as decentralised identifiers, unique serial numbers and biometric identifiers.

Legacy forms of representing physical property include physical or electronic certificates and title deeds, which may be difficult to authenticate and are susceptible to forgery, duplication and loss of records.

Tokenizing physical property makes this available to be used in digital transactions, as collateral and for new types of derivative products and services. Proof of ownership and fractionalised ownership are more feasible. The transaction costs and administrative time of transferring ownership may be dramatically decreased. The provenance, credentials and chain of custody of physical property can be proven. All types of verifiable claims and rights may be associated with the property. Tokenization may reduce counterfeiting by enabling more robust identification and authentication of physical property. It provides new ways of communicating about and organising the use of physical property. This is seen as an important enabler for the sharing economy.

Examples: [Mattereum](https://mattereum.com/),

### 2.7 Data Tokens

Data Tokens contain data assets. These tokens are associated with rights of ownership of data assets and the licenses to use these assets for specific purposes.

Data Token metadata describes data resources, with information about the location and access rights to the data.

Legacy data storage and retrieval systems restrict access and usage of data, to ensure data security and privacy. This traps valuable data in silos and has also had the effect of centralising control and ownership of data by large corporations which have the commercial and technological powers to source, store and process large amounts of data.

Tokenizing data assets makes it possible to create new types of data marketplaces for securely sharing data assets, with automated access control mechanisms. This should democratise market participation and access to big data, which is particularly important for building artificial intelligence capabilities which are not exclusively controlled by large corporations.

Example: [Ocean Protocol](https://oceanprotocol.com/)

### 2.8 Credential Tokens

Credential Tokens contain verifiable claims about the identity and attributes of a subject. The issuers of these claims can be identified and authenticated. The subject of a credential token may have certain rights in specific contexts, which are not available without the credential.

Credential Token metadata describes one or more verifiable claims about an identified subject.

Legacy credential systems require trusted issuers of credentials to maintain a persistent central registry of information which relying parties can access. Analogue or digital credential certificate documents have traditionally been used to represent and operationalise the rights associated with credentials.

Tokenizing credentials enables identity and rights associated with having certain attributes to be authenticated and used in a wider range of physical and virtual contexts.

Examples: [Starname](https://starname.me)

### 2.9 Capability Tokens

Capability Tokens contain electronic rights within software systems. These tokens transfer Object Capabilities, which are authorisations to perform restricted scopes computational processes that get executed at the level of a software operating system.

Capability Token metadata describes object capabilities in object-oriented code.

Legacy software systems do not restrict at a granular level the scopes of computational processes or authorisations which can be implemented across non-concurrent systems. This creates security vulnerabilities and limits the capability to communicate and execute code across systems.

Tokenizing capabilities makes it possible to own a unique object capability and to transfer ownership and/or control of the rights which are associated with this. It makes possible {...tbc}.

Examples: [Agoric](https://agoric.com/)

### 2.10 Commodity Tokens

Commodity Tokens contain information about the identity and origin of commodities.

Tokenizing commodities enables consumers to verify the provenance of a commodity and increases transparency in the commodity supply chain.

{...tbc}

Examples: [Provenance](https://provenance.org), 

## 3. Requirements

The canonical use-cases for NFTs and Metadata have a set of common business and technical requirements. Each use-case relies on a subset of these requirements to be met.

The requirements for Interchain NFTs include that these should be:

1. **Mintable** to issue new tokens of the same class to a token set.
2. **Burnable** to remove tokens from the token set.
3. **Ownable** to control the token metadata using a private key.
4. **Transferable** to change ownership.
5. **Non-transferable** to not permit changes in ownership.
6. **Lockable** to conditionally stop changes in the token metadata.
7. **Immutable** to never permit changes in the token metadata.
8. **Mutable** to unconditionally permit changes in the token metadata.
9. **Fractional** to mint fungible tokens which represent fractional ownership of non-fungible parts.
10. **Composible** to be owned by another non-fungible token and added to that token’s set or to produce other novel combinatorial forms.
11. **Conditional** to only permit changes or transfers when specific conditions have been met.

|  | **Requirements** |  |  |  |  |  |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Use-Case** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** | **10** | **11** |
| Collectible Tokens | X |  | X | X |  | X | X | X | X |  |  |
| Financing Tokens | X | X | X | X | X | X | X | X | X | X | X |
| Impact Tokens | X | X | X | X | X | X | X |  | X | X | X |
| Access Tokens | X | X | X | X | X | X | X | X | X | X | X |
| Art Tokens | X |  | X | X |  |  | X | X | X | X | X |
| Physical Property Tokens | X | X | X | X | X | X | X | X | X | X | X |
| Data Tokens | X | X | X | X | X | X | X | X | X | X | X |
| Credential Tokens | X | X |  | X | X |  | X |  |  | X | X |
| Capability Tokens |  |  |  |  |  |  |  |  |  |  |  |
| Commodity Tokens | X | X | X | X | X | X | X | X | X | X | X |
|  |  |  |  |  |  |  |  |  |  |  |  |

## 4. User Stories

Projects are invited to describe their use-case in the format of a short User Story. This must emphasise the unique challenges and distinctive requirements which must be met by the Interchain Standard for NFTs and Metadata. This includes edge-cases which can be helpful for testing the validity and potential limitations of these standards. To propose new user stories by submitting a Github Pull Request on this document.

### 4.1 Quality Carbon Credits

#### Context
As pressure mounts to balance the yearly global carbon budget due to increasing risk to life, property and markets due to climate related 

Carbon accounting, markets and politics.
Long lobbied by scientists and citizen groups, corporations and governments are finally taking climate related risk seriously.  As voluntary and compliance markets for carbon, corporate science based reporting, emissions taxes and other mechanisms become more common, the demands for carbon accounting integrity become more challenging to meet.  

Carbon accounting and science:
Carbon accounting should follow the natural carbon cycle. Emissions (respiration) and sequestration (inspiration). The global carbon budget must not simply be brought to net zero as quickly as possible, it must also achieve a carbon negative balance for some time to bring us back to pre-industrial levels if we want to guarantee conditions conducive to biosphere functioning as humans have evolved.  

Carbon accounting and markets.
There are three major types of carbon credits.  
Avoided emissions (a factory spent money to increase efficiency and can claim credits as they reduce emissions).
Renewable Energy Credits (a city shifts from fossil fuel based energy to renewable energy and claims credits associated with the quantification of carbon emissions reduction)
Natural carbon or “living carbon” which is incapsulated by “terraculture” and “mariculture” (AFOLU: Agriculture, Forestry and other Land Use) and Blue Carbon in which sequestration and/or maintenance of carbon stocks in living systems is monitored and quantified.

Living Carbon User Story:

User Story One: Interchain credit transfer

Acme Ag and their ecosystem of farmers, processors, and logistics providers, would like to meet the ambitious goals of carbon neutrality by 2030, and even explore if providing carbon credits to industries that cannot hope to achieve carbon negative operations (such as the energy sector), could become a long term profit center.

Acme ag wants to be able to have accurate carbon reporting internally, as well as participate in markets to buy and sell carbon credits to ensure year over year they can meet carbon accounting goals 1st and position themselves to be a provider of carbon to the market they believe is coming, in partnership with their farmers.

Farmer Jane provides produce to Acme ag.  She would like to add carbon credit sales to her list of produce.  In addition to Acme there are also several other marketplaces forming and Jane wants to be able to find the best possible price for her carbon with the least amount of work.

A start up carbon market (Market1) approaches her with an easy monitoring and verification onboarding scheme and upfront payment in exchange for her carbon.  She accepts because she needs the cash.  Market1 is running as a smart contract in an Ethereum state channel.  

Acme ag partners with a second marketplace (Market2) which has a higher price, and a different and more rigorous verification threshold. Jane second guesses her decision and registers on Market2 as well as Market1.

The first round of carbon credits have already been issued. The transition of carbon from Market1 to Market2 requires running additional data collection and uses a different quantification algorithm that is considered by many to be more rigorous and has less uncertainty.  Market2 is running on a cosmosSDK chain.  

Acme ag agrees to underwrite the cost of additional verification.   

Acme ag does not want Farmer Jane's geolocation to be public and desires that this data be kept private and only available to approved monitors and verifiers in the system because they are worried about a competing company poaching their high preforming farmers

#### User Needs
Acme Ag demands that there be no counter carbon claims on the farm in question
Acme Ag demands ability to audit and hold seller liable for double counting
Farmer Jane requires access to multiple markets
Farmer Jane requires monitoring and verification costs to be shouldered by purchaser
Market1: Need to be paid back for the carbon they prepurchased
Market2 Needs to be able to burn or represent the movement of that carbon to market2 Needs to be able to represent the provenance of the carbon in question (both geolocation and the fact it moves from a different registry)
Market2 Needs to be able to update the claim with the new methodology but maintain consistency in the time period and geolocation of the claim

#### Unique Challenges

Carbon markets have four major accounting concerns:

Additionality: “Who has the right to account for the carbon mitigation or sequestration” in some markets you must not only prove that the carbon was not emitted, but also that if you were not paid it WOULD have been emitted (I call this the carbon hostage approach to additionality).  Multiple parties must be able to claim responsibility accurately and with integrity so that the right party(ies) has(ve) the right to claim the carbon.

Permanence: “How long will this carbon be sequestered, or stored?”  In living carbon claims permanence is variable dependent on conditions such as droughts (which force emissions) rainfall (which increases sequestration) that are beyond human control, as well as activities (land use practices) which are within human control. This creates complexity. It is essential to have global carbon buffer pools to cover permanence issues from both human causes and natural caused reduction of carbon stocks. This requires some fungibility.  

Leakage: “Does this change create a carbon emission increase somewhere else”. For instance does forest conservation in one place cause a forest somewhere else to be cut down? Ability to link credit claims to a larger system of carbon accounting (transport, etc) are important.  Ability for counter claims are important.  

Uncertainty: “How sure are we about the monitoring and quantification methodology that is under the hood of the carbon credit in question”.  There is always some uncertainty as this is a probabilistic science, especially with living carbon credits.  Metadata associated with the evidence backing a credit, the specific threshold of “verification”, and clear statements of uncertainty are required.  

#### Distinctive Requirements

### 4.2 Financing commodity trade deals

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.3 Crowd-sourced funding for Pharmaceutical Patents

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.4 Primary Education Impact Bond

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.5 Private Credentials

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.6 Blockchain Transaction Receipts

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.7 Media IP & Distribution

#### Context

#### User Needs

#### Unique Challenges

#### Distinctive Requirements

### 4.8 Resellable Theatre Tickets

#### Context
As COVID restrictions are lessened in their area, Ellenor and Vicki have decided that they want to try to go to their town theatre’s reopening screening of The Phantom of the Opera. After reviewing the theatre’s COVID plan they decide that they are comfortable giving the experience a shot so Ellenor goes to Nearest Town Theatre’s web page to purchase two tickets for the upcoming play. 

Ellenor goes to Nearest Town Theatre’s web page, clicks the “Purchase” button and is taken to the ticketing agency, Nearest Town Ticketing Agency’s, web page who have been given the rights to sell tickets for Nearest Town Theatre along with a set of rules specified by the theatre which detail the COVID seating requirements. Due to these COVID restrictions, Ellenor finds she must reserve specific seats in the theatre to allow for proper spacing of groups. She selects two seats on the aisle about midway back in the theatre and clicks “Complete Purchase” where she is taken to a page requesting payment. 

Here Ellenor is greeted by a page which allows her to select any of the payment options that Nearest Town Ticketing Agency has chosen to accept. Once payment information is submitted, the payment is swapped with the tickets so that in one atomic exchange Nearest Town Theatre receives the payment in question, Ellenor receives the tickets and Nearest Town Ticketing Agency receives their cut of the payment as specified in their contract with Nearest Town Theatre.

As the date of the show approaches, Ellenor has a family emergency come up which is going to prevent her from attending. Ellenor gives Vicki her ticket, as Vicki has previously paid Ellenor in cash for hers, but as money is tight Ellenor tells Vicki that she would, ideally, like to sell her ticket to someone that Vicki would want to go with in her stead. Ellenor creates an offer which gives Vicki the ability to initiate the sale of the ticket to a third party so that when Vicki finds someone that agrees to the price she can send the ticket offer to the found third party. When creating the offer, Ellenor is notified when she selected “Resale” on the ticket that Nearest Town Theatre has restricted the resale price to only allow for resale at the face value sale price of the ticket or below. 

Vicki asks her friend, Stephen, if he is amenable to going and he agrees to pay Ellenor the face value of the ticket with an addendum that he would only want to go if they can sit closer to the stage as he saw that Lin-Manual Miranda was making a cameo appearance and wants to make sure to have a good view. Vicki agrees to this seat change and they both look up the current seat map for the show, deciding on two seats in the second row. As Stephen receiving the ticket is the current limiting factor to show attendance, Vicki first modifies the offer Ellenor gave her and adds a condition specifying that, as part of the third party sale of the ticket a seat change needs to occur. After which Vicki sends the new offer to Stephen, who also modifies the offer, adding a requirement for the purchase that his seat is also changed. 

Ellenor is notified of the proposed changes to the offer and as changing seats does not affect Ellenor’s desire to sell the ticket, she approves the modified offer and this triggers the beginning of the resolution process. First, both Vicki and Stephen are notified that the changes to the offer have been accepted and they are prompted to select the seats which they would like to change to. After they both select their desired seats, Nearest Town Ticketing Agency provides an assurance that the specified seats will be held pending the completion of the ticket sale to Stephen. Once this is complete, Stephen is asked to submit payment to Ellenor in any of the ways she has advertised in the offer. He selects the one he is most comfortable with and submits the payment to be held and released to Ellenor in an atomic swap for the ticket. Once both the seating changes and Stephen’s payment has been submitted, all three items, the ticket to Stephen, the payment to Ellenor and the two seat changes, are exchanged simultaneously. 

On the day of the show, Vicki and Stephen decide on a last minute whim to try and change their seats again. However, this time when they go to request the change they are notified that seats cannot be changed within 24 hours of the show. Despite this they both arrive at the play that night, present their tickets at the ticketing counter and enjoy the play. 

#### User Needs
User needs here are broken down for each of the three users presented in the above story: Ellenor, Vicki and Stephen. 

__Ellenor__
* Mechanism for submitting payment digitally
* Digital storage and display mechanism to store the received tickets
* Mechanism to transfer the tickets to a third party without payment for the ticket
* Mechanism to transfer the tickets to a third party with payment for the ticket
* Ability to give/sell an option to another party
* As well as revoke said option
* Digital Ticket received must specify assigned seat in a human readable format for use at the venue

__Vicki__
* Implied allowance (through initial purchase) for Ellenor to hold her ticket
* Digital Wallet with which to receive the ticket from Ellenor
* Ability to hold the offer given by Ellenor
* Ability to share offer with third party
* Ability to present the ticket at the play
* Ability to give the right to change her seat to Stephen

__Stephen__
* Digital Wallet to receive the initial “ticket offer” from Vicki
* Ability to create a counter-offer with different conditions from the original
* Ability to provide payment in response to fulfill “ticket offer”
* Ability to receive the ticket in his digital wallet
* Ability to present the ticket at the play

#### Unique Challenges
Here the primary unique challenge, outside of the expectation of all parties being onboarded to and using some form of digital wallet (or other digital storage) which can hold the specified data objects, is the handling of the transfer of the play ticket from Ellenor to Stephen with Vicki acting as an intermediary for the transaction. There are a few interesting things happening in this story. 
* First Ellenor providing an offer which allows Vicki to act as an intermediary with Ellenor never needing to know who exactly the ticket is being resold to
* Next Vicki being able to modify the offer to add a condition that she must be allowed to complete a change in seat for the purchase to go through. Here Vicki is a third party to the actual sale of the ticket adding a sale requirement to the offer. 
* Finally Stephen being able to modify the offer in the same way as Vicki
Once the offer modifications happen it then must be ensured that Vicki and Stephen get to choose their seat change after the final offer is accepted by Ellenor and the subsequent atomic transfer of all parties needs: Ellenor gets her money, Stephen gets his ticket and both Vicki and Stephen get their new seat. 

__Metadata Requirements:__ Mintable, Burnable, Ownable, Transferable, Lockable, Mutable, Conditional 

#### Distinctive Requirements
* Delegate the right to initiate a contract handshake to another party
* Resolve an outstanding contract between two entities that have not interacted prior to the attempted contract resolution
* Atomic transfers that satisfy the simultaneous conditions of multiple parties
* Utilization of third parties (though maybe limited to involved third parties, e.g. the ticketing agency) to fulfill/verify conditions placed on a contract

#### NFT Metadata Layer Model
| Layer |  |
|-----|------|
| **8. Operationalization** | At ticketing, Vicki and Stephen each present a QR code representing their ticket to a scanner in the theatre lobby. Lights illuminate a path to their seats and the tickets are recorded as used. |
| **7. Assertions** | TicketAdvisor claims performances through the month of December 15 will have a cameo by Lin-Manual Miranda. [??? is this part of this scenario or is there a better assertion] | 
| **6. Extensions &    Restrictions to Rights** | Seats changed to B16 and B18. Seat changes after December 14 at 8PM are no longer allowed. | 
| **5. Instantiation** | Two tickets to see Phantom of the Opera at 8 PM on December 15, 2020, seats D24 and D26, respectively. (Two separate tokens) |  
| **4. Embodied Rights** | Theatre Ticket: Right to attend and be seated at a particular performance, at a particular venue, at a particular time. Seats are changeable if alternative seats are available. |
| **3. Token Logic** | Resellable Bearer token | 
| **2. Interchain** | Atomic transactions guarantee all transfers happen simultaneously: payment to Ellenor, transfer of ticket to Stephen, and change of both seats | 
| **1. State Machine** | Stephen pays Ellenor via bitcoin. Ticketing is on Ticket Chain, Payments are on MoneyChain (which has fiat onramps / offramps) |

## 5. References


---
## History

Oct 19, 2020 - Initial early draft (not informed by consensus)



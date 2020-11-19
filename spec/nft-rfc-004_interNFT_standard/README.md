---
nft-rfc: 4
title: interNFT standard
stage: draft
category: NFT/INTERFACE
kind: interface
author: Deepanshu Tripathi @deepanshutr
created: 2020-11-19
modified:
---

## Synopsis

This standard describes a set of interfaces that can be utilised to build an inter-chain non-fungible token implementation.

InterNFT is a natively implemented NFT structure for Blockchain applications that implement interoperability protocols. The interNFT is defined by a basic interface that any NFT structure has to implement to be called an interNFT. The ownership of interNFT is maintained by the interNFT wallet. The combination of interNFT and interNFT wallet allows the ownership of the interNFT to be exchanged across interoperable chains while the execution logic of the NFT is still maintained at the native chain.

### Motivation

The current set of common NFT definitions are dominated by the [ERC721](https://eips.ethereum.org/EIPS/eip-721) interface definitions which are biased towards smart contract-based definitions of NFT. A chain app code native definition of NFT may not necessarily be bound by the restrictions that a smart contract definition of NFT will be, allowing for the interface to be made simpler while adding more native implementation relevant methods. Also, the smart contract-based approach for NFT implementation does not account for a common native wallet that may hold ownership representations of multiple NFT implementations and allow for a singular transfer NFT ownership transaction implementation.

The main motivation of the standard is to:
* Define an inter-chain NFT interface that all data structures must implement to be classified as an interNFT and an interNFT wallet interface that can hold the ownership of all such interNFT implementations for an account.
* Define a base implementation of the interNFT and interNFT wallet interfaces method signatures with mint, mutate metadata and burn transactions for base NFT and ownership transfers for the base NFT wallet implementation.
* Define a metadata interface to maintain the interNFT metadata. This interface may further be utilized for storing metadata for objects from other datastructures too.
* Extend the transfer interNFT functionality of the base interNFT wallet implementation to define packet data structure, app logic and encoding for interchain interNFT ownership transfers and define the ICS specification.

This will allow all projects in the inter-chain ecosystem to:
* Define their own implementation of interNFT structures with custom mint, mutation and burn transaction logic maintained at their app chain.
* Have a common wallet implementation for all interNFT implementations which can hold ownership information of multiple kinds of interNFTs from multiple chains in a single wallet for an account.
* Natively send the ownership of interNFTs across chains through inter-chain communication protocols without a requirement for permissioned bridges or token transformation/pegging.

### Definitions

* `interNFT`: An implementation of the `NFT` interface. The `interNFT` is defined to allow for maximum application logic flexibility in one interface and is focused on interchain ownership transfer. In this document `interNFT` will also refer to a basic interface, implementation of which will classify a structure as an `interNFT`

* `classification`: a representation of the type or grouping for an `interNFT`, e.g. an `interNFT` "Toyota Corolla" will be of `classification` car.

* `trait`: a charectersitic/variable related to an `interNFT` defined by `classification` e.g. "top speed" can be a `trait` of `classification` car.

* `signature`: a cryptographic signature using a private key on bytes of information. A signature can be verified against the public key of the signing private key and sign bytes. 

* `fact`: a piece of information. A `fact` can carry `signature`s from `account`(s) e.g. "100 mph (ca. 161 km/h)" is a fact and an `account` can attest it by signing it with their private key.

* `property`: the value of a `trait` is `property`. Every `property` has a `trait` identifier and a corresponding fact `fact` e.g. 

* `account`: a singularly identifiable identity of each actor on the application. An `account` is generally identified by a public key.

* `maintainers`: a group of one or more accounts that can issue and mutate `properties` of a `classification` of `interNFT`

* `interNFT wallet`: a mapping of a set of `interNFT ID`s against an `account` ID. An `interNFT wallet` specifies the `interNFT`s owned by and an account.

* `height`: the block height of the chain. Used as a measure of time for `interNFT` time-bound operations.

* `lock`: the `height` after which the `interNFT` is allowed to be transferred out of an `interNFT wallet`. 

* `burn`: the `height` after which the `interNFT` is allowed to be burned/redeemed by the owner of the `interNFT`. 

* `interNFT ID`: A reference to the `interNFT` specifying the hash of the NFT Immutable, the address of the originating chain, and the class of the NFT. The address is convertible to a String for reference.

* `immutables`: `trait`s of the `interNFT` that do not change after being issued. The hash of these properties is a  part of the NFT Address( `interNFT ID`).

* `mutables`: `trait`s of the `interNFT` that can be changed through transactions defined on it.

### Desired Properties

**Standard ownership transfer logic**
The overall NFT functionality is split into two objects, the NFT, and NFT wallet. NFT object handles the mint, mutation, and burns logic with the NFT wallet object handling the ownership transfers. Both objects can operate independently on different chains.

**Singular representation/instantiation**
The NFTs are addressed by the same hash of the immutable properties, enforcing singular representation/instantiation of NFT across chains.

**Singular wallet implementation**
NFT wallet object implements the wallet and transfer logic and is agnostic to other custom logic associated with the underlying NFT implementation allowing for a singular wallet implementation for all the defined NFT interface.

**Implementation flexibility**
The NFT interface implementation must allow for all the basic functional requirements of an NFT with no restrictions on the extension of the functionalities to account for more complex application logic, as long as the implementation satisfies the NFT interface.

**Reduce load/dependence on inter-chain protocol**
The two objects comprising the NFT functionality, NFT & NFT wallet sould not need to communicate with each other to sync their state at each transaction. They MUST function independently only with a few transactions requiring dependence on the inter-chain protocol(interchain send, burn transactions).

**Commodification**
All the NFTs are represented with a class or classification allowing for transactions to address NFTs though classes instead of direct addresses and hence allowing for NFT commodification.

**Trusted minting, mutation and burn execution and Interoperability with private chains**
The minting, mutation, and burn logic is implemented natively on the issuing chain and is always handled by the same chain instead of handing over the mutation logic to the recipient chain on an NFT ownership transfer. This allows for private and privately validated chains to also exchange their NFTs with other chains while ensuring the execution environment trust and logic privacy(if required).

**Native implementation and interoperability**
The NFT module is implemented at the native chain application logic level instead of at the Smart Contract level, leveraging the chain’s native interoperability protocols to transfer NFTs between chains instead of permissioned bridge Smart Contracts. The basic interface and functionalities of the NFT may be extended by smart contracts to allow for more complex application logic.

## Technical Specification


####  InterNFT interface 

An interface that implements the NFT interface, adding interoperability functionalities to it 

InterNFT interface {

    // Implementing the NFT interface
    NFT

    // ChainID returns the idendtifier, for the NFT's native Chain, as an ID interface
   ChainID() ID

    // HashID return the identifier, for the immutable properties of the InterNFT, as an ID interface
   HashID() ID

    // MaintainersID returns the identifier, for the maintainer froup of the InterNFT, as an ID interface
   MaintainersID() ID

    // Properties returns the properties of the interNFT as a properties interface
   Properties() Properties

    // CanSend returns a boolean telling if the interNFT can be sent or not given the current height
   CanSend(Height) bool

    // CanBurn returns a boolean telling if the interNFT can be burnt or not given the current height
   CanBurn(Height) bool
}

#### Height interface

An interface to define a block height type for a chain, used as a metric of time.

{
    Height interface {

    // Count returns the block count for the Height
   Count() string

    //Current height 
    // IsGraterThat returns a Boolean to tell if the Height is grater than a given Height/Current Height
   IsGraterThat(Height) bool
}

#### Signature interface 

An interface for any type that represents a cryptographic signature that can be verified

Signature interface {

    // String returns the human-readable string format of the Signature
   String() string

   // Bytes returns the byte array of the cryptographic signature 
   Bytes() []byte

    // ID returns the identifier for the Signature as an ID interface
   ID() ID

   // Verify returns a boolean to tell if the signature is valid of not given the public key of the signer and the signed bytes
    Verify(PublicKey, []byte) bool

    // HasExpired returns a boolean to tell if the Signature has expired given a Height/Current Height interface
    HasExpired(Height) bool
}

#### Signatures interface 

An interface for a container of a collection of Signatures. The Interface handles the deterministic operations on the Signature collection.  

Signatures interface {

    // Get returns a Signature stored in the Signatures given an Identifier for it
   Get(ID) Signature

    // Add appends a given Signature with the Signatures Collection
   Add(Signature) error
   // Add removes a given Signature from the Signatures Collection
   Remove(Signature) error
   // Add mutates a given Signature in the Signatures Collection
   Mutate(Signature) error
}

#### Fact interface 

An interface to define a type for any kind of information is the system which is non-consequential to the application logic but has to be stored for provenance. 

Fact interface  {

    // String returns the human-readable string format of the information stored by the Fact
   String() string

   // Bytes returns the byte array of the information contained by the Fact
   Bytes() []byte

    // Signatures return the cyptographic signatures on the Fact as Signatures interface 
   Signatures() Signatures
}

#### Property interface

An interface to define any kind of property associated with an interNFT

Property interface {

    // Name returns the name of the Property
   Name() string

    // ID returns the identifier, of the Property, as an ID interface
   ID() ID

   // Fact returns the Fact associated with the Property
   Fact() Fact
}

#### Properties interface 

An interface for a container of a collection of Properties. The Interface handles the deterministic operations on the Property collection.  

Properties interface {

    // ID returns the identifier, of the Properties, as an ID interface
   Get(ID) Property

    // Add appends the given Property with the Properties collection 
   Add(Property) error
   // Add removes the given Property from the Property collection
   Remove(Property) error
   // Add mutates the given Property in the Property collection
   Mutate(Property) error
}

#### Properties interface 

An interface for any type of Trait associated with a Classification of interNFT 

Trait interface {

    // Name returns the name of the Trait
   Name() string

   // ID returns the identifier, for a Trait, as an ID interface
   ID() ID

    // IsMutable returns a Boolean to tell if a property value of Trait can be mutated or not
   IsMutable() bool
}

#### Traits interface 

An interface for a container of a collection of Traits. The Interface handles the deterministic operations on the Trait collection. 

Traits interface {

    // Get returns a Trait for the given ID
   Get(ID) Trait
}

#### Classification interface 

An interface for a representation of type/class/denomination of the interNFT

Classification interface {

    // Name returns a human redable name for the classification
   Name() string

    // ID return the identifier, for the classification, as an ID interface
   ID() ID

    // Traits returns the traits associated with the Classification
   Traits() Traits
}


## Backwards Compatibility

This interface definition backwards compatible with the NFT interface defined in nft-rfc-003

## Forwards Compatibility

Not applicable

## Example Implementation

TBD

## Other Implementations

* PersistenceSDK assets module https://github.com/persistenceOne/persistenceSDK/tree/master/modules/assets

## References

1. William Entriken, Dieter Shirley, Jacob Evans, Nastassia Sachs 2018.ERC-721 Non-Fungible Token Standard. Retrieved from https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md

## History

2020/11/19 - First Draft

## Copyright

All content herein is licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).

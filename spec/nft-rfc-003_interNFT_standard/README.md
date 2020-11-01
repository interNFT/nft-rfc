---
nft-rfc: 3
title: interNFT standard
stage: draft
category: NFT/INTERFACE
kind: interface
author: Deepanshu Tripathi @deepanshutr
created: 2020-11-02
modified:
---

## Synopsis

This standard describes a set of interfaces that can be utilised to build an interchain non-fungible token.

NFT or Non Fungible Tokens refer to a wide category of data structures with the majority of the standards being defined for Smart Contract implementations. When defining an NFT structure at the native chain code level there are currently no basic NFT interfaces that a type can implement to be classified as an NFT structure. Also, the NFT definitions at the Smart Contract level account for handling the ownership of the NFTs at the Contract level, with no common definition of a wallet which can be used to represent the account ownership for different NFT implementations.

This project aims to define a very basic NFT interface with a minimum set of methods that all NFTs have in common and define a wallet interface to represent the account ownership of the NFTs. The project also aims at defining a base implementation of the NFT and NFT wallet interfaces with create, mutate metadata, change ownership, burn NFT transactions and interchain NFT ownership transfers transaction through the IBC protocol.

### Motivation

The current set of common NFT definitions are dominated by the [ERC721](https://eips.ethereum.org/EIPS/eip-721) interface definitions which biased towards smart contract-based definitions of NFT. A chain app code native definition of NFT may not necessarily be bound by the restrictions that a smart contract definition of NFT will have to, allowing for the interface to be made simpler while adding more native implementation relevant methods. Also, the smart contract-based approach for NFT implementation does not account for a common native wallet that may hold multiple kinds of NFTs and allow for a singular transfer NFT transaction implementation.

The main motivation of the standard is to:
* Distill down a very basic NFT interface that all data structures must implement to be classified as an NFT and an NFT wallet interface that can hold the ownership of all such NFT implements for an account.
* Define a base implementation of the NFT and NFT wallet interfaces as modules with mint, mutate metadata and burn transactions for base NFT and transfer ownership transactions for the base NFT wallet implementation.
* Define a metadata module to maintain the metadata kvStore utilized for storing the NFT metadata. This module may be further utilized for storing metadata for objects from other modules too.
* Extend the transfer NFT functionality of the base NFT wallet implementation to define packet data structure, app logic and encoding for interchain NFT ownership transfers and define the ICS specification.
* Produce tutorials and documentation around the interfaces and base modules to operate, compose with other modules and extend/implement the definitions.

This will allow all projects in the interchain ecosystem to:
* Define their own implementation of NFT structures with custom mint, mutation and burn transaction logic maintained at their app chain.
* Have a common wallet implementation for all NFT implementations which can hold ownership information of multiple kinds of NFTs from multiple chains in a single wallet for an account.
* Natively send the ownership of the NFT across chains through IBC without a requirement for permissioned bridges or token transformation/pegging.

### Definitions

* `NFT`: An NFT or a Non-fungible Token is a structured unit of data that represents the properties of a unique entity, or the entity itself( if it’s a digital asset and all its properties are contained by the NFT). In this document `NFT` will also refer to a basic interface, implementation of which will classify a structure as an `NFT`.

* `NFT ID`: A reference to the `NFT`. The address is convertible to a String for reference.

* `NFT Wallet`: an array of references(`NFT ID`) to Account ID.

* `NFT Classification ID`: an identifier of the type or denomination of the NFT.

* `NFT Metadata`: any metadata related to the NFT. It is defined by an `ID`, `Value` and `Type`

### Desired Properties

**Standard ownership transfer logic**
The NFT functionality is split into two modules, the NFT, and NFT wallet modules. NFT module handles the mint, mutation, and burns logic with the NFT wallet module handling the ownership transfer transactions. Both modules can operate independently on different chains.

**Singular representation/instantiation**
The NFTs are addressed by the same hash of the immutable properties, enforcing singular representation/instantiation of NFT across chains.

**Singular wallet implementation**
NFT wallet module implements the wallet and transfer logic and is agnostic to other custom logic related to the NFTs allowing for a singular wallet implementation of all the NFT types.

**Implementation flexibility**
The NFT module implements all the basic functional requirements of an NFT with no restrictions on the extension of the functionalities to account for more complex application logic, as long as the implementation satisfies the NFT interface.

**Reduced load on interchain protocol**
The three modules comprising the NFT functionality, NFTFactory, Wallet, and Metadata, do no need to communicate with each other to sync their state at each transaction. They function pretty independently only with only a few transactions requiring inter-chain operability(interchain send, burn transactions).

**Commoditization**
All the NFTs are represented with a class or classification allowing for transactions to address NFTs though classes instead of direct addresses and hence allowing for NFT commoditization.

**Trusted minting, mutation and burn execution and Interoperability with private chains**
The minting, mutation, and burn logic is implemented natively on the issuing chain and is always handled by the same chain instead of handing over the mutation logic to the recipient chain on an NFT transfer. This allows for private and privately validated chains to also exchange their NFTs with other chains while ensuring the execution environment trust and logic privacy(if required).

**Native implementation and interoperability**
The NFT module is implemented at the native chain application logic level instead of at the Smart Contract level, leveraging the chain’s native interoperability protocols to transfer NFTs between chains instead of permissioned bridge Smart Contracts.

## Technical Specification


#### ID interface

An interface to be implemented by any type that servers as an identifier for another object/s. ID string could be represented in space-conserving data formats like hexadecimal or base64 or could be made human-readable format if the use-case requires it.

``` go
ID interface{

   // String returns representation of the ID in a human-readable string
  String() string

   // Bytes return the byte array of the ID
  Bytes() []bytes

  // Compare compares the ID to the given ID returning the integer difference between the bytes of the identifier, for sorting or matching
  Compare(ID) int
  }
```
#### NFT interface

A barebone interface to be implemented by any structure that can be classified as an NFT

``` go
NFT interface {

   // GetID returns the identifier for the NFT as an ID interface. Stored as KVStore index
  GetID() ID

  // GetClassificationID returns the classification/type/denomination for the NFT as an ID interface
  GetClassificationID() ID
}
```

#### NFT Wallet interface

A basic interface for a wallet for structures implementing the NFT interface

``` go
Wallet interface {
   // GetAccountAddress returns the accountAddress of the account which the NFTWallet belongs to. Stored as KVStore index
  GetAccountAddress() AccountAddress

  GetNFT(ID) NFT
  // GetNFTIDs returns the identifier, for all the NFTs stored in the wallet, as an ID interface
  GetNFTIDs() []ID

  // ReceiveNFT adds the given array of NFT to the wallet and returns an error if the receive operation is conflicted
  ReceiveNFT([]NFT) error

  // ReceiveNFT removes the given array of NFT from the wallet and returns an error if the send operation is conflicted
  SendNFT([]NFT) error
}
```

### Metadata interface

 An interface for a metadata object which in this case stores the metadata of an NFT

 ``` go
 Metadata interface{
   // GetID returns the identifier for the Metadata as an ID interface. Stored as KVStore index. In the case of NFT, it's a composite key of the structure AssetID+MetadataID.
   GetID() ID
   GetType() string
   GetValue() string
 }
 ```

## Backwards Compatibility

Not applicable.

## Forwards Compatibility

Not applicable.

## Example Implementation

TBD

## Other Implementations

* PersistenceSDK assets module https://github.com/persistenceOne/persistenceSDK/tree/master/modules/assets

## References

1. William Entriken, Dieter Shirley, Jacob Evans, Nastassia Sachs 2018.ERC-721 Non-Fungible Token Standard. Retrieved from https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md

## History

2020/11/02 - First Draft

## Copyright

All content herein is licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).

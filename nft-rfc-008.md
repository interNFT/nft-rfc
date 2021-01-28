---
nft-rfc: 8
title: NFT Resource Verification
stage: draft
category: NFT/METADATA
authors: Shaun Conway @ig-shaun, Eric Schuh @eric-schuh
created: 2021-1-20
modified: 2021-1-28
---

# NFT RFC 008 NFT Assertions

# Motivation
When an NFT represents one or more real-world resources, which are linked to the NFT, 
there must be a  process for verifying the assertions which are made about these physical 
or virtual resources, to determine if the assertions are both true and positively 
correlated with the resource.

Use cases (described in nft-rfc-002) such as: Access Tokens (Section 2.2), 
Impact Tokens (Section 2.3), and Quality Carbon Credits (Section 4.1).  

For example an industrial company may make claims that it has verifiably reduced its carbon 
emissions, or a renewable energy producer makes claims that it has generated specific 
quantities (MwH) of clean energy. These claims give the issuers the right to receive Tradable 
Certified Emission Reduction (CER) units -- commonly referred to as Carbon Credits, or 
Renewable Energy Certificates (REC), which may be traded. These Carbon Economy resources may 
now be represented by NFTs and metadata.

# Technical Specification

## Definitions

### Verifiable Claim
A claim which conforms to the data model of a Verifiable Credential and which has been 
cryptographically signed by the issuer of the claim. The claim may contain attributes, statements 
and other data but the validity and truth of the claim should be independently evaluated, to verify 
whether the claim meets specific acceptance criteria for it to be considered a valid claim, which 
is positively correlated with the identified claim subject, and that passes a threshold probability 
of being true.

### Verifiable Credential
A [standard data model](https://www.w3.org/TR/vc-data-model/) and serialisation format for making statements about subjects, 
where both the subject and issuer are identified by Decentralised Identifiers (DID), 
which can be cryptographically authenticated and the data object is cryptographically 
signed by the issuer.
As specified by the W3C Verifiable Credentials Data Model and DID working groups. 

### Claim Issuer
The entity which issues the source Verifiable Claim which will be evaluated, verified and eventually 
be linked to an NFT resource. 

### Claim Evaluation
The process whereby an agent‒usually independent from the claim issuer‒evaluates the 
content of a verifiable claim, to determine whether the claim meets specific acceptance 
criteria for it to be considered a valid claim which passes a threshold probability of 
being true and is also positively correlated with the identified claim subject.  

### Claim Verification Oracle
An agent  which has the authority to issue signed attestations in the format of a 
Verifiable Credential about the results of a claim evaluation. The attestation may include 
additional information. For instance, converting a claim about renewable energy usage from 
a claimed number of Kilowatt Hours into Verified Carbon Credit units.

## Verification Process
Throughout this overview there will be reference to four different Verifiable Credentials, which 
will be denoted the first time they are used as VC1, VC2, VC3, VC4, and VC5. The set of these five 
VCs will be utilized in the minting of a NFT with its associated metadata.
1. The Claim Issuer (in this case, the Renewable energy producer) holds a Verifiable Credential (VC1) 
   which attests to the Issuer’s right to make claims of a specific type. This may require other conditional 
   requirements to be met by the issuer.
2. The Claim Issuer issues a set of Verifiable Claims (for the Mw Hours of clean energy they have produced). 
   These claims contain all the data necessary for a Verification agent to perform an evaluation of the claim, 
   opinionate and verify whether the contents of the claim are true and positively correlated. 
3. Verifiable Claims are encoded within a Verifiable Credential wrapper to become VC2
   * VC2s contain not only the Verifiable Claim being asserted but also a reference to Claim Issuer’s VC1. 
     The combination of these two: 
	    - Enables cryptographically authenticating the subject and issuer’s identifiers
		- Enables cryptographically verifying that the payload data has not been modified.
   * The VC2s which contain the Verifiable Claims are registered to a blockchain and stored in an appropriate 
     data store which can be accessed by the Claim Verification Agent when they begin the process of evaluation. 
4. VC2s are evaluated by the Claim Verification Agent.
   * If a claim meets the threshold requirements for being both true and positively correlated with the subject, 
     it may be considered a Verified Claim which has been verified by the identified Claim Verification Agent.
   * The Claim Verification Agent will include a Verifiable Credential (VC4) which can be used to verify their 
     ability to evaluate the claims being made in step one. 
   * This combination of the evaluated VC2s, which now represent Verified Claims, and the Claim Verification Agent’s 
     VC4 are wrapped in a new Verifiable Credential, VC3
5. On the basis of one or more Verified Claims and the attestations on these claims by Claim Verification Agent, 
   as bundled in VC3, a Credential Issuing Authority issues a Verifiable Credential (VC5). This is the equivalent 
   of issuing a certificate, in the Carbon Emission Reduction use-case. This resource is tokenized as an NFT.
6. The Credential Issuing Authority may provide the Claim Issuer a capability (such as  in the form of a ZCAP) 
   to take ownership of the minted NFT. 
   * The NFT conforms to the Interchain NFT Specification
   
## VC# Overview
This section gives an overview of the purpose of the five different Verifiable Credentials described in the use-case.

### VC1
The Verifiable Credential issued by a recognized certification agency that gives the Claim Issuer the right to make claims. 
Used by the Claim Verification Agent to validate that a claim has been issued by an authorised claim-issuer.

### VC2
The Verifiable Credential which contains the digital representation of the claim being made by the Claim Producer. 
These Verifiable Claims are registered on a blockchain and stored in a digital data store that, with the proper capability, 
a Claim Verification Agent can access as part of their verification process.

### VC3
The Verifiable Credential which contains, at least by reference, the set of VC1, VC2 and VC4 and is issued by the 
Claim Verification Agent to either attest or contest the validity of the claims being made in VC2.

VC3s also contain assertions made by the Claim Verification Agent as to how they arrived at the conclusion of their claim‒
e.g. how they got to their conclusion and any comments regarding the evaluation‒which provide the Claim Verification Agent’s 
reasoning for the outcome of the evaluation.

### VC4
The Verifiable Credential which is issued to the Claim Verification Agent by a recognized governing body that oversees the types 
of claims the Claim Verification Agent will be evaluating. This Verifiable Credential establishes the validity of the verification 
claims made by the Claim Verification Agent. 

In the case that the Claim Verification Agent is also the recognized governing body which oversees the evaluation of claims of the 
type being made VC4 may not be necessary. 

### VC5
The final Verifiable Credential created in the process. This is tokenized in the minting of the NFT IID which is returned to the 
Claim Producer via a retrieval capability and contains, at least by reference, the set of Verifiable Credentials utilized in the 
process of verifying the initial claims made by the Claim Producer. It must provide the complete set of 
Verifiable Credentials (V1, V2, V3 and V4) so the full chain of verification can be inspected by third parties interested in the 
final NFT IID can inspect the origins of the NFT.

## Carbon Credits Example
To walk through the above Verification Process we are going to use an example of a company, HydroElec Inc., who has recently upgraded 
a dam to support the production of hydroelectric power and is going through the process of claiming 100 tons of Carbon Credits from 
the UN’s International Climate Change Authority (UNFCCC).. 

In this example we will use the name of a few companies representing the different authorities involved in the process: 
* __HydroElec__ Inc is the clean energy producer who issues a renewable energy certificate (REC) claim‒in the format of VC2, of having 
  produced a number of Mw Hours of clean energy through its certified hydroelectric project. 
* __CleanEnergy Certifier__ is the certifying authority who certifies HydroElec Inc’s new hydroelectric dam project and issues VC1
* __CarbonAudit__ is the REC Claim Verification Agent who evaluates the producer’s CER claim and performs uses an approved method to transform 
  this claim into Certified Emission Reduction Units and issues VC3s in the form of a Verified Carbon Emission Reduction. 
* __UNFCCC__ will act as the both governing body who certified CarbonAudit as a Claim Verification Agent and issues VC4 and as the issuing 
  authority for the NFT IID that is produced from VC5

1. CleanEnergy Certifier gets certified by the UNFCCC to act as a Claim Verification Agent for the purposes of issuing Verified REC and receives VC4 
   from the UNFCCC. 
2. HydroElec Inc gets certified as a producer of REC Claims, with a subcategory of hydroelectric power, by CleanEnergy Certifier who audited the 
   installation of the new hydroelectric dam that was recently converted. HyrdoElec Inc receives VC1 from CleanEnergy Certifier once this process is 
   complete. 
3. Once HydroElec Inc has their REC Claim Issuing Certification from CleanEnergy Certifier, they turn on their new dam and allow the turbines to start 
   producing energy. Each turbine has its own, individual IOT device, which outputs a claim after every kilowatt hour of produced energy, 
   including a reference to the VC1 HydroElec Inc received above. Each of the individual claims output by each turbine’s IOT device is a VC2
4. As the turbines IOT devices produce the individual VC2s they are registered on a blockchain, with the actual VC2 being stored in a digital 
   data store that can be accessed given the proper capability. 
5. After a few days of running HydroElec Inc contacts CarbonAudit ask requests that they begin the process of verifying the Verifiable Claims 
   that have been registered to the blockchain and include in this request a capability for CarbonAudit to access the digital data store the 
   VC2s are actually stored in. 
6. CarbonAudit begins processing the VC2s as indexed on the blockchain. Each VC2 is independently evaluated with the contained, referenced 
   VC1 that certifies HydroElec Inc as a valid producer of the claims being made being checked for each VC2 processed. 
7. Once CarbonAudit has verified a set of VC2s from HydroElec Inc that would constitute 100 tons of carbon units, they package the references 
   to the processed VC2s, along with CarbonAudit’s certifying VC4 that can be used to verify their standing with the UNFCCC, into a VC3 which 
   is returned to HydroElec Inc. 
8. Once HydroElec Inc receives a VC3 which asserts CarbonAudit’s verification of RECs worth the equivalent of 100 tons worth of carbon, 
   the VC4 is passed to the UNFCCC for final evaluation.
9. The UNFCCC reviews the submitted VC3, including verifying the referenced certifying agencies issued VC1 (from Sustained Certs) and 
   VC4 (from UNFCCC), and once they are satisfied that all is in order, bundle VC4 with a verification assertion into VC5. 
10. VC5 is then minted into a Carbon Credits NFT which represents 100 tons worth of Carbon Credits. A capability to retrieve this minted NFT 
    is then given to HydroElec Inc by the UNFCCC.
11. HydroElec Inc claims their Carbon Credit NFT, granting them full ownership.

## Diagram

## Example Data Structures 

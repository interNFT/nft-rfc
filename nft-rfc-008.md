---
nft-rfc: 8
title: NFT Resource Verification
stage: draft
category: NFT/METADATA
authors: Shaun Conway @ig-shaun, Eric Schuh @eric-schuh
created: 2021-1-20
modified: 2021-2-3
---

# NFT RFC 008 NFT Assertions

# Motivation
When an NFT represents one or more real-world resources, which are linked to the NFT, 
there must be a  process for verifying the assertions which are made about these physical 
or virtual resources, to determine if the assertions are both true and positively 
correlated with the resource.

Relevant use cases (described in nft-rfc-002) for reference: Access Tokens (Section 2.2), 
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

### Claim Verification Agent
An agent  which has the authority to issue signed attestations in the format of a 
Verifiable Credential about the results of a claim evaluation. The attestation may include 
additional information. For instance, converting a claim about renewable energy usage from 
a claimed number of Kilowatt Hours into Verified Carbon Credit units.

They are provided a capability from the NFT Issuing Authority which enables their right to evaluate the 
set of claims governed by the issuing authority. 

### Cerification Agent
An agent which has the auhtority to issue signed attestations in the form of  a 
Verifiable Credential in regards to a Claim Issuer's ability to produce valid claims.

They are provided capabilities from the NFT Issuing Authority which enables their right to 
evaluate whether or not a particular Claim Issuer is capable of producing valid claims. 

### NFT Issuing Authority
The authority which specifies the schema and criteria for generating an NFT from the claims produced by 
the Claim Issuer. They can provide other entities with capabilities to certify and verify the the Claim
Issuer's claims are acceptable given the criteria specified. 

### Certifier VC (VC1)
Signed by the Issuing Authority, designates the Certification Agent as a verified certifier for the 
minting of the NFT specified by the Issuing Authority.

### Verifier VC (VC2)
Signed by the Issuing Authority, designates the Claim Verification Agent as a certified verification agent
for the purpose of evaluating evidence of claims to satisfy the caveats specified by the Issuing Authority
as a requirement for minting the NFT. 

### Project Description VC (VC3)
Signed by the Claim Issuer, this provides a description of the project which will be issuing claims that will
be minted into NFTs. 

### Project Certification VC (VC4)
Signed by CAP2 (below), provided to the Claim Issuer by the Certifaction Agent and asserts to the project's
ability to issue claims that can be used to mint NFTs of the type specified by the Issuing Authority. 

### Evidence VC (VC5)
Reference VC4 and contain the assertions made by the Claim Issuer which provide the evidence needed by the
Claim Verification Agent to verify the claim being made. VC5s are the digital representation of the claim
being made by the Claim Issuer. 

### Claim Evaluation VC (VC6)
Signed by CAP3 (below), these contain a referense to the VC5(s) evaluated by the Claim Verification Agent and
specify the outcome of the verification process. 

### Certifier's Mint NFT Capability (CAP1)
Provided to the Certification Agent by the Issuing Authority, this capability grants the invoker the ability to
mint the NFT specified by the Issuing Authority provided all caveats are met. This capability is granted to the
Claim Issuer by the Certification Agent along with VC4 after they have completed the certification process. 

A standard set of caveats on CAP1:
* Need Project Certification VC (VC4)
* Need Claim Evaluation VC(s) (VC6)
* Need associated Evidence VC(s) (VC5) to the provided VC6(s)
* Need Certifier VC (VC1)
* Need Verifier VC (VC2)

### Certification Capability (CAP2)
Provided to the Certification Agent by the Issuing Authority, this capability grants the Certification Agent the
ability to sign Project Certification VCs (VC4) on behalf of the Issuing Authority.

### Verification Capability (CAP3)
Provided to the Claim Verification Agent by the Issuing Authority, this capability grands the Claim Verification
Agent the ability to issue Claim Evaluation VCs (VC6) on behalf of the Issuing Authority. 

### Claim Isssuer's Mint NFT Capability (CAP4)
Provided by the Certification Agent upon project certification, this capability follows the same set of rules
and caveats as CAP1 with the addition of project specific caveats specified upon certification. Some category
examples for these new caveats:
* Claim must have been issued inside a certain timeframe 
* Data in claim must conform to a set of specific units 
* Must include a project description (VC3)

## Verification Process

### 1. NFT Class Template Defined
The Issuing Authority defines the class template for the NFT they will be issuing, including specifying the caveats,
and creates the set of capabilities they will need to deligate to the Certification Agents (CAP1, CAP2) and the 
Claim Verification Agents (CAP3). The caveats specified must be evaluatable by the defined class template and as such
must be representable in digital form. For the evaluation of real world caveats--e.g. requiring ID checked at the door
to a play serving alcohol--the Issuing Authority can, either by proxy or themselves, certify real world evaluators of
the caveat whom they trust and whose resulting verification output--in the form of Verifiable Credentials--is the 
caveat required by the NFT Class Template.

### 2. Enable Caveat Resolution
The Issuing Authority certifies Certification Agents and Claim Verification Agents. Providing these entities with the 
proper capabilities and Verifiable Credentials to both execute and validate their roles. 
   * Certification Agent: Receives VC1, CAP1, CAP2
   * Claim Verification Agent: Receives VC2, CAP3
These agents role in the system is to allow for the real world evaluation and resolution of caveats that require 
explicitly off-chain information and/or evaluation of off-chain information and enables an Issuing Authority to have 
a high degree of flexibility in their own policy for acceptable caveat resolution. 

### 3. Create Project
The Claim Issuer starts a new project and creates the project's VC3 which provides all of the necessary details required
by the Issuing Authority for the project to be certified.

### 4. Project Certification
The Claim Issuer gets the project certified by a Ceritification Agent and receives:
   * Project Certification VC (VC4)
   * NFT Minting Capability with specified caveats (CAP4)
This process of creating a project and getting it certified as a valid minter of the NFTs defined in the initial class
definition is subject to the caveats specified by the Issuing Authority. It is completely valid to have an NFT Class 
Template defined without the need for the NFT minter to be certified. 

### 5. Issue Claims
The Claim Issuer begins issuing claims which cite the Project Certification VC (VC4). These claims contain all the
information needed by the Claim Verification Agent to properly verify that the claims meet the caveats as defined in the
NFT Class Template. The need for a Claim Verification Agent only arrises in the case that the NFT Issuing Authority 
specifies this in the caveats. Once again, the caveat would require a Verifiable Credential to be
which is produced by the Claim Verification Agent and which attests to the outcome of the claim evaluation. 

### 6. Evaluate Claims
These claims are presented to the Claim Verification Agent who evaluates the claims being made and issues Claim Evaluation 
VCs (VC6) via the Verification Capability (CAP3) they received from the Issuing Authority. To invoke CAP3 the Claim
Evaluation Agent will need to satisfy any caveats defined by the Issuing Authority regarding the evaluation of the claims 
being made. 

### 7. Mint NFT
Once they have all the necissary data, as specified by the caveats, the Claim Issuer invokes their capability to mint the NFT (CAP4), 
as provided to them by the Certification Agent, and recieves their NFT assuming all caveats are met per the Issuing Authoritie's 
Otherwise the mint transaction will fail and the Claim Issuer will receive a message detailing the failure mode. 

### 8. Dispute Claim
Once the NFT has been minted either the Certification Agent, Claim Verification Agent or the Issuing Authority may dispute the data
used to satisfy the specified caveats. The result of this dispute could result in the Issuing Authority burning the NFT as evidence
that the caveats did not meet the requirements. 

## Example User Story: Renewable Energy Certificates (RECs)
To walk through the above Verification Process we are going to use an example of a company, HydroElec Inc., who has recently upgraded 
a dam to support the production of hydroelectric power and is going through the process of claiming 100 tons of Carbon Credits from 
the UN’s International Climate Change Authority (UNFCCC).

### Actors
* __HydroElec (Claim Issuer)__  is the clean energy producer who issues a renewable energy certificate (REC) claim‒in the format of VC2, of having 
  produced a number of Mw Hours of clean energy through its certified hydroelectric project. 
* __CleanEnergy Certifier (Certification Agent)__ is the certifying authority who certifies HydroElec Inc’s new hydroelectric dam project and issues VC1
* __CarbonAudit (Claim Verification Agent)__ is the REC Claim Verification Agent who evaluates the producer’s REC claim and uses a capability issued by the UNFCCC
  to issue Evaluation Report Credentials (VC3s)
* __UNFCCC (Issuing Authority)__ will act as the both governing body who certified CarbonAudit as a Claim Verification Agent and issues VC4 and as the issuing 
  authority for the NFT IID that is produced from VC5
* __Clean Energy Blockchain__ is a ficticious blockchain where HydroElec will register their issued clean energy claims by reference. The
  claims themselves are stored in a secure data vault controlled by HydroElec which requires an authorised capability to access. 

### 1. NFT Class Template Defined
The UNFCCC publishes a new NFT schema for RECs which includes a set of criteria--as listed below--as well as the set of capabilities they will need to
be delegating to the Certification and Claim Verification Agents (CAP1,2,3):
   * Claim Issuer must have their facilities certified by a certifying agency recognized by the UNFCCC
   * Claim Issuer must have their claims validated by a Claim Verification Agent that is recognized by the UNFCCC
      - Claim Verification Agent must include a hashed reference to each Claim they processed
      - Claim Verification Agent must include a timestamp in ISO 8601 format for when each Claim was processed
   * Energy Claims must be made in units of MWh
   * Energy Claims must include the time range the energy was produced in and must follow ISO 8601
   * Claim Issuer must include a specific IOT device reference the claim was generated from
   * Claim Issuer must include last service date in ISO 8601 format for each IoT device

### 2. Enable Caveat Resolution
CleanEnergy Certifier gets certified by the UNFCCC to act as a project auditor for the purposes of certifying a project to be able to make
REC claims and receives the set of VC1, CAP1 and CAP2 from the UNFCCC. At the same time CarbonAudit gets certified by the UNFCCC as a 
Claim Verification Agent for these new REC NFTs and receives both their certification (VC2) and CAP3 from UNFCCC to issue Claim Evaluations (VC6). 

### 3. Create Project
HydroElec sets up their new project where they have converted an old dam to produce hydroelectric power and create their 
Project Description Credential (VC3).

### 4. Project Certification
HydroElec get CleanEnergy Certifier to audit the new electric dam they just converted and receives a Certifying Credential (VC4) along with the 
capability to mint the UN-REC2021 NFT (CAP4) from CleanEnergy Certifier which is issued to HydroElec via CAP2.

### 5. Issue Claims
HydroElec begins producing renwable energy claims and stores them, by reference, on the Clean Energy Blockchain. Enlisting CarbonAudit, they
provide a capability to CarbonAudit to access the referenced renwable energy claims. As part of HydroElect's agreement with CarbonAudit, they have
specified that CarbonAudit will provide their verification certificates once 100,000KWh of energy worth of claims have been verified and CarbonAudit
must notify HydroElec immediately of any rejected claims. 

### 6. Evaluate Claims
CarbonAudit processes the claims as they are registered to the Clean Energy Blockchain and uses CAP3 to issue sets of Claim Evaluation 
credentials (VC6s) which contain the result of the evaluation as well as a reference to their certification (VC2). Once CarbonAudit has processed
100,000KWh worth of claims from HydroElec, the VC6s are returned to HydroElec.

### 7. Mint NFT
HydroElect takes the set of:
   * Certifier VC (VC1)
   * Verifier VC (VC2)
   * Project Description (VC3)
   * Project Certification VC (VC4)
   * Evidence VCs (VC5s) 
   * Claim Evaluation VCs (VC6s)
And invokes the capability given to them upon completion of their certification process (CAP4). Assuming all caveats pass their checks, HydroElec 
recieves thier REC NFT which represents the credit for 100,000 KWh of clean energy produced. 

### 8. Claim Dispute
A few months after a particular NFT was produced, CleanEnergy Certifier is doing their routine checkup of the facility and finds that one of the turbines
is not properly reporting the energy throughput. They revoke CAP4 from HydroElec until the issue is solved and file a dispute with the UNFCCC regarding 
validity of a number of the NFTs that had been minted over these last few months. Finding the offending claims, the UNFCCC modifies the NFTs that were 
affected by the faulty sensor to omit the claims made by the faulty device. One such REC NFT had more then 50% of its claims for the offending device and
as such this NFT is burned by the UNFCCC. 

## Diagram
![Capability for Minting Tokens](https://user-images.githubusercontent.com/22247137/111194978-fe108f80-8578-11eb-8c3e-4c4799d416ff.png)


## Example Data Structures 

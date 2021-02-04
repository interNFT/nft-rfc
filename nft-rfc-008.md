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

They are provided a capability from the NFT issuing authority which enables their right to evaluate the 
set of claims governed by the issuing authoridy. 

## Verification Process

1. The final issuing authority of the NFT begins by specifying a schema template for the NFT they will be issuing.
   This schema template will define both set of criteria which a Claim Issuer has the burden of satisfying for the 
   NFT issuing authority to accept the claim being made as true and a set of criteria that must be met for the NFT
   issuing authority to receive a minting capability. The criteria to recieve the minting capability from the NFT issuing
   authority and the criteria for the acceptance of a claim or set of claims can and likely will be different. 
   If the criteria, as definited in the schema template, are not met to the satisfaction of the NFT issuing authority 
   they can revoke the minting capability of the Claim Issuer and/or burn any minted NFT(s).
   Some example criteria that could be specified:
   * Claim Issuer must provide a certification from a certifying agency recognised by the NFT issuing authority
   * Claim Issuer must have their Claim validated by a recognized evaluating agency
   * Claim Issuer must provide evidence as referrenced by the Claim Evaluation
   * Claim must be submitted within a certain timeframe of the claim issuing date
   * etc
2. Once the NFT issuing authoriy has specified their schema a Claim Issuer can now evaluate the published schema and 
   begin the process of collecting any credentials they may need to satisfy the criteria set forth in the schema. For
   the Claim Issuer this may include:
   * Contacting a recognized certification agency who can inspect their infrastructure and provide an inspection certificate.
   * Finding a certified Claim Verification Agent to evaluate their claims
   * Ensure the can provide the evidence needed by the Claim Verification Agent
   * etc
3. Now that the Claim Issuer has collected the necessary pieces to fulfill the NFT issuing authority's criteria they can now
   provide an initial set of proof of criteria fulfillment to the NFT issuing authority and receive
   a capability to mint the NFT specified by the schema from the NFT issuing authority. This capability allows the Claim
   Issuer to mint an NFT assuming they provide verifiable proof that the schema criteria has been met. 
4. After the Claim Issuer receives their minting capability they may now begin issuing the claims they will be making. Note
   that this process could and likely will be asynchronous in the a Claim Issuer can start issuing claims prior to any 
   certification process taking place, as long as this does not violate any of the NFT schema's criteria. 
   Some claim examples:
   * Production 1000MWh of solar energy
   * Increased performance of a student by a letter grade over a semester
   * Removal of 50tons of carbon via carbon capture
5. Once the claims have been issued, the Claim Issuer now begins the process of turning their claims into an NFT. This begins
   by first going through the necessary steps to satisfy the NFT schema criteria and may include:
   * A reference to a certification made by a recognized agency
   * A reference to a cerfied Claim Verification Agent's evaluation of the claim
   * etc
6. Only after satisfying criteria as denoted by the NFT schema criteria, and any caveats attached 
to the capability, can the Claim Issuer now take the set
   of data--this being the claim itself and the set of data which satisfies the schema criteria--and use this to mint an NFT.
7. This NFT can now be governed by the particular NFT requirements (e.g. mintable, tradable, immutable, etc) with the NFT
   issuing authority retaining the right to burn the NFT should any dispute be resolved against the Claim Issuer or any 
   attestations made by the Claim Issuer against the specified NFT schema criteria.    

## Carbon Credits Example
To walk through the above Verification Process we are going to use an example of a company, HydroElec Inc., who has recently upgraded 
a dam to support the production of hydroelectric power and is going through the process of claiming 100 tons of Carbon Credits from 
the UN’s International Climate Change Authority (UNFCCC).

Throughout this overview there will be reference to four different Verifiable Credentials, which will be denoted the first time they are 
used as VC1, VC2, VC3, VC4. The set of these five VCs will be utilized in the minting of a NFT with its associated metadata.

In this example we will use the name of a few companies representing the different authorities involved in the process: 
* __HydroElec__ Inc is the clean energy producer who issues a renewable energy certificate (REC) claim‒in the format of VC2, of having 
  produced a number of Mw Hours of clean energy through its certified hydroelectric project. 
* __CleanEnergy Certifier__ is the certifying authority who certifies HydroElec Inc’s new hydroelectric dam project and issues VC1
* __CarbonAudit__ is the REC Claim Verification Agent who evaluates the producer’s REC claim and uses a capability issued by the UNFCCC
  to issue Evaluation Report Credentials (VC3s)
* __UNFCCC__ will act as the both governing body who certified CarbonAudit as a Claim Verification Agent and issues VC4 and as the issuing 
  authority for the NFT IID that is produced from VC5
* __Clean Energy Blockchain__ is a ficticious blockchain where HydroElec will register their issued clean energy claims by reference. The
  claims themselves are stored in a secure data vault controlled by HydroElec which needs a capability to access. 

1. The UNFCCC publishes a new NFT schema for RECs which includes a set of criteria--as listed below--as well as specifying that producing 
   a verifiable certificate from an approved site auditor (CleanEnergy Certifier) can be exchanged for the capability to mint REC NFTs:
   * Claim Issuer must have their facilities certified by a certifying agency recognized by the UNFCCC
   * Claim Issuer must have their claims validated by a Claim Verification Agent that is recognized by the UNFCCC
      - Claim Verification Agent must include a hashed reference to each Claim they processed
      - Claim Verification Agent must include a timestamp in ISO 8601 format for when each Claim was processed
   * Energy Claims must be made in units of MWh
   * Energy Claims must include the time range the energy was produced in and must follow ISO 8601
   * Claim Issuer must include a specific IOT device reference the claim was generated from
   * Claim Issuer must include last service date in ISO 8601 format for each IoT device
2. CleanEnergy Certifier gets certified by the UNFCCC to act as a project auditor for the purposes of certifying a project to be able to make
   REC claims and receives VC4 from the UNFCCC. At the same time CarbonAudit gets certified by the UNFCCC as a Claim Verification Agent for 
   these new REC NFTs and receives a capability from UNFCCC to issue an Evaluation Report Credentials (VC3). 
3. HydroElec get CleanEnergy Certifier to audit the new electric dam they just converted and receives a Certifying Credential (VC1) from 
   CleanEnergy Certifier which includes, by reference, CleanEnergy Certifier's Certification Credential (VC4) they received from UNFCCC.
4. HydroElec submits their Certifying Credential (VC1) to the UNFCCC and receives the capability of minting REC NFTs. 
5. HydroElec begins producing renwable energy claims and stores them, by reference, on the Clean Energy Blockchain. Enlisting CarbonAudit, they
   provide a capability to CarbonAudit to access the referenced renwable energy claims. 
6. CarbonAudit processes the claims as they are registered to the Clean Energy Blockchain and, as they only issue Evaluation Report credentials (VC3s).
7. Once CarbonAudit has evaluated 1,000MWh worth of claims, they bundle their evaluations in a VC3, which contains: 
   * Reference to VC1 describing the project
   * Reference to each claim evaluated
   * Outcome and reasoning for each claim evaluated
8. This Evaluation Report Credential (VC3) is issued via the capability CarbonAudit recieved from the UNFCCC. 
9. The Evaluation Report Credential is packages along with the other data required by the REC NFT schema and HydroElect uses this package to mint
   the REC NFT using the capability they received from the UNFCCC. 
10. Once the minting is complete, HydroElec can now exercise all rights afforded to them as owners of a REC NFT which represents 1,000MWh of
    renwable energy created and utilized. 
11. After their next audit, CleanEnergy Certifier found an issue with one of the turbines at the dam project and as such issues a claim to the
    UNFCCC that all evaluations made based on data from the IOT device attached to the turbing should be invalidated. The UNFCCC reviews the 
    claim made by CleanEnergy Certifier, finds it has good basis can burns the set of NFTs which contained verified data from the time period
    specified by CleanEnergy Certifier. They also temporarily revoke HydroElec's minting capability while additional review of their facilities
    takes place. 
   

## Diagram

## Example Data Structures 

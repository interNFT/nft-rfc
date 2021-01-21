---
nft-rfc: 8
title: NFT Resource Verification
stage: draft
category: NFT/METADATA
authors: Shaun Conway @ig-shaun, Eric Schuh @eric-schuh
created: 2021-1-20
modified: 
---

# NFT RFC 008 NFT Resource Verification

# Motivation
This document exists to formalize the process of verifying NFT 
resources which represent a real world, physical property. The 
verifiability of claims made in relation to NFTs makes it possible 
for NFTs to provide digital representations of real-world resources. 
Use cases (described in nft-rfc-002) -- such as Access Tokens (Section 2.2) 
and Impact Tokens (Section 2.3) -- require claims about resources to be 
verified for their authenticity and truth. 

For this RFC we will use the example of a company making claims that it 
has verifiably reduced its  carbon emissions. This gives the company the 
right to receive Tradable Certified Emission Reduction (CER) units -- commonly 
referred to as Carbon Credits, which are represented by NFTs and their metadata.

# Technical Specification

## Definitions

### Verifiable Claim
A claim which conforms to the data model of a Verifiable Credential and which has 
been cryptographically signed by the issuer of the claim. The claim may contain 
attributes, statements and other data but the validity and truth of the claim should 
be independently evaluated, to verify whether the claim meets specific acceptance 
criteria to be considered a valid claim which is positively correlated with the 
identified claim subject and that it passes a threshold probability of being true.

### Verifiable Credential
A [standard data model](https://www.w3.org/TR/vc-data-model/) and serialisation format for making statements about subjects, 
where both the subject and issuer are identified by Decentralised Identifiers (DID), 
which can be cryptographically authenticated and the data object is cryptographically 
signed by the issuer.
As specified by the W3C Verifiable Credentials Data Model and DID working groups. 

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
1. Verifiable Claims are encoded within a Verifiable Credential wrapper. This makes it possible to:
   - cryptographically authenticate the subject and issuer’s identifiers
   - cryptographically verify that the payload data has not been modified.
2. Verifiable Claims are evaluated by Claim Verification Agents. If a claim meets the threshold requirements 
   for being both true and positively correlated with the subject, it may be considered a Verified Claim which 
   has been verified by the identified Claim Verification Agent.
3. On the basis of one or more Verified Claims and the attestations on these claims by Claim Verification Agents, 
   a Credential Issuing Authority may issue a Verifiable Credential, which may be tokenized as an NFT. For instance 
   the digital representation of a Verified Carbon Emission Reduction Certificate for a specified number of CER units, 
   is issued as a Verifiable Carbon Emission Reduction Credential. This is tokenized as a non-fungible Carbon Token, 
   containing the right to trade the specified number of CER units as Carbon Credits. The state of this token changes over 
   time, as the Carbon Credits‒which may be issued as derivative fungible tokens‒are traded away and the token becomes ‘retired’. 

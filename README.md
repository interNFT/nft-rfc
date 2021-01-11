# NFT+Metada Requests for Comments (NFT-RFC)
The process of developing Interchain Standards for NFTs and Metadata (NFT) MUST allow all proposals and recommendations to proceed through an open submission and *Request for Comments* review process.
This process should follow well-established norms and good practices for developing technical recommendations and implementation options for open technical standards.

Please see [NFT-RFC-1](https://github.com/interNFT/nft-rfc/blob/main/nft-rfc-001_Standard.md) for a description of what an NFC-RFC proposal for an Interchain NFT & Metadata standard or recommendation entails.

Learn more about the [InterNFT Working Group](https://internft.org).

To propose a new standard or to make a recommendation, open a Github issue using the [NFT-RFC Issue Template](https://github.com/interNFT/rfc/issues/new?assignees=&labels=RFC&template=rfc-issue.md&title=).
New issues should be added to the Proposals & Recommendations Inbox on the [Github Project](https://github.com/orgs/interNFT/projects/3).  

For a Draft Proposal to become formally adopted as an Interchain NFT+Metadata standard or recommendation, this should be specified using [this template](https://github.com/interNFT/rfc/blob/main/0000-template.md).
To start a new standardisation document, copy the template and open a PR within the rfc repository.
Do not add an NFT number, as this will be done by the project team.

Proposals may be discussed and prepared before submission, using the [InterNFT Discord](https://discuss.internft.org/).

### NFT-RFC Numbers
Proposals which have formally accepted into the RFC process are allocated a sequential NFT-RFC Number, starting at 1.
A full list of proposals will be maintained at the end of this document.

## Process
Each NFT-RFC submitted will follow a quick-paced and structured process from draft proposal through to final recommendation, as outlined below.
After initial review by the Project Team, for triage and labeling, the issue will be tagged and may be progressed through the review phases.
Once an RFC enters the review process, this will be time-limited to 14-day review and decision cycles.

```sequence
proposer->git repo:create issue
git repo->maintainer: review
maintainer-->git repo: approve issue
proposer->git repo: create draft
git repo->working group: peer review
working group-->git repo: approve
proposer->maintainer: send RFC draft with appovals
maintainer-->git repo: assign S.No., merge
```

### RFC Status Tags:
* DRAFT PROPOSAL: At this stage the RFC submission is work in progress, without a being ready for formal review. This should present a good initial draft on which to get feedback (so consider using Discord for earlier, formative discussions).
* OPEN REVIEW: RFC is fully developed and subjected to a 14-day open review process.
* LAST CALL <date for the last call>: provides a deadline after which no further updates are accepted (changes would require a new RFC to supersede).
* FINAL RECOMMENDATION: RFC is either accepted or rejected for inclusion in the InterChain standard.
* SUPERSEDED by RFCxxx: A new RFC replaces the last proposal.
* ABANDONED: the RFC is no longer pursued by the original authors.

## Acceptance Criteria
* Does not a duplicate a pre-existing NFT-RFC, or has sufficient reason to supersede an existing RFC
* Not disputed (disputed proposals will be subjected to additonal processes)
* Technically sound and feasible, in the general opinion of reviewers
* Contributes a recommendation which is relevant to the Interchain Standard for NFTs + Metadata
* Final review and acceptance of the PR by at least one *Designated Reviewer* appointed by the InterNFT Working Group.

### Disputed RFCs or no visible support
Discussed in the InterNFT Working Group.

## Use in Cosmos ADRs & ICS
Interchain NFT + Metadata RFPs may be used in full or in part, at any stage of their develpment, to instantiate a submission as a Cosmos SDK Architecture Decision Record (ADR) or Interchain Standard for Interblockchain Communication (ICS). Follow instructions in the relevant repos:
* [Cosmos SDK](https://github.com/cosmos/cosmos-sdk/tree/master/docs/architecture)
* [Interchain Standard for Interblockchain Communications](https://github.com/cosmos/ics)

# NFT-RFC Proposals Register

* NFT-RFC-001 Specification Standard for Interchain NFTs and Metadata
* NFT-RFC-002 Use Cases and Requirements Working Document
* NFT-RFC-003 NFT Interface
* NFT-RFC-004 interNFT Standard
* NFT-RFC-005 NFT Rights
* NFT-RFC-007 NFT Layers

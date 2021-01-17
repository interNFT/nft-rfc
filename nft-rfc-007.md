---
nft-rfc: 7
title: NFT Layers Specification
stage: draft
category: NFT/METADATA
author: Joe Andrieu @jandrieu
created: 2020-12-16
modified: 
---

# NFT RFC 007 NFT Layers
One person's metadata is another's data.

We use a layer model as framework for understanding the different types of data and metadata that might apply to non-fungible tokens (NFTs).
Inspired by the seven-layer OSI model \[1\] for networking, the layer model gives a framework for evaluating both what data is used and how to
handle interoperability and substitutability between layers.

# The OSI Model

The Open Systems Interconnection model (OSI model) standardize the
communication functions of an electronic system without regard to its
underlying internal structure and technology. It enabled
interoperability of diverse communication systems using standard
communication protocols.

The model partitions the flow of data into seven abstraction layers,
from the physical implementation of transmitting bits across a
communications medium to the highest-level representation of data of a
distributed application. Each intermediate layer serves a class of
functionality to the layer above it and is served by the layer below it.
Classes of functionality are realized in software by standardized
communication protocols.

In short, the OSI Model allowed component vendors to focus on the
functions they provide and the services they rely on from neighbor
layers without concerns for the rest of the stack. As long as the
interfaces between layers were conformant, then the entire stack works.

<table class="tg">
<thead>
  <tr>
    <th class="tg-y698" colspan="3">Layer</th>
    <th class="tg-y698">Protocol Data Unit (PDU)</th>
    <th class="tg-y698">Function</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-y698" rowspan="4">Host Layers</td>
    <td class="tg-7od5">7</td>
    <td class="tg-7od5">Application</td>
    <td class="tg-7od5" rowspan="3">Data</td>
    <td class="tg-7od5">High-level APIs, including resource sharing, remote file access</td>
  </tr>
  <tr>
    <td class="tg-7od5">6</td>
    <td class="tg-7od5">Presentation</td>
    <td class="tg-7od5">Translation of data between a networking service and an application; including character encoding, data compression, and encryption/decryption</td>
  </tr>
  <tr>
    <td class="tg-7od5">5</td>
    <td class="tg-7od5">Session</td>
    <td class="tg-7od5">Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes</td>
  </tr>
  <tr>
    <td class="tg-7od5">4</td>
    <td class="tg-7od5">Transport</td>
    <td class="tg-7od5">Segment, Datagram</td>
    <td class="tg-7od5">Reliable transmission of data segements between points on a network, including segmentation, acknowledgement, and multiplexing</td>
  </tr>
  <tr>
    <td class="tg-y698" rowspan="3">Media Layers</td>
    <td class="tg-elvq">3</td>
    <td class="tg-elvq">Network</td>
    <td class="tg-elvq">Packet</td>
    <td class="tg-elvq">Structing an managing a multi-node network, including addressing, routing, and traffic control</td>
  </tr>
  <tr>
    <td class="tg-pidv">2</td>
    <td class="tg-pidv">Data link</td>
    <td class="tg-pidv">Frame</td>
    <td class="tg-pidv">Reliable transmission of data frames between two nodes connected by a physical layer</td>
  </tr>
  <tr>
    <td class="tg-90e1">1</td>
    <td class="tg-90e1">Physical</td>
    <td class="tg-90e1">Bit, Symbol</td>
    <td class="tg-90e1">Transmission and reception of raw bit streams over a physical medium</td>
  </tr>
</tbody>
</table>

While the OSI model did not win the day---the Internet protocol stack
did---the model itself is still used for education and illustration.

# The NFT Layer Model

The Interchain NFT Layer Model uses a similar abstraction layer approach
to separate the functionality required by different elements of the solution.

<table class="tg">
<thead>
  <tr>
    <th class="tg-y698" colspan="2">Layer</th>
    <th class="tg-y698">Function</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-90e1">8</td>
    <td class="tg-90e1">Operationalization</td>
    <td class="tg-90e1">How the rights are realized upon receipt/presentation of token
</td>
  </tr>
  <tr>
    <td class="tg-61xu">7</td>
    <td class="tg-61xu">Assertions</td>
    <td class="tg-61xu">Statements about the token and resources referenced in the token</td>
  </tr>
  <tr>
    <td class="tg-x6qq">6</td>
    <td class="tg-x6qq">Extension &amp; Restrictions</td>
    <td class="tg-x6qq">Taveats or addenda to rights represented in token</td>
  </tr>
  <tr>
    <td class="tg-7cvu">5</td>
    <td class="tg-7cvu">Instantiation</td>
    <td class="tg-7cvu">Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes</td>
  </tr>
  <tr height="2px">
    <td class="tg-eul9"></td>
    <td class="tg-eul9"></td>
    <td class="tg-eul9"></td>
  </tr>
  <tr>
    <td class="tg-7od5">4</td>
    <td class="tg-7od5">Affordances </td>
    <td class="tg-7od5">Real-world rights and responsibilities afforded to token owner</td>
  </tr>
  <tr>
    <td class="tg-elvq">3</td>
    <td class="tg-elvq">Token Logic</td>
    <td class="tg-elvq">Property rights and rules. Fungibility, transfer mechanics, etc.</td>
  </tr>
  <tr>
    <td class="tg-pidv">2</td>
    <td class="tg-pidv">Interchain</td>
    <td class="tg-pidv">Cross-chain interactions, especially atomic swaps, adapter signatures, and ledger-to-ledger interactions.</td>
  </tr>
  <tr>
    <td class="tg-90e1">1</td>
    <td class="tg-90e1">State Machine</td>
    <td class="tg-90e1">Distributed consensus (on chain)</td>
  </tr>
</tbody>
</table>
<br/>
We'll use this model to clarify use cases and to highlight requirements
for our specifications.

<br/>
<br/>

\[1\] \"OSI Model\" Wikipedia. Accessed 2020-12-16.
<https://en.wikipedia.org/wiki/OSI_model>

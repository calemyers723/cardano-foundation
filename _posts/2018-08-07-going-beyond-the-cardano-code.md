---
layout: post
date: 2018-08-07
display_date: 2018-08-07
title: "Going Beyond the Cardano Code"
subtitle: ""
language: en
permalink: /press/going-beyond-the-cardano-code/
defaulturl: /press/going-beyond-the-cardano-code/
slug: going-beyond-the-cardano-code
categories: press
image: blog-13-1.jpg
author: steve_wagendorp
---

[View reports](https://www.cardano.org/en/haskell-library-reports/)

In December 2017, Cardano Foundation appointed [FP Complete](https://www.fpcomplete.com/), a renowned Haskell software development and DevOps consultancy, to conduct a third-party, independent audit of Cardano settlement layer.<!--break--> This includes the code, technical documentation and operating procedures of IOHK, Cardano’s development team.

The objective of undertaking this independant and thorough approach to code review and engineering practice is to align with Cardano’s development philosophy of research driven, scientific best practice and rigorous peer-review.

The partnership with [FP Complete](https://www.fpcomplete.com/) was successfully implemented with FP Complete having since produced a number of Cardano audit reports. These include detailed ‘private’ audits for use within the project (i.e. where FP Complete highlight issues that may be security sensitive) and slightly modified versions ‘public’ versions for general release. These comprehensive and highly specific audit reports cover many aspects of the project and code base and this deep audit work is ongoing.

The audit process continues to track the development and engineering practices of the Cardano software build whilst the project progresses through further stages of release. There is no end date planned for the audit, our intention is to continue at least until the projects core objectives of full decentralisation and functionality described in the roadmap is in place. An update on the release of recent public audit reports and the public release process going forward will be provided in the near future.

But right now, we would like to share something the Cardano Foundation is excited and passionate about. It is an extension to the audit initiative, supplementing and expanding the existing process and, we believe, will provide deep value for both the Cardano AND Haskell communities.

<p style="font-weight: bold;">Cardano Haskell library dependencies audit</p>

Software can be designed and developed with the highest standards of assurance and yet still be susceptible to vulnerabilities through the code in its library dependencies. Therefore, we have identified these library dependencies as a particular area of focus for our audit going forward. The importance of software libraries and the specific library dependencies that exist in the Cardano code base is the topic we will elaborate on further in this post.

Broadly speaking, software libraries are collections of resources (code and documentation) used across many projects to implement common functions and behaviour through a well defined set of interfaces. Libraries are built to provide reusable components for multiple independent programs and encourage the sharing of code in a modular fashion by facilitating the distribution of code.

This modular approach to software development is well established and is a fundamental part of the open source software development process that allows for improved efficiency, security and interoperability as a result of collaborative development and crowd sourced expertise.

Although the use of software libraries is not limited to open source software projects, there exists a deepening relationship between the use of libraries and the open source software movement. As a foundation supporting an open source software initiative, we align fundamentally with this open source philosophy and we seek to support endeavours that strengthen it.

Library maintenance is an important part of this ongoing improvement process and is necessary so that bugs are resolved, new features are developed and common code can evolve along with a programming language.

In general, libraries have individual maintainers for regular maintenance of a package and in some cases there may exist formal bodies to provide oversight on the maintenance of libraries. Individual maintainers are responsible for dealing with individual issues and these maintainers are often empowered to unilaterally make decisions on that library.

This raises the question … How should libraries be maintained and what is best practice?

Developers today need to identify the right libraries to use for a given problem. FP Complete’s code audit includes analysis and review of the appropriateness of libraries by identifying redundant or duplicate solutions, highlighting the use of unnecessary dependencies, assessing the maturity of libraries and reviewing the quality and frequency of library maintenance as well as tracking any open issues.

Beyond this high level analysis, a thorough code review of these libraries and their potential vulnerabilities is now being done as a separate formal audit by FP Complete. This involves automated testing practices, manual code review, and leveraging existing static analysis tools in Haskell (not least of which is the compiler itself!). Expect to hear more from FP Complete’s team, as these audits continue, on some of the techniques they have undertaken.

Within the Cardano-sl code base, there are currently over 372 individual library dependencies, all under review as part of the code audit.

FP Complete’s code audit therefore presents a unique opportunity to review libraries and code that is used more widely by the Haskell community and in some cases, code reviews that span multiple versions of the same library.

As a commitment to the Haskell community and the open source software movement in general, Cardano Foundation together with [FP Complete](https://www.fpcomplete.com/) will release regular audit reports reviewing various Haskell Libraries as it continues to review the development of Cardano more specifically.

We hope these audit releases will benefit the wider Haskell developer community, encourage a public discussion around commonly used code and help support and encourage a process for vetting dependencies for safety and security concerns.

The first of such reports is available [here on cardano.org](https://www.cardano.org/en/haskell-library-reports/) and will review the Haskell [binary package](https://github.com/kolmodin/binary) providing high performance, pure binary serialisation.

The binary package is also one of the core libraries in GHC, the most commonly used native Haskell compiler and is therefore widely used in the Haskell community with far-reaching implications. The binary package is used by the Cardano project in the following areas:

<ul style="margin-bottom: 30px;">
  <li><a href="https://github.com/input-output-hk/cardano-sl/blob/7da7cd82cb1db2a1cb4de961b05e2459d4066131/crypto/Pos/Crypto/Orphans.hs#L69..L108">The serialization of public keys, key pairs, proofs and encrypted passwords.</a> Clearly a relevant topic for cryptocurrency stability.</li>
  <li><a href="https://github.com/input-output-hk/cardano-sl/blob/7da7cd82cb1db2a1cb4de961b05e2459d4066131/networking/src/Ntp/Packet.hs#L55..L76">The NTP (network time protocol) implementation</a>, which is crucial for synchronization between nodes in any distributed system. Incorrect time values can compromise the stability of the system.</li>
  <li><a href="https://github.com/input-output-hk/cardano-sl/blob/7da7cd82cb1db2a1cb4de961b05e2459d4066131/networking/src/Node/Message/Class.hs#L38">Messages between nodes are encoded with this method</a>, therefore the protocol between nodes may be affected.</li>
</ul>

As Cardano Foundation continues to serve the broader blockchain community, we hope that by sponsoring these additional library audit reports, we will not only see the direct benefit in strengthening and protecting the Cardano project but also in providing a strong, positive contribution to the Haskell and functional programming community which has provided foundational tools to the Cardano project to build a robust and secure public blockchain technology for the benefit of all.

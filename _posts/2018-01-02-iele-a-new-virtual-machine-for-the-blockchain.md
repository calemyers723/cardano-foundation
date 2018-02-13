---
layout: post
date: 2018-01-02
title: "Protected: IELE: A New Virtual Machine for the Blockchain"
subtitle: ""
language: en
permalink: /press/iele-a-new-virtual-machine-for-the-blockchain/
defaulturl: /press/iele-a-new-virtual-machine-for-the-blockchain/
slug: iele-a-new-virtual-machine-for-the-blockchain
categories: press
image: glow.jpg
author: grigore_rosu
produce_text: This blog article has been produced by IOHK and syndicated by Cardano Foundation for wider distribution.
---

<p>Runtime Verification (RV) is proud to release their first version of IELE, a new virtual machine for the blockchain.</p>

<h2 id="whatisiele">What is IELE?</h2>

<p>IELE is a variant of <a href="http://llvm.org/" title="llvm.org">LLVM</a> specialized to execute smart contracts on the blockchain. Its design, definition and implementation have been done at the highest mathematical standards, following a semantics-first approach with verification of smart contracts as a major objective. Specifically, we have defined the formal syntax and semantics of IELE using the K framework, which in return gives us an executable reference model in addition to a series of program analysis tools, including a program verifier. [K](<a class="vglnk" href="http://kframework.org/" rel="nofollow"><span>http</span><span>://</span><span>kframework</span><span>.</span><span>org</span><span>/</span></a>) was created by our team during the last 15 years and incorporates the state of the art in language design, semantics and formal methods. The design of IELE was based on our experience with formally defining <a href="https://github.com/kframework" title="K Framework, Github">dozens of languages in K</a>, but especially on recent experience and lessons learned while formally defining two other virtual machines in K, namely:</p><!--break-->

<ul>
<li><a href="https://github.com/kframework/evm-semantics" title="EVM Semantics, Github">KEVM</a>, our semantics of the <a href="https://github.com/ethereum/yellowpaper" title="Ethereum Virtual Machine Yellow Paper">Ethereum Virtual Machine</a> (EVM); and</li>

<li>KLLVM, our semantics of <a href="http://llvm.org/" title="llvm.org">LLVM</a>; the latest version of the LLVM semantics will be made public when complete and published, but an earlier version <a href="https://github.com/kframework/llvm-semantics" title="LLVM Semantics">is available</a>.</li>
</ul>

<p>Unlike the EVM, which is a stack-based machine, IELE is a register-based machine, like LLVM. It has an unbounded number of registers and also supports unbounded integers. To get a feel for how IELE programs look like, here are two of them (these have not been verified yet and may change):</p>

<ul>
<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-examples/erc20.iele" title="IELE Examples, erc20">erc20.iele</a> - a IELE implementation of an ERC20 token</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-examples/forwardingWallet.iele" title="forwardingwallet.iele, Github">forwardingWallet.iele</a> - a wallet implementation that creates and calls into another contract</li>
</ul>

<h2 id="designrationale">Design Rationale</h2>

<p>Here are the forces that drove the design of IELE:</p>

<ol>
<li><p>To serve as a uniform, lower-level platform for translating and executing smart contracts from higher-level languages. The contracts can interact with each other by means of an ABI (Application Binary Interface). The ABI is a core element of IELE, and not just a convention on top of it. The unbounded integers and unbounded number of registers should make compilation from higher-level languages more straightforward and elegant and, looking at the success of LLVM, more efficient in the long term. Indeed, many of the LLVM optimizations are expected to carry over. For that reason, IELE followed the design choices and representation of LLVM as much as possible. The team also includes LLVM experts from the University of Illinois (where LLVM was created).</p></li>

<li><p>To provide a uniform gas model, across all languages. The general design philosophy of gas calculation in IELE is "no limitations, but pay for what you consume". For example, the more registers a IELE program uses, the more gas it consumes. Or the larger the numbers computed at runtime, the more gas it consumes. The more memory it uses, in terms of both locations and size of data stored at locations, the more gas it consumes. And so on.</p></li>

<li><p>To make it easier to write secure smart contracts. This includes writing requirements specifications that smart contracts must obey as well as making it easier to develop automated techniques that mathematically verify / prove smart contracts correct with respect to such specifications. For example, pushing a possibly computed number on the stack and then jumping to it regarded as an address makes verification hard, and thus security weaker, with current smart contract paradigms. IELE has named labels, like LLVM, and jump statements can only jump to those labels. Also, it avoids the use of a bounded stack and not having to worry about stack or arithmetic overflow makes specification and verification of smart contracts significantly easier.</p></li>
</ol>

<p>Like <a href="https://github.com/kframework/evm-semantics" title="EVM Semantics, Github">KEVM</a>, the formal semantics of EVM that we previously defined, validated and evaluated using the <a href="http://www.kframework.org/index.php/Main_Page" title="kframework.org">K framework</a>, the design of IELE was also done in a semantics-based style, using K. Together with a fast (LLVM-based) execution backend for K that is still under development, it is expected that the interpreter obtained automatically from the semantics of IELE will be sufficiently efficient to serve as a reference implementation of IELE.</p>

<h2 id="whatsnext">What's next?</h2>

<p>To achieve the full potential of IELE, we plan to next work on the following:</p>

<ul>
<li><p>Efficient backend for K. Then K semantics, including IELE, can be executed at acceptable performance. As discussed in our KEVM paper, the current version of K can execute the EVM semantics at performance that stays within an order of magnitude from the performance of the <a href="https://github.com/ethereum/cpp-ethereum/" title="cpp-ethereum, Github">reference C++ implementation of the EVM</a>. We believe that we can improve the execution performance of K by one order of magnitude. If this is achieved, then there is no incentive to implement IELE in an ad-hoc way: the K executable semantics of IELE will also be its implementation, so it will be correct by construction and thus implementation defects of the VM itself cannot be exploited anymore. Also, IELE itself would be easier to maintain and future versions will be easier to deploy.</p></li>

<li><p>Compilers/Translators from <a href="https://solidity.readthedocs.io/en/develop/" title="Solidity Documentation">Solidity</a> and <a href="https://cardanodocs.com/technical/plutus/introduction/" title="Plutus Introduction, cardanodocs.com">Plutus</a> to IELE. Writing smart contracts directly in IELE is a bit more feasible than in the EVM, because IELE follows the LLVM IR which was designed to be human-readable, but the IELE code is still low-level and thus error-prone. To properly test IELE and gain confidence in its overall design and capabilities, we will implement a compiler/translator from <a href="https://solidity.readthedocs.io/en/develop/" title="Solidity Documentation">Solidity</a> to IELE, also in K. Since <a href="https://cardanodocs.com/technical/plutus/introduction/" title="Plutus Introduction, cardanodocs.com">Plutus</a> rises as a star among the functional programming languages for smart contracts and since we are defining a <a href="https://github.com/kframework/plutus-core-semantics" title="Plutus Core Semantics, Github">formal semantics of Plutus</a> as well, a compiler from Plutus to IELE will be developed immediately after Solidity's.</p></li>

<li><p>Semantics-based compilation. In addition to improving K's performance, we plan to implement a tool that we call semantics-based compiler on top of K. See our previous <a href="https://runtimeverification.com/blog/?p=459" title="New Technologies for the Blockchain: IELE, runtimeverification.com">blog post</a> for details. The idea is to take a programming language semantics L and a program P in L, and generate (using symbolic execution heavily) a new language semantics L' which is a specialization of L for P. We expect at least one order of magnitude increase in performance. More importantly, this will give us a uniform mechanism to translate any programs in any programming languages that have a K semantics to IELE, thus making IELE and K into a universal platform for executing smart contracts in any language.</p></li>

<li><p>Deploy IELE on the Cardano blockchain.</p></li>
</ul>

<h2 id="technicaldetailsanddownload">Technical Details and Download</h2>

<p>IELE is thoroughly commented and freely available under the UIUC license (as permissive as the MIT license) on Github:</p>

<ul>
<li><a href="https://github.com/runtimeverification/iele-semantics" title="IELE Semantics, Github">IELE repository on Github</a></li>
</ul>

<p>In addition to the two IELE programs mentioned above, erc20.iele and forwardingWallet.iele showing that the IELE code is human readable, the following links into the github repo will give a good idea what IELE is and how it differs from EVM and LLVM:</p>

<ul>
<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-syntax.md" title="IELE Textual Syntax">iele-syntax.md</a> - the complete formal syntax of the IELE language.</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele.md" title="IELE Execution">iele.md</a> - the complete formal executable semantics of the IELE language</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/Design.md" title="IELE Design">Design.md</a> - the design rationale of IELE, as well as detailed comparisons with LLVM and EVM</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-gas.md" title="IELE Gas Calculation">iele-gas.md</a> - the current gas model of IELE (which is still to be tuned as we develop compilers to IELE)</li>
</ul>

<h2 id="getinvolved">Get involved</h2>

<p>In the spirit of open source, community-driven development, we will be holding all IELE discussions on our channels</p>

<ul>
<li><a href="https://riot.im/app/#/room/#IELE:matrix.org" title="IELE Riot">#IELE:matrix.org</a> on <a href="https://about.riot.im/" title="riot.im">Riot</a></li>

<li><a href="https://gitter.im/runtimeverification/iele-semantics" title="IELE Gitter">runtimeverification/iele-semantics</a> on <a href="https://gitter.im/" title="Gitter">Gitter</a></li>
</ul>

<p>We encourage any interested parties to engage us, ask questions, contribute code, or build experience with our tools. We are also always looking for contributors able to work on documentation, efficient install/quickstart process for new developers, and more examples and tests. We are hiring, and will be sure to keep an eye open for helpful contributors!</p>

<p>We will also be posting updates on our brand new Twitter page <a href="https://twitter.com/rv_inc" title="Runtime Verification on Twitter">@rv_inc</a>, which we hope any interested developers will follow and interact with.</p>

<p>Let's build more secure smart contracts for everybody, together!</p>

<h2 id="acknowledgements">Acknowledgements</h2>

<p>We warmly thank <a href="https://iohk.io/" title="iohk.io">IOHK</a> for their generous funding support of both <a href="https://github.com/runtimeverification/iele-semantics" title="IELE Semantics, Github">IELE</a> and <a href="https://github.com/kframework/evm-semantics" title="EVM Semantics, Github">KEVM</a>. IELE, in particular, would have not been possible without IOHK's support, its continuous research meetings, and the stimulating technical discussions we had with their research team.</p>

<p>We also thank the K team who defined the <a href="https://github.com/kframework/evm-semantics" title="EVM Semantics, Github">KEVM</a> semantics (see <a href="https://www.ideals.illinois.edu/handle/2142/97207" title="KEVM: A Complete Semantics of the Ethereum Virtual Machine">technical report</a>, too) and verified smart contracts for ERC20 compliance. Their effort and non-trivial proofs at the EVM level led to the quest for a new VM with better support for verification of smart contracts.</p>

<p><small>Artwork, <a href="https://creativecommons.org/licenses/by/4.0/" title="Creative Commons"><i class="fa fa-creative-commons" aria-hidden="true"></i></a> <a href="http://www.beeple-crap.com/resources.php">Mike Beeple</a></small></p>


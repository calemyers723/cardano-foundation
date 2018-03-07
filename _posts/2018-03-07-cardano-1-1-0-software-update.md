---
layout: post
date: 2018-03-07
display_date: 2018-03-07
title: "Cardano 1.1.0 software update"
subtitle: ""
language: en
permalink: /press/cardano-1-1-0-software-update/
defaulturl: /press/cardano-1-1-0-software-update/
slug: cardano-1-1-0-software-update
categories: press
image: blog-9-1.jpg
author: george_agapov
produce_text: This blog article has been produced by IOHK and syndicated by Cardano Foundation for wider distribution.
---

<p style="font-size: 22px;">A major package of improvements and fixes is ready for users</p>

The software update today is the first major release for Cardano since the mainnet was launched at the end of September and it consists of a great deal of work from the development team.<!--break-->

The release contains a few new features that are aimed at improving the user experience. And it also contains a set of important fixes for many of the bugs that were identified since the last release, Cardano SL 1.0.3. [Here is Charles Hoskinson, CEO of IOHK, with a video update about this release](https://www.pscp.tv/w/1dRJZeyZOagGB), and below we outline the most significant changes delivered. Users will notice the changes take effect tomorrow.

The team has been working hard to address the issues some users have experienced with Daedalus and this update contains fixes for some of the problems.

<div class="videoframe">
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/GLciKKGPeTg" frameborder="0" allowfullscreen=""></iframe>
</div>

With this release, Daedalus will detect when the time on a user’s machine is out of sync with the global time and will display an error message asking the user to fix the issue. Before this feature was added when there was a time difference of 20 seconds or more, the Cardano node was unable to connect to the network and validate the blockchain, and Daedalus would be held on the loading screen with the “Connecting to network” message. This feature will eliminate the problem of users being held on the loading screen because of the time difference issue.

Several other instances of the user being stuck on the “Connecting to network” screen were fixed. Many issues that can lead to this have been partially or completely fixed. Problem areas include node shutdown, networking and block retrieval mechanisms.

A new “Support request” feature enables users to report a problem directly from Daedalus. This will automatically include log files along with the problem report. By always including log files, this feature will help the development team to investigate and solve the problems that users are experiencing. This feature is accessible from the main user interface and from the loading screen when there is a delay while connecting to the network or when blockchain syncing stops.

Blockchain retrieval performance and reliability has been gradually improved, in particular bugs have been fixed that caused significant slowdown in syncing to the network after reaching 99.9%, and caused occasional network disconnections. Handling of whether Daedalus is connected or disconnected is improved, and a lost internet connection is now detected and brings the user to the loading screen to indicate that wallet is not currently operational.

In addition to individual fixes, importantly, this major release is the first time-based release containing significant new code, and represents an improvement in our development process. All previous releases of Cardano were scope-based, i.e. the goal was to deliver a particular scope and often the release was repeatedly postponed because of inaccurate estimations on having the scope ready for release.

There is much debate among software developers on which release process is preferable. As was outlined in our [previous blog post](https://iohk.io/blog/what-is-our-release-strategy-for-cardano/), the Cardano team has chosen time-based releases. We had a significant backlog of work to resolve to be able to release our development branch to the mainnet – a substantial amount of testing had to be performed because of large amount of new code. But with the release of 1.1.0, we have made a major step forward.

There will be two more time-based releases in the next couple of months containing more improvements, fixes and new features for Cardano. New features for the Shelley phase of development will begin to be released in Q2 and continue through Q3. For more information see the [Cardano Roadmap](https://cardanoroadmap.com).

<small>
  Artwork, 
  <a href="https://creativecommons.org/licenses/by/4.0/" title="Creative Commons" target="_blank">
    <i class="fa fa-creative-commons" aria-hidden="true"></i>
  </a>
  <a href="http://www.beeple-crap.com" target="_blank">Mike Beeple</a>
</small>

<figure class="alignleft">
  <img src="/images/blog/blog-8-7.png" alt="Alfred and Yvonne" width="100" height="">
</figure>

<style type="text/css">
  .videoframe {
    position: relative;
    padding-bottom: 56.25%;
    padding-top: 0px;
    height: 0;
    margin-bottom: 20px;
  }
</style>
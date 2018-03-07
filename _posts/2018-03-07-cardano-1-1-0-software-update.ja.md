---
layout: post
date: 2018-03-07
display_date: 2018-03-07
title: "カルダノ　1.1.0 ソフトウェアアップデート"
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

<p style="font-size: 22px;">改善と修正が施されたこの主要パッケージは、ユーザーへの提供準備が整っています</p>

今回のソフトウェアアップデートは、mainnetが9月末に発表された以降、カルダノにとってはじめの主要リリースであり、開発チームはこのパッケージに膨大な工程を費やしました。<!--break-->

このリリースには、ユーザーエクスペリエンスの向上を目的とした新機能が含まれています。そして最後のリリースであるカルダノSL1.0.3以降に特定されたバグの修正分も含まれています。IOHKの最高経営責任者であるチャールズ・ホーキンソンが今回のリリースに関する[ビデオアップデート](https://www.pscp.tv/w/1dRJZeyZOagGB)を掲載しました。以下に、このリリースの重要な変更点の概要を説明いたします。ユーザーは明日に変更が反映されることに気付きます。

開発チームは、一部のユーザーがダイダロスで経験している問題に対処するため尽力し、このソフトウェア更新では、それらの修正分も含まれています。

<div class="videoframe">
  <iframe width="100%" height="315" src="https://www.youtube.com/embed/GLciKKGPeTg" frameborder="0" allowfullscreen=""></iframe>
</div>

このリリースでは、ダイダロスは、ユーザーのマシン上の時間がグローバルタイムと同期していない状態を検出し、その問題の解決をユーザーに求めるエラーメッセージを表示させます。この機能の追加前には、20秒以上の時間差があった場合、カルダノノードは、ネットワークに接続してブロックチェーンを検証できませんでしたし、ダイダロスは、「ネットワークへ接続しています」というローディング画面が表示され続けていました。この機能により、時差の問題によるローディング画面が保持されるというユーザーの問題を解消しました。

「ネットワークへ接続しています」の画面で立ち往生しているユーザーの他の例に関しても修正を施しました。この案件に関連した問題は、部分的または完全に修正されています。問題領域は、ノードのシャットダウン、ネットワーキングおよびブロック復旧メカニズムを含んでいます。

新機能「サポートリクエスト」では、ダイダロスから直接問題を報告できるようになりました。エラーレポート送付時に自動的にログファイルが添付されます。この機能ではログファイルを含めることにより、開発チームはユーザーが直面している問題を正確に理解し、調査、解決できるようになりました。この機能はメインのユーザーインターフェース、そしてローディング画面から、さらにネットワーク接続の際の遅延時、ブロックチェーンの同期が停止した時にも新機能へのアクセスが可能になっています。

さらにブロックチェーンの復旧性能と信頼性も徐々に改善されています。99.9％に達した後にネットワーク同期において顕著な減速状態を引き起こしていた特定のバグは修正されました。そして時折ネットワークの切断を引き起こしていましたが、こちらも修正済です。ダイダロスが接続または切断されているか否かのハンドリング技術も向上し、インターネットの接続ロスを検出できるようになり、ユーザーにローディング画面を表示し、ウォレットが現在動作していないことをお知らせできるようになりました。

個々の修正に加えて、この主要リリースは新しいコードを多数含むはじめてのタイムベースのリリースで、私たちの開発プロセスの改善もいたしました。以前のカルダノのリリースはスコープベースで、すなわち目標は特定のスコープを提供することのみでした。多くの場合、スコープのリリースに関する不確かな見積もりのために、リリースが延期されることが度々起っていました。

今回からのリリースプロセスはソフトウェア開発者の間で多くの議論があります。[以前のブログ記事](https://cardanofoundation.org/ja/press/what-is-our-release-strategy-for-cardano/)でご説明したとおり、カルダノチームは、タイムベースのリリースを選択しました。mainnet開発時には作業に関する多数のバックログを解決する必要がありました。新たに大量のコードを実行させるため、膨大なテストも施行しました。しかし今回の1.1.0のリリースによって、私達は大きな前進をした事を実感しています。

この数カ月でさらに2つのタイムベースのリリースを予定しています。それにはカルダノの改良、修正や新機能を含んでいます。シェリー・フェーズの新機能がQ2にリリースされ、工程はQ3を通じて継続されます。詳細については、カルダノ[ロードマップ](https://cardanoroadmap.com/jp/)をご覧ください。

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
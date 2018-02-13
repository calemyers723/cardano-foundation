---
layout: post
date: 2018-01-02
title: "IELE：ブロックチェーンのための新しい仮想マシン"
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

<p>ランタイム・ベリフィケーション(RV) は、ブロックチェーン用の新しい仮想マシンであるIELEの最初のバージョンをリリースすることを誇りに思っています。</p>

<h2 id="iele">IELEとは？</h2>

<p>IELEは、ブロックチェーンでスマートコントラクトを実行するために特化した<a href="http://llvm.org/">LLVM</a>の変種です。その設計、定義、実装は、スマートコントラクトを主要な目的として検証するセマンティクス・ファーストのアプローチに従って、最高の数学的基準で行われてきました。具体的には、Kフレームワークを使用したIELEの正式な構文とセマンティクスを定義しました。これは、プログラム検証ツールを含む一連のプログラム分析ツールに加えて実行可能な参照モデルを提供します。<a href="http://kframework.org/">K</a>は私たちのチームによって過去15年間に作成されたもので、最新の言語設計、セマンティクス、および形式手法を取り入れています。IELEの設計は、<a href="https://github.com/kframework">Kで数十の言語</a>を形式的に定義した経験に基づいていますが、特にKで2つの他の仮想マシンを正式に定義している間の経験と教訓を参考にしています。</p><!--break-->

<ul>
<li><a href="https://github.com/kframework/evm-semantics">KEVM</a>、<a href="https://github.com/ethereum/yellowpaper">Ethereum仮想 マシン</a>(EVM)の意味論。</li>

<li><a href="http://llvm.org/">LLVM</a>の意味論であるKLLVM; LLVMセマンティクスの最新バージョンは完成され次第一般公開されます。初期バージョンはすでに<a href="https://github.com/kframework/llvm-semantics">利用可能</a>です。</li>
</ul>

<p>スタックベースのマシンであるEVMとは異なり、IELEはLLVMのようなレジスタベースのマシンです。無制限の数のレジスタを持ち、無制限の整数もサポートしています。IELEプログラムの挙動を知るために、参考となるものが2つあります（これらはまだ検証されておらず、変更されるかもしれません）：</p>

<ul>
<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-examples/erc20.iele">erc20.iele</a> - ERC20トークンのIELE実装</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-examples/forwardingWallet.iele">forwardingWallet.iele</a> - 別の契約を作成して呼び出すウォレットの実装</li>
</ul>


<h3 id="">設計原理</h3>

<p>IELEの設計が進んだのは以下のような理由からです。</p>

<ol>
<li><p>スマートコントラクトを高水準の言語から翻訳し実行するための、一律で低水準のプラットフォームとして目的に資すること。コントラクトはアプリケーション・バイナリー・インターフェイス(ABI)によって相互に作用します。ABIはIELEの中核となる要素であり、単なる最先端の規約ではありません。整数は無制限、レジスタ数も無制限であるため、高水準の言語からのコンパイルが、いっそう簡潔でエレガントに、そしてLLVMの成果を考えれば、長期的にはさらに効率的になるはずです。実のところ、LLVMの最適化手法の多くが引き継がれると考えられています。そのため、IELEは可能な限りLLVMの設計上の選択や表現にしたがいました。チームには（LLVMを開発した）イリノイ大学のLLVMの専門家も加わっています。</p></li>

<li><p>すべての言語に及ぶ一律の手数料（ガス）モデルを提供すること。IELEのガス計算の一般的な設計哲学は「制約はないが、消費した分の代価を払うこと」です。たとえば、IELEプログラムが使用するレジスタ数が多くなればなるほど必要なガスも多くなります。あるいは、実行時間内に計算する数が大きくなればなるほどガスは多く必要となり、使用メモリが増えれば増えるほど（さまざまな場所に格納されたデータの位置とサイズ双方の観点から）ガスがいっそう増大する、といった具合です。</p></li>

<li><p>
  安全なスマートコントラクトをより簡潔に記述できるようにすること。これには、スマートコントラクトがしたがわなくてはならない要求事項を詳述すること、加えて、その詳細に関してスマートコントラクトの妥当性を立証する自動化技術をさらに開発しやすくすることも含みます。たとえば、どうにかして計算した数をスタックにプッシュし、それをアドレスとみなしてジャンプすると、現在のスマートコントラクトの枠組みでは立証は困難となり、それゆえに安全性は低下します。IELEには、LLVMと同じように名前のついたラベルがあり、ジャンプ文がそういったラベルへジャンプできるのです。またIELEは制限のあるスタックを使用しません。さらに、スタックや桁あふれを懸念する必要がないおかげでスマートコントラクトについて詳述し、立証するのははるかにたやすくなります。
</p>  <p>
<a href="http://www.kframework.org/index.php/Main_Page">Kフレームワーク</a>を用いてすでに定義し、実証し、評価したEVMの形式的セマンティクスである<a href="https://github.com/kframework/evm-semantics ">KEVM</a>と同様に、IELEの設計もセマンティクスベースのスタイルでKを用いて行なわれました。まだ開発中のKの高速な（LLVMベースの）実行バックエンドとともに、IELEのセマンティクスから自動的に得られるインタープリタは効率が非常に良く、IELEのレファレンス実装として役に立つだろうと期待されています。</p></li>
</ol>

<h3 id="-1">次は何をするか？</h3>

<p>IELEの潜在能力を最大限に引き出すために、次の作業として計画しているのは以下の事柄です。</p>

<ul>
<li><p>Kの効率的なバックエンド。これによってIELEをはじめとするKセマンティクスは、許容可能なパフォーマンスで実行できます。KEVM paperで述べているように、Kの現行バージョンがEVMセマンティクスを実行するパフォーマンスは、<a href="https://github.com/ethereum/cpp-ethereum/">EVMのC++リファレンス実装</a>のパフォーマンスよりも1桁小さい範囲内にとどまっています。Kの実行パフォーマンスを1桁分向上させることはできると確信しています。これが達成できれば、暫定的な方法でIELEを実装する必要はありません。IELEの実行可能なKセマンティクスがその実装にもなり、Correct-by-Construction手法によって、もはやVM自体の実装欠損が弱点として悪用されたりはしません。またIELE自体も保守しやすいでしょうし、先々のバージョン展開がやりやすくなるでしょう。</p></li>

<li><p><a href="https://solidity.readthedocs.io/en/develop/">Solidity</a>と<a href="https://cardanodocs.com/technical/plutus/introduction/">Plutus</a>からIELEへのコンパイラ／トランスレータ。IELEに直接スマートコントラクトを記述するほうが、EVMに記述するよりも適しています。なぜならば、IELEは、人間に読み取れるように設計されたLLVM IRにしたがうからです。しかしそれでもIELEのコードは低水準であるため、エラーを起こしやすいのです。IELEを適正にテストし、全体設計や機能への信頼を獲得するために、SolidityからIELEへの、やはりKでのコンパイラ／トランスレータを実装することになるでしょう。スマートコントラクトのための実用本位なプログラム言語のなかでもPlutusはとりわけ人気となっていますし、また<a href="https://github.com/kframework/plutus-core-semantics">Plutusの形式的セマンティクス</a>も定義しているので、<a href="https://solidity.readthedocs.io/en/develop/">Solidity</a>からIELEへのコンパイラに続いて<a href="https://cardanodocs.com/technical/plutus/introduction/">Plutus</a>からのコンパイラもすぐに開発されるでしょう。</p></li>

<li><p>セマンティクスベースのコンパイル。Kのパフォーマンス向上に加えて、Kの最先端のツールを提供する計画です。このツールをセマンティクスベースのコンパイラと呼んでいます。詳細は以前の<a href="https://runtimeverification.com/blog/?p=459">ブログ投稿</a>を参照してください。考え方としては次の通りです。プログラム言語のセマンティクスLとLのプログラムPを用いて、（シンボリック実行をしっかりと行ない）新しい言語セマンティクスL′を生成するのです。L′はP向けにLを特殊化したものです。少なくとも1桁分はパフォーマンスが向上すると予測しています。何より、これによってKセマンティクスに沿う任意のプログラム言語の任意のプログラムをIELEにトランスレートする一律な仕組みができ、こうしてIELE、およびKは任意の言語でスマートコントラクトを実行する普遍的プラットフォームになるでしょう。
</p></li><li><p>
CardanoブロックチェーンでのIELEの利用。</p></li>
</ul>

<h3 id="-2">技術面の詳細とダウンロード</h3>



<p>IELEはGithub上にあり、徹底的に議論されていますし、（MITライセンスと同様に寛容な）UIUCライセンスの元で自由に利用可能です。</p>

<ul><li><a href="https://github.com/runtimeverification/iele-semantics">Github上のIELEリポジトリ</a></li></ul>

<p>上述した2つのIELEプログラム、つまりIELEのコードは人間にも読み取れることを示すerc20.ieleとforwardingWallet.ieleに加え、以下に示すgithubリポジトリへのリンクから、IELEとは何か、および、EVMやLLVMと何が違うのかがよく理解できるでしょう。</p>
<ul>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-syntax.md">iele-syntax.md</a> - IELE言語の形式的構文一式。</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele.md">iele.md</a> - IELE言語の形式的実行可能セマンティクス一式。</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/Design.md">Design.md</a> - IELEの設計原理、およびLLVMやEVMとの詳細な比較。</li>

<li><a href="https://github.com/runtimeverification/iele-semantics/blob/master/iele-gas.md">iele-gas.md</a> - IELEの現状のガスモデル（IELEへのコンパイラ開発時には、いまだにこれにあわせて調整されます）</li>
</ul>




<h3 id="-3">関連事項</h3>

<p>オープンソース、コミュニティ主導による開発という精神の元、IELEに関する議論はすべて、以下に示す手段で継続するつもりです。</p>

<ul>
<li><a href="https://about.riot.im/">ライオット</a>上では<a href="https://riot.im/app/#/room/#IELE:matrix.org">#IELE:matrix.org</a></li>

<li><a href="https://gitter.im/">ギッター</a>上では<a href="https://gitter.im/runtimeverification/iele-semantics">runtimeverification/iele-semantics</a>

<p>関心をお持ちでしたらどんな方々でも、参加し、疑問点を出し、コードを寄せ、あるいは私たちのツールを経験してください。ドキュメント、初めて開発する人向けの効率的なインストール／クイックスタートプロセス、例やテストの充実に取り組める協力者をつねに求めてもいます。力を貸してくださる方を採用していますし、人材募集は今後も継続するつもりです！
開設したばかりのツイッターページ<a href="https://twitter.com/rv_inc">@rv inc</a>
</p><p>
に最新情報を投稿します。関心をお持ちの開発者の方はこれをフォローし、交流してください。</p><p>さらに安全性の高いスマートコントラクトをご一緒に構築しましょう！</p></li>
</ul>

<h3 id="-4">謝辞</h3>

<p>IOHKに対し、<a href="https://github.com/runtimeverification/iele-semantics">IELE</a>と<a href="https://github.com/kframework/evm-semantics">KEVM</a>の双方に惜しみなく資金援助をしてくださったことに心より感謝します。特にIELEは、<a href="https://iohk.io/">IOHK</a>からの援助、継続的な研究会合、それにIOHKの研究チームと交わした刺激的な技術的議論があったからこそ実現できたのです。
</p><p>また、Kチームにも感謝いたします。<a href="https://github.com/kframework/evm-semantics">KEVM</a>セマンティクスの定義を行ない（<a href="https://www.ideals.illinois.edu/handle/2142/97207">テクニカルサポート</a>も参照のこと）、ERC20コンプライアンスのためのスマートコントラクトを立証してくださいました。Kチームの尽力とEVM水準での重要な証明のおかげで、スマートコントラクトの立証に向けたより有益な支援を得て、新たなVM探究が可能となりました。</p>

<p><small>Artwork, <a href="https://creativecommons.org/licenses/by/4.0/" title="Creative Commons"><i class="fa fa-creative-commons" aria-hidden="true"></i></a> <a href="http://www.beeple-crap.com/resources.php">Mike Beeple</a></small></p>





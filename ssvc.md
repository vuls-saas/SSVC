[元論文](https://resources.sei.cmu.edu/asset_files/WhitePaper/2021_019_001_653461.pdf)

# Introduction (序章)

<details><summary>原文</summary><div>

This document defines a testable Stakeholder-Specific Vulnerability Categorization (SSVC) for prioritizing actions during vulnerability management.
The stakeholders in vulnerability management are diverse.
This diversity must be accommodated in the main functionality, rather than squeezed into hard-to-use optional features.
Given this, we aim to avoid one-size-fits-all solutions as much as it is practical.
We will improve vulnerability management by framing decisions better.
The modeling framework determines what output types are possible, identifies the inputs, determines the aspects of vulnerability management that are in scope, defines the aspects of context that are incorporated, identifies how to handle changes over time, describes how the model handles context and different roles, and determines what those roles should be.
</div></details>

このドキュメントは、脆弱性管理中にアクションを優先するためのテスト可能な利害関係者固有の脆弱性分類（SSVC）を定義しています。
脆弱性管理における利害関係者は多様です。
この多様さは、使いづらいオプション機能に詰め込むのでなく、主要な機能に対応する必要があります。
これをうけて、実用的な範囲で万能な解決策を回避することを目指します。
意思決定をよりよくフレームワーク化することにより、脆弱性管理を改善します。
フレームワークのモデリングとはどの形式の出力が可能であるかを決定し、入力を識別し、範囲内の脆弱性管理の側面を決定し、組み込まれているコンテキストの側面を定義し、時間の経過とともに変更を処理する方法を識別し、モデルがコンテキストと様々な役割を処理する方法を説明し、そしてそれらの役割のすべき振る舞いを決定します。

<details><summary>原文</summary><div>

As such, the modeling framework is important but difficult to pin down.
We approach this problem as a satisficing process.
We do not seek optimal formalisms, but an adequate formalism.
Our decision-making process is based on decision trees. A decision tree represents important elements of a decision, possible decision values, and possible outcomes.
We suggest decision trees as an adequate formalism for practical, widespread advice about vulnerability prioritization.
We do not claim this approach is the only viable option.
We suggest that specific vulnerability management stakeholder communities use decision trees.
These suggestions are hypotheses for viable replacements for CVSS in those communities, but the hypotheses require empirical testing before they can be justifiably considered fit for use.
</div></details>

このように、フレームワークの組み立ては重要だがはっきりさせるのが難しい。
私たちは、満足のいくプロセスをもってこの問題に取り組みます。
私たちは最適化した形式主義を求めていませんが、適切な形式主義を求めます。
私達の意思決定プロセスは決定木に基づいています。決定木は、決定の重要な要素、考えられる決定値、および考えられる結果を表します。
私たちは、脆弱性の優先順位付けについての実用的な広範なアドバイスのための適切な形式として、意思決定木を提案します。
このアプローチは唯一の実行可能なオプションです。
私たちは、このアプローチが唯一の実行可能な選択肢であると主張していません。
特定の脆弱性管理の利害関係者コミュニティが決定木を使用することをお勧めします。
これらの提案は、それらのコミュニティにおけるCVSS運用に実現可能な代替にむけた仮説であるが、利用に適していると正当にみなされる前に、経験的な仮説が必要である。

<details><summary>原文</summary><div>

We propose a methodology for such testing.
This document describes version 2 of SSVC.
The main improvements from version 1 are the addition of the coordinator stakeholder perspective, improvements to terminology, integration of feedback on decision point definitions, and tools to support practical use.
These changes are described in more detail in Version 2 Changelog.
The document is organized as follows.
</div></details>

このようなテストのための方法論を提案する。
この文書では、SSVCのバージョン2について説明します。
バージョン1からの主な改善点は、コーディネーターの利害関係者の展望、用語の改善、意思決定点の定義に関するフィードバックの統合、および実用的な使用をサポートするためのツールの追加です。
これらの変更は、バージョン2の変更要素で詳しく説明されています。
文書は次のように編成されています。

<details><summary>原文</summary><div>

- Current State of Practice summarizes the current state of vulnerability management.
- Representing Information for Decisions About Vulnerabilities describes our design goals for an improved prioritization method.
- Vulnerability Management Decisions defines who the decision makers are and what options they are deciding among.
- Likely Decision Points and Relevant Data proposes a definition of decision points that a stakeholder might use during vulnerability management.
- Prioritization combines these decision points into example decision trees that can be used to prioritize action on a work item.
- Evaluation of the Draft Trees describes an early test of this method against the design goals, as much to show an adequate usability test methodology as for the results.
- Worked example provides examples of applying the methodology to sample vulnerabilities and discusses the relationship between SSVC and other vulnerability management prioritization systems.
- Future Work identifies ideas we haven’t had time to incorporate yet.
- Limitations identifies limitations in the design.
- Conclusion provides some final thoughts.
</div></details>

- [Current state of practice (現在の実践の状態)](#current-state-of-practice-現在の実践の状態)は、現在の脆弱性管理の状態をまとめたものです。
- [Representing Information for Decisions About Vulnerabilities (脆弱性についての決定に関する情報の表現)](#representing-information-for-decisions-about-vulnerabilities-脆弱性についての決定に関する情報の表現)は改善された優先順位付け方法のの設計目標を説明します。
- [Vulnerability Management Decisions (脆弱性管理の決定)](#vulnerability-management-decisions-脆弱性管理の決定)は、意思決定者が誰であるか、その人たちがどの選択肢を決定するかを定義します。
- [Likely Decision Points and Relevant Data(可能性のある決定ポイントと関連データ)](#likely-decision-points-and-relevant-data（可能性のある決定ポイントと関連データ）)は利害関係者が脆弱性管理の元で利用できる決断の定義を提案します。
- [Prioritization (優先順位付け)](#Prioritization)はこれらの決断を組み合わせ、作業項目のアクションの優先順位付けに使用できる実用的な決定木にします。
- [Evaluation of the Draft Trees(ドラフトツリーの評価)](#evaluation-of-the-draft-trees)は、設計目標に対するこの方法の初期のテストについて説明し、結果と同様に適切なユーザビリティテストの方法論を示しています。
- [Worked example(作業された例)](#worked-example)では、この方法論をサンプルの脆弱性に適用する実例を示し、SSVCとその他の脆弱性管理優先順位付けシステムとの関係について説明します。
- [Future Work(将来の作業)](#future-work)は、まだ組み込む時間がなかったアイデアをはっきりとさせています。
- [Limitations(限界)](#limitations)この設計の限界をはっきりとさせています。
- [Conclusion(結論)](#conclusion)はいくつかの最終的な考えを提供します。

## Current state of practice (現在の実践の状態)

<details><summary>原文</summary><div>

*Vulnerability management* covers “the discovery, analysis, and handling of new or reported security vulnerabilities in information systems \[and\] the detection of and response to known vulnerabilities in order to prevent them from being exploited” (Benetis et al. 2019).
Prioritization of organizational and analyst resources is an important precursor to vulnerability analysis, handling, and response.
The general problem is: given limited resources, which vulnerabilities should be processed and which can be ignored for now.
We approach this problem from a pragmatic, practitioner-centered perspective.
The de facto standard prioritization language is CVSS (Spring and Illari 2019).
CVSS avoids discussing decisions and, instead, takes *technical severity* as its fundamental operating principle.
</div></details>

*脆弱性管理*とは情報システムにある新規または報告済のセキュリティ脆弱性を発見し、分析し、対応し、それだけでなく攻撃されることを防ぐため既知の脆弱性に対し方針決定し反応することまでを対象としています。(Benetis et al. 2019)
組織と分析者のリソースの優先順位付けは脆弱性の分析・取組み・対応することに先駆けて重要です。
一般的な問題は、次のとおりです。限られたリソースを踏まえると、どの脆弱性は処理するべきでどの脆弱性は今は無視できるか。
私たちは、実用的で実務者中心の観点からこの問題に取り組んでいます。
事実上標準優先順位付け言語はCVSS（Spring and Illari 2019）です。
CVSSは決定の議論を避け、代わりにその基本的な動作原則として*技術的な重大度*を取ります。

<details><summary>原文</summary><div>

However, the standard does not provide clear advice about how CVSS scores might inform decisions (Wiles and Dugal 2019).
SSVC instead considers technical severity as one decision point in vulnerability management.
Severity should only be a part of vulnerability response prioritization (See, e.g., Farris et al. 2018).
Vulnerability managers make decisions at a particular time in a specific context. CVSS base scores are static; we will make SSVC from modular parts that are easier to compose in each manager’s temporal and operational context.
Any re-adaptation of the basic CVSS mindset inherits its deeper issues.
For example, arguments for the CVSS scoring algorithm have not been transparent and the standardization group has not justified the use of the formula either formally or empirically (Spring et al. 2018).
One complaint is that a high CVSS score does not predict which vulnerabilities will be commonly exploited or have exploits publicly released (Allodi and Massacci 2012).
Studies of consistency in CVSS scoring indicate that analysts do not consistently interpret the elements of a CVSS version 3.0 score (Allodi et al. 2018).
Because many adaptations of CVSS simply add additional metrics, we expect they will inherit such inconsistency.
Analyst usability has so far been an afterthought, but we know from other areas of information security that usability is not well-served as an afterthought (Garfinkel and Lipford 2014).
SSVC aims to learn from and improve upon these issues.
</div></details>

ただし、CVSSスコアが決定を知らせる方法についての明確なアドバイスを提供していません（Wiles and Dugal 2019）。
SSVCは代わりに、脆弱性管理の1つの決断に技術的な重大度を考慮します。
重大度は、脆弱性対応の優先順位付けの一部であるべきである（例えば、Farris et al。2018）。
脆弱性管理者は、特別なコンテキストで特定の時間に決定を下します。CVSSベーススコアは静的です。なのでSSVCは、それぞれの管理者の一時的な、運用上のコンテキストの基でより組み立てやすいモジュール部品から作ります。
基本的なCVSSの考えを再適応することは、より深い問題を継承してしまいます。
たとえば、CVSSスコアリングのアルゴリズムの透過性がなく、標準的なグループでは、正式にまたは経験的にこの方式の使用を正当化していません（Spring et al.18）。（※1）
1つの批判は、CVSSスコアが高いということは、その脆弱性が一般的に悪用されている、またはその脆弱性が公に公開されているといったことを予測しているわけではないということです。（AllodiとMassacci 2012）
CVSSスコアリングにおける一貫性の研究は、アナリストがCVSSバージョン3.0スコアの要素を一貫して解釈しないことを示している（Allodi et al。2018）。
CVSS適応（※2）の多くは単に測定基準を追加するだけなので、上記の矛盾は引き継がれてしまうと読んでいます。
アナリストの使いやすさとはこれまでのところ後付けでしたが、私たちは他の情報セキュリティの他の分野から、使いやすさとは後付けと同様によく役立たないことをわかっています（Garfinkel and Lipford 2014）。
SSVCはこれらの問題を学び、改善することを目指しています。

※1原文のstandardization groupが訳せなかったですが、CVSSでは一般的な組織・及び組織内のグループでCVSSをどう使うかを公式では定めていない　という意味合いかと。  
※2CVSSv1.0→v2.0→v3.0...等と、現状に適応することを指している  

<details><summary>原文</summary><div>

Surveys of security metrics (Pendleton et al. 2016) and information sharing in cybersecurity (Laube and Böhme 2017) do not indicate any major efforts to conduct a wholesale rethinking of *vulnerability* prioritization.
The surveys indicate some options a prioritization method might consider, such as exploit availability or system attack surface.
Representing Information for Decisions About Vulnerabilities describes our design goals for a pragmatic prioritization methodology that can improve and build on the state of current practice.
The target audience for SSVC is vulnerability managers of any kind.
SSVC assumes that the vulnerability manager has identified that there is a vulnerability.
We take our definition of vulnerability from (Householder, Wassermann, et al. 2020): “a set of conditions or behaviors that allows the violation of an explicit or implicit security policy.” A variety of problems or issues with computer systems are important but are not vulnerabilities.
SSVC presents a risk prioritization method that might be useful or at least allied to other risk management methods for these other kinds of issues.
However, for this work we focus on decisions in the situation where there is a vulnerability and the vulnerability management team wants to decide what to do about it.
</div></details>

セキュリティメトリクスの調査（Pendleton et al。2016.206）およびサイバーセキュリティ（Laube andBöhme2017）の情報共有は脆弱性の優先順位付けについて棚卸の再考を行うための主要な取り組みを指し示すものではありません。
この調査は、攻撃の可用性、システム攻撃の表層がある等を考慮した優先順位付け方法を選択肢として指し示しています。
脆弱性に関する情報を表す情報を表す現在の実践の状態を改善し構築することができる実用的な優先順位付け方法論のための我々の設計目標を説明しています。
SSVCの対象者は、どんな種類の脆弱性管理者にも当てはまります。
SSVCは、脆弱性管理者は脆弱性が存在することを認識していると想定しています。
私達は脆弱性の定義を（HouseHolder、Waspermann、et al.2020）： "明示的または暗黙的なセキュリティポリシーの違反を可能にする一連の条件または動作"とします。コンピュータシステムに関するさまざまな問題や課題は重要ですが、それは脆弱性ではありません。
SSVCは、有用で少なくとも他の問題に対するリスク管理手法をまとめ上げたリスク優先順付け方法の提案です。
しかし、今回の提案では、脆弱性が存在するなか脆弱性管理チームがその脆弱性に何をすべきか決断したいという状況について焦点をあてています。


## Representing Information for Decisions About Vulnerabilities (脆弱性についての決定に関する情報の表現)

<details><summary>原文</summary><div>

We propose that decisions about vulnerabilities—rather than their severity—are a more useful approach.
Our design goals for the decision-making process are to clearly define whose decisions are involved; properly use evidentiary categories; be based on reliably available evidence; be transparent; and be explainable.
Our inspiration and justification for these design goals are that they are the features of a satisfactory scientific enterprise (Spring, Moore, and Pym 2017) adapted to the vulnerability management problem.
To consider decisions about managing the vulnerability rather than just its technical severity, one must be clear about whose decisions are involved.
Organizations that produce patches and fix software clearly have different decisions to make than those that deploy patches or other security mitigations.
For example, organizations in the aviation industry have different priorities than organizations that make word processors.
These differences indicate a requirement: any formalism must adequately capture the different decisions and priorities exhibited by different groups of stakeholders.
As a usability requirement, the number of stakeholder groups needs to be small enough to be manageable, both by those issuing scores and those seeking them.
The goal of adequacy is more appropriate than optimality.
Our search process need not be exhaustive; we are satisficing rather than optimizing (Simon 1996).
Finding any system that meets all of the desired criteria is enough.
Decisions are not numbers.
</div></details>

その脆弱性がどれほど重大かよりも脆弱性の程度について決断することがより有用な試みであると提案します。
意思決定プロセスのための私達の設計目標は、その決定が関与していることを明確に定義することです。すなわち証明された分類を適切に利用し、確実で利用可能なエビデンスに基づき、透明性があり、そして説明可能であることです。
これらの設計目標に向けた私たちのインスピレーションと正当化は、それらが脆弱性管理問題に適応した満足のいく科学企業（Spring, Moore, and Pym 2017）の特徴であるということです。
技術的な重大度ではなく脆弱性を管理することについての決定を考慮するためには、その決定に関与したものについて明確でなければなりません。
パッチや修正ソフトウェアを作成する組織は、パッチやその他セキュリティ緩和方法を適用する人と明らかに違った決定を下します。
たとえば、航空業界の組織は、単語プロセッサーを作る組織と異なる優先順位を持っています。
これらの違いは右の要件を示しています：適切にさまざまなステークホルダーの集団によって示された様々な決断と優先順位を適切に捉えられるような形式主義でないといけません。
使いやすさの要件として、ステークホルダーグループの数は、スコアを発行しているスコアとそれらを求めるものとの両方によって管理可能なように十分に小さい必要があります。
妥当性の目標は、最適性よりも適切性です。
私たちの追及プロセスは網羅的な必要はありません。最適化しなくても、満足いくものです（Simon 1996）。
すべての要求された基準を満たすシステムを見つけられれば十分です。
決定は数字ではありません。

<details><summary>原文</summary><div>

They are qualitative actions that an organization can take.
In many cases, numerical values can be directly converted to qualitative decisions.
For example, if your child’s temperature is 105°F (40.5°C), you decide to go to the hospital immediately.
Conversion from numerical to qualitative values can be complicated by measurement uncertainty and the design of the metrics. For example, CVSS scores were designed to be accurate with +/- 0.5 points of the given score (CVSS SIG 2019, sec.  7.5). Therefore, under a Gaussian error distribution, 8.9 is really 60% high and 40% critical since the recommended dividing line is 9.0. SSVC decisions should be distinct and crisp, without such statistical overlaps.
We avoid numerical representations for either inputs or outputs of a vulnerability management decision process.
Quantified metrics are more useful when (1) data for decision making is available, and (2) the stakeholders agree on how to measure.
Vulnerability management does not yet meet either criterion.
Furthermore, it is not clear to what extent measurements about a vulnerability can be informative about other vulnerabilities.
Each vulnerability has a potentially unique relationship to the socio-technical system in which it exists, including the Internet.
The context of the vulnerability, and the systems it impacts, are inextricably linked to managing it.
Temporal and environmental considerations should be primary, not optional as they are in CVSS.
We make the deliberation process as clear as is practical; therefore, we risk belaboring some points to ensure our assumptions and reasoning are explicit.
</div></details>

組織が取ることができるのは定性的な行動だけです。
多くの場合、数値は定性的な決定に直接変換することができます。
たとえば、子供の気温が105°F（40.5°C）の場合、すぐに病院に行くことにします。
数値から定性的な値への変換は、測定の不確かさと指標の設計によって複雑になります。たとえば、CVSSスコアは、与えられたスコアの+/- 0.5ポイントで正確になるように設計されていました（CVSS SIG 2019、Sec.7.5）。したがって、ガウス誤差分布の下では、推奨の境界線は9.0であるため、8.9は実際には60％高く、40％が重要です。 SSVCの決定は、そのような統計的な重なりがなく、明確で鮮明であるべきです。
脆弱性管理決定プロセスの入力または出力のいずれかについての数値表現を避けます。
定量化された測定基準は次の場合により有用です。（1）意思決定のためのデータが利用可能であるとき、（2）利害関係者が測定方法について同意しているとき。
脆弱性管理はまだこれらの基準を満たしていません。
さらに、脆弱性について追加で調査することが、どの程度有益であるかも明らかではありません。
各脆弱性は、インターネットを含む、それが存在する社会技術システムと潜在的に独特な関係を持ちます。
この脆弱性の背景、およびシステムへ与える影響はその脆弱性管理と切っても切れない関係があります。
時間的および環境的な考慮事項は、必須なものであるべきで、CVSSのようにオプションでないべきです。
私たちは審議プロセスを実用的でそれと同じように明確にします。したがって、我々は仮定と推論を確実にするためにいくつかの点を長々と論じる恐れがあります。

<details><summary>原文</summary><div>

Transparency should improve trust in the results.
Finally, any result of a decision-making process should be explainable Explainable is defined and used with its common meaning, not as it is used in the research area of explainable artificial intelligence.
An explanation should make the process intelligible to an interested, competent, non-expert person.
There are at least two reasons common explainability is important: (1) for troubleshooting and error correction and (2) for justifying proposed decisions.
To summarize, the following are our design goals for a vulnerability management process:
- Outputs are decisions.
- Pluralistic recommendations are made among a manageable number of stakeholder groups.
- Inputs are qualitative.
- Outputs are qualitative, and there are no (unjustified) shifts to quantitative calculations.
- Process justification is transparent.
- Results are explainable.
</div></details>

透明度は結果への信頼性を向上するはずです。
最後に、意思決定プロセスの結果はどれも説明可能であるべきです。 説明可能とは、一般的な意味のものを指しています。人工知能の研究分野で使われている説明可能と同じではありません。
説明はプロセスを興味がある人、有能な人、非専門家にわかりやすくするべきです。
一般的な説明が重要な理由は少なくとも2つあります。(1) 原因調査とエラー修正のため (2) 提案された決定を正当化するため
要約すると、脆弱性管理プロセスのための設計目標は次のとおりです。
 - 出力は意思決定です。
 - 管理可能な数の利害関係者グループの間で複数の推奨事項がなされています。
 - 入力は定性的です。
 - 出力は定性的なものであり、定量的計算への（不正な）シフトはありません。
 - プロセス正当化は透明です。
 - 結果は説明可能です。


### Formalization Options

<details><summary>原文</summary><div>

This section briefly surveys the available formalization options against the six design goals described above.
Table 1 summarizes the results.
This survey is opportunistic; it is based on conversations with several experts and our professional experience.
The search process leaves open the possibility of missing a better option.
However, at the moment, we are searching for a satisfactory formalism, rather than an optimal one.
We focus on highlighting why some common options or suggestions do not meet the above design goals.
We argue that decision trees are a satisfactory formalism.
</div></details>

このセクションでは、上記の6つの設計目標に対して利用可能な定式化オプションを簡単に調査します。
結果を表1に要約します。
この調査は日和見主義です。それはいくつかの専門家と私たちの職業経験との会話に基づいています。
この追及のプロセスはより良い選択肢を見逃している問題があるままになっています。
しかし、現時点では、最適なものではなく、満足のいく形式を検索しています。
いくつかの一般的な選択肢や提案が上記の設計目標を満たしていない理由を強調に焦点を当てます。
私たちは、決定木が満足のいく形式であると主張しています。

<details><summary>原文</summary><div>

We rule out many quantitative options, such as anything involving statistical regression techniques or Bayesian belief propagation.
Most machine learning (ML) algorithms are also not suitable because they are both unexplainable (in the common sense meaning) and quantitative.
Random forest algorithms may appear in scope since each individual decision tree can be traced and the decisions explained (Russell and Norvig 2011).
However, they are not transparent enough to simply know how the available decision trees are created or mutated and why a certain set of them works better.
In any case, random forests are necessary only when decision trees get too complicated for humans to manage.
We demonstrate below that in vulnerability management, useful decision trees are small enough for humans to manage.
Logics are generally better suited for capturing qualitative decisions. Boolean first-order logic is the “usual” logic—with material implication (if/then), negation, existential quantification, and predicates.
For example, in program verification, satisfiability problem (SAT) and satisfiability modulo theories (SMT) solvers are used to automate decisions about when some condition holds or whether software contains a certain kind of flaw.
While the explanations provided by logical tools are accessible to experts, non-experts may struggle.
</div></details>

私たちは統計的な回帰分析技術やベイジアン確立伝播に関するような定量的な選択肢を除外します。
ほとんどの機械学習（ML）アルゴリズムは、それらが説明不可能（一般的な意味で）で定量的であるために適していません。
それぞれの決定木は追跡可能で意思決定は説明可能なので、ランダムフォレストアルゴリズムは選択肢の範囲内に表れます。
しかしながら、実行可能な決定木をどのように作成・変更したか、そして何故今の木がよりよく動作するのかを簡単にしれる程、透明性は十分ではありません。
いずれにせよ、ランダムフォレストは決定木が人間が管理するのに複雑すぎる場合にのみ必要です。
脆弱性管理では、決定木は人間が管理するのに十分に小さいと主張します。
論理は一般的に定性的な決定を捉えるために適しています。一回述語論理は、「通常の」論理 - 存在含意（if/ then）、否定、存在定量、および述語です。（※）
たとえば、プログラム検証では、満足度の問題（SAT）および満足度モジュロ理論（SMT）ソルバーは、ある状態が保持されているとき、またはソフトウェアがある種の欠陥を含むかどうかについての決定を自動化するために使用されます。
論理による手法で提供される説明は専門家にはわかりやすいが、非専門家はもがく可能性があります。

※ここ知識不足で訳せないですが、一回述語論理の説明になります。

<details><summary>原文</summary><div>

Under special conditions, logical formulae representing decisions about categorization based on exclusive-or conditions can be more compactly and intelligibly represented as a decision tree.
Decision trees are used differently in operations research than in ML.
In ML, decision trees are used as a predictive model to classify a target variable based on dependent variables.
In operations research and decision analysis, a decision tree is a tool that is used to document a human process.
In decision analysis, analysts “frequently use specialized tools, such as decision tree techniques, to evaluate uncertain situations” (Howard and Matheson 1983, viii).
We use decision trees in the tradition of decision analysis, not ML.
</div></details>

特別な条件下では、排他的論理和条件に基づく分類に関する決定を表す論理式は、決定木としてよりコンパクトにかかりやすく表すことができます。
決定木は、MLよりも運用調査で異なる方法で使用されています。
MLでは、決定ツリーは、従属変数に基づいてターゲット変数を分類するための予測モデルとして使用されます。
事業研究と決定分析では、決定木は人間のプロセスを文書化するために使用されるツールです。
決定分析では、アナリストは「不確実な状況を評価するために、決定木の技術のような特殊なツールを頻繁に使用します」（HowardとMatheson 1983、VIII）。
私たちは、MLではなく、決定分析の伝統の決定木を使用しています。

<details><summary>原文</summary><div>

Table 1: How Vulnerability Prioritization Options Meet the Design Goals

|-|Outputs are Decisions|Pluralistic|Qualitative Inputs|Qualitative outputs|Transparent|Explainable|
|---|:-:|:-:|:-:|:-:|:-:|:-:|
|Parametric Regression|✗|✗|✓|✗|✗|✓|
|CVSS v3.0|✗|✗|✓|✗|✗|✗|
|Bayesian Belief networks|✗|Maybe|✗|✗|✓|✓|
|Neural Networks|✗|✗|✗|✗|✗|✗|
|Random Forest|✓|✓|✓|Maybe|✗|Maybe|
|Other ML|✗|Maybe|✗|✗|✗|✗|
|Boolean First Order Logics|Maybe|Maybe|✓|✓|✓|Maybe|
|Decision Trees|✓|✓|✓|✓|✓|✓|
</div></details>

表1：脆弱性優先順位付けオプションが設計目標を満たす方法

|-|出力が意思決定である|多元性|定性的な入力|定性的な出力|透明|説明可能|
|---|:-:|:-:|:-:|:-:|:-:|:-:|
|パラメトリック回帰|✗|✗|✓|✗|✗|✓|
|CVSS v3.0|✗|✗|✓|✗|✗|✗|
|ベイジアンネットワーク|✗|恐らく可|✗|✗|✓|✓|
|ニューラルネットワーク|✗|✗|✗|✗|✗|✗|
|ランダムフォレスト|✓|✓|✓|恐らく可|✗|恐らく可|
|その他機械学習|✗|恐らく可|✗|✗|✗|✗|
|二値一回述語論理|恐らく可|恐らく可|✓|✓|✓|恐らく可|
|決定木|✓|✓|✓|✓|✓|✓|

### Decision Trees (決定木)

<details><summary>原文</summary><div>

A decision tree is an acyclic structure where nodes represent aspects of the decision or relevant properties and branches represent possible options for each aspect or property.
Each decision point can have two or more options.
Decision trees can be used to meet all of the design goals, even plural recommendations and transparent tree-construction processes.
Decision trees support plural recommendations because a separate tree can represent each stakeholder group.
The opportunity for transparency surfaces immediately: any deviation among the decision trees for different stakeholder groups should have a documented reason—supported by public evidence when possible—for the deviation.
Transparency may be difficult to achieve, since each node in the tree and each of the values need to be explained and justified, but this cost is paid infrequently.
There has been limited but positive use of decision trees in vulnerability management. For example, Vulnerability Response Decision Assistance (VRDA) studies how to make decisions about how to respond to vulnerability reports (Manion et al. 2009).
This paper continues roughly in the vein of such work to construct multiple decision trees for prioritization within the vulnerability management process.
</div></details>

決定木は非巡回構造であり、ノードは決定または関連するプロパティの側面を表し、分岐は各側面またはプロパティの可能な選択肢を表します。
各決定点には2つ以上の選択肢を持つことができます。
決定木は全ての設計目標を満たすために利用可能で、さらに複数の推奨事項または透過性のある木構造のプロセスさえも満たします。
それぞれの木は利害関係者グループ毎に表現できるので、決定木は複数の推奨事項をサポートできます。
透明性への選択機会はすぐに次のことを明らかにします: 異なる利害関係者グループ間で決定木が異なる場合、その逸脱の理由について(可能であれば公的な証拠で裏付された)文書化する必要があります。
ツリー内の各ノードと各値を説明し正当化する必要があるため、透明性を達成するのが難しい場合がありますが、このコストはまれに支払われます。
脆弱性管理における決定木の積極的な使用が制限されています。たとえば、脆弱性対応意思援助（VRDA）は、脆弱性報告書にどのように対応するかについての決定を行う方法を研究します（Manion et al.2009）。
この論文は、脆弱性管理プロセス内で優先順位を付けるための複数の決定木を構築するために、このような作業を大まかに続けています。

### Representation choices (表現の選択肢)

<details><summary>原文</summary><div>

A decision tree can represent the same content in different ways.
Since a decision tree is a representation of logical relationships between qualitative variables, the equivalent content can be represented in other formats as well.
The R package data.tree has a variety of both internal representations and visualizations.
For data input, we elected to keep SSVC simpler than R, and just use a CSV (or other fixed-delimiter separated file) as canonical data input.
All visualizations of a tree should be built from a canonical CSV that defines the decisions for that stakeholder.
Examples are located in SSVC/data.
An interoperable CSV format is also flexible enough to support a variety of uses.
Every situation in SSVC is defined by the values for each decision point and the priority label (outcome) for that situation (as defined in Likely Decision Points and Relevant Data).
A CSV will typically be 30-100 rows that each look something like: 2,none,slow,diffuse,laborious,partial,minor,defer Where “2” is the row number, none through minor are values for decision points, and defer is a priority label or outcome.
Different stakeholders will have different decision points (and so different options for values) and different outcomes, but this is the basic shape of a CSV file to define SSVC stakeholder decisions.
</div></details>

決定木は、異なる方法で同じ内容を表すことができます。
決定木は定性的な変数間での論理関係の表現であるため、同等の内容も他のフォーマットで表すことができます。
Rの`Data.Tree`には、内部表現と視覚化の両方があります。
データ入力については、SSVCをRよりも単純に保ち、CSV（または他の固定区切り文字で区切られたファイル）を正規のデータ入力として使用することを選択しました。
決定木の視覚化は全て、その利害関係者に向けた意思決定を定義した、正規化されたCSVから作り上げられるべきです。
例は`SSVC/data`にあります。（※）
相互運用可能なCSVフォーマットもさまざまな用途をサポートするのに十分柔軟です。
SSVCではあらゆる状況で各決定点と優先順位ラベル（結果）の値によって定義されます（[Likely Decision Points and Relevant Data](#likely-decision-points-and-relevant-data)で定義されているように）
CSVは通常、次のようなものになります。:2, none, slow, diffuse, laborious, partial, minor, defer。2は列番号を表し、none~minorは決定点の値、そしてdeferは優先順位ラベルまたは出力です。
さまざまな利害関係者は、異なる決定点（そして値のためのさまざまなオプション）とさまざまな結果を持ちますが、これはSSVCの利害関係者の決定を定義するためのCSVファイルの基本的な形状です。  


※このリポジトリを指しているものと思われます
https://github.com/CERTCC/SSVC/tree/main/data

<details><summary>原文</summary><div>

The tree visualization options are more diverse.
We provide an example format, and codified it in src/SSVC_csv-to-latex.py.
Why have we gone to this trouble when (for example) the R data.tree package has a handy print-to-ASCII function?
Because this function produces output like the following:
</div></details>

決定木の視覚化オプションはより多様です。
例示的なフォーマットを提供し、`SRC / SSVC_CSV-To-LateX.py`でその文書化しました。※
（例えば）`R data.tree`パッケージには便利なASCII出力関数があるのに、なぜわざわざこんなことをしたのか？
なぜならこの関数は次のように出力を生成するからです。  

※https://github.com/CERTCC/SSVC/blob/main/src/SSVC_csv-to-latex.py

```
1 start
2 ¦--AV:N
3 ¦ ¦--AC:L
4 ¦ ¦ ¦--PR:N
...
31 ¦ ¦ ¦ ¦ ¦ ¦ ¦--A:L Medium
32 ¦ ¦ ¦ ¦ ¦ ¦ °--A:N Medium
33 ¦ ¦ ¦ ¦ ¦ °--C:N
34 ¦ ¦ ¦ ¦ ¦ ¦--I:H
35 ¦ ¦ ¦ ¦ ¦ ¦ ¦--A:H Critical

1 start
2 ¦--AV:N
3 ¦ ¦--AC:L
4 ¦ ¦ ¦--PR:N
...
31 ¦ ¦ ¦ ¦ ¦ ¦ ¦--A:L Medium
32 ¦ ¦ ¦ ¦ ¦ ¦ °--A:N Medium
33 ¦ ¦ ¦ ¦ ¦ °--C:N
34 ¦ ¦ ¦ ¦ ¦ ¦--I:H
35 ¦ ¦ ¦ ¦ ¦ ¦ ¦--A:H Critical
```

<details><summary>原文</summary><div>

This sample is a snippet of the CVSS version 3.0 base scoring algorithm represented as a decision tree.
The full tree can be found in doc/graphics/cvss_tree_severity-score.txt.
This tree representation is functional, but not as flexible or aesthetic as might be hoped.
The visualizations provided by R are geared towards analysis of decision trees in a random forest ML model, rather than operations-research type trees.
</div></details>

このサンプルは、決定木として表されるCVSSバージョン3.0ベーススコアリングアルゴリズムのスニペットです。
完全な木は`doc/graphics/cvss_tree_severity-score.txt`にあります。※
この木の表現は機能的であるが、期待通りな柔軟性があるわけでも美的でもない。
Rによって提供される視覚化は、オペレーションズリサーチ形式の木よりもむしろ、ランダムな森林MLモデルの決定木の分析に向けられています。  

※ファイル名変わっていますが、恐らくこれです。  
https://github.com/CERTCC/SSVC/blob/main/doc/graphics/cvss_tree_score-severity.txt

---

## Vulnerability Management Decisions (脆弱性管理の決定)

<details><summary>原文</summary><div>

This section will define our audience for decision advice and how we are scoping our advice on vulnerability management decisions.
Viable decision guidance for vulnerability management should (at a minimum) consider the stakeholder groups, their potential decision outcomes, and the data needed for relevant decision points.
This section covers the first of these three parts, and the following sections address the other parts in turn.
The “who” is primarily about categories of stakeholders—suppliers, deployers, and coordinators—as well as their individual risk tolerances.
The “what” is about the scope, both in how the affected system is defined and how much of the world an analyst should consider when estimating effects of a vulnerability.
While we strive to make our examples realistic, we invite the community to engage and conduct empirical assessments to test them. The following construction should be treated as an informed hypothesis rather than a conclusion.
</div></details>

このセクションでは、意思決定のアドバイスの対象者と、脆弱性管理の意思決定に関するアドバイスの範囲を定義します。
脆弱性管理に対する実行可能な決定指針（最小限のもの）は、利害関係者グループ、その潜在的な決定結果、および関連する決定点に必要なデータを考慮する必要があります。
このセクションでは、これら3つの部分の最初の部分について説明し、次のセクションでは他の部分について順番に説明します。
「誰が」は主に、利害関係者のカテゴリ（サプライヤー、展開者、コーディネーター）と、それらの個々のリスク許容度に関するものです。
「何を」は範囲について、影響あるシステムがどのように定義されるか、及びアナリストが脆弱性の影響を見積もるときに世界にどの程度まで影響あるか考慮すべきか、という範囲についてです。
私たちは例を現実的にするよう努めていますが、コミュニティにそれらをテストするための経験的評価を実施してもらうよう呼びかけています。次の構成は、結論ではなく、情報に基づいた仮説として扱う必要があります。

### Enumerating Stakeholders (ステークホルダーの列挙)

<details><summary>原文</summary><div>

Stakeholders in vulnerability management can be identified within multiple independent axes.
For example, they can be identified by their responsibility: whether the group supplies, deploys, or coordinates remediation actions.
Depending what task a team is performing in a supply chain, the team may be considered a supplier, deployer, or a coordinator. Therefore, one organization may have teams that take on different roles.
For example, an organization that develops and uses its own software might delegate the supplier role to its development team and the deployer role to its IT operations team.
On the other hand, organizations using a DevOps approach to providing services might have a single group responsible for both the supplier and deployer roles.
Organizations may also be distinguished by the type of industry sector.
</div></details>

脆弱性管理の利害関係者は、複数の独立した軸内で識別できます。
たとえば、それらの責任で識別することができます。どのグループが修正対応を提供、展開、または調整するかで識別できます。
チームがサプライチェーンで実行しているタスクに応じて、チームはサプライヤ、デプロイヤ、またはコーディネーターと見なされることがあります。したがって、1つの組織には、さまざまな役割を果たすチームがあります。
たとえば、独自のソフトウェアを開発して使用する組織は、サプライヤロールを開発チームに、デプロイヤーロールはそのITオペレーションチームに委任する可能性があります。
一方、サービスを提供するためのDevOpsアプローチを使用する組織は、サプライヤとデプロイヤの両方の役割に責任がある単一のグループがあるかもしれません。
組織はまた、業界部門の種類によって区別される可能性があります。

<details><summary>原文</summary><div>

While it might be useful to enumerate all the sectors of the economy, we propose to draft decision points that include those from multiple important sectors.
For example, we have safety-related questions in the decision path for all suppliers and deployers.
The decision will be assessed whether or not the stakeholder is in a safety-critical sector.
The choice not to segregate the decisions by sector is reinforced by the fact that any given software system might be used by different sectors.
It is less likely that one organization has multiple responsibilities within the vulnerability management process.
Even if there is overlap within an organization, the two responsibilities are often located in distinct business units with distinct decision-making processes.
We can treat the responsibilities as non-overlapping, and, therefore, we can build two decision trees—one for each of the “patch supplier” and “patch deployer” responsibilities in the vulnerability management process.
</div></details>

経済のすべての分野を列挙するのは有用であるかもしれませんが、私たちは複数の重要な分野からのものを含む決定点の草案を提案します。
たとえば、すべてのサプライヤやデプロイヤーの意思決定パスに安全関連の質問があります。
決定は、利害関係者が安全性の重要な分野にあるかどうかを評価されます。
分野によって決定を分離しない選択は、特定のソフトウェアシステムがさまざまな分野によって使用される可能性があるという事実によって強化されています。
脆弱性管理プロセス内で複数の組織に複数の責任がある可能性が低いです。
組織内に重複がある場合でも、2つの責任は異なる意思決定プロセスを備えた異なる事業単位にあります。
私たちは責任を重複なく扱うことができます。したがって、脆弱性管理プロセスの「パッチサプライヤ」と「パッチ配置者」の責任ごとに2つの決定木を構築できます。

<details><summary>原文</summary><div>

We leave “coordinating patches” as future work.
Each of these trees will have different decision points that they take to arrive at a decision about a given unit of work.
The next two sections describe the decision space and the relevant decision points that we propose for these two responsibilities within the vulnerability management process.
The target audience for this paper is professional staff responsible for making decisions about information systems.
This audience encompasses a broad class of professionals, including suppliers, system maintainers, and administrators of many types.
It also includes other roles, such as risk managers, technical managers, and incident responders.
Although every layperson who owns a computing device makes decisions about managing it, they are not the target audience.
The following decision system may help such laypeople, but we do not intend it to be used by that audience.
While C-level executives and public policy professionals often make, shape, or incentivize decisions about managing information systems, they are not the target audience, either.
To the extent that decision trees for vulnerability management help higher level policy decisions, we believe the best way to help policy makers is by making technical decisions more transparent and explainable.
Policy makers may see indirect benefits, but they are not our primary audience and we are not designing an approach for them directly.
</div></details>

今後の作業として「パッチの調整」を残します。
これらの木のそれぞれは、与えられた作業単位についての決定に帰着するための異なる決定点を持つでしょう。
次の2つのセクションでは、脆弱性管理プロセス内でこれら2つの責任について提案する決定空間と関連する決定点について説明します。
この論文のターゲットオーディエンスは、情報システムに関する決定を下す責任を負うプロのスタッフです。
この聴衆は、サプライヤー、システムメンテナ、および多くの種類の管理者を含む幅広い専門家を網羅しています。
リスク管理者、技術マネージャ、およびインシデントレスポンダなど、他の役割も含まれています。
コンピューティングデバイスを所有するすべての素人はそれを管理することについて決定を下しますが、それらはターゲットオーディエンスではありません。
次の意思決定システムはそのような素人を助けるかもしれませんが、その聴衆によって使われることは意図しません。
Cレベルのエグゼクティブおよびパブリックポリシーの専門家は、情報システムの管理に関する決定、形状、またはインセンションを行っている間、それらはターゲットオーディエンスではありません。（※）
脆弱性管理の決定木がより高いレベルのポリシー決定に役立つ限り、ポリシー作成者を支援する最善の方法は、技術的な決定をより透明で説明しやすいものにすることであると信じています。
ポリシー作成者は間接的な利益を見るかもしれませんが、彼らは私たちの主要な聴衆ではなく、私たちは直接彼らのためのアプローチをデザインしていません。  

※Cレベル=経営幹部・上層部・役員かと

### Enumerating Decisions (決定の列挙)

<details><summary>原文</summary><div>

Stakeholders with different responsibilities in vulnerability management have very different decisions to make.
This section focuses on the differences among organizations based on their vulnerability management responsibilities.
Some decision makers may have different responsibilities in relation to different software.
For example, an Android app developer is a developer of the app, but is a deployer for any changes to the Android OS API.
This situation is true for libraries in general.
</div></details>

脆弱性管理における責任が異なるステークホルダーには、決定を下すのが非常に異なります。
このセクションでは、脆弱性管理責任に基づく組織間の違いに焦点を当てています。
いくつかの意思決定者は、さまざまなソフトウェアに関して異なる責任を負う可能性があります。
たとえば、Androidアプリ開発者はアプリ開発者ですが、Android OS APIへの変更のデプロイヤです。
この状況は、一般的なライブラリに当てはまります。

<details><summary>原文</summary><div>

A web browser developer makes decisions about applying patches to DNS lookup libraries and transport layer security (TLS) libraries.
A video game developer makes decisions about applying patches released to the Unreal Engine.
A medical device developer makes decisions about applying patches to the Linux kernel.
The list goes on. Alternatively, one might view applying patches as including some development and distribution of the updated product.
Or one might take the converse view, that development includes updating libraries.
</div></details>

Webブラウザ開発者は、DNSルックアップライブラリおよびトランスポート層セキュリティ（TLS）ライブラリへのパッチの適用に関する決定を下します。
ビデオゲーム開発者は、Unreal Engineにリリースされたパッチを適用することに関する決定を下します。
医療機器開発者は、Linuxカーネルへのパッチの適用に関する決定を下します。
リストは続きます。あるいは、パッチの適用を、更新された製品の開発と配布を含むものと見なす場合もあります。
あるいは逆の見方をすると、その開発にライブラリ更新することが含まれます。

<details><summary>原文</summary><div>

Either way, in each of these examples (mobile device apps, web browsers, video games, medical devices), we recommend that the professionals making genuine decisions do three things: (1) identify the decisions explicitly, (2) describe how they view their role(s), and (3) identify which software projects their decision relates to.
If their decisions are explicit, then the decision makers can use the recommendations from this document that are relevant to them.
</div></details>

いずれにも、これらの例のそれぞれ（モバイルデバイスアプリ、Webブラウザ、ビデオゲーム、医療機器）では、本物の決定を下す専門家が次の3つのことを行うことをお勧めします。（1）明示的な決定を特定する、（2）彼らが自分の役割をどのように捉えているかを説明する、および（3）どのソフトウェアプロジェクトが彼らの決定と関連するかをはっきりとさせる。
彼らの決定が明示的であれば、意思決定者は彼らに関連するこの文書の推奨事項を使うことができます。

### Enumerating Vulnerability Management Actions (脆弱性管理アクションの列挙)

<details><summary>原文</summary><div>

SSVC models the decision of “With what priority should the organization take action on a given vulnerability management work unit?” to be agnostic to whether or not a patch is available.
A unit of work means either remediating the vulnerability—such as applying a patch—or deploying a mitigation.
Both remediation and mitigations often address multiple identified vulnerabilities.
The unit of work may be different for different stakeholders.
The units of work can also change as the vulnerability response progresses through a stakeholder’s process.
We elucidate these ideas with the following examples.
</div></details>

SSVCモデル「組織は特定の脆弱性管理作業単位に対してどんな優先順位付けで行動を取るべきか」の決定を、パッチが利用可能かどうかに依存しなくなるようにモデル化します。※
作業単位は、パッチを適用するなど、脆弱性を修正すること、または軽減の展開を意味します。
修正と軽減の両方が多くの場合、個々の脆弱性に対処します。
仕事の単位はそれぞれ、利害関係者が異なる場合があります。
脆弱性の対応がステークホルダーのプロセスを経て進行するにつれて、作業単位も変更できます。
以下の実施例でこれらのアイデアを解明しました。  

※agnosticを依存しなくなると訳しました：[wikipedia](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%B0%E3%83%8E%E3%82%B9%E3%83%86%E3%82%A3%E3%83%83%E3%82%AF_(%E6%83%85%E5%A0%B1%E5%B7%A5%E5%AD%A6))

#### Supplier Units of Work (サプライヤーワーク単位)

<details><summary>原文</summary><div>

On the input side of the Supplier process, Suppliers typically receive reports of vulnerabilities in one or more versions of their product.
Part of the Supplier’s task on initial report intake is to resolve the initial report into a set of products and versions that are affected by the reported vulnerability.
Our working assumption is that for SSVC purposes, the supplier’s unit of work is the combination of the vulnerability with each affected product.
</div></details>

サプライヤプロセスの入力側では、サプライヤは通常、自分の製品の1つ以上のバージョンで脆弱性のレポートを受け取ります。
サプライヤの初期レポートでのタスクの一部は、初回レポートを報告された脆弱性の影響を受ける一連の製品とバージョンに解決することです。
私たちの作業上の前提は、SSVCの目的では、サプライヤの作業単位は、影響を受ける各製品との脆弱性の組み合わせであるということです。

<details><summary>原文</summary><div>

This implies the need for Suppliers to be able to resolve whatever they receive to that level of granularity in order to make best use of SSVC.
Products will often need to be addressed individually because they may have diverse development processes or usage scenarios.
There are a variety of ways a Supplier might need to resolve the set of affected products.
</div></details>

これは、SSVCを最大限活用するために、サプライヤが受け取るその粒度のレベルに解決することの必要性を表しています。
製品は多様な開発プロセスや使用シナリオがある可能性があるため、製品を個別に対処する必要があります。
サプライヤが影響を受ける製品のセットを解決するために必要となる可能性のあるさまざまな方法があります。

<details><summary>原文</summary><div>

For example, they might
- recognize, on further investigation of the initial report, that additional versions of the product are affected
- discover that other products are affected due to code sharing or programmer error consistent across products
- receive reports of vulnerabilities in third party libraries they utilize in one or more of their products
- receive fix bundles for third party libraries used in one or more of their products (where a fix bundle might resolve multiple vulnerabilities or add new features)
</div></details>

たとえば彼らは、
 - 初期レポートのさらなる調査で、製品の追加バージョンが影響を受けることを認識しています
 - コードの共有もしくは製品を通じた一貫性のあるプログラマのエラーによって他の製品も影響を受けていることを発見します
 - 自分の製品の1つ以上を利用しているサードパーティのライブラリの脆弱性の報告を受け取ります
 -  1つ以上の製品で使用されているサードパーティのライブラリの修正バンドルを受け取ります（フィックスバンドルが複数の脆弱性を解決するか、新しい機能を追加する可能性がある場合）。

<details><summary>原文</summary><div>

Without belaboring the point, the above methods are similar to how CVE Numbering Authorities discern “independently fixable vulnerabilities” (CVE Board 2020).
We also note that SBOM(Jump and Manion 2019) seems well-placed to aid in that resolution process for the third-party library scenarios.
In the end, Suppliers provide remediations and/or mitigations for affected products.
A supplier-provided remediation is usually a software update which contains fixes for multiple vulnerabilities and, often, new or improved features.
Supplier output is relevant because it will become input to Deployers. SSVC focuses only on the remediation in this case; a set of remediations for multiple vulnerabilities is a fix bundle.
Suppliers may also produce mitigations, such as recommended configuration changes, to limit the impact of a vulnerability.
</div></details>

<details><summary>原文</summary><div>

論点を細かく議論しなければ、上記の方法はCNAが「個別に修正可能な脆弱性」（CVE Board 2020）を見分けている方法と似ています。
また、SBOM（Jump and Manion 2019）は、サードパーティ製ライブラリのシナリオ解決プロセスを支援するために適切に配置されているようです。
最後に、サプライヤーは影響を受ける製品のために修復および/または緩和を提供します。
サプライヤ提供の修復は通常、複数の脆弱性および、多くの場合、新機能または改善された機能の修正を含むソフトウェアアップデートです。
デプロイヤへの入力となるため、サプライヤの出力は関連性があります。
SSVCはこの場合の修復にのみ焦点を当てています。複数の脆弱性に対する一連の修正は修正バンドルです。
サプライヤはまた、脆弱性の影響を抑えるための緩和（例えば推奨設定の変更等）を提供することもあるでしょう。
</div></details>

#### Deployer Units of Work (デプロイヤー作業単位)

<details><summary>原文</summary><div>

Deployers are usually in the position of receiving remediations or mitigations from their Suppliers for products they have deployed.
They must then decide whether to deploy the remediation or mitigation to a particular instance (or not).
Whether they have the option of deploying only part of a remediation such as a fix bundle depends on whether the Supplier has engineered their release process to permit that degree of flexibility.
For example, if service packs are fix bundles, the Supplier might choose to release individually deployable fixes as well.
</div></details>

デプロイヤは通常、開発した製品に、サプライヤからの修復または緩和を受け取るするポジションにいます。
その後、修復または緩和を特定のインスタンスに展開するか（またはそうしない）かを決定する必要があります。
修正バンドルなどの修復の一部のみを展開するオプションがあるかどうかは、サプライヤがその柔軟性のある程度を許可するために自分のリリースプロセスを設計したかどうかによって異なります。
たとえば、Service PackがFix Bundlesの場合、サプライヤは個別に展開可能な修正を解除することを選択できます。

<details><summary>原文</summary><div>

The vulnerability management process for deployers has at its core the collation of data including
- an inventory of deployed instances of product versionsWe invite further refinement
- a mapping of vulnerabilities to remediations or mitigations
- a mapping of remediations and/or mitigations to product versions
</div></details>

デプロイヤの脆弱性管理プロセスは、その中核に次のデータを含みます。
- 製品バージョンの展開インスタンスの作成（さらなる洗練を招待します）※
- 複数の脆弱性に対する修復及び緩和のマッピング
- それぞれの製品バージョンへの修復かつ/または緩和のマッピング

※原文が若干崩れていて、意図も汲めなかったので（）にそのまま書いてます

<details><summary>原文</summary><div>

The first must be collected by the Deployer, while the latter two most often originate from the product Supplier.
Managing this information is generally called asset management.
The relationship between SSVC and asset management is discussed further in Relationship to asset management.
In turn, Deployers must resolve this information into specific actions in which a remediation or mitigation is slated for deployment to replace or modify a particular instance of the product.
The Deployer tree in SSVC considers the mission and safety risks inherent to the category of systems to which those deployed instances belong.
For this reason, we recommend that the pairing of remediation or mitigation to a product version instance constitutes the unit of work most appropriate for the SSVC.
</div></details>

最初のものはデプロイヤが収集しなければなりませんが、後者の2つはよく主に製品のサプライヤから由来するものになります。
この情報を管理することは、一般的に資産管理と呼ばれます。
SSVCと資産管理の関係は、[Relationship to asset management]()でさらに説明されています。
次に、デプロイヤは、この情報を特定のアクションに解決する必要があります。このアクションでは、製品の特定のインスタンスを置換または変更するために、修復または緩和のデプロイが予定されています。
SSVCのデプロイヤの木は、これらのデプロイされたインスタンスが属するシステムのカテゴリから引き継ぐミッションおよび安全上のリスクを考慮します。※
このため、製品バージョンインスタンスへの修復または緩和の組み合わせは、SSVCに最も適した作業単位で構成することをお勧めします。  

※SSVCで同じように分類されるシステムではミッション/ リスクも同様になる　といった意味合いかと

#### Coordinator Units of Work (コーディネーター作業単位)

<details><summary>原文</summary><div>

Coordinator units of work tend to coincide with whatever arrives in a single report, which spans the range from a single vulnerability affecting a specific version of an individual product from one Supplier all the way to fundamental design flaws in system specifications that could affect every Supplier and product that uses or implements the flawed specification.
Coordinators may need to reorganize reports (e.g., merge, split, expand, or contract) according to their workflow demands.
SSVC can be applied to either the initial report or to the results of such refinement.
</div></details>

コーディネーターの作業単位は、1つのレポートに含まれるものと一致する傾向があります。
そのレポートは、1人のサプライヤの個別の製品のバージョンに影響を与える1脆弱性から、
全てのサプライヤに影響を与え得るシステム仕様上の基礎的な設計ミス、そして欠陥のある仕様を使用または実装している製品にまで
はるばると及びます。
コーディネーターは、その業務フローの要求に従って、レポートを再編成（例えば、マージ、分割、拡張、または契約）する必要があるかもしれません。
SSVCは、初回のレポートまたはその再編成の結果に適用できます。

#### Aggregation of SSVC across units of work (仕事単位を越えたSSVCの集計)

<details><summary>原文</summary><div>

SSVC users should answer the suggested questions for whatever discrete unit of work they are considering.
There is not necessarily a reliable function to aggregate a recommendation about remediation out of its constituent vulnerabilities.
For the sake of simplicity of examples, we treat the remediation as a patch of one vulnerability, and comment on any difficulty in generalizing our advice to a more complex patch where appropriate.
To further clarify terms, “Remediation occurs when the vulnerability is eliminated or removed.
Mitigation occurs when the impact of the vulnerability is decreased without reducing or eliminating the vulnerability” (Office of the DoD Chief Information Officer 2020, sec. 3.5).
Examples of remediation include applying patches, fixes and upgrades; or removing the vulnerable software or system from operation.
Mitigating actions may include software configuration changes, adding firewall ACLs, or otherwise limiting the system’s exposure to reduce the risk of the impact of the vulnerability; or accepting the risk.
</div></details>

SSVCユーザーは、彼らが検討しているあらゆる離散的な作業単位について提案された質問に答えるべきです。
構成要素の脆弱性から修復に関する推奨を集約するための信頼できる機能は必ずしもありません。
例を簡単にするために、修復を1つの脆弱性のパッチとして扱い、必要に応じて、アドバイスをより複雑なパッチに一般化することの難しさについてコメントします。
用語をさらに明確にするために：「脆弱性が排除または削除されたときに修復が発生します。
緩和は、脆弱性を少なくしたり排除したりすることなく脆弱性の影響が減少したときに発生します (Office of the DoD Chief Information Officer 2020, sec. 3.5)。」
修復の例には、パッチ、修正およびアップグレードの適用が含まれます。または運用から脆弱なソフトウェアまたはシステムを排除することを含みます。
緩和のアクションには、この脆弱性の影響のリスクを軽減するためにソフトウェア構成の変更したり、ファイアウォールACLの追加したり、またはその他の方法でシステムの公開範囲を制限したりすることを含みます。または、またはリスクを受け入れることも含みます。

#### Supplying Patches (パッチの供給)

<details><summary>原文</summary><div>

At a basic level, the decision at a software development organization is whether to issue a work order and what resources to expend to remediate a vulnerability in the organization’s software.
Prioritization is required because, at least in the current history of software engineering, the effort to patch all known vulnerabilities will exceed available resources.
The organization considers several other factors to build the patch; refactoring a large portion of the code base may be necessary for some patches, while others require relatively small changes.
We focus only on the priority of building the patch, and we consider four categories of priority, as outlined in Table 2.
</div></details>

基本的なレベルでは、ソフトウェア開発機関の決定とは、作業指示を発行するかどうか、および組織のソフトウェアの脆弱性を修復するためにどのリソースを支払うかのかどうかです。
優先順位付けは必要です。なぜなら、少なくとも現在のソフトウェア工学の歴史において、すべての既知の脆弱性をパッチするための労力は利用可能なリソースを超えるためです。
組織はパッチを構築するために他のいくつかの要因を考慮します。コードベースの大部分をリファクタリングする必要があるものもあれば、他のパッチは比較的小さな変更が必要とされるものもあります。
私たちはパッチ構築の優先順位にのみ焦点をあてて、 表2に概説したように、4つのカテゴリの優先順位を考慮しています。

<details><summary>原文</summary><div>

Table 2: Proposed Meaning for Supplier Priority Outcomes

| Supplier Priority | Description |
| --- | --- |
| Defer | Do not work on the patch at present. |
| Scheduled | Develop a fix within regularly scheduled maintenance using supplier resources as normal. |
| Out-of-Cycle | Develop mitigation or remediation out-of-cycle, taking resources away from other projects and releasing the fix as a security patch when it is ready. |
| Immediate | Develop and release a fix as quickly as possible, drawing on all available resources, potentially including drawing on or coordinating resources from other parts of the organization. |
</div></details>

表2: 提案しているサプライヤ優先順位出力の意味

| サプライヤ優先順位 | 説明 |
| --- | --- |
| Defer | 現在パッチ作業をしない |
| Scheduled | 通常のサプライヤのリソースを利用し、定期メンテナンスで改修する |
| Out-of-Cycle | 他プロジェクトからもリソースを割き、準備ができ次第セキュリティパッチとして修正をリリースして、緩和もしくは修復を例外的なサイクルで開発する |
| Immediate | 可能な限り迅速に修正プログラムを開発してリリースし、利用可能なすべてのリソースを利用します。これには、組織の他の部分からのリソースの利用や調整も含まれる可能性があります。 |

※Defer, Scheduled, Out-of-Cycle, Immedeiateは出力の区分なので、無理に訳す必要ないと判断して訳していません。

#### Deploying Patches (パッチの展開)

<details><summary>原文</summary><div>

A mitigation that successfully changes the value of a decision point may shift the priority of further action to a reduced state.
An effective firewall or IDS rule coupled with an adequate change control process for rules may be enough to reduce the priority where no further action is necessary.
In the area of Financial impacts, a better insurance policy may be purchased, providing necessary fraud insurance. Physicial well-being impact may be reduced by testing the physicial barriers designed to restrict a robot’s ability to interact with humans.
Mission impact could be reduced by correcting the problems identified in a disaster recover test-run of the alternate business flow.
</div></details>

決定点の値をうまく変更する緩和は、さらなる行動の優先順位を縮小状態にシフトするかもしれない。
規則のための適切な変更制御プロセスと組み合わされた効果的なファイアウォールまたはIDS規則は、それ以上にアクションが必要ないような、優先順位を減らすのに十分なものであるだろう。
Financialの影響の分野では、避けがたい詐欺保険を提供されても、よりよい保険契約が購入されるでしょう。
人間と交流する能力を持ったロボットを制限するために設計された物理的な障壁をテストすることでPhysicalの幸福への影響は減るでしょう。
代替ビジネスフローの災害回復試験実行で識別された問題を修正することによってMissionの影響を減らすことができます。

※ここ適切な訳がわからなかったです

<details><summary>原文</summary><div>

If applying a mitigation reduces the priority to defer, the deployer may not need to apply a remediation if it later becomes available.
Table 3 displays the action priorities for the deployer, which are similar to the supplier case.
When remediation is available, usually the action is to apply it.
When remediation is not yet available, the action space is more diverse, but it should involve mitigating the vulnerability (e.g., shutting down services or applying additional security controls) or accepting the risk of not mitigating the vulnerability.
Applying mitigations may change the value of decision points. For example, effective firewall and IDS rules may change System Exposure from open to controlled.
</div></details>

緩和の適用により優先順位をdeferに下げた場合、デプロイヤは後で利用可能になった場合に修復を適用する必要がないかもしれません。
表3は、サプライヤの場合と同様のデプロイヤのアクション優先順位を示しています。
修復が可能な場合は、通常その適用がアクションとなります。
修復がまだ利用できない場合、アクションの範囲はより多様になりますが、そのアクションとはこの脆弱性を緩和（例えば、サービスのシャットダウンまたは追加のセキュリティコントロールの適用）するものであるか、またはこの脆弱性を緩和しないリスクを受け入れるものになります。
緩和の適用は、決定点の価値を変えるかもしれません。例えば、効果的なファイアウォールおよびIDS規則は、システム露出をオープンから規制状態に変更することができる。

<details><summary>原文</summary><div>

Financial well-being, a Saftey Impact category, might be reduced with adequate fraud detection and insurance.
Physical well-being, also a Saftey Impact category, might be reduced by physical barriers that restrict a robot’s ability to interact with humans.
Mission Impact might be reduced by introducing back-up business flows that do not use the vulnerable component.
In a later section we combine Mission and Situated Safety Impact to reduce the complexity of the tree.
However, these mitigation techniques will not always work.
For example, the implementation of a firewall or IDS rule to mitigate System Exposure from open to controlled is only valid until someone changes the rule.
</div></details>

Financial well-being、Safety Impactの影響カテゴリは、適切な不正検出と保険で減少する可能性があります。
Physical well-being、これもSaftey Impactの影響カテゴリですが、ロボットの人間と対話する能力を制限する物理的な障壁によって減らすかもしれません。
脆弱なコンポーネントを使用しないバックアップビジネスフローを導入することで、Mission Imapctを減らすことができます。
後のセクションでは、Mssion ImpactとSituated Safety Impactを組み合わせて、木の複雑さを軽減します。
しかし、これらの緩和技術は常に機能しないでしょう。
たとえば、System Exposureをオープンからコントロールに軽減するためのファイアウォールまたはIDSルールの実装は、誰かがルールを変更するまで有効です。

<details><summary>原文</summary><div>

In the area of Financial impacts, the caps on the insurance may be too low to act as a mitigation.
The Physical impact may be increased by incorrect installation of the physical barriers designed to restrict a robot’s ability to interact with humans.
The Mission Impact could be increased when a disaster recovery test-run identifies problems with an alternate business flow.
The mitigating action may not be permanent or work as designed.
A mitigation that successfully changes the value of a decision point may shift the priority of further action to a reduced state.
</div></details>

Fincancial impactsの分野では、保険の頂点は緩和として機能するには低すぎる可能性があります。
Physical impactは、ロボットの人間と対話する能力を制限するように設計された物理的な障壁の誤った設置によって増加するかもしれません。
災害復旧試験実行が代替ビジネスフローに関する問題を特定すると、Mission Impactを増やす可能性があります。
緩和作用は、設計されているように恒久的または作業ではない可能性があります。
決定点の値をうまく変更する緩和は、さらなる行動の優先順位を縮小状態にシフトするかもしれない。

<details><summary>原文</summary><div>

If applying a mitigation reduces the priority to defer, the deployer may not need to apply a remediation, if later, it becomes available. Table 3 displays the action priorities for the deployer, which are similar to the supplier case.
In a later section, the different types of impacts are defined and then implemented in the decision trees as examples of how the various impacts affect the priority.
For now, assume the decision points are ordered as: Exploitation; Exposure; Utility; and Well-being and Mission Impact.
In this order, an active state of Exploitation will never result in a defer priority.
</div></details>

緩和を適用して優先順位をdeferに下げた場合、デプロイヤは修復を適用する必要がない場合がありますが、後に利用可能になります。表3は、サプライヤの場合と同様のデプロイヤのアクション優先順位を示しています。
後のセクションでは、さまざまな影響が優先順位に影響を与える方法の例として、さまざまな種類の影響が定義され、そして決定木に実装されます。
今のところ、決定点は次のように要求されていると仮定します。Exploitation, Exposure, Utility, Well-being, Mission Impact.
この順序では、活動的な利用状況は遅延優先順位を引き起こすことはありません。

<details><summary>原文</summary><div>

A none state of Exploitation (no evidence of exploitation) will result in either defer or scheduled priority—unless the state of Well-being and Mission Impact is very high, resulting in an out-of-cycle priority.
As opposed to mitigation, applying a remediation finishes an SSVC analysis of a deployed system.
While specific vulnerabilities in specific systems can be remediated, the vulnerability cannot be ’disposed of’ or eliminated from future consideration within an IT environment.
Since software and systems are dynamic, a single vulnerability can be re-introduced after initial remediation through updates, software rollbacks, or other systemic actions that change the operating conditions within an environment.
It is therefore important to continually monitor remediated environments for vulnerabilities reintroduced by either rollbacks or new deployments of outdated software.
</div></details>

Exploitationがnoneの状態（攻撃手段の証拠がない）は、Well-beingとMission Impactの状態が非常に高くない限り、deferまたはscheduledの優先順位いずれかになり、その結果、out-of-cycleの優先順位があります。
緩和とは対照的に、修復を適用すると、デプロイしたシステムのSSVC分析は終了します。
特定のシステムにおける特定の脆弱性を修復ることはできるが一方で、その脆弱性はIT環境内で将来の考慮から排除も廃棄もできません。
ソフトウェアとシステムは動的であるため、アップデート、ソフトウェアロールバック、または環境内の動作条件を変更する他のシステム的なアクションを通じて、初回の修復適用後に脆弱性を再導入できてしまいます。
したがって、最新のソフトウェアのロールバックまたは新しい展開によって再導入された脆弱性についての修復環境を継続的に監視することが重要です。

<details><summary>原文</summary><div>

Table 3: Proposed Meaning for Deployer Priority Outcomes

| Deployer Priority | Description |
| --- | --- |
| Defer | Do not act at present. |
| Scheduled | Act during regularly scheduled maintenance time. |
| Out-of-cycle | Act more quickly than usual to apply the mitigation or remediation out-of-cycle, during the next available opportunity, working overtime if necessary. |
| Immediate | Act immediately; focus all resources on applying the fix as quickly as possible, including, if necessary, pausing regular organization operations. |
</div></details>

表3：デプロイヤ優先成果のための提案された意味

| Deployer Priority | Description |
| --- | --- |
| Defer | 現在は対応しない。 |
| Scheduled | 定期メンテナンス中に対応する。 |
| Out-of-cycle | サイクル外（次の可能な機会もしくは必要であれば作業時間外）で、通常より早く緩和または修復の対応をする。 |
| Immediate | 即時対応する。必要であれば定期的な組織の運用を停止してでも可能な限り素早く、全てのリソースを修正に集中させる。 |
#### Coordinating Patches (パッチの調整)

<details><summary>原文</summary><div>

In coordinated vulnerability disclosure (CVD), there are two available decisions modelled in version 2 of SSVC.
The first decision is whether or not to coordinate a vulnerability report.
This decision is also known as triage.
Vulnerability Response Decision Assistance (VRDA) provides a starting point for a decision tree for this situation.
</div></details>

脆弱性情報調整（CVD）では、SSVCのバージョン2でモデル化された2つの利用可能な決定があります。
最初の決定は、脆弱性報告書を調整するかどうかです。
この決定はトリアージとしても知られています。
脆弱性対応意思決定支援（VRDA）は、この状況のための決定木の出発点を提供します。

<details><summary>原文</summary><div>

VRDA is likely adequate for national-level CSIRTs that do general CVD, but other CSIRT types may have different needs.
The CERT Guide to Coordinated Vulnerability Disclosure provides something similar for those who are deciding how to report and disclose vulnerabilities they have discovered (Householder, Wassermann, et al. 2020, sec. 6.10). The second decision is whether to publish information about a vulnerability.
We omit a table for this decision because the options are do not publish or publish.
</div></details>

VRDAは一般的なCVDを行う全国レベルのCSIRTに適していますが、他のCSIRTタイプには異なるニーズがある場合があります。
協調した脆弱性の開示の証明書ガイドは、発見した脆弱性を報告および開示する方法を決定している人に似たものを提供します（HouseHolder、Wassermann、et al.2020、Sec.6.10）。2番目の決定は、脆弱性に関する情報を公開するかどうかです。
オプションが公開または公開されていないため、この決定のためのテーブルを省略します。

<details><summary>原文</summary><div>

Table 4: Proposed Coordinator Triage Priority Outcomes

| Triage | Priority Description |
| --- | --- |
| Decline | Do not act on the report. |
| Track | Receive information about the vulnerability and monitor for status changes but do not take any overt actions. |
| Coordinate | Take action on the report. “Action” may include any one or more of: technical analysis, reproduction, notifying vendors, publication, and assist another party. |
</div></details>

表4：提案されたコーディネータのトリアージ優先的な結果

| Triage | Priority Description |
| --- | --- |
| Decline | レポートに対してアクションを取らない。 |
| Track | 脆弱性情報を受け取りステータス変化を監視するが、具体的なアクションはとらない。 |
| Coordinate | レポートのアクションを実行する。そのアクションには、技術的な分析、再現、ベンダーへの通知、公開、他パーティへの支援が含まれだろう。 |

### Items With the Same Priority (同じ優先順位の項目)

<details><summary>原文</summary><div>

Within each setting, the decisions are a kind of equivalence class for priority.
That is, if an organization must deploy patches for three vulnerabilities, and if these vulnerabilities are all assigned the scheduled priority, then the organization can decide which to deploy first.
The priority is equivalent. This approach may feel uncomfortable since CVSS gives the appearance of a finer grained priority.
CVSS appears to say, “Not just 4.0 to 6.9 is ‘medium’ severity, but 4.6 is more severe than 4.5.”
However, as discussed previously (see page 4), CVSS is designed to be accurate only within +/- 0.5, and, in practice, is scored with errors of around +/- 1.5 to 2.5 (Allodi et al. 2018, see Figure 1).
</div></details>

各設定内で、決定は優先順位のための一種の等価クラスです。
つまり、組織が3つの脆弱性に対してパッチを展開する必要がある場合、およびこれらの脆弱性がすべてscheduledな優先順位に割り当てられている場合、組織は最初にどれをデプロイするか決定できます。
優先順位は同等です。このアプローチは、CVSSがより細かい粒状優先順位の外観を与えるので、不快に感じるかもしれません。
CVSSは「わずか4.0から6.9は深刻さは中ですが、4.6は4.5より深刻です。」と表現しています。
しかしながら、前述したように（4ページ参照）、CVSSは±0.5以内にのみ正確になるように設計されており、実際には±1.5から2.5の誤差で評価している（Allodi et al.2018, see Figure 1）。

<details><summary>原文</summary><div>

An error of this magnitude is enough to make all of the “normal” range from 4.0 to 6.9 equivalent, because 5.5 +/- 1.5 is the range 4.0 to 7.0. Our proposal is an improvement over this approach.
CVSS errors often cross decision boundaries; in other words, the error range often includes the transition between “high” and “critical” or “medium.”
Since our approach keeps the decisions qualitatively defined, this fuzziness does not affect the results.
Returning to the example of an organization with three vulnerabilities to remediate that were assigned scheduled priority, in SSVC, they can be patched in any order.
</div></details>

5.5±1.5の範囲とは4.0~7.0であるため、この大きさの誤差は4.0から6.9のすべての範囲のすべての「通常」の範囲を考慮するのに十分です。私たちの提案はこのアプローチの改善です。
CVSS誤差はしばしば決定境界を超えています。言い換えれば、誤差範囲はしばしば「高」と「クリティカル」または「中」との間が誤差の範囲に含まれます。
私たちのアプローチは意思決定を定性的な定義に留めているので、この曖昧さは結果に影響を与えません。
3つの脆弱性に修復をしたいがscheduledの優先順位が割り当てられていた先の組織の例に戻ると、SSVCでは、パッチを任意の順に充てることができる。

<details><summary>原文</summary><div>

This is an improvement over CVSS, since based on the scoring errors, CVSS was essentially just giving random fine-grained priorities within qualitative categories anyway.
With our system, organizations can be more deliberate about conveniently organizing work that is of equivalent priority.
</div></details>

誤差の評価という観点で、CVSSは基本的に定性的なカテゴリの中でランダムで微細な優先順位を与えるだけなので、SVCCはCVSSの改善です。
私たちのシステムでは、組織は同等の優先順位の仕事を便利に整理することについて、より慎重になることがあります。 ※  
※CVSSは数値で出力されるのでカテゴリ（severity）内でも比較できる一方、SVCCは定性出力のみなので同じ優先順位のものに対してどうするかは対応者側で考える必要があるということかと。

### Risk Tolerance and Response Priority (リスク許容誤差と応答の優先事項)

<details><summary>原文</summary><div>

SSVC enables stakeholders to balance and manage their risks themselves.
We follow the risk management vocabulary from (ISO 2009) and define risk as “effect of uncertainty on objectives;” see (ISO 2009) for notes on the terms in the definition.
A successful vulnerability management practice must balance at least two risks:
</div></details>

SSVCは、利害関係者が彼らのリスク自体のバランスをとり管理することを可能にします。
(ISO 2009) からのリスク管理語彙に従い、「目的に対する不確実性の影響」としてリスクを定義します。定義内の用語に関する注意事項については、（ISO 2009）を参照してください。
成功する脆弱性管理の運用は、少なくとも2つのリスクとのバランスをとる必要があります。

<details><summary>原文</summary><div>

1. Change risk: the potential costs of deploying remediation, which include testing and deployment in addition to any problems that could arise from making changes to production systems.
2. Vulnerability risk: the potential costs of incidents resulting from exploitation of vulnerable systems
</div></details>

1. リスクの変化：生産システムへの変更を加えることから生じる可能性のある問題に加え、テストとデプロイを含む修復をデプロイする潜在的コスト。
2. 脆弱性リスク：脆弱なシステムへの攻撃から生じるインシデントの潜在的なコスト。


<details><summary>原文</summary><div>

To place these risks in context, we follow the SEI’s Taxonomy of Operational Cyber Security Risks (Cebula and Young 2010).
Change risk can be characterized as a combination of Class 2 and/or Class 3 risks.
Class 2: Systems and Technology Failures includes hardware, software, and systems risks.
Class 3: Failed Internal Processes can arise from process design, process execution, process controls, or supporting processes. Meanwhile, vulnerability risk falls into Subclass 1.2: Actions of People: Deliberate.
</div></details>

これらのリスクを状況に応じて配置するために、私たちは、SEIの運用サイバーセキュリティリスク（Cebula and Young 2010）の分類法に従います。
変更リスクは、クラス2および/またはクラス3リスクの組み合わせとして特徴付けることができます。
クラス2：システムとテクノロジの失敗には、ハードウェア、ソフトウェア、およびシステムのリスクが含まれます。
クラス3：失敗した内部プロセスは、プロセス設計、プロセス実行、プロセス制御、またはサポートプロセスから発生する可能性があります。一方、脆弱性リスクはサブクラス1.2に落ちる：人々の行動：審議。

<details><summary>原文</summary><div>

In developing the decision trees in this document, we had in mind stakeholders with a moderate tolerance for risk.
The resulting trees reflect that assumption.
Organizations may of course be more or less conservative in their own vulnerability management practices, and we cannot presume to determine how an organization should balance their risk.
We therefore remind our readers that the labels on the trees (defer, immediate, etc.) can and should be customized to suit the needs of individual stakeholders wherever necessary and appropriate.
For example, an organization with a high aversion to change risk might choose to accept more vulnerability risk by lowering the overall response labels for many branches in the trees, resulting in fewer vulnerabilities attaining the most urgent response.
On the other hand, an organization with a high aversion to vulnerability risk could elevate the priority of many branches to ensure fixes are deployed quickly.
</div></details>

この文書の決定木を育成する際には、リスクのための適度な許容誤差を持つステークホルダーを念頭に置いていました。
結果の木はその仮定を反映しています。
組織はもちろん、彼ら自身の脆弱性管理の慣行においてもっと多かれ少なかれ保守的であり得、そして私達は組織がリスクのバランスをとるべきかを決定することを推定することはできません。
したがって、我々は、木のラベル（defer, immediate, ...）は、必要性があり適用可能なものはどれでも、個々の利害関係者の需要に合うようにカスタマイズ可能でありすべきであることを読者に思い出させる。
たとえば、リスクの変更を嫌う組織は、ツリー内の多くのブランチの全体的な応答ラベルを下げることで、より多くの脆弱性リスクを受け入れることを選択し、最も緊急な応答を達成している脆弱性を減らすことができます。※
一方、脆弱性リスクへの高い嫌悪感を持つ組織は、修正が迅速に展開されるように、多くの分岐の優先順位を高める可能性があります。  
※ここでいう応答とは、defer, immediate, ...等の決定木の応答を表しています。


### Scope (範囲)

<details><summary>原文</summary><div>

Scope is an important variable in the answers of these decision points.
It has at least three aspects.
The first is how the boundaries of the affected system are set.
The second is whose security policy is relevant.
The third is how far forward in time or causal steps one reasons about effects and harms.
</div></details>

スコープは、これらの決定点の答えに重要な変数です。
それは少なくとも3つの側面を持っています。
1つ目は、影響を受けるシステムの境界がどのように設定されているかです。
2つ目はセキュリティポリシーが関連していることです。
3つ目は、影響と被害についての1つの理由として、時間または因果関係のステップがどれだけ進んでいるかです。

<details><summary>原文</summary><div>

We put forward recommendations for each of these aspects of scope.
However, users of the decision process may want to define different scopes.
Users may define a different scope as long as the scope (1) is consistent across decisions, and (2) is credible, explicit, and accessible to all relevant decision makers.
For example, suppliers often decline to support products beyond a declared end-of-life (EOL) date.
</div></details>

スコープのこれらの側面のそれぞれについての推奨事項を提案します。
ただし、決定プロセスのユーザーは、異なるスコープを定義したい場合があります。
ユーザーは、スコープが（1）意思決定全体で一貫しており、（2）信頼性が高く、明示的で、関連するすべての意思決定者がアクセスできる限り、異なるスコープを定義できます。
たとえば、サプライヤはしばしば宣言されたライフサイクル終了（EOL）日を超えて製品をサポートするために却下します。

<details><summary>原文</summary><div>

In these cases, a supplier could reasonably consider vulnerabilities in those products to be out of scope.
However, a deployer may still have active instances of EOL products in their infrastructure.
It remains appropriate for a deployer to use SSVC to prioritize their response to such situations, since even if there is no remediation forthcoming from the supplier it may be possible for the deployer to mitigate or remediate the vulnerability in other ways, up to and including decommissioning the affected system(s).
</div></details>

このような場合、サプライヤは、それらの製品の脆弱性を範囲外にすると合理的に検討することができます。
ただし、デプロイヤは、製品基盤にEOL製品のアクティブなインスタンスを持っている可能性があります。
デプロイヤがSSVCを使用して、このような状況への対応を優先順位を付けることは適切であると再起されます。
サプライヤからの修正がない場合でも、影響を受けるシステムの廃止まで含む他の方法で、デプロイヤが脆弱性を軽減または修正できる可能性があるからです。

#### Boundaries of the Affected System (影響を受けるシステムの境界)

<details><summary>原文</summary><div>

One distinction is whether the system of interest is software per se or a cyber-physical system. A problem is that in every practical case, both are involved.
Software is what has vulnerabilities and is what vulnerability management is focused on remediating. Multiple pieces of software run on any given computer system.
To consider software vulnerabilities in a useful scope, we follow prior work and propose that a vulnerability affects “the set of software instructions that executes in an environment with a coherent function and set of permissions” (Spring, Kern, and Summers 2015).
This definition is useful because it lets us keep to common usage and intuition and call the Linux kernel—at least a specific version of it—“one piece” of software.
</div></details>

1つの違いは、対象のシステムがソフトウェア自体であるか、サイバーフィジカルシステムであるかです。問題は、すべての実際のケースで、両方が関係しているということです。
ソフトウェアは脆弱性を持つものであり、脆弱性管理は修復に焦点を当てられています。任意の特定のコンピュータシステム上で複数のソフトウェアが実行されます。
ソフトウェアの脆弱性を有用な範囲で検討するために、私たちは以前の仕事に従い、脆弱性が「コヒーレント関数と許可のセットを持つ環境で実行するソフトウェア命令のセット」（Spring, Kern, and Summers 2015）に影響を与えることを提案します。
この定義は、一般的な使用と直感のまま、Linuxカーネルを少なくともソフトウエアの特定のバージョンで呼び出すことができるので便利です。

<details><summary>原文</summary><div>

But decision points about safety and mission impact are not about the software in isolation; they are about the entire cyber-physical system, of which the software is a part.
The term “physical” in “cyber-physical system” should be interpreted broadly; selling stocks or manipulating press outlet content are both best understood as affecting human social institutions.
These social institutions do not have much of a corporeal instantiation, but they are physical in the sense that they are not merely software, and so are parts of cyber-physical systems.
</div></details>

しかし、安全性とミッションの影響に関する決定点は、孤立しているソフトウェアについてではありません。それらはサイバー物理システム全体についてであり、そのうちソフトウェアは一部です。
「サイバー物理システム」の「物理」という用語は広く解釈されるべきです。在庫品やプレスコンセントのコンテンツの販売は、人間の社会的機関に影響を与えると理解されています。
これらの社会的機関は、体外のインスタンスの多くはありませんが、それらは単にソフトウェアではないという意味では物理的なもので、サイバー物理システムの一部です。

<details><summary>原文</summary><div>

The hard part of delineating the boundaries of the affected system is specifying what it means for one system to be part of another system.
Just because a computer is bolted to a wall does not mean the computer is part of the wall’s purpose, which is separating physical space.
At the same time, an off-premises DNS server may be part of the site security assurance system if the on-premises security cameras rely on the DNS server to connect to the displays at the guard’s desk.
We define computer software as part of a cyber-physical system if the two systems are mutually manipulable; that is, changes in the part (the software) will (at least, often) make detectable and relevant changes to the whole (the cyber-physical system), and changes in the whole will (often) make relevant and detectable changes in the part (Spring and Illari 2018).
</div></details>

影響を受けるシステムの境界を描写する難しい部分は、1つのシステムが別のシステムの一部になることを意味するということを指していますしています。
コンピューターが壁にボルトで固定されているからといって、コンピューターが壁の目的の一部であり、物理的な空間を分離しているわけではありません。
同様に、オンプレミスの防犯カメラが警備員のデスクのディスプレイに接続するためにDNSサーバーに依存している場合、オフプレミスのDNSサーバーがサイトのセキュリティ保証システムの一部になる可能性があります。
2つのシステムが相互に操作可能である場合は、コンピュータソフトウェアをサイバー物理システムの一部として定義します。すなわち、部品（ソフトウェア）の変化は（少なくとも、しばしば）検出可能で関連性のある変更を行い、全体の変化（しばしば）が関連して検出可能な変更を加えることになる。パート（春とIllari 2018）。
2つのシステムが相互に操作可能である場合、コンピューターソフトウェアをサイバーフィジカルシステムの一部として定義します。 つまり、部分（ソフトウェア）の変更は（少なくとも頻繁に）全体（サイバーフィジカルシステム）に検出可能で関連性のある変更を加え、全体の変更は（多くの場合）一部に関連性のある検出可能な変更を生じさせます（Spring and Illari 2018）

<details><summary>原文</summary><div>

When reasoning about a vulnerability, we assign the vulnerability to the nearest, relevant—yet more abstract—discrete component.
This assignment is particularly important when assessing technical impact on a component.
This description bears some clarification, via each of the adjectives:
</div></details>

脆弱性について推論するときは、最も近い、関連性のある、さらに抽象的な個別のコンポーネントに脆弱性を割り当てます。
この割り当ては、コンポーネントへの技術的影響を評価するときに特に重要です。
この説明は、各形容詞を介して、いくつか説明があります。。

<details><summary>原文</summary><div>

- Nearest is relative to the abstraction at which the vulnerability exists.
- Relevant implies that the impacted component must be in the chain of abstraction moving upward from the location of the flaw.
- More abstract means that the impacted component is at least one level of abstraction above the specific location of the vulnerability. For example, if the vulnerability is localized to a single line of code in a function, then the function, the module, the library, the application, the product, and the system it belongs to are all “more abstract.”
- Discrete means there is an identifiable thing that can be remediated (e.g., the unit of patching).
</div></details>

- **最も近い** とは脆弱性が存在する抽象化との関連性を表しています。
- **関連性** とは、影響を受けるコンポーネントが、欠陥がある状態から良い方向に変化する抽象化のチェーン内にあるはずだということを意味しています。
- **より抽象的である**とは、影響を受けるコンポーネントが、脆弱性の特定の場所より少なくとも1レベル上の抽象化であることを意味します。たとえば、脆弱性が関数内の1行のコードに限定されている場合、関数、モジュール、ライブラリ、アプリケーション、製品、およびそれが属するシステムはすべて「より抽象的」です。
- **離散的**とは、修理することができて識別可能であることを意味する（例えば、パッチを割り当てる単位）。

<details><summary>原文</summary><div>

Products, libraries, and applications tend to be appropriate objects of focus when seeking the right level to analyze the impact of a vulnerability.
For example, when reasoning about the technical impact of a vulnerability that is localized to a function in a module in an open source library, the nearest relevant discrete abstraction is the library because the patches are made available at the library level.
Similarly, analysis of a vulnerability in closed source database software that supports an enterprise resource management (ERM) system would consider the technical impact to the database, not to the ERM system.
</div></details>

製品、ライブラリ、およびアプリケーションは、脆弱性の影響を分析するために適切なレベルを探すときに適切なフォーカスの対象となる傾向があります。
たとえば、オープンソースライブラリのモジュール内の関数にローカライズされた脆弱性の技術的影響について推論する場合、パッチはライブラリレベルで利用可能になるため、最も近い関連する個別の抽象化はライブラリです。
同様に、エンタープライズリソース管理（ERM）システムをサポートするクローズドソースデータベースソフトウェアの脆弱性の分析では、ERMシステムではなく、データベースへの技術的な影響が考慮されます。


#### Relevant Security Policy (関連セキュリティポリシー)

<details><summary>原文</summary><div>

Our definition of a vulnerability includes a security policy violation, but it does not clarify whose security policies are relevant (Householder, Wassermann, et al. 2020).
For an organizational PSIRT or CSIRT, the organization’s security policy is most relevant.
The answer is less clear for coordinators or ISACs.
An example scenario that brings the question into focus is phone OS jailbreak methods.
</div></details>

脆弱性の定義にはセキュリティポリシー違反が含まれていますが、誰のセキュリティポリシーが関連しているかは明確ではありません （HouseHolder、WasperMann、et al.2020）。
PSIRTまたはCSIRTといった組織の場合、その組織のセキュリティポリシーは最も関連性があります。
コーディネーターやISACにとって、その答えはあまり明確ではありません。
質問に焦点をあてるシナリオの例は、スマホOSのジェイルブレイク方法です。

<details><summary>原文</summary><div>

The owner of the phone may elect to jailbreak it; there is at least an implicit security policy from the owner that allows this method.
However, from the perspective of the explicit phone OS security policy embedded in the access controls and separation of privileges, the jailbreak is exploiting a vulnerability.
If a security policy is embedded in technical controls, such as OS access controls on a phone, then anything that violates that security policy is a vulnerability.
</div></details>

電話の所有者はジェイルブレイクを選ぶかもしれません。この方法を許可している所有者からは少なくとも暗黙のセキュリティポリシーがあります。
ただし、アクセス制御に埋め込まれた明示的な電話OSセキュリティポリシーと特権の分離の観点から、ジェイルブレイクは脆弱性を悪用しています。
電話機のOSアクセス制御などの技術的制御にセキュリティポリシーが組み込まれている場合、そのセキュリティポリシーに違反するものはすべて脆弱性です。

### Reasoning Steps Forward (推論ステップ)

<details><summary>原文</summary><div>

This aspect of scope is about immediacy, prevalence, and causal importance.
Immediacy is about how soon after the decision point adverse effects should occur to be considered relevant.
Prevalence is about how common adverse effects should be to be considered relevant.
Causal importance is about how much an exploitation of the software in the cyber-physical system contributes to adverse effects to be considered relevant.
</div></details>

範囲のこの側面は即時性、有病率、そして因果的重要性についてのものです。
**即時性**は、決定点の影響がどのくらい早く関連性があると見なされるべきであるかについてです。
**有病率**は、一般的な副作用がどの程度関連性があると見なされるべきかについてです。
**因果的重要性**は、サイバーフィジカルシステムでのソフトウェアの悪用が、関連性があると見なされる悪影響にどの程度寄与するかについてです。

<details><summary>原文</summary><div>

Our recommendation is to walk a pragmatic middle path on all three aspects.
Effects are not relevant if they are merely possible, too infrequent, far distant, or unchanged by the vulnerability.
But effects are relevant long before they are absolutely certain, ubiquitous, or occurring presently.
Overall, we summarize this aspect of scope as consider credible effects based on known use cases of the software system as a part of cyber-physical systems.
</div></details>

私たちの推奨は、3つの側面すべてで実用的な中間の経路を歩くことです。
単に可能性があるというだけで、稀で、縁遠く、脆弱性によって変化が起こらない場合、悪影響は関係ありません。
しかし、それらが絶対に確実である、遍在する、または現在発生する前に、効果は長い間関連性があります。
全体として、ソフトウェアシステムの既知の使用例に基づく信頼できる効果を、サイバー物理システムの一部としての既知の使用例に基づく信頼できる効果を考慮しています。

---


## Likely Decision Points and Relevant Data（可能性のある決定ポイントと関連データ）

<details><summary>原文</summary><div>

We propose the following decision points and associated values should be a factor when making decisions about vulnerability prioritization.
Each decision point is tagged with the stakeholder it is relevant to: deployers, suppliers, or both.
We emphasize that these descriptions are hypotheses to be further tested and validated.
We made every effort to put forward informed and useful decision frameworks with wide applicability, but the goal of this paper is more to solicit feedback than make a declaration.
We welcome questions, constructive criticism, refuting evidence, or supporting evidence about any aspect of this proposal.
One important omission from the values for each category is an “unknown” option.
Instead, we recommend explicitly identifying an option that is a reasonable assumption based on prior events.
Such an option requires reliable historical evidence for what tends to be the case; of course, future events may require changes to these assumptions over time. 
Therefore, our assumptions require evidence and are open to debate in light of new evidence.
Different risk tolerance or risk discounting postures are not addressed in the current work; accommodating such tolerance or discounting explicitly is an area for future work.
This flexibility fits into our overall goal of supplying a decision-making framework that is both transparent and fits the needs of different communities.
Resisting an “unknown” option discourages the modeler from silently embedding these assumptions in their choices for how the decision tree flows below the selection of any “unknown” option.
We propose satisfactory decision points for vulnerability management in the next sections, in no particular order.
Each section has a subsection with advice on gathering information about the decision point.
SSVC using Current Information Sources will provide some suggestions about how existing sources of information about vulnerabilities can be used to collate responses to these decision points.
</div></details>

脆弱性の優先順位付けを決定する際には、次の決定ポイントと関連する値を考慮に入れる必要があることを提案します。
各決定ポイントには、関連する利害関係者（デプロイヤー、サプライヤー、またはその両方）がタグ付けされています。
このタグ付けによる説明は、さらにテストおよび検証される仮説であることを強調します。
私たちは、幅広い適用性を備えた、情報に基づいた有用な意思決定フレームワークを提案するためにあらゆる努力をしましたが、このペーパーの目的は、宣言を行うことよりもフィードバックを求めることです。
各カテゴリの値からの重要な排除の1つは、「unknown」の選択肢です。
代わりに、以前のイベントに基づいて合理的な仮定であるオプションを明示的に特定することをお勧めします。
そのようなオプションには、何が起こりがちかについての信頼できる歴史的証拠が必要です。 もちろん、将来のイベントでは、これらの仮定を時間の経過とともに変更する必要があります。
したがって、私たちの仮定には証拠が必要であり、新しい証拠に照らして議論することができます。
現在の作業では、さまざまなリスク許容度またはリスク削減の姿勢は取り上げられていません。 このような許容範囲に対応したり、明示的に削減したりすることは、将来の作業の領域です。
この柔軟性は、透明性があり、さまざまなコミュニティのニーズに適合する意思決定フレームワークを提供するという私たちの全体的な目標に適合します。
次のセクションでは、脆弱性管理のための満足のいく決定ポイントを順不同で提案します。
各セクションには、決定ポイントに関する情報の収集に関するアドバイスを含むサブセクションがあります。
現在の情報ソースを使用するSSVCは、脆弱性に関する既存の情報ソースを使用して、これらの決定ポイントへの応答を照合する方法に関するいくつかの提案を提供します。

### Exploitation（攻撃）

<details><summary>原文</summary><div>

Evidence of Active Exploitation of a Vulnerability

The intent of this measure is the present state of exploitation of the vulnerability.
The intent is not to predict future exploitation but only to acknowledge the current state of affairs.
Predictive systems, such as EPSS, could be used to augment this decision or to notify stakeholders of likely changes (Jacobs et al. 2019).

Table 5: Exploitation Decision Values

| Value | Definition |
| --- | --- |
| None | There is no evidence of active exploitation and no public proof of concept (PoC) of how to exploit the vulnerability. |
| PoC (Proof of Concept) | One of the following cases is true: (1) exploit code is sold or traded on underground or restricted fora; (2) a typical public PoC in places such as Metasploit or ExploitDB; or (3) the vulnerability has a well-known method of exploitation. Some examples of condition (3) are open-source web proxies serve as the PoC code for how to exploit any vulnerability in the vein of improper validation of TLS certificates. As another example, Wireshark serves as a PoC for packet replay attacks on ethernet or WiFi networks. |
| Active | Shared, observable, reliable evidence that the exploit is being used in the wild by real attackers; there is credible public reporting. |
</div></details>

有効な脆弱性を悪用した証拠

この対策の目的は、脆弱性の悪用の現状です。
目的は、将来の悪用を予測することではなく、現在の状況を確認することだけです。
EPSSなどの予測システムを使用して、この決定を補強したり、関係者に変更の可能性を通知したりできます（Jacobs et al.2019）。

表5: 攻撃決定値

| Value | Definition |
| --- | --- |
| None | 積極的な悪用の証拠はなく、脆弱性を悪用する方法の公的な概念実証（PoC）もありません。 |
| PoC (Proof of Concept) | 次のいずれかの場合に当てはまります。（1）エクスプロイトコードがアンダーグラウンドまたは限られたフォーラムで販売または取引されている。 （2）MetasploitやExploitDBなどの場所での一般的な公開されているPoC。 または（3）脆弱性には、よく知られた悪用方法がある。 条件（3）の例はたとえば、オープンソースのWebプロキシが、TLS証明書の不適切な検証によるネットワークの脆弱性を悪用する方法のPoCコードとして提供されているということです。 別の例として、WiresharkはイーサネットまたはWiFiネットワークでのパケットリプレイ攻撃のPoCとして機能します。 |
| Active | エクスプロイトが実際の攻撃者によって実際に使用されているという、共有されていて、観測可能で、信頼できる証拠、すなわち信頼できる公開されたレポートがあります。 |

#### Gathering Information About Exploitation（攻撃についての情報収集）

<details><summary>原文</summary><div>

(Householder, Chrabaszcz, et al. 2020) presents a method for searching the GitHub repositories of open-source exploit databases.
This method could be employed to gather information about whether PoC is true.
However, part (3) of PoC would not be represented in such a search, so more information gathering would be needed.
For part (3), perhaps we could construct a mapping of CWE-IDs which always represent vulnerabilities with well-known methods of exploitation.
For example, CWE-295, Improper Certificate Validation, and its child CWEs, describe improper validation of TLS certificates.
These CWE-IDs could always be marked as PoC since that meets condition (3) in the definition.
A comprehensive set of suggested CWE-IDs for this purpose is future work.
Gathering information for active is a bit harder.
If the vulnerability has a name or public identifier (such as a CVE-ID), a search of news websites, Twitter, the vendor’s vulnerability description, and public vulnerability databases for mentions of exploitation is generally adequate.
However, if the organization has the ability to detect exploitation attempts—for instance, through reliable and precise IDS signatures based on a public PoC—then detection of exploitation attempts also signals that active is the right choice.
Determining which vulnerability a novel piece of malware uses may be time consuming, requiring reverse engineering and a lot of trial and error.
Additionally, capable incident detection and analysis capabilities are required to make reverse engineering possible.
Because most organizations do not conduct these processes fully for most incidents, information about which vulnerabilities are being actively exploited generally comes from public reporting by organizations that do conduct these processes.
As long as those organizations also share detection methods and signatures, the results are usually quickly corroborated by the community.
For these reasons, we assess public reporting by established security community members to be a good information source for active; however, one should not assume it is complete.
The description for none says that there is no evidence of active exploitation.
This framing admits that an analyst may not be able to detect or know about every attack.
An analyst should feel comfortable selecting none if they (or their search scripts) have performed searches in the appropriate places for public PoCs and active exploitation (as described above) and found none.
Acknowledging that Exploitation values can change relatively quickly, we recommend conducting these searches frequently: if they can be automated to the organization’s satisfaction, perhaps once a day (see also Guidance on Communicating Results).
</div></details>

(Householder, Chrabaszcz, et al. 2020)は、オープンソースのエクスプロイトデータベースのGitHubリポジトリを検索する方法を提供します。
この方法は、PoCが真であるかどうかに関する情報を収集するために使用できます。
ただし、PoCのパート（3）はこのような検索では表示されないため、より多くの情報収集が必要になります。
パート（3）では、常によく知られている悪用方法で脆弱性を表すCWE-IDのマッピングを構築できます。
たとえば、CWE-295、不適切な証明書の検証、およびその子CWEは、TLS証明書の不適切な検証について説明しています。
これらのCWE-IDは、定義の条件（3）を満たしているため、常にPoCとしてマークできます。
この目的のために提案されたCWE-IDの包括的なセットは、将来の作業です。
有効な情報を収集するのは少し難しいです。
脆弱性に名前または公開識別子（CVE-IDなど）がある場合は、ニュースWebサイト、Twitter、ベンダーの脆弱性の説明、および悪用について言及するための公開脆弱性データベースを検索するのが一般的に適切です。
ただし、組織が悪用の試みを検出する機能を備えている場合（たとえば、パブリックPoCに基づく信頼性の高い正確なIDSシグニチャを通じて）、悪用の試みの検出は、有効が正しい選択であることも示します。
新しいマルウェアがどの脆弱性を使用しているかを判断するには時間がかかる可能性があり、リバースエンジニアリングと多くの試行錯誤が必要になります。
さらに、リバースエンジニアリングを可能にするには、有能なインシデント検出および分析機能が必要です。
ほとんどの組織はほとんどのインシデントに対してこれらのプロセスを完全に実行していないため、どの脆弱性が積極的に悪用されているかに関する情報は、通常、これらのプロセスを実行する組織による公開レポートから取得されます。
これらの組織が検出方法と署名も共有している限り、結果は通常、コミュニティによって迅速に裏付けられます。
これらの理由から、確立されたセキュリティコミュニティメンバーによる公開レポートは、アクティブな情報源として優れていると評価しています。ただし、それが完全であると想定するべきではありません。

### Technical Impact（技術的影響）

<details><summary>原文</summary><div>

Technical Impact of Exploiting the Vulnerability

When evaluating Technical Impact, recall the scope definition in the Scope Section.
Total control is relative to the affected component where the vulnerability resides.
If a vulnerability discloses authentication or authorization credentials to the system, this information disclosure should also be scored as “total” if those credentials give an adversary total control of the component.
As mentioned in Current State of Practice, the scope of SSVC is just those situations in which there is a vulnerability.
Our definition of vulnerability is based on the determination that some security policy is violated.
We consider a security policy violation to be a technical impact—or at least, a security policy violation must have some technical instantiation.
Therefore, if there is a vulnerability then there must be some technical impact.

Table 6: Technical Impact Decision Values

| Value | Definition |
| --- | --- |
| Partial | The exploit gives the adversary limited control over, or information exposure about, the behavior of the software that contains the vulnerability. Or the exploit gives the adversary an importantly low stochastic opportunity for total control. In this context, “low” means that the attacker cannot reasonably make enough attempts to overcome the low chance of each attempt not working.  Denial of service is a form of limited control over the behavior of the vulnerable
component. |
| Total | The exploit gives the adversary total control over the behavior of the software, or it gives total disclosure of all information on the system that contains the vulnerability |
</div></details>

脆弱性の悪用による技術的影響

技術的影響を評価するときは、スコープセクションのスコープ定義を思い出してください。
全体的な制御は、脆弱性が存在する影響を受けるコンポーネントに関連しています。
脆弱性が認証または承認のクレデンシャルをシステムに開示する場合、それらのクレデンシャルが攻撃者にコンポーネントの完全な制御を与える場合、この情報開示も「合計」としてスコアリングする必要があります。
現在の実務状況で述べたように、SSVCの範囲は、脆弱性が存在する状況にすぎません。
脆弱性の定義は、一部のセキュリティポリシーに違反しているという判断に基づいています。
セキュリティポリシー違反は技術的な影響であると考えています。少なくとも、セキュリティポリシー違反には技術的なインスタンス化が必要です。
したがって、脆弱性がある場合は、技術的な影響があるはずです。

表6: 技術的影響の決定値

| Value | Definition |
| --- | --- |
| Partial | この悪用は、脆弱性を含むソフトウェアの動作を攻撃者に限定的に制御したり、情報を公開したりします。 または、このエクスプロイトは、敵対者に完全な制御のための非常に低い確率的機会を与えます。 この文脈では、「低い」とは、攻撃の各試行を機能しないようにするために、攻撃するのに十分な合理的な試行をさせないということを意味します。サービス拒否は、脆弱なコンポーネントの動作に対する制限のひとつです。 |
| Total | このエクスプロイトは、攻撃者にソフトウェアの動作を完全に制御させたり、脆弱性を含むシステム上のすべての情報を完全に開示したりします。 |

#### Gathering Information About Technical Impact（技術的影響についての情報収集）

<details><summary>原文</summary><div>

Assessing Technical Impact amounts to assessing the degree of control over the vulnerable component the attacker stands to gain by exploiting the vulnerability.
One way to approach this analyiss is to ask whether the control gained is total or not.
If it is not total, it is partial.
If an answer to one of the following questions is yes, then control is total.
After exploiting the vulnerablily,

- can the attacker install and run arbitrary software?
- can the attacker trigger all the actions that the vulnerable component can perform?
- does the attacker get an account with full privileges to the vulnerable component (administrator or root user accounts, for example)?

This list is an evolving set of heuristics.
If you find a vulnerability that should have total Technical Impact but that does not answer yes to any of these questions, please describe the example and what question we might add to this list in an issue on the SSVC GitHub.
</div></details>

技術的影響の評価は、攻撃者が脆弱性を悪用することによって得られる脆弱なコンポーネントに対する制御の程度を評価することを意味します。
この分析にアプローチする1つの方法は、得られたコントロールが完全であるかどうかを尋ねることです。
totalでない場合は、partialです。
次の質問のいずれかに対する答えが「はい」の場合、コントロールは完全です。
脆弱性を悪用し、

- 攻撃者は任意のソフトをインストールして実行できるか？
- 攻撃者は脆弱性のあるコンポーネントを実行できる全ての行動をとることができるか？
- 攻撃者は脆弱性のあるコンポーネントへ完全な権限が付与されているアカウントを取得できるか（例えばadministorやrootユーザのアカウント）？

このリストは、進化するヒューリスティックのセットです。
全体的な技術的影響があるはずの脆弱性を見つけたが、これらの質問のいずれにも「はい」と答えない場合は、SSVC GitHubの問題で、例とこのリストに追加する可能性のある質問を説明してください。

### Utility（ユーティリティ）

<details><summary>原文</summary><div>

The Usefulness of the Exploit to the Adversary

Utility estimates an adversary’s benefit compared to their effort based on the assumption that they can exploit the vulnerability.
Utility is independent from the state of Exploitation, which measures whether a set of adversaries have ready access to exploit code or are in fact exploiting the vulnerability.
In economic terms, Exploitation measures whether the capital cost of producing reliable exploit code has been paid or not.
Utility estimates the marginal cost of each exploitation event.
More plainly, Utility is about how much an adversary might benefit from a campaign using the vulnerability in question, whereas Exploitation is about how easy it would be to start such a campaign or if one is already underway.
 Heuristically, we base Utility on a combination of the value density of vulnerable components and whether potential exploitation is automatable.
This framing makes it easier to analytically derive these categories from a description of the vulnerability and the affected component.
Automatable as (no or yes) and Value Density as (diffuse or concentrated) define those decision points.
 Roughly, Utility is a combination of two things: (1) the value of each exploitation event and (2) the ease and speed with which the adversary can cause exploitation events.
We define Utility as laborious, efficient, or super effective, as described in Utility Decision Values.
The next table is an equivalent expression of Utility that resembles a lookup table in a program.


Table 7: Utility Decision Values

| Value | Definition |
| --- | --- |
| Laborious | No to automatable and diffuse value |
| Efficient | {Yes to automatable and diffuse value} OR {No to automatable and concentrated value} |
| Super | Effective Yes to automatable and concentrated value |

Table 8: Utility to the Adversary, as a Combination of Automatable and Value Density

| Automatable | Value Density | Utility |
| no | diffuse | laborious |
| no | concentrated | efficient |
| yes | diffuse | efficient |
| yes | concentrated | super effective |
</div></details>

敵対者への攻撃の有用性

Utilityは、攻撃者が脆弱性を悪用できるという仮定に基づいて、攻撃者の努力と比較した場合の利益を推定します。
Utilityは、一連の攻撃者がコードを悪用する準備ができているかどうか、または実際に脆弱性を悪用しているかどうかを測定する[Exploitation](#Exploitation)から独立しているものです。
経済的には、Exploitationは、信頼できるエクスプロイトコードを作成するための資本コストが支払われているかどうかを測定します。
Utilityは、各悪用イベントの限界費用を見積もります。
より明確に言えば、Utilityは、問題の脆弱性を使用して攻撃者がキャンペーンからどれだけの利益を得ることができるかについてですが、エクスプロイトは、そのようなキャンペーンを開始するのがどれほど簡単か、またはキャンペーンがすでに進行中であるかどうかについてです。
ヒューリスティックに、脆弱なコンポーネントの価値密度と潜在的な悪用が自動化可能かどうかの組み合わせに基づいてUtilityを作成します。
このフレーミングにより、脆弱性と影響を受けるコンポーネントの説明からこれらのカテゴリを分析的に導き出すことが容易になります。
Automatable（no / yes）およびValue Density（diffuse or concentrated）は、これらの決定ポイントを定義します。
大まかに言えば、Utilityは2つの要素の組み合わせです。それは（1）各悪用イベントの価値と（2）攻撃者が悪用イベントを引き起こす可能性のある容易さとスピードです。
Utility決定値で説明​​されているように、Utilityを面倒、効率的、または非常に効果的と定義します。
次のテーブルは、プログラムのルックアップテーブルに似たUtilityの同等の式です。

表7: ユーティリティ決定値

| Value | Definition |
| --- | --- |
| Laborious | AtutomatableがnoでDensityがdiffuse |
| Efficient | {Automatable が Yesかつ Densityがdiffuse} または {Automatable がNoかつ Densityがconcentrated} |
| Super Effective | AutomatableがYesかつDensityがconcentrated |

表8: Density値と自動化可能性の組み合わせとしての攻撃者にとっての有用性

| Automatable | Value Density | Utility |
| --- | --- | --- |
| no | diffuse | laborious |
| no | concentrated | efficient |
| yes | diffuse | efficient |
| yes | concentrated | super effective |

### Automatable（自動化可能）

<details><summary>原文</summary><div>

Automatable captures the answer to the question “Can an attacker reliably automate creating exploitation events for this vulnerability?”.
This metric can take the values no or yes:
- no: Attackers cannot reliably automate steps 1-4 of the kill chain (Hutchins, Cloppert, and Amin 2011) for this vulnerability. These steps are (1) reconnaissance, (2) weaponization, (3) delivery, and (4) exploitation. Reasons why a step may not be reliably automatable could include the following:
    1. the vulnerable component is not searchable or enumerable on the network,
    2. weaponization may require human direction for each target,
    3. delivery may require channels that widely deployed network security configurations block, and
    4. exploitation is not reliable, due to exploit-prevention techniques enabled by default; ASLR is an example of an exploit-prevention tool.
- yes: Attackers can reliably automate steps 1-4 of the kill chain. If the vulnerability allows remote code execution or command injection, the expected response should be yes.

Due to vulnerability chaining, there is some nuance as to whether reconnaissance can be automated. For
example, consider a vulnerability A. If the systems vulnerable to A are usually not openly connected to
incoming traffic (that is, Exposure is small or controlled), reconnaissance probably cannot be automated
(scans would be blocked, etc.). This would make Automatable equal to no for vulnerability A. However,
suppose that another vulnerability B where Automatable is equal to yes can be reliably used to chain to
vulnerability A. This automates the reconnaissance of vulnerable systems. In this situation, the analyst
should continue to analyze vulnerability A to understand whether the remaining steps in the kill chain can
be automated.
</div></details>

Automatableは、「攻撃者はこの脆弱性の悪用イベントの作成を確実に自動化できるか」という質問に対する答えを捉えます。
この測定では、noまたはyesの値を取ることができます。
- no: 攻撃者は、この脆弱性に対してキルチェーンのステップ1〜4（Hutchins、Cloppert、and Amin 2011）を確実に自動化することはできません。
これらのステップは、（1）偵察、（2）武器化、（3）デリバリー、および（4）エクスプロイトです。 ステップを確実に自動化できない理由には、次のようなものがあります
  1. 脆弱なコンポーネントは、ネットワーク上で検索または列挙できません。
  2. 武器化には、ターゲットごとに人間の指示が必要な場合があります。
  3. デリバリーには、広く展開されているネットワークセキュリティ構成がブロックするチャネルが必要になる場合があります。
  4. エクスプロイト防止技術がデフォルトで有効になっているため、エクスプロイトは信頼できません。 例えばASLRは、エクスプロイト防止ツールの一例です。
- yes: 攻撃者は、キルチェーンのステップ1〜4を確実に自動化できます。 脆弱性によりリモートでコードが実行またはコマンドが挿入される可能性がある場合、予想される応答は「はい」であるはずです。

#### Gathering Information About Automatable （Automatableに関する情報の収集）

<details><summary>原文</summary><div>

An analyst should be able to sketch the automation scenario and how it either does or does not satisfy each of the four kill chain steps.
Once one step is not satisfied, the analyst can stop and select no.
Code that demonstrably automates all four kill chain steps certainly satisfies as a sketch.
We say sketch to indicate that plausible arguments, such as convincing psuedocode of an automation pathway for each step, are also adequate evidence in favor of a yes to Automatable.
Like all SSVC decision points, Automatable should capture the analyst’s best understanding of plausible scenarios at the time of the analysis.
An answer of no does not mean that it is absolutely inconceivable to automate exploitation in any scenario.
It means the analyst is not able to sketch a plausible path through all four kill chain steps.
“Plausible” sketches should account for widely deployed network and host-based defenses.
Liveness of Internet-connected services means quite a few overlapping things (Bano et al.  2018).
For most vulnerabilities, an open port does not automatically mean that reconnaissance, weaponization, and delivery are automatable.
Furthermore, discovery of a vulnerable service is not automatable in a situation where only two hosts are misconfigured to expose the service out of 2 million hosts that are properly configured.
As discussed in in Reasoning Steps Forward, the analyst should consider credible effects based on known use cases of the software system to be pragmatic about scope and providing values to decision points.
</div></details>

アナリストは、自動化シナリオと、それが4つのキルチェーンステップのそれぞれをどのように満たすか、または満たさないかを概略できる必要があります。
1つのステップが満たされない場合、アナリストは「いいえ」を選択し終了できます。
4つのキルチェーンステップすべてを明示的に自動化するコードは、概略として確かに満足します。
概略するとは、もっともらしい議論（例えば各ステップの自動化手順の説得力のある擬似コード）も、Automatableがyesになると賛同する十分な証拠であるということを指しています。
すべてのSSVC決定ポイントと同様に、Automatableは、分析の時点で、分析者がもっともらしいシナリオを最もよく理解していることを把握する必要があります。
「いいえ」の答えは、どのシナリオでも悪用を自動化することが絶対に考えられないという意味ではありません。
これは、アナリストが4つのキルチェーンステップすべてを通るもっともらしいパスを概略できないことを意味します。
「もっともらしい」概略は、広く展開されているネットワークとホストベースの防御を説明する必要があります。
インターネットに接続されたサービスのライブネスは、かなりの数の重複することを意味します（Bano et al.2018）。
ほとんどの脆弱性の場合、開いているポートがあるということは、偵察、武器化、および配信が自動化可能であることを自動的に意味するわけではありません。
さらに、適切に構成された200万のホストのうち、サービスを公開するために2つのホストのみが誤って構成されている状況では、脆弱なサービスの検出を自動化することはできません。
Reasoning Steps Forwardで説明したように、アナリストは、ソフトウェアシステムの既知のユースケースに基づく信頼できる効果を、範囲と意思決定ポイントへの価値の提供について実用的であると見なす必要があります。

### Value Density （価値密度）

<details><summary>原文</summary><div>

Value Density is described as diffuse or concentrated based on the resources that the adversary will gain control over with a single exploitation event:

- diffuse: The system that contains the vulnerable component has limited resources.
That is, the resources that the adversary will gain control over with a single exploitation event are relatively small.
Examples of systems with diffuse value are email accounts, most consumer online banking accounts, common cell phones, and most personal computing resources owned and maintained by users.
(A “user” is anyone whose professional task is something other than the maintenance of the system or component.
As with Safety Impact, a “system operator” is anyone who is professionally responsible for the proper operation or maintenance of a system.)
- concentrated: The system that contains the vulnerable component is rich in resources.
Heuristically, such systems are often the direct responsibility of “system operators” rather than users.
Examples of concentrated value are database systems, Kerberos servers, web servers hosting login pages, and cloud service providers.
However, usefulness and uniqueness of the resources on the vulnerable system also inform value density.
For example, encrypted mobile messaging platforms may have concentrated value, not because each phone’s messaging history has a particularly large amount of data, but because it is uniquely valuable to law enforcement.

</div></details>

値密度は、攻撃者が単一の悪用イベントで制御できるリソースに基づいて、diffuseまたはconcentratedと説明されます。

- diffuse: 脆弱なコンポーネントを含むシステムのリソースは限られています。
つまり、攻撃者が1回の悪用イベントで制御できるリソースは比較的小さいです。
diffuseのあるシステムの例としては、電子メールアカウント、ほとんどの消費者向けオンラインバンキングアカウント、一般的な携帯電話、およびユーザーが所有および保守しているほとんどのパーソナルコンピューティングリソースがあります。
（「ユーザー」とは、システムまたはコンポーネントの保守以外の専門的なタスクを行う人を指します。
Safety Impactと同様に、「システムオペレーター」とは、システムの適切な操作または保守に専門的な責任を負う人のことです。 ）。
- concentrated: 脆弱なコンポーネントを含むシステムは、リソースが豊富です。
ヒューリスティックに、このようなシステムは、多くの場合、ユーザーではなく「システムオペレーター」の直接の責任です。
集中的な価値の例としては、データベースシステム、Kerberosサーバー、ログインページをホストするWebサーバー、クラウドサービスプロバイダーなどがあります。
ただし、脆弱なシステム上のリソースの有用性と独自性も、価値密度に影響を与えます。
たとえば、暗号化されたモバイルメッセージングプラットフォームは、各電話のメッセージング履歴に特に大量のデータがあるためではなく、法執行機関にとって独自に価値があるため、価値が集中している可能性があります。

#### Gathering Information About Value Density （値密度の情報収集）


<details><summary>原文</summary><div>

The heuristics presented in the Value Density definitions involve whether the system is usually maintained by a dedicated professional, although we have noted some exceptions (such as encrypted mobile messaging applications).
If there are additional counterexamples to this heuristic, please describe them and the reasoning why the system should have the alternative decision value in an issue on the SSVC GitHub.
An analyst might use market research reports or Internet telemetry data to assess an unfamiliar product.
Organizations such as Gartner produce research on the market position and product comparisons for a large variety of systems.
These generally identify how a product is deployed, used, and maintained.
An organization’s own marketing materials are a less reliable indicator of how a product is used, or at least how the organization expects it to be used.
Network telemetry can inform how many instances of a software system are connected to a network.
Such telemetry is most reliable for the supplier of the software, especially if software licenses are purchased and checked.
Measuring how many instances of a system are in operation is useful, but having more instances does not mean that the software is a densely valuable target.
However, market penetration greater than approximately 75% generally means that the product uniquely serves a particular market segment or purpose.
This line of reasoning is what supports a determination that an ubiquitous encrypted mobile messaging application should be considered to have a concentrated Value Density.
</div></details>

値密度の定義に示されているヒューリスティックには、システムが通常は専任の専門家によって保守されているかどうかが含まれますが、いくつかの例外（暗号化されたモバイルメッセージングアプリケーションなど）についても説明しました。
このヒューリスティックに追加の反例がある場合は、それらと、システムがSSVC GitHubのissueで代わりとなる決定値を持つ必要がある理由を説明してください。
アナリストは、市場調査レポートまたはインターネットテレメトリデータを使用して、なじみのない製品を評価する場合があります。
Gartnerなどの組織は、多種多様なシステムの市場での位置付けと製品の比較に関する調査を行っています。
これらは通常、製品のデプロイ、使用、および保守の方法を識別します。
組織独自のマーケティング資料は、製品がどのように使用されているか、または少なくとも組織が製品の使用をどのように期待しているかを示す信頼性の低い指標です。
ネットワークテレメトリは、ソフトウェアシステムのインスタンスがネットワークに接続されている数を通知できます。
このようなテレメトリは、特にソフトウェアライセンスを購入して確認する場合、ソフトウェアのサプライヤにとって最も信頼性が高くなります。
システムのインスタンスがいくつ稼働しているかを測定することは有用ですが、インスタンスが多いからといって、ソフトウェアが非常に価値のあるターゲットであるとは限りません。
ただし、市場浸透率が約75％を超える場合は、通常、製品が特定の市場セグメントまたは目的に独自に対応していることを意味します。
この一連の推論は、ユビキタスな暗号化されたモバイルメッセージングアプリケーションが集中した価値密度を持っていると見なされるべきであるという決定をサポートするものです。

### Alternative Utility Outputs （Utiltiyの代替出力）

<details><summary>原文</summary><div>

Alternative heuristics can plausibly be used as proxies for adversary utility.
One example is the value of the vulnerability if it were sold on the open market.
Some firms, such as Zerodium, make such pricing structures public.
The valuable exploits track the Automatable and Value Density heuristics for the most part.
Within a single system—whether it is Apache, Windows, iOS or WhatsApp—more successfully automated steps in the kill lead to higher exploit value.
Remote code execution with sandbox escape and without user interaction are the most valuable exploits, and these features describe automation of the relevant kill chain steps.
How equivalently Automatable exploits for different systems are priced relative to each other is more idiosyncratic.
Price does not only track the Value Density of the system, but presumably also the existing supply of exploits and the installation distribution among the targets of Zerodium’s customers.
Currently, we simplify the analysis and ignore these factors.
However, future work should look for and prevent large mismatches between the outputs of the Utility decision point and the exploit markets.
</div></details>

代替ヒューリスティックは、敵対者のユーティリティの代わりとして使用できる可能性があります。
一例として、公開市場で販売された場合の脆弱性の価値があります。
Zerodiumなどの一部の企業は、そのような価格設定構造を公開しています。
貴重なエクスプロイトは、ほとんどの場合、自動化可能および値密度のヒューリスティックを追跡します。
Apache、Windows、iOS、WhatsAppのいずれであっても、単一のシステム内で、キルの自動化されたステップが成功すると、エクスプロイトの価値が高まります。
サンドボックスエスケープを使用し、ユーザーの操作を使用しないリモートコード実行は、最も価値のあるエクスプロイトであり、これらの機能は、関連するキルチェーンステップの自動化を説明します。
さまざまなシステムの自動化可能なエクスプロイトの価格が互いにどの程度同等であるかは、より特異です。
価格は、システムの価値密度を追跡するだけでなく、おそらく、エクスプロイトの既存の供給と、Zerodiumの顧客のターゲット間のインストールの分布も追跡します。
現在、分析を簡素化し、これらの要因を無視しています。
ただし、将来の作業では、ユーティリティ決定ポイントの出力とエクスプロイト市場の間の大きな不一致を探して防止する必要があります。

### Safety Impact （安全性への影響）

<details><summary>原文</summary><div>

Safety Impacts of Affected System Compromise

We take an expansive view of safety, in which a safety violation is a violation of what the United States Centers for Disease Control (CDC) calls well-being.
Physical well-being violations are common safety violations, but we also consider economic, social, emotional, and psychological well-being to be important.
Weighing fine differences among these categories is probably not possible, so we will not try.
Each decision option lists examples of the effects that qualify for that value/answer in the various types of violations of well-being.
These examples should not be considered comprehensive or exhaustive, but rather as suggestive.
The stakeholder should consider the safety impact on the system operators (by “system operator,” we mean those who are professionally responsible for the proper operation of the cyber-physical system, as the term is used in the safety analysis literature) and users of the software they provide.
If software is repackaged and resold by a stakeholder to further downstream entities who will then sell a product, the initial stakeholder can only reasonably consider so many links in that supply chain.
However, a stakeholder should know its immediate consumers who are one step away in the supply chain.
Those consumers may repackage or build on the software and then provide that product further on.
We expect that a stakeholder should be aware of common usage of their software about one step away in the supply chain.
This expectation holds in both open source and proprietary contexts.
Further steps along the supply chain are probably not reasonable for the stakeholder to consider consistently; however, this is not a license to willfully ignore common downstream uses of the stakeholder’s software.
If the stakeholder is contractually or legally responsible for safe operation of the software or cyber-physical system of which it is part, that also supersedes our rough supply-chain depth considerations.
For software used in a wide variety of sectors and deployments, the stakeholder may need to estimate an aggregate safety impact.
Aggregation suggests that the stakeholder’s response to this decision point cannot be less than the most severe credible safety impact, but we leave the specific aggregation method or function as a domain-specific extension for future work.
</div></details>

影響を受けるシステム侵害の安全性への影響

私たちは安全性について広範な見解を持っています。安全性違反は、米国疾病対策センター（CDC）が幸福と呼んでいるものに対しての違反です。
身体的幸福違反は一般的な安全違反ですが、経済的、社会的、感情的、心理的幸福も重要であると考えています。
これらのカテゴリー間の微妙な違いを比較検討することはおそらく不可能なので、私たちは試みません。
各決定オプションには、さまざまなタイプの幸福の違反におけるその価値/回答の対象となる効果の例がリストされています。
これらの例は、包括的または網羅的であると見なされるべきではなく、むしろ示唆的なものと見なされるべきです。
利害関係者は、システムオペレーター（「システムオペレーター」とは、安全分析の文献で使用されているサイバーフィジカルシステムの適切な運用に専門的に責任を負う者を意味します）およびユーザーに対する安全上の影響を考慮する必要があります。彼らが提供するソフトウェア。
ソフトウェアが再パッケージ化され、利害関係者によってさらに下流のエンティティに再販され、その後製品を販売する場合、最初の利害関係者は、そのサプライチェーン内の非常に多くのリンクのみを合理的に検討できます。
ただし、利害関係者は、サプライチェーンの一歩先にある直接の消費者を知っている必要があります。
それらの消費者は、ソフトウェアを再パッケージ化または構築してから、その製品をさらに提供することができます。
利害関係者は、サプライチェーンの約1歩先でソフトウェアの一般的な使用法を認識している必要があります。
この期待は、オープンソースとプロプライエタリの両方のコンテキストに当てはまります。
サプライチェーンに沿ったさらなるステップは、利害関係者が一貫して検討するのにおそらく合理的ではありません。ただし、これは、利害関係者のソフトウェアの一般的なダウンストリーム使用を故意に無視するライセンスではありません。
利害関係者が、その一部であるソフトウェアまたはサイバーフィジカルシステムの安全な運用について契約上または法的に責任を負う場合、それはまた、サプライチェーンの深さに関する大まかな考慮事項に優先します。
さまざまな分野や展開で使用されるソフトウェアの場合、利害関係者は安全への影響の総計を見積もる必要があるかもしれません。
集計は、この決定ポイントに対する利害関係者の応答が、最も深刻な信頼できる安全上の影響を下回ることはできないことを示唆していますが、特定の集計方法または機能は、将来の作業のためにドメイン固有の拡張として残します。

#### Gathering Information About Safety Impact （安全性への影響についての情報収集）

<details><summary>原文</summary><div>

The factors that influence the safety impact level are diverse.
This paper does not exhaustively discuss how a stakeholder should answer a question; that is a topic for future work.
At a minimum, understanding safety impact should include gathering information about survivability of the vulnerable component, determining available operator actions to compensate for the vulnerable component, understanding relevant insurance, and determining the viability of existing backup measures.
Because each of these information items depends heavily on domain-specific knowledge, it is out of the scope of this paper to give a general-purpose strategy for how they should be included.
For example, viable manual backup mechanisms are likely to be important in assessing the safety impact of an industrial control system in a sewage plant, but in banking the insurance structures that prevent bankruptcies are more important.
The decision values for safety impact are based on the hazard categories for aircraft software (RTCA, Inc. 2012; FAA 2000, Section 3.3.2).
To assign a value to Safety Impact, at least one type of harm must reach that value.
For example, for a Safety Impact of major, at least one type of harm must reach major level.
All types of harm do not need to rise to the level of major, just one type of harm does.

Table 9: Safety Impact Decision Values

| Value | Type of Harm | Definition |
| --- | --- | --- |
| None | All | Does not mean no impact literally; the effect is below the threshold for all aspects described in Minor |
| Minor | Physical Harm | Physical discomfort for users of the system OR a minor occupational safety hazard OR reduction in physical system safety margins |
| Minor | Environment | Minor externalities (property damage, environmental damage, etc.) imposed on other parties |
| Minor | Financial | Financial losses, which are not readily absorbable, to multiple persons |
| Minor | Psychological | Emotional or psychological harm, sufficient to be cause for counseling or therapy, to multiple persons |
| Major | Physical Harm | Physical distress and injuries for users of the system OR a significant occupational safety hazard OR failure of physical system functional capabilities that support safe operation |
| Major | Environment | Major externalities (property damage, environmental damage, etc.) imposed on other parties |
| Major | Financial | Financial losses that likely lead to bankruptcy of multiple persons |
| Major | Psychological | Widespread emotional or psychological harm, sufficient to be cause for counseling or therapy, to populations of people |
| Hazardous | Physical Harm | Serious or fatal injuries, where fatalities are plausibly preventable via emergency services or other measures OR parts of the cyber-physical system that support safe operation break |
| Hazardous | Environment | Serious externalities (threat to life as well as property, widespread environmental damage, measurable public health risks, etc.) imposed on other parties |
| Hazardous | Financial | Socio-technical system (elections, financial grid, etc.) of which the affected component is a part is actively destabilized and enters unsafe state |
| Hazardous | Psychological | N/A |
| Catastrophic | Physical Harm | Multiple immediate fatalities (emergency response probably cannot save the victims.) |
| Catastrophic | Environment  | Extreme externalities (immediate public health threat, environmental damage leading to small ecosystem collapse, etc.) imposed on other parties |
| Catastrophic | Financial | Social systems (elections, financial grid, etc.) supported by the software collapse |
| Catastrophic | Psychological | N/A |
</div></details>

安全影響レベルに影響を与える要因は多様です。
このペーパーでは、利害関係者が質問にどのように答えるべきかを網羅的に説明していません。それは将来の仕事のトピックです。
少なくとも、安全への影響を理解するには、脆弱なコンポーネントの存続可能性に関する情報を収集し、脆弱なコンポーネントを補うために利用可能なオペレーターのアクションを決定し、関連する保険を理解し、既存のバックアップ手段の実行可能性を決定する必要があります。
これらの各情報項目はドメイン固有の知識に大きく依存しているため、それらをどのように含めるかについての汎用戦略を示すことは、この論文の範囲外です。
たとえば、実行可能な手動バックアップメカニズムは、下水処理場の産業用制御システムの安全性への影響を評価する上で重要である可能性がありますが、破産を防ぐ保険構造を銀行に預ける場合はより重要です。
安全性への影響の決定値は、航空機ソフトウェアの危険有害性カテゴリに基づいています（RTCA、Inc. 2012; FAA 2000、セクション3.3.2）。
Safety Impactに値を割り当てるには、少なくとも1つのタイプの危害がその値に到達する必要があります。
たとえば、メジャーの安全性への影響については、少なくとも1つのタイプの危害がメジャーレベルに到達する必要があります。
すべての種類の危害は、重大なレベルまで上昇する必要はありません。1つの種類の危害だけが上昇します。

表 9: 安全性への影響の決定値

| 値 | 害の種類 | 定義 |
| --- | --- | --- |
| None | すべて | 文字通り影響がないという意味ではありません。効果は、Minorで説明されているすべての側面のしきい値を下回っています。 |
| Minor | 身体的危害 | システムのユーザーに対する身体的不快感、または軽微な労働安全上の危険、または物理的システムの安全マージンの低下 | 
| Minor | 環境 | 他者に課せられた軽微な外部性（物的損害、環境被害など） | 
| Minor | 財務 | 容易に吸収できない複数の人への経済的損失 | 
| Minor | 心理学 | 複数の人へのカウンセリングまたは治療の原因となるのに十分な感情的または心理的危害 | 
| Major | 身体的危害 | システムのユーザーの身体的苦痛および負傷、または重大な労働安全上の危険、または安全な操作をサポートする物理的システムの機能の障害 | 
| Major | 環境 | 他者に課せられる主な外部性（物的損害、環境被害など） | 
| Major | 財務 | 複数人の破産につながる可能性のある経済的損失 | 
| Major | 心理学 | 人々の集団に対するカウンセリングまたは治療の原因となるのに十分な、広範囲にわたる感情的または心理的危害 | 
| Hazardous | 身体的危害 | 救急サービスやその他の手段、または安全な操作の中断をサポートするサイバーフィジカルシステムの一部を介して死亡者を予防できる可能性のある重傷または致命傷 | 
| Hazardous | 環境 | 他の当事者に課せられた深刻な外部性（生命および財産への脅威、広範囲にわたる環境被害、測定可能な公衆衛生上のリスクなど） | 
| Hazardous | 財務 | 影響を受けるコンポーネントがその一部である社会技術システム（選挙、金融証券など）は、活発に不安定化され、危険な状態になります。
| Hazardous | 心理学 | 該当なし | 
| Catastrophic | 身体的危害 | 複数の即時の死者（緊急対応はおそらく犠牲者を救うことはできません。） | 
| Catastrophic | 環境 | 他の当事者に課せられた極端な外部性（即時の公衆衛生上の脅威、小さな生態系の崩壊につながる環境被害など） | 
| Catastrophic | 財務 | ソフトウェアによって支えられた社会システム（選挙、金融証券など）の崩壊 | 
| Catastrophic | 心理学 | 該当なし | 

#### Public Safety Impact

<details><summary>原文</summary><div>

Suppliers necessarily have a rather coarse-grained perspective on the broadly defined safety impacts described above.
Therefore we simplify the above into a binary categorization: Significant is when any impact meets the criteria for an impact of Major, Hazardous, or Catastrophic in the above table.
Minimal is when none do.

Table 10: Public Safety Impact Decision Values
| Value | Definition |
| --- | --- |
| Minimal | Safety Impact of None or Minor |
| Significant | Safety Impact of Major, Hazardous, or Catastrophic |
</div></details>

サプライヤーは必然的に、上記の広く定義された安全への影響についてかなり大まかな見方をしています。
したがって、上記を2値の分類に単純化します。重要なのは、影響が上記の表の重大、危険、または壊滅的な影響の基準を満たしている場合です。
最小とは、何もしない場合です。

表10：大衆への安全影響の決定値
| 値 | 定義 |
| --- | --- |
| Minimal | NoneまたはMinorの安全性への影響 |
| Significant | Major, Hazardous, Catastrophicな安全への影響 |

#### Situated Safety Impact

<details><summary>原文</summary><div>

Deployers are anticipated to have a more fine-grained perspective on the safety impacts broadly defined in Safety Impact. We defer this topic for now because we combine it with Mission Impact to simplify implementation for deployers.
</div></details>

デプロイヤーは、安全性への影響で広く定義されている安全性への影響について、よりきめ細かい視点を持つことが期待されます。 このトピックをMissionImpactと組み合わせてデプロイヤーの実装を簡素化するため、このトピックは今のところ延期します。

### Mission Impact

<details><summary>原文</summary><div>

Impact on Mission Essential Functions of the Organization

A mission essential function (MEF) is a function “directly related to accomplishing the organization’s mission as set forth in its statutory or executive charter” (Fenton 2017, A–1). Identifying MEFs is part of business continuity planning or crisis planning. The rough difference between MEFs and non-essential functions is that an organization “must perform a[n MEF] during a disruption to normal operations” (Fenton 2017, B–2). The mission is the reason an organization exists, and MEFs are how that mission is affected.  Non-essential functions do not directly support the mission per se; however, they support the smooth delivery or success of MEFs. Financial losses—especially to publicly traded for-profit corporations—are covered here as a (legally mandated) mission of such corporations is financial performance.

Table 11: Mission Impact Decision Values

| Value | Definition |
| --- | --- |
| None / Non-Essential Degraded | Little to no impact up to degradation of non-essential functions; chronic degradation would eventually harm essential functions |
| MEF Support Crippled | Activities that directly support essential functions are crippled; essential functions continue for a time |
| MEF Failure | Any one mission essential function fails for period of time longer than acceptable; overall mission of the organization degraded but can still be accomplished for a time |
| Mission Failure | Multiple or all mission essential functions fail; ability to recover those functions degraded; organization’s ability to deliver its overall mission fails |
</div></details>

組織のミッションに不可欠な機能への影響

Mission essntial function（MEF）は、「法定または執行憲章に定められている組織のミッションの達成に直接関連する」機能です（Fenton 2017、A–1）。
MEFの特定は、事業継続計画または危機計画の一部です。
MEFと非必須機能の大まかな違いは、組織が「通常の運用の中断中に[n MEF]を実行する必要がある」ことです（Fenton 2017、B–2）。
ミッションは組織が存在する理由であり、MEFはそのミッションがどのように影響を受けるかです。
本質的でない機能は、ミッション自体を直接サポートするものではありません。
ただし、MEFのスムーズな配信または成功をサポートします。
特に上場営利企業にとっての経済的損失は、そのような企業の（法的に義務付けられた）使命は財務実績であるため、ここでカバーされます。

表 11: ミッションへの影響の決定値

| 値 | 定義 |
| --- | --- |
| None / Non-Essential Degraded | 本質的でない機能の低下まで、ほとんどまたはまったく影響がありません。 慢性的な劣化は、最終的には本質的な機能を損なうでしょう |
| MEF Support Crippled | 重要な機能を直接サポートする活動は機能しません。 重要な機能はしばらく続く |
| MEF Failure | 1つのミッションに不可欠な機能は、許容範囲を超える期間にわたって失敗します。 組織の全体的な使命は低下しましたが、それでもしばらくの間達成することができます |
| Mission Failure | 複数またはすべてのミッションに不可欠な機能が失敗します。 これらの機能を回復する能力が低下しました。 全体的な使命を果たす組織の能力は失敗します |

#### Gathering Information About Mission Impact

<details><summary>原文</summary><div>

The factors that influence the mission impact level are diverse. This paper does not exhaustively discuss how a stakeholder should answer a question; that is a topic for future work. At a minimum, understanding mission impact should include gathering information about the critical paths that involve vulnerable components, viability of contingency measures, and resiliency of the systems that support the mission.  There are various sources of guidance on how to gather this information; see for example the FEMA guidance in Continuity Directive 2 (Fenton 2017) or OCTAVE FORTE (Tucker 2018). This is part of risk management more broadly. It should require the vulnerability management team to interact with more senior management to understand mission priorities and other aspects of risk mitigation.  As a heuristic, Utility might constrain Mission Impact if both are not used in the same decision tree. For example, if the Utility is super effective, then Mission Impact is at least MEF support crippled.
</div></details>

ミッションの影響レベルに影響を与える要因はさまざまです。このペーパーでは、利害関係者が質問にどのように答えるべきかを網羅的に説明していません。それは将来の仕事のトピックです。少なくとも、ミッションへの影響を理解するには、脆弱なコンポーネントが関与するクリティカルパス、緊急対策の実行可能性、およびミッションをサポートするシステムの復元力に関する情報を収集する必要があります。この情報を収集する方法については、さまざまなガイダンスがあります。たとえば、Continuity Directive 2（Fenton 2017）またはOCTAVE FORTE（Tucker 2018）のFEMAガイダンスを参照してください。これは、より広義のリスク管理の一部です。脆弱性管理チームは、ミッションの優先順位やリスク軽減の他の側面を理解するために、より上級管理職と対話する必要があります。ヒューリスティックとして、両方が同じデシジョンツリーで使用されていない場合、ユーティリティはミッションインパクトを制約する可能性があります。たとえば、ユーティリティが非常に効果的である場合、MissionImpactは少なくともMEFサポートが機能しなくなります。

### Human Impact

<details><summary>原文</summary><div>

Combined Situated Safety and Mission Impact

In pilot implementations of SSVC, we received feedback that organizations tend to think of mission and safety impacts as if they were combined into a single factor: in other words, the priority increases regardless which of the two impact factors was increased. We therefore combine Situated Safety and Mission Impact for deployers into a single Human Impact factor as a dimension reduction step as follows.  We observe that the day-to-day operations of an organization often have already built in a degree of tolerance to small-scale variance in mission impacts. Thus in our opinion we need only concern ourselves with discriminating well at the upper end of the scale. Therefore we combine the three lesser mission impacts of none, non-essential degraded, and MEF support crippled into a single category, while retaining the distinction between MEF Failure and Mission Failure at the extreme. This gives us three levels of mission impact to work with.  On the other hand, most organizations tend to have lower tolerance for variance in safety. Even small deviations in safety are unlikely to go unnoticed or unaddressed. We suspect that the presence of regulatory oversight for safety issues and its absence at the lower end of the mission impact scale influences this behavior. Because of this higher sensitivity to safety concerns, we chose to retain a four-level resolution for the safety dimension. We then combine Mission Impact with Situated Safety impact and map them onto a 4-tiered scale (Low, Medium, High, Very High). The mapping is shown in the following table.

table 12: combining mission and situated safety impact into human impact

| situated safety impact | mission impact | combined value (human impact) |
| --- | --- | --- |
| none/minor | none/degraded/crippled | low |
| none/minor | mef failure | medium |
| none/minor | mission failure | very high |
| major | none/degraded/crippled | medium |
| major | mef failure | high |
| major | mission failure | very high |
| hazardous | none/degraded/crippled | high |
| hazardous | mef failure | high |
| hazardous | mission failure | very high |
| catastrophic | none/degraded/crippled | very high |
| catastrophic | mef failure | very high |
| catastrophic | mission failure | very high |
</div></details>

状況に応じた安全性とミッションへの影響の組み合わせ

SSVCの案内的な実装では、組織はミッションと安全性の影響を1つの要素にまとめられているかのように考える傾向があるというフィードバックを受け取りました。
つまり、2つの影響要素のどちらが増加しても、優先度が高くなります。
したがって、次のように、次元削減ステップとして、デプロイヤーの状況に応じた安全性とミッションインパクトを単一のヒューマンインパクト要素に統合します。
組織の日常業務では、ミッションの影響の小規模な変動に対するある程度の許容度がすでに組み込まれていることがよくあります。
したがって、私たちの意見では、スケールの上限でうまく区別することだけに関心を向ける必要があります。
したがって、MEFの失敗とミッションの失敗の極端な区別を維持しながら、ミッションの影響が少ない、本質的ではない劣化、およびMEFサポートの3つの影響を1つのカテゴリにまとめます。
これにより、3つのレベルのミッションへの影響を処理できます。
一方、ほとんどの組織は、安全性の変動に対する許容度が低い傾向があります。
安全性のわずかな逸脱でさえ、見過ごされたり、対処されなかったりする可能性はほとんどありません。
安全性の問題に対する規制上の監視の存在と、ミッションの影響スケールの下限での監視の欠如が、この動作に影響を与えていると思われます。
安全上の懸念に対するこの高い感度のために、安全次元の4レベルの解像度を維持することを選択しました。
次に、ミッションの影響と状況に応じた安全の影響を組み合わせて、4段階のスケール（Low, Medium, High, Very High）にマッピングします。マッピングを次の表に示します。

表 12: ミッションと状況への影響を組み合わせた人類への影響

| situated safety impact | mission impact | combined value (human impact) |
| --- | --- | --- |
| none/minor | none/degraded/crippled | low |
| none/minor | MEF failure | medium |
| none/minor | mission failure | very high |
| major | none/degraded/crippled | medium |
| major | MEF failure | high |
| major | mission failure | very high |
| hazardous | none/degraded/crippled | high |
| hazardous | MEF failure | high |
| hazardous | mission failure | very high |
| catastrophic | none/degraded/crippled | very high |
| catastrophic | MEF failure | very high |
| catastrophic | mission failure | very high |

#### Safety and Mission Impact Decision Points for Industry Sectors

<details><summary>原文</summary><div>

We expect to encounter diversity in both safety and mission impacts across different organizations.  However, we also anticipate a degree of commonality of impacts to arise across organizations within a given industry sector. For example, different industry sectors may have different use cases for the same software. Therefore, vulnerability information providers—that is, vulnerability databases, Information Sharing and Analysis Organizations (ISAOs), or Information Sharing and Analysis Centers (ISACs)—may provide SSVC information tailored as appropriate to their constituency’s safety and mission concerns. For considerations on how organizations might communicate SSVC information to their constituents, see
Guidance on Communicating Results.
</div></details>

さまざまな組織間で、安全性とミッションへの影響の両方に多様性が見られることを期待しています。 ただし、特定の業界セクター内の組織間である程度の影響の共通性が生じることも予想されます。 たとえば、異なる業界セクターでは、同じソフトウェアのユースケースが異なる場合があります。 したがって、脆弱性情報プロバイダー（つまり、脆弱性データベース、情報共有および分析組織（ISAO）、または情報共有および分析センター（ISAC））は、構成員の安全および任務の懸念に応じて調整されたSSVC情報を提供する場合があります。 組織がSSVC情報を構成員に伝達する方法に関する考慮事項については、Guidance on Communicating Resultsを参照してください。

### System Exposure

<details><summary>原文</summary><div>

The Accessible Attack Surface of the Affected System or Service Measuring the attack surface precisely is difficult, and we do not propose to perfectly delineate between small and controlled access. Exposure should be judged against the system in its deployed context, which may differ from how it is commonly expected to be deployed. For example, the exposure of a device on a vehicle’s CAN bus will vary depending on the presence of a cellular telemetry device on the same bus.  If a vulnerability cannot be remediated, other mitigations may be used. Usually, the effect of these mitigations is to reduce exposure of the vulnerable component. Therefore, a deployer’s response to Exposure may change if such mitigations are put in place. If a mitigation changes exposure and thereby reduces the priority of a vulnerability, that mitigation can be considered a success. Whether that mitigation allows the deployer to defer further action varies according to each case.

Table 13: System Exposure Decision Values

| Value | Definition |
| --- | --- |
| Small | Local service or program; highly controlled network |
| Controlled | Networked service with some access restrictions or mitigations already in place (whether locally or on the network). A successful mitigation must reliably interrupt the adversary’s attack, which requires the attack is detectable both reliably and quickly enough to respond. Controlled covers the situation in which a vulnerability can be exploited through chaining it with other vulnerabilities. The assumption is that the number of steps in the attack path is relatively low; if the path is long enough that it is implausible for an adversary to reliably execute it, then exposure should be small. |
| Open | Internet or another widely accessible network where access cannot plausibly be restricted or controlled (e.g., DNS servers, web servers, VOIP servers, email servers) |
</div></details>

影響を受けるシステムまたはサービスのアクセス可能な攻撃対象領域を正確に測定することは困難であり、小規模なアクセスと制御されたアクセスを完全に区別することは提案していません。
Exposureは、配備された状況でシステムに対して判断する必要があります。
これは、一般的に配備されると予想される方法とは異なる場合があります。
たとえば、車両のCANバス上のデバイスの露出は、同じバス上のセルラーテレメトリデバイスの存在によって異なります。
脆弱性を修正できない場合は、他の緩和策を使用できます。
通常、これらの緩和策の効果は、脆弱なコンポーネントの露出を減らすことです。
したがって、このような緩和策を講じると、Exposureに対するデプロイヤの応答が変わる可能性があります。
緩和策によってExposureが変更され、それによって脆弱性の優先度が低下した場合、その緩和策は成功と見なすことができます。
その緩和策により、デプロイヤがそれ以上のアクションを延期できるかどうかは、ケースごとに異なります。

表 13: System Exposure Decision Values

| Value | Definition |
| --- | --- |
| Small | ローカルサービスまたはプログラム。 高度に制御されたネットワーク |
| Controlled | いくつかのアクセス制限または緩和策がすでに実施されているネットワークサービス（ローカルまたはネットワーク上）。 緩和を成功させるには、敵の攻撃を確実に中断する必要があります。これには、攻撃が確実に検出され、応答するのに十分な速さである必要があります。 Controlledは、脆弱性を他の脆弱性と連鎖させることで悪用される可能性のある状況をカバーします。 攻撃パスのステップ数は比較的少ないと想定されています。 パスが十分に長く、敵が確実に実行することが不可能な場合は、露出を小さくする必要があります。 |
| Open | インターネットまたはアクセスを制限または制御できない可能性のある別の広くアクセス可能なネットワーク（DNSサーバー、Webサーバー、VOIPサーバー、電子メールサーバーなど） |

#### Gathering Information About System Exposure

<details><summary>原文</summary><div>

System Exposure is primarily used by Deployers, so the question is about whether some specific system is in fact exposed, not a hypothetical or aggregate question about systems of that type. Therefore, it generally has a concrete answer, even though it may vary from vulnerable component to vulnerable component, based on their respective configurations.  System Exposure can be readily informed by network scanning techniques. For example, if the vulnerable component is visible on Shodan or by some other external scanning service, then it is open. Network policy or diagrams are also useful information sources, especially for services intentionally open to the Internet such as public web servers. An analyst should also choose open for a phone or PC that connects to the web or email without the usual protections (IP and URL blocking, updated firewalls, etc.).  Distinguishing between small and controlled is more nuanced. If open has been ruled out, some suggested heuristics for differentiating the other two are as follows. Apply these heuristics in order and stop when one of them applies.
- If the system’s networking and communication interfaces have been physically removed or disabled,
choose small.
- If Automatable is yes, then choose controlled. The reasoning behind this heuristic is that if
reconnaissance through exploitation is automatable, then the usual deployment scenario exposes
the system sufficiently that access can be automated, which contradicts the expectations of small.
- If the vulnerable component is on a network where other hosts can browse the web or receive email, choose controlled.
If you have suggestions for further heuristics, or potential counterexamples to these, please describe the example and reasoning in an issue on the SSVC GitHub.

</div></details>

System Exposureは主にデプロイヤーによって使用されるため、問題は特定のシステムが実際にExposureされているかどうかに関するものであり、そのタイプのシステムに関する架空の質問や集約的な質問ではありません。したがって、脆弱なコンポーネントごとにそれぞれの構成に基づいて変化する可能性がありますが、一般的に具体的な答えがあります。システムの露出は、ネットワークスキャン技術によって簡単に通知できます。たとえば、脆弱なコンポーネントがShodanまたはその他の外部スキャンサービスで表示されている場合、そのコンポーネントは開いています。ネットワークポリシーや図も、特にパブリックWebサーバーなど、意図的にインターネットに公開されているサービスにとって有用な情報源です。アナリストは、通常の保護（IPおよびURLのブロック、更新されたファイアウォールなど）なしでWebまたは電子メールに接続する電話またはPCに対してもオープンを選択する必要があります。小さいものと制御されたものを区別することは、より微妙です。オープンが除外されている場合、他の2つを区別するためのいくつかの提案されたヒューリスティックは次のとおりです。これらのヒューリスティックを順番に適用し、そのうちの1つが適用されたら停止します。

- システムのネットワークおよび通信インターフェースが物理的に削除または無効にされている場合、 小さいものを選択してください。
- Automatableがyesの場合は、controlledを選択します。 このヒューリスティックの背後にある理由は、悪用による偵察は自動化可能であり、通常の展開シナリオでは次のようになります。 アクセスを自動化できるほどのシステムであり、これは小規模の期待と矛盾します。
- 脆弱なコンポーネントが、他のホストがWebを閲覧したり、電子メールを受信したりできるネットワーク上にある場合は、制御を選択します。

さらなるヒューリスティックの提案、またはこれらに対する潜在的な反例がある場合は、SSVCGitHubのissueで例と理由を説明してください。

## Decisions During Vulnerability Coordination (脆弱性調整中の決定)

<details><summary>原文</summary><div>

Coordinators are facilitators within the vulnerability management ecosystem. Since coordinators neither supply nor deploy the vulnerable component in question, their decisions are different from suppliers’ or deployers’ decisions. This section provides a window into CERT/CC’s decisions as an example of how a coordinator might use SSVC to make its own decisions.  Coordinators vary quite a lot, and their use of SSVC may likewise vary. A coordinator may want to gather and publish information about SSVC decision points that it does not use internally in order to assist its constituents. Furthermore, a coordinator may only publish some of the information it uses to make decisions. Consistent with other stakeholder perspectives (supplier and deployer), SSVC provides the priority with which a coordinator should take some defined action, but not how to do that action. For more information about types of coordinators and their facilitation actions within vulnerability management, see (Householder, Wassermann, et al. 2020).  The two decisions that CERT/CC makes as a coordinator that we will discuss in terms of SSVC are the initial triage of vulnerability reports and whether a publication about a vulnerability is warranted.  The initial coordination decision is a prioritization decision, but it does not have the same values as prioritization by a deployer or supplier. The publication decision for us is a binary yes/no. These two decisions are not the entirety of vulnerability coordination, but we leave further details of the process for future work.
Different coordinators have different scopes and constituencies. See (Householder, Wassermann, et al.  2020, 3.5) for a listing of different coordinator types. If a coordinator receives a report that is outside its own work scope or constituency, it should make an effort to route the report to a more suitable coordinator. The decisions in this section assume the report or vulnerability in question is in the work scope or constituency for the coordinator.
</div></details>

コーディネーターは、脆弱性管理エコシステム内のファシリテーターです。コーディネーターは問題の脆弱なコンポーネントを提供も展開もしないため、コーディネーターの決定はサプライヤーまたは展開者の決定とは異なります。このセクションでは、コーディネーターがSSVCを使用して独自の決定を行う方法の例として、CERT/CCの決定への窓を提供します。コーディネーターは非常に多様であり、SSVCの使用も同様に異なる可能性があります。コーディネーターは、構成員を支援するために、内部で使用しないSSVC決定ポイントに関する情報を収集して公開したい場合があります。さらに、コーディネーターは、意思決定に使用する情報の一部のみを公開できます。他の利害関係者の視点（サプライヤーと展開者）と一致して、SSVCは、コーディネーターが何らかの定義されたアクションを実行する優先順位を提供しますが、そのアクションを実行する方法は提供しません。コーディネーターの種類と脆弱性管理におけるそれらの促進行動の詳細については、（Householder、Wassermann、et al.2020）を参照してください。 CERT / CCがコーディネーターとしてSSVCに関して説明する2つの決定は、脆弱性レポートの最初のトリアージと、脆弱性に関する公開が必要かどうかです。最初の調整の決定は優先順位の決定ですが、デプロイヤーまたはサプライヤーによる優先順位付けと同じ値はありません。私たちの出版決定は、バイナリのyes/noです。これらの2つの決定は、脆弱性の調整全体ではありませんが、今後の作業のためにプロセスの詳細を残します。
コーディネーターが異なれば、スコープと構成員も異なります。 さまざまなコーディネータータイプのリストについては、（Householder、Wassermann、et al。2020、3.5）を参照してください。 コーディネーターは、自身の作業範囲または構成員の範囲外のレポートを受け取った場合、そのレポートをより適切なコーディネーターにルーティングするように努力する必要があります。 このセクションの決定は、問題のレポートまたは脆弱性がコーディネーターの作業範囲または構成員にあることを前提としています。

### Coordination Triage Decisions

<details><summary>原文</summary><div>

We take three priority levels in our decision about whether and how to coordinate a vulnerability (Householder, Wassermann, et al. 2020, 1.1) based on an incoming report:
- Decline—Do not act on the report. May take different forms, including ignoring the report as well as an acknowledgement to the reporter that we will not act and suggest the reporter to go to vendor or publish if unresponsive.
- Track—Receive information about the vulnerability and monitor for status changes but do not take any overt actions.
- Coordinate—Take action on the report. “Action” may include any one or more of: technical analysis, reproduction, notifying vendors, lead coordination (notify, communicate, and publish), publish only (amplify public message), advise only, secondary coordinator (assist another lead coordinator). See (Benetis et al. 2019) for additional vulnerability management services a coordinator may provide.
</div></details>

受け取ったレポートに基づいて、脆弱性を調整するかどうか、および調整する方法（Householder、Wassermann、et al。2020、1.1）について、3つの優先レベルを採用します。
- Decline レポートに基づいて行動しないでください。 レポートを無視することや、私たちが行動しないことをレポーターに認め、応答がない場合はベンダーに行くか公開することをレポーターに提案するなど、さまざまな形をとることがあります。
- Track 脆弱性に関する情報を受け取り、ステータスの変化を監視しますが、明白なアクションは実行しません。
- Coordinate レポートに対してアクションを実行します。 「アクション」には、テクニカル分析、複製、ベンダーへの通知、リードコーディネーション（通知、伝達、公開）、公開のみ（パブリックメッセージの増幅）、アドバイスのみ、セカンダリコーディネーター（別のリードコーディネーターの支援）のいずれか1つ以上が含まれます。 コーディネーターが提供する可能性のある追加の脆弱性管理サービスについては、（Benetis et al。2019）を参照してください。

### Coordinator Decision Points

<details><summary>原文</summary><div>

Our goal with the coordination decision is to base it on information that is available to the analyst when CERT/CC receives a vulnerability report. In addition to using some of the decision points in Likely Decision Points; coordination makes use of Utility and Public Safety Impact decision points. The coordination and publication decisions for CERT/CC are about the social and collaborative state of vulnerability management. To assess this, the decision involves five new decision points.
</div></details>

調整の決定に関する私たちの目標は、CERT/CCが脆弱性レポートを受け取ったときにアナリストが利用できる情報に基づいて調整することです。 可能性のある決定ポイントでいくつかの決定ポイントを使用することに加えて、 調整では、ユーティリティと公安への影響の決定ポイントを利用します。 CERT / CCの調整と公開の決定は、脆弱性管理の社会的および協調的な状態に関するものです。 これを評価するために、決定には5つの新しい決定ポイントが含まれます。


#### Report Public

<details><summary>原文</summary><div>

Is a viable report of the details of the vulnerability already publicly available?
- Yes
- No
</div></details>

脆弱性の詳細に関する実行可能なレポートはすでに公開されていますか？
- Yes
- No

#### Supplier Contacted

<details><summary>原文</summary><div>

Has the reporter made a good-faith effort to contact the supplier of the vulnerable component using a quality contact method?
- Yes
- No
A quality contact method is a publicly posted known good email address, public portal on vendor website, etc.
</div></details>

レポーターは、質の高い連絡方法を使用して、脆弱なコンポーネントのサプライヤーに連絡するために誠意を持って努力しましたか？
- Yes
- No
質の高い連絡方法は、公に投稿された既知の適切な電子メールアドレス、ベンダーのWebサイトの公開ポータルなどです。

#### Supplier Cardinality

<details><summary>原文</summary><div>

How many suppliers are responsible for the vulnerable component and its remediation or mitigation plan?
- One
- Multiple
</div></details>

脆弱なコンポーネントとその修復または緩和計画に責任を持つサプライヤーはいくつありますか？
- One
- Multiple

#### Supplier Engagement

<details><summary>原文</summary><div>

Is the supplier responding to the reporter’s contact effort and actively participating in the coordination
effort?
- Active
- Unresponsive
</div></details>

サプライヤーはレポーターの連絡作業に対応し、調整作業に積極的に参加していますか？
- Active
- Unresponsive

### Report Credibility

<details><summary>原文</summary><div>

Assessing the credibility of a report is complex, but the assessment must reach a conclusion of either:
- Credible
- Not credible
An analyst should start with a presumption of credibility and proceed toward disqualification. The reason for this is that, as a coordinator, occasionally doing a bit of extra work on a bad report is preferable to rejecting legitimate reports. This is essentially stating a preference for false positives over false negatives with respect to credibility determination.
The following subsections provide suggestive guidance on assessing credibility. There are no ironclad rules for this assessment, and other coordinators may find other guidance works for them. Credibility assessment topics include indicators for and against credibility, perspective, topic, and relationship to report scope.
</div></details>

レポートの信頼性の評価は複雑ですが、評価は次のいずれかの結論に達する必要があります。
- Credible
- Not credible

アナリストは、信頼性の推定から始めて、失格に向かって進む必要があります。 この理由は、コーディネーターとして、正当なレポートを拒否するよりも、悪いレポートに対して少し余分な作業を行う方が望ましい場合があるためです。 これは基本的に、信頼性の判断に関して、誤検知よりも誤検知を優先することを示しています。
次のサブセクションは、信頼性を評価するための示唆的なガイダンスを提供します。 この評価には確固たる規則はなく、他のコーディネーターが他のガイダンス作業を見つける可能性があります。 信頼性評価のトピックには、信頼性、視点、トピック、およびレポート範囲との関係に対する賛否両論の指標が含まれます。

<details><summary>原文</summary><div>

Credibility Indicators The credibility of a report is assessed by a balancing test. The indicators for or against are not commensurate, and so they cannot be put on a scoring scale, summed, and weighed.  A report may be treated as credible when either (1) the vendor confirms the existence of the vulnerability or (2) independent confirmation of the vulnerability by an analyst who is neither the reporter nor the vendor. If neither of these confirmations are available, then the value of the Report Credibility decision point depends on a balancing test among the following indicators.
</div></details>

信頼性指標レポートの信頼性は、バランステストによって評価されます。 賛成または反対の指標は釣り合っていないため、スコアリングスケールに配置したり、合計したり、重み付けしたりすることはできません。 （1）ベンダーが脆弱性の存在を確認するか、（2）レポーターでもベンダーでもないアナリストによる脆弱性の独立した確認のいずれかである場合、レポートは信頼できるものとして扱われる可能性があります。 これらの確認のいずれも利用できない場合、レポートの信頼性決定ポイントの値は、次の指標間のバランステストに依存します。

<details><summary>原文</summary><div>

Indicators for Credibility include:
- The report is specific about what is affected
- The report provides sufficient detail to reproduce the vulnerability.
- The report describes an attack scenario.
- The report suggests mitigations.
- The report includes proof-of-concept exploit code or steps to reproduce.
- Screenshots and videos, if provided, support the written text of the report and do not replace it.
- The report neither exaggerates nor understates the impact.
</div></details>

信頼性の指標は次のとおりです。
- レポートは、影響を受けるものについて具体的です
- レポートは、脆弱性を再現するのに十分な詳細を提供します。
- レポートには、攻撃シナリオが記載されています。
- レポートは緩和策を提案しています。
- レポートには、概念実証のエクスプロイトコードまたは再現手順が含まれています。
- スクリーンショットとビデオが提供されている場合は、レポートのテキストをサポートし、それを置き換えることはありません。
- レポートは、影響を誇張したり過小評価したりしていません。

<details><summary>原文</summary><div>

Indicators against Credibility include:
- The report is “spammy” or exploitative (for example, the report is an attempt to upsell the receiver on some product or service).
- The report is vague or ambiguous about which vendors, products, or versions are affected (for example, the report claims that all “cell phones” or “wifi” or “routers” are affected).
- The report is vague or ambiguous about the preconditions necessary to exploit the vulnerability.  • The report is vague or ambiguous about the impact if exploited.
- The report exaggerates the impact if exploited.
- The report makes extraordinary claims without correspondingly extraordinary evidence (for example, the report claims that exploitation could result in catastrophic damage to some critical system without a clear causal connection between the facts presented and the impacts claimed).  • The report is unclear about what the attacker gains by exploiting the vulnerability. What do they get that they didn’t already have? For example, an attacker with system privileges can already do lots of bad things, so a report that assumes system privileges as a precondition to exploitation needs to explain what else this gives the attacker.
- The report depends on preconditions that are extremely rare in practice, and lacks adequate evidence for why those preconditions might be expected to occur (for example, the vulnerability is only exposed in certain non-default configurations—unless there is evidence that a community of practice has established a norm of such a non-default setup).
- The report claims dire impact for a trivially found vulnerability. It is not impossible for this to occur, but most products and services that have been around for a while have already had their low-hanging fruit major vulnerabilities picked. One notable exception would be if the reporter applied a completely new method for finding vulnerabilities to discover the subject of the report.
- The report is rambling and is more about a narrative than describing the vulnerability. One description is that the report reads like a food recipe with the obligatory search engine optimization preamble.
- The reporter is known to have submitted low-quality reports in the past.
- The report conspicuously misuses technical terminology. This is evidence that the reporter may not understand what they are talking about.
- The analyst’s professional colleagues consider the report to be not credible.
- The report consists of mostly raw tool output. Fuzz testing outputs are not vulnerability reports.
- The report lacks sufficient detail for someone to reproduce the vulnerability.
- The report is just a link to a video or set of images, or lacks written detail while claiming “it’s all in the video”. Imagery should support a written description, not replace it.
- The report describes a bug with no discernible security impact.
- The report fails to describe an attack scenario, and none is obvious.  We considered adding poor grammar or spelling as an indicator of non-credibility. On further reflection, we do not recommend that poor grammar or spelling be used as an indicator of low report quality, as many reporters may not be native to the coordinator’s language. Poor grammar alone is not sufficient to dismiss a report as not credible. Even when poor grammar is accompanied by other indicators of non-credibility, those other indicators are sufficient to make the determination.
</div></details>

信頼性に相対する指標は次のとおりです。
- レポートは「スパム」または搾取的です（たとえば、レポートは、ある製品またはサービスで受信者をアップセルしようとする試みです）。
- レポートは、影響を受けるベンダー、製品、またはバージョンについてあいまいまたはあいまいです（たとえば、レポートには、すべての「携帯電話」、「wifi」、または「ルーター」が影響を受けると記載されています）。
- レポートは、脆弱性を悪用するために必要な前提条件についてあいまいまたはあいまいです。 •レポートは、悪用された場合の影響についてあいまいまたはあいまいです。
- レポートは、悪用された場合の影響を誇張しています。
- レポートは、対応する異常な証拠なしに異常な主張をします（たとえば、報告は、提示された事実と主張された影響との明確な因果関係なしに、悪用がいくつかの重要なシステムに壊滅的な損害をもたらす可能性があると主張します）。 •レポートは、攻撃者が脆弱性を悪用することによって何を得るかについて不明確です。彼らはまだ持っていなかったものを何を得ますか？たとえば、システム特権を持つ攻撃者はすでに多くの悪いことをする可能性があるため、悪用の前提条件としてシステム特権を想定しているレポートでは、これが攻撃者に他に何を与えるかを説明する必要があります。
- レポートは、実際には非常にまれな前提条件に依存しており、これらの前提条件が発生すると予想される理由についての十分な証拠がありません（たとえば、脆弱性は、特定のデフォルト以外の構成でのみ公開されます。ただし、実践は、そのようなデフォルト以外の設定の規範を確立しました）。
- レポートは、些細なことに発見された脆弱性に対する悲惨な影響を主張しています。これが発生することは不可能ではありませんが、しばらくの間存在していたほとんどの製品とサービスは、すでにそれらのぶら下がっている果物の主要な脆弱性を選んでいます。注目すべき例外の1つは、レポーターが脆弱性を見つけるためのまったく新しい方法を適用して、レポートの主題を発見した場合です。
- レポートはとりとめのないものであり、脆弱性を説明するというよりも物語に関するものです。 1つの説明は、レポートが必須の検索エンジン最適化プリアンブルを備えた食品レシピのように読み取られることです。
- 記者は過去に質の低い報告を提出したことが知られています。
- レポートは、技術用語を著しく誤用しています。これは、記者が彼らが話していることを理解していない可能性があるという証拠です。
- アナリストの専門家の同僚は、レポートが信頼できないと考えています。
- レポートは、主に未加工のツール出力で構成されています。ファズテストの出力は脆弱性レポートではありません。
- レポートには、誰かが脆弱性を再現するための十分な詳細が欠けています。
- レポートは、ビデオまたは一連の画像への単なるリンクであるか、「すべてがビデオに含まれている」と主張している間、詳細が書かれていません。画像は、説明を置き換えるのではなく、書面による説明をサポートする必要があります。
- レポートには、セキュリティへの影響が認識できないバグが記載されています。
- レポートは攻撃シナリオを説明しておらず、明らかなものはありません。信頼性の欠如の指標として、貧弱な文法やスペルを追加することを検討しました。さらに考えてみると、多くの記者はコーディネーターの言語にネイティブではない可能性があるため、不十分な文法やスペルをレポート品質の低さの指標として使用することはお勧めしません。文法が不十分なだけでは、信頼できないとしてレポートを却下するのに十分ではありません。貧弱な文法が信頼性のない他の指標を伴う場合でも、それらの他の指標は決定を下すのに十分です。

<details><summary>原文</summary><div>

Credibility of what to whom SSVC is interested in the coordinating analyst’s assessment of the credibility of a report.
This is separate from the fact that a reporter probably reports something because they believe the report is credible.
The analyst should assess the credibility of the report of the vulnerability, not the claims of the impact of the vulnerability.
A report may be credible in terms of the fact of the vulnerability’s existence even if the stated impacts are inaccurate.
However, the more extreme the stated impacts are, the more skepticism is necessary.
For this reason, “exaggerating the impact if exploited” is an indicator against credibility.
Furthermore, a report may be factual but not identify any security implications; such reports are bug reports, not vulnerability reports, and are considered out of scope.
A coordinator also has a scope defined by their specific constituency and mission.
A report can be entirely credible yet remain out of scope for your coordination practice.
Decide what to do about out of scope reports separately, before the vulnerability coordination triage decision begins.
If a report arrives and would be out of scope even if true, there will be no need to proceed with judging its credibility.
</div></details>

レポートの信頼性に関するアナリストの評価を調整することこそがSSVCが関心を持っているものとしての信頼性。
これは、レポートが信頼できると信じているために、報告者が何かを報告するという事実とは別のものです。
アナリストは、脆弱性の影響の主張ではなく、脆弱性のレポートの信頼性を評価する必要があります。
記載されている影響が不正確であっても、脆弱性が存在するという事実に関して、レポートは信頼できる場合があります。
ただし、記載されている影響が極端であるほど、懐疑的な見方が必要になります。
このため、「悪用された場合の影響を誇張する」ことは、信頼性に対する指標です。
さらに、レポートは事実である可能性がありますが、セキュリティへの影響を特定するものではありません。このようなレポートはバグレポートであり、脆弱性レポートではなく、範囲外と見なされます。
コーディネーターには、特定の構成員と使命によって定義される範囲もあります。
レポートは完全に信頼できるものでありながら、調整の実践の範囲外のままである可​​能性があります。
脆弱性調整トリアージの決定を開始する前に、範囲外のレポートを個別に処理することを決定します。
報告書が届き、たとえ真実であっても範囲外となる場合は、その信頼性の判断を進める必要はありません。

### Coordination Triage Decision Process

<details><summary>原文</summary><div>

The decision tree for reaching a Decision involves seven decision points. The first two function as gating questions:
- If a report is already public, then CERT/CC will decline the case unless there are multiple suppliers, super effective Utility , and significant Public Safety Impact.
- If no suppliers have been contacted, then CERT/CC will decline the case unless there are multiple suppliers, super effective Utility , and significant Public Safety Impact.

In the second case, CERT/CC may encourage the reporter to contact the supplier and submit a new case request if the supplier is unresponsive.

These two sets of exceptional circumstances mean that the seven decision points involved in the coordination triage tree can be compressed slightly, as the tree shows. This tree’s information is available as either a CSV or PDF
</div></details>

決定に到達するための決定木には、7つの決定ポイントが含まれます。 最初の2つはゲーティング質問として機能します。※  
※gating 
- レポートがすでに公開されている場合、CERT/CCは、複数のサプライヤー、非常に効果的なユーティリティ、および重大な公安への影響がない限り、ケースを拒否します。
- サプライヤーに連絡がない場合、CERT/CCは、複数のサプライヤー、非常に効果的なユーティリティ、および重大な公安への影響がない限り、ケースを拒否します。

2番目のケースでは、CERT / CCは、サプライヤーが応答しない場合、レポーターにサプライヤーに連絡し、新しいケースリクエストを提出するように勧めることがあります。

これらの2セットの例外的な状況は、ツリーが示すように、調整トリアージツリーに含まれる7つの決定ポイントをわずかに圧縮できることを意味します。 このツリーの情報は、CSVまたはPDFのいずれかで入手できます
### Publication Decision

<details><summary>原文</summary><div>

A coordinator often has to decide when or whether to publish information about a vulnerability.
A supplier also makes a decision about publicity—releasing information about a remediation or mitigation could be viewed as a kind of publication decision.
While the context of publication is different for coordinators, a supplier may find some use in a publication decision if they need to decide whether to publish before a mitigation or remediation is available.
However, that is not the intended use case; this section describes how a coordinator might decide to publish information about a vulnerability.
The publication decision is always a decision at a point in time.
As discussed in Guidance on Communicating Results, a SSVC decision may change over time as the inputs to that decision change.
A decision to publish cannot be revoked, since the publication is likely to be archived or at least remembered.
However, a decision to not publish is a decision not to publish at the time the decision was made.
It is not a decision never to publish in the future.
One benefit of encoding the decision process in SSVC is the analysts can all agree on what new information would change the decision and prioritize maintaining awarenss of just those decision points.
This section is based on CERT/CC policy choices.
Two points where this clearly influences the publication decision are embargo periods and scope.
As a matter of policy, CERT/CC will support an embargo from the public of information about a vulnerability through its choice not to publish that information while a number of conditions hold:

- A negotiated embargo timer has not expired. The CERT/CC default embargo period is 45 days.
- Other exceptions have not been met, including active exploitation of the vulnerability in the wild or other public discussion of the vulnerability details.
Regardless, the decision described in this section assumes the embargo period is over, one way or another.
The second point is related to the Coordination Triage Decisions and the status of the vulnerability.
CERT/CC only expects to publish about vulnerabilities with a coordinate status.
While an issue that is tracked or declined may be reevaluated at a later date and status changed to coordinate, unless that happens we would not publish about the vulnerability.
Other organizations, such as NVD, would have different publication criteria and may want to include decision points or the decision itself from the Coordination Triage Decisions in their publication decision.

In addition to the two decision points defined in this section, the publication decision uses the Exploitation
decision point.
</div></details>

コーディネーターは、脆弱性に関する情報をいつ公開するか、公開するかどうかを決定しなければならないことがよくあります。
サプライヤーはまた、宣伝について決定を下します。改善または緩和に関する情報を公開することは、一種の公開決定と見なすことができます。
コーディネーターによって公開のコンテキストは異なりますが、緩和策または修復が利用可能になる前に公開するかどうかを決定する必要がある場合、サプライヤーは公開の決定に何らかの用途を見つけることがあります。
ただし、これは意図されたユースケースではありません。このセクションでは、コーディネーターが脆弱性に関する情報を公開することを決定する方法について説明します。
公開の決定は、常にある時点での決定です。
結果の伝達に関するガイダンスで説明されているように、SSVCの決定は、その決定への入力が変化するにつれて、時間の経過とともに変化する可能性があります。
公開はアーカイブされるか、少なくとも記憶される可能性が高いため、公開の決定を取り消すことはできません。
ただし、公開しないという決定は、決定がなされた時点で公開しないという決定です。
将来公開しないという決定ではありません。
SSVCで意思決定プロセスをエンコードすることの利点の1つは、アナリスト全員が、どの新しい情報が意思決定を変更するかについて合意し、それらの意思決定ポイントのみの認識を維持することを優先できることです。
このセクションは、CERT/CCポリシーの選択に基づいています。
これが出版決定に明らかに影響を与える2つのポイントは、禁輸期間と範囲です。
ポリシーの問題として、CERT / CCは、脆弱性に関する情報の公開を、いくつかの条件が満たされている間は公開しないという選択を通じて、一般からの禁止をサポートします。

- ネゴシエートされた禁輸タイマーの期限が切れていません。 CERT/CCのデフォルトの禁止期間は45日です。
- 他の例外は満たされていません。これには、実際の脆弱性の積極的な悪用や、脆弱性の詳細に関するその他の公開討論が含まれます。
とにかく、このセクションで説明されている決定は、何らかの形で禁輸期間が終了したことを前提としています。
2番目のポイントは、調整トリアージの決定と脆弱性のステータスに関連しています。
CERT / CCは、調整ステータスを持つ脆弱性についてのみ公開することを期待しています。
追跡または拒否された問題は後日再評価され、ステータスが調整のために変更される可能性がありますが、それが発生しない限り、脆弱性については公開しません。
NVDなどの他の組織では、公開基準が異なり、公開決定に決定ポイントまたは調整トリアージ決定からの決定自体を含めることができます。

このセクションで定義されている2つの決定ポイントに加えて、公開決定では悪用決定ポイントが使用されます。

#### Public Value Added

<details><summary>原文</summary><div>

This decision point asks how much value a publication from the coordinator would benefit the broader community.
The value is based on the state of existing public information about the vulnerablity.

- Precedence—the publication would be the first publicly available, or be coincident with the first publicly available.
- Ampliative—amplifies and/or augments the existing public information about the vulnerability, for example, adds additional detail, addresses or corrects errors in other public information, draws further attention to the vulnerability, etc.
- Limited—minimal value added to the existing public information because existing information is already high quality and in multiple outlets.

The intent of the definition is that one rarely if ever transitions from limited to ampliative or ampliative to precedence
A vulnerability could transition from precedence to ampliative and ampliative to limited
That is, Public Value Added should only be downgraded through future iterations or re-evaluations
This directionality is because once other organizations make something public, they cannot effectively un-publish it (it’ll be recorded and people will know about it, even if they take down a webpage)
The rare case where Public Value Added increases would be if an organization published viable information, but then published additional misleading or obscuring information at a later time
Then one might go from limited to ampliative in the interest of pointing to the better information
</div></details>

この決定ポイントは、コーディネーターからの出版物がより広いコミュニティにどれだけの価値をもたらすかを尋ねます。
この値は、脆弱性に関する既存の公開情報の状態に基づいています。

- 優先順位—出版物は最初に公開されるか、最初に公開されるものと一致します。
- 拡張性—脆弱性に関する既存の公開情報を増幅および/または拡張します。たとえば、詳細を追加したり、他の公開情報のエラーに対処または修正したり、脆弱性にさらに注意を向けたりします。
- 限定的—既存の情報はすでに高品質で複数の販売店にあるため、既存の公開情報に付加価値が最小限に抑えられます。

定義の目的は、限定から増幅、または増幅から優先に移行することはめったにないということです。
脆弱性は、優先順位から増幅に移行し、増幅から制限に移行する可能性があります
つまり、パブリックバリューアディッドは、将来の反復または再評価によってのみダウングレードする必要があります
この方向性は、他の組織が何かを公開すると、それを効果的に非公開にすることができないためです（ウェブページを削除しても、記録され、人々はそれについて知ることができます）
公共の付加価値が増加するまれなケースは、組織が実行可能な情報を公開したが、後で追加の誤解を招く情報やあいまいな情報を公開した場合です。
次に、より良い情報を指すために、限定的なものから増幅的なものに移行する可能性があります

#### Supplier Involvement

<details><summary>原文</summary><div>

This decision point accounts for the state of the supplier’s work on addressing the vulnerability.
- Fix Ready—the supplier has provided a patch or fix
- Cooperative—the supplier is actively generating a patch or fix; they may or may not have provided a mitigation or work-around in the mean time.
- Uncooperative/Unresponsive—the supplier has not responded, declined to generate a remediation, or no longer exists.
</div></details>

この決定ポイントは、脆弱性に対処するためのサプライヤーの作業の状態を説明します。
- Fix Ready-サプライヤがパッチまたは修正を提供しました
- Cooperative-サプライヤはパッチまたは修正を積極的に生成しています。 その間に、緩和策または回避策を提供した場合と提供しなかった場合があります。
- Uncooperative/Unresponsive-サプライヤが応答していないか、修復の生成を拒否したか、または存在しなくなりました。

## Prioritization

<details><summary>原文</summary><div>

Given a specific stakeholder decision and set of useful decision points, we are now in a position to combine
them into a comprehensive set of decisions about the priority with which to act. The definition of choices
can take a logical form, such as:
• IF
• (Exploitation IS PoC) AND
• (Exposure IS controlled) AND
• (Utility IS laborious) AND
• (Well-being and Mission Impact IS medium)
• THEN priority is scheduled.
This logical statement is captured in line 50 of the deployer .csv file.
There are different formats for capturing these prioritization decisions depending on how and where they
are going to be used. In this paper, we primarily represent a full set of guidance on how one stakeholder
will make a decision as a decision tree. This section presents example trees for each stakeholder: supplier,
deployer, and coordinator. This section also provides some guidance on how to construct and customize a
decision tree and gather evidence to make decisions. How this decision information might be stored or
communicated is the topic of subsections on Asset Management and Communication.

Figure 1: Suggested Supplier Tree
</div></details>

特定の利害関係者の決定と一連の有用な決定ポイントを考えると、私たちは今、組み合わせる立場にあります
それらを、行動する優先順位に関する包括的な一連の決定にまとめます。選択肢の定義
次のような論理形式をとることができます。
-  IF
- （エクスプロイトはPoCです）AND
- （露出は制御されます）AND
- （ユーティリティは面倒です）そして
- （ウェルビーイングとミッションインパクトは中程度）
- THEN 優先順位がスケジュールされます。
この論理ステートメントは、デプロイヤーの.csvファイルの50行目にキャプチャされています。
これらの優先順位の決定をキャプチャするための形式は、方法と場所に応じて異なります。
使用されます。このペーパーでは、主に1人の利害関係者がどのように行うかについてのガイダンスの完全なセットを表します
決定木として決定を下します。このセクションでは、各利害関係者のツリーの例を示します。
デプロイヤー、およびコーディネーター。このセクションでは、を構築およびカスタマイズする方法に関するガイダンスも提供します。
決定木と証拠を収集して決定を下します。この決定情報の保存方法または
伝達されるのは、資産管理と伝達に関するサブセクションのトピックです。

![fig1](https://user-images.githubusercontent.com/39690536/163165633-c9b33da6-8aac-455c-adcf-b2ab59bb3c30.jpg)
Figure 1: Suggested Supplier Tree

### Supplier Tree

<details><summary>原文</summary><div>

The example supplier tree PDF shows the proposed prioritization decision tree for the supplier. Both
supplier and deployer trees use the above decision point definitions. Each tree is a compact way of
expressing assertions or hypotheses about the relative priority of different situations. Each tree organizes
how we propose a stakeholder should treat these situations. Rectangles are decision points, and triangles
represent outcomes. The values for each decision point are different, as described above. Outcomes are
priority decisions (defer, scheduled, out-of-cycle, immediate); outcome triangles are color coded:
- Defer = gray with green outline
- Scheduled = yellow
- Out-of-Cycle = orange
- Immediate = red with black outline
</div></details>

サプライヤツリーPDFの例は、サプライヤに対して提案された優先順位決定ツリーを示しています。 両方
サプライヤツリーとデプロイヤツリーは、上記の決定ポイントの定義を使用します。 各ツリーはコンパクトな方法です
さまざまな状況の相対的な優先順位に関する主張または仮説を表現する。 各ツリーは整理します
利害関係者をどのように提案するかは、これらの状況を処理する必要があります。 長方形は決定点であり、三角形は
結果を表します。 上記のように、各決定ポイントの値は異なります。 結果は
優先順位の決定（延期、スケジュール、サイクル外、即時）; 結果の三角形は色分けされています：
- Defer = 灰色と緑色の輪郭
- Scheduled =黄色
- Out-of-Cycle =オレンジ
- Immediate =赤と黒の輪郭

### Deployer Tree

<details><summary>原文</summary><div>

The example deployer tree PDF is depicted below.

Figure 2: Suggested Deployer Tree
</div></details>

デプロイヤの木のPDFは下記の通り表現されます
![fig2](https://user-images.githubusercontent.com/39690536/163165733-c0f470b4-a8bb-4e14-8b59-227bd7a65f86.jpg)

表2: デプロイヤ木の提案


### Coordinator trees

<details><summary>原文</summary><div>

As described in Decisions During Vulnerability Coordination, a coordination stakeholder usually makes separate triage and publication decisions.
Each have trees presented below.
</div></details>

脆弱性調整中の決定で説明されているように、調整の利害関係者は通常、トリアージと公開の決定を別々に行います。
それぞれの下に木があります。

#### Triage decision tree

<details><summary>原文</summary><div>
This tree is a suggestion in that CERT/CC believes it works for us.
Other coordinators should consider customizing the tree to their needs, as described in Tree Construction and Customization Guidance.
</div></details>

この木は、CERT/CCが私たちのために機能すると信じているという点での提案です。
他のコーディネーターは、ツリーの構築とカスタマイズのガイダンスで説明されているように、ニーズに合わせてツリーをカスタマイズすることを検討する必要があります。

#### Publication decision tree

<details><summary>原文</summary><div>
Suggested decision values for this decision are available in CSV and PDF formats.
</div></details>

この決定の推奨決定値は、CSVおよびPDF形式で入手できます。

#### Tree Construction and Customization Guidance

<details><summary>原文</summary><div>

Stakeholders are encouraged to customize the SSVC decision process to their needs.
Indeed, the first part of SSVC stands for "stakeholder-specific."
However, certain parts of SSVC are more amenable to customization than others.
In this section, we’ll cover what a stakeholder should leave static, what we imagine customization looks like, and some advice on building a usable and manageable decision tree based on our experience so far.

We suggest that the decision points, their definitions, and the decision values should not be customized.
Different vulnerability management teams inevitably think of topics such as Utility to the adversary in slightly different ways.
However, a key contribution of SSVC is enabling different teams to communicate about their decision process.
In order to clearly communicate differences in the process, the decision points that factor into the process need to be the same between different teams.
A stakeholder community may come together and, if there is broad consensus, add or change decision points.

Which decision points are involved in a vulnerability management team’s decision and the priority label for each resulting situation are, for all intents and purposes, totally at the discretion of the team.
We have provided some examples for different stakeholder communities here.
What decision points a team considers reflects what it cares about and the risks prioritizes.
Different teams may legitimately prioritize different objectives.
It should be easier for teams to discuss and communicate such differences if the definitions of the decision points remain static.
The other aspect of risk management that SSVC allows a team to customize is its risk appetite or risk tolerance.

A team’s risk appetite is reflected directly by the priority labels for each combination of decision values.
For example, a vulnerability with no or minor Public Safety Impact, total Technical Impact, and efficient Utility might be handled with scheduled priority by one team and out-of-cycle priority by another.
As long as each team has documented this choice and is consistent in its own application of its own choice, the two teams can legitimately have different appetites for vulnerability risk.
SSVC enables teams with such different risk appetites to discuss and communicate precisely the circumstances where they differ.

When doing the detailed risk management work of creating or modifying a tree, we recommend working from text files with one line or row for each unique combination of decision values.
For examples, see SSVC/data.
An important benefit, in our experience, is that it is easier to identify a question by saying “I’m unsure about row 16” than anything else we have thought of so far.
Once the humans agree on the decision tree, it can be converted to a JSON schema for easier machine-readable communication, following the provided SSVC provision JSON schema.


Figure 3: Suggested Coordinator Triage Tree

Figure 4: Suggested Coordinator Publication Tree

</div></details>

利害関係者は、SSVCの意思決定プロセスをニーズに合わせてカスタマイズすることをお勧めします。
実際、SSVCの最初の部分は、「利害関係者固有」の略です。
ただし、SSVCの特定の部分は、他の部分よりもカスタマイズに適しています。
このセクションでは、利害関係者が静的なままにしておくべきこと、カスタマイズがどのように見えるか、およびこれまでの経験に基づいて使用可能で管理しやすい意思決定ツリーを構築するためのアドバイスについて説明します。

決定ポイント、それらの定義、および決定値はカスタマイズしないことをお勧めします。
さまざまな脆弱性管理チームは、必然的に、敵対者へのユーティリティなどのトピックをわずかに異なる方法で考えます。
ただし、SSVCの重要な貢献は、さまざまなチームが意思決定プロセスについてコミュニケーションできるようにすることです。
プロセスの違いを明確に伝えるために、プロセスに影響を与える決定ポイントは、異なるチーム間で同じである必要があります。
利害関係者のコミュニティが集まり、幅広いコンセンサスがある場合は、決定ポイントを追加または変更することができます。

脆弱性管理チームの決定に関与する決定ポイントと、結果として生じる各状況の優先順位ラベルは、すべての意図と目的において、完全にチームの裁量に委ねられています。
ここでは、さまざまな利害関係者コミュニティの例をいくつか示しました。
チームが検討する決定ポイントは、チームが気にかけていることとリスクが優先することを反映しています。
異なるチームは、異なる目的を合法的に優先する場合があります。
決定ポイントの定義が静的なままである場合、チームがそのような違いについて話し合い、伝達するのが容易になるはずです。
SSVCがチームにカスタマイズを許可するリスク管理のもう1つの側面は、リスク食欲またはリスク許容度です。

チームのリスクアペタイトは、意思決定値の各組み合わせの優先順位ラベルに直接反映されます。
たとえば、公安への影響がない、または軽微な脆弱性、全体的な技術的影響、および効率的なユーティリティは、あるチームがスケジュールされた優先度で、別のチームがサイクル外の優先度で処理される場合があります。
各チームがこの選択を文書化し、独自の選択の独自のアプリケーションで一貫している限り、2つのチームは脆弱性リスクに対して合法的に異なる欲求を持つことができます。
SSVCを使用すると、リスクの欲求が異なるチームが、異なる状況について正確に話し合い、伝達することができます。

ツリーを作成または変更する詳細なリスク管理作業を行う場合は、決定値の一意の組み合わせごとに1行または1行のテキストファイルから作業することをお勧めします。
例については、SSVC/dataを参照してください。
私たちの経験では、これまで考えてきたどの方法よりも、「16行目がわからない」と言って質問を特定しやすいという重要な利点があります。
人間が決定木に同意すると、提供されたSSVCプロビジョニングJSONスキーマに従って、機械で読み取り可能な通信を容易にするために、決定木をJSONスキーマに変換できます。

![fig3](https://user-images.githubusercontent.com/39690536/163165849-c32493e0-acd6-4d5d-b82c-ea6e955c14a6.jpg)
Figure 3: Suggested Coordinator Triage Tree

![fig4](https://user-images.githubusercontent.com/39690536/163165942-ad6073c3-81c1-449d-a816-c54d7a61573e.jpg)
Figure 4: Suggested Coordinator Publication Tree


<details><summary>原文</summary><div>

Once the decision points are selected and the prioritization labels agreed upon, it is convenient to be able to visually compress the text file by displaying it as a decision tree.
Making the decision process accessible has a lot of benefits.
Unfortunately, it also makes it a bit too easy to overcomplicate the decision.
The academic literature surrounding the measurement of decision tree quality is primarily concerned with measuring classification errors given a particular tree and a labeled data set.
In our case, we are not attempting to fit a tree to data.
Rather, we are interested in producing usable trees that minimize extraneous effort.
To that end, we briefly examine the qualities for which decision tree measurement is suitable.

Decision tree construction methods must address four significant concerns: feature selection, feature type, overfitting, and parsimony.

Feature selection is perhaps the most important consideration for SSVC, because it directly affects the information gathering requirements placed on the analyst attempting to use the tree.
Each decision point in SSVC is a feature.

The SSVC version 1 ~applier~ deployer tree had 225 rows when we wrote it out in long text form.
It only has four outcomes to differentiate between.
Thus, on average that decision process treats one situation (combination of decision values) as equivalent to 65 other situations.
If nothing else, this means analysts are spending time gathering evidence to make fine distinctions that are not used in the final decision.
The added details also make it harder for the decision process to accurately manage the risks in question.
This difficulty arises because more variance and complexity there is in the decision increases the possibility of errors in the decision process itself.
Regarding feature types, all of the features included in SSVC version 2 can be considered ordinal data.
That is, while they can be ordered (e.g. ,for Exploitation, active is greater than poc is greater than none), they can not be compared via subtraction or division (active - poc = nonsense).
The use of ordinal features is a key assumption behind our use of the parsimony analysis that follows.

When decision trees are used in a machine learning context, overfitting increases tree complexity by incorporating the noise in the training data set into the decision points in a tree.
In our case, our “data” is just the set of outcomes as decided by humans, so overfitting is less of a concern, assuming the feature selection has been done with care.

Parsimony is, in essence, Occam’s Razor applied to tree selection.
Given the choice between two trees that have identical outputs, one should choose the tree with fewer decisions.
One way to evaluate the parsimony of a tree is by applying the concept of feature importance to ensure that each feature is contributing adequately to the result.
While there are a few ways to compute feature importance, the one we found most useful is permutation importance.
Permutation importance can be calculated on a candidate tree to highlight potential issues.
It works by randomly shuffling the values for each feature individually and comparing a fitness metric on the shuffled tree to the original.
The change in fitness is taken to be the importance of the feature that was shuffled.
Permutation importance is usually given as a number in the interval \[0,1\].
Python’s scikit-learn provides a permutation importance method, which we used to evaluate our trees.

Interpreting the results of a permutation importance computation on a tree involves nuance, but one rule we can state is this: any feature with a computed permutation importance of zero can be eliminated from the tree without losing any relevant information.
When all of the permutation importance scores for all features are relatively equal, that is an indication that each feature is approximately equally relevant to the decision.

More likely, however, is that some subset of features will be of relatively equal importance, and one might be of considerably lower importance (yet not zero).
In this case, the lowest importance feature should be considered for refinement or elimination.
It is possible that adjusting the definition of a feature or its available values (whether redefining, adding, or removing options) could increase its importance.
Reasons to retain a low-importance feature include:
- the feature is relevant to a small set of important circumstances that a tree without the feature would otherwise be unable to discriminate
- the effort required to determine the correct value for the feature is relatively small, for example information that might be collected automatically
- the feature enables other features to be defined more clearly Features that meet none of the above criteria may be good candidates for elimination.

Customizing a tree by changing the outcome priority labels can also affect the importance of a feature.
This sort of customization is often the simplest way to adjust the importance of a feature.

While there is no hard and fast rule for when a tree is too big, we suggest that if all of your outcomes are associated with more than 15 situations (unique combinations of decision values), you would benefit from asking whether your analysts actually use all the information they would be gathering.
Thus, 60 unique combinations of decision values is the point at which a decision tree with four distinct outcomes is, on average, potentially too big.

SSVC trees should be identifiable by name and version.
A tree name is simply a short descriptive label for the tree derived from the stakeholder and/or function the tree is intended for.
Tree versions are expected to share the major and minor version numbers with the SSVC version in which their decision points are defined.
Revisions should increment the patch number.
For example: “Applier Tree v1.1.0” would be the identity of the version of the Applier Tree as published in version 1.1 of SSVC.
“Coordinator Publish Tree v2.0.3” would be the identity of a future revision of the Coordinator Publish Tree as described in this document.
The terms “major”, “minor”, and “patch” with respect to version numbering are intended to be consistent with Semantic Versioning 2.0.0.
</div></details>

決定点が選択され、優先順位ラベルが合意されると、テキストファイルを決定木として表示することで視覚的に圧縮できるので便利です。
意思決定プロセスにアクセスできるようにすることには、多くの利点があります。
残念ながら、それはまた、決定を過度に複雑にすることを少し簡単にします。
決定木の品質の測定を取り巻く学術文献は、主に、特定のツリーとラベル付けされたデータセットが与えられた場合の分類エラーの測定に関係しています。
私たちの場合、ツリーをデータに適合させようとはしていません。
むしろ、余分な労力を最小限に抑える使用可能なツリーを作成することに関心があります。
そのために、決定木の測定が適している品質を簡単に調べます。

決定木の構築方法は、特徴選択、特徴タイプ、過剰適合、および節約という4つの重要な懸念に対処する必要があります。

特徴選択は、ツリーを使用しようとするアナリストに課せられる情報収集要件に直接影響するため、SSVCにとっておそらく最も重要な考慮事項です。
SSVCの各決定点は機能です。

SSVCバージョン1の~アプライヤ~デプロイヤーツリーは、長いテキスト形式で書き出したときに225行でした。
区別する結果は4つだけです。
したがって、平均して、その決定プロセスは1つの状況（決定値の組み合わせ）を他の65の状況と同等に扱います。
他に何もないとしても、これは、アナリストが最終決定で使用されない細かい区別をするために証拠を収集することに時間を費やしていることを意味します。
追加された詳細により、意思決定プロセスが問題のリスクを正確に管理することも困難になります。
この困難は、意思決定に分散と複雑さが増すと、意思決定プロセス自体にエラーが発生する可能性が高くなるために発生します。
機能タイプに関しては、SSVCバージョン2に含まれるすべての機能は順序データと見なすことができます。
つまり、順序付けはできますが（たとえば、エクスプロイトの場合、アクティブはpocがなしよりも大きい）、減算または除算では比較できません（アクティブ-poc =ナンセンス）。
順序関数の使用は、以下の節約分析の使用の背後にある重要な仮定です。

決定木が機械学習のコンテキストで使用される場合、過剰適合は、トレーニングデータセットのノイズをツリーの決定点に組み込むことにより、ツリーの複雑さを増します。
私たちの場合、私たちの「データ」は人間が決定した結果のセットにすぎないため、特徴選択が慎重に行われていれば、過剰適合はそれほど問題になりません。

節約は、本質的に、オッカムの剃刀が木の選​​択に適用されます。※
同一の出力を持つ2つのツリーから選択する場合、決定が少ないツリーを選択する必要があります。
ツリーの節約を評価する1つの方法は、特徴の重要性の概念を適用して、各特徴が結果に適切に貢献していることを確認することです。
特徴の重要度を計算する方法はいくつかありますが、最も有用であることがわかったのは順列の重要度です。
順列の重要度は、潜在的な問題を強調するために候補ツリーで計算できます。
これは、各機能の値を個別にランダムにシャッフルし、シャッフルされたツリーのフィットネスメトリックを元のツリーと比較することで機能します。
フィットネスの変化は、シャッフルされた機能の重要性であると見なされます。
順列の重要度は通常、区間\[0,1\]の数値として与えられます。
Pythonのscikit-learnは、ツリーの評価に使用した順列重要度メソッドを提供します。  
※オッカムの剃刀...ある事柄を説明するためには、必要以上に多くを仮定するべきでないということ [参考](https://ja.wikipedia.org/wiki/%E3%82%AA%E3%83%83%E3%82%AB%E3%83%A0%E3%81%AE%E5%89%83%E5%88%80)

ツリーでの順列の重要度の計算結果の解釈には微妙な違いがありますが、1つのルールは次のとおりです。計算された順列の重要度がゼロの特徴は、関連情報を失うことなくツリーから削除できます。
すべての機能のすべての順列重要度スコアが比較的等しい場合、それは各機能が決定にほぼ等しく関連していることを示しています。

ただし、より可能性が高いのは、機能の一部のサブセットの重要性が比較的等しく、重要性がかなり低い（ただしゼロではない）可能性があることです。
この場合、最も重要度の低い機能を改良または排除することを検討する必要があります。
機能の定義またはその使用可能な値（オプションの再定義、追加、または削除）を調整すると、その重要性が高まる可能性があります。
重要度の低い機能を保持する理由は次のとおりです。
- 機能は、機能のないツリーが他の方法では識別できない重要な状況の小さなセットに関連しています
- 機能の正しい値を決定するために必要な労力は比較的少なく、たとえば、自動的に収集される可能性のある情報などです。
- この機能により、他の機能をより明確に定義できます。上記の基準のいずれにも当てはまらない機能は、削除の候補として適している可能性があります。

結果の優先度ラベルを変更してツリーをカスタマイズすることも、機能の重要性に影響を与える可能性があります。
この種のカスタマイズは、多くの場合、機能の重要性を調整するための最も簡単な方法です。

ツリーが大きすぎる場合の厳格なルールはありませんが、すべての結果が15を超える状況（決定値の一意の組み合わせ）に関連付けられている場合は、アナリストが実際にすべてを使用するかどうかを尋ねることでメリットが得られることをお勧めします。彼らが収集するであろう情報。
したがって、決定値の60の一意の組み合わせは、4つの異なる結果を持つ決定木が平均して大きすぎる可能性があるポイントです。

SSVCツリーは、名前とバージョンで識別できる必要があります。
ツリー名は、利害関係者および/またはツリーが対象とする機能から派生したツリーの短い説明ラベルです。
ツリーバージョンは、メジャーバージョン番号とマイナーバージョン番号を、決定ポイントが定義されているSSVCバージョンと共有することが期待されています。
リビジョンはパッチ番号をインクリメントする必要があります。
例：「ApplierTree v1.1.0」は、SSVCのバージョン1.1で公開されたApplierTreeのバージョンのIDになります。
「CoordinatorPublishTreev2.0.3」は、このドキュメントで説明されているCoordinatorPublishTreeの将来のリビジョンのIDになります。
バージョン番号付けに関する「メジャー」、「マイナー」、および「パッチ」という用語は、セマンティックバージョニング2.0.0と一致することを目的としています。

### Guidance for Evidence Gathering

<details><summary>原文</summary><div>

To answer each of these decision points, a supplier or deployer should, as much as possible, have a repeatable evidence collection and evaluation process.
However, we are proposing decisions for humans to make, so evidence collection and evaluation is not totally automatable.
That caveat notwithstanding, some automation is possible.
For example, whether exploitation modules are available in ExploitDB, Metasploit, or other sources is straightforward.
We hypothesize that searching Github and Pastebin for exploit code can be captured in a script.
A supplier or deployer could then define Exploitation to take the value of PoC if there are positive search results for a set of inputs derived from the CVE entry in at least one of these venues.
At least, for those vulnerabilities that are not “automatically” PoC-ready, such as on-path attackers for TLS or network replays.

Some of the decision points require a substantial upfront analysis effort to gather risk assessment or organizational data.
However, once gathered, this information can be efficiently reused across many vulnerabilities and only refreshed occasionally.
An obvious example of this is the mission impact decision point.
To answer this, a deployer must analyze their essential functions, how they interrelate, and how they are supported.
Exposure is similar; answering that decision point requires an asset inventory, adequate understanding of the network topology, and a view of the enforced security controls.
Independently operated scans, such as Shodan or Shadowserver, may play a role in evaluating exposure, but the entire exposure question cannot be reduced to a binary question of whether an organization’s assets appear in such databases.
Once the deployer has the situational awareness to understand MEFs or exposure, selecting the answer for each individual vulnerability is usually straightforward.
Stakeholders who use the prioritization method should consider releasing the priority with which they handled the vulnerability.
This disclosure has various benefits.
For example, if the supplier publishes a priority ranking, then deployers could consider that in their decision-making process.
One reasonable way to include it is to break ties for the deployer.
If a deployer has three “scheduled” vulnerabilities to remediate, they may address them in any order.
If two vulnerabilities were produced by the supplier as “scheduled” patches, and one was “out-of-cycle,” then the deployer may want to use that information to favor the latter.


In the case where no information is available or the organization has not yet matured its initial situational analysis, we can suggest something like defaults for some decision points.
If the deployer does not know their exposure, that means they do not know where the devices are or how they are controlled, so they should assume System Exposure is open.
If the decision maker knows nothing about the environment in which the device is used, we suggest assuming a major Safety Impact.
This position is conservative, but software is thoroughly embedded in daily life now, so we suggest that the decision maker provide evidence that no one’s well-being will suffer.
The reach of software exploits is no longer limited to a research network.
Similarly, with Mission Impact, the deployer should assume that the software is in use at the organization for a reason, and that it supports essential functions unless they have evidence otherwise.
With a total lack of information, assume support crippled as a default.
Exploitation needs no special default; if adequate searches are made for exploit code and none is found, the answer is none.
If nothing is known about Automatable, the safer answer to assume is yes.
Value Density should always be answerable; if the product is uncommon, it is probably diffuse.
The resulting decision set {none, open, efficient, medium} results in a scheduled patch application in our recommended deployer tree.
</div></details>

これらの決定ポイントのそれぞれに答えるために、サプライヤーまたは展開者は、可能な限り、反復可能な証拠収集および評価プロセスを持っている必要があります。
しかし、私たちは人間が下す決定を提案しているので、証拠の収集と評価は完全に自動化できるわけではありません。
その警告にもかかわらず、いくつかの自動化が可能です。
たとえば、エクスプロイトモジュールがExploitDB、Metasploit、またはその他のソースで利用可能かどうかは簡単です。
GithubとPastebinでエクスプロイトコードを検索すると、スクリプトでキャプチャできると仮定します。
サプライヤまたはデプロイヤは、これらの場所の少なくとも1つでCVEエントリから派生した一連の入力に対して肯定的な検索結果がある場合に、PoCの値を取得するようにExploitationを定義できます。
少なくとも、TLSやネットワークリプレイのパス上の攻撃者など、「自動的に」PoCに対応していない脆弱性については。

一部の決定ポイントでは、リスク評価または組織データを収集するために、かなりの事前分析作業が必要です。
ただし、一度収集されると、この情報は多くの脆弱性にわたって効率的に再利用でき、たまにしか更新されません。
この明らかな例は、ミッション影響の決定ポイントです。
これに答えるには、デプロイヤーは、それらの重要な機能、それらがどのように相互に関連し、どのようにサポートされているかを分析する必要があります。
露出も同様です。その決定ポイントに答えるには、資産インベントリ、ネットワークトポロジの十分な理解、および実施されたセキュリティ制御のビューが必要です。
ShodanやShadowserverなどの独立して運用されるスキャンは、エクスポージャーの評価に役割を果たす可能性がありますが、エクスポージャーの質問全体を、組織の資産がそのようなデータベースに表示されるかどうかの2つの質問に還元することはできません。
展開者がMEFまたはエクスポージャーを理解するための状況認識を持ったら、通常、個々の脆弱性ごとに答えを選択するのは簡単です。
優先順位付け方法を使用する利害関係者は、脆弱性を処理した優先順位を解放することを検討する必要があります。
この開示にはさまざまな利点があります。
たとえば、サプライヤが優先順位を公開している場合、展開者は意思決定プロセスでそれを考慮することができます。
これを含めるための合理的な方法の1つは、デプロイヤーの関係を断ち切ることです。
デプロイヤに修正すべき3つの「スケジュールされた」脆弱性がある場合、それらは任意の順序で対処できます。
2つの脆弱性が「スケジュールされた」パッチとしてサプライヤによって生成され、1つが「サイクル外」であった場合、デプロイヤはその情報を使用して後者を優先することができます。


情報が入手できない場合、または組織が最初の状況分析をまだ成熟させていない場合は、いくつかの決定ポイントのデフォルトのようなものを提案できます。
展開者がエクスポージャーを知らない場合、つまり、デバイスがどこにあるか、またはデバイスがどのように制御されているかがわからないため、システムエクスポージャーが開いていると想定する必要があります。
意思決定者がデバイスが使用される環境について何も知らない場合は、大きな安全上の影響を想定することをお勧めします。
この立場は保守的ですが、ソフトウェアは現在日常生活に完全に組み込まれているため、意思決定者は誰の幸福も損なわれないという証拠を提供することをお勧めします。
ソフトウェアエクスプロイトの範囲は、もはや研究ネットワークに限定されていません。
同様に、Mission Impactの場合、展開者は、ソフトウェアが何らかの理由で組織で使用されており、他に証拠がない限り、重要な機能をサポートしていると想定する必要があります。
情報がまったく不足しているため、デフォルトでサポートが機能しなくなったと想定します。
悪用には特別なデフォルトは必要ありません。エクスプロイトコードを適切に検索しても何も見つからない場合、答えは「none」です。
Automatableについて何も知られていない場合、より安全な答えは「yes」です。
価値密度は常に答えられるべきです。製品が珍しい場合、それはおそらく拡散しています。
結果として得られる決定セット{none, open, efficient, medium}は、推奨されるデプロイヤーツリーにスケジュールされたパッチアプリケーションをもたらします。

### Relationship to asset management


<details><summary>原文</summary><div>

Vulnerability management is a part of asset management.
SSVC can benefit from asset management practices and systems, particularly in regard to automating data collection and answers for some decision points.
SSVC depends on asset management to some extent, particularly for context on the cost and risk associated with changing or updating the asset.

Asset management can help automate the collection of the Mission Impact, Situated Safety Impact, and System Exposure decision points.
These decision points tend to apply per asset rather than per vulnerability.
Therefore, once each is assessed for each asset, it can be applied to each vulnerability that applies to that asset.
While the asset assessment should be reviewed occasionally for accuracy, storing this data in an asset management system should enable automated scoring of new vulnerabilities on these decision points for those assets.

Our method is for prioritizing vulnerabilities based on the risk stemming from exploitation.
There are other reasonable asset management considerations that may influence remediation timelines.
There are at least three aspects of asset management that may be important but are out of scope for SSVC.
First and most obvious is the transaction cost of conducting the mitigation or remediation.
System administrators are paid to develop or apply any remediations or mitigations, and there may be other transactional costs such as downtime for updates.
Second is the risk of the remediation or mitigation introducing a new error or vulnerability.
Regression testing is part of managing this type of risk.
Finally, there may be an operational cost of applying a remediation or mitigation, representing an ongoing change of functionality or increased overhead.
A decision maker could order work within one SSVC priority class (scheduled, out-of-cycle, etc.) based on these asset management considerations, for example.
Once the organization remediates or mitigates all the high-priority vulnerabilities, they can then focus on the medium-level vulnerabilities with the same effort spent on the high-priority ones.

Asset management and risk management also drive some of the up-front work an organization would need to do to gather some of the necessary information.
This situation is not new; an asset owner cannot prioritize which fixes to deploy to its assets if it does not have an accurate inventory of its assets.
The organization can pick its choice of tools; there are about 200 asset management tools on the market (Captera 2019).
Emerging standards like the Software Bill of Materials (SBOM) (Jump and Manion 2019) would likely reduce the burden on asset management, and organizations should prefer systems which make such information available.
If an organization does not have an asset management or risk management (see also Gathering Information About Mission Impact) plan and process in place, then SSVC provides some guidance as to what information is important to vulnerability management decisions and the organization should start capturing, storing, and managing.
</div></details>

脆弱性管理は資産管理の一部です。
SSVCは、特にデータ収集といくつかの決定ポイントの回答の自動化に関して、資産管理の実践とシステムから利益を得ることができます。
SSVCは、特に資産の変更または更新に関連するコストとリスクのコンテキストについて、ある程度資産管理に依存しています。

資産管理は、ミッションインパクト、状況安全インパクト、およびシステムエクスポージャーの決定ポイントの収集を自動化するのに役立ちます。
これらの決定ポイントは、脆弱性ごとではなく、資産ごとに適用される傾向があります。
したがって、各資産についてそれぞれが評価されると、その資産に適用される各脆弱性に適用できます。
資産評価の正確性を時々確認する必要がありますが、このデータを資産管理システムに保存すると、これらの資産のこれらの決定ポイントで新しい脆弱性の自動スコアリングが可能になります。

私たちの方法は、悪用に起因するリスクに基づいて脆弱性に優先順位を付けることです。
修復のタイムラインに影響を与える可能性のある他の合理的な資産管理の考慮事項があります。
資産管理には、重要かもしれないがSSVCの範囲外である少なくとも3つの側面があります。
最初で最も明白なのは、緩和または修復を実行するためのトランザクションコストです。
システム管理者は、修復または緩和策を開発または適用するために報酬を受け取り、更新のダウンタイムなどの他のトランザクションコストが発生する可能性があります。
2つ目は、新しいエラーまたは脆弱性を導入する修復または軽減のリスクです。
回帰テストは、このタイプのリスクの管理の一部です。
最後に、改善または緩和を適用するための運用コストが発生する可能性があります。これは、機能の継続的な変更またはオーバーヘッドの増加を表します。
意思決定者は、たとえば、これらの資産管理の考慮事項に基づいて、1つのSSVC優先度クラス（スケジュール済み、サイクル外など）内で作業を注文できます。
組織がすべての優先度の高い脆弱性を修正または軽減すると、優先度の高い脆弱性と同じ努力で中レベルの脆弱性に焦点を当てることができます。

資産管理とリスク管理は、必要な情報の一部を収集するために組織が行う必要のある先行作業の一部も推進します。
この状況は新しいものではありません。アセットの所有者は、アセットの正確なインベントリがない場合、アセットに展開する修正に優先順位を付けることができません。
組織はツールの選択肢を選ぶことができます。市場には約200の資産管理ツールがあります（Captera2019）。
Software Bill of Materials（SBOM）（Jump and Manion 2019）のような新しい標準は、資産管理の負担を軽減する可能性が高く、組織はそのような情報を利用できるようにするシステムを好む必要があります。
組織に資産管理またはリスク管理（ミッションの影響に関する情報の収集も参照）の計画とプロセスがない場合、SSVCは、脆弱性管理の決定に重要な情報に関するガイダンスを提供し、組織はキャプチャ、保存を開始する必要があります、および管理。

### Development Methodology

<details><summary>原文</summary><div>

For this tabletop refinement, we could not select a mathematically representative set of CVEs.
The goal was to select a handful of CVEs that would cover diverse types of vulnerabilities.
The CVEs that we used for our tabletop exercises are CVE-2017-8083, CVE-2019-2712, CVE-2014-5570, and CVE-2017-5753.

We discussed each one from the perspective of supplier and deployer.
We evaluated CVE-2017-8083 twice because our understanding and descriptions had changed materially after the first three CVEs (six evaluation exercises).
After we were satisfied that the decision trees were clearly defined and captured our intentions, we began the formal evaluation of the draft trees, which we describe in the next section.
</div></details>

この卓上での改良では、数学的に代表的なCVEのセットを選択できませんでした。
目標は、さまざまな種類の脆弱性をカバーする少数のCVEを選択することでした。
卓上演習に使用したCVEは、CVE-2017-8083、CVE-2019-2712、CVE-2014-5570、およびCVE-2017-5753です。

サプライヤーとデプロイヤーの観点からそれぞれについて話し合いました。
最初の3つのCVE（6つの評価演習）の後で理解と説明が大幅に変更されたため、CVE-2017-8083を2回評価しました。
決定木が明確に定義され、意図を捉えたことに満足した後、次のセクションで説明するドラフトツリーの正式な評価を開始しました。

## Guidance on Communicating Results

<details><summary>原文</summary><div>

There are many aspects of SSVC that two parties might want to communicate.
Not every stakeholder will use the decision points to make comparable decisions.
Suppliers and deployers make interdependent decisions, but the actions of one group are not strictly dependent on the other.
Recall that one reason for this is that SSVC is about prioritizing a vulnerability response action in general, not specifically applying a patch that a supplier produced.
Coordinators are particularly interested in facilitating communication because that is their core function.
This section handles three aspects of this challenge: formats for communicating SSVC, how to handle partial or incomplete information, and how to handle information that may change over time.

This section is about communicating SSVC information about a specific vulnerability.
Any stakeholder making a decision on allocating effort should have a decision tree with its decision points and possible values specified already.
Representation choices and Tree Construction and Customization Guidance discussed how SSVC uses a text file as the canonical form of a decision tree; the example trees can be found in SSVC/data.
This section discusses the situation where one stakeholder, usually a supplier or coordinator, wants to communicate some information about a specific vulnerability to other stakeholders or constituents.
</div></details>

SSVCには、2者が通信したい多くの側面があります。
すべての利害関係者が決定ポイントを使用して同等の決定を行うわけではありません。
サプライヤーと展開者は相互に依存する決定を下しますが、一方のグループの行動は他方に厳密に依存しているわけではありません。
この理由の1つは、SSVCが一般的に脆弱性対応アクションを優先することであり、サプライヤが作成したパッチを具体的に適用することではないことを思い出してください。
コーディネーターは、コミュニケーションを促進することに特に関心があります。それが彼らのコア機能だからです。
このセクションでは、この課題の3つの側面を扱います。SSVCを通信するための形式、部分的または不完全な情報を処理する方法、および時間の経過とともに変化する可能性のある情報を処理する方法です。

このセクションでは、特定の脆弱性に関するSSVC情報の伝達について説明します。
努力の割り当てを決定する利害関係者は、決定ポイントと可能な値がすでに指定された決定木を持っている必要があります。
表現の選択とツリーの構築およびカスタマイズのガイダンスでは、SSVCが決定木の標準形式としてテキストファイルをどのように使用するかについて説明しました。サンプルツリーはSSVC/dataにあります。
このセクションでは、1人の利害関係者（通常はサプライヤーまたはコーディネーター）が特定の脆弱性に関する情報を他の利害関係者または構成員に伝えたい状況について説明します。

### Communication Formats

<details><summary>原文</summary><div>

We recommend two structured communication formats, abbreviated and full.
The goal of the abbreviated format is to fill a need for providing identifying information about a vulnerability or decision in charts, graphs, and tables.
Therefore, the abbreviated format is not designed to stand alone.
The goal of the full format is to capture all the context and details about a decision or work item in a clear and machine-readable way.

Abbreviated Format SSVC abbreviated form borrows directly from the CVSS “vector string” notation.
Since the purpose of the abbreviated form is to provide labels for charts and graphics, it does not stand alone.
The basic format for SSVC is: SSVC/(version)/(decision point):(value)[/decision point:value[/decision point:value[...]]][/time]/
Where version is v2 if it is based on this current version of the SSVC.
The term decision point is one or two letters derived from the name of the decision point as follows:
- Start with the decision point name as given in Likely Decision Points and Relevant Data.
- Remove any text in parentheses (and the parentheses themselves).
- Remove the word “Impact” if it is part of the name.
- Create an initialism from remaining title-case words (ignore “of,” etc.), taking only the first two words.
- The first letter of the initialism is upper case; if there is a second letter, then it is lower case.
- Verify that the initialism is unique among decision points in the version of SSVC. If two initialisms collide, sort their source names equivalent to LC_ALL=C sort. The name that sorts first keeps the initialism for which there is a collision. Set the second letter of the initialism to the first character in the name that resolves the collision. If the names were Threat and Threshold, T would be Threat and Ts would be Threshold. We make an effort to design SSVC without such collisions.

For example, Technical Impact becomes T and Public Safety Impact becomes Ps.
The term value is a statement of the value or possible values of the decision point that precedes it and to which it is connected by a colon (:).
Similar to decision point, value should be made up of one or two letters derived from the name of the decision value in the section for its associated decision point.
For example MEF support crippled becomes Ms and efficient becomes E.
The process is the same as above except that labels for a value do not need to be unique to the SSVC version, just unique to the associated decision point.

The character / separates decision-point:value pairs.
As many pairs should be provided in the abbreviated form as are required to communicate the desired information about the vulnerability or work item.
A vector must contain at least one decision-point:value pair.
The ordering of the pairs should be sorted alphabetically from A to Z by the ASCII characters representing the decision points.
A trailing / is used to close the string.

The vector is not tied to a specific decision tree.
It is meant to communicate information in a condensed form.
If priority labels (defer, etc.) are connected to a vector, then the decision tree used to reach those decisions should generally be noted.
However, for complex communication, machine-to-machine communication, or long-term storage of SSVC data, the JSON format and schema should be used.
The optional parameter time is the time in seconds since the UNIX epoch that the SSVC information was collected or last checked for freshness and accuracy.
Based on this, an example string could be: SSVCv2/Ps:Nm/T:T/U:E/1605040000/ For a vulnerability with no or minor Public Safety Impact, total Technical Impact, and efficient Utility, which was evaluated on Nov 10, 2020.

While these abbreviated format vectors can be uniquely produced based on a properly formatted JSON object, going from abbreviated form to JSON is not supported.
Therefore, JSON is the preferred storage and transmission method.
</div></details>

省略形と完全形の2つの構造化された通信形式をお勧めします。
省略形の目的は、チャート、グラフ、および表で脆弱性または決定に関する識別情報を提供する必要性を満たすことです。
したがって、省略形はスタンドアロンとして設計されていません。
フルフォーマットの目標は、意思決定または作業項目に関するすべてのコンテキストと詳細を、明確で機械可読な方法でキャプチャすることです。

省略形SSVCの省略形は、CVSSの「ベクトル文字列」表記から直接借用しています。
省略形の目的はチャートやグラフィックのラベルを提供することであるため、それは独立したものではありません。
SSVCの基本的な形式は次のとおりです。SSVC/（バージョン）/（決定ポイント）:(値）[/決定ポイント：値[/決定ポイント：値[...]]] [/ time] /
SSVCのこの現在のバージョンに基づいている場合、バージョンはv2です。
決定ポイントという用語は、次のように決定ポイントの名前から派生した1文字または2文字です。
- 可能性のある決定ポイントと関連データで指定されている決定ポイント名から始めます。
- 括弧内のテキスト（および括弧自体）をすべて削除します。
- 名前の一部である場合は、「Impact」という単語を削除します。
- 残りのタイトルケースの単語からイニシャリズムを作成し（「of」などは無視します）、最初の2つの単語のみを使用します。
- イニシャリズムの最初の文字は大文字です。 2番目の文字がある場合は、小文字です。
- 初期化がSSVCのバージョンの決定ポイント間で一意であることを確認します。 2つのイニシャリズムが衝突する場合は、LC_ALL=Cソートと同等のソース名をソートします。最初にソートする名前は、衝突が発生する初期性を維持します。イニシャリズムの2番目の文字を、衝突を解決する名前の最初の文字に設定します。名前がThreatおよびThresholdの場合、TはThreatになり、TsはThresholdになります。このような衝突のないSSVCの設計に努めています。

たとえば、Technical ImpactはTになり、PublicSafetyImpactはPsになります。
値という用語は、その前にあり、コロン（:)で接続されている決定ポイントの値または可能な値のステートメントです。
決定ポイントと同様に、値は、関連する決定ポイントのセクションの決定値の名前から派生した1文字または2文字で構成する必要があります。
たとえば、不自由なMEFサポートはMsになり、効率はEになります。
プロセスは上記と同じですが、値のラベルがSSVCバージョンに固有である必要はなく、関連する決定ポイントに固有である必要があります。

文字/は、decision-point：valueのペアを区切ります。
脆弱性または作業項目に関する必要な情報を伝達するために必要な数のペアを省略形で提供する必要があります。
ベクトルには、少なくとも1つの決定点と値のペアが含まれている必要があります。
ペアの順序は、決定ポイントを表すASCII文字でAからZのアルファベット順に並べ替える必要があります。
末尾の/は、文字列を閉じるために使用されます。

ベクトルは特定の決定木に関連付けられていません。
情報を凝縮した形で伝達することを目的としています。
優先度ラベル（延期など）がベクトルに接続されている場合、それらの決定に到達するために使用される決定木は、一般的に注意する必要があります。
ただし、複雑な通信、マシン間通信、またはSSVCデータの長期保存には、JSON形式とスキーマを使用する必要があります。
オプションのパラメータ時間は、SSVC情報が収集された、または鮮度と正確性について最後にチェックされたUNIXエポックからの秒単位の時間です。
これに基づくと、文字列の例は次のようになります。SSVCv2 / Ps：Nm / T：T / U：E / 1605040000 / 11月に評価された、公安への影響がない、または軽微な脆弱性、技術的影響の合計、および効率的なユーティリティ2020年10月10日。

これらの省略形式のベクトルは、適切にフォーマットされたJSONオブジェクトに基づいて一意に生成できますが、省略形式からJSONへの移行はサポートされていません。
したがって、JSONが推奨される保存および送信方法です。

### Full JSON format

<details><summary>原文</summary><div>

For a more robust, self-contained, machine-readable, we provide JSON schemas. The provision schema is equivalent to a decision tree and documents the full set of logical statements that a stakeholder uses to make decisions. The computed schema expresses a set of information about a work item or vulnerability at a point in time. A computed schema should identify the provision schema used, so the options from which the information was computed are specified.
Each element of choices should be an object that is a key-value pair of decision point:value, where the term decision point is a string derived from the name of the decision point as follows:
- Start with the decision point name as given in Likely Decision Points and Relevant Data.
- Remove any text in parentheses (and the parentheses themselves).
- Remove colon characters, if any (:).
- Convert the string to lower camel case by lowercasing the string, capitalizing any letter after a space, and removing all spaces.

The value term is derived the same way as decision point except start with the value name as given in the relevant decision point subsection of Likely Decision Points and Relevant Data.
</div></details>

より堅牢で、自己完結型で、機械可読であるために、JSONスキーマを提供します。プロビジョニングスキーマは意思決定ツリーと同等であり、利害関係者が意思決定に使用する論理ステートメントの完全なセットを文書化します。計算されたスキーマは、ある時点での作業項目または脆弱性に関する一連の情報を表します。計算スキーマは、使用されるプロビジョニングスキーマを識別する必要があるため、情報の計算元のオプションが指定されます。
選択肢の各要素は、決定ポイント：値のキーと値のペアであるオブジェクトである必要があります。ここで、決定ポイントという用語は、次のように決定ポイントの名前から派生した文字列です。
- 可能性のある決定ポイントと関連データで指定されている決定ポイント名から始めます。
- 括弧内のテキスト（および括弧自体）をすべて削除します。
- コロン文字がある場合は削除します（:)。
- 文字列を小文字にし、スペースの後の文字を大文字にし、すべてのスペースを削除して、文字列を小文字のキャメルケースに変換します。

値の項は、「可能性のある決定ポイントと関連データ」の関連する決定ポイントのサブセクションで指定されている値の名前で始まることを除いて、決定ポイントと同じ方法で導出されます。

### Partial or Incomplete Information

<details><summary>原文</summary><div>

What an analyst knows about a vulnerability may not be complete.
However, the vulnerability management community may still benefit from partial information.
In particular, suppliers and coordinators who might not know everything a deployer knows can still provide benefit to deployers by sharing what partial information they do know.
A second benefit to providing methods for communicating partial information is the reduction of bottlenecks or barriers to information exchange.
A timely partial warning is better than a complete warning that is too late.

The basic guidance is that the analyst should communicate all of the vulnerability’s possible states, to the best of the analyst’s knowledge.
If the analyst knows nothing, all states are possible.
For example, Utility may be laborious, efficient, or super effective.
In abbreviated form, write this as U:LESe.
Since a capital letter always indicates a new value, this is unambiguous.

The reason a stakeholder might publish something like U:LESe is that it expresses that the analyst thought about Utility but does not have anything to communicate.
A stakeholder might have information to communicate about some decision points but not others.
If SSVC uses this format to list the values that are in play for a particular vulnerability, there is no need for a special “I don’t know” marker.

The merit in this “list all values” approach emerges when the stakeholder knows that the value for a decision point may be A or B, but not C.
For example, say the analyst knows that Value Density is diffuse but does not know the value for *Automatability.
Then the analyst can usefully restrict Utility to one of laborious or efficient.
In abbreviated form, write this as U:LE.
As discussed below, information can change over time.
Partial information may be, but is not required to be, sharpened over time into a precise value for the decision point.
</div></details>

アナリストが脆弱性について知っていることは完全ではない可能性があります。
ただし、脆弱性管理コミュニティは、部分的な情報の恩恵を受ける可能性があります。
特に、デプロイヤーが知っていることすべてを知らない可能性のあるサプライヤーやコーディネーターは、知っている部分的な情報を共有することで、デプロイヤーに利益をもたらすことができます。
部分的な情報を伝達する方法を提供することの2番目の利点は、情報交換のボトルネックまたは障壁を減らすことです。
タイムリーな部分的な警告は、遅すぎる完全な警告よりも優れています。

基本的なガイダンスは、アナリストは、アナリストの知る限り、脆弱性の可能性のあるすべての状態を伝達する必要があるということです。
アナリストが何も知らなければ、すべての状態が可能です。
たとえば、ユーティリティは面倒、効率的、または非常に効果的である可能性があります。
省略形で、これをU：LESeと記述します。
大文字は常に新しい値を示すため、これは明確です。

利害関係者がU：LESeのようなものを公開する理由は、アナリストがユーティリティについて考えたが、伝達するものが何もないことを表現しているためです。
利害関係者は、いくつかの決定ポイントについて伝達するための情報を持っているかもしれませんが、他のものについては持っていないかもしれません。
SSVCがこの形式を使用して特定の脆弱性に関与している値を一覧表示する場合、特別な「わからない」マーカーは必要ありません。

この「すべての値をリストする」アプローチのメリットは、利害関係者が決定ポイントの値がAまたはBである可能性があるが、Cではない可能性があることを知っている場合に現れます。
たとえば、アナリストはValue Densityが拡散していることは知っているが、*Automatabilityの値は知らないとします。
次に、アナリストは、ユーティリティを面倒または効率的なものに制限することができます。
省略形で、これをU：LEと記述します。
以下で説明するように、情報は時間の経過とともに変化する可能性があります。
部分的な情報は、時間の経過とともに決定ポイントの正確な値にシャープ化される場合がありますが、必須ではありません。

### Information Changes Over Time

<details><summary>原文</summary><div>

Vulnerability management decisions are dynamic, and may change over time as the available information changes.
Information changes are one reason why SSVC decisions should always be timestamped.
SSVC decision points have different temporal properties.
Some, such as Utility, are mostly static.
For Utility to change, the market penetration or deployment norms of a vulnerable component would have to meaningfully change.
Some, such as State of Exploitation, may change quickly but only in one direction.

Both of these examples are out of the direct control of the vulnerability manager.
Some, such as Exposure, change mostly due to actions taken by the organization managing the vulnerable component.
If the actor who can usually trigger a relevant change is the organization using SSVC, then it is relatively straightforward to know when to update the SSVC decision.
That is, the organization should reevaluate the decision when they make a relevant change.
For those decision points that are about topics outside the control of the organization using SSVC, then the organization should occasionally poll their information sources for changes.
The cadence or rate of polls is different for each decision point, based on the expected rate of change.

We expect that updating information over time will be most useful where the evidence-gathering process can be automated.
Organizations that have mature asset management systems will also find this update process more efficient than those that do not.
For an organization without a mature asset management system, we would recommend putting organizational resources into maturing that function before putting effort into regular updates to vulnerability prioritization decision points.

The following decision points are usually out of the control of the organization running SSVC.
As an initial heuristic, we suggest the associated polling frequency for each.
These frequencies can be customized, as the update frequency is directly related to the organization’s tolerance for the risk that the information is out of date.
As discussed in Tree Construction and Customization Guidance, risk tolerance is unique to each organization.
Risk tolerance and risk appetite are primarily reflected in the priority labels (that is, decisions) encoded in the SSVC decision tree, but information polling frequency is also a risk tolerance decision and each organization may choose different time values.

- State of Exploitation: every 1 day
- Technical Impact: never (should be static per vulnerability)
- Utility: every 6 months
- Public Safety Impact: every 1 year

The following decision points are usually in the control of the organization running SSVC and should be reevaluated when a relevant change is made or during annual reviews of assets.

- Situated Safety Impact
- Mission Impact
- System Exposure

If SSVC information is all timestamped appropriately (as discussed earlier in this section), then an analyst can compare the timestamp to the current date and determine whether information is considered stale.
The above rates are heuristic suggestions, and organizations may choose different ones.
Any public repository of vulnerability information should keep a change log of when values change for each decision point, for each vulnerability.
Vulnerability response analysts should keep such change logs as well.
Similar to logging practices recommended for incident response (Cichonski et al.  2012), such practices make the process less error-prone and facilitate after-action reviews.
</div></details>

脆弱性管理の決定は動的であり、利用可能な情報が変化するにつれて時間とともに変化する可能性があります。
情報の変更は、SSVCの決定に常にタイムスタンプを付ける必要がある理由の1つです。
SSVC決定ポイントには、さまざまな時間的特性があります。
ユーティリティなどの一部は、ほとんど静的です。
ユーティリティを変更するには、脆弱なコンポーネントの市場浸透率または展開基準を有意義に変更する必要があります。
State of Exploitationなどの一部は、急速に変化する可能性がありますが、一方向にしか変化しません。

これらの例は両方とも、脆弱性マネージャーの直接の制御から外れています。
エクスポージャーなどの一部は、主に脆弱なコンポーネントを管理している組織によって実行されたアクションによって変更されます。
通常、関連する変更をトリガーできるアクターがSSVCを使用している組織である場合、SSVCの決定をいつ更新するかを知ることは比較的簡単です。
つまり、組織は、関連する変更を行うときに決定を再評価する必要があります。
SSVCを使用している組織の管理外のトピックに関する決定ポイントの場合、組織は情報ソースをポーリングして変更を確認する必要があります。
ポーリングのリズムまたはレートは、予想される変化率に基づいて、決定ポイントごとに異なります。

証拠収集プロセスを自動化できる場合は、時間の経過とともに情報を更新することが最も役立つと期待しています。
成熟した資産管理システムを備えている組織は、そうでない組織よりもこの更新プロセスの方が効率的であることがわかります。
成熟した資産管理システムを持たない組織の場合、脆弱性の優先順位付けの決定ポイントを定期的に更新する前に、組織のリソースをその機能に成熟させることをお勧めします。

以下の決定ポイントは通常、SSVCを実行している組織の管理外です。
最初のヒューリスティックとして、それぞれに関連するポーリング頻度を提案します。
更新頻度は、情報が古くなるリスクに対する組織の許容度に直接関係しているため、これらの頻度はカスタマイズできます。
ツリーの構築とカスタマイズのガイダンスで説明したように、リスク許容度は組織ごとに異なります。
リスク許容度とリスクアペタイトは、主にSSVCデシジョンツリーにエンコードされた優先度ラベル（つまり、決定）に反映されますが、情報ポーリングの頻度もリスク許容度の決定であり、組織ごとに異なる時間値を選択できます。

- 搾取の状態：1日ごと
- 技術的影響：決して（脆弱性ごとに静的である必要があります）
- ユーティリティ：6か月ごと
- 公安への影響：1年ごと

以下の決定ポイントは通常、SSVCを実行している組織の管理下にあり、関連する変更が行われたとき、または資産の年次レビュー中に再評価する必要があります。

- 状況に応じた安全性への影響
- ミッションインパクト
- システムへの暴露

SSVC情報にすべて適切なタイムスタンプが付けられている場合（このセクションで前述したように）、アナリストはタイムスタンプを現在の日付と比較して、情報が古くなっていると見なされるかどうかを判断できます。
上記の料金はヒューリスティックな提案であり、組織は別の料金を選択する場合があります。
脆弱性情報の公開リポジトリは、脆弱性ごとに、決定ポイントごとに値が変更されたときの変更ログを保持する必要があります。
脆弱性対応アナリストは、このような変更ログも保持する必要があります。
インシデント対応に推奨されるロギングプラクティス（Cichonski et al。2012）と同様に、このようなプラクティスにより、プロセスでエラーが発生しにくくなり、アクション後のレビューが容易になります。

## Version 2 Changelog

<details><summary>原文</summary><div>

This section summarizes the changes between SSVC version 2 and SSVC version 1.
1 as published at the Workshop on the Ecnomics of Information Security (WEIS 2020).
The details of what changes were made can be viewed on the SSVC GitHub issues closed under the SSVC v2 Development project.
We addressed about 60 issues.
About 10 issues identified “bugs” or errors in version 1.1.
About 20 issues improved documentation of tools or improved the clarity of document text.
The remaining 30 issues were focused on enhancing SSVC based on feedback received on version 1, though several of the bug fixes and documentation improvements also provided improvements.
This section focuses on changes that provided enhancements.
</div></details>

このセクションでは、情報セキュリティの経済学に関するワークショップ（WEIS 2020）で公開されたSSVCバージョン2とSSVCバージョン1.1の間の変更点を要約します。
加えられた変更の詳細は、SSVCv2開発プロジェクトでクローズされたSSVCGitHubの問題で確認できます。
約60の問題に対処しました。
バージョン1.1で「バグ」またはエラーを特定した約10の問題。
約20の問題により、ツールのドキュメントが改善され、ドキュメントテキストの明瞭さが向上しました。
残りの30の問題は、バージョン1で受け取ったフィードバックに基づいてSSVCを強化することに焦点を当てていましたが、バグ修正とドキュメントの改善のいくつかも改善を提供しました。
このセクションでは、機能強化を提供した変更に焦点を当てます。

### Coordinator stakeholder

<details><summary>原文</summary><div>

Version 1 only considered two stakeholders: those who make software, and those who use information systems.
Version 2 introduces a coordinator stakeholder and two distinct decisions for that stakeholder group: vulnerability intake triage and publication about a vulnerability.
These decisions use some existing decision points, but also introduce six new decision points to support coordinators in making these decisions.
The coordinator stakeholder is based on CERT/CC’s experience coordinating vulnerabilities.
</div></details>

バージョン1では、ソフトウェアを作成する関係者と情報システムを使用する関係者の2つの利害関係者のみが考慮されました。
バージョン2では、コーディネーターの利害関係者と、その利害関係者グループに対する2つの明確な決定が導入されています。脆弱性の取り込みトリアージと脆弱性に関する公開です。
これらの決定は、いくつかの既存の決定ポイントを使用しますが、これらの決定を行う際にコーディネーターをサポートするために6つの新しい決定ポイントも導入します。
コーディネーターの利害関係者は、脆弱性を調整したCERT/CCの経験に基づいています。

### Terminology changes

<details><summary>原文</summary><div>

Some terms have been adjusted to better align with other usage in the field or based on feedback.
Therefore, “patch developer” became supplier and “patch applier” became deployer.
These terms in version 2 better reflect the stakeholder’s relationship to the vulnerable component and also help keep clear that SSVC is about prioritization of work items in vulnerability management, not just patches.
We have also generally removed the word patch and instead use the more general “remediation” for a complete fix and “mitigation” for actions that reduce risk but do not remove a vulnerability from a system.
“Virulence” was renamed Automatable in a effort to be more direct and clear, rather than relying on an epidemiology metaphor.
We changed “out-of-band” to out-of-cycle.
Some concepts needed to be clarified or added.
These changes are a bit more substantive than the above terminology changes, but are similar.
For example, we clarified how end-of-life products are prioritized with SSVC.
We also clarified in Scope concepts around vulnerability identificatin and disambiguation.
Version 2 adopts an explicit definition of risk (from ISO Guide 73).
We also differentiated between vulnerability risk, or that risk arising from an unmanaged vulnerability in an information system, and change risk, or that risk from modifying or updating an information system to mitigate or remediate a vulnerability.
SSVC version 2 focuses on assessing and managing vulnerability risk, not change risk.
This stance was not explicit in SSVC version 1.
</div></details>

一部の用語は、フィールドでの他の使用法との整合性を高めるため、またはフィードバックに基づいて調整されています。
したがって、「パッチ開発者」はサプライヤーになり、「パッチアプライヤー」はデプロイヤーになりました。
バージョン2のこれらの用語は、脆弱なコンポーネントに対する利害関係者の関係をより適切に反映し、SSVCがパッチだけでなく、脆弱性管理における作業項目の優先順位付けに関するものであることを明確にするのにも役立ちます。
また、一般的にパッチという言葉を削除し、代わりに、完全な修正にはより一般的な「修復」を使用し、リスクを軽減するがシステムから脆弱性を除去しないアクションには「緩和」を使用します。
「病原性」は、疫学の比喩に頼るのではなく、より直接的で明確にするためにAutomatableに名前が変更されました。
「帯域外」をサイクル外に変更しました。
いくつかの概念を明確にするか追加する必要がありました。
これらの変更は、上記の用語の変更よりも少し実質的ですが、類似しています。
たとえば、SSVCで保守終了製品がどのように優先されるかを明確にしました。
また、スコープの概念で、脆弱性の識別と曖昧性解消に関する概念を明確にしました。
バージョン2は、リスクの明示的な定義を採用しています（ISOガイド73から）。
また、脆弱性リスク、つまり情報システムの管理されていない脆弱性から生じるリスクと、脆弱性を軽減または修正するために情報システムを変更または更新することによるリスクを変更するリスクを区別しました。
SSVCバージョン2は、変更リスクではなく、脆弱性リスクの評価と管理に重点を置いています。
このスタンスは、SSVCバージョン1では明示されていませんでした。

### Improvements to decision points

<details><summary>原文</summary><div>

Version 1 had a decision point for well-being impact that was shared between supplier and deployer stakeholders.
Since these types of stakeholder have access to different information about safety and well-being, Version 2 splits this concept into *Public Safety Impact and Situated Safety Impact.
The underlying definition remains largely the same.
However, *Public Safety Impact has fewer output options (it is less granular) in recognition that a supplier or coordinator has less information about the context of deployment than a deployer does.
In addition, based on feedback from SSVC users, the SSVC version 2 recommended applier tree makes use of a combined value for Mission Impact and Situated Safety Impact.
The intuition behind this change is that if a person is going to die OR the organization is going to fail (for example, go bankrupt), then the organization will likely want to act with highest priority.
Either situation is sufficient to increase the priority, and there do not appear to be situations where a low Mission Impact would mitigate a high Situated Safety Impact or vice versa.
On the other hand, a low Utility or System Exposure may mitigate a high mission or well-being impact.
So the Version 2 recommended tree is more usable than the Version 1 tree, thanks to these changes.
</div></details>

バージョン1には、サプライヤーと展開者の利害関係者の間で共有される幸福への影響に関する決定ポイントがありました。
これらのタイプの利害関係者は、安全と福祉に関するさまざまな情報にアクセスできるため、バージョン2は、この概念を* PublicSafetyImpactとSituedSafetyImpactに分割します。
基本的な定義はほとんど同じです。
ただし、* Public Safety Impactは、サプライヤーまたはコーディネーターが展開のコンテキストに関する情報を展開者よりも少なくしていることを認識して、出力オプションが少なくなっています（詳細度が低くなっています）。
さらに、SSVCユーザーからのフィードバックに基づいて、SSVCバージョン2が推奨するアプライヤーツリーは、ミッションインパクトとシチュエーションセーフティインパクトの合計値を利用します。
この変更の背後にある直感は、人が死ぬか、組織が破産する（たとえば、破産する）場合、組織は最優先で行動したいと思う可能性が高いということです。
どちらの状況でも優先度を上げるのに十分であり、低いミッションの影響が高い状況の安全の影響を軽減する、またはその逆の状況はないようです。
一方、ユーティリティまたはシステムの露出が低いと、高いミッションまたは幸福への影響が軽減される可能性があります。
したがって、これらの変更のおかげで、バージョン2の推奨ツリーはバージョン1のツリーよりも使いやすくなっています。

### Tree management and communication tools

<details><summary>原文</summary><div>

The section Tree Construction and Customization Guidance is largely new or revised.
We produced new software tools for interacting with SSVC, which are documented in that section.
Version 2 adds reasoning behind why a stakeholder might customize a decision tree, what aspects of the tree are best to customize, tools for encoding custom trees in JSON, and scripts for visualizing custom trees.
Similarly, the section on Guidance on Communicating Results is largely new.
The section presents both an abbreviated and unabridged format for communicating SSVC information about a vulnerability.
This communication may be connected to the formats for communicating a whole decision tree.
Version 2 also addresses several other questions about SSVC information management, such as handling information changes over time, partial information, sourcing information for each decision point, and how collection and analysis of SSVC decision points can be automated.
</div></details>

ツリーの構築とカスタマイズのガイダンスのセクションは、主に新しいか改訂されています。
SSVCと対話するための新しいソフトウェアツールを作成しました。これについては、そのセクションで説明しています。
バージョン2では、利害関係者が決定木をカスタマイズする理由、ツリーのどの側面をカスタマイズするのが最適か、JSONでカスタムツリーをエンコードするためのツール、およびカスタムツリーを視覚化するためのスクリプトが追加されています。
同様に、結果の伝達に関するガイダンスのセクションはほとんど新しいものです。
このセクションでは、脆弱性に関するSSVC情報を伝達するための省略形式と非簡略形式の両方を示します。
この通信は、決定木全体を通信するためのフォーマットに接続することができます。
バージョン2は、SSVC情報管理に関する他のいくつかの質問にも対応しています。たとえば、時間の経過に伴う情報の変更の処理、部分的な情報、各決定ポイントの情報の調達、SSVC決定ポイントの収集と分析の自動化方法などです。

## Evaluation of the Draft Trees

<details><summary>原文</summary><div>

We conducted a pilot test on the adequacy of the hypothesized decision trees.
This section reports results for SSVC version 1.
The method of the pilot test is described in Pilot Methodogy.
The study resulted in several changes to the hypothesized trees; we capture those changes and the reason for each of them in Pilot Results.
The version 1 supplier and deployer trees included the improvements reported in Improvement Instigated by the Pilot.
</div></details>

仮定した決定木の妥当性についてパイロットテストを実施しました。
このセクションでは、SSVCバージョン1の結果を報告します。
パイロットテストの方法は、パイロット方法論で説明されています。
この研究の結果、仮定された樹木にいくつかの変更が加えられました。 これらの変更とそれぞれの理由をパイロット結果に記録します。
バージョン1のサプライヤーとデプロイヤーのツリーには、パイロットによって引き起こされた改善で報告された改善が含まれていました。

### Pilot Methodology

<details><summary>原文</summary><div>

The pilot study tested inter-rater agreement of decisions reached.
Each author played the role of an analyst in both stakeholder groups (supplying and deploying) for nine vulnerabilities.
We selected these nine vulnerabilities based on expert analysis, with the goal that the nine cases cover a useful series of vulnerabilities of interest.
Specifically, we selected three vulnerabilities to represent safety-critical cases, three to represent regulated-systems cases, and three to represent general computing cases.
During the pilot, we did not form guidance on how to assess the values of the decision points.
However, we did standardize the set of evidence that was taken to be true for the point in time representing the evaluation.
Given this static information sheet, we did not synchronize an evaluation process for how to decide whether Exploitation, for example, should take the value of none, PoC, or active.
We agreed on the descriptions of the decision points and the descriptions of their values.
The goal of the pilot was to test the adequacy of those descriptions by evaluating whether the analysts agreed.
We improved the decision point descriptions based on the results of the pilot; our changes are documented in Improvement Instigated by the Pilot.

In the design of the pilot, we held constant the information available about the vulnerability.
This strategy restricted the analyst to decisions based on the framework given that information.
That is, it controlled for differences in information search procedure among the analysts.
The information search procedure should be controlled because this pilot was about the framework content, not how people answer questions based on that content.
After the framework is more stable, a separate study should be devised that shows how analysts should answer the questions in the framework.
The basis for the assessment that information search will be an important aspect in using the evaluation framework is based on our experience while developing the framework.
During informal testing, often disagreements about a result involved a disagreement about what the scenario actually was; different information search methods and prior experiences led to different understandings of the scenario.
This pilot methodology holds the information and scenario constant to test agreement about the descriptions themselves.
This strategy makes constructing a prioritization system more tractable by separating problems in how people search for information from problems in how people make decisions.
This paper focuses only on the structure of decision making.
Advice about how to search for information about a vulnerability is a separate project that will be part of future work.
In some domains, namely exploit availability, we have started that work in parallel.
</div></details>

パイロット研究では、評価者間の決定の合意が達成されたことをテストしました。
各作成者は、9つの脆弱性について、両方の利害関係者グループ（供給と展開）でアナリストの役割を果たしました。
専門家の分析に基づいてこれらの9つの脆弱性を選択し、9つのケースが関心のある一連の有用な脆弱性をカバーすることを目標としています。
具体的には、セーフティクリティカルなケースを表す3つの脆弱性、規制対象システムのケースを表す3つの脆弱性、および一般的なコンピューティングのケースを表す3つの脆弱性を選択しました。
パイロット期間中、決定ポイントの値を評価する方法についてのガイダンスは作成しませんでした。
ただし、評価を表す時点で真であると見なされた一連の証拠を標準化しました。
この静的な情報シートを前提として、たとえば、悪用がnone、PoC、またはactiveの値を取るかどうかを決定する方法の評価プロセスを同期しませんでした。
決定点の説明とその値の説明について合意しました。
パイロットの目標は、アナリストが同意したかどうかを評価することにより、これらの説明の妥当性をテストすることでした。
パイロットの結果に基づいて、決定ポイントの説明を改善しました。私たちの変更は、パイロットによって引き起こされた改善に文書化されています。

パイロットの設計では、脆弱性について入手可能な情報を一定に保ちました。
この戦略は、アナリストをその情報を与えられたフレームワークに基づく決定に制限しました。
つまり、アナリスト間の情報検索手順の違いを制御しました。
このパイロットはフレームワークのコンテンツに関するものであり、そのコンテンツに基づいて人々が質問に答える方法ではないため、情報検索手順を制御する必要があります。
フレームワークがより安定した後、アナリストがフレームワークの質問にどのように答えるべきかを示す別の調査を考案する必要があります。
情報検索が評価フレームワークを使用する上で重要な側面になるという評価の基礎は、フレームワークを開発する際の私たちの経験に基づいています。
非公式のテストでは、結果に関する意見の不一致には、シナリオが実際に何であるかについての意見の不一致が含まれることがよくありました。さまざまな情報検索方法と以前の経験により、シナリオのさまざまな理解がもたらされました。
このパイロット方法論は、説明自体に関する合意をテストするために、情報とシナリオを一定に保ちます。
この戦略は、人々が情報を検索する方法の問題と、人々が決定を下す方法の問題を分離することにより、優先順位付けシステムの構築をより扱いやすくします。
このホワイトペーパーでは、意思決定の構造のみに焦点を当てています。
脆弱性に関する情報を検索する方法に関するアドバイスは、将来の作業の一部となる別のプロジェクトです。
一部のドメイン、つまりエクスプロイトの可用性では、並行してその作業を開始しました。

<details><summary>原文</summary><div>

The structure of the pilot test is as follows.
Table 11 provides an example of the information provided to each analyst.
The supplier portfolio details use strikeout font because this decision item was removed after the pilot.
The decision procedure for each case is as follows: for each analyst, for each vulnerability, for each stakeholder group, do the following.

1. Start at the root node of the relevant decision tree (deployer or supplier).
2. Document the decision branch that matches the vulnerability for this stakeholder context.
3. Document the evidence that supports that decision.
4. Repeat this decision-and-evidence process until the analyst reaches a leaf node in the tree.

Table 14: Example of Scenario Information Provided to Analysts (Using CVE-2019-9042 as the Example)

| Information Item | Description Provided to Analysts |
| --- | --- |
| Use of Cyber-Physical System | Sitemagic’s content management system (CMS) seems to be fairly popular among smaller businesses because it starts out with a free plan to use it.  Then it gradually has small increments in payment for additional features. Its ease-of-use, good designs, and one-stop-shopping for businesses attracts a fair number of clients. Like any CMS, it “manages the creation and modification of digital content. These systems typically support multiple users in a collaborative environment, allowing document management with different styles of governance and workflows. Usually the content is a website” (Wikipedia, 2019) |
| State of Exploitation | Appears to be active exploitation of this vulnerability according to NVD.  They have linked to the exploit: http://www.iwantacve.cn/index.php/archives/116/. |
| ~Developer Portfolio Details~ | ~Sitemagic is an open-source project. The only thing the brand name applies to is the CMS, and it does not appear to be part of another open-source umbrella. The project is under active maintenance (i.e., it is not a dead project).~ |
| Technical Impact of Exploit | An authenticated user can upload a .php file to execute arbitrary code with system privileges.  Scenario Blurb We are a small business that uses Sitemagic to help run our business.  Sitemagic handles everything from digital marketing and site design to facilitating the e-commerce transactions of the website. We rely on this website heavily, even though we do have a brick-and-mortar store. Many times, products are not available in-store, but are available online, so we point many customers to our online store. |
| Deployer Mission | We are a private company that must turn a profit to remain competitive.  We want to provide customers with a valuable product at a reasonable price, while still turning a profit to run the business. As we are privately held (and not public), we are free to choose the best growth strategy (that is, we are not legally bound to demonstrate quarterly earnings for shareholders and can take a longer-term view if it makes us competitive). |
| Information Item | Description Provided to Analysts |
| Deployment of Affected System | We have deployed this system such that only the web designer Cheryl and the IT admin Sally are allowed to access the CMS as users. They login through a password-protected portal that can be accessed anywhere in the world for remote administration. The CMS publishes content to the web, and that web server and site are publicly available. |

This test structure produced a series of lists similar in form to the contents of Table 12. Analysts also noted how much time they spent on each vulnerability in each stakeholder group.

Table 15: Example Documentation of a Single Decision Point

| Decision Point | Branch Selected | Supporting Evidence |
| --- | --- | --- |
| Exploitation=active | Controlled | The CMS has a limited number of authorized users, and the vulnerability is exploitable only by an authenticated user |

We evaluated inter-rater agreement in two stages.
In the first stage, each analyst independently documented their decisions.
This stage produced 18 sets of decisions (nine vulnerabilities across each of two stakeholder groups) per analyst.
In the second stage, we met to discuss decision points where at least one analyst differed from the others.
If any analyst changed their decision, they appended the information and evidence they gained during this meeting in the “supporting evidence” value in their documentation.
No changes to decisions were forced, and prior decisions were not erased, just amended.
After the second stage, we calculated some statistical measures of inter-rater agreement to help guide the analysis of problem areas.

To assess agreement, we calculate Fleiss’ kappa, both for the value in the leaf node reached for each case and every decision in a case (Fleiss and Cohen 1973).
Evaluating individual decisions is complicated slightly because the different paths through the tree mean that a different number of analysts may have evaluated certain items, and Fleiss’ kappa requires a static number of raters.
“Leaf node reached” is described to pick out the specific path through the tree the analyst selected and to treat that as a label holistically.
Measuring agreement based on the path has the drawback that ostensibly similar paths (for example, paths that agree on 3 of 4 decisions) are treated as no more similar than paths that agree on 0 of 4 decisions.
The two measures of agreement (per decision and per path) are complementary, so we report both.
</div></details>

パイロットテストの構成は次のとおりです。
表11に、各アナリストに提供される情報の例を示します。
この決定項目はパイロット後に削除されたため、サプライヤポートフォリオの詳細には取り消し線フォントが使用されています。
各ケースの決定手順は次のとおりです。各アナリスト、各脆弱性、各利害関係者グループについて、次の手順を実行します。

1. 関連するデシジョンツリー（デプロイヤまたはサプライヤ）のルートノードから開始します。
2. この利害関係者のコンテキストの脆弱性に一致する意思決定ブランチを文書化します。
3. その決定を裏付ける証拠を文書化します。
4. アナリストがツリーのリーフノードに到達するまで、この決定と証拠のプロセスを繰り返します。

表14：アナリストに提供されるシナリオ情報の例（例としてCVE-2019-9042を使用）

| 情報アイテム | アナリストに提供される説明 |
| --- | --- |
| サイバーフィジカルシステムの使用 | Sitemagicのコンテンツ管理システム（CMS）は、無料で使用できるようになっているため、中小企業の間でかなり人気があるようです。その後、追加機能の支払いが徐々に少しずつ増えていきます。その使いやすさ、優れたデザイン、およびビジネス向けのワンストップショッピングは、かなりの数のクライアントを魅了しています。他のCMSと同様に、「デジタルコンテンツの作成と変更を管理します。これらのシステムは通常、コラボレーション環境で複数のユーザーをサポートし、さまざまなスタイルのガバナンスとワークフローを使用したドキュメント管理を可能にします。通常、コンテンツはWebサイトです」（ウィキペディア、2019年）|
| 搾取の状態 | NVDによると、この脆弱性を積極的に利用しているようです。それらはエクスプロイトにリンクしています：http：//www.iwantacve.cn/index.php/archives/116/。 |
| ~開発者ポートフォリオの詳細~ | ~Sitemagicはオープンソースプロジェクトです。ブランド名が適用されるのはCMSだけであり、別のオープンソースの傘の一部ではないようです。プロジェクトはアクティブなメンテナンス中です（つまり、デッドプロジェクトではありません）。~ |
| エクスプロイトの技術的影響 | 認証されたユーザーは、.phpファイルをアップロードして、システム権限で任意のコードを実行できます。シナリオの宣伝文句私たちは、Sitemagicを使用してビジネスを運営する中小企業です。 Sitemagicは、デジタルマーケティングやサイトのデザインから、Webサイトのeコマーストランザクションの促進まで、すべてを処理します。実店舗はありますが、このWebサイトに大きく依存しています。多くの場合、商品は店頭では入手できませんが、オンラインで入手できるため、多くのお客様にオンラインストアを紹介しています。 |
| デプロイヤミッション | 私たちは、競争力を維持するために利益を上げなければならない民間企業です。事業を営むために利益を上げながら、リーズナブルな価格でお客様に価値ある製品を提供したいと考えています。非公開企業（非公開企業）であるため、最善の成長戦略を自由に選択できます（つまり、株主の四半期収益を法的に証明する義務はなく、競争力があれば長期的な視点をとることができます）。 |
| 情報アイテム | アナリストに提供される説明 |
| 影響を受けるシステムの展開 | このシステムは、WebデザイナーのCherylとIT管理者のSallyだけがユーザーとしてCMSにアクセスできるように展開されています。彼らは、リモート管理のために世界中のどこからでもアクセスできるパスワードで保護されたポータルを介してログインします。 CMSはコンテンツをWebに公開し、そのWebサーバーとサイトは公開されています。 |

### Pilot participant details

<details><summary>原文</summary><div>

The pilot participants are the five authors plus one analyst who had not seen the draft system before participating.
Five of the six participants had spent at least one year as professional vulnerability analysts prior to the pilot (Spring was the exception).
Three of the participants had at least ten years of experience each.
The participants experience is primarily as coordinators at the CERT® Coordination Center.
On the one hand, this is a different perspective than either suppliers or deployers; on the other, the coordinator role is an information broker that often interacts with these perspectives (Householder, Wassermann, et al. 2020, sec. 3).

These participant demographics limit the generalizability of the results of the pilot.
Even though the results cannot be systematically generalized to other analysts, there are at least three benefits to conducting the pilot among this limited demographic.
First, it should surface any material tacit disagreements about term usage among the authors.
Tacit agreements that are not explained in the text likely survive the pilot study without being acknowledged, but places where the authors tacitly disagreed should be surfaced.
We found this to be the case; Improvement Instigated by the Pilot documents these results.
Second, the pilot provides a case study that demonstrate SSVC is at least possible for some small group of analysts to use.
This achievement is not large, but it is a first step.
Third, the pilot provides a proof of concept method and metric that any vulnerability prioritization method could use to examine usability for analysts more generally.
While the effect of education on vulnerability assessment with CVSS has been tested (Allodi et al. 2018), we are not aware of any current vulnerability prioritization method that tests usability or agreement among analysts as part of the development process.
Future work on SSVC as well as further development of other prioritization methods can benefit from using the method described in the pilot.
Future instances should use more representative participant demographics.
</div></details>

パイロット参加者は、参加する前にドラフトシステムを見たことがなかった5人の作成者と1人のアナリストです。
6人の参加者のうち5人は、パイロットの前にプロの脆弱性アナリストとして少なくとも1年を過ごしました（春は例外でした）。
参加者のうち3人は、それぞれ少なくとも10年の経験がありました。
参加者の経験は、主にCERT®コーディネーションセンターのコーディネーターとして行われます。
一方では、これはサプライヤーや展開者とは異なる視点です。一方、コーディネーターの役割は、これらの視点と頻繁にやり取りする情報ブローカーです（Householder、Wassermann、et al。2020、sec.3）。

これらの参加者の人口統計は、パイロットの結果の一般化を制限します。
結果を他のアナリストに体系的に一般化することはできませんが、この限られた人口統計の中でパイロットを実施することには、少なくとも3つの利点があります。
第一に、著者間の用語の使用に関する重要な暗黙の不一致を明らかにする必要があります。
本文で説明されていない暗黙の合意は、承認されることなくパイロット研究を生き残る可能性が高いが、著者が暗黙のうちに反対した場所を明らかにする必要がある。
これが事実であることがわかりました。パイロットによって引き起こされた改善は、これらの結果を文書化します。
次に、パイロットは、SSVCが少なくとも一部の少数のアナリストグループが使用できることを実証するケーススタディを提供します。
この成果は大きくはありませんが、第一歩です。
第3に、パイロットは、脆弱性の優先順位付け方法がアナリストのユーザビリティをより一般的に調べるために使用できる概念実証方法とメトリックを提供します。
CVSSによる脆弱性評価に対する教育の効果はテストされていますが（Allodi et al。2018）、開発プロセスの一部としてアナリスト間のユーザビリティまたは合意をテストする現在の脆弱性の優先順位付け方法は認識されていません。
SSVCに関する今後の作業、および他の優先順位付け方法のさらなる開発は、パイロットで説明されている方法を使用することで恩恵を受けることができます。
将来のインスタンスでは、より代表的な参加者の人口統計を使用する必要があります。

### Vulnerabilities used as examples

<details><summary>原文</summary><div>

The vulnerabilities used as case studies are as follows. All quotes are from the National Vulnerability Database (NVD) and are illustrative of the vulnerability; however, during the study each vulnerability was evaluated according to information analogous to that in Table 11.  Safety-Critical Cases
- CVE-2015-5374: “Vulnerability . . . in \[Siemens\] Firmware variant PROFINET IO for EN100 Ethernet module. . . Specially crafted packets sent to port 50000/UDP could cause a denial-of-service of the affected device. . . ”
- CVE-2014-0751: “Directory traversal vulnerability in . . . GE Intelligent Platforms Proficy HMI/SCADA - CIMPLICITY before 8.2 SIM 24, and Proficy Process Systems with CIMPLICITY, allows remote attackers to execute arbitrary code via a crafted message to TCP port 10212, aka ZDI-CAN-1623.”
- CVE-2015-1014: “A successful exploit of these vulnerabilities requires the local user to load a crafted DLL file in the system directory on servers running Schneider Electric OFS v3.5 with version v7.40 of SCADA Expert Vijeo Citect/CitectSCADA, OFS v3.5 with version v7.30 of Vijeo Citect/CitectSCADA, and OFS v3.5 with version v7.20 of Vijeo Citect/CitectSCADA. If the application attempts to open that file, the application could crash or allow the attacker to execute arbitrary code.”

Regulated Systems Cases
- CVE-2018-14781: “Medtronic insulin pump [specific versions] when paired with a remote controller and having the “easy bolus” and “remote bolus” options enabled (non-default), are vulnerable to a capture-replay attack. An attacker can . . . cause an insulin (bolus) delivery.”
- CVE-2017-9590: “The State Bank of Waterloo Mobile . . . app 3.0.2 . . . for iOS does not verify X.509 certificates from SSL servers, which allows man-in-the-middle attackers to spoof servers and obtain sensitive information via a crafted certificate.”
- CVE-2017-3183: “Sage XRT Treasury, version 3, fails to properly restrict database access to authorized users, which may enable any authenticated user to gain full access to privileged database functions. Sage XRT Treasury is a business finance management application. . . . ”

 General Computing Cases
- CVE-2019-2691: “Vulnerability in the MySQL Server component of Oracle MySQL (subcomponent: Server: Security: Roles). Supported versions that are affected are 8.0.15 and prior. Easily exploitable vulnerability allows high privileged attacker with network access via multiple protocols to . . . complete DoS of MySQL Server.”
- CVE-2019-9042: “\[I\]n Sitemagic CMS v4.4. . . the user can upload a .php file to execute arbitrary code, as demonstrated by 404.php. This can only occur if the administrator neglects to set FileExtensionFilter and there are untrusted user accounts. . . . ”
- CVE-2017-5638: “The Jakarta Multipart parser in Apache Struts 2 2.3.x before 2.3.32 and 2.5.x before 2.5.10.1 has incorrect exception handling and error-message generation during file-upload attempts, which allows remote attackers to execute arbitrary commands via crafted [specific headers], as exploited in the wild in March 2017. . . ”
</div></details>

ケーススタディとして使用された脆弱性は次のとおりです。すべての引用はNationalVulnerabilityDatabase（NVD）からのものであり、脆弱性を示しています。ただし、調査中、各脆弱性は表11の情報に類似した情報に従って評価されました。セーフティクリティカルケース
- CVE-2015-5374：「脆弱性... \[Siemens\]ファームウェアバリアントPROFINETIOforEN100イーサネットモジュール...ポート50000/UDPに送信される特別に細工されたパケットは、影響を受けるデバイスのサービス拒否を引き起こす可能性があります...」
- CVE-2014-0751：「ディレクトリトラバーサルの脆弱性... GEインテリジェントプラットフォームスProficyHMI/ SCADA-8.2SIM24より前のCIMPLICITYおよびCIMPLICITYを備えたProficyProcessSystemsにより、リモートの攻撃者は、細工されたメッセージを介してTCPポート10212（別名ZDI-CAN-1623）への任意のコードを実行できます。
- CVE-2015-1014：「これらの脆弱性を悪用するには、ローカルユーザーがSchneider ElectricOFSv3.5とバージョンv7.40のSCADAExpertVijeo Citect/CitectSCADAを実行しているサーバーのシステムディレクトリに細工されたDLLファイルをロードする必要があります。 OFSv3.5とバージョンv7.30のVijeoCitect/ CitectSCADA、およびOFSv3.5とバージョンv7.20のVijeoCitect/CitectSCADA。アプリケーションがそのファイルを開こうとすると、アプリケーションがクラッシュしたり、攻撃者が任意のコードを実行できるようになる可能性があります。」

規制対象システムの事例
- CVE-2018-14781：「メドトロニックインスリンポンプ\[特定のバージョン\]をリモートコントローラーと組み合わせて、「イージーボーラス」および「リモートボーラス」オプションを有効（デフォルト以外）にすると、キャプチャリプレイ攻撃に対して脆弱になります。攻撃者はできます...インスリン（ボーラス）送達を引き起こします。」
- CVE-2017-9590：「ウォータールーモバイルの州立銀行...アプリ3.0.2... for iOSは、SSLサーバーからのX.509証明書を検証しません。これにより、中間者攻撃者がサーバーをスプーフィングし、細工された証明書を介して機密情報を取得できるようになります。」
- CVE-2017-3183：「SageXRT Treasuryバージョン3は、許可されたユーザーへのデータベースアクセスを適切に制限できません。これにより、認証されたユーザーが特権データベース機能へのフルアクセスを取得できる可能性があります。 Sage XRT Treasuryは、ビジネス財務管理アプリケーションです... 。 」

一般的なコンピューティングの事例
- CVE-2019-2691：「OracleMySQLのMySQLサーバーコンポーネント（サブコンポーネント：サーバー：セキュリティ：ロール）の脆弱性。 影響を受けるサポートされているバージョンは8.0.15以前です。 簡単に悪用可能な脆弱性により、特権の高い攻撃者が複数のプロトコルを介してネットワークにアクセスできるようになります... MySQLサーバーの完全なDoS。」
- CVE-2019-9042：「\[I\]nSitemagicCMSv4.4... 404.phpで示されているように、ユーザーは.phpファイルをアップロードして任意のコードを実行できます。 これは、管理者がFileExtensionFilterの設定を怠り、信頼できないユーザーアカウントがある場合にのみ発生する可能性があります... 。 」
- CVE-2017-5638：「ApacheStruts 2のJakartaマルチパートパーサー2.3.32より前の2.3.xおよび2.5.10.1より前の2.5.xでは、ファイルのアップロード試行中に誤った例外処理とエラーメッセージが生成されるため、リモートの攻撃者が許可されます 2017年3月に実際に悪用されたように、細工された[特定のヘッダー]を介して任意のコマンドを実行する。 。 」

### Pilot Results

<details><summary>原文</summary><div>

For each of the nine CVEs, six analysts rated the priority of the vulnerability as both a supplier and deployer.
Table 13 summarizes the results by reporting the inter-rater agreement for each decision point.
For all measures, agreement (κ) is above zero, which is generally interpreted as some agreement among analysts.
Below zero is interpreted as noise or discord.
Closer to 1 indicates more or stronger agreement.

How close κ should be to 1 before agreement can be considered strong enough or reliable enough is a matter of some debate.
The value certainly depends on the number of options among which analysts select.
For those decision points with five options (mission and safety impact), agreement is lowest.
Although portfolio value has a higher κ than mission or safety impact, it may not actually have higher agreement because portfolio value only has two options.
The results for portfolio value are nearly indistinguishable as far as level of statistical agreement from mission impact and safety impact.
The statistical community does not have hard and fast rules for cut lines on adequate agreement.
We treat κ as a descriptive statistic rather than a test statistic.

Table 13 is encouraging, though not conclusive.
κ<0 is a strong sign of discordance.
Although it is unclear how close to 1 is success, κ<0 would be clear sign of failure.
In some ways, these results may be undercounting the agreement for SSVC as presented.
These results are for SSVC prior to the improvements documented in Improvement Instigated by the Pilot, which are implemented in SSVC version 1.
On the other hand, the participant demographics may inflate the inter-rater agreement based on shared tacit understanding through the process of authorship.
The one participant who was not an author surfaced two places where this was the case, but we expect the organizational homogeneity of the participants has inflated the agreement somewhat.
The anecdotal feedback from vulnerability managers at several organizations (including VMware (Akbar 2020) and McAfee) is about refinement and tweaks, not gross disagreement.
Therefore, while further refinement is necessary, this evidence suggests the results have some transferability to other organizations and are not a total artifact of the participant organization demographics.
</div></details>

9つのCVEのそれぞれについて、6人のアナリストが脆弱性の優先度をサプライヤーとデプロイヤーの両方として評価しました。
表13は、各決定ポイントの評価者間合意を報告することにより、結果をまとめたものです。
すべての測定値について、合意（κ）はゼロを上回っています。これは通常、アナリスト間の合意と解釈されます。
ゼロ未満は、ノイズまたは不一致として解釈されます。
1に近いほど、一致が多いか強いことを示します。

合意が十分に強力または十分に信頼できると見なされる前に、κが1にどれだけ近いかは、いくつかの議論の問題です。
値は確かにアナリストが選択するオプションの数に依存します。
5つのオプション（ミッションと安全性への影響）がある決定ポイントの場合、合意は最も低くなります。
ポートフォリオの価値は、ミッションや安全性への影響よりもκが高くなりますが、ポートフォリオの価値には2つの選択肢しかないため、実際には高い合意が得られない場合があります。
ポートフォリオの価値の結果は、統計的合意のレベルがミッションの影響および安全性の影響とほとんど区別できません。
統計コミュニティには、適切な合意に基づくカットラインに関する厳格なルールがありません。
κを検定統計量ではなく記述統計量として扱います。

表13は、決定的なものではありませんが、有望です。
κ<0は不一致の強い兆候です。
1にどれだけ近いかは不明ですが、κ<0は明らかに失敗の兆候です。
ある意味で、これらの結果は、提示されたSSVCの合意を過小評価している可能性があります。
これらの結果は、SSVCバージョン1で実装されている、パイロットによって開始された改善に記載されている改善前のSSVCに関するものです。
一方、参加者の人口統計は、著者のプロセスを通じて共有された暗黙の理解に基づいて、評価者間合意を膨らませる可能性があります。
著者ではない1人の参加者は、これが当てはまる2つの場所に浮上しましたが、参加者の組織の均質性により、合意がいくらか膨らんだと予想されます。
いくつかの組織（VMware（Akbar 2020）やMcAfeeを含む）の脆弱性マネージャーからの逸話的なフィードバックは、全体的な不一致ではなく、改良と調整に関するものです。
したがって、さらなる改善が必要ですが、この証拠は、結果が他の組織にある程度転送可能であり、参加組織の人口統計の完全な成果物ではないことを示唆しています。

Table 16: Inter-Rater Agreement for Decision Points

| Safety Impact | ExploitationTechnical Impact | Portfolio Value | Mission Impact | Exposure | Dev Result | Deployer Result |
| --- | --- | --- | --- | --- | --- | --- |
| Fleiss’ κ | 0.122 | 0.807 | 0.679 | 0.257 | 0.146 | 0.480 | 0.226 | 0.295 |
| Disagreement range | 2,4 | 1,2 | 1,1 | 1,1 | 2,4 | 1,2 | 1,3 | 2,3 |


<details><summary>原文</summary><div>

For all decision points, the presumed goal is for κ to be close or equal to 1.
The statistics literature has identified some limited cases in which Fleiss’ k behaves strangely—for example it is lower than expected when raters are split between 2 of q ratings when q>2 (Falotico and Quatto 2015).
This paradox may apply to the safety and mission impact values, in particular.
The paradox would bite hardest if the rating for each vulnerability was clustered on the same two values, for example, minor and major.
Falotico and Quatto’s proposed solution is to permute the columns, which is safe with unordered categorical data.
Since the nine vulnerabilities do not have the same answers as each other (that is, the answers are not clustered on the same two values), we happen to avoid the worst of this paradox, but the results for safety impact and mission impact should be interpreted with some care.

This solution identifies another difficulty of Fleiss’ kappa, namely that it does not preserve any order; none and catastrophic are considered the same level of disagreement as none and minor.
Table 13 displays a sense of the range of disagreement to complement this weakness.
This value is the largest distance between rater selections on a single vulnerability out of the maximum possible distance.
So, for safety impact, the most two raters disagreed was by two steps (none to major, minor to hazardous, or major to catastrophic) out of the four possible steps (none to catastrophic).
The only values of κ that are reliably comparable are those with the same number of options (that is, the same maximum distance).
In other cases, closer to 1 is better, but how close is close enough to be considered “good” changes.
In all but one case, if raters differed by two steps then there were raters who selected the central option between them.
The exception was mission impact for CVE-201814781; it is unclear whether this discrepancy should be localized to a poor test scenario description, or to SSVC’s mission impact definition.
Given it is an isolated occurrence, we expect the scenario description at least partly.

Nonetheless, κ provides some way to measure improvement on this a conceptual engineering task.
The pilot evaluation can be repeated, with more diverse groups of stakeholders after the descriptions have been refined by stakeholder input, to measure fit to this goal.
For a standard to be reliably applied across different analyst backgrounds, skill sets, and cultures, a set of decision point descriptions should ideally achieve κ of 1 for each item in multiple studies with diverse participants.
Such a high level of agreement would be difficult to achieve, but it would ensure that when two analysts assign a priority with the system that they get the same answer.
Such agreement is not the norm with CVSS currently (Allodi et al. 2018).
</div></details>

すべての決定点について、推定される目標は、κが1に近いか等しいことです。
統計の文献では、Fleissのkが奇妙に動作するいくつかの限られたケースが特定されています。たとえば、q> 2のときに評価者がq評価の2つに分割された場合、予想よりも低くなります（Falotico and Quatto2015）。
このパラドックスは、特に安全性とミッションへの影響の値に当てはまる可能性があります。
各脆弱性の評価が同じ2つの値（マイナーとメジャーなど）にクラスター化されている場合、パラドックスは最も深刻になります。
FaloticoとQuattoが提案するソリューションは、列を並べ替えることです。これは、順序付けされていないカテゴリデータで安全です。
9つの脆弱性は互いに同じ答えを持っていないため（つまり、答えは同じ2つの値にクラスター化されていない）、このパラドックスの最悪の事態を回避できますが、安全性への影響とミッションへの影響の結果は次のようになります。慎重に解釈されます。

このソリューションは、フライスのκ係数のもう1つの難しさ、つまり順序​​を保持しないことを示しています。 noneと壊滅的は、noneおよびminorと同じレベルの不一致と見なされます。
表13は、この弱点を補完するための不一致の範囲の感覚を示しています。
この値は、可能な最大距離のうち、単一の脆弱性に対する評価者の選択間の最大距離です。
したがって、安全性への影響について、意見が一致しなかった評価者のほとんどは、考えられる4つのステップ（なしから壊滅的）のうち2つのステップ（なしからメジャー、マイナーから危険、またはメジャーから壊滅的）でした。
確実に比較できるκの値は、オプションの数が同じ（つまり、最大距離が同じ）の値だけです。
他の場合では、1に近い方が良いですが、「良い」変化と見なされるのに十分近い距離です。
1つのケースを除くすべてのケースで、評価者が2つのステップで異なる場合、それらの間の中央オプションを選択した評価者がいました。
例外は、CVE-2018-14781のミッションへの影響でした。この不一致を、不十分なテストシナリオの説明に限定する必要があるのか​​、SSVCのミッション影響の定義に限定するのかは不明です。
それが孤立した出来事であることを考えると、シナリオの説明は少なくとも部分的に期待されます。

それにもかかわらず、κはこの概念的なエンジニアリングタスクの改善を測定するための何らかの方法を提供します。
パイロット評価は、この目標への適合性を測定するために、説明が利害関係者の入力によって洗練された後、より多様な利害関係者のグループで繰り返すことができます。
さまざまなアナリストのバックグラウンド、スキルセット、および文化に確実に適用される標準の場合、一連の決定ポイントの説明は、多様な参加者による複数の調査で、各項目のκを1にするのが理想的です。
このような高レベルの合意を達成することは困難ですが、2人のアナリストがシステムに優先順位を割り当てたときに、同じ回答が得られるようにすることができます。
このような合意は、現在CVSSとの標準ではありません（Allodi et al.2018）。

Table 17: SSVC pilot scores compared with the CVSS base scores for the vulnerabilities provided by NVD.

| CVE-ID | Representative SSVC decision values | SSVC recommendation (supplier, deployer) | NVD’s CVSS base score |
| --- | ---- | --- | --- |
| CVE-2014-0751 | E:N/T:T/U:L/S:H/X:C/M:C | (Sched, OOC) | 7.5 (High) (v2) |
| CVE-2015-1014 | E:N/T:T/U:L/S:J/X:S/M:F | (Sched, Sched) | 7.3 (High) (v3.0) |
| CVE-2015-5374 | E:A/T:P/U:L/S:H/X:C/M:F | (Immed, Immed) | 7.8 (High) (v2) |
| CVE-2017-3183 | E:N/T:T/U:E/S:M/X:C/M:C | (Sched, Sched) | 8.8 (High) (v3.0) |
| CVE-2017-5638 | E:A/T:T/U:S/S:M/X:U/M:C | (Immed, OOC) | 10.0 (Critical) (v3.0) |
| CVE-2017-9590 | E:P/T:T/U:E/S:M/X:U/M:D | (OOC, Sched) | 5.9 (Medium) (v3.0) |
| CVE-2018-14781| E:P/T:P/U:L/S:H/X:C/M:F | (OOC, OOC) | 5.3 (Medium) (v3.0) |
| CVE-2019-2691 | E:N/T:P/U:E/S:M/X:C/M:C | (Sched, Sched) | 4.9 (Medium) (v3.0) |
| CVE-2019-9042 | E:A/T:T/U:L/S:N/X:C/M:C | (OOC, Sched) | 7.2 (High) (v3.0) |

<details><summary>原文</summary><div>

Table 14 presents the mode decision point value for each vulnerability tested, as well as the recommendation that would result from that set based on the recommended decision trees in SSVC version 1.
The comparison with the NVD’s CVSS base scores mostly confirms that SSVC is prioritizing based on different criteria, as designed.
In particular, differences in the state of exploitation and safety impact are suggestive.

Based on these results, we made about ten changes, some bigger than others.
We did not execute a new rater agreement experiment with the updated descriptions.
The pilot results are encouraging, and we believe it is time to open up a wider community discussion.
</div></details>

表14は、テストされた各脆弱性のモード決定ポイント値と、SSVCバージョン1の推奨決定木に基づいてそのセットから得られる推奨値を示しています。
NVDのCVSS基本スコアとの比較により、SSVCが設計どおりにさまざまな基準に基づいて優先順位を付けていることがほとんど確認されます。
特に、搾取の状態と安全への影響の違いは示唆的です。

これらの結果に基づいて、約10の変更を行いましたが、一部は他よりも大きくなっています。
更新された説明を使用して、新しい評価者合意実験を実行しませんでした。
パイロットの結果は心強いものであり、より幅広いコミュニティの議論を開く時が来たと私たちは信じています。

### Improvements Instigated by the Pilot

<details><summary>原文</summary><div>

The following changes were reflected in the version 1 Section "Decision Trees for Vulnerability Management."

- Technical impact: We clarified that partial/total is decided regarding the system scope definition, which considers a database or a web server program as the “whole” system. Furthermore, “total” also includes any technical impact that exposes authentication credentials to the adversary, if those credentials are to the whole system.
- We added advice for information gathering to answer safety impact and mission impact questions.  This change is needed because of the particularly wide variety of background assumptions analysts made that influenced results and agreement.
- We clarified that “MEF failure” refers to any one essential function failing, not failure of all of them. We changed most severe mission impact to “mission failure” to better reflect the relationship between MEFs and the organization’s mission.
- We removed the “supplier portfolio value” question since it had poor agreement, and there is no clear way to correct it. We replaced this question with Utility, which better captures the relevant kinds of value (namely, to the adversary) of the affected component while remaining amenable to pragmatic analysis.
- We clarified that “proof of concept” (see Exploitation) includes cases in which existing tooling counts as a PoC. The examples listed are suggestive, not exhaustive.
- We reorganized the decision trees based on which items are easier to gather information for or which ones have a widely verifiable state. This change moved exploitation to the first question.
- We changed the decision tree results such that if exposure is “small,” then the resulting priority is lower than before the pilot study. That is, “small” exposure has a stronger effect on reducing urgency.
</div></details>

以下の変更は、バージョン1のセクション「脆弱性管理の決定木」に反映されています。

- 技術的影響：データベースまたはWebサーバープログラムを「システム全体」と見なすシステムスコープ定義に関して、部分的/全体的に決定されることを明確にしました。さらに、「合計」には、認証クレデンシャルがシステム全体に対するものである場合に、認証クレデンシャルを攻撃者に公開する技術的影響も含まれます。
- 安全への影響とミッションへの影響に関する質問に答えるための情報収集に関するアドバイスを追加しました。この変更が必要なのは、アナリストが結果と合意に影響を与えた背景の仮定が特に多様であるためです。
- 「MEF障害」とは、すべての機能の障害ではなく、1つの重要な機能の障害を指すことを明確にしました。 MEFと組織のミッションとの関係をより適切に反映するために、最も深刻なミッションの影響を「ミッションの失敗」に変更しました。
- 合意が不十分であり、それを修正する明確な方法がないため、「サプライヤーポートフォリオの価値」の質問を削除しました。この質問をユーティリティに置き換えました。ユーティリティは、影響を受けるコンポーネントの関連する種類の値（つまり、敵対者）をより適切にキャプチャし、実用的な分析を行います。
- 「概念実証」（活用を参照）には、既存のツールがPoCとしてカウントされる場合が含まれることを明確にしました。リストされている例は示唆的なものであり、網羅的なものではありません。
- 情報収集が容易な項目、または広く検証可能な状態の項目に基づいて、決定木を再編成しました。この変更により、悪用が最初の質問に移りました。
- 露出が「小さい」場合、結果の優先度がパイロット調査前よりも低くなるように、決定木の結果を変更しました。つまり、「小さな」露出は緊急性を減らすのにより強い効果があります。

### Questions Removed as Ineffective

<details><summary>原文</summary><div>

In this section, we present ideas we tried but rejected for various reasons.
We are not presenting this section as the final word on excluding these ideas, but we hope the reasons for excluding them are instructive, will help prevent others from re-inventing the proverbial wheel, and can guide thinking on future work.

Initially, we brainstormed approximately 12 potential decision points, most of which we removed early in our development process through informal testing.
These decision points included adversary’s strategic benefit of exploiting the vulnerability, state of legal or regulatory obligations, cost of developing remediation, patch distribution readiness, financial losses to customers due to potential exploitation, and business losses to the deployer.

Some of these points left marks on other decision points.
The decision point “financial losses of customers” led to an amendment of the definition of Safety to include “well-being,” such that, for example, bankruptcies of third parties are now a major safety impact.
The “business losses to the deployer” decision point is covered as a mission impact insofar as profit is a mission of publicly traded corporations.
Three of the above decision points left no trace on the current system.
“State of legal or regulatory obligations,” “cost of developing remediation,” and “patch distribution readiness” were dropped as either being too vaguely defined, too high level, or otherwise not within the scope of decisions by the defined stakeholders.
The remaining decision point, “adversary’s strategic benefit of exploiting the vulnerability,” transmuted to a different sense of system value.
In an attempt to be more concrete and not speculate about adversary motives, we considered a different sense of value: supplier portfolio value.

The only decision point that we have removed following the pilot is developer portfolio value.
This notion of value was essentially an over-correction to the flaws identified in the “adversary’s strategic benefit of exploiting the vulnerability” decision point.
“Supplier portfolio value” was defined as “the value of the affected component as a part of the developer’s product portfolio.
Value is some combination of importance of a given piece of software, number of deployed instances of the software, and how many people rely on each.
The developer may also include lifecycle stage (early development, stable release, decommissioning, etc.) as an aspect of value.”
It had two possible values: low and high.
As Table 13 demonstrates, there was relatively little agreement among the six analysts about how to evaluate this decision point.
We replaced this sense of portfolio value with Utility, which combines Value Density and Automatability.
</div></details>

このセクションでは、私たちが試したがさまざまな理由で拒否したアイデアを紹介します。
これらのアイデアを除外する最後の言葉としてこのセクションを提示することはありませんが、それらを除外する理由が有益であり、他の人がことわざの輪を再発明するのを防ぎ、将来の仕事について考えるのに役立つことを願っています。

最初に、約12の潜在的な決定ポイントについてブレインストーミングを行いましたが、そのほとんどは、開発プロセスの早い段階で非公式のテストを通じて削除しました。
これらの決定ポイントには、脆弱性を悪用することによる敵対者の戦略的利益、法的または規制上の義務の状態、修復の開発コスト、パッチ配布の準備、潜在的な悪用による顧客への経済的損失、および展開者へのビジネス上の損失が含まれていました。

これらのポイントのいくつかは、他の決定ポイントに痕跡を残しました。
「顧客の経済的損失」という決定点により、安全性の定義が「幸福」を含むように修正され、たとえば、第三者の破産が安全性に大きな影響を与えるようになりました。
「展開者へのビジネス上の損失」の決定ポイントは、利益が上場企業の使命である限り、使命の影響としてカバーされます。
上記の決定ポイントのうちの3つは、現在のシステムに痕跡を残しませんでした。
「法的または規制上の義務の状態」、「修復の開発コスト」、および「パッチ配布の準備」は、定義が曖昧すぎるか、レベルが高すぎるか、または定義された利害関係者による決定の範囲内にないために削除されました。
残りの決定ポイントである「脆弱性を悪用することによる攻撃者の戦略的利益」は、システム価値の異なる感覚に変わりました。
より具体的で、敵の動機について推測しないようにするために、私たちは別の価値観、つまりサプライヤーポートフォリオの価値を検討しました。

パイロット後に削除した唯一の決定ポイントは、開発者ポートフォリオの価値です。
この価値の概念は、本質的に、「脆弱性を悪用することによる攻撃者の戦略的利益」の決定ポイントで特定された欠陥に対する過剰な修正でした。
「サプライヤーポートフォリオの価値」は、「開発者の製品ポートフォリオの一部としての影響を受けるコンポーネントの価値」として定義されました。
価値とは、特定のソフトウェアの重要性、ソフトウェアの展開されたインスタンスの数、およびそれぞれに依存している人の数の組み合わせです。
開発者は、価値の側面としてライフサイクル段階（初期開発、安定したリリース、廃止措置など）を含めることもできます。」
可能な値は、lowとhighの2つでした。
表13が示すように、この決定点を評価する方法について、6人のアナリストの間で比較的ほとんど合意がありませんでした。
このポートフォリオの価値観を、価値密度と自動化性を組み合わせたユーティリティに置き換えました。

## Worked Example

<details><summary>原文</summary><div>

As an example, we will evaluate CVE-2018-14781 step by step from the deployer point of view.
The scenario here is that used for the pilot study. This example uses the SSVC version 1 deployer decision tree.

The analyst’s first question is related to exploitation.
Technically, one could answer the questions in any order; however, exploitation is a good starting point because given an adequately defined search procedure, one can always answer whether it finds an available exploit or proof of concept.
The scenario description for the pilot study reads as follows:

- **State of exploitation**: Metasploit and ExploitDB do not return results for this vulnerability. The NVD does not report any active exploitation of this vulnerability.

This information rules out “active” given the (perhaps limited) search procedure. While the search did not produce a precise PoC, based on the description of the vulnerability, it is a fairly standard traffic capture and replay attack that, given access to the transmission medium, should be straightforward to conduct with Wireshark. Therefore, we select the “PoC” branch and then ask about exposure. This considers the (fictional) deployer scenario blurb and the notional deployment of the affected system, as follows.

- Scenario blurb: We are a hospital that uses Medtronic devices frequently because of their quality and popularity in the market. We give these devices out to clients who need to monitor and track their insulin intake. If clients need to access data on their device, they can physically connect it to their computer or connect via Bluetooth to an app on their phone for monitoring capabilities.  Occasionally, clients who use this device will have a doctor’s appointment in which the doctors have machines that can access the device as well to monitor or change settings. It is unknown how secure the doctor’s computer that interfaces directly with this insulin pump is. If the doctor’s computer is compromised, it potentially means that every device that connects to it is compromised as well. If an update to the insulin pump is required, a client can do this on their own through their computer or app or through a doctor while they are on-site at the hospital.

- Deployment of affected system: These pumps are attached directly to the client. If an update is required, the client is permitted to do that through their own computer or app. However, we have not provided them with documentation on properly using their computer or app to securely access their device. This is done for convenience so that if the user needs to change something quickly, they can. They also can also come to us (hospital) for a change in their device’s settings for dosage etc. The doctor’s computer that directly handles interfacing with these devices is only connected to the intranet for the purpose of updating the client’s settings on the device. Doctors authenticate with ID badge and password.
</div></details>

例として、デプロイヤーの観点からCVE-2018-14781を段階的に評価します。
ここでのシナリオは、パイロット研究に使用されたものです。 この例では、SSVCバージョン1デプロイヤデシジョンツリーを使用しています。

アナリストの最初の質問は、搾取に関するものです。
技術的には、質問には任意の順序で答えることができます。 ただし、適切に定義された検索手順があれば、利用可能なエクスプロイトまたは概念実証を見つけるかどうかを常に答えることができるため、エクスプロイトは良い出発点です。
パイロットスタディのシナリオの説明は次のとおりです。

- **悪用の状態**：MetasploitおよびExploitDBは、この脆弱性の結果を返しません。 NVDは、この脆弱性の積極的な悪用を報告していません。

この情報は、（おそらく限定された）検索手順を考えると「アクティブ」を除外します。脆弱性の説明に基づくと、検索では正確なPoCは生成されませんでしたが、これはかなり標準的なトラフィックキャプチャおよびリプレイ攻撃であり、伝送メディアへのアクセスがあれば、Wiresharkで簡単に実行できます。したがって、「PoC」ブランチを選択してから、露出について質問します。これは、次のように、（架空の）展開シナリオの宣伝文句と影響を受けるシステムの概念的な展開を考慮しています。

- シナリオの宣伝文句：私たちは、市場での品質と人気のためにMedtronic機器を頻繁に使用する病院です。これらのデバイスは、インスリン摂取量を監視および追跡する必要があるクライアントに配布されます。クライアントがデバイス上のデータにアクセスする必要がある場合は、デバイスをコンピューターに物理的に接続するか、Bluetooth経由で電話のアプリに接続して監視機能を利用できます。時折、このデバイスを使用するクライアントは、医師の予約があり、医師はデバイスにアクセスして設定を監視または変更できるマシンを持っています。このインスリンポンプと直接インターフェースする医師のコンピューターがどれほど安全かは不明です。医師のコンピュータが危険にさらされている場合、それに接続するすべてのデバイスも危険にさらされている可能性があります。インスリンポンプの更新が必要な場合、クライアントは自分のコンピューターやアプリを介して、または病院にいる​​間に医師を介して自分でこれを行うことができます。

- 影響を受けるシステムの展開：これらのポンプはクライアントに直接接続されています。更新が必要な場合、クライアントは自分のコンピューターまたはアプリを介して更新を行うことができます。ただし、コンピュータまたはアプリを適切に使用してデバイスに安全にアクセスするためのドキュメントは提供されていません。これは、ユーザーが何かをすばやく変更する必要がある場合に変更できるように、便宜上行われています。また、投与量などのデバイスの設定を変更するために私たち（病院）に来ることもできます。これらのデバイスとのインターフェースを直接処理する医師のコンピューターは、デバイスのクライアントの設定を更新する目的でのみイントラネットに接続されます。医師はIDバッジとパスワードで認証します。

<details><summary>原文</summary><div>

System Exposure is less straightforward than Exploitation.
The option open is clearly ruled out.
However, it is not clear whether the optional Bluetooth connection between the medical device and a phone app represents controlled or small exposure.
The description does not explicitly handle the capture/replay aspect of the vulnerability.
If the only way to exploit the vulnerability is to be within physical transmission range of the device, then that physical constraint argues for exposure being small.
However, if the client’s phone app could be used to capture and replay attack packets, then unless that app is particularly well secured, the answer should be controlled.
Regardless, the answer is not clear from the supplied information.
Furthermore, if this fictional app is specific to the insulin pump, then even if it is not compromised, the attack might use its installation to remotely identify targets.
However, since most of the hospital’s clients have not installed the app, and for nearly all cases, physical proximity to the device is necessary; therefore, we select small and move on to ask about mission impact.

According to the fictional pilot scenario, “Our mission dictates that the first and foremost priority is to contribute to human welfare and to uphold the Hippocratic oath (do no harm).” The continuity of operations planning for a hospital is complex, with many MEFs.
However, even from this abstract, it seems clear that “do no harm” is at risk due to this vulnerability.
A mission essential function to that mission is each of the various medical devices works as expected, or at least if a device fails, it cannot actively be used to inflict harm.
Unsolicited insulin delivery would mean that MEF “fails for a period of time longer than acceptable,” matching the description of MEF failure.
The question is then whether the whole mission fails, which does not seem to be the case.
The recovery of MEF functioning is not affected, and most MEFs (the emergency services, surgery, oncology, administration, etc.) would be unaffected.
Therefore, we select MEF failure and move on to ask about safety impact.

This particular pilot study used SSVC version 1. In the suggested deployer tree for SSVC version 2, mission and safety impact would be used to calculate the overall Human Impact; Utility would need to be answered as well. Conducting further studies with the recommended version 2 Deployer tree remains an area of future work. In the pilot study, this information is conveyed as follows:

• Use of the cyber-physical system: Insulin pumps are used to regulate blood glucose levels in diabetics. Diabetes is extremely common in the US. Misregulation of glucose can cause a variety of problems. Minor misregulation causes confusion or difficulty concentrating. Long-term minor mismanagement causes weigh management issues and blindness. Severe acute mismanagement can lead unconsciousness in a matter of minutes and death in a matter of hours. The impacted insulin pumps have a local (on-patient) wireless control, so wires to the pump do not have to be connected to the patient’s control of the system, making the system lighter and less prone to be ripped out.

The closest match to “death in a matter of hours” would be hazardous because that description reads “serious or fatal injuries, where fatalities are plausibly preventable via emergency services or other measures.”
Depending on the details of the hospital’s contingency plans and its monitoring of their patients, the Safety Impact could be catastrophic.
If there is no way to tell whether the insulin pumps are misbehaving, for example, then exploitation could go on for some time, leading to a catastrophic Safety Impact.
The pilot information is inadequate in this regard, which is the likely source of disagreement about Safety Impact in Table 13.
For the purposes of this example, imagine that after gathering that information, the monitoring situation is adequate, and select hazardous.
Therefore, mitigate this vulnerability out-of-cycle, meaning that it should be addressed quickly, ahead of the usual update and patch cycle.
</div></details>

システムエクスポージャーは、エクスプロイトほど単純ではありません。
オープンオプションは明確に除外されています。
ただし、医療機器と電話アプリの間のオプションのBluetooth接続が、制御された露出を表すのか、それともわずかな露出を表すのかは明らかではありません。
この説明では、脆弱性のキャプチャ/再生の側面を明示的に処理していません。
脆弱性を悪用する唯一の方法がデバイスの物理的な送信範囲内にある場合、その物理的な制約は露出が小さいことを主張します。
ただし、クライアントの電話アプリを使用して攻撃パケットをキャプチャして再生できる場合は、そのアプリが特に安全でない限り、回答を管理する必要があります。
とにかく、提供された情報から答えは明確ではありません。
さらに、この架空のアプリがインスリンポンプに固有のものである場合、侵害されていなくても、攻撃はそのインストールを使用してターゲットをリモートで識別する可能性があります。
ただし、病院のクライアントのほとんどはアプリをインストールしていないため、ほとんどすべての場合、デバイスに物理的に近接している必要があります。したがって、私たちは小さいものを選択し、ミッションの影響について質問します。

架空のパイロットシナリオによると、「私たちの使命は、人間の福祉に貢献し、ヒポクラテスの誓いを守ること（害を及ぼさないこと）を最優先することです。」病院の運営計画の継続性は複雑で、多くのMEFがいます。
ただし、この要約からも、この脆弱性のために「害を及ぼさない」ことが危険にさらされていることは明らかです。
その使命に不可欠な機能は、さまざまな医療機器のそれぞれが期待どおりに機能することです。または、少なくとも機器が故障した場合、それを積極的に使用して危害を加えることはできません。
未承諾のインスリン送達は、MEFが「許容範囲よりも長い期間失敗する」ことを意味し、MEFの失敗の説明と一致します。
問題は、ミッション全体が失敗するかどうかですが、そうではないようです。
MEF機能の回復は影響を受けず、ほとんどのMEF（救急サービス、手術、腫瘍学、管理など）は影響を受けません。
したがって、MEF障害を選択し、安全性への影響について質問します。

この特定のパイロット調査では、SSVCバージョン1を使用しました。SSVCバージョン2の推奨デプロイヤーツリーでは、ミッションと安全性への影響を使用して、全体的な人的影響を計算します。ユーティリティにも回答する必要があります。推奨されるバージョン2のDeployerツリーを使用してさらに調査を行うことは、今後の作業領域のままです。パイロットスタディでは、この情報は次のように伝えられます。

- サイバーフィジカルシステムの使用：インスリンポンプは、糖尿病患者の血糖値を調節するために使用されます。糖尿病は米国では非常に一般的です。ブドウ糖の誤調節は、さまざまな問題を引き起こす可能性があります。軽微な誤調節は、混乱や集中力の低下を引き起こします。長期にわたる軽微な管理ミスは、体重管理の問題と失明を引き起こします。深刻な急性の管理ミスは、数分で意識を失い、数時間で死に至る可能性があります。影響を受けるインスリンポンプはローカル（患者）のワイヤレス制御を備えているため、ポンプへの配線を患者のシステム制御に接続する必要がなく、システムが軽量になり、破れにくくなります。

「数時間での死亡」に最も近い一致は危険です。その説明には、「緊急サービスまたはその他の手段によって死亡を予防できる可能性のある重大または致命的な傷害」と記載されているためです。
病院の緊急時対応計画の詳細と患者の監視によっては、安全性への影響が壊滅的なものになる可能性があります。
たとえば、インスリンポンプが誤動作しているかどうかを判断する方法がない場合、悪用がしばらく続く可能性があり、壊滅的な安全上の影響につながる可能性があります。
パイロット情報はこの点で不十分であり、これが表13の安全性への影響に関する意見の不一致の原因である可能性があります。
この例の目的のために、その情報を収集した後、監視状況が適切であると想像し、危険を選択します。
したがって、この脆弱性をサイクル外で軽減します。つまり、通常の更新とパッチサイクルの前に、迅速に対処する必要があります。

### Related Vulnerability Management Systems

<details><summary>原文</summary><div>

There are several other bodies of work that are used in practice to assist vulnerability managers in making decisions.
Three relevant systems are CVSS (CVSS SIG 2019), EPSS (Jacobs et al.2019), and Tenable’s Vulnerability Priority Rating (VPR).
There are other systems derived from CVSS, such as RVSS for robots (Vilches et al.2018) and MITRE’s effort to adapt CVSS to medical devices (Chase and Coley 2019).
There are also other nascent efforts to automate aspects of the decision making process, such as vPrioritizer.
This section discusses the relationship between these various systems and SSVC.
</div></details>

脆弱性管理者が意思決定を行うのを支援するために実際に使用される作業は他にもいくつかあります。
関連する3つのシステムは、CVSS（CVSS SIG 2019）、EPSS（Jacobs et al.2019）、およびTenableの脆弱性優先度評価（VPR）です。
ロボット用のRVSS（Vilches et al.2018）やCVSSを医療機器に適応させるMITREの取り組み（Chase and Coley 2019）など、CVSSから派生した他のシステムがあります。
vPrioritizerなど、意思決定プロセスの側面を自動化するための他の初期の取り組みもあります。
このセクションでは、これらのさまざまなシステムとSSVCの関係について説明します。

### CVSS

<details><summary>原文</summary><div>

CVSS version 3.1 has three metric groups: base, environmental, and temporal.
The metrics in the base group are all required, and are the only required metrics.
In connection with this design, CVSS base scores and base metrics are far and away the most commonly used and communicated.
A CVSS base score has two parts: the exploitability metrics and the impact metrics.
Each of these are echoed or reflected in aspects of SSVC, though the breadth of topics considered by SSVC is wider than CVSS version 3.1.

How CVSS is used matters.
Using just the base scores, which are “the intrinsic characteristics of a vulnerability that are constant over time and across user environments,” as a stand-alone prioritization method is not recommended (CVSS SIG 2019).
Two examples of this include the U.S.government (see Scarfone et al.2008, 7–4; Souppaya and Scarfone 2013, 4; and Cybersecurity and Infrastructure Security Agency 2015) and the global payment card industry (PCI Security Standards Council 2017) where both have defined such misuse as expected practice in their vulnerability management requirements.
CVSS scores have a complex relationship with patch deployment in situations where it is not mandated, at least in an ICS context (Wang et al.2017).

CVSS has struggled to adapt to other stakeholder contexts.
Various stakeholder groups have expressed dissatisfaction by making new versions of CVSS, such as medical devices (Chase and Coley 2019), robotics (Vilches et al. 2018), and industrial systems (Figueroa-Lorenzo, Añorga, and Arrizabalaga 2020).
In these three examples, the modifications tend to add complexity to CVSS by adding metrics.
Product vendors have varying degrees of adaptation of CVSS for development prioritization, including but not limited to Red Hat, Microsoft, and Cisco.
The vendors codify CVSS’s recommended qualitative severity rankings in different ways, and Red Hat and Microsoft make the user interaction base metric more important.
</div></details>

CVSSバージョン3.1には、基本、環境、および時間の3つのメトリックグループがあります。
基本グループのメトリックはすべて必須であり、必須のメトリックのみです。
この設計に関連して、CVSSの基本スコアと基本メトリックは、最も一般的に使用され、伝達されています。
CVSSの基本スコアには、悪用可能性メトリックと影響メトリックの2つの部分があります。
SSVCで検討されるトピックの幅はCVSSバージョン3.1よりも広いですが、これらのそれぞれはSSVCの側面に反映または反映されます。

CVSSの使用方法が重要です。
スタンドアロンの優先順位付け方法として、「時間の経過とともにユーザー環境全体で一定である脆弱性の固有の特性」である基本スコアのみを使用することはお勧めしません（CVSS SIG2019）。
この2つの例には、米国政府（Scarfone et al.2008、7–4; Souppaya and Scarfone 2013、4;およびCyber​​security and Infrastructure Security Agency 2015を参照）とグローバルペイメントカード業界（PCI Security Standards Council 2017）が含まれます。脆弱性管理要件で予想される慣行としてそのような誤用を定義しました。
CVSSスコアは、少なくともICSのコンテキストでは、パッチの展開が義務付けられていない状況では、パッチの展開と複雑な関係があります（Wang et al.2017）。

CVSSは、他の利害関係者の状況に適応するのに苦労しています。
さまざまな利害関係者グループが、医療機器（Chase and Coley 2019）、ロボット工学（Vilches et al。2018）、産業システム（Figueroa-Lorenzo、Añorga、Arrizabalaga 2020）などの新しいバージョンのCVSSを作成することで不満を表明しています。
これらの3つの例では、変更によってメトリックが追加され、CVSSが複雑になる傾向があります。
製品ベンダーは、Red Hat、Microsoft、Ciscoなど、開発の優先順位付けのためにCVSSをさまざまな程度で適応させています。
ベンダーは、CVSSが推奨する定性的重大度ランキングをさまざまな方法で体系化しており、Red HatとMicrosoftは、ユーザーインタラクションの基本メトリックをより重要にしています。

#### Exploitability metrics (Base metric group)

<details><summary>原文</summary><div>

The four metrics in this group are Attack Vector, Attack Complexity, Privileges Required, and User Interaction.
This considerations may likely be involved in the Automatability decision point.
If Attack Vector = Network and Privileges Required = None, then the delivery phase of the kill chain is likely to be automatable.
Attack Vector may also be correlated with the Exposure decision point.
Attack Complexity may influence how long it may take an adversary to craft an automated exploit, but Automatability only asks whether exploitation can be automated, not how difficult it was.
However, Attack Complexity may influence the weaponization phase of the kill chain.
User Interaction does not cleanly map to a decision point.
In general, SSVC does not care whether a human is involved in exploitation of the vulnerability or not.
Some human interaction is for all intents and purposes automatable by attackers: most people click on links in emails as part of their normal processes.
In most such situations, user interaction does not present a firm barrier to automatability; it presents a stochastic barrier.
Automatability is written to just consider firm barriers to automation.

Automatability includes considerations that are not included in the exploitability metrics.
Most notably the concept of vulnerability chaining is addressed in Automatability but not addressed anywhere in CVSS.
Automatability is also outcomes focused.
A vulnerability is evaluated based on an observable outcome of whether the first four steps of the kill chain can be automated for it.
A proof of automation in a relevant environment is an objective evaluation of the score in a way that cannot be provided for some CVSS elements, such as Attack Complexity.
</div></details>

このグループの4つのメトリックは、攻撃ベクトル、攻撃の複雑さ、必要な特権、およびユーザーの相互作用です。
この考慮事項は、自動化の決定ポイントに関係している可能性があります。
攻撃ベクトル=ネットワークおよび必要な特権=なしの場合、キルチェーンの配信フェーズは自動化できる可能性があります。
攻撃ベクトルは、露出決定ポイントと相関している場合もあります。
攻撃の複雑さは、攻撃者が自動化されたエクスプロイトを作成するのにかかる時間に影響を与える可能性がありますが、自動化可能性は、悪用を自動化できるかどうかだけを尋ね、それがどれほど難しいかではありません。
ただし、攻撃の複雑さは、キルチェーンの兵器化フェーズに影響を与える可能性があります。
ユーザーインタラクションは、決定ポイントに明確にマッピングされません。
一般に、SSVCは、人間が脆弱性の悪用に関与しているかどうかを気にしません。
一部の人間の相互作用は、攻撃者が自動化できるすべての意図と目的のためのものです。ほとんどの人は、通常のプロセスの一部として電子メール内のリンクをクリックします。
このようなほとんどの状況では、ユーザーの操作は自動化に対する確固たる障壁にはなりません。それは確率論的障壁を提示します。
自動化可能性は、自動化に対する確固たる障壁を考慮するために作成されています。

自動化可能性には、悪用可能性メトリックに含まれていない考慮事項が含まれます。
最も注目すべきは、脆弱性連鎖の概念は自動化可能性で扱われていますが、CVSSのどこでも扱われていません。
自動化可能性も結果に焦点を当てています。
脆弱性は、キルチェーンの最初の4つのステップを自動化できるかどうかの観察可能な結果に基づいて評価されます。
関連する環境での自動化の証明は、攻撃の複雑さなど、一部のCVSS要素では提供できない方法でスコアを客観的に評価することです。

#### Impact metrics (Base metric group)

<details><summary>原文</summary><div>

The metrics in this group are Confidentiality, Integrity, and Availability.
There is also a loosely associated Scope metric.
The CIA impact metrics are directly handled by Technical Impact.
Scope is a difficult CVSS metric to categorize.
The specification describes it as “whether a vulnerability in one vulnerable component impacts resources in components beyond its security scope” (CVSS SIG 2019).
This is a fuzzy concept.
SSVC better describes this concept by breaking it down into component parts.
The impact of exploitation of the vulnerable component on other components is covered under Mission Impact, public and situated Well-being Impact, and the stakeholder-specific nature where SSVC is tailored to stakeholder concerns.
CVSS addresses some definitions of the scope of CVSS as a whole under the Scope metric definition.
In SSVC, these definitions are in the Scope section.
</div></details>

このグループのメトリックは、機密性、整合性、および可用性です。
緩く関連付けられたスコープメトリックもあります。
CIAの影響メトリックは、TechnicalImpactによって直接処理されます。
スコープは、分類するのが難しいCVSSメトリックです。
仕様では、「1つの脆弱なコンポーネントの脆弱性が、そのセキュリティ範囲を超えてコンポーネントのリソースに影響を与えるかどうか」と説明しています（CVSS SIG2019）。
これはファジーコンセプトです。
SSVCは、この概念を構成要素に分解することで、この概念をより適切に説明します。
脆弱なコンポーネントの悪用が他のコンポーネントに与える影響は、ミッションインパクト、公的および位置付けられたウェルビーイングインパクト、およびSSVCが利害関係者の懸念に合わせて調整されている利害関係者固有の性質でカバーされます。
CVSSは、スコープメトリック定義の下で全体としてCVSSのスコープのいくつかの定義に対応します。
SSVCでは、これらの定義は[Scope](#scope-範囲)セクションにあります。

#### Temporal metric groups

<details><summary>原文</summary><div>

The temporal metric group primarily contains the Exploit Code Maturity metric.
This metric expresses a concept similar to Exploitation.
The main difference is that Exploitation is not optional in SSVC and that SSVC accounts for the observation that most vulnerabilities with CVE-IDs do not have public exploit code (Householder, Chrabaszcz, et al.2020) and are not actively exploited Jacobs et al.(2019).
</div></details>

時間メトリックグループには、主にエクスプロイトコード成熟度メトリックが含まれます。
このメトリックは、悪用と同様の概念を表します。
主な違いは、SSVCではエクスプロイトはオプションではなく、SSVCは、CVE-IDのほとんどの脆弱性に公開エクスプロイトコードがなく（Householder、Chrabaszcz、et al.2020）、積極的にエクスプロイトされていないという観察結果を説明していることです。 （2019）。

#### Environmental metric group

<details><summary>原文</summary><div>

The environmental metric group allows a consumer of a CVSS base score to change it based on their environment.
CVSS needs this functionality because the organizations that produce CVSS scores tend to be what SSVC calls suppliers and consumers of CVSS scores are what SSVC calls deployers.
These two stakeholder groups have a variety of natural differences, which is why SSVC treats them separately.
SSVC does not have such customization as a bolt-on optional metric group because SSVC is stakeholder-specific by design.
</div></details>

環境メトリックグループを使用すると、CVSSベーススコアのコンシューマーは、環境に基づいてスコアを変更できます。
CVSSスコアを生成する組織は、SSVCがサプライヤーと呼ぶ傾向があり、CVSSスコアのコンシューマーは、SSVCがデプロイヤーと呼ぶものであるため、CVSSにはこの機能が必要です。
これらの2つの利害関係者グループにはさまざまな自然の違いがあるため、SSVCはそれらを別々に扱います。
SSVCは設計上利害関係者固有であるため、SSVCにはボルトオンオプションのメトリックグループなどのカスタマイズはありません。

### EPSS

<details><summary>原文</summary><div>

EPSS is an “effort for predicting when software vulnerabilities will be exploited.”
EPSS is currently based on a machine-learning classifier and proprietary IDS alert data from Kenna Security.
While the group has made an effort to make the ML classifier transparent, ML classifiers are not able to provide an intelligible, human-accessible explanation for their behavior (Jonathan M.Spring et al.2019).
The use of proprietary training data makes the system less transparent.

EPSS could be used to inform the Exploitation decision point.
Currently, Exploitation focuses on the observable state of the world at the time of the SSVC decision.
EPSS is about predicting if a transition will occur from the SSVC state of none to active.
A sufficiently high EPSS score could therefore be used as an additional criterion for scoring a vulnerability as active even when there is no observed active exploitation.
</div></details>

EPSSは、「ソフトウェアの脆弱性がいつ悪用されるかを予測するための取り組み」です。
EPSSは現在、機械学習分類器とKennaSecurityの独自のIDSアラートデータに基づいています。
グループはML分類子を透過的にするための努力をしましたが、ML分類子は、その動作についてわかりやすく、人間がアクセスできる説明を提供できません（Jonathan M.Spring et al.2019）。
独自のトレーニングデータを使用すると、システムの透明性が低下します。

EPSSを使用して、悪用の決定ポイントを通知できます。
現在、Exploitationは、SSVC決定時の世界の観測可能な状態に焦点を合わせています。
EPSSは、SSVC状態がない状態からアクティブになる状態への遷移が発生するかどうかを予測することを目的としています。
したがって、十分に高いEPSSスコアは、アクティブな悪用が観察されない場合でも、脆弱性をアクティブとしてスコアリングするための追加の基準として使用できます。

### VPR

<details><summary>原文</summary><div>

VPR is a prioritization product sold by Tenable.
VPR determines the severity level of a vulnerability based on “technical impact and threat.”
Just as Technical Impact in SSVC, technical impact in VPR tracks the CVSS version 3 impact metrics in the base metric group.
The VPR threat component is about recent and future threat activity; it is comparable to Exploitation if EPSS were added to Exploitation.
VPR is therefore essentially a subset of SSVC.
VPR is stylistically methodologically quite different from SSVC.
VPR is based on machine learning models and proprietary data, so the results are totally opaque.
There is no ability to coherently and transparently customize the VPR system.
Such customization is a central feature of SSVC, as described in Tree Construction and Customization Guidance.
</div></details>

VPRは、Tenableが販売する優先製品です。
VPRは、「技術的な影響と脅威」に基づいて脆弱性の重大度を判断します。
SSVCの技術的影響と同様に、VPRの技術的影響は、基本メトリックグループのCVSSバージョン3の影響メトリックを追跡します。
VPR脅威コンポーネントは、最近および将来の脅威アクティビティに関するものです。 EPSSがExploitationに追加された場合、それはExploitationに匹敵します。
したがって、VPRは本質的にSSVCのサブセットです。
VPRは、スタイル的には方法論的にSSVCとはかなり異なります。
VPRは機械学習モデルと独自のデータに基づいているため、結果は完全に不透明です。
VPRシステムを一貫して透過的にカスタマイズする機能はありません。
このようなカスタマイズは、ツリーの構築とカスタマイズのガイダンスで説明されているように、SSVCの中心的な機能です。

### CVSS spin offs

<details><summary>原文</summary><div>

Attempts to tailor CVSS to specific stakeholder groups, such as robotics or medical devices, are are perhaps the biggest single reason we created SSVC.
CVSS is one-size-fits-all by design.
These customization efforts struggle with adapting CVSS because it was not designed to be adaptable to different stakeholder considerations.
The SSVC section Tree Construction and Customization Guidance explains how stakeholders or stakeholder communities can adapt SSVC in a reliable way that still promotes repeatability and communication.
</div></details>

ロボット工学や医療機器などの特定の利害関係者グループに合わせてCVSSを調整する試みは、おそらく私たちがSSVCを作成した最大の理由です。
CVSSは、設計上、万能です。
これらのカスタマイズの取り組みは、さまざまな利害関係者の考慮事項に適応できるように設計されていないため、CVSSの適応に苦労しています。
SSVCセクションのツリー構築とカスタマイズのガイダンスでは、利害関係者または利害関係者のコミュニティが、再現性とコミュニケーションを促進しながら、信頼できる方法でSSVCを適応させる方法について説明しています。

### vPrioritizer

<details><summary>原文</summary><div>

vPrioritizer is an open-source project that attempts to integrate asset management and vulnerablity prioritization.
The software is mostly the asset management aspects.
It currently includes CVSS base scores as the de facto vulnerability prioritization method; however, fundamentally the system is agnostic to prioritization method.
vPrioritizer is an example of a product that is closely associated with vulnerability prioritization, but is not directly about the prioritization method.
In that sense, it is compatible with any of methods mentioned above or SSVC.
However, SSVC would be better suited to address vPrioritizer’s broad spectrum asset management data.
For example, vPrioritizer aims to collect data points on topics such as asset significance.
Asset significance could be expressed through the SSVC decision points of Mission Impact and situated Well-being Impact, but it does not have a ready expression in CVSS, EPSS, or VPR.
</div></details>

vPrioritizerは、資産管理と脆弱性の優先順位付けを統合しようとするオープンソースプロジェクトです。
ソフトウェアは主に資産管理の側面です。
現在、事実上の脆弱性の優先順位付け方法としてCVSSベーススコアが含まれています。 ただし、基本的に、システムは優先順位付け方法に依存しません。
vPrioritizerは、脆弱性の優先順位付けと密接に関連している製品の例ですが、優先順位付けの方法に直接関係しているわけではありません。
その意味で、上記のいずれかの方法またはSSVCと互換性があります。
ただし、SSVCは、vPrioritizerの幅広い資産管理データに対応するのに適しています。
たとえば、vPrioritizerは、資産の重要性などのトピックに関するデータポイントを収集することを目的としています。
資産の重要性は、ミッションインパクトと位置付けられたウェルビーイングインパクトのSSVC決定ポイントを通じて表現できますが、CVSS、EPSS、またはVPRではすぐに表現できません。

### SSVC using Current Information Sources

<details><summary>原文</summary><div>

Some SSVC decision points can be informed or answered by currently available information feeds or sources.
These include Exploitation, System Exposure, Technical Impact, and Public Safety Impact.
This section provides an overview of some options; we cannot claim it is exhaustive.
Each decision point has a subsection for Gathering Information About it.
These sections provide suggestions that would also contribute to creating or honing information feeds.
However, if there is a category of information source we have not captured, please create an issue on the SSVC GitHub page explaining it and what decision point it informs.

Various vendors provide paid feeds of vulnerabilities that are currently exploited by attacker groups.
Any of these could be used to indicate that active is true for a vulnerability.
Although the lists are all different, we expect they are all valid information sources; the difficulty is matching a list’s scope and vantage with a compatible scope and vantage of the consumer.
We are not aware of a comparative study of the different lists of active exploits; however, we expect they have similar properties to block lists of network touchpoints (Metcalf and Spring 2015) and malware (Kührer, Rossow, and Holz 2014).
Namely, each list has a different view and vantage on the problem, which makes them appear to be different, but each list accurately represents its particular vantage at a point in time.

System Exposure could be informed by the various scanning platforms such as Shodan and Shadowserver.
A service on a device should be scored as open if such a general purpose Internet scan finds that the service responds.
Such scans do not find all open systems, but any system they find should be considered open.
Scanning software, such as the open-source tool Nessus, could be used to scan for connectivity inside an organization to catalogue what devices should be scored controlled if, say, the scan finds them on an internal network where devices regularly connect to the Internet.

Some information sources that were not designed with SSVC in mind can be adapted to work with it.
Three prominent examples are CVSS impact base metrics, CWE, and CPE.
</div></details>

一部のSSVC決定ポイントは、現在利用可能な情報フィードまたはソースによって通知または回答できます。
これらには、悪用、システムへの暴露、技術的影響、および公安への影響が含まれます。
このセクションでは、いくつかのオプションの概要を説明します。網羅的であるとは言えません。
各決定ポイントには、それに関する情報を収集するためのサブセクションがあります。
これらのセクションでは、情報フィードの作成または研ぎ澄ましにも役立つ提案を提供します。
ただし、キャプチャしていない情報ソースのカテゴリがある場合は、SSVC GitHubページで問題を作成して、それとそれが通知する決定ポイントについて説明してください。

さまざまなベンダーが、攻撃者グループによって現在悪用されている脆弱性の有料フィードを提供しています。
これらのいずれかを使用して、脆弱性に対してアクティブが真であることを示すことができます。
リストはすべて異なりますが、すべて有効な情報源であると期待しています。難しいのは、リストの範囲と見晴らしを、互換性のある範囲と消費者の見晴らしと一致させることです。
アクティブなエクスプロイトのさまざまなリストの比較研究については認識していません。ただし、ネットワークタッチポイント（MetcalfおよびSpring 2015）およびマルウェア（Kührer、Rossow、およびHolz 2014）のブロックリストと同様のプロパティがあると予想されます。
つまり、各リストには問題に対する異なる見方と見方があり、異なるように見えますが、各リストはある時点での特定の見晴らしを正確に表しています。

システムエクスポージャーは、ShodanやShadowserverなどのさまざまなスキャンプラットフォームから通知を受けることができます。
そのような汎用インターネットスキャンでサービスが応答することが判明した場合、デバイス上のサービスはオープンとしてスコアリングされる必要があります。
このようなスキャンでは、開いているすべてのシステムが検出されるわけではありませんが、検出されたシステムはすべてオープンであると見なす必要があります。
オープンソースツールのNessusなどのスキャンソフトウェアを使用して、組織内の接続をスキャンし、デバイスが定期的にインターネットに接続している内部ネットワークでデバイスを検出した場合に、どのデバイスをスコアリング制御するかをカタログ化できます。

SSVCを念頭に置いて設計されていない一部の情報ソースは、SSVCで動作するように適合させることができます。
3つの顕著な例は、CVSS影響ベースメトリック、CWE、およびCPEです。

<details><summary>原文</summary><div>

Technical Impact is directly related to the CVSS impact metric group.
However, this metric group cannot be directly mapped to Technical Impact in CVSS version 3 because of the Scope metric.
Technical Impact is only about adversary control of the vulnerable component.
If the CVSS version 3 value of “Scope” is “Changed,” then the impact metrics are the maximum of the impact on the vulnerable component and other components in the environment.
If confidentiality, integrity, and availability metrics are all “high” then Technical Impact is total, as long as the impact metrics in CVSS are clearly about just the vulnerable component.
However, the other values of the CVSS version 3 impact metrics cannot be mapped directly to partial because of CVSS version 3.1 scoring guidance.
Namely, “only the increase in access, privileges gained, or other negative outcome as a result of successful exploitation should be considered” (CVSS SIG 2019).
The example given is that if an attacker already has read access, but gains all other access through the exploit, then read access didn’t change and the confidentiality metric score should be “None” .
However, in this case, SSVC would expect the decision point to be evaluated as total because as a result of the exploit the attacker gains total control of the device, even though they started with partial control.

As mentioned in the discussion of Exploitation, CWE could be used to inform one of the conditions that satisfy proof of concept.
For some classes of vulnerabilities, the proof of concept is well known because the method of exploitation is already part of open-source tools.
For example, on-path attacker scenarios for intercepting TLS certificates.
These scenarios are a cluster of related vulnerabilities.
Since CWE classifies clusters of related vulnerabilities, the community could likely curate a list of CWE-IDs for which this condition of well known exploit technique is satisfied.
Once that list were curated, it could be used to automatically populate a CVE-ID as proof of concept if the CWE-ID of which it is an instance is on the list.
Such a check could not be exhaustive, since there are other conditions that satisfy proof of concept.
If paired with automatic searches for exploit code in public repositories, these checks would cover many scenarios.
If paired with active exploitation feeds discussed above, then the value of Exploitation could be determined almost entirely from available information without direct analyst involvement at each organization.

CPE could possibly be curated into a list of representative Public Safety Impact values for each platform or product.
The Situated Safety Impact would be too specific for a classification as broad as CPE.
But it might work for Public Safety Impact, since it is concerned with a more general assessment of usual use of a component.
Creating a mapping between CPE and Public Safety Impact could be a community effort to associate a value with each CPE entry, or an organization might label a fragment of the CPE data with Public Safety Impact based on the platforms that the supplier needs information about most often.
</div></details>

一部のSSVC決定ポイントは、現在利用可能な情報フィードまたはソースによって通知または回答できます。
これらには、悪用、システムへの暴露、技術的影響、および公安への影響が含まれます。
このセクションでは、いくつかのオプションの概要を説明します。網羅的であるとは言えません。
各決定ポイントには、それに関する情報を収集するためのサブセクションがあります。
これらのセクションでは、情報フィードの作成または研ぎ澄ましにも役立つ提案を提供します。
ただし、キャプチャしていない情報ソースのカテゴリがある場合は、SSVC GitHubページで問題を作成して、それとそれが通知する決定ポイントについて説明してください。

さまざまなベンダーが、攻撃者グループによって現在悪用されている脆弱性の有料フィードを提供しています。
これらのいずれかを使用して、脆弱性に対してアクティブが真であることを示すことができます。
リストはすべて異なりますが、すべて有効な情報源であると期待しています。難しいのは、リストの範囲と見晴らしを、互換性のある範囲と消費者の見晴らしと一致させることです。
アクティブなエクスプロイトのさまざまなリストの比較研究については認識していません。ただし、ネットワークタッチポイント（MetcalfおよびSpring 2015）およびマルウェア（Kührer、Rossow、およびHolz 2014）のブロックリストと同様のプロパティがあると予想されます。
つまり、各リストには問題に対する異なる見方と見方があり、異なるように見えますが、各リストはある時点での特定の見晴らしを正確に表しています。

システムエクスポージャーは、ShodanやShadowserverなどのさまざまなスキャンプラットフォームから通知を受けることができます。
そのような汎用インターネットスキャンでサービスが応答することが判明した場合、デバイス上のサービスはオープンとしてスコアリングされる必要があります。
このようなスキャンでは、開いているすべてのシステムが検出されるわけではありませんが、検出されたシステムはすべてオープンであると見なす必要があります。
オープンソースツールのNessusなどのスキャンソフトウェアを使用して、組織内の接続をスキャンし、デバイスが定期的にインターネットに接続している内部ネットワークでデバイスを検出した場合に、どのデバイスをスコアリング制御するかをカタログ化できます。

SSVCを念頭に置いて設計されていない一部の情報ソースは、SSVCで動作するように適合させることができます。
3つの顕著な例は、CVSS影響ベースメトリック、CWE、およびCPEです。

### Potential Future Information Feeds

<details><summary>原文</summary><div>

So far, we have identified information sources that can support scalable decision making for most decision points.
Some sources, such as CWE or existing asset management solutions, would require a little bit of connective glue to support SSVC, but not too much.
The SSVC decision point that we have not identified an information source for is Utility.
Utility is composed of Automatable and Value Density, so the question is what a sort of feed could support each of those decision points.

A feed is plausible for both of these decision points.
The values for Automatable and Value Density are both about the relationship between a vulnerability, the attacker community, and the aggregate state of systems connected to the Internet.
While that is a broad analysis frame, it means that any community that shares a similar set of adversaries and a similar region of the Internet can share the same response to both decision points.
An organization in the People’s Republic of China may have a different view than an organization in the United States, but most organizations within each region should should have close enough to the same view to share values for Automatable and Value Density.
These factors suggest a market for an information feed about these decision points is a viable possibility.

At this point, it is not clear that an algorithm or search process could be designed to automate scoring Automatable and Value Density.
It would be a complex natural language processing task.
Perhaps a machine learning system could be designed to suggest values.
But more likely, if there is a market for this information, a few analysts could be paid to score vulnerabilities on these values for the community.

Supporting such analysts with further automation could proceed by small incremental improvements.
For example, perhaps information about whether the Reconnaissance step in the kill chain is Automatable or not could be automatically gathered from Internet scanning firms such as Shodan or Shadowserver.
This wouldn’t make a determination for an analyst, but would be a step towards automatic assessment of the decision point.
</div></details>

これまで、ほとんどの意思決定ポイントでスケーラブルな意思決定をサポートできる情報ソースを特定してきました。
CWEや既存の資産管理ソリューションなどの一部のソースでは、SSVCをサポートするために少しの接続接着剤が必要になりますが、それほど多くは必要ありません。
情報源を特定していないSSVCの決定ポイントはユーティリティです。
ユーティリティは自動化可能密度と値密度で構成されているため、問題は、どのような種類のフィードがこれらの各決定ポイントをサポートできるかということです。

フィードは、これらの決定ポイントの両方にもっともらしいです。
AutomatableとValueDensityの値はどちらも、脆弱性、攻撃者コミュニティ、およびインターネットに接続されているシステムの全体的な状態の間の関係に関するものです。
これは広範な分析フレームですが、同様の敵対者のセットとインターネットの同様の地域を共有するコミュニティは、両方の決定ポイントに対して同じ応答を共有できることを意味します。
中華人民共和国の組織は、米国の組織とは異なる見解を持っている可能性がありますが、各地域内のほとんどの組織は、自動化可能および価値密度の値を共有するために、同じ見解に十分近い必要があります。
これらの要因は、これらの決定ポイントに関する情報フィードの市場が実行可能な可能性であることを示唆しています。

現時点では、自動化可能および値密度のスコアリングを自動化するためのアルゴリズムまたは検索プロセスを設計できるかどうかは明らかではありません。
それは複雑な自然言語処理タスクになります。
おそらく、機械学習システムは、価値を提案するように設計できます。
しかし、より可能性が高いのは、この情報の市場がある場合、コミュニティのこれらの値の脆弱性をスコアリングするために数人のアナリストに報酬を支払うことができるということです。

このようなアナリストをさらに自動化してサポートすることは、少しずつ改善することで進めることができます。
たとえば、キルチェーンの偵察ステップが自動化可能かどうかに関する情報は、ShodanやShadowserverなどのインターネットスキャン会社から自動的に収集される可能性があります。
これはアナリストの決定にはなりませんが、決定ポイントの自動評価に向けた一歩となります。

## Future Work

<details><summary>原文</summary><div>

We intend SSVC to offer a workable baseline from which to improve and refine a vulnerability-prioritization methodology.
We are working to improve SSVC.
Several of the future work items in this section have issues associated with them on the SSVC GitHub page (https://github.com/CERTCC/SSVC/issues), which is a good place to go to check on progress or help.
Plans for future work focus on further requirements gathering, analysis of types of risk, and further testing of the reliability of the decision process.
</div></details>

SSVCは、脆弱性の優先順位付けの方法論を改善および改善するための実行可能なベースラインを提供する予定です。
SSVCの改善に取り組んでいます。
このセクションの今後の作業項目のいくつかには、SSVC GitHubページ（https://github.com/CERTCC/SSVC/issues）で関連する問題があります。これは、進捗状況を確認したり、ヘルプを表示したりするのに適した場所です。
将来の作業の計画は、さらなる要件の収集、リスクの種類の分析、および意思決定プロセスの信頼性のさらなるテストに焦点を当てています。

### Requirements Gathering via Sociological Research

<details><summary>原文</summary><div>

The community should know what users of a vulnerability prioritization system want.
To explore their needs, it is important to understand how people actually use CVSS and what they think it tells them.
In general, such empirical, grounded evidence about what practitioners and decision makers want from vulnerability scoring is lacking.
We have based this paper’s methodology on multiple decades of professional experience and myriad informal conversations with practitioners.
Such evidence is not a bad place to start, but it does not lend itself to examination and validation by others.
The purpose of understanding practitioner expectations is to inform what a vulnerability-prioritization methodology should actually provide by matching it to what people want or expect.
The method this future work should take is long-form, structured interviews.
We do not expect anyone to have access to enough consumers of CVSS to get statistically valid results out of a short survey, nor to pilot a long survey.

Coordinators in particular are likely to be heterogeneous.
While the FIRST service frameworks for PSIRTs and CSIRTs differentiate two broad classes of coordinators, we have focused on CSIRTs here.
PSIRTs may have somewhat different concerns.
Investigating the extent to which SSVC should be customized for this group is future work as well.
</div></details>

コミュニティは、脆弱性優先順位付けシステムのユーザーが何を望んでいるかを知る必要があります。
彼らのニーズを探求するには、人々が実際にCVSSをどのように使用しているか、そしてそれが彼らに何を伝えていると思うかを理解することが重要です。
一般に、実践者や意思決定者が脆弱性スコアリングに何を求めているかについてのそのような経験的で根拠のある証拠は欠けています。
このホワイトペーパーの方法論は、数十年にわたる専門的な経験と、実務家との無数の非公式な会話に基づいています。
このような証拠は、開始するのに悪い場所ではありませんが、他の人による調査や検証には役立ちません。
開業医の期待を理解する目的は、脆弱性の優先順位付けの方法論が、人々が望んでいる、または期待しているものと一致させることによって、実際に何を提供すべきかを知らせることです。
この将来の仕事がとるべき方法は、長い形式の構造化面接です。
短い調査から統計的に有効な結果を得るのに十分なCVSSの消費者にアクセスしたり、長い調査を試験的に実施したりすることは誰にも期待されていません。

特にコーディネーターは異質である可能性が高いです。
PSIRTとCSIRTのFIRSTサービスフレームワークは、2つの幅広いクラスのコーディネーターを区別しますが、ここではCSIRTに焦点を当てています。
PSIRTには、多少異なる懸念がある場合があります。
このグループのためにSSVCをどの程度カスタマイズする必要があるかを調査することも、今後の作業です。

### Types of Risks

<details><summary>原文</summary><div>

SSVC estimates the relative risk created by a vulnerability in an information system.
The priority of acting to mitigate or remediate a vulnerability goes up as this vulnerability risk goes up.
SSVC does not currently take into account the change risk due to applying a mitigation or remediation.

One way to view what SSVC currently provides is that it tells you how urgently a stakeholder should analyze overall risk due to a vulnerability.
For all but the most dire vulnerabilities, what the stakeholder chooses to do may include accepting the vulnerability risk because the change risk or other costs of mitigation or remediation are too high.
Future work should attempt to provide a method for evaluating change risk or cost relative to vulnerability risk.

Tree Construction and Customization Guidance discusses how the prioritization labels in an SSVC tree reflect risk appetite or risk tolerance.
Specifically, these reflect vulnerability risk appetite.
Appetite for vulnerability risk may be negatively correlated with change risk; future work could explore this relationship.
Furthermore, future work could examine suggested practices for connecting tree customization to risk management.

Reasoning Steps Forward states the scope of SSVC analysis is “consider credible effects based on known use cases of the software system as a part of cyber-physical systems.”
The unit of prioritization in SSVC should be work items.
For deployers, a work item is often applying a patch that addresses multiple vulnerabilities.
The “credible effects” to consider are those of all vulnerabilities remediated by the patch.
How exactly to aggregate these different effects is not currently specified except to say that the unit of analysis is the whole work item.
Future work should provide some examples of how this holistic analysis of multiple vulnerabilities remediated in one patch should be conducted.
</div></details>

SSVCは、情報システムの脆弱性によって生じる相対リスクを推定します。
この脆弱性のリスクが高まるにつれて、脆弱性を軽減または修正するために行動することの優先順位が上がります。
SSVCは現在、緩和または修復を適用することによる変更リスクを考慮していません。

SSVCが現在提供しているものを確認する1つの方法は、脆弱性による全体的なリスクを利害関係者がどれほど緊急に分析する必要があるかを示すことです。
最も悲惨な脆弱性を除くすべての場合、変更リスクまたはその他の緩和または修復のコストが高すぎるため、利害関係者が行うことを選択することには、脆弱性リスクを受け入れることが含まれる場合があります。
今後の作業では、脆弱性リスクに関連する変更リスクまたはコストを評価する方法を提供することを試みる必要があります。

ツリーの構築とカスタマイズのガイダンスでは、SSVCツリーの優先順位ラベルがリスクの食欲またはリスクの許容度をどのように反映しているかについて説明しています。
具体的には、これらは脆弱性リスクの欲求を反映しています。
脆弱性リスクへの欲求は、変化リスクと負の相関関係にある可能性があります。将来の仕事はこの関係を探求する可能性があります。
さらに、将来の作業では、ツリーのカスタマイズをリスク管理に接続するための推奨プラクティスを検討する可能性があります。

推論のステップフォワードは、SSVC分析の範囲は、「サイバーフィジカルシステムの一部としてのソフトウェアシステムの既知のユースケースに基づいて信頼できる効果を検討する」と述べています。
SSVCの優先順位付けの単位は、作業項目である必要があります。
デプロイヤーの場合、作業項目は多くの場合、複数の脆弱性に対処するパッチを適用しています。
考慮すべき「信頼できる効果」は、パッチによって修正されたすべての脆弱性の効果です。
分析の単位が作業項目全体であるということを除いて、これらのさまざまな効果をどの程度正確に集計するかは現在指定されていません。
今後の作業では、1つのパッチで修正された複数の脆弱性のこの全体的な分析を実行する方法の例をいくつか提供する必要があります。

### Further Decision Tree Testing

<details><summary>原文</summary><div>

More testing with diverse analysts is necessary before the decision trees are reliable.
In this context, reliable means that two analysts, given the same vulnerability description and decision process description, will reach the same decision.
Such reliability is important if scores and priorities are going to be useful.
If they are not reliable, they will vary widely over time and among analysts.
Such variability makes it impossible to tell whether a difference in scores is really due to one vulnerability being higher priority than other.

The SSVC version 1 pilot study provides a methodology for measuring and evaluating reliability of the decision process description based on the agreement measure κ.
This study methodology should be repeated with different analyst groups, from different sectors and with different experience, using the results to make changes in the decision process description until the agreement measure is adequately close to 1.

Internationalization and localization of SSVC will also need to be considered and tested in future work.
It is not clear how best to consider translating SSVC decision points, if at all.
And at a very practical level, the Abbreviated Format would have to define a new algorithm for creating initialisms that is not dependent an an alphabet for languages based on syllabaries or ideograms.
But a more actionable item of future work would be to include non-native English speakers in future usability studies.

A different approach to testing the Utility decision point could be based on Alternative Utility Outputs.
Namely, future work could example exploit resale markets and compare the value of exploits to the Utility score of the exploited vulnerability.
There are some limitations to this approach, since exploit markets target certain adversary groups (such as those with lots of resources) and may not be representative of all adversary types.
However, such analysis would provide some information as to whether the definition of Utility is reasonable.
</div></details>

デシジョンツリーが信頼できるようになるには、多様なアナリストによるさらなるテストが必要です。
このコンテキストでは、信頼できるとは、同じ脆弱性の説明と決定プロセスの説明が与えられた2人のアナリストが同じ決定に到達することを意味します。
このような信頼性は、スコアと優先順位が役立つ場合に重要です。
それらが信頼できない場合、それらは時間の経過やアナリスト間で大きく異なります。
このような変動性により、スコアの違いが実際に1つの脆弱性が他の脆弱性よりも優先度が高いことが原因であるかどうかを判断することは不可能です。

SSVCバージョン1パイロット調査は、合意尺度κに基づいて意思決定プロセス記述の信頼性を測定および評価するための方法論を提供します。
この調査方法は、さまざまなセクターのさまざまな経験を持つさまざまなアナリストグループで繰り返し、その結果を使用して、合意の測定値が1に十分に近づくまで、意思決定プロセスの説明を変更する必要があります。

SSVCの国際化とローカリゼーションも、今後の作業で検討およびテストする必要があります。
仮にあったとしても、SSVC決定ポイントの翻訳を検討する最善の方法は明確ではありません。
そして、非常に実用的なレベルでは、省略形は、音節文字または表意文字に基づく言語のアルファベットに依存しない初期化を作成するための新しいアルゴリズムを定義する必要があります。
しかし、将来の作業のより実用的な項目は、将来のユーザビリティ研究に英語を母国語としない人を含めることです。

ユーティリティ決定ポイントをテストするための別のアプローチは、代替ユーティリティ出力に基づくことができます。
つまり、将来の作業では、エクスプロイトの再販市場の例を示し、エクスプロイトの価値をエクスプロイトされた脆弱性のユーティリティスコアと比較することができます。
エクスプロイト市場は特定の攻撃者グループ（多くのリソースを持つグループなど）をターゲットにしており、すべての攻撃者タイプを代表しているとは限らないため、このアプローチにはいくつかの制限があります。
ただし、そのような分析は、効用の定義が合理的であるかどうかに関するいくつかの情報を提供します。

## Limitations

<details><summary>原文</summary><div>

SSVC has some inherent limits in its approach, which should be understood as tradeoffs.
There are other limiting aspects of our implementation, but those have been covered as topics that need improvement and are described in Future Work.

We made two important tradeoffs compared to the current state of the practice.
Other systems make different tradeoffs, which may be better or worse depending on the context of use.
While these are inherently limitations of SSVC, we do not intend SSVC to be the one and only vulnerability management tool available.
Those for whom these limitations are a must-have may be better supported by a different vulnerability management framework.

1. We eliminated numerical scores; this may make some practitioners uncomfortable. We explained with the fact that, psychologically, users find that comforting. As this comfort gap may negatively impact adoption, this fact is a limitation. Although it is ungainly, it would be sound to convert the priority outcomes to numbers at the end of the process, if existing processes require it. Which numbers we choose to convert to is immaterial, as long as the ordering is preserved. CVSS has set a precedent that higher numbers are worse, so a scale [1, 2, 3, 4] would work, with defer = 1 and immediate = 4. However, if it were important to maintain backwards compatibility to the CVSS range zero to ten, we could just as well relabel outcomes as [2, 5.5, 8, 9.5] for the midpoints of the current CVSS severity ranges. This is not a calculation of any kind, just an assignment of a label which may make adoption more conventient. Of course, these labels are dangerous, as they may be misused as numbers. Therefore, we prefer the use defer, scheduled, etc., as listed in Enumerating Vulnerability Management Actions.
2. We incorporated a wider variety of inputs from contexts beyond the affected component. Some organizations are not prepared or configured to reliably produce such data (e.g., around mission impact or safety impact). There is adequate guidance for how to elicit and curate this type information from various risk management frameworks, including OCTAVE (Caralli et al. 2007).  Not every organization is going to have sufficiently mature risk management functions to apply SSVC. This second limitation should be approached with two strategies:
(a) Organizations should be encouraged and enabled to mature their risk management capabilities
(b) In the meantime, organizations such as NIST could consider developing default advice. The most practical framing of this approach might be for the NIST NVD to produce scores from the perspective of a new stakeholder—something like “national security” or “public well-being” that is explicitly a sort of default advice for otherwise uninformed organizations that can then explicitly account for national priorities, such as critical infrastructure.
</div></details>

SSVCのアプローチにはいくつかの固有の制限があり、トレードオフとして理解する必要があります。
実装には他にも制限的な側面がありますが、それらは改善が必要なトピックとして取り上げられており、今後の作業で説明されています。

現在の慣行と比較して、2つの重要なトレードオフを行いました。
他のシステムは異なるトレードオフを行いますが、これは使用状況に応じて良くも悪くもなります。
これらは本質的にSSVCの制限ですが、SSVCが利用可能な唯一の脆弱性管理ツールになることを意図していません。
これらの制限が必須である場合は、別の脆弱性管理フレームワークによってより適切にサポートされる可能性があります。

1. 数値スコアを削除しました。これは、一部の開業医を不快にする可能性があります。私たちは、心理的に、ユーザーがその慰めを感じるという事実で説明しました。この快適さのギャップは採用に悪影響を与える可能性があるため、この事実は制限です。不当ですが、既存のプロセスで必要な場合は、プロセスの最後に優先順位の結果を数値に変換するのが適切です。順序が保持されている限り、どの数値に変換するかは重要ではありません。 CVSSは、数値が大きいほど悪いという先例を設定しているため、スケール[1、2、3、4]は、defer=1およびimmediate=4で機能します。ただし、CVSS範囲0との下位互換性を維持することが重要な場合現在のCVSS重大度範囲の中間点について、結果を[2、5.5、8、9.5]と同じように再ラベル付けすることもできます。これはいかなる種類の計算でもありません。採用をより便利にする可能性のあるラベルの割り当てにすぎません。もちろん、これらのラベルは数字として誤用される可能性があるため、危険です。したがって、脆弱性管理アクションの列挙にリストされているように、使用の延期、スケジュールなどをお勧めします。
2. 影響を受けるコンポーネント以外のコンテキストからのさまざまな入力を組み込みました。一部の組織は、そのようなデータを確実に生成するように準備または構成されていません（たとえば、ミッションへの影響や安全への影響など）。 OCTAVEを含むさまざまなリスク管理フレームワークからこのタイプの情報を引き出してキュレートする方法についての適切なガイダンスがあります（Caralli et al.2007）。すべての組織がSSVCを適用するのに十分に成熟したリスク管理機能を備えているわけではありません。この2番目の制限には、次の2つの戦略で取り組む必要があります。
（a）組織は、リスク管理能力を成熟させるように奨励され、可能にされるべきです。
（b）それまでの間、NISTなどの組織はデフォルトのアドバイスを作成することを検討できます。このアプローチの最も実用的な枠組みは、NIST NVDが新しい利害関係者の観点からスコアを生成することである可能性があります。これは、「国家安全保障」や「公共の福祉」など、他の方法では情報がない組織に対するデフォルトのアドバイスの一種です。次に、重要なインフラストラクチャなど、国の優先事項を明示的に説明できます。

## Conclusion

<details><summary>原文</summary><div>

SSVC version 2 presents a method for suppliers, deployers, and coordinators to use to prioritize their effort to mitigate vulnerabilities.
We have built on SSVC version 1 through public presentation and feedback, private consultation, and continued analyst testing.
The evaluation process we developed in version 1 remains an important part of continued improvement of SSVC, and will be used to continue refinements of SSVC version 2.
We invite participation and further refinement of the prioritization mechanism from the community as well, such as by posting an issue.
We endeavored to be transparent about our process and provide justification for design decisions.

We invite questions, comments, and further community refinement in moving forward with a transparent and justified vulnerability prioritization methodology that is inclusive for the various stakeholders and industries that develop and use information and computer technology.
</div></details>

SSVCバージョン2は、サプライヤ、デプロイヤ、およびコーディネータが脆弱性を軽減するための取り組みに優先順位を付けるために使用する方法を提供します。
SSVCバージョン1は、公開プレゼンテーションとフィードバック、非公開の相談、および継続的なアナリストテストを通じて構築されています。
バージョン1で開発した評価プロセスは、SSVCの継続的な改善の重要な部分であり、SSVCバージョン2の継続的な改良に使用されます。
また、問題を投稿するなど、コミュニティからの優先順位付けメカニズムへの参加とさらなる改善を呼びかけます。
私たちは、プロセスについて透明性を保ち、設計上の決定を正当化するよう努めました。

情報やコンピューター技術を開発および使用するさまざまな利害関係者や業界に包括的である、透明で正当化された脆弱性の優先順位付け方法論を前進させるために、質問、コメント、およびさらなるコミュニティの改善を歓迎します。

## Acknowledgements

The authors thank the following people for helpful comments on prior drafts: Deana Shick; Will Dormann (CERT/CC); Michel van Eeten and the anonymous WEIS reviewers; Sounil Yu and other attendees at A Conference on Defense (ACoD), Austin TX 2020; Dale Peterson, Ralph Langer, and attendees at S4, Miami FL 2020; Muhammad Akbar and Manish Gaur (VMWare); David Oxley (McAfee); CISA analysts; Jeroen van der Ham; CVSS and EPSS SIG members; and others who wish to remain anonymous.

## References

Akbar, Muhammad. 2020. “A Critical First Look at Stakeholder Specific Vulnerability Categorization (SSVC).” March 6, 2020. https://blog.secursive.com/posts/critical-look-stakeholder-specific-vulnera bility-categorization-ssvc/.

Allodi, Luca, Marco Cremonini, Fabio Massacci, and Woohyun Shim. 2018. “The Effect of Security Education and Expertise on Security Assessments: The Case of Software Vulnerabilities.” In Workshop on Economics of Information Security. Innsbruck, Austria.

Allodi, Luca, and Fabio Massacci. 2012. “A Preliminary Analysis of Vulnerability Scores for Attacks in Wild: The EKITS and SYM Datasets.” In Workshop on Building Analysis Datasets and Gathering Experience Returns for Security, 17–24. ACM.

Bano, Shehar, Philipp Richter, Mobin Javed, Srikanth Sundaresan, Zakir Durumeric, Steven J Murdoch, Richard Mortier, and Vern Paxson. 2018. “Scanning the Internet for Liveness.” SIGCOMM Computer Communication Review 48 (2): 2–9.

Benetis, Vilius, Olivier Caleff, Cristine Hoepers, Angela Horneman, Allen Householder, Klaus-Peter Kossakowski, Art Manion, et al. 2019. “Computer Security Incident Response Team (CSIRT) Services Framework.” ver. 2. Cary, NC, USA: FIRST.

Captera. 2019. “IT Asset Management Software.” 2019. https://www.capterra.com/it-asset-manageme nt-software/.

Caralli, Richard, James Stevens, Lisa Young, and William Wilson. 2007. “Introducing OCTAVE Allegro: Improving the Information Security Risk Assessment Process.” CMU/SEI-2007-TR-012. Pittsburgh, PA: Software Engineering Institute, Carnegie Mellon University. https://resources.sei.cmu.edu/library/ asset-view.cfm?AssetID=8419.

Cebula, James L, and Lisa R Young. 2010. “A Taxonomy of Operational Cyber Security Risks.” CMU/SEI-2010-TN-028. Pittsburgh, PA: Software Engineering Institute, Carnegie Mellon University.  https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=9395.

Chase, Melissa P, and Steven M Cristey Coley. 2019. “Rubric for Applying CVSS to Medical Devices.” 18-2208. McLean, VA, USA: MITRE Corporation.

Cichonski, Paul, Tom Millar, Tim Grance, and Karen Scarfone. 2012. “Computer Security Incident Handling Guide.” SP 800-61r2. Gaithersburg, MD: US Dept of Commerce, National Institute of Standards; Technology.

CVE Board. 2020. “CVE Numbering Authority (CNA) Rules.” ver. 3.0. Bedford, MA: MITRE.  https://cve.mitre.org/cve/cna/rules.html.

CVSS SIG. 2019. “Common Vulnerability Scoring System.” version 3.1 r1. Cary, NC, USA: Forum of Incident Response; Security Teams. https://www.first.org/cvss/v3.1/specification-document.

Cybersecurity and Infrastructure Security Agency. 2015. “Critical Vulnerability Mitigation.” May 21, 2015.  https://cyber.dhs.gov/bod/15-01/.  FAA. 2000. “System Safety Handbook.” Washington, DC: US Dept. of Transportation, Federal Aviation
Administration. https://www.faa.gov/regulations_policies/handbooks_manuals/aviation/risk_man
agement/ss_handbook/.
Falotico, Rosa, and Piero Quatto. 2015. “Fleiss’ Kappa Statistic Without Paradoxes.” Quality & Quantity
49 (2): 463–70.
Farris, Katheryn A, Ankit Shah, George Cybenko, Rajesh Ganesan, and Sushil Jajodia. 2018. “VULCON:
A System for Vulnerability Prioritization, Mitigation, and Management.” Transactions on Privacy and
Security 21 (4): 16.
Fenton, Robert J., ed. 2017. “Federal Continuity Directive 2: Federal Executive Branch Mission Essential
Functions and Candidate Primary Mission Essential Functions Identification and Submission Process.”
US Department of Homeland Security, Federal Emergency Management Agency. https://www.fema.gov
/media-library-data/1499702987348-c8eb5e5746bfc5a7a3cb954039df7fc2/FCD-2June132017.pdf.
Figueroa-Lorenzo, Santiago, Javier Añorga, and Saioa Arrizabalaga. 2020. “A Survey of IIoT Protocols:
A Measure of Vulnerability Risk Analysis Based on CVSS.” ACM Comput. Surv. 53 (2). https:
//doi.org/10.1145/3381038.
Fleiss, Joseph L, and Jacob Cohen. 1973. “The Equivalence of Weighted Kappa and the Intraclass
Correlation Coefficient as Measures of Reliability.” Educational and Psychological Measurement 33
(3): 613–19.
Garfinkel, Simson, and Heather Richter Lipford. 2014. “Usable Security: History, Themes, and Challenges.”
Synthesis Lectures on Information Security, Privacy, and Trust 5 (2): 1–124.
Guido, Dan. 2011. “The Exploit Intelligence Project.” iSEC Partners. http://www.trailofbits.com/resour
ces/exploit_intelligence_project_2_slides.pdf.
Householder, Allen D, Jeff Chrabaszcz, Trent Novelly, David Warren, and Jonathan M Spring. 2020.
“Historical Analysis of Exploit Availability Timelines.” In Workshop on Cyber Security Experimentation
and Test. Virtual conference: USENIX.
Householder, Allen D, Garret Wassermann, Art Manion, and Christopher King. 2020. “The CERT Guide to
Coordinated Vulnerability Disclosure.” CMU/SEI-2017-TR-022. Pittsburgh, PA: Software Engineering
Institute, Carnegie Mellon University. https://vuls.cert.org/confluence/display/CVD/Executive+Sum
mary.
Howard, Ronald A, and James E Matheson, eds. 1983. Readings on the Principles and Applications of
Decision Analysis: General Collection. Vol. 1. Strategic Decisions Group.
Hutchins, Eric M, Michael J Cloppert, and Rohan M Amin. 2011. “Intelligence-Driven Computer Network
Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains.” Leading Issues in
Information Warfare & Security Research 1: 80.
ISO. 2009. “Risk Management – Vocabulary.” 73:2009(en). Geneva, CH: International Organization for
Standardization. https://www.iso.org/obp/ui/#iso:std:iso:guide:73:ed-1:v1:en.
Jacobs, Jay, Sasha Romanosky, Benjamin Edwards, Michael Roytman, and Idris Adjerid. 2019. “Exploit
Prediction Scoring System (EPSS).” In Workshop on the Economics of Information Security. Boston,
MA. https://arxiv.org/abs/1908.04856.
Jump, Michelle, and Art Manion. 2019. “Framing Software Component Transparency: Establishing
a Common Software Bill of Material (SBOM).” Washington, DC: National Telecommunications;
Information Administration.
Kührer, Marc, Christian Rossow, and Thorsten Holz. 2014. “Paint It Black: Evaluating the Effectiveness
of Malware Blacklists.” In Recent Advances in Intrusion Detection, 1–21. LNCS 8688. Gothenburg,
Sweden: Springer.
Laube, Stefan, and Rainer Böhme. 2017. “Strategic Aspects of Cyber Risk Information Sharing.” ACM
Comput. Surv. 50 (5). https://doi.org/10.1145/3124398.
Manion, Art, Kazuya Togashi, Joseph B. Kadane, Fumihiko Kousaka, Shawn McCaffrey, Christopher
King, Masanori Yamaguchi, and Robert Weiland. 2009. “Effectiveness of the Vulnerability Response
Decision Assistance (VRDA) Framework.” Pittsburgh, PA: Software Engineering Institute, Carnegie
Mellon University. https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=50301.
Metcalf, Leigh B, and Jonathan M Spring. 2015. “Blacklist Ecosystem Analysis: Spanning Jan 2012 to
Jun 2014.” In Workshop on Information Sharing and Collaborative Security, 13–22. Denver: ACM.
Office of the DoD Chief Information Officer. 2020. “DoD Instruction 8531.01 DoD Vulnerability
Management.” Washington, DC: Department of Defense. https://fas.org/irp/doddir/dod/i8531_01.
pdf.
PCI Security Standards Council. 2017. “Payment Card Industry (PCI) Data Security Standard: Approved
Scanning Vendors.” ver 3.0. Wakefield, MA, USA. https://www.pcisecuritystandards.org/documents
/ASV_Program_Guide_v3.0.pdf.
Pendleton, Marcus, Richard Garcia-Lebron, Jin-Hee Cho, and Shouhuai Xu. 2016. “A Survey on Systems
Security Metrics.” ACM Comput. Surv. 49 (4): 62:1–35.
RTCA, Inc. 2012. “Software Considerations in Airborne Systems and Equipment Certification.” DO-178C.
Washington, DC: EUROCAE WG-12.
Russell, Stuart J, and Peter Norvig. 2011. Artificial Intelligence: A Modern Approach. 3rd ed. Upper
Saddle River, NJ: Pearson Education.
Scarfone, Karen, Murugiah Souppaya, Amanda Cody, and Angela Orebaugh. 2008. “Technical Guide to
Information Security Testing and Assessment.” SP 800-115. Gaithersburg, MD: US Dept of Commerce,
National Institute of Standards; Technology.
Simon, Herbert A. 1996. The Sciences of the Artificial. 3rd ed. Cambridge, MA: MIT press.
Souppaya, Muragiah, and Karen Scarfone. 2013. “Guide to Enterprise Patch Management Technologies.”
SP 800-40r3. Gaithersburg, MD: US Dept of Commerce, National Institute of Standards; Technology.
Spring, Jonathan M., Joshua Fallon, April Galyardt, Angela Horneman, Leigh Metcalf, and Ed Stoner.
2019. “Machine Learning in Cybersecurity: A Guide.” CMU/SEI-2019-TR-005. Pittsburgh, PA:
Software Engineering Institute, Carnegie Mellon University. http://resources.sei.cmu.edu/library/asse
t-view.cfm?AssetID=633583.
Spring, Jonathan M, Eric Hatleback, Allen D Householder, Art Manion, and Deana Shick. 2018. “Towards
Improving CVSS.” Pittsburgh, PA: Software Engineering Institute, Carnegie Mellon University.
Spring, Jonathan M, and Phyllis Illari. 2018. “Building General Knowledge of Mechanisms in Information
Security.” Philosophy & Technology 32 (September): 627–59. https://doi.org/10.1007/s13347-018-0
329-z.
———. 2019. “Review of Human Decision-Making During Incident Analysis.” CoRR abs/1903.10080
(April). http://arxiv.org/abs/1903.10080.
Spring, Jonathan M, Sarah Kern, and Alec Summers. 2015. “Global Adversarial Capability Modeling.” In
APWG Symposium on Electronic Crime Research (eCrime). Barcelona: IEEE.
Spring, Jonathan M, Tyler Moore, and David Pym. 2017. “Practicing a Science of Security: A
Philosophy of Science Perspective.” In New Security Paradigms Workshop. Santa Cruz, CA, USA.
https://tylermoore.utulsa.edu/nspw17.pdf.
Tucker, Brett. 2018. “OCTAVE FORTE and FAIR Connect Cyber Risk Practitioners with the Boardroom.”
June 2018. https://insights.sei.cmu.edu/insider-threat/2018/06/octave-forte-and-fair-connect-cyberrisk-practitioners-with-the-boardroom.html.
Vilches, V’ictor Mayoral, Endika Gil-Uriarte, Irati Zamalloa Ugarte, Gorka Olalde Mendia, Rodrigo Izquierdo
Pisón, Laura Alzola Kirschgens, Asier Bilbao Calvo, Alejandro Hernández Cordero, Lucas Apa, and
César Cerrudo. 2018. “Towards an Open Standard for Assessing the Severity of Robot Security
Vulnerabilities, the Robot Vulnerability Scoring System (RVSS).” arXiv Preprint arXiv:1807.10357.
Wang, Brandon, Xiaoye Li, Leandro P de Aguiar, Daniel S Menasche, and Zubair Shafiq. 2017. “Characterizing and Modeling Patching Practices of Industrial Control Systems.” Measurement and Analysis
of Computing Systems 1 (1): 1–23.
Wiles, Darius, and Dave Dugal, eds. 2019. “Common Vulnerability Scoring System SIG.” FIRST. 2019.
https://www.first.org/cvss/.

------

## Contact Us

Software Engineering Institute
4500 Fifth Avenue, Pittsburgh, PA 15213-2612
Phone: 412.268.5800 | 888.201.4479
Web: www.sei.cmu.edu
Email: info@sei.cmu.edu
Copyright 2021 Carnegie Mellon University. This material is based upon work funded and supported by the
Department of Homeland Security under Contract No. FA8702-15-D-0002 with Carnegie Mellon University
for the operation of the Software Engineering Institute, a federally funded research and development
center sponsored by the United States Department of Defense. The view, opinions, and/or findings
contained in this material are those of the author(s) and should not be construed as an official Government
position, policy, or decision, unless designated by other documentation. References herein to any specific
commercial product, process, or service by trade name, trade mark, manufacturer, or otherwise, does not
necessarily constitute or imply its endorsement, recommendation, or favoring by Carnegie Mellon University
or its Software Engineering Institute. NO WARRANTY. THIS CARNEGIE MELLON UNIVERSITY
AND SOFTWARE ENGINEERING INSTITUTE MATERIAL IS FURNISHED ON AN "AS-IS" BASIS.
CARNEGIE MELLON UNIVERSITY MAKES NO WARRANTIES OF ANY KIND, EITHER EXPRESSED
OR IMPLIED, AS TO ANY MATTER INCLUDING, BUT NOT LIMITED TO, WARRANTY OF FITNESS
FOR PURPOSE OR MERCHANTABILITY, EXCLUSIVITY, OR RESULTS OBTAINED FROM USE
OF THE MATERIAL. CARNEGIE MELLON UNIVERSITY DOES NOT MAKE ANY WARRANTY
OF ANY KIND WITH RESPECT TO FREEDOM FROM PATENT, TRADEMARK, OR COPYRIGHT
INFRINGEMENT.
[DISTRIBUTION STATEMENT A] This material has been approved for public release and unlimited
distribution. Please see Copyright notice for non-US Government use and distribution.
Internal use:* Permission to reproduce this material and to prepare derivative works from this material
for internal use is granted, provided the copyright and “No Warranty” statements are included with all
reproductions and derivative works. External use:* This material may be reproduced in its entirety, without
modification, and freely distributed in written or electronic form without requesting formal permission.
Permission is required for any other external and/or commercial use. Requests for permission should be
directed to the Software Engineering Institute at permission@sei.cmu.edu. * These restrictions do not
apply to U.S. government entities. Carnegie Mellon® and CERT Coordination Center® are registered in
the U.S. Patent and Trademark Office by Carnegie Mellon University. DM21-0402

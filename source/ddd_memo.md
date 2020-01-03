---
title: ドメイン駆動設計メモ
date: 2019-01-01
---

ドメイン = 「ソフトウェア化する対象」
モデル = 「問題解決のために、物事の特定の側面を抽象化したもの」
ドメインモデル = ドメインの問題を解決するためのモデル
データモデル = データベースになにかを永続化するためのモデル
ルールエンジン = 業務知識をルールベースとして蓄積することで、高度な意思決定の自動化を実現するシステム
不変条件 = モデルが有効である期間中、常に一貫している必要のある状態のこと

[DDDのモデリングとは何なのか、 そしてどうコードに落とすのか - slides-hare ](https://www.slideshare.net/koichiromatsuoka/domain-modeling-andcoding)

# 日本語版への序文

- 根本的に、DDD を駆動している原則は3つのみ
    - コアドメインに集中すること
    - ドメインの実践者とソフトウェアの実践者による創造的な共同作業を通じて、モデルを探求すること
    - 明示的な境界づけられたコンテキストの内部で、ユビキタス言語を語ること

## ドメイン駆動設計におけるモデルの有用性（P.3）

- モデルと設計の核心が相互に形成し合う（第３章）
    - モデルと実装が密接に結びつく → モデルはドメインと深く関連したものになる
    - モデルに対する分析が、最終青果物である実際に動くプログラムに適されることが保証される
    - モデルの結びつきは、保守や継続的開発にも有効
    - モデルを理解することで、コードを解釈できる
- モデルは、チームメンバ全員が使用する言語の基盤である（第２章）
    - モデルと実装が結びついているので、開発者はプログラムについて話すときにこの言語を使える
    - 通訳不要になる
- モデルとは、蒸留された知識である（第1章）
    - モデルは、ドメインの知識を構成して、最も関心のある要素を区別するためのチーム内で取り決めた方法でもある
    - モデルと実装が紐付いているので、ソフトウェアの初期バージョンで得た経験が、フィードバックとしてモデリングプロセスに適用できるようになる


# 第1章 知識を噛み砕く

## 効果的なモデリングの要素（P.13）

- 1. モデルと実装を結びつける
    - 荒削りなプロトタイプによって、本質的な結びつきが早い時期に作り、以降はイテレーションを通してずっと維持できた
- 2. モデルに基づいて言語を洗練させる
    - プロジェクトメンバ全員が、モデルで使用している用語で理解し合えるようになった
- 3. 知識豊富なモデルを開発する
    - モデル ≠ 単なるデータスキーマ
    - 複雑な問題を解決するのに欠かせないもの
- 4. モデルを蒸留する
    - モデルが完成されていくにつれて、重要な概念が追加され、役に立たないものは排除していった
- 5. ブレインストーミングと実験を行う
    - スケッチやブレインストーミングと組み合わせることで、モデルの実験用バリエーションを本当に使えるか判断することができた

## 知識のかみ砕き（P.14）

- 知識の噛み砕きは、開発者とドメインエキスパートとの共同して行う
    - 開発者が情報を引き出し、噛み砕き、役立つ形にする
- 旧来のウォーターフォールの欠点
    - ビジネスエキスパート → アナリスト → 開発者 というフロー
        - フィードバックが欠ける
        - 開発者から学ぶことができない（知識が一方通行）
    - プログラマがドメインに興味を持たなければならない
- チームメンバ間のやりとりは、メンバ全員がモデルを一緒に噛み砕くことで変化する
    - モデルは、プロジェクト内で流れる情報を体系化するためのツールになる

## 継続的学習（P.16）

- ソフトウェアを書き始めるとき、対象を十分に理解していない
    - どの知識が必要かも分からない
    - どれほど理解していないか認識していない
- なにかを習得した人が他のプロジェクトに移動すると、知識が流出する
    - 典型的な設計アプローチの場合、コードとドキュメントを苦労して手に入れた知識を使える形式で表現しないため、口頭での伝承が途切れたら、知識は失われてしまう
- 良いチームは、自分たちの知識を意識的に育てて、継続的学習を実践する
    - ドメインモデリングのスキルと合わせて、技術的な知識の向上（開発者）

ドメインモデリング ＝ システムに関する業務知識（ドメイン）を簡潔に整理(要約・モデル化)し、その関係性がわかるようにすること

## 知識豊富な設計（P.17）

- 「名詞を見つける」ことだけでなく、ドメインに関する豊富な知識も必要
    - 知識を噛み砕くことで、よりよいモデルが生み出される

## 深いモデル（P.20）

- ドメインを理解することによって、最初は重要と思っていたモデル要素を破棄するか、違った視点でアプローチすることになる
    - ドメインにとって、何が重要かを最初から把握するのは難しい
        - 知識を噛み砕いて理解することが重要

# 第2章 コミュニケーションと言語の使い方

- モデルに基づいたコミュニケーションは、統一モデリング言語（UML）で書かれた図とは限られない

## ユビキタス言語（UBIQUITOUS LANGUAGE） （P.24）

- ドメインエキスパートは、自分の得意分野の専門用語を使用する（ソフトウェア開発の専門用語は使わない）
    - 開発者は…（訳が意味不明）
- 言語の間に断絶があるため…
    - ドメインエキスパート → 自分たちが欲しいものを曖昧にしか記述しない
    - 開発者 → 知らないドメインを理解しようと苦労するが、理解も曖昧
    - チームメンバ → 両者の言語を理解できるようになるが、情報の流れがボトルネックになり、通訳も正確ではない
- ユビキタス言語には、クラスや主要な操作の名前、議論するための用語を含む
    - 高次の構成原理（コンテキストマップや大規模な構造など）
    - ドメインモデルに対して一般に適用されるパターン名によって、言語は強化される
    - 開発者の間や、ドメインエキスパートとのやり取りにも使用する

## 声を出してモデリングする（P.30）

- 考えられるモデルのバリエーションから生じるさまざまな概念を、声に出して構成してみる
    - 粗削りな表現はすぐに分かる
- ドメインモデルのユビキタス言語を議論で使用する
    - 全員がその言語でよどみなく話せるようになり、ニュアンスを互いに教え合う
- **システムを語る際に、モデルを色々と試してみること**
    - モデルに許された方法で概念を結びつけながら、シナリオを声に出して描写すること
    - 表現することをより簡単に言う方法を見つけ、その新しい考え方をコードに再び反映させること

## 1つのチームに1つの言語（P.32）

- 技術系のメンバーが、ドメインエキスパートを「わかっていない」と批判することがある
    - それは**豊富な知識をもつドメインエキスパートがモデルを理解できていないとしたら、モデルに何か問題がある**
- ドメインエキスパートと開発者がユビキタス言語を使用すると、多くのことに気付ける
    - モデルがドメインエキスパートの要求を満たしていない
    - モデルが誤っている
    - ドメインエキスパート自身が思考の矛盾や曖昧さが明らかにされる領域がある
- 開発者の専門用語も、ドメインエキスパートに伝わるように変更する必要がある


## ドキュメントと図（P.34）

- UML を使うと、問題が発生する場合がある
    - オブジェクトモデル図は、多くの情報を省いていることがある
    - 完全すぎて、詳細にしすぎてモデルが見づらくなってしまう
- 実装では UML を使用しても、モデルを伝えるには**図**
    - 図では、考え方の骨格を表現している
    - 設計に関する本質的な詳細は、コードにおいて捉えられる
    - モデルは図ではない
        - あくまでモデルについてコミュニケーションするときのサポート役

### 書かれた設計ドキュメント（P.36）

- 話すだけでなく、役立つドキュメントも必要（難しいけど）
    - ドキュメントを評価する一般的な指針だけ提示する

##### ドキュメントはコードや会話での表現を補わなければならない

- エクストリームプログラミング（余計なドキュメントを使用しないで、コードですべて表現する）
    - 限界がある
        - 概念を直接実装できないときは、ドキュメントによって、設計の意図を明確にすることができる
    - すでにコードがうまくやっていることを、ドキュメントでやろうとしてはいけない

##### ドキュメントは活動の役に立たなければならず、最新の状態を保たなければならない

- モデルをドキュメントに書き出す場合、モデルで厳選した小さな集合を図にかいて、その周りにテキストで補足する
- ドキュメントは、プロジェクトの活動に取り込まれていなければならない
    - ユビキタス言語とドキュメントの相互作用を観察することで、↑がちゃんとできているか分かる

## 説明のためのモデル（P.39）

- **実装、設計、チーム内のコミュニケーションの根底にあるモデルは1つだけあるべき**

# 第3章 モデルと実装を紐付ける（P.43）

- 分析モデル: ソフトウェアで果たす役割を考慮せず、ドメインを分析した結果から、概念をまとめ上げる
    - 分析モデルは、ドメインを理解するためだけに使うツール
    - 設計の問題と混同しない
    - 設計と分析モデルの紐付けを維持することは、費用対効果が低い
    - コーディングが始まった瞬間捨てられる
- 分析モデルをつかって、ドメインを理解することすらできない
- 分析は、ドメインから得られる基本的な概念を分かりやすく表現力豊かな方法でとらえる
- 設計は、コンポーネントの集合を定義しなければならない
    - コンポーネントは、アプリケーションに課せられた問題を正しく解決できなければならない

---

- モデル駆動設計は、分析と設計という二分法を捨てて、単一のモデルを探す
- ドメインを抽象化する方法、設計技法はたくさんある
    - モデルと設計を結びつけることは現実的には可能
        - 代償：分析を妥協してはいけない

モデルを適切なものにするには…
1. 設計では、ドメインモデルを文字通りの意味で忠実に反映させること
2. モデルを再検討し、より自然にソフトウェアに実装されるように修正すること
3. **強固なユビキタス言語を支えることによって、ドメインと実装両方の目的に使える単一なモデルを要求すること**
4. 設計で使用する用語法と責務の基礎的な割り当てをモデルから引き出すこと

## モデリングパラダイムとツールによるサポート

- オブジェクト指向プログラミングが優れているのは、あるモデリングパラダイムに基づいて、モデルを構成する概念に実装を提供するから。
https://qiita.com/j5ik2o/items/7ee00cfb22154efbab55

## 骨格を見せる：なぜモデルがユーザにとって重要なのか？（P.55）

(例)IE のお気に入り機能

- 「Qiita：ドメイン駆動設計」という名前で登録しようとすると「ファイル名に以下の文字を含めることはできません：・￥：＊？」と表示される
    - ユーザから見たら、ファイルとはどれのことか分からない
- ユーザに「ファイルシステムを使ってますよ！」と明かす
    - 混乱を招くような代わりのモデルを排除しなければならない
    - モデルを明らかにすることで、ソフトウェアの潜在能力にもっと触れられる
        - ファイルを直接をいじって、自由度の高い変更を加えたり………？
- お気に入り機能を違う手法で実装するのもよい（データファイルに保存するとか）

## 実践的モデラ（P.57）

- コードを変更したら、モデルも変わることを開発者は認識していなければならない
    - そうしないと、開発者によるリファクタリングによって、モデルの力を失ってしまう
- モデルに貢献する技術者は、ある程度の時間をコードに触れることに費やさなければならない
    - コードの変更に対して責任を負う人はだれでも、コードを通してモデルを表現することを習得しなければならない
    - その他の方法で参画する人々は、ユビキタス言語を通じてモデルに対する考え方をダイナミックに交換する際には、コードに触れる人々を意識して巻き込まなければならない

--- 

# 第２部 モデル駆動設計の構成要素

- 本書の設計スタイルは「責務駆動設計（Responsibility-driven design）」

# 第4章 ドメインを隔離する(P.65)

## レイヤー化アーキテクチャ

- オブジェクト指向では、UI、DBおよびその他の補助的なコードが、ビジネスオブジェクトに直接書かれることがある（簡単で楽だから！！）
    - ドメイン関連のコードが拡散してしまうと、コード理解が困難になる
    - すべての技術とロジックがそれぞれの活動に関係しているので、プログラムを非常にシンプルに保たなければ理解できなくなる
- ソフトウェア・システムを分割する方法の一つ「レイヤ化アーキテクチャ」

| 名前 | 説明 |
| :--- | :--- |
| ユーザーインターフェース | ユーザに情報を表示する（UI） |
| アプリケーション層 | ソフトウェアが行う仕事を定義し、表現力豊かなドメインオブジェクトが問題を解決するように導く |
| ドメイン層 | ビジネスの概念、ビジネスが置かれた状況に関する情報、ビジネスルールを表す責務 <br/> 格納したらインフラストラクチャに委譲する |
| インフラストラクチャ層 | 上位のレイヤーを支える一般的な技術的機能を提供する。 <br />アプリケーションのためのメッセージ送信、ドメインのための永続化、ユーザーインターフェースのためのウィジェット描画などなど|

- 複雑なプログラムはレイヤに分割すること
- 各レイヤで設計を進め、凝集度を高めて下位層だけに依存すること
    - 上位のレイヤーに対しては疎結合にすること
- ドメインモデルに関係するコード全部を1つの層に集中させること
    - ユーザーインターフェース、アプリケーション、インフラストラクチャからは分離

### アーキテクチャフレームワーク

- 複雑な技術的問題を解決する一方で、ドメイン開発者がモデルを表現することに集中できるようにする
    - ドメインについての設計の選択肢を制限する前提を多く設け過ぎたり、開発の速度を低下させるほど実装を難しくしてしまう可能性もある
- 新しいフレームワークによって便利になれば、コアビジネスの問題をモデリングすることに多くの時間を割けるようになる
    - しかし、技術的な解決策に固執しないようにする
        - （例）フレームワークが定義したクラスのサブクラスを実装したり、メソッドシグネチャを規定したり

## ドメイン層はモデルが息づく場所（P.73）

- ドメイン層は、モデルに直接関係する設計上のすべての要素が現れる場所
- ドメインの実装を隔離することは、ドメイン駆動設計の必要条件

## 利口なUI「アンチパターン」（P.74）

- レイヤ化アーキテクチャを伴うモデル駆動設計は、習得の難しさに苦労する
    - インフラストラクチャと各レイヤを管理するオーバーヘッドにより、非常に単純な作業でも時間がかかる
- ドメイン駆動設計が最も効果を発揮するのは、大掛かりなプロジェクト
    - 実現するには強力なスキルも必要

---
- 利口なUIとは？
    - すべてのビジネスロジックにユーザーインターフェースを入れること
    - アプリケーションを小さな機能に分割、それぞれ独立したインターフェースとして実装し、ビジネスルールもその中に埋め込むこと
    - DBは、共有リポジトリとして使用すること
    - ユーザーインターフェースと視覚的なプログラミングについて、最も自動化が進んでいるものを使用すること

**ユーザーインターフェースとロジックが密結合でいいんですかね…？**

- **アーキテクチャがドメインに関連するコードを隔離して、凝集度が高いドメインの設計が、システムの他の部分と疎結合できるようにしているなら、そのアーキテクチャはおそらくドメイン駆動設計を支えられる**

# 第5章 ソフトウェアで表現されたモデル

- モデルを表現する3パターン
    - エンティティ
    - 値オブジェクト
    - サービス

| | エンティティ | 値オブジェクト |
| :--- | :--- | :--- |
| 同一性判定 | 識別子が同一であれば同一 | 保持する属性が同一であれば同一 |
| 可変性 | 可変、生成されてから変異する | 不変、生成されたら破棄されるのみ |

- 例）社員がエンティティ、社員に紐づく誕生日や電話番号、氏名などなどが値オブジェクト
- 操作を行う責務はサービス（エンティティや値オブジェクトでは行わない）

## 関連（P.80）

- モデルにおいて遡ることができる関連それぞれに対応して、ソフトウェアにおいても同じ特性をもつ仕組みが存在する
- 現実世界では、多対多の関連が多く、双方向である
    - 深く理解すると、「限定された」関係の一対多であることが多い
    - 国に「期間」をもたせれば、大統領（人）が特定できる

## エンティティ（別名　参照オブジェクト）

- オブジェクトの中には、主要な定義が属性に寄ってなされないものもある
    - オブジェクトは同一性のつながりを表現するのであり、その同一性は、時間が経っても、異なるかたちで表現されても変わらない
    - オブジェクトは属性が異なっていても、他のオブジェクトと一致しなければならないことがある
    - 同じ属性を持っていたとしても、他のオブジェクトと区別しなければならない。 → 同一性を取り違えるとデータの破損に繋がりかねない
- ライフサイクルを通じた連続性をもち、アプリケーションのユーザーによって重要な区別が属性から独立しているもの = **エンティティ**

### エンティティをモデル化する（P.91）

- エンティティにとって、最も基本的な責務は、ふるまいが明確で予測可能になるように連続性を確立すること
    - 余計なものがない状態が保たれているとき
    - エンティティを識別するものや、検索して突き合わせるのに通常使用されるもの

### 同一性のための操作を設計する（P.92）

- 真に一意のキーがない場合、一般的に各インスタンスにクラス内で一意の記号（番号や文字列など）をつける
    - ID属性は、だいたいシステムによって自動生成される
    - 生成されるIDが、ユーザーにとって関心の対象となる場合がある
        - 例）配達サービスの追跡番号や、予約サイトの申込番号とか…


## 値オブジェクト（Value Objects）（P.95）

- モデルで最も目立つオブジェクトがエンティティで、各エンティティの同一性を追跡することが非常に重要
    - フレームワークの中には、あらゆるオブジェクトに一意のIDを割り当てるものもある
- エンティティ以外のオブジェクトに同一性を与えてしまうと、システムの性能を損なうことになる
    - 分析作業が増える
    - すべてのオブジェクトの見た目が同じになる
- 値オブジェクトは、よくオブジェクト間のメッセージでパラメータとして渡される
    - エンティティの属性としても使用される
        - 人は同一性のあるエンティティとしてモデル化されるかもしれないが、その人の名前は値オブジェクトである
- **あるモデル要素で、その属性しか関心の対象にならないのであれば、その要素は値オブジェクト**
    - 自分が伝える属性の意味を表現させ、関係した機能を与えること
    - 値オブジェクトを不変なものとして扱うこと
    - 同一性を与えない
        - エンティティを維持するために必要となる複雑な設計を割けること

### 値オブジェクトを設計する

- オブジェクトを安全に共有するためには、オブジェクトは不変でなければならない
- 値オブジェクトの数が多くなりがち
    - インスタンスを1つだけ共有して、それを何度も参照するようにすれば、値オブジェクトの数を抑えることができる
- インスタンス共有が有益な場合
    - DB内で、スペースやオブジェクト数を節約することが重要である場合
    - 通信オーバーヘッドが低い場合
    - 共有オブジェクトが完全に不変である場合

### 値オブジェクトを含む関連を設計する（P.101）

- モデルの中の関連は、数が少なく単純であればあるほどよい
- 値オブジェクト同士の双方向の関連は、完全に取り除くこと
    - 同一性がなければ、あるオブジェクトが参照し返しているのは、自身を参照しているのと同じ値オブジェクトだと言っても無意味
    - そういうオブジェクトが必要だと思ったら、そのオブジェクトを値オブジェクトにすること自体間違っているかも
        - まだ明示的には認識されていない同一性があるはず

## サービス（P.103）

- サービスとは、モデルにおいて独立したインターフェースとして提供される操作
    - エンティティと値オブジェクトのように状態をカプセル化しない
- 優れたサービスの特徴
    - 操作がドメインの概念に関係しており、その概念がエンティティや値オブジェクトの自然な一部ではない
    - ドメインモデルの他の要素の観点からインターフェースが定義されている
    - 操作に状態がない
        - どのクライアントでも、特定のサービスの任意のインスタンスを使うにあたって、インスタンスの持つ個々の履歴を気にする必要がない
- エンティティや値オブジェクトの自然な責務ではない場合、サービスとして宣言される独立したインターフェースとしてモデルに追加すること
    - モデルの言語を用いてインターフェースを定義し、操作名が必ずユビキタス言語の一部になること
    - サービスには状態を持たせないこと

### サービスと隔離されたドメイン層（P.105）

- サービスのほとんどはインフラストラクチャ層に属する
    - ドメイン層とアプリケーション層のサービスは、インフラストラクチャ層のサービスと協力して動作する

- 銀行業アプリケーションを例にして、レイヤを分けると…
    - アプリケーションサービス：人間が分析できるように取引を変換してスプレッドシートにエクスポートする
    - ドメインサービス：資金をある口座から別の口座に振り替える機能
    - インフラストラクチャサービス：アプリケーションの指示に従って、電子メールや手紙、その他のメッセージを送信する

### 粒度（P.106）

- TODO）分からん

### サービスへのアクセス（P.107）

- サービスへのアクセスを提供する手段は、特定の責務を切り出すという設計上の意思決定ほどは重要ではない
    - サービスのインターフェースを実装するのに、「実行者」オブジェクトで十分な場合もある
    - 単純なシングルトンは、簡単に作成できる

## モジュール（別名：パッケージ）（P.108）

- モジュールとは？
    - オブジェクトをまとめて管理する方法
    - Java でいうパッケージ
- モジュール間では低結合、モジュール内では高凝集が必要
    - モジュールに分割されるのはコードだけではなく、概念も分割される
    - 関係する責務を負ったオブジェクトの凝集度が高いことで、モデリングと設計は1つのモジュール内で集中できる
- モジュールを選択する際、概念の凝集した集合を含んでいるものを選択すること
    - モジュール間を低結合にすることが多い
        - そうでない場合はモデルを変更すること
        - モジュールの基礎となる概念を見逃していないか模索すること
    - モジュールには、ユビキタス言語の一部になる名前をつけること

### アジャイルモジュール（P.110）

- モジュールは、モデルと同様にリファクタリングし続ける必要がある
    - 初期に間違いが犯されることは避けられないが、そのことが高結合に繋がり、それによってリファクタリングが困難になる
    - モジュールを再構成するしかない

### インフラストラクチャ駆動パッケージの落とし穴（P.111）

ティア化 = 断片化

- ティア化アーキテクチャーでは、モデルオブジェクトの実装が断片化されるかもしれない。
- 別々のサーバにコードを分散させようという意図が実際にない限り、単一の概念オブジェクトを実装するコードは全て、同一のオブジェクトにならなくても、同一のモジュールにまとめること。
- ドメイン層を他のコードから分離するためにパッケージングを使用すること。そうでなければ、ドメインの開発者にできる限り選択の余地を残し、モデルと設計上の選択をサポートするように、ドメインオブジェクトをパッケージングできるようにすること。
- 別々のサーバにコードを分離させようという意図が実際にない限り、単一の概念オブジェクトを実装するコードはすべて、同一のオブジェクトにならなくても、同一のモジュールにまとめること
- ドメイン層を他のコードから分離するためにパッケージングを使用すること

### モデリングパラダイム（P.114）

- モデリング
    - 広義の意味での模型（モデル）を組み立てる事を言う。
- パラダイム
    - ある時代のものの見方・考え方を支配する認識の枠組み。
- モデリングパラダイム
    - モデルを組み立てるための認識の枠組み
- 現在主流となっているパラダイムは「オブジェクト指向設計」

##### なぜオブジェクトパラダイムは主流なのか

- シンプルで洗練されているから
- ドメインについての重要な知識をとらえることができる

##### オブジェクトの世界におけるオブジェクトではないもの


##### パラダイムを混在させる際にはモデル駆動設計に忠実であること（P.118）

- オブジェクトのカプセル化のせいで、グローバルなルールが適用しにくくなる
    - ルールエンジンを使用することで、ルールパラダイムを効果的にオブジェクトパラダイムと混在できるようになる
        - うまく動かせないこともあるので、常にモデルの観点から考えることが重要
        - チームはどちらの実装パラダイムでも使える単一のモデルを見つけなければならない
- ルールとオブジェクトをつなぐ環境が必要
    - ユビキタス言語を使って、2つの環境で一貫した名前を適用する
- オブジェクト指向が主流のシステムに、非オブジェクト（ルールやワークフロー）の要素を混ぜるための経験則
    - 実装パラダイムと対立しないこと
        - パラダイムに合うモデルの概念を見つけること
    - ユビキタス言語に頼ること
        - ツール間に厳格なつながりがなくても、言語を一貫していれば、設計の各部分が分かれていってしまうことはない
    - UMLにこだわらないこと
        - UML図のようなツールに固執すると。モデルが歪められるかもしれない
            - 別の作図スタイルを採用したり、単純な自然言語で記述したり…
    - 懐疑的であること
        - ルールがあるからといって、ルールエンジンを使うオーバーヘッドが必要とは限らない

# 第6章 ドメインオブジェクトのライフサイクル

- オブジェクトによってライフサイクルは異なる
    - 寿命の長いオブジェクトがあったり、メモリ上だけに存在するだけとも限らない
- ↑の課題は2つのカテゴリに分けられる
    - 1. ライフサイクルを通じて整合性を維持すること
    - 2. ライフサイクルを管理するのが複雑でも、モデルを侵食されないようにすること
- 3つのパターンで対応
    - 集約：明確な所有権と境界を定義
    - ファクトリ：ライフサイクルの始まりに合わせて、複雑なオブジェクトや集約を生成したり再構成
    - リポジトリ：ライフサイクルの中期と終末に対応。永続化されたオブジェクトにアクセスする手段を提供、アクセスに伴って必要となる巨大なインフラストラクチャをカプセル化する

## 集約（P.123）

- 複雑な関連を伴うモデルは、オブジェクトに対する変更の一貫性を保証するのは難しい
    - 人オブジェクトを削除して、生年月日や職務経歴は消せるが、住所は消せない（他の人オブジェクトがそこに住んでいるかもしれない）
    - 他の複数のオブジェクトから構成されているオブジェクトが、いつ作られ、いつなくなるのか、どうすればわかるのか？
        - 境界が定義されていないことが問題
- 例）自動車修理店のソフトウェア
    - 自動車が集約のルートエンティティ
        - 集約の境界がタイヤも囲い込むことになる
        - タイヤは一時的な参照
        - タイヤから自動車を探そうとする人はいない
    - アプリによっては、エンジンが集約を持ち、ルートになる
    - グローバルな同一性 ＝ 車両登録番号
- エンティティ（自動車、タイヤなど）と値オブジェクト（走行距離、位置、使用期間など）を集約の中にまとめて、各集約の周囲に境界を定義すること
    - 各集約はルートとなるエンティティを1つ選ぶ（自動車）
    - 境界の内部に存在するオブジェクトへのアクセスは、ルートとなるエンティティを経由して制御すること
    - 外部のオブジェクトが参照を保持できるのは、ルートのみ
    - 内部の値オブジェクトに対する一時的な参照を渡してよいのは、単一の操作で使用するときだけ

## ファクトリ（P.134）

- オブジェクトの生成は、主要な操作になり得る
    - 複雑な組み立て操作の場合、生成されるオブジェクトの責務に合わない
    - 理解しにくく、不格好な設計が作り出されるかもしれない
        - クライアントに直接構築させると、カプセル化にも違反するし、生成されるオブジェクトの実装とクライアントが過度に結合する
- 複雑なオブジェクトの生成はドメイン層の責務
    - しかし、その仕事はモデルを表現するオブジェクトのものではない
    - オブジェクトの生成は、エンティティ／値オブジェクト／サービスのどれとも違う構成要素をドメイン設計に追加しなければならない
        - モデルの中のどれにも対応しないが、ドメイン層の責務の一部

### ファクトリとその場所を選択する

- ファクトリを生成するのは、詳細を隠したいと思うものを構成するため
- ファクトリを配置するのは、制御を行わせたい場所
    - 具体的な置き場所がなさそうな場合は、専用のファクトリオブジェクトかサービスを作成しなければならない
    - 集約の内部にあるオブジェクトがファクトリを必要とし、集約ルートがそのファクトリの妥当な置き場所でない場合は、ためらわず独立したファクトリを作成すること

### コンストラクタがあればよい場合（P.139）

- クラスが型（type）である
- クライアントが実装に関心がある
- クライアントが目にするコンストラクタの内部に、さらに別のオブジェクトの生成がネストされること
- 構築が複雑ではない
- 公開コンストラクタは、ファクトリと同じルールに従わなければならない
- コンストラクタ内で他のクラスのコンストラクタを呼び出すのは避ける

### インターフェースを設計する（P.141）

- 各操作はアトミック（最小）でなければならない
    - ファクトリとのやりとり1回ですべて渡さなければならない
    - 不変条件のどれかが満たされずに生成が失敗した場合にどうなるかも決めておく
- ファクトリは、その引数と結合する 
    - 入力パラメータは慎重に選択
        - 複雑な依存関係を作り出しかねない

### 不変条件のロジックはどこへ置くべきか？（P.142）

- 不変条件は、ファクトリにおくと、生成物はシンプルに保つことができる
- ファクトリは、生成するオブジェクトや集約に関する不変条件が、すべて満たされていることを保証する責務を負っている
- 不変条件は、各操作の終わりに適用されるのが原則
    - オブジェクトで起きることが認められる変遷のせいで、不変条件が利用されないこともしばしばある

### エンティティファクトリ対値オブジェクトファクトリ（P.142）

- 値オブジェクトは不変
    - 値オブジェクトファクトリを操作するときは、生成物を完全に記述することを考えなければならない
- エンティティファクトリは、有効な集約を生成するために必要な属性だけを受け取る
    - 不変条件によって求められていないのならば、詳細は後から追加すればいい
- 一意のIDを生成することは、データベースの「シーケンス」や他のインフラストラクチャの仕組みによって行われる。
    - 何を要求して、どれをどこに入れるのか、知っているのはファクトリだけでいい

### 格納したオブジェクトを再構成する（P.143）

再構成とは？ → DBに格納、再びDBから取り出して組み立てること

- 再構成に使用されるエンティティファクトリでは、新しい追跡IDを割り当てることがない
    - 割り当てると、再構成前のオブジェクトとの連続性が失われる
- オブジェクトを再構成するファクトリは、不変条件の違反を違うかたちで制御する
    - 新規オブジェクトを生成の場合は、不変条件を満たさなければ、ファクトリは処理を中止してもよい
    - 再構成の場合は、柔軟な対応が必要
        - すでにオブジェクトがシステムのどこかに存在しているのに無視はできない
        - ルール違反もだめ

## リポジトリ（P.146）

- ライフサイクルの中期にあるエンティティや値オブジェクトに対して、関連を辿り始める場所がなければならない
- 格納したオブジェクトを取り出すことは、生成することのサブセット
    - データベースから取り出されたデータは、新しいオブジェクトを組み立てることに使用されるから
    - 格納されたデータからインスタンスを生成することを**再生成**と呼ぶ
- ドメイン駆動設計の目標：**技術ではなくドメインについてのモデルに焦点を合わせる**
- クライアントにとって必要なものは、すでに存在するドメインオブジェクトへの参照を手に入れること
    - インフラストラクチャ層にクエリを渡すようにするのはモデルを混乱させてしまう
        - ドメインロジックがクエリとクライアントコードに移され、エンティティと値オブジェクトはただのデータコンテナになってしまう

---

- リポジトリとは？
    - データの保管庫
    - コレクションのように動作する
    - エンティティや値オブジェクトから構成される集約の格納と取得を担当
        - クエリメソッドを使用する
    - 適切な型のオブジェクトについて追加や削除を実行されると、リポジトリの背後にある仕組みが、データベースに対して挿入や削除を行う
- リポジトリの利点
    - クライアントに対して、永続化されたオブジェクトを取得し、そのライフサイクルを管理するためのシンプルなモデルを与える
    - アプリケーションとドメインの設計を、永続化技術や複数のデータベース戦略、さらには複数のデータソースからも分離する
    - オブジェクトアクセスに関する設計上の決定を伝える
    - テストで使用するためには、ダミーの実装を置き換えるのが容易になる
        - インメモリを使用するのが一般的）

#### リポジトリに対して問い合わせる（P.151）

- 構築するのが最も簡単なリポジトリは？
    - ハードコードされたクエリを持ち、特定のパラメータを受け取るだけのもの
- 大量の問合せが必要なプロジェクトの場合、自作したリポジトリフレームワークは、より柔軟なクエリを実行できるように構築されるだろう
- 柔軟にクエリを構築できるリポジトリを設計する
    - 特殊なクエリをハードコードして追加できるようにしなければならない

#### クライアントのコードはリポジトリの実装を無視するが、開発者はそうではない（P.153）

- メモリ不足になったりする場合がある
- 実装者はどのような動きをするのか熟知していなければならない

#### リポジトリを実装する（P.154）

- 理想は、クライアントから内部の働きを隠蔽すること
    - クライアントコードが、データの格納場所に関わらず同じになること
        - RDBだろうが、NoSQLだろうが、インメモリだろうが関係なくなる
- 懸案事項
    - 型を抽象化すること
        - 特定の型のインスタンスをすべて「含んでいる」が、各クラスに1つ必要というわけではない
        - 抽象基底クラスでも構わない
    - クライアントから切り離す利点を活かすこと
        - クエリのテクニックを変更できる
        - 永続化の戦略をいつでも変更できる
        - クライアントコードとドメインオブジェクトのテストは、簡単に操作できるダミーのインメモリ戦略を使うことが楽になる
    - トランザクション制御はクライアントに委ねること
        - リポジトリがトランザクション管理しないほうが楽

#### フレームワークの範囲内で作業する（P.156）

- リポジトリを実装する前に、アーキテクチャフレームワークを慎重に検討する必要がある
    - リポジトリを簡単に作成できるかもしれない
    - 例）J2EEプロジェクトでは、エンティティ Bean は使用していない

#### ファクトリとの関係（P.157）

- 誤解）リポジトリはオブジェクトを生成するからファクトリ！
    - 格納されたオブジェクトを再構成することは、新しい概念オブジェクトを生成することとは違う
    - ファクトリとリポジトリは、別々の責務
        - ファクトリ = 新しいオブジェクトを生成
        - リポジトリ = 古いオブジェクトを見つけ出す
- 新しいオブジェクトと既存オブジェクトを区別すること
    - 両方を組み合わせて実装すると、状況を混乱させてしまう

#### 関係データベースに合わせてオブジェクトを設計する（P.159）

関係データベース ＝ RDB

- 両者間にある不整合
    - DBの主目的がオブジェクトを格納することである
    - DBが、別のシステムのために設計されている
    - DBは該当するシステムのために設計されているが、オブジェクトを格納する以外の役割を果たしている


# 第7章 言語を使用する：応用例（P.163）

## 貨物輸送システムを導入する

- 次の3つの基本的な機能が必要
    - 顧客貨物に対する主要な荷役を追跡する
    - あらかじめ貨物を予約する
    - 貨物が荷役の過程で所定の場所に到達した際に、自動的に請求書を顧客に送付する

荷役（にやく、にえき）→ 貨物の積み込みや荷降ろし、あるいは倉庫・ヤード等への入庫・出庫を総称した作業のこと

## ドメインを隔離する：アプリケーションの導入（P.166）

- ドメインの責務が、システムの他の部分が持つ責務と混ざらないようにするため、レイヤ化アーキテクチャを適用してドメイン層を区切る
    - 1. 特定の貨物に対して行われた過去と現在の荷役にアクセスできる追跡問い合わせ
    - 2. 新規の貨物を登録できるようにして、それに対してシステムの準備を整える予約アプリケーション
    - 3. 貨物に対して行われた各荷役を記録できるイベント記録アプリケーション（追跡問い合わせで検索される情報を提供する）

## エンティティと値オブジェクトを区別する（P.166）

- 顧客
    - エンティティ
- 貨物（Cargo）
    - エンティティ
    - 貨物1つ1つ追跡IDを割り当てている
- 荷役イベント（Handling Event) と輸送機器移動（Carrier Movement）
    - エンティティ
    - 現実世界の出来事を反映していて、通常は置き換えることができないから。
- 位置（Location）
    - エンティティ
    - 緯度と経度から一意なキーとするのは、実用的ではない
    - 
- 配送記録（Delivery History）
    - エンティティ
    - 交換できないから。
    - 配送記録は貨物と1対1になるべき
- 配送仕様（Delivery Specification）
    - 値オブジェクト
    - 同じ場所に向かっている2つの貨物がある場合、同一の配送**仕様**を共有することはできるが、配送**記録**を共有することはできない
- 役割とその他の属性（P.168）
    - 値オブジェクト

## 輸送ドメインの関連を設計する（P.168）

- 発送した貨物全てに対して顧客が直接参照を持っていた場合
    - 顧客が長年のリピータであったときに使いにくい
    - 顧客は貨物に固有のものではない
    - 顧客には多くのオブジェクトに対して果たす役割がある
        - 特定の責務からは解放すべき
        - 例）顧客から貨物を検索する場合、クエリを発行すれば実現できる ｌzl 
- ビジネスとして追跡したいのは貨物だけ
    - 荷役イベントから輸送機器移動への関連のみ辿れるようにする
        - 1つのオブジェクトへの参照へと単純化される

## 集約の境界（P.170）

- 貨物(ルートエンティティ)の集約は、特定の貨物がなければ存在しないであろうもの
    - 配送記録
    - 配送仕様
- 荷役イベントは別
    - 荷役イベントを検索する2つの方法
        - コレクションの代わりとして、配送記録に関する荷役イベントを見つける → 貨物の集約内に閉じることになる
        - 特定の輸送機器移動に向けて、荷積みと準備を行うすべての業務を見つける → 貨物の集約内に閉じれない → 別の集約であるべき

## リポジトリを選択する（P.171）

- 予約アプリケーションのために…
    - 顧客リポジトリ
- アクティビティ記録アプリケーションのために…
    - 輸送機器移動リポジトリ
- どの貨物が荷積みされたかシステムに伝えなければならないので…
    - 貨物リポジトリ
- 荷役イベントリポジトリがないのは…
    - 配送記録との関連は、コレクションとして実装することにしたから
    - アプリケーションの要求にはないから

## シナリオをウォークスルーする（P.173）

### サンプルアプリケーションの機能：貨物の荷出し地を変更する

荷出し地 ＝ 配送先？ = というかドメイン言語かもしれない

- 配送先を間違えて頼んでしまった場合
    - 配送仕様は値オブジェクトなので、いまあるものを破棄して新しいオブジェクトを取得して、貨物のセッターメソッドを使用して、新しい配送仕様で古いものを置き換えればよい

### サンプルアプリケーションの機能：リピータへの対応

- 同じ顧客によって繰り返される予約は似ている傾向があるので、新規の貨物のプロトタイプとして古い貨物を使用したい
    - プロトタイプパターンを使用して設計
    - 貨物はルートエンティティだから、コピーを慎重にしなければならない
        - 配送記録：新しい空の記録を生成
        - 顧客の役割：役割をキーとした顧客を参照するマップは、キーも含めてコピーする
        - 追跡ID：新しい追跡IDを生成
    - 貨物集約の境界内にあるものは全てコピーして修正したが、**集約境界外のものに対しては、影響を及ぼしていない**ことに注意

## オブジェクトの生成（P.174）

### 貨物用のファクトリとコンストラクタ

### 荷役イベントを追加する

## リファクタリングのために立ち止まる：貨物集約についてもう1つの設計（P.177）

- 荷役イベントを追加するときに配送記録を更新しなければならない
  - 貨物集約が↑のトランザクションに巻き込まれる
  - 他のユーザーが貨物を編集していたら、荷役イベントトランザクションは失敗もしくは遅延する可能性がある
    - アプリケーション的には、貨物の編集より、荷役イベントのほうが重要
- 配送記録がもつ荷役イベントのコレクションをクエリで置き換える
  - 荷役イベントをルートとした集約の外部に整合性の問題を引き起こすことなく、荷役イベントを追加できる
  - トランザクションの競合がなくなる
  - 貨物と荷役イベントとの間にある循環参照において、一貫性を保つのも容易になる
- 荷役イベント用にリポジトリを追加する
  - 特定の貨物に関係したイベントに対するクエリをサポートする

## 輸送モデルにおけるモジュール（P.179）

- モジュールへ構成することで、モデルが影響を受ける
- 凝集度の高い概念を探し、プロジェクトにおいて他の人々に伝えたいことに集中すること
  - 顧客、請求、輸送にモジュールを分けている

## 新機能を導入する：配分チェック（P.182）

- 機能内容
  - 特定のタイプの貨物をどれくらい予約するべきかについて配分できるようにする
  - 予約システムと統合したい
- 必要な情報は2箇所
  - 貨物リポジトリ
  - 販売管理システム

#### 2つのシステムを接続する（P.183）

- 予約アプリケーションが販売管理システムの設計を受け入れなければならない
  - 明確なモデル駆動設計を維持することが困難
    - ユビキタス言語に混乱をきたす
- 新規クラスを作成して、予約アプリケーションと販売管理システムの言語間を変換させる
  - 以降、**配分チェックサービス**と呼ぶ = 腐敗防止層
- 今後も統合が必要になったら、その責務を果たすサービスとともに、別の変換サービスが作成されることになる
  - 配分チェックサービスの後ろにいるので、ドメイン設計に出てこない

#### モデルを強化する：ビジネスのセグメント化（P.183）

- 既存のドメインモデルでは、貨物のカテゴリ分けはしていない
  - 新しい概念が必要
- エンタープライズセグメントと呼ばれるクラスを追加する
  - ビジネスの分割方法を定義した次元軸の集まり
  - 各タイプを様々な軸(カテゴリ名や重量など)から表現する
- 配分チェックサービスは、エンタープライズセグメントと外部システムのカテゴリ名との間で変換を行う
- 貨物リポジトリも、エンタープライズセグメントに基づいてクエリを提供する
  - 販売管理システムに変更が加えられても、配分チェックサービスまでで影響範囲が収まる

#### パフォーマンスチューニング（P.186）

- 販売管理システムが別サーバで稼働して、地理的にも別の場所にあるかもしれない
  - 通信のオーバーヘッドが発生するかも
  - 取得した貨物のエンタープライズセグメントをキャッシュして、配分チェックサービスのあるサーバへ配置しなおせるようにして、メッセージングのオーバーヘッドを減らす

# 第8章 ブレイクスルー（P.195）

ブレイクスルーとは？
本質的な課題を打ち破る革新的な解決策

- コードとモデルを改良するたびに、開発者の視界は明確になってくる
  - 洞察のブレイクスルーをもたらす可能性がある
- ブレイクスルーを引き起こそうとしてはいけない
  - 適度なリファクタリングを行う必要がある

# 第9章 暗黙的な概念を明示的にする（P.207）

ドメインモデルとそれに対応したコードが大きく変更するのは、議論で示唆されたり、設計の中に暗に存在したりする概念に開発者が気づき、それを1つあるいは複数のオブジェクトや関係性を使って、モデルの中で明示的に表現したとき

## 概念を掘り出す（P.207）

- 開発者は、暗黙的に潜んでいる概念を明らかにする手がかりに対して敏感にならなければならない
  - 積極的に探さなければならない

### 言葉に耳を傾ける（P.208）

- ドメインエキスパートが使う言葉に耳を傾けること
  - 何か複雑なものを完結に述べている用語がないだろうか？
  - ドメインエキスパートに言葉の選び方を正されていないか？
  - 自分が特定のフレーズを使ったときに、ドメインエキスパートは困惑した表情をしていないか？
- モデルにとって、有益になり得る概念を示す手がかりである

#### 例9.1 - 輸送モデルに欠けている概念を聞き分ける（P.209）

- エキスパートに耳を傾けることによって、「輸送日程」の概念を明示的にすることができた
  - エキスパートにとってどれだけ重要かもわかった

### ぎこちなさを精査する（P.212）

- 掘り下げるべきは、設計の中でも最もぎこちない部分
  - 手続きによって、説明しにくい複雑な処理が行われているところ
  - 新しい要求が出るたびに、複雑さが増しているようなところ
- モデルの解決策が浮かばない場合は…
  - 積極的にドメインエキスパートを調査に参加させるべき

#### 例9.2 - 利息を得る 難しい方法（P.213）

- 利息計算サービスがぎこちなかった（複雑だった） 
  - 「発生」という用語を掘り出せたことで、ユビキタス言語が豊かになった
    - 支払いと利益が切り離され、より深いモデルになった

### 矛盾について熟考する（P.218）

- ドメインエキスパートが同一人物だとしても、注意して分析すると整合性が合わないことがある
  - プログラムの要件を掘り下げる際に常に遭遇するものだが、より深いモデルへの大きな手がかりになり得る
  - すべての矛盾に折り合いをつけることは現実的ではない

#### 文献を読む（P.218）

- 多くの分野において、基本的な概念や社会通念について解説している文献が見つかる
  - 本を読むことで、首尾一貫し深く検討された見方を始められるかもしれない

#### 例 9.3 - 利息を得る 文献を用いた場合（P.219）

- ドメインエキスパートがソフトウェア開発にあまり関心がない
- エキスパートをたよってブレインストーミングができない
  - そのドメインの書籍を読むことで理解を深め、深まったモデルを作ることができる

### 何度でも挑戦すること（P.221）

- 試行錯誤を繰り返すことで、より優れた考え方が生み出される
  - モデラや設計者は、自身の考えに固執してはいけない
- 方向性を変えることは無駄ではない
  - 変更するたびに、より深い洞察がモデルに反映される
- リファクタリングするたびに、設計はよりしなやかになる
  - 次回の変更がより容易になる


## それほど明白でない概念をモデル化する方法（P.221）

オブジェクト指向における3つのカテゴリについて議論する

#### 明示的な制約（P.221）

- 制約は暗黙的に現れることが多い
  - 明示的に表現する
  - 制約を独立したメソッドに分割、明白な名前をつける
    - 設計上でも、制約を明示できるようになる
    - 制約についても議論がしやくなる
- 制約によって、オブジェクトの基本的責務が曖昧になっている場合
- 制約がドメインでははっきりと見てとれるのに、モデルがそうでもない場合
  - 制約をくくりだして明示的に1オブジェクトにする
  - オブジェクトの集まりとそれらの関係性としてモデル化してもよい

### ドメインオブジェクトとしてのプロセス（P.224）

- ドメインに存在するプロセスは、モデルの中に表現されなければならない
  - サービス：こんなプロセスを明示的に表現しつつ、極端に複雑なアルゴリズムを引き続きカプセル化する方法の1つ
  - プロセスの実行方法が複数ある場合：アルゴリズムそのものやアルゴリズムの主要な部分を独立したオブジェクトにするというアプローチがある（詳細は第12章 ドメインにおけるストラテジーの使用について）
- 明示すべきプロセスと隠蔽すべきプロセスを区別するためには？
  - ドメインエキスパートが話題に上げるものか、コンピュータ・プログラムにおける仕組みの一部に過ぎないか
- 制約とプロセスは、オブジェクト指向言語でプログラミングしているときにすぐには思い浮かばない、2大モデル概念
  - これらは一旦モデル要素として考えるようにすると、設計は鋭くなる

# 第10章 しなやかな設計（P.247）

- ソフトウェアの最終的な目的は、ユーザーの役に立つこと
  - それ以前に、そのソフトウェアは開発者の役に立たなければならない
    - リファクタリングを重視するプロセスに特に当てはまる
- 複雑なふるまいをするソフトウェアの設計が優れたものでないと、リファクタリングしたり、複数の要素を結びつけたりするのは困難
  - 開発者が暗黙的に含まれているものを予測できないと、コードは重複する
  - 設計要素が一枚岩のようになっていると、各部分を再結合させることができないため、重複が避けられない
  - ソフトウェアの設計が明確でないと、リファクタリングとイテレーションによる改良をしなくなる
- **しなやかな設計とは？**
  - 過去に作成したレガシーにおよって押しつぶされないようにし、開発の進行に合わせてプロジェクトを加速させるためには、楽しく仕事ができて変更を呼び込むような設計
- 扱いやすいソフトウェアの設計はシンプル
  - だが、シンプルに作成することは容易ではない

## 意図の明確なインタフェース（P.251）

- 開発者がコンポーネントを使用するために、その実装についてじっくり考えなければならないのであれば、カプセル化の価値は失われている
  - コンポーネントを開発した人とは別の人が、オブジェクトや操作の目的を推測するためにコードを確認しなければならないのであれば、新しい開発者は、操作やクラスが偶然満たしているだけの機能を目的と勘違いしてしまうかもしれない
  - 推測された目的が本来の意図と異なっていたら、設計の概念的な基盤が崩壊し、2人の開発者は互いに矛盾した目的に向けて仕事をすることになる
- 型名、メソッド名、引数名が全て組み合わされ、意図の明白なインタフェースを形成する
  - クラスと操作には、その効果と目的を記述する名前をつけて、約束したことを実行する手段には言及しないこと
    - クライアント開発者はインタフェースの内部を理解しなくてよくなる
    - こうした名前はユビキタス言語に従っていなければならない
    - ユビキタス言語にすることで、チームメンバーは意味を推測することができる
    - 振る舞いを作成する前にテストを書いて、自分がインタフェースの開発者の視点で考えられるようになる

## 副作用のない関数（P.255）

- 操作はコマンド(command) と クエリ(query) の2つのカテゴリに分けられる
  - コマンド(command)：システムに何らかの変更を与える操作
  - クエリ(query)：システムから情報を取得するもの
- 副作用を起こさずに結果を戻す操作は関数(function)と呼ばれる
  - 関数は何度呼び出しても、同じ値を戻すことができる
  - 副作用とは、コンピュータ科学では、システムの状態に対して与えられる、あらゆる影響を意味する。
    - ここでは、システムの状態に対するあらゆる変化のうちで将来の操作に影響するもの
- ほとんどのソフトウェアはコマンドを使用する。この問題を抑える方法は2つある。
  - 1. コマンドとクエリを別の操作に厳密に分離する
    - 変更を引き起こすメソッドに関して、ドメインデータを戻さないようにすること
    - 可能な限りシンプルに保つこと
    - クエリと演算を全て、目に見える副作用を起こさないメソッドで実行するとこ
  - 2. オブジェクトを変更する代わりに新しい値オブジェクトを生成して戻す
    - 値オブジェクトは不変なので、すべての操作は関数になる
    - 関数と同じように、値オブジェクトも安全に利用することができ、テストも容易である
- しなやかな設計のためには、プログラムのロジックをできる限り関数にすること
- 副作用のあるコマンドとは厳密に分離して、ドメインについての情報を戻さない、単純な操作をすること
- 値オブジェクトの責務に合致する場合には、複雑なロジックをその値オブジェクトに移すことによって、副作用をさらに制御すること


## 表明（P.261）

- 複雑な演算を副作用のない関数に分離することによって、問題は適当な大きさに切り詰められる
- エンティティ上にはまだ副作用を作り出すコマンドが残っており、そのコマンドを使用する人は誰でも、結果を理解していなければならない
  - 表明があることで、副作用が明示的になり、対処しやすくなる
- 操作の副作用が実装によって暗黙的にしか定義されていない場合、委譲が多く行われている設計では、原因と結果がもつれる
  - カプセル化の価値は失われる（分岐をたどらないと分からないため）
  - 抽象化も意味がなくなる
- 操作の事後条件と、クラス及び集約の不変条件を宣言すること
  - プログラミング言語で表明を直接コーディングできない場合は、自動化されたユニットテストを書くこと
  - プロジェクトの開発プロセスのスタイルに合う場合には、表明をドキュメンテーションや図の中に記述すること
- 凝集した概念が集まったモデルを探し求めること
  - 意図された表明を開発者に推測させ、学習効率を上げながら、矛盾したコードが作られるリスクを小さくするものでなければならない

## 概念の輪郭（P.266）

- オブジェクトの粒度は、むやみに細かくしたり粗くしたりすればよいわけではない
- ドメインにはいくつもの概念が隠されていて、それら凝集度の高い概念群の間には目に見えない境界線 = 概念の輪郭が存在する
- モデルのリファクタリングを繰り返すことで、概念の輪郭を見つけ出し、オブジェクトの粒度がその輪郭に沿うようにする
  - これがドメインモデリングにおける高凝集のガイドライン













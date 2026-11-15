# 設計書 — The Little Book of Kaggle 1st Place Solutions

公開用仕様 3.1 / 2026年11月15日

## 0. 目的と使い方

この設計書と、収録するKaggleコンペの正式名またはURLの一覧から、日本語の技術書を制作する。実行AIは一次資料の調査、執筆、独自図の作成、表紙イラストの新規生成、PDF組版、内容と全ページの検査を行う。組版・検査コードと表紙の生成仕様は末尾のテキスト付録に収録する。以前の会話、参照書籍の手元コピー、別添の画像を入力として必要としない。

必要な実行能力は、Web資料の取得、Pythonによるファイル処理とPDF生成、画像生成、生成画像とPDFページの視覚確認である。実行AIは作業開始時に使える機能を確認する。表紙を生成できない環境では本文制作を進め、表紙生成に必要な機能を不足として報告する。静的な既存画像や仮の図形を完成表紙へ代用して成功としない。

利用者は例えば「この設計書に従い、［コンペAのURL］、［コンペBのURL］をこの順に収録した書籍を完成させてください」と依頼できる。AIは指定順を保持し、曖昧な別年・部門等は公式資料から解決する。調べても章の内容を決められない曖昧さだけを利用者に確認する。通常の表記・配置・試験方法の判断で制作を止めない。

既定の書名は `The Little Book of Kaggle 1st Place Solutions`、本文は日本語、著者表示はなし。序章、各コンペの四部構成、終章、付録を含める。公開・外部サービスへの登録は、利用者が依頼したときに行う。

### 0.1 再現性を三つに分ける

| 再現する対象 | 新しい書籍で固定するもの | 変わるもの・求めない一致 |
| --- | --- | --- |
| 内容と編集 | 初学者にも追える説明、四部構成、根拠のある1位解法、解法図と探索図、章末課題 | 競技固有の事実、例、図、コード、文章。旧書籍の文章や同じ140ページへの固定は求めない |
| 紙面と表紙の設計 | 判型、本文9/13 pt、余白、図表・引用・柱・目次、白地と階調による読書風景の表紙 | 改ページ、章長、新規生成する挿絵の具体的な構図・細部 |
| 確定した一冊の再出力 | 採用済み原稿・画像・コード・書体・依存版 | 同じ資材と環境では本文・ページ数・PDFハッシュの一致を確認する。新しい画像を生成した別の版とのハッシュ一致は求めない |

組版コードは、完成した原稿JSONからPDFを作る。競技の調査・本文の判断・表紙画像の新規生成は、この設計書を読んだAIが担当する。組版試験の合格を、未調査のコンペの内容が正しい証拠として使わない。

### 0.2 完成時に保存するもの

| ファイル | 役割 |
| --- | --- |
| `book.pdf` | 新規生成した前表紙と本文を連結した閲覧版 |
| `interior.pdf` / `front-cover.pdf` | 表紙を除く本文と、前表紙単体 |
| `book.json` | 全原稿、章順、図表、出典・主張の対応、採用した表紙画像の指定 |
| `assets/` | その書籍用に生成した表紙、独自図の元データ、数式等の素材 |
| `source-log.jsonl` / `claim-log.jsonl` | 取得状態・資料の版と、重要な主張の根拠 |
| `cover-generation.json` | 実際のプロンプト、生成機能、取得できた設定、画像寸法・ハッシュ・採用理由 |
| `content-review.json` | 対象原稿・根拠台帳へ結び付いた独立した内容監査の記録 |
| `review.json` | 対象PDFへ結び付いた全ページの視覚確認と警告の処理理由 |
| `manifest.json` / `qa.json` | ページ数、書体・依存・ファイルのハッシュ、生成ID、技術検査と公開判定 |
| `制作元.zip` | 確定入力、独自素材、生成・検査コード、依存情報、根拠と検証記録 |

`wrap-cover.pdf` は必要な場合に作る。寸法確認用の展開表紙と、印刷会社・KDPの公式テンプレートへ照合した入稿用表紙を区別する。閲覧版 `book.pdf` をそのまま本文入稿用として提出しない。

本文・調査結果・図の編集元・再開情報はファイルへ保存する。長いコードをチャットへ貼り直さず、付録はファイル操作で抽出する。制作が中断した場合は、この設計書と保存済みの進捗から再開する。

## 1. 完成品の品質基準

再制作の到達点は、読者が「何を作る競技か」「何を測るか」「基本解法のどこが足りないか」「1位解法が何を変えたか」「自分ならどの比較を選ぶか」を説明できる一冊である。モデル名の一覧や、公開解法の短い要約だけを完成品にしない。

| 観点 | 必須の確認 | 不合格となる例 |
| --- | --- | --- |
| 競技の同定 | 年・部門・順位と考案者・解法の対応 | 別部門の順位、本人資料と異なる解法 |
| タスクの理解 | 入出力・制約・一件の例・採点と集約 | スコアの向きが逆、例で使う情報が本番では見えない |
| 解法の説明 | 基本解法からの差、主要構成の入出力と理由 | 手法名だけ、図と本文の工程が食い違う |
| 学び直す道筋 | 観察、複数仮説、比較、採否・戻り先 | 完成パラメータを答えとして配るだけ、本人の心理を創作 |
| 根拠と実測 | 本人報告・コード読解・教材実行・探索案の区分 | 未実行のコードを実行済み、公開得点を本書実測と表示 |
| 読解可能性 | 初出用語、記号、数式の小例、図の前後の説明 | 未定義の略語、同じ説明の反復による水増し |
| 紙面 | 全頁の機械検査と、読める倍率での点検 | 欠落、切れ、重なり、孤立見出し、崩れた表・コード |
| 再出力 | 確定入力・採用画像・環境から別の出力先へ再生成 | 未添付の画像や古い原稿への依存、改頁と目次の不一致 |

参照書籍の本文は140ページ、各コンペ章は20–30ページ程度だった。この密度は目安とし、新規コンペの情報量に応じて調整する。必要な説明を削ったり、本文を縮小したり、同じ文章を反復したりしてページ数へ合わせない。試験用の短縮版は短縮版と明示し、通常の一冊の説明深度を検証したことにはしない。


## 2. 一冊の編集設計

想定読者は、Kaggleや対象分野の知識が十分でない読者から、解法を自分で追試したい実践者までとする。最初から数式やモデル名を並べず、「何を入力し、何を返し、どう採点されるか」を一件の具体例から説明する。用語は初出で役割を説明し、その後に正式名・略称を示す。既に説明した一般用語を章ごとに長く繰り返す必要はないが、その章だけでも入出力と採点を追えるようにする。

本文は連続した説明文を主とする。箇条書き、表、数式、コード、図は、文章で説明した関係を整理・検証するために使う。節を数行の箇条書きへ置き換えたり、設計メモをそのまま本文へ貼り付けたりしない。各段落は前の説明を受け、一つの新しい理解へ進める。学習と推論、開発中と本番、観測できる情報と隠された情報、候補選択と主催者採点を混ぜない。

| 順序 | 内容と役割 |
| --- | --- |
| 扉・書誌 | 書名、版、本文言語、資料参照基準日、解法の考案者への帰属と本書の説明の範囲 |
| 全体目次 | 序章、全コンペ章と四節、終章、付録。実際の組版ページを反映する |
| 本書の読み方 | Kaggleの最小限の説明、四部構成、本人報告・本書の実験・説明例・考察の読み分け |
| 序章 | `On Beginning Again`。競技を終えて1位解法を開いた一人の参加者の場面から、調べ直し・再現・次の挑戦へ関心をつなぐ |
| コンペ章 | 一つのコンペを四節で説明する。独自の主要図を少なくとも二つ置く |
| 終章 | `He Will Win the Next Competition`。序章の参加者へ戻り、各章で得た判断の仕方が次の実験に現れる場面で閉じる |
| 付録・奥付 | 共通用語、実験記録のひな型、再現環境の読み方、資料への案内、版と制作基準日 |

序章・終章の参加者は説明のための人物とし、未確認の著者の実体験にしない。「彼」は物語上の参加者であり、読者の属性を限定する呼びかけにしない。既存書籍や有名な序文の表現を長く翻訳・模写せず、独自に書く。終章は単なる章別要約で終えず、何を測り、どの比較を選び、どう中止・継続を決めるかを新しい場面へ移す。

参照書籍に近い説明の密度を目指し、各コンペおおむね20～30ページを試し組みの目安にする。章の長さは内容に合わせる。競技数が変われば全体のページ数も変える。水増し、説明の省略、本文サイズの縮小で目標ページ数に合わせない。巻頭・序章・終章・付録にも役割に必要な文章を与える。

## 3. 各コンペ章の必須構成

章タイトルは「第N章 正式コンペ名」とする。以下の四節を必ずこの順に置く。丸数字の見出しや、章ごとに異なる言い換えは使わない。章末事項は第4節の後半または章末の小見出しにまとめ、第五の同格節にして四部構成を崩さない。

### 1. タスク

最初に、小さく具体的な入力と期待される出力を示す。実データを使えない場合は「説明用の例」と明記する。続いて、次のことを本文で説明する。

- 競技の目的と、参加者が作るもの。予測値、生成物、エージェント等のどれか。
- 提出物、提出後の実行、使用できる情報、時間・容量・外部データ等の主要制約。
- 配布されたデータ・コード・評価ヘルパーと、非公開のテスト部分。開発中に見える情報の範囲。
- 一件の評価値と全体の集約。記号、単位、スコアの向き、罰則、同点条件等、解法を理解するために必要な採点規則。
- 一つの小例での計算または処理の追跡と、なぜ単純な方法では難しいか。

数式は装飾として置かない。各記号の意味、何を改善すると値が変わるか、どの段階で計算するかを説明する。公式説明と公開評価実装が異なる場合は、採用する版と差を保持する。複数条件の値を一つの公式スコアのように合成しない。

### 2. 基本解法

まず、入出力が成立する最小の動作例を示し、その後で改善の比較に使う基準解法を説明する。入力、処理、出力、必要な依存、できること、できないことを順に追う。教材として作った方法を、優勝者が実際に最初に使った方法とは書かない。

小さなコードを載せる場合は、目的を先に説明し、実行可能なPython、疑似コード、人間向けの手順を明確に分ける。人間が行う判断をコード枠へ囲んでPythonと表示しない。依存・入力・省略箇所の説明なしに、架空のAPIを実装済みのように呼ばない。出力例は実行ログか説明用の例かを区別する。

### 3. 1位解法

冒頭で、基本解法に対して何を変え、どの制約・失敗を改善したかを一段落で述べる。次に、全体像の主要図Aを置き、データの作成、学習、候補の生成、選択、推論・実行、提出の関係を必要な順に説明する。競技にない工程を形式上追加しない。

重要な部品については、入力と出力、働き、採用理由、根拠、限界を示す。上位に共通する発想と1位の具体的な組み合わせを分ける。可能なら2位等の本人解説と比較するが、資料がなければ比較を捏造しない。本人の報告値、固定したコードから読めた処理、本書で実行した結果を一つの実測として扱わない。

大きなスコア差があっても、条件をそろえた比較がなければ特定の部品の因果効果と断定しない。採用されなかった案、転移しなかった条件、必要資源、公開物だけでは再現できない範囲を、資料が確認できる範囲で示す。公開コードが存在することと、データ・重み・環境までそろって優勝得点を再現できることは区別する。

### 4. 自力で1位解法に辿り着くには

完成解から必要な発見を逆算し、競技中に入手できた情報から前向きに選べる探索の道筋へ組み直す。この節と主要図Bは、本書が提案する思考実験・実験計画であることを明記する。本人の実際の開発年表、心理、失敗履歴として語らない。

各段階に「観察→複数の仮説→切り分ける比較→見る量→採用・棄却・保留の条件→次の行動」を置く。最初から完成した文字列やハイパーパラメータを答えとして渡さず、なぜその要素を調べるのかを前段の観測から説明する。時間・GPU・試行回数が限られる場合の優先順位と、結果が出ないときの戻り先も示す。

章末には、要点、理解を確かめる問いと短い解答、小規模に試せる再現課題、一次資料の一覧、実施済みと未実施の範囲を置く。問いは本文を読めば答えられ、再現課題には入力、実行環境、見る出力、合否の考え方を付ける。未実施の実験には架空の成功率やログを添えない。

## 4. 独自図・表・コードの編集契約

各章に少なくとも主要図A・Bを一つずつ置く。図Aは第3節の処理全体、図Bは第4節の観察・比較・判断の経路を示す。単に同じ箱と矢印を並べた図を章ごとに流用せず、競技固有のボトルネックと判断を反映する。図Aの矢印には実際の入出力関係、図Bの分岐には比較結果に応じた行動を対応させる。

図は新規のベクター作図を基本とする。元図をなぞって独自図と呼ばない。図の前に読む目的を一文で示し、図の後に重要な経路と限界を説明する。概念図と実際の処理結果を区別し、必要な箇所に「模式図」「説明用の例」等を添える。色だけで区別せず、ラベル・形・線種を使う。線と図中文字は最終配置サイズで確認する。

表は比較軸をそろえる。本人報告と本書実測が混じる場合は行ごとの区分と条件を残す。図表番号は章ごとの連番とし、本文から実在する番号へ参照する。図タイトルは中央揃え、表タイトルは左揃え、いずれもゴシック、字下げなし、末尾句点なしとする。通常の本文段落は見出し直後を含めて一字下げにする。この二つの指定を混同しない。

コードの状態は、`未実施`、`構文確認`、`教材実行`、`公開実装の部分実行`、`提出全体の追試`から選び、実際に確認した範囲を記録する。構文が通ることはモデルや採点器を実行した証拠ではない。算術例の実行は採点モデルの成功、自己対戦の学習、優勝得点の再現ではない。外部コードを実行する際は取得元と版、依存、入力、コマンド、出力、資源を保存する。

## 5. 出典と主張を固定する

参照の優先順位は、公式の競技説明・評価・最終順位、優勝者本人の解説・公開コード、他の上位者本人の解説、手法の原論文・公式文書とする。検索結果の抜粋を全文読了と扱わない。本人のページが取得できないときは、取得できた部分と経路を記録する。資料間で重要な矛盾があれば、採用理由を残すか、区分を保持して本文へ説明する。

各章の調査開始時に`source-log.jsonl`と`claim-log.jsonl`を作り、本文と図の制作時にも更新する。以下は構造の例であり、`example`を含むURLやIDを最終原稿へ残さない。

```json
{"id":"C01-S01","kind":"official_spec","url":"https://www.kaggle.com/competitions/example/overview","title":"公式評価説明","retrieved_at":"YYYY-MM-DD","read_status":"body_read","version":null,"locator":"Evaluation","redistribution":"link_only"}
```

`read_status`は`body_read`、`partial`、`body_read_via_index`、`metadata_only`、`unavailable`を使う。取得したコードにはコミットSHAやNotebookの版を保存する。ハッシュは実際に保存したバイトに対してだけ付ける。出典の存在と、本文の重要な主張を実際に支えていることを分けて確認する。

```json
{"id":"C01-CL01","text":"ここに採点の向きと集約方法の確定文を置く","kind":"official_spec","source_ids":["C01-S01"],"locator":"Evaluationの該当段落","verification":"supported","used_in":["C01.1","F1-A"]}
```

`kind`は`official_spec`、`author_report`、`code_reading`、`book_experiment`、`synthetic_example`、`reverse_engineered_path`を区別する。順位、スコア、候補数、学習量、計算資源、所要時間、各部品の採否には出典または実行記録を対応させる。説明用の数値と本書の探索案には、その区分を本文にも示す。全ての一般的な接続文へ引用を付ける必要はない。

本文の引用番号は、全書で一意の章接頭辞付きIDを用い、括弧を含めて本文より小さい7ptの上付きにする。章末の資料一覧にはID、資料名、考案者または発行主体、URL、取得日、採用版を記す。URLの文字列だけで資料を同定させない。存在しないID、孤立した出典、重複したIDを検査する。

外部の文章・図・コード・データ・重みをそのまま再配布することは既定にしない。独自の説明と構成図を作り、原資料は取得先を示す。必要な短い引用等を採用する場合には、その出所と使用条件を記録する。出典を付けたことだけで転載条件を満たしたとみなさない。認証情報や非公開資料を本文・Git・ログへ保存しない。

## 6. 制作と再開の手順

| 段階 | AIが実行すること | 保存する中間成果 | 次へ進む条件 |
| --- | --- | --- | --- |
| 0 環境確認 | コンペ順・調査・画像生成・Python・視覚確認の機能を確認し、コードを抽出する | request.json、環境の版 | 必要能力と書体の準備ができる |
| 1 競技の同定 | 年・部門・公式URL・順位を確認し、本人資料を探索する | source-log、取得状態 | 競技と採用解法が対応する |
| 2 根拠の固定 | 採点、制約、採用構成、重要値を確認する | claim-log、矛盾と不足の一覧 | 四節を書くための必須事実が確認できる |
| 3 章の設計 | 一件の導入例、四節の説明順、図A/B、再現課題を作る | chapter-plan | 各図と説明の根拠、読者の到達点が対応する |
| 4 執筆と作図 | 説明文、数式、表、教材コード、独自図を制作する | 編集元、図の元データ、book.json | 四節・二図・章末事項がそろい、仮置きがない |
| 5 内容検査 | 出典、数値、式、コード区分、本文と図を照合する | content-review | 重要な未根拠主張、架空の実測、参照欠落がない |
| 5b 表紙生成 | 固定した意匠に従い画像を新規生成し、原寸と前表紙PDFで採否を判断する | 採用画像、プロンプト、生成・採用記録 | 構図・白地・画質・文字なし・配置の条件を満たす |
| 6 全書の組版 | 巻頭・序章・終章・付録を統合し、参照実装で生成する | 本文・新規表紙・閲覧版・生成記録 | 実ページ目次、章順、偶数総数、背幅の入力が一致する |
| 7 全頁確認と修正 | 全ページを描画し、読み取れる倍率で確認する | ページ別QA、修正記録 | 切れ・重なり・欠字・読みづらい図表が残らない |
| 8 再生成と保存 | 確定した入力から別ディレクトリへ再生成し、比較する | ハッシュ、ページ数、検証結果、最終ファイル | 同じ入力と環境で一致し、未確認範囲が記録される |

章単位で独立に調査・執筆を進めても、用語、引用ID、章番号、図表番号は統合時に検査する。内容の調査とPDFの検査は異なる作業である。PDFが生成できたことを、採点式や優勝解法の事実確認の代わりにしない。

長い制作では`progress.json`と`resume.md`を更新する。後者には確定済み入力、完成した章、残件、現在のファイル、次に実行する具体的な一手を記す。中断後のAIは、この設計書と保存ファイルを読み、完了済みの調査・原稿を生かして続行する。失敗した実行でも確認済みの成果を消さず、失敗状態のPDFは合格版と分ける。

変更が入ったら、その影響を受ける箇所を再確認する。採点仕様の変更は式・例・図・第4節の探索案へ、章順の変更は章番号・引用・図表番号・目次へ、文字組の変更は全改ページ・ページ数・表紙寸法へ反映する。古いPDFの検査結果を新しいPDFの合格記録として使わない。

## 7. 完成判定

完成と報告する前に、次の三つを別々に判定する。

| 判定 | 必須の証拠 |
| --- | --- |
| 内容が完成 | 指定順の全コンペ、四節、主要二図、章末事項、巻頭・序章・終章・付録がそろう。重要事実は一次資料または記録で支えられ、仮置き・未根拠の断定がない |
| PDFが完成 | 全頁の寸法、フォント埋め込み、実ページ目次、文字組、図表・コード・数式、引用、章柱・ノンブルを機械検査と全頁の視覚確認で確かめる |
| 再生成が可能 | この設計書から抽出した実装、確定入力、独自素材、依存版、実行コマンドがそろい、別の出力先への再生成を実際に成功させる |

PDFの検査では、本文全段落の一字下げ、見出し直後の一字下げ、図表タイトルのゴシック・末尾句点なし・字下げなし、表タイトルの左揃え、括弧込み上付き引用、奇数ページ上部右の章柱、外側のノンブルを重点的に点検する。段落・コード・表セル・図中文字の内容を抽出して、入力にある重要なテキストが出力から欠落していないかも確認する。

表紙を採用して確定した一冊の再生成では、画像生成を再実行せず、まずページ数、本文抽出結果、ページ寸法、図表・コードの存在を比較する。実装が決定的な出力を保証する環境ではPDFのSHA-256も一致させる。環境差による字体・改行の差を許容するときは、その差と環境を明記する。内容の編集品質、紙面の健全性、確定資材のバイト一致を分けて報告する。

取得不能の必須資料、解消できない重要な資料矛盾、未知のフォント文字、本文の欠落、組版のはみ出し、全頁未確認は、完成判定を止める。AIは代替経路と修正を試し、それでも解決しない項目だけを具体的に報告する。補助的な上位比較資料の欠如やGPU追試の未実施は、それを明記すれば書籍の完成を妨げない。未実施の優勝得点追試を、書籍PDF生成の再現性試験へ混ぜない。

参照実装のテストに説明用の競技・数値・短文を使った場合、その試験は組版とデータ処理の確認として記録する。別の実在コンペについて、調査から一冊の内容確認まで実行したとは報告しない。完成後も、新しいコンペを入力するたびに一次資料の確認と本文の内容検査を行う。

KDP用の裏表紙・背付き表紙を追加する場合は、その時点の紙・印刷条件・実ページ数で公式条件とテンプレートを確認する。閲覧版の本文・前表紙の生成成功を、KDPの受付、Print Previewer、実物校正の完了とは扱わない。


### 7.1 公開判定は五つの条件のANDとする

`public_release_ready` は、次の全条件を満たしたときだけ真になる。途中の機械検査が合格したこととは区別する。

1. **公開用入力**：トップレベルに `"profile": "public"` を明示し、正式な競技識別子、出典・主張台帳、採用表紙の生成記録が整っている。本文9pt・行送り13ptを固定する。
2. **内容監査**：現在の原稿と根拠台帳に結び付いた `content-review.json` があり、必須の8観点が全て合格し、未解決の重要主張・完成阻害事項がない。
3. **機械検査**：本文の全表示文字と出典参照を原稿へ対応付けた文字サイズ検査を含め、全ての技術検査が合格する。
4. **全頁の視覚確認**：検査対象PDFのハッシュに対応する全ページの確認記録があり、未処理の確認フラグがない。
5. **独立した再出力**：同一入力・同一実装から別の出力先へ実際に二度生成し、全PDFのバイト列が一致する。比較先の省略、同じディレクトリ、同じ生成結果をコピーしただけの比較は合格にしない。

参照実装は、生成のたびに異なる `build_id` をmanifestへ記録する。PDFの文字・画像・日時情報等は従来どおり決定的に生成するため、同じ資材ならPDFハッシュは一致する。`build_id` を含むmanifest自体のバイト一致は要求しない。

入力の `profile` が省略または `draft` の場合、機械検査に合格しても公開判定は偽となる。公開用入力の検査は既定で上記の受入判定を要求する。途中の版面確認には `--layout-only` を明示する。この場合の `passed` は技術検査の結果であり、`pass_scope` は `technical_only`、公開可否は別の `public_release_ready` を読む。最終検査には `--require-public-release` を使う。

内容監査は、出典の真偽や文章の妥当性をプログラムが自動証明するものではない。AIまたは人が実際に資料・原稿を確認し、その記録の完全性と対象原稿への対応を検査する。重要な公式仕様・本人報告・コード読解の主張は、既定で `essential: true` と扱い、`verification: "supported"` を必須とする。補足的な未確定事項を記載する場合は `essential: false` と明示し、`limitation` に限定を記し、本文にもその範囲を表す。


## 8. 表紙を毎回新規生成する


### 8.1 固定する意匠と変えてよい要素

前表紙は108 × 175 mm、白地とする。英文書名は上から `The Little Book`、`of`、`Kaggle 1st Place Solutions` の3行、17 pt、中央54 mm位置に置く。ページ上端から各基準線まで30.0 / 41.75 / 53.5 mmを基準にする。著者名は表示しない。文字はPDF組版時に配置し、画像へ焼き込まない。

イラストは、実行環境で利用できるAIの画像生成機能を使い、書籍を新規制作するたびに生成する。同じコンペ一覧でも、新規の書き起こしとして依頼された場合は新しい画像を生成する。古い表紙画像、Base64、利用者固有の画像パスを必要としない。利用者がコンペ一覧だけを渡した場合は、以下の既定プロンプトを使ってAIが制作し、候補を確認して採用画像を決める。

> 白い紙の上に描かれた、静かな庭の読書風景の挿絵。庭の小さなテーブルに開いた本があり、そばに一羽のガチョウがいる。草木や庭の道が控えめに背景をつくる。上品な技術書の表紙に合う、繊細な線と柔らかな鉛筆・淡墨の階調。白から黒までのグレースケール。落ち着いた明暗、細部を詰め込みすぎない。縦横比4:5の縦長構図。四辺には白い余白を設け、絵が白地へ自然につながる。文字、数字、ロゴ、透かし、枠、書籍全体のモックアップを描かない。小さく配置しても開いた本と庭の情景が読み取れる、完成した一枚のイラスト。

固定するのは、白地、グレースケール、静かな庭と読書、開いた本・テーブル・ガチョウ、穏やかな線と階調、文字を含めないこと、縦長の配置である。植物の種類、テーブルや道の向き、小物の位置、光の向き等は毎回変えてよい。コンペの題材を反映するときも、一つの控えめな小物や形にとどめ、競技のロゴや説明図へ置き換えない。利用者の追加指示がなければ、AIがこの範囲で変化を決める。

画像の配置領域は、表紙左上から約14.9 / 59.663 mm、幅78.2 × 高さ97.716 mmとする。生成画像は原寸で実効300 ppi以上を確保する。必要画素数の下限は幅924 × 高さ1155 pxであり、利用可能なら1024 × 1280 px以上の縦長出力を用いる。生成機能の対応サイズを確認し、対応していないパラメータを架空のAPIで指定しない。比率がわずかに異なる画像は白地を補って領域へ収め、引き伸ばしで変形しない。主要な物体を切るトリミングや低解像度画像の単純拡大で合格にしない。

生成後は画像そのものと、書名を組んだ前表紙PDFを別々に確認する。書名との衝突、異物や不自然な物体、読めない文字に似た模様、強すぎる黒、細かすぎる描写、白地の不連続があれば、プロンプトを直して再生成する。小型判の実寸表示と拡大表示の双方で静かで読みやすい表紙に仕上げる。

採用後は画像ファイルを固定し、同じ書籍の組版をやり直す際に画像生成を繰り返さない。画像を変えるのは、新しい書籍の制作または表紙改訂のときである。制作元には採用画像、最終プロンプト、実行した生成機能の名称と取得できた設定、作成日、画素寸法、画像ハッシュ、配置寸法、採用理由を残す。設定値や生成日時を記憶から補わない。

### 8.2 採用条件

| 対象 | 合格条件 |
| --- | --- |
| 設計 | 白地、3行の17 pt書名、108 × 175 mm、指定した配置領域が保たれている |
| 挿絵 | 今回の制作で新規生成し、静かな庭・本・テーブル・ガチョウの情景を認識できる |
| 画質 | 配置時300 ppi以上。比率の変形がなく、主要な物体が欠けていない |
| 階調 | 白黒主体の階調で読め、白地へ自然につながり、暗部で形が潰れていない |
| 文字 | 文字はPDFで組まれ、挿絵に擬似文字・透かし・ロゴがない。書名と絵が衝突しない |
| 確認 | 生成画像、実寸の前表紙PDF、拡大した前表紙PDFを確認し、確認結果を記録している |


画像のエンコード、埋込みデータ、既存画像の固定URLを、この設計書へ追加しない。プロンプトと採用条件を再利用し、新しい書籍では新しい画像を作る。単純な線画への置換、古いPNGの無断再利用、対応していない生成パラメータの創作で工程を省略しない。

生成機能の出力はRGB形式の場合がある。見た目のモノクロ表現と、RGBの全画素が厳密に同値であるグレースケールを区別して検査・記録する。厳密な白黒入稿が必要なときは正規のプリプレス工程で色空間をそろえ、変換後のPDFを再検査する。画像生成のプロンプトだけで色空間まで合格と推定しない。

## 9. 紙面の固定仕様

| 要素 | 指定 |
| --- | --- |
| 判型・綴じ | 108 × 175 mm、横組み、左綴じ、白地、単段、本文裁ち落としなし |
| 本文 | 明朝系9 pt、行送り13 pt、黒。全段落の冒頭を1字＝9 pt下げる。見出し直後も同じ |
| 左右の余白 | 内側13 mm、外側10 mm、本文幅85 mm。偶数・奇数で左右を反転 |
| 上下の基準 | 上12 mm、下15 mm。柱とノンブルは本文に重ねない |
| 章見出し | 明朝太字14 pt。正式名を複数行にし、縮小で押し込まない |
| 四節の見出し | 明朝太字11 pt、同一階層・同一書式 |
| 項見出し | ゴシック太字9 pt |
| 図番号・図タイトル | ゴシック太字7 pt、中央揃え、字下げ0、末尾句点なし |
| 表番号・表タイトル | ゴシック太字7 pt、左揃え、字下げ0、末尾句点なし |
| 出典参照 | 括弧込みで7 pt、基準線より約2.4 pt上げる。全書で一意のID |
| コード | 等幅7 pt以上、行送り9.5 pt程度。改行・空白を保持し、長行は表示上折り返す |
| 図と表の文字 | 最終配置で7 pt以上。主要な罫線・図の線は0.75 pt以上 |
| 章柱 | 技術章の奇数ページ上部右、7 pt。章頭・白ページには付けない |
| ノンブル | 7 pt、本文版面の外側。偶数左・奇数右、基準線は下端9 mm。扉と意図的白ページは表示しない |
| 目次 | 序章、各章・四節、終章、付録の実開始ページから生成する |
| ページ数 | 本文は偶数へ確定する。調整白ページも本文総数に含める。前表紙は含めない |

書体は明朝・ゴシック・等幅・英文ローマンの役割を分ける。参照実装のNoto系とLiberation Serifは、埋込みと配布条件を確認できる静的書体を明示して用いる。元の参照PDFの汎用的な埋込み名から書体ファミリーを断定しない。同じ寸法でも書体を変えれば改行は変わるため、変更後に再検査する。

本文の字下げは段落スタイルで指定し、先頭の全角空白を重ねない。図表タイトル、コード、表セル、数式には本文用の字下げを誤適用しない。出典を通常の本文ブロック `p` で記す場合は1字下げとする。専用リストの体裁が必要なら、対応するスタイルを実装して検査する。

### 9.1 改頁と情報を失わない配置

見出しだけがページ下端に残る配置、図とタイトルの分離、表の列見出しの欠落を認めない。短いコードはまとまりで保ち、長いコードは意味のある関数・処理単位で分ける。単位がページを超える場合は、原稿の例を小さく再設計し、完全なソースを制作元へ保存する。構文を切って紙面へ収めない。

長いURL・識別子・英語の正式名を含むページを検査する。勝手な空白の挿入で意味を変えず、表示上の折返しと編集元を区別する。表の一行がページより高い場合は、内容を複数行や本文へ分け、読み手が対応を追えるようにする。図は縦横比を保ち、ノード内の文字の収まり、矢印と文字の交差、別ノードとの重なりを確認する。

必要な数式を本文から落とさない。単純な式はUnicodeで組み、記号・単位・代入例を添える。分数・行列等は、実行環境の正規の数式組版機能で図版化するか、検査付きで対応を追加する。文字列の `$...$` や `\\frac` が自動的に数式として組まれると仮定しない。

### 9.2 ページ数と印刷条件

本文が300ページを超えるなど、確定ページ数に対して内側余白が不足する場合は、余白を増やして再組版する。ページ数、余白、目次、表紙の背幅が一致するまで反復する。新しい文字サイズへ勝手に縮小して解決しない。内蔵実装は300ページまで内側13mm、301–500ページで16mm以上へ切り替えて再組版する。500ページを超える書籍は、検証済みの大冊用プロファイルを追加するまで明示的に停止する。下記の公式余白表があることを、その区分の実装済みという意味にしない。

KDP入稿時は公式の最新条件とテンプレートを確認する。2026年11月15日に確認した最低内側余白は、24–150ページ9.6 mm、151–300ページ12.7 mm、301–500ページ15.9 mm、501–700ページ19.1 mm、701–828ページ22.3 mm。白黒・白用紙の背幅の参考式は `本文ページ数 × 0.002252 × 25.4 mm`、展開表紙の全幅は `216 + 背幅 + 6.35 mm`、高さ181.35 mmである。紙・インクを変更した場合は対応条件を再確認する。

ローカルでの検査、公式テンプレートへの照合、Print Previewer、紙の校正刷りを別々に記録する。閲覧版の生成成功から、外部の受付や実物の印刷結果を推定しない。

## 10. 実行環境と入力データ

### 10.1 テキスト付録を抽出する

このファイルを空の作業ディレクトリへ `設計書.md` として保存し、末尾の抽出コマンドを実行する。抽出するのは、組版コード、検査コード、組版試験用JSON、表紙生成用プロンプトの4つのUTF-8テキストである。画像データは含まれない。抽出時に各資材のバイト数とSHA-256を照合する。

試験用JSONは説明用の架空競技を含み、内容の完成品ではない。新しく生成した表紙画像を指定して組版機能を確認するために使う。実在のコンペの本文は、AIが一次資料を確認して別の `book.json` へ制作する。

### 10.2 依存と書体

検証環境はPython 3.12.14 / Linux x86_64。Python 3.10以上の独立環境で次を導入する。他の版を使う場合は版を記録し、改めて検査する。

```bash
python3 -m venv .venv
. .venv/bin/activate
python3 -m pip install reportlab==4.4.9 fonttools==4.61.1 pypdf==6.21.4 Pillow==13.0.0 PyMuPDF==1.26.6
```

PDF出力はReportLabとpypdf、書体処理はfontTools、検査・描画はPyMuPDFを使う。Popplerの `pdffonts` / `pdftoppm` も検査に利用できる。Debian/Ubuntu系では日本語書体に `fonts-noto-cjk`、英文書体に `fonts-liberation`、描画等に `poppler-utils` を導入できる。

他の環境ではNoto等の公式配布元から、埋込み可能な静的TTF/OTF/TTCを用意して `fonts` へパスを明示する。CID参照だけで書体の埋込みを省略しない。コードは使用文字の存在を検査し、CFF形式を必要な文字にサブセット化してTrueType輪郭へ変換する。欠字を空白や別の文字へ黙って置換しない。

### 10.3 原稿の構造

| フィールド | 内容 |
| --- | --- |
| `profile` | 完成・公開用原稿はトップレベルに `"public"` を明示。省略・`"draft"` は技術検査用で、公開可能にはならない |
| `book` | 書名、表紙3行、著者表示、本文9/13 pt、章の奇数開始、新規生成画像のパスと生成記録 |
| `fonts` | 明朝、明朝太字、ゴシック、ゴシック太字、等幅、英文ローマンの書体パス。省略時は実装の候補を使う |
| `frontmatter` | 書誌・本書の読み方等のブロック。目次は組版結果から自動生成 |
| `prologue` / `epilogue` / `appendix` | `title` と `blocks` を持つオブジェクト |
| `chapters` | 指定順の章。正式名、競技識別子、四つの `sections` |
| `sources` / `claims` | 公開用の原稿内に保持する出典と重要主張。外部の作業台帳と同期する |

`p` は本文、`h2` は項見出し、`formula` はUnicodeの式、`code` はコード、`table` は表、`figure` は独自図を表す。図は正規化したノード・矢印でベクター描画するか、最終配置で300 ppi以上の画像を指定する。図・表の番号は章内連番で付与し、タイトルへ重ねて書かない。本文の `[[C01-S01]]` は括弧込みの上付き参照へ変換する。任意のHTMLは解釈しない。

公開用入力では、出典ID、主張と根拠、コードの種類、表紙の生成記録等を明示する。構文・参照・素材の整合をプログラムで検査しても、資料が主張を正しく支えるかはAIが本文と照合する。詳細なフィールドと対応範囲は内蔵コード先頭のスキーマ説明を正とし、未対応の入力を削除して通さない。

### 10.4 生成して確定する

表紙を新規生成し、例えば `assets/cover.png` として保存する。生成仕様と採用記録を `cover-generation.json` に残し、入力の `book.cover_image` と `book.cover_provenance` を実ファイルへ対応させる。ファイル名の慣例は自由だが、古い固定画像を前提にしない。

```bash
python3 portable_book.py --input book.json --output release-a
python3 portable_book.py --input book.json --output release-b
python3 verify_reproduction.py --input book.json --output release-a --layout-only --report qa-technical.json
```

一度採用した表紙画像は、この二回の組版では再生成しない。新規制作の差異と、同じ一冊の再出力の一致を分離して検査する。上の `--layout-only` は途中の技術検査である。次節で内容監査・全頁確認を記録した後、比較先と両監査ファイルを指定した公開用の最終検査を実行する。


## 11. 内容・レイアウト・再生成の受入試験

### 11.1 内容を監査する

各章について、競技の正式名・部門・確定順位と考案者、入出力、採点式、制約、1位解法の主要構成を一次資料へ戻って確認する。少なくとも、採点を追う一件の小例、基本解法からの差を説明する段落、図A/Bと本文の対応、確認問いと解答、再現課題、実施範囲を点検する。重要な値には本文の出典IDまたは実行記録を対応させる。

原稿を書いたAI以外の独立した読み直しを行う。疑わしい記述は原資料まで確認し、部分的に取得できた資料を全文読了としない。競技後に更新されたコードは、その版の読解として書く。競技当時の最終提出と同一であることを別途確認していなければ、同一と断定しない。

実行可能な教材は実際に実行して出力を保存し、紙面のコードと突き合わせる。Pythonの構文確認、架空入力の算術、公開実装の部分実行、全体の学習・推論・提出を区別する。未実施の範囲を明記すれば、教材としての書籍制作は進められる。未実施を成功として記すことは認めない。

### 11.2 全ページを機械検査する

寸法、偶数本文ページ数、表紙との連結、章順、実ページ目次、埋込み書体、文字サイズ、行送り、字下げ、図表タイトル、引用、柱・ノンブルを調べる。原稿の本文・表セル・コード・図ラベルが出力へ保持されているか確認する。繰り返した文章も、出現回数と改頁を考慮して照合する。

見えている文字の座標、文字同士の重なり、紙面外や版面外へのはみ出し、後から白で隠された文字、細すぎる線、消えた図の枠、意図しない白ページ、孤立見出しを検査する。入力側では図のノードと矢印の衝突、コードの論理単位、素材の存在と実効解像度も確認する。

幾何検査の警告を無条件に無視しない。上付き参照と本文、罫線と表セル、意図した余白など、正当な配置もあるため、確認が必要な警告はページを見て理由付きで処理する。実際のはみ出しを許容幅の拡大で通すのではなく、改行や配置の原因を修正する。

検査コード自体についても、意図的に壊したPDFで故障を見つけられるかを確かめる。ハッシュ不一致だけを検出したのでは配置検査の証明にならない。検査用に生成記録と連結PDFのハッシュを更新した後でも、重なり、欠落、文字サイズ、図の欠損等の対象故障を検出することを確認する。


本文の文字サイズは「9ptの文字が存在するか」では判定しない。原稿の全 `p` と `formula` を読順に並べ、版面内の通常明朝書体による表示文字列と一対一で照合する。その上で、空白・改行を除く全表示文字について、原稿の本文位置は9pt、原稿の `[[出典ID]]` に対応する位置だけは7ptと照合する。7ptの本文を出典参照だと推測して除外しない。見出し・表・コード・図・目次・柱・ノンブルは別書体の役割として区別し、それぞれの既存検査へ渡す。

この照合は、単にPDF中の `Tf` の数値を見るのではなく、描画後の実際の文字サイズを使う。書体の役割が曖昧、表示文字の数や順序が原稿と不一致、段落の一部が別書体へ変わった等で対応を確定できない場合も不合格にする。検査結果には照合ブロック数・文字数と、不一致のページ・原稿位置・期待値・実測値を残す。参照テンプレートの書体構成を変更した場合は、役割の対応も検証し、未識別の文字を無視して成功としない。

### 11.3 全ページを読める倍率で点検する

全ページを描画し、本文・図中文字・コード・表セルを実際に読める倍率で順に確認する。小さな一覧は構成の確認に使えるが、それだけで全頁点検を完了としない。分担する場合は、ページ範囲と対象PDFのハッシュを明示し、抜け・重複を管理する。

確認するのは、切れ・重なり・欠字・文字化け、長い正式名やURL、意図しない改頁、見出しと後続本文、図とタイトル、長表の継続、コードの空白と論理単位、数式の記号・添字、余白と読み進める順序である。余白が大きいページは、不可分の教材や図を次ページへ送った理由が妥当かを判断する。必要な内容を重複させて埋めない。

採用画像単体と、書名を配置した表紙PDFも、実寸と拡大で確認する。擬似文字、不自然な物体、黒つぶれ、主要要素の欠け、比率の変形、書名との干渉があれば再生成または配置の修正を行う。

修正後は影響するページを再確認する。改頁が変わった場合は、その後の本文・目次・ノンブル・背幅まで再検査する。PDFのハッシュが変わったら、旧記録をそのまま合格扱いにしない。同じ条件で描画したページ画像の画素・寸法が完全に一致するページだけは、画像ハッシュと元の確認記録を対応させて引き継げる。画像が変わったページは必ず読める倍率で再確認する。新PDFの全ページがこのいずれかで覆われることを記録する。

### 11.4 内容監査・視覚確認・再生成を公開判定へ結び付ける

`content-review.json` には、原稿と根拠台帳の独立した読み直しを記録する。原稿を書いたAI自身の「完成した」という宣言だけで埋めない。次の8観点を実際に確認し、各項目に具体的な確認内容を記す。

| キー | 監査対象 |
| --- | --- |
| `competition_identity` | 正式名・年・部門・順位・本人解法の対応 |
| `task_metric_constraints` | 入出力、採点・集約、制約、情報の可用性 |
| `winner_solution_sources` | 1位解法の主要構成と一次資料・固定実装の対応 |
| `examples_and_math` | 説明例、計算、式、条件のそろった比較 |
| `figures_and_text` | 図A/Bと本文の意味の一致 |
| `code_execution_scope` | コードの内容、実行記録、実施済み・未実施の区分 |
| `reconstructed_path_labeling` | 第4節を本人の開発史・実測と混同していないこと |
| `chapter_structure_and_endmatter` | 四部構成・章末事項・一冊の構成・説明の深さ |

以下は未監査のテンプレートであり、そのままでは公開判定に合格しない。全項目について実際の監査と必要な修正を終えた後、`status` を `pass` とし、`note` に具体的な根拠を記す。

```json
{
  "schema_version": "1.0",
  "status": "pending",
  "input_sha256": "book.jsonの実ハッシュ",
  "manuscript_sha256": "本文構造の実ダイジェスト",
  "sources_claims_sha256": "出典・主張台帳の実ダイジェスト",
  "reviewer": "実際に独立監査したAIまたは人の識別",
  "method": "実際に確認した方法と範囲",
  "checks": {
    "competition_identity": {"status": "pending", "note": ""},
    "task_metric_constraints": {"status": "pending", "note": ""},
    "winner_solution_sources": {"status": "pending", "note": ""},
    "examples_and_math": {"status": "pending", "note": ""},
    "figures_and_text": {"status": "pending", "note": ""},
    "code_execution_scope": {"status": "pending", "note": ""},
    "reconstructed_path_labeling": {"status": "pending", "note": ""},
    "chapter_structure_and_endmatter": {"status": "pending", "note": ""}
  },
  "blocking_issues": [],
  "unresolved_essential_claim_ids": []
}
```

次のコマンドは原稿の識別値だけを計算する。監査項目を自動で合格へ変更しない。

```bash
python3 - book.json <<'PY'
import json,sys
from verify_reproduction import sha,manuscript_digest,sources_claims_digest
from pathlib import Path
p=Path(sys.argv[1]);data=json.loads(p.read_text(encoding='utf-8'))
print(json.dumps({"input_sha256":sha(p),"manuscript_sha256":manuscript_digest(data),
                  "sources_claims_sha256":sources_claims_digest(data)},ensure_ascii=False,indent=2))
PY
```

`input_sha256` は実際の入力ファイル、`manuscript_sha256` は巻頭・序章・各章・終章・付録の正規化JSON、`sources_claims_sha256` は出典・主張台帳の正規化JSONを識別する。いずれかが対象と一致しなければ、内容監査済みとは判定しない。本文や台帳を変更した場合は、影響する箇所を再監査する。表紙情報やJSON整形のみを変更した場合も、本文・台帳の同一性と変更内容を確認し、入力ハッシュの対応を更新した経緯を残す。

視覚確認は、別の `review.json` へ実際に読める倍率で確認したPDFのハッシュ、ページ番号、方法、警告の処理理由を保存する。次のページ配列は形式例であり、そのまま全頁確認の証拠にしない。

```json
{
  "full_size_visual_review": {
    "pdf_sha256": "対象interior.pdfの実ハッシュ",
    "pages": [1, 2, 3],
    "method": "readable-scale page-by-page"
  },
  "accepted_flags": {
    "whitespace-p13": "ページを確認し、短い教材全体を次ページへ置くための余白と判断"
  }
}
```

公開用の最終検査では、次を実行する。

```bash
python3 verify_reproduction.py --input book.json --output release-a --compare release-b --review-decisions review.json --content-review content-review.json --require-public-release --require-visual-review --report qa.json
```

`passed: true`、`pass_scope: "public_release"`、`public_release_ready: true` の全てを確認する。公開用モード、出典・主張、表紙生成記録、内容監査、全頁確認、未処理フラグ、独立した再出力、技術検査のいずれかが欠ければ不合格となり、CLIも非ゼロの終了コードを返す。公開用入力に対しては `--require-public-release` を省略してもこの厳しい判定が既定になる。

`--layout-only` は執筆途中の技術検査用である。内容監査を省略して「公開可能」と表示するためのオプションではない。内容の正しさ、画像の新規生成の実体、記録した監査を本当に実施したかを、ファイルの形式検査だけで自動認証できるとは主張しない。


### 11.5 確定資材から再出力する

完成した `book.json`、採用画像、独自素材、コード、書体と依存を固定し、別の出力先へもう一度生成する。同じ一冊では画像生成を再実行せず、ページ数、抽出本文、全PDFのSHA-256が一致するか確認する。入力・素材を別のディレクトリへ移した場合にも、絶対パスによってPDFの内容が変わらないことを確認する。

異なる章数、長い正式名・数式・表・コード、新しい画像比率などの変更を加えたときは、その入力の内容と紙面を改めて検査する。二つの実在コンペを検証したことを、将来の全コンペ・全入力の保証へ広げない。新規制作のたびに、この節の受入試験を実行する。


## 12. 検証記録と適用範囲

第12.1–12.2節は、3.0で得た実在二競技の内容・紙面の検証来歴である。3.1の公開判定と文字サイズ検査の受入結果は第12.3節に示す。過去のコードハッシュを現行版の実装と混同せず、現行資材の完全性は第14節を正とする。

### 12.1 何を再現し、何を再現していないか

2.0の実績は合成原稿の組版と固定資材の再生成に限られ、新しい実在コンペの内容を制作できることの裏付けが不足していた。3.0では次を分離して実証した。

| 対象 | 確認した再現・改善 | 確認していない範囲 |
| --- | --- | --- |
| 内容 | 別分野の実在二競技を一次資料から新規執筆。四節・図・教材・出典を独立監査 | 未調査の全コンペへの無条件の一般化 |
| 紙面 | 9/13pt・小型判・図表・引用等を維持し、全68頁を確認。実原稿で見つかった右余白超過と数値・引用の分断を修正 | 元書籍の全画素・全改頁・元字体の完全一致 |
| 表紙 | 静的PNGを撤去し、同じ生成仕様から独立した二画像を制作。配置・17pt書名・解像度を検査 | 同一プロンプトでの同一画素、厳密なDeviceGray |
| 固定版の再生成 | 原稿・採用画像・環境を固定した4PDFのSHA-256一致 | 新規画像を生成した別版との同一ハッシュ |
| 教材と実験 | 小さなPython教材の実行と出力の照合 | 実競技データの全学習・実動画推論・優勝得点の追試 |
| 数式 | 読み下せる行内演算表記と記号の説明 | 任意TeXの自動組版。必要な書籍では数式素材を追加して検査する |

### 12.2 実在コンペによる最終受入試験

2026年11月15日（日本時間）、新たに選んだ二つの実在コンペについて、一次資料の確認、新規原稿・独自図の制作、全書PDFの生成と検証を行った。元の五章や合成文章を新しい章の本文として流用していない。

| 対象 | 最終結果 |
| --- | --- |
| 第1章 Optiver Realized Volatility Prediction | 本文7–32ページ、26ページ、四節・主要図2点 |
| 第2章 Deepfake Detection Challenge | 本文33–62ページ、30ページ、四節・主要図2点 |
| 全書 | 本文68ページ、前表紙付き閲覧版69ページ。巻頭・序章・終章・付録を含む |
| 根拠の管理 | 24出典・20主張。19件supported、1件limited。取得索引・本文直接読解・部分取得を区別 |
| 主版の最終検査 | 47項目合格、全68ページの視覚確認記録、未解決フラグ0、public_release_ready=true |
| 同じ入力・素材から別出力先への再生成 | 本文・前表紙・閲覧版・展開表紙の4種類でSHA-256完全一致 |
| 章順を反転 | 68ページ、44項目合格。新しい目次・柱・章番号・図表番号が一致 |
| 表紙を別生成したB案へ変更 | 本文SHA-256は同一、表紙と閲覧版は異なる。17pt書名・寸法・画素・解像度・縦横比を確認 |
| 意図的に破損させたPDFの検査 | 6種類すべてを狙った検査で検出。manifestと閲覧版を更新し、単なるハッシュ不一致を検出理由にしない |
| 公開用メタデータの異常入力 | 9種類すべてで明示エラー。失敗PDFを完成出力へ昇格しない |

実在原稿の初回66ページでは、ReportLabの句読点ぶら下げによる版面超過を検出した。厳密な禁則・幅計算へ修正した後は68ページとなり、本文9pt・行送り13ptのまま、文字・図形のはみ出し、重なり、欠字、白塗りによる遮蔽を検査して合格した。さらに通常の整数・小数・負数・指数表記、終端の引用番号、ASCII開き括弧を扱い、読みづらい分断を修正した。

全68ページは150–165.6dpiの読める大きさで個別確認した。修正後は、変更ページを読み直し、他のページは最終PDFから再描画した全ページRGB画素が既確認画像と完全一致することを証拠として引き継いだ。PDFのハッシュが変わっただけで古い確認を一括流用したのではない。

章順反転版は全ページの機械検査に加え、全56章ページの本文・文字サイズ・配置・ベクター図形を、章番号等の変更を正規化して比較した。目次、章頭、節の途中など7ページを読める大きさで目視確認した。反転版の全68ページを再度目視したとは主張しない。

破損試験は、同じ位置への二重描画、後置白矩形による文字遮蔽、ページ外への移動、図タイトルの6pt化、予期しない白ページ、図の線画だけの削除である。公開メタデータの試験は、出典不足、競技重複、未知の引用ID、本文未読資料をsupportedとした主張、参照位置不足、表紙制作記録不足、表紙ハッシュ不一致、未知の根拠ID、教材実行ログ不足である。

教材Pythonは別途実行した。Optiver章ではRV=0.005000、RMSPE=0.158113883、定数予測=0.012000、画像章では架空値のlog loss=0.860505を確認した。これは教材計算であり、実データの学習や優勝得点の追試ではない。公式最終得点はnyanpの0.19548、Selim Seferbekovの0.42798であることを、公式順位表・主催者資料へ戻って確認した。

任意のTeX入力、未知の競技の無調査での執筆、KDPでの受付、紙の校正刷り、出版社の人間による校閲は今回の合格範囲に含めない。表紙A/Bは新規生成した階調風のRGB画像であり、厳密な無彩色チャンネルやDeviceGrayへの適合を宣言しない。新しい組み合わせごとに一次資料と本文の内容監査を行う。

| 最終主版の出力 | SHA-256 |
| --- | --- |
| `interior.pdf` | `f1611a806c13cc46ab82c9cecd0ef7e2bad28f3e4c3413b9bfd5ea65e7787f3a` |
| `front-cover.pdf` | `6d2bd51ad25799fe047c4461ba48f500bbb7e12bfa09ef0283ebd2136336943a` |
| `book.pdf` | `8c024cc2778e2d89b45e74dc326cd21138b0a029d5b006069ad67b646d2c82e0` |
| `wrap-cover.pdf` | `243d6c1844a7295453c826ecd0b023a050b90b9f1299b72545ed85d9734c290e` |

生成コード：`35049471390a75b74201997e71bcd0d16d77059605be9dbc157ac14a3edaf56f`。検査コード：`66de9d1384f473e62018868912af77451a71841fde5bbeeed388893026d9e958`。入力原稿：`516179e8d19821df735c11b4dda1cc00f24ce1f640c8eb2882f6d8851a837e01`。固定した依存版と書体ハッシュは最終manifestへ記録した。


### 12.3 3.1で修正した判定と受入結果

3.0の評価では、公開用のメタデータを持たない試験原稿でも、視覚確認の記録さえ指定すれば `public_release_ready` が真になり得た。また、本文の一部を9ptから8ptへ変更しても、ほかに9ptの本文が残っていると旧検査は見逃した。3.1では前者を公開用の必須条件のAND、後者を原稿と表示文字の全件照合へ置き換えた。

**本文の指定は9pt、行送り13pt、出典の上付き参照は7ptのままである。8ptは検出能力を試すために評価用PDFのコピーへ入れた故障であり、本文の新しい指定でも、上付き参照の指定でもない。** 配布用の生成物を8ptへ変更していない。

| 3.1の受入対象 | 実際に確認した結果 |
| --- | --- |
| 正常な公開用入力 | 既存の実在二競技・本文68頁について58検査全て合格。`pass_scope: public_release`、`public_release_ready: true` |
| 本文と原稿の対応 | 本文・数式248ブロック、空白・改行を除く33,635文字が原稿順に一致 |
| 通常本文と数式 | 33,283文字全てが9pt。出典参照を除いた文字を全件検査 |
| 出典参照 | 原稿に指定した352文字全てが7pt。本文の7ptを参照だと推測して除外しない |
| 故障を入れた実PDF | 12頁の通常本文を8ptへ変更、本文1文字だけを8ptへ変更、本文1文字だけを7ptへ変更、出典参照を8ptへ変更した4例を、対象の文字サイズ検査で全て不合格と判定 |
| 公開判定の欠落・不一致 | 公開モード、出典・主張、表紙生成記録、監査の対象ハッシュ・必須項目・阻害事項、全頁確認、未処理フラグ、比較先の欠落・同一先・同じ生成結果のコピー等、19例を該当する公開条件で不合格と判定 |
| CLIと下書きの区別 | 公開用入力は監査等を省略すると終了コード非ゼロ。以前すり抜けた下書きは技術検査に合格しても公開不可。下書きに公開判定を要求した場合も不合格 |
| 小さい組版試験用原稿 | 架空競技を含む試験入力でも本文・数式30ブロック、1,632文字を照合。技術検査は合格し、内容の完成品でない下書きを公開可能とは判定しない |
| 独立した再出力 | 別々に実行した二回の生成IDは異なり、4種類のPDFのSHA-256は全て一致。本文・表紙・改頁・文字配置も3.0の検証済み最終版と同じ |

受入試験は、正常例1件、公開条件の故障19件、実PDFの文字サイズ故障4件、CLI・下書きの統合確認3件の計27件を実行した。故障PDFはmanifestと連結閲覧PDFも更新し、単なる古いハッシュの不一致ではなく、意図した検査が失敗することを確認した。公開条件の個別試験も、該当条件の判定を検証した。

今回の3.1では、既存の検証書籍の原稿・根拠台帳・採用画像を変更していない。内容監査は、同じ本文ダイジェスト `560969188805d638c1bd8ce7f57020dbcb9206eada8fb52621593d1f3afac42b` に対する既存の独立監査を8観点へ対応付け、入力・本文・根拠台帳の識別値とともに記録した。全68頁の視覚確認も、同じ `interior.pdf` のハッシュに対応する実施済み記録を引き継いだ。未確認のページを新しく合格扱いにしたものではない。

4PDFのハッシュは第12.2節の値と一致した。3.1の実装は第14節のハッシュで識別する。本文の変更がないため、今回の修正を新たな競技内容の制作実績や、三つ目の実在競技の検証実績とは数えない。新しい競技の組合せでは、その原稿に対する内容監査・全頁確認・再出力を実施して初めて公開可能とする。


### 12.4 再現しないものと、追加が必要な場合

元書籍の文章、全ページ数、字体・改頁・画素の完全一致は対象ではない。新しい競技の内容は新たに調査して書き起こし、表紙も新たに生成する。画像生成の結果や将来の競技の資料取得を、組版プログラムだけで保証するものではない。

参照実装はUnicodeと行内演算表記の数式に対応するが、TeXエンジンや数学記号の自動フォント切替は内蔵しない。検証書籍では `sqrt` や `_i` などを用いた読み下せる式も使った。分数・行列等を精密に組む書籍では、実行AIが正規の数式組版機能で独自の数式素材を作り、記号の定義と元データを保持し、最終配置で点検する。対応していない記号を黙って落として通さない。

複雑な図の自動経路探索、原資料の真偽の自動認証、全ての視覚的不具合の自動検出も内蔵しない。図の構成、出典と主張の対応、全ページの視覚確認はAIが実施する。検証済みの二競技を超える入力では、内容と配置の受入試験を再実行する。

画像生成の同じプロンプトから同じ画素が得られるとは主張しない。新しい書籍の表紙は採用条件を満たす範囲で変化し、採用後の一冊の再組版ではその画像を固定する。RGBで得られた階調イラストと、厳密なグレースケール色空間は区別する。今回の新規画像は見た目が白黒主体のRGB画像であり、DeviceGrayの入稿認定ではない。

KDP登録、Print Previewer、校正刷り、公開競技データを使った勝者の全学習・実推論・優勝得点の再現は、この設計書の受入試験では実施していない。これらを本文PDFの生成や教材算術の成功と混同しない。

## 13. 公式資料と実装の対応範囲

固定した実行環境で検証した。新しい依存版に更新するときは、行分割・数式・表・コード・図・目次の回帰試験と全頁確認をやり直す。とくに内蔵の厳密な日本語行分割は、ReportLab 4.4.9に対して検証した実装である。

- [ReportLab公式ユーザーガイド](https://www.reportlab.com/docs/reportlab-userguide.pdf)
- [fontTools公式文書](https://fonttools.readthedocs.io/)
- [pypdf公式文書](https://pypdf.readthedocs.io/)
- [Noto CJK公式配布元](https://github.com/notofonts/noto-cjk)
- [KDP Print Options](https://kdp.amazon.com/en_US/help/topic/G201834180)
- [KDP Set Trim Size, Bleed, and Margins](https://kdp.amazon.com/en_US/help/topic/GVBQ3CMEQW3W2VL6)
- [KDP Paperback Submission Guidelines](https://kdp.amazon.com/en_US/help/topic/G201857950)
- [KDP Create a Paperback Cover](https://kdp.amazon.com/en_US/help/topic/G201953020)
- [KDP Cover Calculator](https://kdp.amazon.com/cover-templates)

## 14. テキスト資材の抽出と完全性

下記の4資材を抽出する。PNG、Base64、固定画像へのURLは含めない。生成画像は制作のたびに別途作り、その書籍の制作元へ保存する。試験JSONの `book.cover_image` は、実際に生成した画像の相対パスへ設定してから使う。

```bash
python3 - 設計書.md <<'PY'
import pathlib,re,sys,hashlib
text=pathlib.Path(sys.argv[1]).read_text(encoding='utf-8')
assets=re.findall(r'<!-- asset:([A-Za-z0-9_.-]+);encoding:text -->\n```[^\n]*\n(.*?)\n```',text,re.S)
expected={'portable_book.py','verify_reproduction.py','layout-fixture.json','cover-prompt.txt'}
assert len(assets)==len(expected) and {n for n,_ in assets}==expected,'資材の欠落・重複'
for name,body in assets:
    p=pathlib.Path(name)
    assert not p.exists(),f'既存ファイルを保護: {p}'
    data=(body+'\n').encode('utf-8')
    row=re.search(r'\| `'+re.escape(name)+r'` \| (\d+) \| `([0-9a-f]{64})` \|',text)
    assert row and len(data)==int(row[1]) and hashlib.sha256(data).hexdigest()==row[2],f'資材の不一致: {name}'
    p.write_bytes(data)
print('4つのテキスト資材を抽出しました。表紙は新規生成してください。')
PY
```

| ファイル | bytes | SHA-256 |
| --- | ---: | --- |
| `portable_book.py` | 49084 | `316ad0a5b648be3808264a5c55c4246b38cf621ee19a1c85dceb8d816d7da25e` |
| `verify_reproduction.py` | 53209 | `ca09ce8a73e8a6b8be803f53b471d0982e5d80f36501a1a4916305bcdaf81606` |
| `layout-fixture.json` | 13171 | `d48e8a679ab05c557839af70b92545ea931ef1f96e67ba59ebd30b50144b21f7` |
| `cover-prompt.txt` | 1536 | `fef6bd1f1d7ac0b0f253f17bfd5a3070d2a77355bd1944f1f96a9851478630ad` |

## 15. 内蔵テキスト資材

### portable_book.py

<!-- asset:portable_book.py;encoding:text -->
```python
#!/usr/bin/env python3
"""Portable book renderer 3.1. Python >=3.10; reportlab, fonttools, pypdf, pillow.

Input JSON:
{ "book": {"title": str, "cover_lines": [str,str,str], "author": null|str,
  "body_pt":9,"leading_pt":13,"odd_chapters":true,"wrap_cover":true,
  "cover_image":"assets/new-cover.png", "inner_mm":13, "auto_gutter":true},
  "fonts": {"serif":path,"sans":path,"bold":path,"sans_bold":path,"mono":path,"roman":path},
  "font_numbers": {"serif":0,"sans":0,"bold":0,"sans_bold":0,"mono":5},
  "frontmatter": [block,...], "prologue":{"title":str,"blocks":[block,...]},
  "chapters":[{"title":str,"sections":[{"title":required_title,"blocks":[block,...]}]}],
  "epilogue":{"title":str,"blocks":[block,...]},"appendix":{"title":str,"blocks":[block,...]}}
Required section titles, in order: タスク / 基本解法 / 1位解法 / 自力で1位解法に辿り着くには.
Block types:
  p: {type:'p',text:str}; h2: same; formula: same (Unicode, no TeX parser);
  code: {type:'code',text:str,language:str,kind:'python'|'python_fragment'|'pseudocode'|'text'}; table: {type:'table',title:str,
  headers:[str,...],rows:[[str,...],...],widths?:[positive fractions,...]};
  figure: {type:'figure',title:str,height_mm?:float,nodes:[{id,label,x,y,w,h}],
  edges:[[from_id,to_id],...]}, normalized coordinates; or figure with path to PNG/JPG.
Public profile (top-level profile:'public') fixes body9/leading13 and additionally requires:
  sources:[{id,url,title,kind,read_status}], claims:[{id,text,kind,source_ids,
  locator,verification:'supported'|'limited'|'unconfirmed'}], and chapter.competition_slug.
  Source read_status: body_read, partial, body_read_via_index, metadata_only, unavailable.
  cover_provenance in book: {kind:'new_generation'|'new_original',prompt|description,
  sha256,generation_run_id?}. This records a new book's illustration; rerenders reuse
  those same verified bytes. The renderer does not create or bundle any artwork.
Figures with path use width_mm/height_mm as an aspect-preserving contain box;
  default bounds are current text width x 105 mm. Both body and cover need >=300 ppi.
Code units for long non-Python blocks may be supplied as units:[str,...], whose
  newline join reproduces text. Whole short blocks stay together. Complete Python
  modules split only between top-level AST statements; functions never split. An
  oversized indivisible unit fails with an explicit error rather than overflowing.
The 301..500 page profile uses inner gutter >=16 mm; auto_gutter rerenders when
  needed. Books exceeding 500 pages fail until a separately verified profile exists.
Citations in prose: [[S01]] -> superscript [S01]. Literal XML is escaped.
All paths other than font paths must remain below the input JSON directory.
Each successful manifest has a fresh build_id; the PDFs remain deterministic.
Publication acceptance is performed by verify_reproduction.py with a bound content
audit, complete visual review and a separately generated matching output.
No network, manuscript generation, claim verification, or KDP certification occurs here.
"""
from __future__ import annotations
import argparse, ast, hashlib, html, importlib.metadata, io, json, math, os, re, shutil, sys, tempfile, uuid
from urllib.parse import urlparse
from pathlib import Path
from reportlab import rl_config
from reportlab.lib import colors
from reportlab.lib.enums import TA_CENTER, TA_LEFT
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.units import mm
from reportlab.lib.utils import ImageReader
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont as RLFont
from reportlab.pdfgen import canvas
from reportlab.platypus import (BaseDocTemplate, Flowable, Frame, Image, KeepTogether,
    LongTable, PageBreak, PageTemplate, Paragraph, Spacer, TableStyle, CondPageBreak)
from reportlab.platypus.tableofcontents import TableOfContents
from pypdf import PdfReader, PdfWriter
from PIL import Image as PILImage

# ReportLab's default CJK splitter deliberately hangs closing punctuation outside
# its width. This strict variant instead backs up the preceding character so
# Japanese kinsoku and the declared physical margins are both respected.
# It retains ReportLab fragment objects, superscripts, links, and TOC callbacks.
from reportlab.platypus import paragraph as _rlparagraph
from reportlab.lib.textsplit import ALL_CANNOT_START as _CJK_NO_START, ALL_CANNOT_END as _CJK_NO_END
_CJK_NO_END+='('  # ASCII opening parentheses must also stay off the line end.

_NUMERIC_TOKEN=re.compile(r'[+−-]?(?:[0-9]{1,3}(?:,[0-9]{3})+|[0-9]+)(?:\.[0-9]+)?(?:[eE][+−-]?[0-9]+)?')

def strict_cjk_lines(self,maxWidths):
    if getattr(self,'_splitpara',False) and hasattr(self,'blPara'):return self.blPara
    widths=list(maxWidths) if isinstance(maxWidths,(tuple,list)) else [maxWidths]
    _rlparagraph._handleBulletWidth(self.bulletText,self.style,widths)
    units=[]
    for fragment in self.frags:
        text=getattr(fragment,'text','')
        if isinstance(text,bytes):text=text.decode('utf-8')
        # Keep normal decimal/scientific numbers and source citations whole.
        # A token longer than a whole line may fall back to character wrapping.
        if getattr(fragment,'rise',0)>0 or not text:
            unit=_rlparagraph.cjkU(text,fragment,'utf-8')
            if text.startswith('[') and text.endswith(']'):unit._strict_atomic='citation'
            units.append(unit)
        else:
            previous=0
            for match in _NUMERIC_TOKEN.finditer(text):
                units.extend(_rlparagraph.cjkU(char,fragment,'utf-8') for char in text[previous:match.start()])
                token=_rlparagraph.cjkU(match.group(),fragment,'utf-8')
                if token.width<=min(widths)+1e-6:
                    token._strict_atomic='number';units.append(token)
                else:units.extend(_rlparagraph.cjkU(char,fragment,'utf-8') for char in match.group())
                previous=match.end()
            units.extend(_rlparagraph.cjkU(char,fragment,'utf-8') for char in text[previous:])
    calc=getattr(self,'autoLeading',getattr(self.style,'autoLeading','')) not in ('','off')
    lines=[];start=0;n=len(units)
    def first(unit):return unit[0] if unit else ''
    def last(unit):return unit[-1] if unit else ''
    def legal(cut):
        return (cut>=n or first(units[cut]) not in _CJK_NO_START) and (cut==0 or last(units[cut-1]) not in _CJK_NO_END)
    def wordchar(char):return bool(re.fullmatch('[A-Za-z0-9_]',char))
    while start<n:
        # Ordinary word-separating spaces are represented by the line break;
        # NBSP used for code indentation is deliberately preserved.
        if lines:
            skipped=[]
            while start<n and units[start]==' ':skipped.append(units[start]);start+=1
            lines[-1]._strict_source_suffix.extend(skipped)
            if start>=n:break
        limit=float(widths[min(len(lines),len(widths)-1)])
        if limit<=0:raise ValueError('E_TEXT_WIDTH: nonpositive available paragraph width')
        stop=start;used=0.;forced=False
        while stop<n:
            unit=units[stop];width=unit.width
            if hasattr(width,'normalizedValue'):width=width.normalizedValue(limit)
            width=float(width)
            if hasattr(unit.frag,'lineBreak'):
                stop+=1;forced=True;break
            if used+width>limit+1e-6:
                if stop==start:raise ValueError('E_TEXT_UNIT_TOO_WIDE: indivisible glyph/reference exceeds line width')
                break
            used+=width;stop+=1
        if not forced and stop<n:
            cut=stop
            while cut>start and not legal(cut):cut-=1
            if cut<=start:raise ValueError('E_KINSOKU_WIDTH: no legal Japanese break; rewrite this punctuation run')
            # Prefer a nearby Latin word boundary, retaining a character split
            # for unbroken identifiers and URLs that exceed a whole line.
            if wordchar(last(units[cut-1])) and wordchar(first(units[cut])):
                lower=start+max(1,(cut-start)//2)
                for candidate in range(cut-1,lower-1,-1):
                    if legal(candidate) and not (wordchar(last(units[candidate-1])) and wordchar(first(units[candidate]))):
                        cut=candidate;break
            remaining=[unit for unit in units[cut:] if str(unit).strip()]
            if len(remaining)==1 and getattr(remaining[0],'_strict_atomic','')=='citation':
                # A terminal citation must not form a line all by itself. Bring
                # one preceding content unit and its closing punctuation along.
                back=cut-1
                while back>start and (not str(units[back]).strip() or first(units[back]) in _CJK_NO_START):back-=1
                while back>start and not legal(back):back-=1
                if back>start:cut=back
            stop=cut
        visible_stop=stop
        while visible_stop>start and units[visible_stop-1]==' ':visible_stop-=1
        chosen=units[start:visible_stop]
        actual=0.
        for unit in chosen:
            width=unit.width
            if hasattr(width,'normalizedValue'):width=width.normalizedValue(limit)
            actual+=float(width)
        if actual>limit+1e-5:raise ValueError('E_TEXT_OVERFLOW: strict line width invariant failed')
        if chosen:
            line=_rlparagraph.makeCJKParaLine(chosen,limit,actual,limit-actual,forced,calc)
            line._strict_source_suffix=list(units[visible_stop:stop])
            lines.append(line)
        start=stop
    return _rlparagraph.ParaLines(kind=1,lines=lines)

def strict_split_fragments(blPara,start,stop):
    # ReportLab's generic hard splitter appends spaces directly to the printed
    # line fragments. Clone instead, restoring only real source whitespace.
    result=[]
    for line in blPara.lines[start:stop]:
        result.extend(fragment.clone() for fragment in line.words)
        for unit in getattr(line,'_strict_source_suffix',[]):
            result.append(unit.frag.clone(text=str(unit)))
    return result

_original_split_selector=Paragraph._get_split_blParaFunc

def strict_split_selector(self):
    if self.blPara.kind==1 and all(hasattr(line,'_strict_source_suffix') for line in self.blPara.lines):return strict_split_fragments
    return _original_split_selector(self)

Paragraph.breakLinesCJK=strict_cjk_lines
Paragraph._get_split_blParaFunc=strict_split_selector

SECTIONS = ['タスク','基本解法','1位解法','自力で1位解法に辿り着くには']
PAGE = (108*mm,175*mm)
INNER, OUTER, TOP, BOTTOM = 13*mm,10*mm,12*mm,15*mm
WIDTH = PAGE[0]-INNER-OUTER
CITE = re.compile(r'\[\[([A-Za-z0-9_.:-]+)\]\]')
FRAME_HEIGHT = PAGE[1]-TOP-BOTTOM

def configure_layout(book,inner_override=None):
    global INNER, WIDTH
    inner=float(inner_override if inner_override is not None else book.get('inner_mm',13))
    if not 13<=inner<=22.5: fail('E_GUTTER: inner_mm must be 13..22.5 mm')
    INNER=inner*mm;WIDTH=PAGE[0]-INNER-OUTER

def fail(message):
    raise ValueError(message)

def sha(path):
    return hashlib.sha256(Path(path).read_bytes()).hexdigest()

def plain(value, where):
    if not isinstance(value,str) or not value.strip(): fail(f'{where}: nonempty string required')
    return value

def caption(value):
    return plain(value,'caption').rstrip('。．. ')

def safe_asset(root, value):
    p=(root/value).resolve()
    if not p.is_relative_to(root): fail(f'asset outside input directory: {value}')
    if not p.is_file(): fail(f'asset missing: {value}')
    return p

def all_strings(value):
    if isinstance(value,str): yield value
    elif isinstance(value,list):
        for item in value: yield from all_strings(item)
    elif isinstance(value,dict):
        for key,item in value.items():
            if key not in ('path','serif','sans','bold'): yield from all_strings(item)

def rendered_strings(data):
    book=data['book']
    yield from book['cover_lines']
    if book.get('author'):yield book['author']
    def block_text(block):
        for key in ('text','title','language'):
            if key in block:yield str(block[key])
        if block.get('type')=='table':
            for row in [block['headers']]+block['rows']:
                for value in row:yield str(value)
        if block.get('type')=='figure':
            for node in block.get('nodes',[]):yield node['label']
    for block in data.get('frontmatter',[]):yield from block_text(block)
    for name in ('prologue','epilogue','appendix'):
        yield data[name]['title']
        for block in data[name]['blocks']:yield from block_text(block)
    for chapter in data['chapters']:
        yield chapter['title']
        for section in chapter['sections']:
            yield section['title']
            for block in section['blocks']:yield from block_text(block)

def image_layout(block,root,cover=False):
    path=safe_asset(root,plain(block.get('path'),'image path'))
    with PILImage.open(path) as image:
        if image.format not in ('PNG','JPEG'):fail('E_IMAGE_FORMAT: use PNG or JPEG')
        iw,ih=image.size
    if cover:maxw,maxh=78.2*mm,97.7158*mm
    else:
        maxw=float(block.get('width_mm',WIDTH/mm))*mm
        maxh=float(block.get('height_mm',105))*mm
        if not 10*mm<=maxw<=WIDTH+.01:fail('E_IMAGE_WIDTH: image box exceeds text width or is below 10 mm')
        if not 15*mm<=maxh<=105*mm:fail('E_IMAGE_HEIGHT: image box must be 15..105 mm high')
    scale=min(maxw/iw,maxh/ih);w,h=iw*scale,ih*scale
    ppi=min(iw/(w/72),ih/(h/72))
    if ppi<299.999:fail(f'E_IMAGE_PPI: {path.name} is {ppi:.1f} ppi; minimum is 300')
    return path,w,h,ppi

def validate_metadata(data,root):
    public=data.get('profile','draft')=='public'
    if data.get('profile','draft') not in ('draft','public'):fail('E_PROFILE: draft or public required')
    sources=data.get('sources',[]);claims=data.get('claims',[])
    if public and (not sources or not claims):fail('E_PUBLIC_METADATA: sources and claims required')
    known={}
    for source in sources:
        sid=plain(source.get('id'),'source.id')
        if sid in known:fail('E_SOURCE_ID: duplicate '+sid)
        for key in ('title','kind','read_status'):plain(source.get(key),'source.'+key)
        parsed=urlparse(plain(source.get('url'),'source.url'))
        if parsed.scheme not in ('http','https') or not parsed.netloc:fail('E_SOURCE_URL: absolute HTTP(S) URL required')
        if source['read_status'] not in ('body_read','partial','body_read_via_index','metadata_only','unavailable'):fail('E_SOURCE_STATUS: unknown read status')
        known[sid]=source
    cids=set()
    for claim in claims:
        cid=plain(claim.get('id'),'claim.id')
        if cid in cids:fail('E_CLAIM_ID: duplicate '+cid)
        cids.add(cid);plain(claim.get('text'),'claim.text')
        kind=claim.get('kind')
        if kind not in ('official_spec','author_report','code_reading','book_experiment','synthetic_example','reverse_engineered_path'):fail('E_CLAIM_KIND: unsupported claim kind')
        ids=claim.get('source_ids',[])
        if not isinstance(ids,list) or any(i not in known for i in ids):fail('E_CLAIM_SOURCE: unknown source reference')
        status=claim.get('verification')
        if public and status not in ('supported','limited','unconfirmed'):fail('E_CLAIM_STATUS: explicit verification required')
        if kind in ('official_spec','author_report','code_reading'):
            if not ids:fail('E_CLAIM_SOURCE: factual claim requires source_ids')
            if not claim.get('locator'):fail('E_CLAIM_LOCATOR: factual claim needs exact source locator')
            if status=='supported' and all(known[i]['read_status'] in ('metadata_only','unavailable') for i in ids):fail('E_CLAIM_SUPPORT: source body was not read')
        if kind=='book_experiment' and public and not claim.get('evidence_path'):fail('E_EXPERIMENT_EVIDENCE: execution evidence path required')
        if claim.get('evidence_path'):safe_asset(root,claim['evidence_path'])
    if public:
        slugs=[]
        for chapter in data.get('chapters',[]):
            slug=plain(chapter.get('competition_slug'),'chapter.competition_slug')
            if not re.fullmatch(r'[a-z0-9][a-z0-9-]*',slug):fail('E_COMPETITION_SLUG: invalid slug')
            slugs.append(slug)
        if len(slugs)!=len(set(slugs)):fail('E_COMPETITION_SLUG: duplicate competition')
        for value in all_strings(data):
            for sid in CITE.findall(value):
                if sid not in known:fail('E_CITATION: unknown source '+sid)
    provenance=data['book'].get('cover_provenance')
    if public and not provenance:fail('E_COVER_PROVENANCE: provenance required for a newly created book cover')
    if provenance:
        if provenance.get('kind') not in ('new_generation','new_original'):fail('E_COVER_PROVENANCE: kind must be new_generation or new_original')
        plain(provenance.get('prompt') or provenance.get('description'),'cover generation prompt/description')
        actual=sha(safe_asset(root,data['book']['cover_image']))
        if provenance.get('sha256')!=actual:fail('E_COVER_HASH: cover bytes disagree with provenance')
    return public

def validate(data, root):
    if not isinstance(data,dict): fail('input must be an object')
    book=data.get('book',{})
    plain(book.get('title'),'book.title')
    if not isinstance(book.get('cover_lines'),list) or len(book.get('cover_lines',[]))!=3: fail('book.cover_lines requires exactly 3 lines')
    for text in book['cover_lines']: plain(text,'cover line')
    plain(book.get('cover_image'),'book.cover_image (a new illustration is required; no bundled default)')
    image_layout({'path':book['cover_image']},root,cover=True)
    body=float(book.get('body_pt',9)); leading=float(book.get('leading_pt',13))
    if not 9<=body<=12 or leading<body*1.25: fail('E_BODY_SIZE: body must be >=9 pt, with adequate leading')
    ch=data.get('chapters')
    if not isinstance(ch,list) or not ch: fail('chapters must be nonempty')
    for i,chapter in enumerate(ch,1):
        plain(chapter.get('title'),f'chapter {i} title')
        sections=chapter.get('sections',[])
        if [section.get('title') for section in sections]!=SECTIONS: fail(f'chapter {i}: four required sections missing/out of order')
        figures=0
        for section in sections:
            if not section.get('blocks'): fail(f'chapter {i}: empty section')
            figures+=sum(b.get('type')=='figure' for b in section['blocks'])
        if figures<2: fail(f'chapter {i}: at least 2 major figures required')
    for name in ('prologue','epilogue','appendix'):
        part=data.get(name)
        if not part or not part.get('blocks'): fail(f'{name} required')
        plain(part.get('title'),name+' title')
    blocks=list(data.get('frontmatter',[]))
    for name in ('prologue','epilogue','appendix'): blocks.extend(data[name]['blocks'])
    for chapter in ch:
        for section in chapter['sections']: blocks.extend(section['blocks'])
    public=validate_metadata(data,root)
    if public and (abs(body-9)>.001 or abs(leading-13)>.001):
        fail('E_PUBLIC_STYLE: this public template requires body 9 pt / leading 13 pt')
    for b in blocks:
        kind=b.get('type')
        if kind in ('p','h2','formula','code'):
            plain(b.get('text'),kind)
            if kind=='code':
                code_kind=b.get('kind')
                if public and code_kind not in ('python','python_fragment','pseudocode','text'):fail('E_CODE_KIND: public code needs an explicit kind')
                if code_kind=='python':
                    try:ast.parse(b['text'])
                    except SyntaxError as exc:fail(f'E_CODE_SYNTAX: Python block: {exc}')
                if 'units' in b and (not isinstance(b['units'],list) or not b['units'] or any(not isinstance(t,str) or not t.strip() for t in b['units'])):fail('E_CODE_UNITS: nonempty string list required')
                if 'units' in b:
                    if code_kind in ('python','python_fragment'):fail('E_CODE_UNITS: Python logical units are inferred; omit explicit units')
                    canonical=lambda text:'\n'.join(line.rstrip() for line in text.strip().splitlines())
                    if canonical('\n'.join(b['units']))!=canonical(b['text']):fail('E_CODE_UNITS: newline-joined units must preserve text')
        elif kind=='table':
            caption(b.get('title')); n=len(b.get('headers',[]))
            if n<1 or not b.get('rows') or any(len(row)!=n for row in b['rows']): fail('E_TABLE_SHAPE: table dimensions invalid')
            if 'widths' in b and (len(b['widths'])!=n or any(not isinstance(w,(int,float)) or not math.isfinite(w) or w<=0 for w in b['widths'])): fail('E_TABLE_WIDTHS: table widths invalid')
        elif kind=='figure':
            caption(b.get('title'))
            height=float(b.get('height_mm',58))
            if not 15<=height<=105: fail('E_FIGURE_HEIGHT: figure height must be 15..105 mm')
            if 'path' in b:image_layout(b,root)
            else:
                nodes=b.get('nodes',[]); ids=[n.get('id') for n in nodes]
                if not nodes or len(set(ids))!=len(ids): fail('E_FIGURE_NODE_ID: node IDs missing/duplicate')
                rects=[]
                for node in nodes:
                    plain(node.get('label'),'node label')
                    x,y,w,h=[float(node[k]) for k in ('x','y','w','h')]
                    if not all(math.isfinite(v) for v in (x,y,w,h)) or min(x,y)<0 or min(w,h)<=0 or x+w>1.00001 or y+h>1.00001: fail('E_FIGURE_BOUNDS: node outside diagram')
                    for ax,ay,aw,ah in rects:
                        if min(x+w,ax+aw)-max(x,ax)>1e-6 and min(y+h,ay+ah)-max(y,ay)>1e-6:fail('E_FIGURE_OVERLAP: diagram boxes overlap')
                    rects.append((x,y,w,h))
                seen=set()
                for edge in b.get('edges',[]):
                    if len(edge)!=2 or any(v not in ids for v in edge): fail('E_FIGURE_EDGE: edge references unknown node')
                    if edge[0]==edge[1] or tuple(edge) in seen:fail('E_FIGURE_EDGE: self or duplicate edge')
                    seen.add(tuple(edge))
        else: fail(f'unsupported block type: {kind!r}')
    return book

from pathlib import Path
import hashlib
from fontTools.ttLib import TTFont
from fontTools import subset
from fontTools.fontBuilder import FontBuilder
from fontTools.pens.ttGlyphPen import TTGlyphPen
from fontTools.pens.cu2quPen import Cu2QuPen


def prepare_font(source_path, target_path, chars, bold=False, font_number=0):
    """Subset an embeddable static TTF/OTF/TTC, converting CFF outlines to TTF.

    ``chars`` must contain every character that can be printed with this font.
    Noto CJK collection index zero is the Japanese face on the tested Linux
    fonts. Supply ``font_number`` explicitly for another collection layout.
    This is an outline-format conversion, not a license grant. Only use a font
    whose terms permit conversion and embedding. ``bold`` labels the selected
    source; it does not synthesize a bold face.
    """
    source_path, target_path = Path(source_path), Path(target_path)
    target_path.parent.mkdir(parents=True, exist_ok=True)
    required = {ord(c) for c in chars if c not in '\r\n\t\f'}
    font = TTFont(str(source_path), fontNumber=font_number,
                  recalcTimestamp=False, lazy=False)
    if 'fvar' in font or 'CFF2' in font:
        raise ValueError('Use a static TTF/OTF/TTC font, not variable/CFF2: ' + str(source_path))
    cmap = font.getBestCmap() or {}
    missing = sorted(required - set(cmap))
    if missing:
        raise ValueError('Missing font glyphs in %s: %s' % (
            source_path, ', '.join('U+%04X %r' % (u, chr(u)) for u in missing[:30])))
    fs_type = int(getattr(font.get('OS/2'), 'fsType', 0))
    if fs_type & (0x0002 | 0x0100 | 0x0200):
        raise ValueError('Font flags forbid this embedding/subset path: ' + str(source_path))
    options = subset.Options()
    options.recalc_timestamp = False
    options.notdef_glyph = True
    options.notdef_outline = True
    options.glyph_names = True
    options.drop_tables += ['GSUB', 'GPOS', 'GDEF', 'BASE', 'JSTF', 'DSIG', 'vhea', 'vmtx', 'VORG', 'FFTM']
    sub = subset.Subsetter(options=options)
    sub.populate(unicodes=required)
    sub.subset(font)
    if 'glyf' in font:
        font['head'].created = font['head'].modified = 2082844800
        font.save(str(target_path))
        font.close()
        return str(target_path)
    if 'CFF ' not in font:
        raise ValueError('Unsupported outline format: ' + str(source_path))
    glyph_order = font.getGlyphOrder()
    glyph_set = font.getGlyphSet()
    glyphs = {}
    upm = font['head'].unitsPerEm
    for name in glyph_order:
        pen = TTGlyphPen(glyph_set)
        glyph_set[name].draw(Cu2QuPen(pen, max_err=max(0.5, upm / 2000), reverse_direction=True))
        glyphs[name] = pen.glyph()
    fb = FontBuilder(upm, isTTF=True)
    fb.setupGlyphOrder(glyph_order)
    fb.setupCharacterMap(font.getBestCmap())
    fb.setupGlyf(glyphs)
    fb.setupHorizontalMetrics({n: font['hmtx'].metrics[n] for n in glyph_order})
    fb.setupHorizontalHeader(ascent=font['hhea'].ascent, descent=font['hhea'].descent,
                             lineGap=font['hhea'].lineGap)
    os2 = font['OS/2']
    fb.setupOS2(sTypoAscender=os2.sTypoAscender, sTypoDescender=os2.sTypoDescender,
                sTypoLineGap=os2.sTypoLineGap, usWinAscent=os2.usWinAscent,
                usWinDescent=os2.usWinDescent, usWeightClass=700 if bold else 400,
                fsType=fs_type)
    digest = hashlib.sha256((source_path.name + str(font_number) + ''.join(map(chr, sorted(required)))).encode()).hexdigest()[:12]
    family = 'BookSubset' + digest
    style = 'Bold' if bold else 'Regular'
    names = {'familyName': family, 'styleName': style,
             'uniqueFontIdentifier': family + '-' + style,
             'fullName': family + ' ' + style,
             'psName': family + '-' + style, 'version': 'Version 1.0'}
    for key, nid in [('copyright', 0), ('trademark', 7), ('manufacturer', 8),
                     ('designer', 9), ('licenseDescription', 13), ('licenseInfoURL', 14)]:
        value = font['name'].getDebugName(nid)
        if value:
            names[key] = value
    fb.setupNameTable(names)
    fb.setupPost()
    fb.setupMaxp()
    fb.font['head'].created = fb.font['head'].modified = 2082844800
    target_path.parent.mkdir(parents=True, exist_ok=True)
    fb.save(str(target_path))
    font.close()
    return str(target_path)



def invariant_canvas(*args,**kwargs):
    kwargs.update(invariant=1,initialFontName='BookSerif')
    return canvas.Canvas(*args,**kwargs)

def rich(value):
    value=html.escape(str(value),quote=False).replace('\n','<br/>')
    return CITE.sub(lambda m:'<super rise="2.4" size="7"><font size="7">['+m.group(1)+']</font></super>',value)

def styles(book):
    bp=float(book.get('body_pt',9)); lp=float(book.get('leading_pt',13))
    common=dict(fontName='BookSerif',fontSize=bp,leading=lp,wordWrap='CJK',textColor=colors.black,
                spaceAfter=4,allowWidows=0,allowOrphans=0,splitLongWords=1)
    s={'p':ParagraphStyle('body',firstLineIndent=bp,**common)}
    s['plain']=ParagraphStyle('plain',**common)
    for name,size,lead in [('chapter',14,19),('section',11,15),('h2',9,13)]:
        s[name]=ParagraphStyle(name,fontName=('BookSansBold' if name=='h2' else 'BookBold'),fontSize=size,leading=lead,wordWrap='CJK',
                              spaceBefore=8,spaceAfter=6,keepWithNext=True)
    s['title']=ParagraphStyle('title',fontName='BookBold',fontSize=17,leading=23,wordWrap='CJK',alignment=TA_CENTER,spaceAfter=12)
    s['cap']=ParagraphStyle('caption',fontName='BookSansBold',fontSize=7,leading=10,wordWrap='CJK',alignment=TA_CENTER,spaceBefore=4,spaceAfter=8)
    s['tcap']=ParagraphStyle('tablecaption',parent=s['cap'],alignment=TA_LEFT,keepWithNext=True)
    s['cell']=ParagraphStyle('cell',fontName='BookSans',fontSize=7.5,leading=10,wordWrap='CJK',splitLongWords=1,allowWidows=0,allowOrphans=0,spaceAfter=0)
    s['headcell']=ParagraphStyle('headcell',parent=s['cell'],fontName='BookSansBold')
    s['code']=ParagraphStyle('code',fontName='BookMono',fontSize=7,leading=9.5,wordWrap='CJK',splitLongWords=1,allowWidows=0,allowOrphans=0,spaceAfter=0)
    s['formula']=ParagraphStyle('formula',fontName='BookSerif',fontSize=9,leading=13,wordWrap='CJK',alignment=TA_CENTER,spaceBefore=5,spaceAfter=7)
    s['toc0']=ParagraphStyle('toc0',fontName='BookSans',fontSize=9,leading=13,wordWrap='CJK',spaceBefore=5,rightIndent=16)
    s['toc1']=ParagraphStyle('toc1',parent=s['toc0'],fontSize=7.5,leading=10,leftIndent=9,spaceBefore=1)
    return s

class ParityStart(Flowable):
    """After a PageBreak, consume a blank even page before an odd chapter."""
    def wrap(self,w,h):
        doc=self._doctemplate
        if doc.page%2==0:
            doc.blank_pages.add(doc.page)
            doc.frame.add_generated_content(PageBreak())
        return 0,0
    def draw(self): pass

class EvenEnd(Flowable):
    def wrap(self,w,h):
        doc=self._doctemplate
        if doc.page%2==1:
            doc.blank_pages.add(doc.page+1)
            doc.frame.add_generated_content(PageBreak(),Spacer(1,0.1))
        return 0,0
    def draw(self): pass

class Diagram(Flowable):
    def __init__(self,b,sty):
        super().__init__(); self.b=b; self.width=WIDTH; self.height=float(b.get('height_mm',58))*mm; self.sty=sty
    def wrap(self,w,h):
        self.check_layout()
        return self.width,self.height
    def check_layout(self):
        W,H=self.width,self.height
        ns=self.b['nodes']
        node_style=ParagraphStyle('nodecheck',parent=self.sty['cell'],alignment=TA_CENTER,fontSize=8,leading=10)
        for node in ns:
            w,h=node['w']*W,node['h']*H
            if w<=9 or h<=7:fail('E_FIGURE_LABEL: node too small for text padding')
            paragraph=Paragraph(rich(node['label']),node_style)
            _,height=paragraph.wrap(w-8,h-6)
            if height>h-6+.01:fail('E_FIGURE_LABEL: text does not fit node: '+node['label'])
        # An edge may enter its source/target, but must not pass through another box.
        lookup={n['id']:n for n in ns}
        for start,end in self.b.get('edges',[]):
            a,b=lookup[start],lookup[end]
            x1,y1=a['x']+a['w']/2,a['y']+a['h']/2
            x2,y2=b['x']+b['w']/2,b['y']+b['h']/2
            for node in ns:
                if node['id'] in (start,end):continue
                if segment_hits_rect(x1,y1,x2,y2,node):fail('E_FIGURE_EDGE_COLLISION: edge crosses node '+node['id'])
    def draw(self):
        c=self.canv; W,H=self.width,self.height
        boxes={n['id']:(n['x']*W,n['y']*H,n['w']*W,n['h']*H,n['label']) for n in self.b['nodes']}
        def boundary(rect,dx,dy):
            x,y,w,h,_=rect; factor=min((w/2)/abs(dx) if dx else 1e20,(h/2)/abs(dy) if dy else 1e20)
            return x+w/2+dx*factor,y+h/2+dy*factor
        c.setLineWidth(0.8);c.setStrokeColor(colors.black);c.setFillColor(colors.black)
        for a,b in self.b.get('edges',[]):
            ra,rb=boxes[a],boxes[b]; dx=rb[0]+rb[2]/2-ra[0]-ra[2]/2;dy=rb[1]+rb[3]/2-ra[1]-ra[3]/2
            if dx==0 and dy==0: fail('overlapping diagram centers')
            x1,y1=boundary(ra,dx,dy);x2,y2=boundary(rb,-dx,-dy)
            c.line(x1,y1,x2,y2); angle=math.atan2(y2-y1,x2-x1)
            c.line(x2,y2,x2-4*math.cos(angle-.45),y2-4*math.sin(angle-.45))
            c.line(x2,y2,x2-4*math.cos(angle+.45),y2-4*math.sin(angle+.45))
        node_style=ParagraphStyle('node',parent=self.sty['cell'],alignment=TA_CENTER,fontSize=8,leading=10)
        for x,y,w,h,label in boxes.values():
            p=Paragraph(rich(label),node_style);pw,ph=p.wrap(w-8,h-6)
            if ph>h-6: fail('diagram text does not fit node: '+label)
            c.setFillColor(colors.white);c.roundRect(x,y,w,h,3,fill=1,stroke=1)
            c.setFillColor(colors.black);p.drawOn(c,x+4,y+(h-ph)/2)

def segment_hits_rect(x1,y1,x2,y2,node):
    low,high=0.,1.;dx,dy=x2-x1,y2-y1
    for p,q in [(-dx,x1-node['x']),(dx,node['x']+node['w']-x1),(-dy,y1-node['y']),(dy,node['y']+node['h']-y1)]:
        if abs(p)<1e-12:
            if q<=0:return False
        else:
            t=q/p
            if p<0:low=max(low,t)
            else:high=min(high,t)
    return low<high and high>0 and low<1

def code_flowables(block,sty):
    language=block.get('language','コード')
    def lines(text):
        result=[]
        for line in text.expandtabs(4).split('\n'):
            escaped=html.escape(line,quote=False).replace(' ','&#160;') or '&#160;'
            result.append(Paragraph(escaped,sty['code']))
        return result
    def height(items):return sum(item.wrap(WIDTH,FRAME_HEIGHT)[1] for item in items)
    label=Paragraph(rich(language),sty['cap']);label.keepWithNext=True
    whole=lines(block['text']);label_height=label.wrap(WIDTH,FRAME_HEIGHT)[1]+label.getSpaceBefore()+label.getSpaceAfter()
    if label_height>FRAME_HEIGHT/3:fail('E_CODE_LABEL_TOO_TALL: shorten language/kind label')
    if height(whole)+label_height+5<=FRAME_HEIGHT:return [KeepTogether([label]+whole+[Spacer(1,5)])]
    units=block.get('units')
    if units:
        # Explicit logical chunks must preserve the supplied source, apart from blank separators.
        canonical=lambda t:'\n'.join(line.rstrip() for line in t.strip().splitlines())
        if canonical('\n'.join(units))!=canonical(block['text']):fail('E_CODE_UNITS: units do not reconstruct text')
    elif block.get('kind')=='python':
        module=ast.parse(block['text']);source=block['text'].splitlines();starts=[]
        for node in module.body:
            begins=[node.lineno]+[d.lineno for d in getattr(node,'decorator_list',[])]
            starts.append(min(begins)-1)
        starts=sorted(set([0]+starts))+[len(source)]
        units=['\n'.join(source[a:b]) for a,b in zip(starts,starts[1:]) if any(line.strip() for line in source[a:b])]
    else:fail('E_CODE_BLOCK_TOO_TALL: split into explicit logical units; a block is never cut mid-procedure')
    result=[label]
    for unit in units:
        chunk=lines(unit)
        if height(chunk)+20>FRAME_HEIGHT:fail('E_CODE_UNIT_TOO_TALL: shorten or explicitly redesign the long function/procedure')
        result.append(KeepTogether(chunk+[Spacer(1,4)]))
    return result

def check_table_rows(rows,widths,title):
    heights=[]
    for index,row in enumerate(rows):
        height=max(cell.wrap(width-6,FRAME_HEIGHT)[1] for cell,width in zip(row,widths))+8
        heights.append(height)
        budget=FRAME_HEIGHT-30-(heights[0] if index else 0)
        if height>budget:fail(f'E_TABLE_ROW_TOO_TALL: {title}, row {index}; split or rewrite this row')
    if len(heights)>1 and heights[0]+heights[1]+30>FRAME_HEIGHT:fail('E_TABLE_HEADER_TOO_TALL: header and first row cannot fit together')
    return heights

def heading(text,style,level,key):
    p=Paragraph(rich(text),style);p.book_toc=(level,text,key);return p

def render_blocks(blocks,sty,root,chapter_no=0,counts=None):
    out=[]
    if counts is None: counts={'fig':0,'table':0}
    for b in blocks:
        kind=b['type']
        if kind in ('p','h2','formula'):
            out.append(Paragraph(rich(b['text']),sty[kind]))
        elif kind=='code':
            out.extend(code_flowables(b,sty))
        elif kind=='table':
            counts['table']+=1; table=counts['table']; label=f'表{chapter_no}.{table}' if chapter_no else f'表{table}'
            cap=Paragraph(rich(label+' '+caption(b['title'])),sty['tcap'])
            rows=[[Paragraph(rich(x),sty['headcell']) for x in b['headers']]]
            rows.extend([[Paragraph(rich(x),sty['cell']) for x in row] for row in b['rows']])
            fractions=b.get('widths',[1]*len(b['headers']));total=sum(fractions)
            widths=[WIDTH*x/total for x in fractions]
            row_heights=check_table_rows(rows,widths,b['title'])
            minimum=cap.wrap(WIDTH,FRAME_HEIGHT)[1]+cap.getSpaceBefore()+cap.getSpaceAfter()+sum(row_heights[:2])
            if minimum>FRAME_HEIGHT:fail('E_TABLE_CAPTION_TOO_TALL: caption, header and first row do not fit together')
            t=LongTable(rows,colWidths=widths,repeatRows=1,hAlign='LEFT',splitByRow=1,splitInRow=0)
            t.setStyle(TableStyle([('FONTNAME',(0,0),(-1,-1),'BookSans'),('VALIGN',(0,0),(-1,-1),'TOP'),('LEFTPADDING',(0,0),(-1,-1),3),
                ('RIGHTPADDING',(0,0),(-1,-1),3),('TOPPADDING',(0,0),(-1,-1),4),('BOTTOMPADDING',(0,0),(-1,-1),4),
                ('LINEABOVE',(0,0),(-1,0),.75,colors.black),('LINEBELOW',(0,0),(-1,0),.75,colors.black),
                ('LINEBELOW',(0,-1),(-1,-1),.75,colors.black)]))
            out.extend([CondPageBreak(minimum),cap,t,Spacer(1,7)])
        elif kind=='figure':
            counts['fig']+=1; fig=counts['fig'];label=f'図{chapter_no}.{fig}' if chapter_no else f'図{fig}'
            if 'path' in b:
                path,iw,ih,_=image_layout(b,root)
                graphic=Image(io.BytesIO(path.read_bytes()),width=iw,height=ih);graphic.hAlign='CENTER'
            else:graphic=Diagram(b,sty)
            cap=Paragraph(rich(label+' '+caption(b['title'])),sty['cap'])
            group_height=graphic.wrap(WIDTH,FRAME_HEIGHT)[1]+cap.wrap(WIDTH,FRAME_HEIGHT)[1]+cap.getSpaceBefore()+cap.getSpaceAfter()
            if group_height>FRAME_HEIGHT:fail('E_FIGURE_CAPTION_TOO_TALL: figure and caption must fit on one page')
            out.append(KeepTogether([graphic,cap]))
    return out

class BookDoc(BaseDocTemplate):
    def __init__(self,path,title,sty):
        super().__init__(str(path),pagesize=PAGE,leftMargin=INNER,rightMargin=OUTER,topMargin=TOP,bottomMargin=BOTTOM,
                         allowSplitting=1,title=title,author='',pageCompression=1)
        self.sty=sty;self.current='';self.current_start=0;self.entries=[];self.blank_pages=set();self.title_text=title
        def frame(name,left): return Frame(left,BOTTOM,WIDTH,PAGE[1]-TOP-BOTTOM,id=name,leftPadding=0,rightPadding=0,topPadding=0,bottomPadding=0)
        self.addPageTemplates([PageTemplate(id='odd',frames=[frame('o',INNER)],onPageEnd=self.page_head),
                               PageTemplate(id='even',frames=[frame('e',OUTER)],onPageEnd=self.page_head)])
    def handle_pageBegin(self):
        self.pageTemplate=self.pageTemplates[self.page%2]
        super().handle_pageBegin()
    def beforeDocument(self): self.current='';self.current_start=0;self.entries=[];self.blank_pages=set()
    def page_head(self,c,doc):
        if doc.page==1 or doc.page in self.blank_pages:return
        c.saveState();c.setFont('BookSerif',7)
        left=INNER if doc.page%2 else OUTER;right=left+WIDTH
        if doc.page%2 and self.current.startswith('第') and doc.page!=self.current_start:
            label=self.current
            while label and pdfmetrics.stringWidth(label,'BookSerif',7)>WIDTH:label=label[:-1]
            if label!=self.current:label=label[:-1]+'…'
            c.drawRightString(right,PAGE[1]-9.5*mm,label)
        c.setFont('BookRoman',7)
        if doc.page%2:c.drawRightString(right,9*mm,str(doc.page))
        else:c.drawString(left,9*mm,str(doc.page))
        c.restoreState()
    def afterFlowable(self,f):
        if hasattr(f,'book_toc'):
            level,text,key=f.book_toc
            if level==0:self.current=text;self.current_start=self.page
            self.canv.bookmarkPage(key);self.canv.addOutlineEntry(text,key,level=level,closed=False)
            self.notify('TOCEntry',(level,text,self.page,key));self.entries.append({'level':level,'title':text,'page':self.page,'key':key})

class TitleLines(Flowable):
    def __init__(self,book):
        super().__init__();self.book=book;self.width=WIDTH;self.height=60*mm
    def wrap(self,w,h):return self.width,self.height
    def draw(self):
        self.canv.setFont('BookRoman',17)
        for i,line in enumerate(self.book['cover_lines']):
            self.canv.drawCentredString(PAGE[0]/2-INNER,self.height-(18+11.75*i)*mm,line)

def make_interior(data,root,out,sty):
    book=data['book'];story=[TitleLines(book)]
    story.append(PageBreak())
    story.append(Paragraph('目次',sty['chapter']))
    toc=TableOfContents(tableStyle=TableStyle([('FONTNAME',(0,0),(-1,-1),'BookSans'),('LEFTPADDING',(0,0),(-1,-1),0),('RIGHTPADDING',(0,0),(-1,-1),0)]));toc.levelStyles=[sty['toc0'],sty['toc1']];story.extend([toc,PageBreak()])
    story.extend(render_blocks(data.get('frontmatter',[]),sty,root));story.append(PageBreak())
    for name in ('prologue',):
        part=data[name];story.append(heading(part['title'],sty['chapter'],0,name));story.extend(render_blocks(part['blocks'],sty,root));story.append(PageBreak())
    for i,ch in enumerate(data['chapters'],1):
        if book.get('odd_chapters',True):story.append(ParityStart())
        title=f'第{i}章 {ch["title"]}';story.append(heading(title,sty['chapter'],0,f'chapter-{i}'))
        counts={'fig':0,'table':0}
        for j,sec in enumerate(ch['sections'],1):
            story.append(heading(f'{j}. {sec["title"]}',sty['section'],1,f'chapter-{i}-section-{j}'))
            story.extend(render_blocks(sec['blocks'],sty,root,i,counts))
        story.append(PageBreak())
    for name in ('epilogue','appendix'):
        part=data[name];story.append(heading(part['title'],sty['chapter'],0,name));story.extend(render_blocks(part['blocks'],sty,root))
        if name!='appendix':story.append(PageBreak())
    story.append(EvenEnd())
    doc=BookDoc(out/'interior.pdf',book['title'],sty)
    doc.multiBuild(story,maxPasses=8,canvasmaker=invariant_canvas)
    return doc.entries,sorted(doc.blank_pages)

def draw_front(c,x,y,book):
    c.saveState();c.translate(x,y)
    c.setFillColor(colors.white);c.rect(0,0,*PAGE,fill=1,stroke=0)
    c.setFillColor(colors.black);c.setFont('BookRoman',17)
    for i,line in enumerate(book['cover_lines']):
        if pdfmetrics.stringWidth(line,'BookRoman',17)>PAGE[0]-12*mm:fail('cover line wider than page; change cover_lines')
        c.drawCentredString(PAGE[0]/2,PAGE[1]-(30+11.75*i)*mm,line)
    image_path=book.get('_cover_image_resolved')
    if not image_path: fail('book.cover_image must point to the provided cover illustration')
    _,iw,ih,_=image_layout({'path':book['cover_image']},Path(book['_asset_root']),cover=True)
    ix=14.9*mm+(78.2*mm-iw)/2;iy=(175-59.6629-97.7158)*mm+(97.7158*mm-ih)/2
    c.drawImage(ImageReader(io.BytesIO(Path(image_path).read_bytes())),ix,iy,width=iw,height=ih,mask='auto')
    if book.get('author'):
        c.setFont('BookSans',9);c.drawCentredString(PAGE[0]/2,9*mm,book['author'])
    c.restoreState()

def covers(book,out,pages):
    c=canvas.Canvas(str(out/'front-cover.pdf'),pagesize=PAGE,invariant=1,pageCompression=1,initialFontName='BookSerif')
    c.setTitle(book['title']);c.setAuthor(book.get('author') or '');draw_front(c,0,0,book);c.showPage();c.save()
    if book.get('wrap_cover',True):
        bleed=3.175*mm;spine=pages*.002252*25.4*mm;size=(2*PAGE[0]+spine+2*bleed,PAGE[1]+2*bleed)
        c=canvas.Canvas(str(out/'wrap-cover.pdf'),pagesize=size,invariant=1,pageCompression=1,initialFontName='BookSerif')
        c.setTitle(book['title']);c.setAuthor(book.get('author') or '')
        draw_front(c,bleed+PAGE[0]+spine,bleed,book);c.showPage();c.save()

def merge_book(out,book):
    w=PdfWriter()
    for name in ('front-cover.pdf','interior.pdf'):w.append(str(out/name))
    w.add_metadata({'/Title':book['title'],'/Author':book.get('author') or '','/Creator':'portable_book.py'})
    with (out/'book.pdf').open('wb') as f:w.write(f)

def main():
    parser=argparse.ArgumentParser();parser.add_argument('--input',required=True,type=Path);parser.add_argument('--output',required=True,type=Path)
    args=parser.parse_args();src=args.input.resolve();root=src.parent;targetout=args.output.resolve();targetout.parent.mkdir(parents=True,exist_ok=True)
    temporary=tempfile.TemporaryDirectory(prefix='.book-build-',dir=targetout.parent);out=Path(temporary.name)
    data=json.loads(src.read_text(encoding='utf-8'));configure_layout(data.get('book',{}));book=validate(data,root)
    text='\n'.join(rendered_strings(data))+''.join(map(chr,range(32,127)))+'\u00a0図表第章目次コード…' 
    chars=set(text)-set('\n\r\t');fontspec=data.get('fonts',{})
    defaults={'serif':'/usr/share/fonts/opentype/noto/NotoSerifCJK-Regular.ttc',
              'sans':'/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc',
              'bold':'/usr/share/fonts/opentype/noto/NotoSerifCJK-Bold.ttc',
              'sans_bold':'/usr/share/fonts/opentype/noto/NotoSansCJK-Bold.ttc',
              'roman':'/usr/share/fonts/truetype/liberation/LiberationSerif-Regular.ttf',
              'mono':'/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc'}
    fontlog={};fontdir=out/'fonts';fontdir.mkdir(exist_ok=True)
    for kind,name in [('serif','BookSerif'),('sans','BookSans'),('bold','BookBold'),('sans_bold','BookSansBold'),('mono','BookMono')]:
        source=Path(fontspec.get(kind,defaults[kind])).expanduser()
        if not source.is_absolute():source=root/source
        if not source.is_file():fail(f'font missing: {source}; supply fonts.{kind}')
        target=fontdir/(kind+'.ttf');prepare_font(source,target,chars,bold=kind in ('bold','sans_bold'),font_number=data.get('font_numbers',{}).get(kind,5 if kind=='mono' and source.name=='NotoSansCJK-Regular.ttc' else 0))
        pdfmetrics.registerFont(RLFont(name,str(target)))
        fontlog[kind]={'source_sha256':sha(source),'embedded_subset_sha256':sha(target)}
    roman=Path(fontspec.get('roman',defaults['roman'])).expanduser()
    if not roman.is_absolute():roman=root/roman
    roman_chars=set(''.join(book['cover_lines'])+'0123456789')
    if not roman.is_file():fail('font missing: supply fonts.roman for a Roman serif TTF')
    prepare_font(roman,fontdir/'roman.ttf',roman_chars)
    pdfmetrics.registerFont(RLFont('BookRoman',str(fontdir/'roman.ttf')))
    fontlog['roman']={'source_sha256':sha(roman),'embedded_subset_sha256':sha(fontdir/'roman.ttf')}
    cover_image=safe_asset(root,book['cover_image'])
    book['_cover_image_resolved']=str(cover_image);book['_asset_root']=str(root)
    rl_config.warnOnMissingFontGlyphs=1
    entries,blanks=make_interior(data,root,out,styles(book));pages=len(PdfReader(out/'interior.pdf').pages)
    if pages>500:fail('E_PAGE_PROFILE: more than 500 pages is outside this validated profile')
    if pages>300 and INNER/mm<16:
        if not book.get('auto_gutter',True):fail('E_GUTTER_PROFILE: 301..500 pages require inner_mm>=16 or auto_gutter=true')
        configure_layout(book,16);validate(data,root)
        entries,blanks=make_interior(data,root,out,styles(book));pages=len(PdfReader(out/'interior.pdf').pages)
        if pages>500:fail('E_PAGE_PROFILE: gutter correction produced more than 500 pages')
    if pages%2:fail('internal error: interior page count is odd')
    covers(book,out,pages);merge_book(out,book)
    names=['interior.pdf','front-cover.pdf','book.pdf']+(['wrap-cover.pdf'] if book.get('wrap_cover',True) else [])
    outputs={name:{'sha256':sha(out/name),'bytes':(out/name).stat().st_size,'pages':len(PdfReader(out/name).pages)} for name in names}
    manifest={'renderer':'portable_book.py','renderer_version':'3.1','renderer_sha256':sha(Path(__file__)),
      'build_id':uuid.uuid4().hex, 'profile':data.get('profile','draft'), 'blank_pages':blanks,
      'layout':{'inner_mm':INNER/mm,'outer_mm':OUTER/mm,'top_mm':TOP/mm,'bottom_mm':BOTTOM/mm,'body_width_mm':WIDTH/mm},
      'cover_image_sha256':sha(cover_image),'cover_image_placement':'aspect-preserving contain in 78.2 x 97.7158 mm lower art zone',
      'metadata_validation':'integrity only; no independent fact verification','input_sha256':sha(src),'body_pt':book.get('body_pt',9),'leading_pt':book.get('leading_pt',13),
      'trim_mm':[108,175],'interior_pages':pages,'spine_mm_estimate':pages*.002252*25.4,
      'kdp_status':'NOT_CERTIFIED: compare current KDP template and previewer before printing',
      'fonts':fontlog,'dependencies':{p:importlib.metadata.version(p) for p in ['reportlab','fonttools','pypdf','pillow']},
      'toc':entries,'outputs':outputs}
    (out/'manifest.json').write_text(json.dumps(manifest,ensure_ascii=False,indent=2)+'\n',encoding='utf-8')
    targetout.mkdir(parents=True,exist_ok=True)
    (targetout/'fonts').mkdir(exist_ok=True)
    for fontfile in sorted((out/'fonts').glob('*.ttf')):os.replace(fontfile,targetout/'fonts'/fontfile.name)
    for name in names:os.replace(out/name,targetout/name)
    if not book.get('wrap_cover',True) and (targetout/'wrap-cover.pdf').exists():(targetout/'wrap-cover.pdf').unlink()
    os.replace(out/'manifest.json',targetout/'manifest.json')
    temporary.cleanup()
    print(json.dumps({'interior_pages':pages,'outputs':outputs},ensure_ascii=False))

if __name__=='__main__':
    try:main()
    except Exception as exc:
        print(f'BUILD FAILED: {type(exc).__name__}: {exc}',file=sys.stderr);raise SystemExit(1)
```

### verify_reproduction.py

<!-- asset:verify_reproduction.py;encoding:text -->
```python
#!/usr/bin/env python3
"""QA and recorded release gate for portable_book.py 3.1.

Public input defaults to the complete release gate. Use --layout-only for
intermediate technical checks. Draft/omitted profile can never be publicly ready.
A release requires --compare, --content-review and --review-decisions files.
Content/visual records must come from real independent reviews; this program
checks their completeness and binding, not the truth of every competition fact.
The full source p/formula sequence is mapped to actual visible serif glyphs;
normal body9 and source-defined citations7 are checked character by character.
"""
import argparse
from collections import Counter
import hashlib
import json
import math
import re
import itertools
import collections
import io
from pathlib import Path

import fitz
from pypdf import PdfReader
from fontTools.ttLib import TTFont
from PIL import Image

MM = 72 / 25.4


def rect_intersection(a, b):
    x0, y0, x1, y1 = max(a[0], b[0]), max(a[1], b[1]), min(a[2], b[2]), min(a[3], b[3])
    return (x0, y0, x1, y1) if x1 > x0 and y1 > y0 else None


def rect_area(rect):
    return max(0, rect[2] - rect[0]) * max(0, rect[3] - rect[1])


def merged_length(intervals):
    total = 0; end = -1e20
    for start, stop in sorted(intervals):
        total += max(0, stop - max(start, end)); end = max(end, stop)
    return total


def segment_enters_rectangle(a, b, box):
    """Liang-Barsky clipping, with a small inset to ignore boundary tangencies."""
    x0, y0, x1, y1 = box
    inset = min(x1 - x0, y1 - y0) * .04
    x0 += inset; y0 += inset; x1 -= inset; y1 -= inset
    dx, dy = b[0] - a[0], b[1] - a[1]
    lo, hi = 0.0, 1.0
    for p, q in ((-dx, a[0] - x0), (dx, x1 - a[0]), (-dy, a[1] - y0), (dy, y1 - a[1])):
        if abs(p) < 1e-12:
            if q < 0: return False
        else:
            t = q / p
            if p < 0: lo = max(lo, t)
            else: hi = min(hi, t)
            if lo > hi: return False
    return hi > lo


def geometry_audit(data, doc, manifest, review_decisions=None):
    """Independent all-page PDF geometry checks. Flags require human review.

    Text traces are tested as actual occupied glyph rectangles, avoiding the
    full font ascender box and allowing small kerning/superscript contacts.
    Diagram edge/node checks use the authored coordinates independently of
    the renderer. This cannot judge semantic clarity or illustration quality.
    """
    layout = manifest.get('layout', {})
    inner = float(layout.get('inner_mm', 13)); outer = float(layout.get('outer_mm', 10))
    top = float(layout.get('top_mm', 12)); bottom = float(layout.get('bottom_mm', 15))
    body_width = float(layout.get('body_width_mm', 108 - inner - outer))
    chapter_starts = {entry['page'] for entry in manifest['toc'] if entry['key'].startswith('chapter-') and entry['level'] == 0}
    section_starts = {entry['page'] for entry in manifest['toc']}
    prologue_start = next(entry['page'] for entry in manifest['toc'] if entry['key'] == 'prologue')
    epilogue_start = next(entry['page'] for entry in manifest['toc'] if entry['key'] == 'epilogue')
    allowed_blank = set(manifest.get('blank_pages', []))
    allowed_blank |= {page - 1 for page in chapter_starts if page > 1 and (page - 1) % 2 == 0}
    if len(doc) % 2 == 0: allowed_blank.add(len(doc))
    results = {'outside_page': [], 'glyph_overlap': [], 'text_occluded': [], 'white_text': [],
               'thin_strokes': [], 'unintended_blank': [], 'orphan_headings': [], 'diagram_geometry': [],
               'missing_figure_shapes': [], 'graphics_outside_page': []}
    pages = []; flags = []
    known_headings = {normalize(entry['title']) for entry in manifest['toc']}
    known_headings |= {normalize(block['text']) for block in blocks(data) if block['type'] == 'h2'}
    for page in doc:
        pn = page.number + 1; w, h = page.rect.width, page.rect.height
        body = (inner * MM if pn % 2 else outer * MM, top * MM,
                (inner * MM if pn % 2 else outer * MM) + body_width * MM, h - bottom * MM)
        traces = page.get_texttrace(); glyphs = []; occupied = []; seq_bounds = []
        for span in traces:
            char_boxes = [char[3] for char in span.get('chars', []) if chr(char[0]).strip()]
            text = ''.join(chr(char[0]) for char in span.get('chars', []))
            if not char_boxes: continue
            bbox = span['bbox']; seq_bounds.append((span.get('seqno', -1), bbox, text))
            opacity = span.get('opacity', 1.0)
            color = span.get('color', (0,))
            if opacity < .05 or (isinstance(color, (tuple, list)) and min(color) > .98):
                results['white_text'].append({'page': pn, 'text': text[:70], 'opacity': opacity})
            for char in span.get('chars', []):
                if not chr(char[0]).strip(): continue
                box = char[3]
                if box[0] < -.2 or box[1] < -.2 or box[2] > w + .2 or box[3] > h + .2:
                    results['outside_page'].append({'page': pn, 'char': chr(char[0]), 'bbox': box})
                if rect_intersection(box, body):
                    glyphs.append((box, char[0], span.get('seqno', -1)))
                    occupied.append(box)
        # Sweep nearby glyphs only. Kerning contacts narrower than .7 pt are
        # ignored; a real overprinted layer has a large area intersection.
        active = []
        for box, char, seq in sorted(glyphs, key=lambda item: item[0][0]):
            active = [item for item in active if item[0][2] > box[0] + .7]
            for other, other_char, other_seq in active:
                intersection = rect_intersection(box, other)
                if not intersection: continue
                iw, ih = intersection[2] - intersection[0], intersection[3] - intersection[1]
                min_area = min(rect_area(box), rect_area(other))
                if iw > .7 and ih > 1.4 and min_area > 0 and rect_area(intersection) / min_area > .28:
                    results['glyph_overlap'].append({'page': pn, 'chars': chr(other_char) + chr(char),
                                                     'area_fraction': round(rect_area(intersection) / min_area, 3),
                                                     'bbox': intersection})
                    if len(results['glyph_overlap']) > 100: break
            active.append((box, char, seq))
        drawings = page.get_drawings()
        for drawing in drawings:
            bounds = tuple(drawing['rect'])
            if bounds[0] < -.4 or bounds[1] < -.4 or bounds[2] > w + .4 or bounds[3] > h + .4:
                results['graphics_outside_page'].append({'page': pn, 'kind': 'vector', 'bbox': bounds})
            if rect_intersection(bounds, body) and rect_area(bounds) > 20:
                occupied.append(bounds)
            if drawing.get('type') in ('s', 'fs') and 0 < drawing.get('width', 1) < .74:
                results['thin_strokes'].append({'page': pn, 'width': drawing['width'], 'bbox': bounds})
            fill = drawing.get('fill')
            if fill and min(fill) > .98 and drawing.get('fill_opacity', 1) > .98:
                for seq, text_box, text in seq_bounds:
                    intersection = rect_intersection(bounds, text_box)
                    if drawing.get('seqno', -1) > seq and intersection and rect_area(text_box) > 0 and rect_area(intersection) / rect_area(text_box) > .9:
                        results['text_occluded'].append({'page': pn, 'text': text[:70], 'bbox': text_box})
        for image in page.get_image_info():
            bounds = tuple(image['bbox'])
            if bounds[0] < -.4 or bounds[1] < -.4 or bounds[2] > w + .4 or bounds[3] > h + .4:
                results['graphics_outside_page'].append({'page': pn, 'kind': 'image', 'bbox': bounds})
            if rect_intersection(bounds, body): occupied.append(bounds)
        body_text = page.get_text(clip=fitz.Rect(body)).strip()
        is_blank = not body_text and not drawings and not page.get_image_info()
        if is_blank and pn != 1 and pn not in allowed_blank:
            results['unintended_blank'].append(pn)
        bands = [(max(body[1], box[1]), min(body[3], box[3])) for box in occupied
                 if min(body[3], box[3]) > max(body[1], box[1])]
        occupancy = merged_length(bands) / max(1, body[3] - body[1])
        # Chapter-ending pages and intentional blanks naturally have space;
        # other sparse pages are review flags, never silently labelled wrong.
        terminal = pn == len(doc) or pn + 1 in section_starts or pn + 2 in chapter_starts
        technical_page = min(chapter_starts) <= pn < epilogue_start
        if technical_page and not is_blank and occupancy < .30 and not terminal:
            flags.append({'id': f'whitespace-p{pn}', 'page': pn, 'kind': 'large_whitespace',
                          'occupied_vertical_fraction': round(occupancy, 3)})
        body_lines = [(line, spans, text) for line, spans, text in page_lines(page)
                      if line['bbox'][1] >= body[1] - .5 and line['bbox'][1] < body[3]]
        for index, (line, spans, text) in enumerate(body_lines):
            normalized = normalize(text)
            if pn < prologue_start and normalized in {normalize(entry['title']) for entry in manifest['toc']}:
                continue  # This is a TOC label, not the actual section heading.
            is_heading = normalized in known_headings or (len(normalized) >= 5 and any(
                heading.endswith(normalized) for heading in known_headings) and any('Bold' in span['font'] for span in spans))
            if not is_heading: continue
            following = [other for other, _, other_text in body_lines[index + 1:]
                         if other['bbox'][1] >= line['bbox'][3] - .5 and other_text.strip()]
            if not following:
                results['orphan_headings'].append({'page': pn, 'heading': text})
        pages.append({'page': pn, 'blank': is_blank, 'occupied_vertical_fraction': round(occupancy, 3),
                      'glyph_count': len(glyphs), 'image_count': len(page.get_image_info())})
    for chapter_index, chapter in enumerate(data['chapters'], 1):
        figures = [block for section in chapter['sections'] for block in section['blocks'] if block['type'] == 'figure']
        for figure_index, figure in enumerate(figures, 1):
            if 'nodes' not in figure: continue
            nodes = figure['nodes']; by_id = {node['id']: node for node in nodes}
            caption = f'図{chapter_index}.{figure_index}'
            caption_pages = [page for page in doc if normalize(caption + ' ' + figure['title'].rstrip('。．. ')) in normalize(page.get_text())]
            if len(caption_pages) == 1:
                available = [tuple(drawing['rect']) for drawing in caption_pages[0].get_drawings()
                             if drawing.get('type') in ('s', 'fs')]
                used = set()
                for node in nodes:
                    ew = node['w'] * body_width * MM
                    eh = node['h'] * float(figure.get('height_mm', 58)) * MM
                    match = next((index for index, rect in enumerate(available) if index not in used
                                  and abs(rect[2] - rect[0] - ew) < 1.1 and abs(rect[3] - rect[1] - eh) < 1.1), None)
                    if match is None:
                        results['missing_figure_shapes'].append({'chapter': chapter_index, 'figure': figure_index,
                                                                  'page': caption_pages[0].number + 1, 'node': node['id']})
                    else: used.add(match)
            for a, b in itertools.combinations(nodes, 2):
                ra = (a['x'], a['y'], a['x'] + a['w'], a['y'] + a['h'])
                rb = (b['x'], b['y'], b['x'] + b['w'], b['y'] + b['h'])
                overlap = rect_intersection(ra, rb)
                if overlap and rect_area(overlap) > .00001:
                    results['diagram_geometry'].append({'chapter': chapter_index, 'figure': figure_index, 'overlapping_nodes': [a['id'], b['id']]})
            for start, end in figure.get('edges', []):
                a, b = by_id[start], by_id[end]
                ca, cb = (a['x'] + a['w'] / 2, a['y'] + a['h'] / 2), (b['x'] + b['w'] / 2, b['y'] + b['h'] / 2)
                for node in nodes:
                    if node['id'] in (start, end): continue
                    rect = (node['x'], node['y'], node['x'] + node['w'], node['y'] + node['h'])
                    if segment_enters_rectangle(ca, cb, rect):
                        results['diagram_geometry'].append({'chapter': chapter_index, 'figure': figure_index, 'edge_through_node': [start, end, node['id']]})
    decisions = review_decisions or {}
    visual_record = decisions.get('full_size_visual_review', {})
    record_matches_pdf = visual_record.get('pdf_sha256') == manifest.get('outputs', {}).get('interior.pdf', {}).get('sha256')
    accepted = decisions.get('accepted_flags', {}) if record_matches_pdf else {}
    unresolved = [flag for flag in flags if not isinstance(accepted.get(flag['id']), str) or not accepted[flag['id']].strip()]
    reviewed_pages = set(visual_record.get('pages', []))
    checks = [{'name': 'layout_' + name, 'passed': not values, 'detail': values[:100]} for name, values in results.items()]
    return {'checks': checks, 'pages': pages, 'review_flags': flags, 'unresolved_review_flags': unresolved,
            'full_size_visual_review_complete': record_matches_pdf and reviewed_pages == set(range(1, len(doc) + 1)) and bool(visual_record.get('method')),
            'limits': ['No automated geometry check proves semantic clarity, typography quality, or winner facts.',
                       'Whitespace flags are decisions for an actual full-size page review, with recorded reasons.']}


def code_indentation_audit(data, doc, output, layout):
    """Check preserved display indentation independently of whitespace-free text."""
    path = Path(output) / 'fonts' / 'mono.ttf'
    if not path.exists():
        return {'name': 'code_indentation_preserved', 'passed': False, 'detail': 'Embedded mono.ttf not found'}
    with TTFont(path) as font:
        family = font['name'].getDebugName(6).split('-')[0]
        space = font['hmtx'].metrics[font.getBestCmap()[32]][0] / font['head'].unitsPerEm * 7
    inner, outer = float(layout.get('inner_mm', 13)), float(layout.get('outer_mm', 10))
    observed = []
    for page in doc:
        for block in page.get_text('rawdict')['blocks']:
            for line in block.get('lines', []):
                chars = [char for span in line['spans'] if family == span['font'].split('-')[0]
                         for char in span.get('chars', [])]
                if not chars: continue
                text = ''.join(char['c'] for char in chars)
                ink = next((char for char in chars if char['c'].strip()), None)
                if ink:
                    observed.append({'page': page.number + 1, 'text': normalize(text), 'x': ink['bbox'][0]})
    failures = []; evidence = []
    for block in blocks(data):
        if block['type'] != 'code': continue
        for original in block['text'].expandtabs(4).splitlines():
            indentation = len(original) - len(original.lstrip(' '))
            content = normalize(original)
            if indentation == 0 or len(content) < 6: continue
            candidates = [line for line in observed if line['text'] == content or (
                len(line['text']) >= 14 and content.startswith(line['text']))]
            if not candidates:
                failures.append({'line': original[:90], 'reason': 'position not found'})
                continue
            matching = []
            for candidate in candidates:
                left = (inner if candidate['page'] % 2 else outer) * MM
                deviation = candidate['x'] - left - indentation * space
                item = {'page': candidate['page'], 'line': original[:80], 'indent_spaces': indentation,
                        'deviation_pt': round(deviation, 3)}
                if abs(deviation) <= .65: matching.append(item)
            if matching:
                evidence.extend(matching)
            else:
                failures.append({'line': original[:90], 'reason': 'no matching line has the source indentation',
                                 'observed': [{'page': item['page'], 'x': item['x']} for item in candidates]})
    return {'name': 'code_indentation_preserved', 'passed': not failures,
            'detail': {'failures': failures[:30], 'checked_lines': len(evidence), 'sample': evidence[:12]}}


def normalize(value):
    value = re.sub(r'\[\[([A-Za-z0-9_.:-]+)\]\]', r'[\1]', str(value))
    return re.sub(r'\s+', '', value)


def blocks(data):
    yield from data.get('frontmatter', [])
    yield from data['prologue']['blocks']
    for chapter in data['chapters']:
        for section in chapter['sections']:
            yield from section['blocks']
    for name in ('epilogue', 'appendix'):
        yield from data[name]['blocks']


def expected_text(data):
    for block in blocks(data):
        kind = block['type']
        if kind in ('p', 'h2', 'formula'):
            yield kind, block['text']
        elif kind == 'code':
            for line in block['text'].splitlines():
                if line.strip():
                    yield 'code', line
        elif kind == 'table':
            yield 'caption', block['title'].rstrip('。．. ')
            for cell in block['headers']:
                yield 'table', cell
            for row in block['rows']:
                for cell in row:
                    yield 'table', cell
        elif kind == 'figure':
            yield 'caption', block['title'].rstrip('。．. ')
            for node in block.get('nodes', []):
                yield 'figure', node['label']


def sha(path):
    return hashlib.sha256(Path(path).read_bytes()).hexdigest()


def pixel_fingerprint(value):
    with Image.open(io.BytesIO(value) if isinstance(value, bytes) else value) as image:
        rgb = image.convert('RGB')
        return {'size': rgb.size, 'sha256': hashlib.sha256(rgb.tobytes()).hexdigest()}


def page_lines(page):
    for block in page.get_text('dict')['blocks']:
        for line in block.get('lines', []):
            spans = line.get('spans', [])
            yield line, spans, ''.join(span['text'] for span in spans)


def embedded_fonts(pdf):
    found = {}
    for page in PdfReader(pdf).pages:
        for _, reference in page['/Resources'].get('/Font', {}).items():
            font = reference.get_object()
            name = str(font.get('/BaseFont', ''))
            children = font.get('/DescendantFonts')
            effective = children[0].get_object() if children else font
            descriptor = effective.get('/FontDescriptor')
            descriptor = descriptor.get_object() if descriptor else {}
            embedded = any(key in descriptor for key in ('/FontFile', '/FontFile2', '/FontFile3'))
            found[name] = embedded
    return found



def manuscript_blocks(data):
    """JSON pointer and block, in the exact reading order of this template."""
    for index, block in enumerate(data.get('frontmatter', [])):
        yield f'frontmatter/{index}', block
    for name in ('prologue',):
        for index, block in enumerate(data[name]['blocks']):
            yield f'{name}/blocks/{index}', block
    for ci, chapter in enumerate(data['chapters']):
        for si, section in enumerate(chapter['sections']):
            for bi, block in enumerate(section['blocks']):
                yield f'chapters/{ci}/sections/{si}/blocks/{bi}', block
    for name in ('epilogue', 'appendix'):
        for index, block in enumerate(data[name]['blocks']):
            yield f'{name}/blocks/{index}', block


def manuscript_digest(data):
    value = {key: data[key] for key in ('frontmatter', 'prologue', 'chapters', 'epilogue', 'appendix')}
    return hashlib.sha256(json.dumps(value, ensure_ascii=False, sort_keys=True,
                                    separators=(',', ':')).encode('utf-8')).hexdigest()


def sources_claims_digest(data):
    value = {key: data.get(key, []) for key in ('sources', 'claims')}
    return hashlib.sha256(json.dumps(value, ensure_ascii=False, sort_keys=True,
                                    separators=(',', ':')).encode('utf-8')).hexdigest()


def complete_body_font_audit(data, doc, output, manifest):
    """Match every visible p/formula character to source BEFORE testing its size.

    In this template only p/formula use the regular serif face in the body area.
    Titles, tables, code, TOC, diagrams and folios have separate faces; running
    heads are outside that area. Ambiguous faces, missing characters or a changed
    text order fail closed. A 7pt character is allowed only at a citation position
    explicitly present in the source; it is never inferred to be a citation from
    its size. Spaces/line breaks are not visible glyphs and are excluded.
    """
    def failed(message):
        return [{'name': 'body_source_mapping_complete', 'passed': False, 'detail': message},
                {'name': 'body_font_size', 'passed': False, 'detail': 'source mapping incomplete'},
                {'name': 'citation_font_size_complete', 'passed': False, 'detail': 'source mapping incomplete'}]

    expected = []; block_count = 0
    cite = re.compile(r'\[\[([A-Za-z0-9_.:-]+)\]\]')
    body_pt = float(data['book'].get('body_pt', 9))
    for pointer, block in manuscript_blocks(data):
        if block['type'] not in ('p', 'formula'): continue
        block_count += 1; text = block['text']; cursor = 0
        def add(value, role, size):
            for char in value:
                if not char.isspace(): expected.append((char, role, size, pointer))
        for match in cite.finditer(text):
            add(text[cursor:match.start()], 'body', body_pt if block['type'] == 'p' else 9)
            add('[' + match.group(1) + ']', 'citation', 7)
            cursor = match.end()
        add(text[cursor:], 'body', body_pt if block['type'] == 'p' else 9)
    if not expected: return failed('No visible source p/formula text to audit')
    faces = {}
    try:
        for role in ('serif', 'bold', 'sans', 'sans_bold', 'mono', 'roman'):
            path = Path(output) / 'fonts' / (role + '.ttf')
            if sha(path) != manifest['fonts'][role]['embedded_subset_sha256']:
                return failed('Font audit file differs from manifest: ' + role)
            with TTFont(path) as font:
                faces[role] = font['name'].getDebugName(6)
    except (OSError, KeyError, TypeError, ValueError) as exc:
        return failed('Cannot resolve source font roles: ' + str(exc))
    observed = []; ambiguous = []
    top = float(manifest['layout'].get('top_mm', 12)) * MM
    bottom = (175 - float(manifest['layout'].get('bottom_mm', 15))) * MM
    for page in doc:
        for span in sorted(page.get_texttrace(), key=lambda item: item.get('seqno', 0)):
            face = re.sub(r'^[A-Z]{6}\+', '', span['font'])
            # MuPDF may truncate a long PostScript name. Do not remove '-Bold'
            # or '-Regular': those distinguish native TTF faces of one family.
            matches = [role for role, name in faces.items()
                       if face == name or name.startswith(face) or face.startswith(name)]
            if 'serif' not in matches: continue
            for codepoint, _, origin, bbox in span['chars']:
                char = chr(codepoint)
                if char.isspace() or not top - .2 <= origin[1] <= bottom + .2: continue
                if len(matches) != 1:
                    ambiguous.append({'page': page.number + 1, 'font': face, 'roles': matches})
                    continue
                observed.append((char, float(span['size']), page.number + 1, tuple(bbox)))
    if ambiguous: return failed({'ambiguous_font_roles': ambiguous[:10]})
    source = ''.join(item[0] for item in expected)
    actual = ''.join(item[0] for item in observed)
    if source != actual:
        index = next((i for i, (a, b) in enumerate(zip(source, actual)) if a != b),
                     min(len(source), len(actual)))
        return failed({'expected_visible_characters': len(source), 'mapped_characters': len(actual),
                       'first_difference': index,
                       'source_block': expected[index][3] if index < len(expected) else None,
                       'page': observed[index][2] if index < len(observed) else None,
                       'expected_excerpt': source[max(0, index - 15):index + 35],
                       'observed_excerpt': actual[max(0, index - 15):index + 35]})
    groups = {'body': {}, 'citation': {}}; counts = Counter()
    for (char, role, target, pointer), (_, size, page, bbox) in zip(expected, observed):
        counts[role] += 1
        if abs(size - target) <= .02: continue
        key = (page, pointer, target, round(size, 3))
        group = groups[role].setdefault(key, {'page': page, 'source_block': pointer,
                                            'expected_pt': target, 'actual_pt': round(size, 3),
                                            'characters': 0, 'sample': ''})
        group['characters'] += 1
        if len(group['sample']) < 45: group['sample'] += char
    return [
        {'name': 'body_source_mapping_complete', 'passed': True,
         'detail': {'source_blocks': block_count, 'visible_characters': len(source),
                    'mapped_characters': len(actual), 'method': 'complete source-order glyph mapping'}},
        {'name': 'body_font_size', 'passed': not groups['body'] and counts['body'] > 0,
         'detail': {'checked_characters': counts['body'], 'mismatched_groups': len(groups['body']),
                    'failures': list(groups['body'].values())[:100]}},
        {'name': 'citation_font_size_complete', 'passed': not groups['citation'],
         'detail': {'checked_characters': counts['citation'], 'expected_pt': 7,
                    'mismatched_groups': len(groups['citation']),
                    'failures': list(groups['citation'].values())[:100]}}]


CONTENT_REVIEW_CHECKS = (
    'competition_identity', 'task_metric_constraints', 'winner_solution_sources',
    'examples_and_math', 'figures_and_text', 'code_execution_scope',
    'reconstructed_path_labeling', 'chapter_structure_and_endmatter')


def publication_audit(data, input_path, output, manifest, compare, content_review_path,
                      geometry, technical_passed):
    """Release gate: recorded independent audits, not automatic fact verification."""
    root = Path(input_path).resolve().parent; output = Path(output).resolve()
    checks = []
    def record(name, passed, detail=None):
        checks.append({'name': name, 'passed': bool(passed), 'detail': detail})
    def checked_file(value):
        path = (root / value).resolve()
        if not path.is_relative_to(root) or not path.is_file():
            raise ValueError('missing or out-of-root evidence/asset: ' + str(value))
        return path

    record('release_public_profile', data.get('profile') == 'public' and manifest.get('profile') == 'public',
           {'input': data.get('profile'), 'manifest': manifest.get('profile')})
    errors = []
    try:
        sources = data.get('sources', []); claims = data.get('claims', [])
        if not isinstance(sources, list) or not sources or not isinstance(claims, list) or not claims:
            raise ValueError('nonempty sources and claims are required')
        known = {}
        for source in sources:
            sid = source['id']
            if not isinstance(sid, str) or not sid or sid in known: raise ValueError('missing/duplicate source id')
            if not all(isinstance(source.get(k), str) and source[k].strip() for k in ('title', 'kind', 'url', 'read_status')):
                raise ValueError('incomplete source fields: ' + sid)
            if not re.fullmatch(r'https?://[^\s/]+(?:/[^\s]*)?', source['url']): raise ValueError('invalid source URL: ' + sid)
            if source['read_status'] not in ('body_read', 'partial', 'body_read_via_index', 'metadata_only', 'unavailable'):
                raise ValueError('unknown source read status: ' + sid)
            known[sid] = source
        ids = set()
        for claim in claims:
            cid = claim['id']; kind = claim['kind']; status = claim.get('verification')
            if not isinstance(cid, str) or not cid or cid in ids: raise ValueError('missing/duplicate claim id')
            ids.add(cid)
            if not isinstance(claim.get('text'), str) or not claim['text'].strip(): raise ValueError('empty claim: ' + cid)
            if kind not in ('official_spec', 'author_report', 'code_reading', 'book_experiment', 'synthetic_example', 'reverse_engineered_path'):
                raise ValueError('unknown claim kind: ' + cid)
            refs = claim.get('source_ids', [])
            if not isinstance(refs, list) or any(sid not in known for sid in refs): raise ValueError('unknown claim source: ' + cid)
            if status not in ('supported', 'limited', 'unconfirmed'): raise ValueError('unknown verification: ' + cid)
            if kind in ('official_spec', 'author_report', 'code_reading'):
                if not refs or not claim.get('locator'): raise ValueError('missing factual source/locator: ' + cid)
                essential = claim.get('essential', True)
                if essential and status != 'supported': raise ValueError('essential factual claim unresolved: ' + cid)
                if status != 'supported' and not claim.get('limitation'):
                    raise ValueError('nonessential limited claim requires a limitation: ' + cid)
                if status == 'supported' and all(known[sid]['read_status'] in ('metadata_only', 'unavailable') for sid in refs):
                    raise ValueError('factual source body unread: ' + cid)
            if kind == 'book_experiment':
                if status != 'supported': raise ValueError('execution evidence unresolved: ' + cid)
                checked_file(claim['evidence_path'])
        for block in blocks(data):
            for sid in re.findall(r'\[\[([A-Za-z0-9_.:-]+)\]\]', json.dumps(block, ensure_ascii=False)):
                if sid not in known: raise ValueError('unknown inline citation: ' + sid)
        slugs = [chapter['competition_slug'] for chapter in data['chapters']]
        if len(slugs) != len(set(slugs)) or any(not isinstance(slug, str) or not re.fullmatch('[a-z0-9][a-z0-9-]*', slug) for slug in slugs):
            raise ValueError('missing/duplicate competition identifiers')
        required = ['タスク', '基本解法', '1位解法', '自力で1位解法に辿り着くには']
        for chapter in data['chapters']:
            if [s['title'] for s in chapter['sections']] != required: raise ValueError('four section contract not met')
            if sum(b['type'] == 'figure' for s in chapter['sections'] for b in s['blocks']) < 2:
                raise ValueError('two major figures required')
    except (OSError, KeyError, TypeError, ValueError) as exc:
        errors.append(str(exc))
    record('release_metadata_complete', not errors, errors)
    errors = []
    try:
        provenance = data['book']['cover_provenance']
        if provenance.get('kind') not in ('new_generation', 'new_original') or not (provenance.get('prompt') or provenance.get('description')):
            raise ValueError('cover generation/original creation record required')
        if provenance.get('sha256') != sha(checked_file(data['book']['cover_image'])):
            raise ValueError('cover record does not match adopted image')
    except (OSError, KeyError, TypeError, ValueError) as exc: errors.append(str(exc))
    record('release_cover_provenance', not errors, errors)
    record('release_template_9_13', abs(float(data['book'].get('body_pt', 9)) - 9) < .001 and
           abs(float(data['book'].get('leading_pt', 13)) - 13) < .001)
    errors = []
    try:
        if content_review_path is None: raise ValueError('content-review.json is required')
        review = json.loads(Path(content_review_path).read_text(encoding='utf-8'))
        if review.get('schema_version') != '1.0' or review.get('status') != 'pass': raise ValueError('content audit must pass schema 1.0')
        if review.get('input_sha256') != sha(input_path): raise ValueError('content audit is for another input')
        if review.get('manuscript_sha256') != manuscript_digest(data): raise ValueError('content audit manuscript mismatch')
        if review.get('sources_claims_sha256') != sources_claims_digest(data): raise ValueError('content audit source/claim mismatch')
        for key in ('reviewer', 'method'):
            if not isinstance(review.get(key), str) or not review[key].strip(): raise ValueError('content audit missing ' + key)
        if review.get('blocking_issues') != [] or review.get('unresolved_essential_claim_ids') != []:
            raise ValueError('content audit has missing or unresolved blocker fields')
        for key in CONTENT_REVIEW_CHECKS:
            item = review.get('checks', {}).get(key, {})
            if item.get('status') != 'pass' or not isinstance(item.get('note'), str) or not item['note'].strip():
                raise ValueError('content audit incomplete: ' + key)
    except (OSError, KeyError, TypeError, ValueError) as exc: errors.append(str(exc))
    record('release_content_review_bound', not errors, errors)
    record('release_full_size_visual_review', geometry['full_size_visual_review_complete'])
    record('release_review_flags_resolved', not geometry['unresolved_review_flags'], geometry['unresolved_review_flags'])
    errors = []
    try:
        if compare is None: raise ValueError('a separately generated comparison directory is required')
        other = Path(compare).resolve()
        if other == output: raise ValueError('comparison output must be a different directory')
        other_manifest = json.loads((other / 'manifest.json').read_text(encoding='utf-8'))
        for value in (manifest, other_manifest):
            if not re.fullmatch('[0-9a-f]{32}', value.get('build_id', '')): raise ValueError('3.1 build_id is missing')
            if value.get('input_sha256') != sha(input_path): raise ValueError('comparison input differs')
            if value.get('profile') != 'public': raise ValueError('comparison must use public profile')
        if manifest['build_id'] == other_manifest['build_id']: raise ValueError('comparison is a copy of the same build')
        if manifest.get('renderer_sha256') != other_manifest.get('renderer_sha256'): raise ValueError('renderer versions differ')
        if set(manifest['outputs']) != set(other_manifest['outputs']): raise ValueError('output sets differ')
        for name in manifest['outputs']:
            if name not in ('interior.pdf', 'front-cover.pdf', 'book.pdf', 'wrap-cover.pdf'): raise ValueError('unknown output entry')
            if sha(output / name) != sha(other / name): raise ValueError('PDF bytes differ: ' + name)
            if sha(other / name) != other_manifest['outputs'][name]['sha256']: raise ValueError('comparison manifest stale: ' + name)
    except (OSError, KeyError, TypeError, ValueError) as exc: errors.append(str(exc))
    record('release_independent_rebuild_matches', not errors, errors)
    record('release_all_technical_checks', technical_passed)
    return checks


def verify(input_path, output, compare=None, review_decisions=None, require_visual_review=False,
           content_review_path=None, require_public_release=None):
    data = json.loads(Path(input_path).read_text(encoding='utf-8'))
    output = Path(output)
    manifest = json.loads((output / 'manifest.json').read_text(encoding='utf-8'))
    layout = manifest.get('layout', {})
    inner = float(layout.get('inner_mm', 13)); outer = float(layout.get('outer_mm', 10))
    top = float(layout.get('top_mm', 12)); bottom = float(layout.get('bottom_mm', 15))
    body_width = float(layout.get('body_width_mm', 108 - inner - outer))
    checks = []

    def record(name, passed, detail=None):
        checks.append({'name': name, 'passed': bool(passed), 'detail': detail})

    record('manifest_input_hash_matches', manifest.get('input_sha256') == sha(input_path),
           {'recorded': manifest.get('input_sha256'), 'actual': sha(input_path)})

    interior = fitz.open(output / 'interior.pdf')
    reader = fitz.open(output / 'book.pdf')
    cover = fitz.open(output / 'front-cover.pdf')
    record('even_interior', len(interior) % 2 == 0, len(interior))
    record('reader_page_count', len(reader) == len(interior) + 1,
           {'interior': len(interior), 'reader': len(reader)})
    record('reader_interior_text_matches', len(reader) == len(interior) + 1 and all(
        normalize(reader[index + 1].get_text()) == normalize(page.get_text()) for index, page in enumerate(interior)))
    record('reader_front_cover_text_matches', normalize(reader[0].get_text()) == normalize(cover[0].get_text()))
    record('one_front_cover', len(cover) == 1)
    dimensions = [(round(page.rect.width / MM, 3), round(page.rect.height / MM, 3))
                  for pdf in (interior, reader, cover) for page in pdf]
    record('all_trim_108x175', all(abs(w - 108) < .01 and abs(h - 175) < .01 for w, h in dimensions))
    bad_boxes = []
    for name in ('interior.pdf', 'front-cover.pdf', 'book.pdf'):
        for index, page in enumerate(PdfReader(output / name).pages, 1):
            media, crop = [float(x) for x in page.mediabox], [float(x) for x in page.cropbox]
            if any(abs(a - b) > .2 for a, b in zip(media, crop)) or int(page.get('/Rotate', 0)) % 360:
                bad_boxes.append({'file': name, 'page': index, 'media': media, 'crop': crop})
    record('media_crop_boxes_and_rotation', not bad_boxes, bad_boxes)
    record('manifest_page_count', manifest['interior_pages'] == len(interior))
    record('spine_from_interior', math.isclose(manifest['spine_mm_estimate'], len(interior) * .002252 * 25.4))

    fonts = {name: embedded_fonts(output / name) for name in ('interior.pdf', 'front-cover.pdf', 'book.pdf')}
    record('fonts_embedded', all(all(items.values()) for items in fonts.values()), fonts)
    # A paragraph can span pages. Exclude running heads and folios before
    # testing its contiguous source text, otherwise furniture interrupts it.
    full_text = normalize(''.join(page.get_text(clip=fitz.Rect(0, top * MM, 108 * MM, (175 - bottom) * MM))
                                 for page in interior))
    absent = [{'type': kind, 'text': text[:100]} for kind, text in expected_text(data)
              if normalize(text) not in full_text]
    record('all_input_text_present', not absent, absent[:30])
    required_counts = Counter(normalize(text) for _, text in expected_text(data) if len(normalize(text)) >= 8)
    counts_missing = [{'text': text[:70], 'required': count, 'found': full_text.count(text)}
                      for text, count in required_counts.items() if full_text.count(text) < count]
    record('repeated_input_text_preserved', not counts_missing, counts_missing[:20])

    entries = manifest['toc']
    headings_missing = []
    for entry in entries:
        if normalize(entry['title']) not in normalize(interior[entry['page'] - 1].get_text()):
            headings_missing.append(entry)
    record('toc_points_to_actual_headings', not headings_missing, headings_missing)
    actual_titles = [entry['title'] for entry in entries if entry['key'].startswith('chapter-') and entry['level'] == 0]
    expected_titles = [f'第{i}章 {chapter["title"]}' for i, chapter in enumerate(data['chapters'], 1)]
    record('chapter_order', actual_titles == expected_titles, actual_titles)
    chapter_entries = [entry for entry in entries if entry['level'] == 0 and entry['key'].startswith('chapter-')]
    record('odd_chapter_starts', all(entry['page'] % 2 for entry in chapter_entries), chapter_entries)
    section_entries = [entry for entry in entries if entry['level'] == 1]
    record('four_sections_per_chapter', len(section_entries) == 4 * len(data['chapters']), len(section_entries))
    prologue = next(entry for entry in entries if entry['key'] == 'prologue')
    # TOC page numbers can be drawn before titles in the content stream. Rebuild
    # physical rows before comparing titles and page numbers, and remove leaders.
    toc_rows = []
    for page in interior[:prologue['page'] - 1]:
        groups = {}
        for _, spans, text in page_lines(page):
            if not spans:
                continue
            baseline = round(spans[0]['origin'][1], 1)
            groups.setdefault(baseline, []).append((spans[0]['bbox'][0], text))
        for baseline in sorted(groups):
            row = ' '.join(text for _, text in sorted(groups[baseline]))
            toc_rows.append(re.sub(r'(?:\.\s*){2,}', '', row))
    toc_text = normalize('\n'.join(toc_rows))
    toc_missing = [entry for entry in entries
                   if normalize(entry['title']) + str(entry['page']) not in toc_text]
    record('printed_toc_matches_manifest', not toc_missing, toc_missing[:10])

    all_lines = [(page.number + 1, line, spans, text) for page in interior for line, spans, text in page_lines(page)]
    body_size = float(data['book'].get('body_pt', 9))
    checks.extend(complete_body_font_audit(data, interior, output, manifest))
    bounds_failures = []
    for pn, line, spans, text in all_lines:
        if line['bbox'][1] < top * MM or line['bbox'][1] > (175 - bottom) * MM:
            continue
        left = (inner if pn % 2 else outer) * MM
        if line['bbox'][0] < left - .8 or line['bbox'][2] > left + body_width * MM + .8 or line['bbox'][3] > (175 - bottom) * MM + .8:
            bounds_failures.append({'page': pn, 'text': text[:80], 'bbox': line['bbox']})
    record('body_text_within_margins', not bounds_failures, bounds_failures[:20])
    footers = []
    for page in interior:
        if page.number == 0 or not page.get_text().strip():
            footers.append(True)
            continue
        candidates = [(line, spans) for line, spans, text in page_lines(page)
                      if text.strip() == str(page.number + 1) and line['bbox'][1] > 155 * MM]
        footers.append(bool(candidates))
    record('page_numbers_present', all(footers), [i + 1 for i, present in enumerate(footers) if not present])
    bad_folio_positions = []
    for pn, line, spans, text in all_lines:
        if text.strip() != str(pn) or line['bbox'][1] < 155 * MM:
            continue
        target = (108 - outer) * MM if pn % 2 else outer * MM
        x = line['bbox'][2] if pn % 2 else line['bbox'][0]
        if abs(x - target) > .5 or any(abs(span['size'] - 7) > .02 for span in spans):
            bad_folio_positions.append(pn)
    record('folio_outer_alignment_and_size', not bad_folio_positions, bad_folio_positions)
    captions = [(pn, line, spans, text) for pn, line, spans, text in all_lines
                if re.match(r'^[図表]\d+\.', text)]
    record('caption_size_7', bool(captions) and all(all(abs(span['size'] - 7) < .02 for span in spans)
                                                  for _, _, spans, _ in captions), len(captions))
    with TTFont(output / 'fonts' / 'sans_bold.ttf') as font:
        caption_font = font['name'].getDebugName(6)
    # MuPDF can truncate long PostScript names; retain the full family digest.
    record('caption_sans_bold', bool(captions) and all(all(caption_font.split('-')[0] == span['font'].split('-')[0] for span in spans)
                                                    for _, _, spans, _ in captions), caption_font)
    record('caption_no_full_stop', all(not text.rstrip().endswith(('。', '．', '.')) for _, _, _, text in captions))
    caption_align = []
    for pn, line, _, text in captions:
        left = (inner if pn % 2 else outer) * MM
        if text.startswith('表'):
            caption_align.append(abs(line['bbox'][0] - left) < 1)
        else:
            center = left + body_width * MM / 2
            caption_align.append(abs((line['bbox'][0] + line['bbox'][2]) / 2 - center) < 2)
    record('caption_alignment', all(caption_align), caption_align)

    indent_evidence = []
    for block in blocks(data):
        if block['type'] != 'p' or len(block['text']) < 8:
            continue
        prefix = normalize(block['text'][:8])
        candidates = [(pn, line) for pn, line, _, text in all_lines if normalize(text).startswith(prefix)]
        if len(candidates) == 1:
            pn, line = candidates[0]
            target = (inner if pn % 2 else outer) * MM + body_size
            indent_evidence.append({'prefix': prefix, 'offset_pt': round(line['bbox'][0] - target, 3),
                                    'passed': abs(line['bbox'][0] - target) < .5})
    record('paragraph_first_line_indent', bool(indent_evidence) and all(x['passed'] for x in indent_evidence), indent_evidence[:30])

    leading_evidence = []
    for block in blocks(data):
        if block['type'] != 'p' or len(block['text']) < 35:
            continue
        prefix = normalize(block['text'][:8])
        candidates = [(index, pn, line, spans) for index, (pn, line, spans, text) in enumerate(all_lines)
                      if normalize(text).startswith(prefix)]
        if len(candidates) != 1:
            continue
        index, pn, line, spans = candidates[0]
        if index + 1 < len(all_lines):
            next_pn, _, next_spans, next_text = all_lines[index + 1]
            if next_pn == pn and spans and next_spans and normalize(next_text) in normalize(block['text']):
                leading = next_spans[0]['origin'][1] - spans[0]['origin'][1]
                leading_evidence.append(round(leading, 3))
    if leading_evidence:
        expected_leading = float(data['book'].get('leading_pt', 13))
        record('body_line_leading', all(abs(value - expected_leading) < .05 for value in leading_evidence), leading_evidence)

    technical_ranges = []
    for index, entry in enumerate(chapter_entries):
        following = chapter_entries[index + 1]['page'] if index + 1 < len(chapter_entries) else next(
            item['page'] for item in entries if item['key'] == 'epilogue')
        technical_ranges.append((entry['page'], following, entry['title']))
    header_failures = []
    observed_header_pages = set()
    for page_number, line, spans, text in all_lines:
        if line['bbox'][3] >= top * MM:
            continue
        observed_header_pages.add(page_number)
        relevant = next(((start, end, title) for start, end, title in technical_ranges
                         if start <= page_number < end), None)
        if not relevant or page_number % 2 == 0 or page_number == relevant[0]:
            header_failures.append({'page': page_number, 'unexpected_header': text})
        elif abs(line['bbox'][2] - (108 - outer) * MM) > .8:
            header_failures.append({'page': page_number, 'wrong_alignment': text})
    for start, end, title in technical_ranges:
        for page_number in range(start + 1, end):
            if page_number % 2 == 0:
                continue
            body_text = interior[page_number - 1].get_text(clip=fitz.Rect(0, top * MM, 108 * MM, (175 - bottom) * MM)).strip()
            if body_text and page_number not in observed_header_pages:
                header_failures.append({'page': page_number, 'missing_header': title})
    record('running_headers_correct_pages_and_alignment', not header_failures, header_failures)

    superscripts = []
    for pn, _, spans, _ in all_lines:
        for index, span in enumerate(spans):
            if re.fullmatch(r'\[[A-Za-z0-9_.:-]+\]', span['text']):
                neighbours = [other for other in spans if abs(other['size'] - body_size) < .02]
                if neighbours:
                    rise = neighbours[0]['origin'][1] - span['origin'][1]
                    superscripts.append({'page': pn, 'size': span['size'], 'rise': round(rise, 3)})
    if any('[[' in block.get('text', '') for block in blocks(data)):
        record('citations_superscript_7_rise_2p4', bool(superscripts) and all(
            abs(s['size'] - 7) < .02 and abs(s['rise'] - 2.4) < .05 for s in superscripts), superscripts)

    if compare:
        compare = Path(compare)
        equal = {name: sha(output / name) == sha(compare / name) for name in manifest['outputs']}
        record('deterministic_pdf_hashes', all(equal.values()), equal)
    record('manifest_output_hashes', all(sha(output / name) == info['sha256']
                                       for name, info in manifest['outputs'].items()))
    cover_lines = [(line, spans, text) for page in cover for line, spans, text in page_lines(page)]
    record('cover_three_title_lines_17pt', all(any(text.strip() == expected and all(abs(span['size'] - 17) < .02 for span in spans)
                                                  for _, spans, text in cover_lines) for expected in data['book']['cover_lines']))
    source_image = Path(input_path).resolve().parent / data['book']['cover_image']
    source_pixels = pixel_fingerprint(source_image)
    cover_images = cover[0].get_image_info(xrefs=True)
    image_checks = []
    for info in cover_images:
        if not info.get('xref'): continue
        extracted = cover.extract_image(info['xref'])
        pixels = pixel_fingerprint(extracted['image'])
        bbox = info['bbox']; width, height = bbox[2] - bbox[0], bbox[3] - bbox[1]
        ppi = min(info['width'] / (width / 72), info['height'] / (height / 72))
        ratio_error = abs(width / height - source_pixels['size'][0] / source_pixels['size'][1])
        image_checks.append({'same_pixels': pixels == source_pixels, 'ppi': round(ppi, 3),
                             'aspect_ratio_error': ratio_error})
    record('cover_asset_pixels_resolution_aspect', any(item['same_pixels'] and item['ppi'] >= 299.9 and item['aspect_ratio_error'] < .0001
                                                       for item in image_checks), image_checks)
    geometry = geometry_audit(data, interior, manifest, review_decisions)
    checks.extend(geometry['checks'])
    checks.append(code_indentation_audit(data, interior, output, layout))
    if require_visual_review:
        record('all_pages_full_size_visual_review_recorded', geometry['full_size_visual_review_complete'])
        record('all_review_flags_resolved', not geometry['unresolved_review_flags'], geometry['unresolved_review_flags'])
    technical_passed = all(item['passed'] for item in checks)
    release_checks = publication_audit(data, input_path, output, manifest, compare,
                                       content_review_path, geometry, technical_passed)
    ready = technical_passed and all(item['passed'] for item in release_checks)
    enforce = data.get('profile') == 'public' if require_public_release is None else require_public_release
    result = {'passed': ready if enforce else technical_passed,
              'pass_scope': 'public_release' if enforce else 'technical_only',
              'technical_checks_passed': technical_passed,
              'checks': checks + release_checks if enforce else checks,
              'publication_checks': release_checks, 'layout_audit': geometry,
              'public_release_ready': ready,
              'limits': ['Publication readiness requires recorded content and visual audits; their factual truth is not automatically established.',
                         'Draft/omitted profile can pass technical QA but can never be public_release_ready.',
                         'KDP acceptance and physical print proof are separate.']}
    interior.close(); reader.close(); cover.close()
    return result


def main():
    parser = argparse.ArgumentParser(description=__doc__)
    parser.add_argument('--input', required=True, type=Path)
    parser.add_argument('--output', required=True, type=Path)
    parser.add_argument('--compare', type=Path)
    parser.add_argument('--report', type=Path)
    parser.add_argument('--review-decisions', type=Path)
    parser.add_argument('--content-review', type=Path)
    release = parser.add_mutually_exclusive_group()
    release.add_argument('--require-public-release', dest='require_public_release', action='store_const', const=True)
    release.add_argument('--layout-only', dest='require_public_release', action='store_const', const=False)
    parser.set_defaults(require_public_release=None)
    parser.add_argument('--require-visual-review', action='store_true')
    args = parser.parse_args()
    decisions = json.loads(args.review_decisions.read_text(encoding='utf-8')) if args.review_decisions else None
    result = verify(args.input, args.output, args.compare, decisions, args.require_visual_review,
                    args.content_review, args.require_public_release)
    payload = json.dumps(result, ensure_ascii=False, indent=2) + '\n'
    if args.report:
        args.report.write_text(payload, encoding='utf-8')
    print(payload)
    raise SystemExit(0 if result['passed'] else 1)


if __name__ == '__main__':
    main()
```

### layout-fixture.json

<!-- asset:layout-fixture.json;encoding:text -->
```json
{
  "book": {
    "title": "The Little Book of Kaggle 1st Place Solutions",
    "cover_lines": [
      "The Little Book",
      "of",
      "Kaggle 1st Place Solutions"
    ],
    "author": null,
    "cover_image": "assets/cover.png",
    "wrap_cover": false
  },
  "frontmatter": [
    {
      "type": "p",
      "text": "組版検証用。すべて架空の教材であり、既存の競技の解法を主張しない。"
    }
  ],
  "prologue": {
    "title": "On Beginning Again",
    "blocks": [
      {
        "type": "p",
        "text": "一つの観察から、次の比較を選ぶ。これは生成経路を確かめるための文章である。"
      }
    ]
  },
  "chapters": [
    {
      "title": "架空の競技 Alpha",
      "sections": [
        {
          "title": "タスク",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "h2",
              "text": "評価の意味"
            },
            {
              "type": "formula",
              "text": "score = (a + b) / 2"
            },
            {
              "type": "table",
              "title": "条件の対応。",
              "headers": [
                "条件",
                "観測する値"
              ],
              "rows": [
                [
                  "基準",
                  "得点と計算時間"
                ],
                [
                  "変更",
                  "同じ予算での得点と計算時間"
                ]
              ]
            }
          ]
        },
        {
          "title": "基本解法",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "code",
              "language": "Python（検証用）",
              "text": "def score(a, b):\n    return (a + b) / 2\n\nassert score(1, 3) == 2",
              "kind": "python"
            }
          ]
        },
        {
          "title": "1位解法",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "figure",
              "title": "解法の関係",
              "height_mm": 52,
              "nodes": [
                {
                  "id": "a",
                  "label": "入力と条件",
                  "x": 0.05,
                  "y": 0.65,
                  "w": 0.35,
                  "h": 0.25
                },
                {
                  "id": "b",
                  "label": "比較と判断",
                  "x": 0.6,
                  "y": 0.15,
                  "w": 0.35,
                  "h": 0.25
                }
              ],
              "edges": [
                [
                  "a",
                  "b"
                ]
              ]
            }
          ]
        },
        {
          "title": "自力で1位解法に辿り着くには",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "figure",
              "title": "発見へ進む判断",
              "height_mm": 52,
              "nodes": [
                {
                  "id": "a",
                  "label": "入力と条件",
                  "x": 0.05,
                  "y": 0.65,
                  "w": 0.35,
                  "h": 0.25
                },
                {
                  "id": "b",
                  "label": "比較と判断",
                  "x": 0.6,
                  "y": 0.15,
                  "w": 0.35,
                  "h": 0.25
                }
              ],
              "edges": [
                [
                  "a",
                  "b"
                ]
              ]
            }
          ]
        }
      ]
    },
    {
      "title": "架空の競技 Beta",
      "sections": [
        {
          "title": "タスク",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "h2",
              "text": "評価の意味"
            },
            {
              "type": "formula",
              "text": "score = (a + b) / 2"
            },
            {
              "type": "table",
              "title": "条件の対応。",
              "headers": [
                "条件",
                "観測する値"
              ],
              "rows": [
                [
                  "基準",
                  "得点と計算時間"
                ],
                [
                  "変更",
                  "同じ予算での得点と計算時間"
                ]
              ]
            }
          ]
        },
        {
          "title": "基本解法",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "code",
              "language": "Python（検証用）",
              "text": "def score(a, b):\n    return (a + b) / 2\n\nassert score(1, 3) == 2",
              "kind": "python"
            }
          ]
        },
        {
          "title": "1位解法",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "figure",
              "title": "解法の関係",
              "height_mm": 52,
              "nodes": [
                {
                  "id": "a",
                  "label": "入力と条件",
                  "x": 0.05,
                  "y": 0.65,
                  "w": 0.35,
                  "h": 0.25
                },
                {
                  "id": "b",
                  "label": "比較と判断",
                  "x": 0.6,
                  "y": 0.15,
                  "w": 0.35,
                  "h": 0.25
                }
              ],
              "edges": [
                [
                  "a",
                  "b"
                ]
              ]
            }
          ]
        },
        {
          "title": "自力で1位解法に辿り着くには",
          "blocks": [
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "p",
              "text": "これは組版検証用の架空例である。競技の結果や実測を示さない。入力を受け取り、比較条件をそろえて、評価値を確認する。[[S01]]"
            },
            {
              "type": "figure",
              "title": "発見へ進む判断",
              "height_mm": 52,
              "nodes": [
                {
                  "id": "a",
                  "label": "入力と条件",
                  "x": 0.05,
                  "y": 0.65,
                  "w": 0.35,
                  "h": 0.25
                },
                {
                  "id": "b",
                  "label": "比較と判断",
                  "x": 0.6,
                  "y": 0.15,
                  "w": 0.35,
                  "h": 0.25
                }
              ],
              "edges": [
                [
                  "a",
                  "b"
                ]
              ]
            }
          ]
        }
      ]
    }
  ],
  "epilogue": {
    "title": "He Will Win the Next Competition",
    "blocks": [
      {
        "type": "p",
        "text": "得た理解を次の比較に生かす。"
      }
    ]
  },
  "appendix": {
    "title": "付録",
    "blocks": [
      {
        "type": "h2",
        "text": "出典"
      },
      {
        "type": "p",
        "text": "[S01] この検証のために作成した架空の例。外部の競技資料ではない。"
      }
    ]
  },
  "profile": "draft"
}
```

### cover-prompt.txt

<!-- asset:cover-prompt.txt;encoding:text -->
```text
Use case: illustration-story
Asset type: original illustration to place beneath a separately typeset title on a small Japanese technical book cover, The Little Book of Kaggle 1st Place Solutions.
Create a completely new high-quality portrait illustration, approximately 4:5 aspect ratio, at least 1200 px wide.
Scene: a quiet cottage garden with an outdoor wooden reading table, one open blank book, a couple of closed unmarked books, flowers, and a calm goose standing beside the table. The book celebrates patient study, experimentation, reflection, and learning.
Style: refined monochrome graphite and delicate pen engraving, fine natural texture and restrained gray washes, white paper, literary small-press book illustration. Natural anatomy and plausible perspective, mature understated composition.
Composition: complete scene contained within the image, generous clean white perimeter on all four sides, soft natural fade into pure white edges, no enclosing rectangular border; keep main goose, open book, and table distinct and legible when printed 78 by 98 mm. Moderate detail, no muddy dark mass, no essential element cropped. This is illustration only; typography will be added by layout code outside the illustration.
Palette: strictly black, neutral gray, and pure white, no hue.
Text: no letters, no numbers, no text, no labels, no watermark, no logos.
Invariants: original unbranded artwork; quiet reading garden, visible blank open book, single goose, bright white surround, grayscale, publication quality.
Variation: 
```


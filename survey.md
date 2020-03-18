---
tags: kubeflow
---

# kubeflow community & release survey

- 初版：2019/08/06
- Update:2020/03/18

## 調査結果サマリ

- 2020/03/10 にリリースされた。
    - v1.0はv1.0-rc1などのバージョンが存在せず3/10に突如リリースされた。
- v1.0で予定されていた開発コンポーネントは大部分が予定通りにリリースされている。
- 機能的な観点では、今回のリリースによってDevelop→Build→Train→Deploy→Develop... のループを回すための最低限のコンポーネントが揃ったと報告されている。
    - ![](https://miro.medium.com/max/1600/0*tBPpU3UqM_MeJ0-P)
- 一方でコミュニティの運営の観点では、以下が報告されている。
    - Kubeflowを構成するコンポーネントがGraduatedとなる基準の[ガイドライン](https://github.com/kubeflow/community/blob/master/guidelines/application_requirements.md)が設定された。
    - コンポーネントのバージョンに関しても[ポリシー](https://www.kubeflow.org/docs/reference/version-policy/)が規定された。
    - 貢献数に占めるGoogleメンバーの割合は現在39%であり徐々に割合が下がってきている。コミュニティとしての公平性も徐々に整ってきている印象がある。

## リリース日まとめ

| バージョン | 予定 | 実績 | 備考 |
| --- | --- | --- | --- |
| v0.5 | 2019/03末 | 2019/04/09 |  |
| v0.6 | 明示されず | 2019/07/19| v0.5からおよそ3ヶ月後 |
| v0.7 | 2019/10 | [2019/11/05](https://github.com/kubeflow/kubeflow/releases/tag/v0.7.0)  | v0.6からおよそ3ヶ月後。当初予定から若干スライドして11月の頭にリリースされた。 |
| v1.0 | 2020/01〜03 | [2020/03/10](https://github.com/kubeflow/kubeflow/releases/tag/v1.0) | v1.0はRCなどは無く突如v1.0がリリース |

- コミュニティとしてはリリースは3ヶ月ごとと決めている様子。

## リリースごとの実装機能の予定と実際

### v0.5

- ソース
    - https://medium.com/kubeflow/kubeflow-v0-5-simplifies-model-development-with-enhanced-ui-and-fairing-library-78e19cdc9f50

- 予定
    - 主にUIを改善してJupyterNotebookの利用者(データサイエンティスト)が集中できる環境を整備
    - ※この頃からCUJ(CriticalUserJourney)という単語が散見される。一般的なWebサイトの設計などでも使われる単語の模様。意味合いとしては、ユーザの目標を達成するためにユーザが必要な作業やページの遷移などを指す。Kubeflowコミュニティとしてはユーザ(おそらくデータサイエンティスト)が自分たちの一連のML処理(build-train-deploy)を実行できるように(UIだけで完結するように)整備していくモチベーションが高いと思われる。
- 実績
    - Kubeflowのデプロイが容易になった。
    - その他は当初の予定通りUIの改善がメイン。
    - Jupyter Notebookからボリュームをアタッチ可能
    - 複数のJupyter Notebookを同時に起動可能
    - FairingによってJupyter NotebookなどからKubeflowのジョブを作成することが可能
    - Kubeflowのダッシュボードの見た目の統一

### v0.6
- ソース
    - https://github.com/kubeflow/kubeflow/releases
    - https://medium.com/kubeflow/kubeflow-v0-6-a-robust-foundation-for-artifact-tracking-data-versioning-multi-user-support-9896d329412c

- 予定
    - 主に[ksonnet から kustomize への移行](https://docs.google.com/document/d/1SVm-xffIdWiMYkl_nQO5C6HHK46NWkfDGPDUL5ukeME/edit#)
- 実績
    - Metadataコンポーネントの追加
    - multi-user authentication & authorization with SSO.
        - Istioを使って実現している
    - Kubeflow Pipelines’ DSL which support Persistent Volumes and Volume Snapshots
    - ドキュメントの改善
    - ksonnet から kustomize への移行

### v0.7
- ソース
    - リリース: https://github.com/kubeflow/kubeflow/releases/tag/v0.7.0
    - [更新内容(Draft)](https://docs.google.com/document/d/13fv-D0m40v1ugE1Pt8kXe0T7xA5MSS1yno3dUK732r8/edit#heading=h.s5sf36exyj4f)
        - [最終ドラフト](https://medium.com/@joshbottum/kubeflow-v0-7-delivers-beta-functionality-in-the-leadup-to-v1-0-1e63036c07b8)
        - [ref](https://github.com/kubeflow/community/issues/294): いまだ詳細のリリースノートが公開されていない模様。
    - Gihtubでのタスク管理: https://github.com/orgs/kubeflow/projects/22
        - カンバン形式によるタスク管理が実施されている。
    - その他: [ref1](https://github.com/kubeflow/kubeflow/blob/c6abed891c57338d94c146458662bc14e5c780ea/ROADMAP.md), [ref2](https://github.com/kubeflow/kubeflow/commit/c6abed891c57338d94c146458662bc14e5c780ea#diff-38574c080d4e2eb38c49b86e6588ad98)

- 予定
    - Notebooksの改善(JupyterNotebookやKubeflow関連Webアプリの改善)
    - Deployment
        - kfctlコマンドの改善
        - KfDefをv1beta1へ(KfDefはkfctlが解釈するデプロイ設定ファイルの形式)
        - マイナーバージョンのアップグレードサポート
    - Metadata
        - Metadataコンポーネントの更新
    - Enterprise Support
        - Namespaceごとにアクセス範囲を限定
        - Profileコントローラをbetaへ
        -  identity management APIとUIをbetaへ
    - Onpremise Support
        - オンプレ環境でのE2E実行サポート
        - マルチユーザ対応
    - テスト等の改善
    - Pipelines
        - 開発用途としてローカルでの実行機能
        - Metadataとの連携を拡充
- 実績
    - KFServingによるモデルのサービングと管理の更新
        - Tensorflow, PyTorch等を使ったサービングが可能になっている模様。
    - kfctlの拡張
        - build や deploy に関する操作を簡易化。
            - [ここ](https://raw.githubusercontent.com/kubeflow/manifests/v0.7-branch/kfdef/kfctl_existing_arrikto.0.7.0.yaml)のような設定ファイルを利用してKubeflowの設定を定義し、 `kfctl apply -f` で適用できるようになった。
        - APIバージョンが v1beta1 へ。次のリリースでは v1 になる予定。
    - Kubeflowアプリケーション(Kubeflowの構成コンポーネント) のバージョンや稼働時間などが確認できるようになった。
    - Kubeflow Notebook(JupyterNotebook)のAPIバージョンが上がりv1.0への準備が進んでいる。また、NotebookのイメージにTensorflow2.0(GPU対応付き)が含まれるようになった。
    - ML用のOperator(TFJob 1.0, Pytorch 1.0など) をv1.0に向けて更新。
    - KatibとMetadataの更新
        - 将来的にPipelinesと連携して、メタデータやハイパーパラメータを利用できるようになる模様。
    - Pipelinesの各種機能更新
        - Metadataとの連携機能
        - 新規パラメータの追加
        - その他コンポーネントとの連携サンプル
    - マルチユーザ操作を行うための権限の整備(K8SのClusterRoleBinding周り）
    - PythonからKubeflowを利用するためのSDKの整備
    - GoogleServiceAccountとの連携機能の実装。
        - Kubeflow上のプロセスからGCPサービスをシームレスに利用可能になる模様。
    - ドキュメント整備
        - KFServing
        - Pipelines
        - Metadataなど
### v1.0
- ソース
    - https://github.com/kubeflow/kubeflow/blob/master/ROADMAP.md
    - https://medium.com/kubeflow/the-making-of-kubeflow-1-0-designing-for-stability-and-broad-market-adoption-a190358e96b6
    - https://medium.com/kubeflow/kubeflow-1-0-cloud-native-ml-for-everyone-a3950202751
- 予定
    - Pipelinesを始めとする機能の整備が完了していること
    - We are targeting a 1.0 release in January 2020. Our 1.0 release consists of the following key pieces
  - build-train-deployの流れのCUJ(build-train-deployの一連の処理)を実現できるようになっていること。
  - Cloudとオンプレで、セキュアなデプロイの実現とマルチユーザでKubeflowが利用できること。
- 以下のコンポーネントは1.0になっていること。
    - kfctl
    - TFJob and PyTorch(既になっている)
    - Jupyter notebook controllerと周辺のwebアプリ
    - Profile controllerとUI
- 以下はBetaになっていることが望ましい。
    - Katib
    - fairing SDK
    - Metadata SDKとUIとバックエンド
    - KFServing
    - Pipelines
- 実績
    - 2020/03/10 にリリースされた。
        - v1.0はv1.0-rc1などのバージョンが存在せず3/10に突如リリースされた。
    - Stableのコンポーネントは以下。(これらは予定されていた通りリリース)
        - Kubeflow’s UI, the central dashboard
        - Jupyter notebook controller and web app
        - Tensorflow Operator (TFJob) and PyTorch Operator for distributed training
        - kfctl for deployment and upgrades
        - Profile controller and UI for multiuser management
    - Betaのコンポーネントは以下。(KFServingだけリリースされていないが、それ以外は予定通りのリリース)
        - Pipelines (beta) for defining complex ML workflows
        - Metadata (beta) for tracking datasets, jobs, and models,
        - Katib (beta) for hyper-parameter tuning
        - Distributed operators for other frameworks like xgboost
    - 今回の注目点は以下。
        - Develop→Build→Train→Deploy→Develop... のループを回すための最低限のコンポーネントが揃った。
        - ![](https://miro.medium.com/max/1600/0*tBPpU3UqM_MeJ0-P)
        - Jupyterを使ってモデルを開発(Develop)し、Fairing等を使って学習を実行するコンテナイメージを作成(Build)、Kubeflow上でTFやPyTorchなどを使い学習(Train)し、KFServingを使いサービスを提供(Deploy)する。
        - WebブラウザからアクセスできるKubeflow UIを使い各データサイエンティスト用のJupyterを起動、必要なリソース制限を指定して一定のパフォーマンスを確保することなども可能。
        - kfctlを使うことでk8sクラスタに対するKubeflowのインストールが可能。各IaaS向けに1コマンドで導入が完了するUXになった。
        ```sh
        # Kubeflowのインストールコマンド例。
        kfctl apply -f kfctl_gcp_iap.v1.0.0.yaml
        kfctl apply -f kfctl_k8s_istio.v1.0.0.yaml
        kfctl apply -f kfctl_aws_cognito.v1.0.0.yaml
        kfctl apply -f kfctl_ibm.v1.0.0.yaml
        ```
        - TensorBoardをデプロイすることで、推論の精度などのモニタリングも可能。
    - コミュニティの運営の観点からは以下が注目される。
        - Kubeflowは2017年に発表され、その後約2年でv1.0となった。
        - Kubeflowを構成するコンポーネントがGraduatedとなる基準のガイドラインが設定された。
            - https://github.com/kubeflow/community/blob/master/guidelines/application_requirements.md
        - コンポーネントのバージョンに関してもポリシーが規定された。
            - https://www.kubeflow.org/docs/reference/version-policy/
        - v1.0のタイミングでコミュニティへ参加している企業は約33。
            - https://github.com/kubeflow/community/blob/master/member_organizations.yaml
        - 上記からコミュニティとしてのガバナンスは整備されてきている印象がある。また、貢献数に占めるGoogleメンバーの割合は現在39%であり徐々に割合が下がってきている。コミュニティとしての公平性も正しい方向に進んでいると考えられる。


<!--
    - 週次でコミュニティミーティングが実施され[v1.0に向けたタスクが管理されている](https://github.com/orgs/kubeflow/projects/25)。
    - 2020/02/28時点ではkubeflow/kubeflow v1.0に向けたP0(Priority0:最大重要度)トピックが残り13件。
    - 残りの要作業項目は少なくないが開発は進んでいる。
    - 2020/01/24にKubeflowの[v1.0用ビルドジョブが作成された](https://github.com/kubernetes/test-infra/pull/15999)
    - 登録されているジョブは殆どがkfctlのものであり、その他のコンポーネントに対するジョブは少ない。コミュニティノートを確認すると他のコンポーネントにおけるテストがまだ通らないものが多いため、現在コミュニティではテストの修正・実装を並行して実施していると思われる。
    - 一方、Kubeflow v1.0に含まれる予定のkfctlは現在 [v1.0](https://github.com/kubeflow/kfctl/releases)が2020/02/27にリリースされた。
-->

<!--
- Kubeflowの内部での活用指針を明確にする
    - Kubefowの利用シーンからの考察
    - KubeflowとGoogleなどの団体との関係からの考察
    - 構築・運用コストからの考察
-->

<!--
[here 2019-09-10 5:30PM PT](https://docs.google.com/document/d/1Wdxt1xedAj7qF_Rjmxy1R0NRdfv7UWs-r2PItewxHpE/edit#)
```
(Josh) Themes we came up with for 0.6, for context on what we thought of as feature candidates for 1.0
Kfctl (beta) 
Jupyter CR v1 beta
 Upgrade functionality
 Multi-User improvements  
Data Science & Workflow 
Enhancements 
Simplified integration with accelerators (gpu, tpu, nnp)
 Improved Tensorboard creation and management 
 Persistent Volume Management via a Central Dashboard UI 
Metadata enhancements: Logging, Parameter setting, Execution Context Metadata integration with Tensorboard, Katib 
```
-->

# その他
## コミュニティの状況

- KubeflowのOrgメンバーは42名
- 開発にはCLAサインが必要
    - https://www.kubeflow.org/docs/about/contributing/
    - https://github.com/kubeflow/community/blob/master/CONTRIBUTING.md
- v1.0 は 2020/01予定としているものの、2019 4Qリリース案もまだ考えている様子。
    - https://github.com/kubeflow/kubeflow/pull/3824#issuecomment-518326701
    - Github上でコンセンサスを取っている。対象メンバーは以下
        - @jlewi(Google)
        - @abhi-g(Google)
        - @ddutta(cisco)
        - @kkasravi(Intel)
        - @jbottum(Unknown)
        - @vkoukis(Unknown)
        - @theadactyl(Google)
        - @aronchick(Microsoft)
    - 上記8名がチェアか。
- kubeflowのdevstats
    - 開発に参加企業のうちGoogleは全体の45%の活動を占めており支配的。
        - https://devstats.kubeflow.org/d/5/companies-summary?orgId=1
    - 開発参加企業は約15。開発参加者は約280名。
    -  https://devstats.kubeflow.org/d/7/contributing-companies?orgId=1
- GCP上にKubeflowをデプロイするサイトが存在しており、Kubeflowをオンプレで使おうと考えるユーザが少ないか？
    - https://deploy.kubeflow.cloud/#/
- Googleの日本人
    - ウチダマコトさん
        - 共同でPipelinesでProposalを作ってる。
        - https://docs.google.com/document/d/1_n3q0mNOr7gUSM04yaA0e5BO9RrS0Vkh1cNCyrB07WM/edit#heading=h.fhhpb0lbxrjb

## イベント
### Kubeflow Contributor Summit 2019
- https://docs.google.com/document/d/14Jr79aWVjsJg8xq38CLVE4rKRwM1_-gHLuxhGAhrGTI/edit
- March 12 & 13, 2019
- サニーベール
### Kubeflow Summit
- https://github.com/kubeflow/community/wiki/Kubeflow-Summit,-October-2019-Day-1-Agenda
- Monday, October 28,29
    - from Gmail
- Kubeflow Summit Day 1
- Contributor Day on Day 2
### KubeCon + CloudNativeCon NA 2019
- https://events19.linuxfoundation.org/events/kubecon-cloudnativecon-north-america-2019/schedule/
- kubeflow で検索すると16件のセッションがヒット。
<!--- 内1件は[Googleによる有料のハンズオンのセッション](https://sched.co/W536)
- Kubeflow関連セッション MachineLearning + Data のトラック
    - 企業グレードの認証基盤との連携
    - KFServingの紹介
    - 事例 Snap(Computer Vision Model)
    - 事例 Lyft(メトリクスを測定・活用したKubeflowのクラスタについて)
    - 事例 Spotify 
    - Serverlessの文脈でKnative、Istio等との連携に関して
    - 金融機関での利用について(パネルディスカッション)
    - 医療関連での利用について
    - Kubeflowの使い方チュートリアルのセッション
- セッション数が増えていると同時に、事例紹介も一気に増えている。
- 逆にKubeflow自体の紹介は見当たらない。
-->
#### Building and Managing a Centralized Kubeflow Platform at Spotify 
- Keshi Dai & Ryan Clough, Spotify
- Spotify(音楽配信サービス)による社内の機械学習プラットフォームの構築と管理について
    - Spotifyはシステムの一式をGCPに乗せている。
    - 複数のチームが自律的(autonomy)にプロジェクトを遂行している。
    - 1チームは5-8名。Backend, Frontend, ML Engineer, Data Engineer, Data Scientistなどが各メンバーのロール。
    - 各チームがそれぞれのK8Sクラスタを作るとK8Sの技術と知識が必要となりサイロ化が進んでしまう。そのため、中央にK8Sクラスタを配置して複数のチームで使う構成とした。
        - この構成ではインフラの利用効率は高まり、ML技術を早期にサービスに適用することができた。
        - 一方でセキュリティ(チーム間の適切なアクセスコントロール)が課題として残った。
- セッション最後のまとめにて以下が述べられた。
    - MLエンジニアがKubeflowを使うための学習コストが高い
        - K8Sの専門知識が必要なため。
        - Spotifyではプラットフォームチームに依るK8S知識に対するサポートで対応している。
            - 負荷はインフラチームに集中している。
    - Kubelowはコンポーネントが多い(Kubeflow Pipelines, Metadata, Istio, Kustomize, etc)ため一度に活用するには大きすぎる。
        - そのための負荷はインフラチームに集中している。
    - セキュリティについて考慮するべきことは小さくない。
        - Kubeflowはマルチテナントに対応していない。
        - 私見としては、Kubernetes自体がマルチテナントに対してのアプローチがまだ薄いと感じる。
## その他
Kubeflowを内部で活用するための指針を明確にするため、以下をまとめる。
- Kubefowの利用シーンからの考察
- KubeflowとGoogleなどの団体との関係からの考察
- 構築・運用コストからの考察

### Kubefowの利用シーンからの考察
1. データサイエンティストの個人マシンあるいは限定的な小規模デプロイを使ってある程度試す。次に大規模なKFクラスタにデプロイして本番の処理を実施するパターン
1. 大規模なKFクラスタを構築、社内のデータサイエンティストが試行錯誤からそのクラスタで実施するパターン
 
- 大規模なクラスタはどこに作るか？
    - オンプレ環境に構築する。
    - GCP等パブリッククラウドのVMに構築する。
        - 特にGCPでは[Kubeflowデプロイ自動化のページ](https://deploy.kubeflow.cloud/#/deploy)が存在している。
            - [使い方の解説ページ](https://www.kubeflow.org/docs/gke/deploy/deploy-ui/)
        - Spotifyはこちらのパターン

- 学習対象データとしてクラウドに配置できない特性を持つものがある？(情報の機密性の観点から)
    - あるならオンプレで実行するしか無い。
    - 機密性のある情報をマスクすればクラウドに上げることが可能か？
- 大量のデータが存在する場合にクラウドに転送するコストが無視できないことがありえるか？
    - あり得ると思うが、当初よりその観点がネックとなる案件は珍しいと思う。
- オンプレのインフラが足りないときにクラウド側に処理をオフロードしたい要求があるか？
    - あると思う。その分費用は高くなると思われるが。

- 段階的な移行アプローチをとりたいときの移行作業量インパクトを小さくするための使い方としてKubeflowを考えることが可能ではないか？ 
    - 個人マシンのAll-in-Oneクラスタ
    - オンプレ小規模クラスタ
    - オンプレ大規模クラスタ
    - クラウドの大規模クラスタ
- これらの環境間で同一の学習処理を実行したい場合、KFを使えば環境を移行するときのインパクトを少なくすることが可能。
    - 機械学習におけるKubernetesのような位置づけになるのが究極的なゴールと捉えることが可能。

- 必要な要素・作業・スキル
    - KFのデプロイスキル
    - KFの運用スキル
    - KF利用のスキル
    - KF利用のための教育
    - KF利用のコンサル
    - ---
    - k8sのデプロイスキル
    - k8sの運用スキル
    - k8s利用のスキル
    - k8s利用のための教育
    - k8s利用のコンサル

- この、もれなく「k8sの○○○○」が必要となるのがKF導入の最も大きな障害になり得ると考える。

- 機械学習にコンテナライズの概念をとりいれることにより、環境移行インパクトの最小化、高い再現性の実現、CI/CDとの親和性向上などが見込める。
    - これはk8sを取り入れることによるアプリケーション開発・サービス開発にもたらされる利点と全く同一。
    - k8sの上に構築されている仕組みなのである意味で自明であるが。
- であれば、コンテナライズのアプローチと全く同じことが言える。[CNCF Trail Map](https://raw.githubusercontent.com/cncf/trailmap/master/CNCF_TrailMap_latest.png)と同じアプローチ。
    - アプリケーションを開発
    - アプリケーションをコンテナ化(Containerization)
    - CI/CDの仕組みに乗せる
        - 開発効率の向上
    - KFに適用する(Orchestration)
        - 実行処理効率の向上
    - 繰り返す
        - CI/CDに乗っているので繰り返しが容易
    - モニタリング(Observability&Analysis)
        - ML処理の精度測定：アプリケーションの精度向上の判断材料となる。
        - 実行処理の効率測定：インフラ増強・別の環境利用の判断材料となる。

- 最近のk8s界隈はマルチクラウドでマルチk8sクラスタの流れも出てきている。これと同じことがKFによる機械学習でも言えると思う。つまり環境移行のインパクトを少なく、多くの環境で同じ処理を実施可能になる世界の実現。

### KubeflowとGoogleなどの団体との関係からの考察
- Kubeflowが一番効率よく利用できるのはGCPと考えられる。
- Kubeflowコミュニティ内でのGoogleの割合は緩やかに減少しており、コミュニティとして健全な構成になりつつあると考えられる。


- 現在はAWSやAzureなどでのエンドトゥエンドテスト(e2eテスト)も実装されているので、他のパブリッククラウドとの親和性も今後向上すると予想できる。
- とはいえ、新機能のチュートリアルなどは一番早く公開されるのはGCPを使った利用方法であることが多い。(PipelinesのチュートリアルではGCP Cloud Storageとの連携が前提として書かれていた時期があった。)
- 開発に参加企業のうちGoogleは全体の40%(44895/111733)の活動を占めており支配的だが、前回の調査時には45%(2019/12)だったため、緩やかにではあるがGoogleから他の企業へ分散してきていることがわかる。
- 開発参加企業は約15。開発参加者は約319名。前回(2019/12)は開発参加企業は約15。開発参加者は約280名だったため、開発者も緩やかに増加している。
- https://devstats.kubeflow.org/d/5/companies-summary?orgId=1
- https://devstats.kubeflow.org/d/7/contributing-companies?orgId=1

### 構築・運用コストからの考察
- Kubeflow自体を構築・運用するコストは決して低くない。


### ネタ
Kubeflowの構想として、データサイエンティストやMLシステムのオペレータに寄り添ったUXｗ提供するというのが当初からある。
思い立ったらすぐに活用できるような手軽さと、実際に計算処理を実行するインフラ構成の細部までは意識する必要のない仕組みを提供するのがあるべき姿だと考える。

その時、まずデータサイエンティストには「特定のフレームワークを強要しない」というのが重要だとこれまでの活動の中で感じている。
データサイエンティストはプログラム全般のスペシャリストではなく「自分が得意とする特定のMLフレームワークを極限まで活用できるスキルを持った専門家(プログラマではない)」という認識を持ちました。
そのため、彼らが扱える世界に寄り添う仕組みが必要なのだと考える。
また、MLシステムのオペレータは純粋なインフラオペレータとも違い、MLシステムを構成する主なリソース(CPU、メモリ、GPUなど)のみから考えた効率的なスケジューリングや、稼働中のMLシステムのメトリクス取得・分析機能を必要としているのだと考えます。

ここまでで考えると巷のML系、AI系のクラウドサービスでも実現可能だと感じているが、Kubelowは自分たちで構築できるというのも特徴だと考えている。(OSSとしての特徴ですが。)
現在ではクラウドサービスが広く受け入れられており、その手軽さや従量課金性から利用者数は増えていると思うが、一方でオンプレにそれなりに大きなインフラを抱えている企業や団体が、時bンたちのインフラを活用するためにKubeflowをデプロイするというシナリオがあると思います。

これは、Kubeflowコミュニティの動向調査結果で以前に触れていますが、Kubeflowコミュニティは比較的多くの教育機関(大学など)が参加しています。
これは、
・研究する際のツールとしてML、AIに興味のある機関が多いだろうこと。
　(ML,AI自体を研究している場合もあると思います)
・大量のデータを機関としてもている傾向があること。
に加えて、
・彼らは比較的大きな自分のインフラを持っていること。
　(大学は計算機センターなどを抱えていることが多いと思います。)
という状況がうまくはまっているのかもしれません。

これを少し汎化して、顧客(一般企業、教育団体問わず)のインフラ(オンプレ、クラウド上のVM問わず)にKubeflowのシステム導入から使い方の教育実施までを含めたソリューションはありえると考える。 




以上。

<!--
# Ref
- Deploy on GCP
    - https://deploy.kubeflow.cloud/#/
    - got link above from [here](https://medium.com/kubeflow/kubeflow-v0-5-simplifies-model-development-with-enhanced-ui-and-fairing-library-78e19cdc9f50)

# チュートリアル
- https://eksworkshop.com/kubeflow/
    - From [meeting note 2019-08-27 5:30PM PT](https://docs.google.com/document/d/1Wdxt1xedAj7qF_Rjmxy1R0NRdfv7UWs-r2PItewxHpE/edit#heading=h.5nxloyjb1708)

# その他

- ※MLやSlackからリリースの遅れなどあったか確認する。
- ※Issue,PR,google docsあたりで動向を確認する。

## キーマン
- Jeremy Lewi (jlewi), Google
- Abhishek Gupta (abhi-g), Google


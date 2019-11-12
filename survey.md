---
tags: kubeflow
---

# kubeflow community & release survey

調査日：2019/08/06
Update:2019/11/12

## 調査結果サマリ

- 2019/11/05 に v0.7 がリリースされた。
- v1.0リリースは 2020/01 となっている。(前回から変わらず)
- 現状のKubeflowはデータサイエンティストにとって必ずしも使いやすいものではなく、v1.0リリースを待つ必要がある

v0.7がリリース。リリース予定日にはリリースされなかったが、およそ1週間程度の遅れなのでガバナンスが利いてきていると思われる。
v0.7リリースの主な変更は全体的にv1.0のための準備と明記されていることが多く、v1.0に向けて活動していること、次のリリースはv1.0になりそうであることが色濃くなってきた印象。(今の所v0.8の名言は無い)

v1.0のリリース要件は依然として明確ではなく「Kubeflowを構成するコンポーネントがv1.0になったときにKubeflowもv1.0になる」という基準のまま。時期についても以前と同じく2020/01になると記述がある。
一点だけ、前回調査時(2019/08)からの差分として、Pipelinesに対するマイルストーンがロードマップに明記されており、注目されたコンポーネントであることがわかる。
これまでのリリース時期の傾向から、当初予定から1ヶ月弱は遅れる可能性があるため、2020/02中のリリースが現実的な線だと考える。

機能面でKubeflowの優位性が提供できるようになるには v1.0 のリリースが必須と考えられる。これまでの調査結果と同じであるが、現状ではまだそれぞれのパーツが用意されているだけと考えられ、現状のKubeflowは「データサイエンティストが自分の作業に集中できるようにするもの(データサイエンティストのために一連の操作をブラウザから操作できるようにするという説明が散見される。)」と考えることは難しい。


## リリース日まとめ

| バージョン | 予定 | 実績 | 備考 |
| --- | --- | --- | --- |
| v0.5 | 2019/03末 | 2019/04/09 |  |
| v0.6 | 明示されず | 2019/07/19| v0.5からおよそ3ヶ月後 |
| v0.7 | 2019/10 | [2019/11/05](https://github.com/kubeflow/kubeflow/releases/tag/v0.7.0)  | v0.6からおよそ3ヶ月後。当初予定から若干スライドして11月の頭にリリースされた。 |
| v1.0 | 2020/01 | 未リリース | 当初のロードマップでは2019年後半と書かれていた。※前回調査時から時期は変わらず。 |

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
        - Mitadataとの連携機能
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
### v1.0(未リリース)
- ソース
    - https://github.com/kubeflow/kubeflow/blob/master/ROADMAP.md
    - https://github.com/kubeflow/kubeflow/blob/c6abed891c57338d94c146458662bc14e5c780ea/ROADMAP.md
    - history から差分を調査する。★★
- 予定
    - Pipelinesを始めとする機能の整備が完了している。
- [ref from here](https://github.com/kubeflow/kubeflow/pull/3824)
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
- Kubeflow Contributor Summit 2019
    - https://docs.google.com/document/d/14Jr79aWVjsJg8xq38CLVE4rKRwM1_-gHLuxhGAhrGTI/edit
    - March 12 & 13, 2019
    - サニーベール
- Kubeflow Summit
    - https://github.com/kubeflow/community/wiki/Kubeflow-Summit,-October-2019-Day-1-Agenda
    - Monday, October 28,29
        - from Gmail
    - Kubeflow Summit Day 1
    - Contributor Day on Day 2

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


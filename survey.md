---
tags: kubeflow
---

# kubeflow community & release survey

調査日：2019/08/06

## 調査結果サマリ

- v1.0リリースは 2020/01 に後ろ倒しされている
- 現状のKubeflowはデータサイエンティストにとって必ずしも使いやすいものではなく、v1.0リリースを待つ必要がある

以下、それぞれについて記述する。

前回の調査(昨年度)ではv0.6はksonnetからkustomizeの移行をメインで行うと言われていたため、v0.6での新機能の実装はあまりないと考えていたものの、実際はMetadataコンポーネントやマルチユーザ認証の導入などの機能実装が含まれており、開発は進んでいる印象。

一方で、v0.7という新しいバージョンがロードマップに出てくるなど(前回調査時にはv0.6の次はv1.0と思われた)、予定変更が見られる。そのため、安定版であるv1.0のリリースは遅れる見込みである。
v1.0のリリース要件はあまり明確ではなく「Kubeflowを構成するコンポーネントがv1.0になったときにKubeflowもv1.0になる」という基準である。そのため、そもそも「いつまでにリリースする」という予定ありきではないものの、2019年後半ではないかと当初予想されていた。今回の調査結果では時期がもう少し詳しく書かれており、2020/01になると記述がある。

これまでのリリース時期の傾向から、当初予定から1ヶ月弱は遅れる可能性があるため、2020/02中のリリースが現実的な線だと考える。

機能面でKubeflowの優位性が提供できるようになるには v1.0 のリリースが必須と考えられる。これまでの調査結果と同じであるが、現状ではまだそれぞれのパーツが用意されているだけと考えられ、現状のKubeflowは「データサイエンティストが自分の作業に集中できるようにするもの(データサイエンティストのために一連の操作をブラウザから操作できるようにするという説明が散見される。)」と考えることは難しい。


## リリース日まとめ

| バージョン | 予定 | 実績 | 備考 |
| --- | --- | --- | --- |
| v0.5 | 2019/03末 | 2019/04/09 |  |
| v0.6 | 明示されず | 2019/07/19 | v0.5からおよそ3ヶ月後 |
| v0.7 | 2019/10 | 未リリース | v0.6からおよそ3ヶ月後 |
| v1.0 | 2020/01 | 未リリース | 当初のロードマップでは2019年後半と書かれていた |

- 今後のリリース情報の更新が以下PRで提案されている。
    - https://github.com/kubeflow/kubeflow/pull/3824
    - v0.6やv0.7(今回初めて出てきたリリース番号。)についての明記、v1.0のターゲットの修正が提案されている。
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

### v0.7(未リリース)
- ソース
    - https://github.com/kubeflow/kubeflow/blob/5a8466ff8abbfab67f397bb6104e23c781cdfd69/ROADMAP.md
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

### v1.0(未リリース)
- ソース
    - https://github.com/kubeflow/kubeflow/blob/master/ROADMAP.md
    - https://github.com/kubeflow/kubeflow/blob/5a8466ff8abbfab67f397bb6104e23c781cdfd69/ROADMAP.md
- 予定
    - Pipelinesを始めとする機能の整備が完了している。
- [ref from here](https://github.com/kubeflow/kubeflow/pull/3824)
- We are targeting a 1.0 release in January 2020. Our 1.0 release consists of the following key pieces
  - CUJ(build-train-deployの一連の処理)を実現できるようになっていること。
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


# その他
## コミュニティの状況
- 2回目のコントリビュータサミットを実施している。Googleの人ばかりだが。
https://www.kubeflow.org/docs/about/events/

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
    - 開発参加企業は18。開発参加者は295名。
    -  https://devstats.kubeflow.org/d/7/contributing-companies?orgId=1
- GCP上にKubeflowをデプロイするサイトが存在しており、Kubeflowをオンプレで使おうと考えるユーザが少ないか？
    - https://deploy.kubeflow.cloud/#/

以上。

# Ref
- Deploy on GCP
    - https://deploy.kubeflow.cloud/#/
    - got link above from [here](https://medium.com/kubeflow/kubeflow-v0-5-simplifies-model-development-with-enhanced-ui-and-fairing-library-78e19cdc9f50)

# その他

- ※MLやSlackからリリースの遅れなどあったか確認する。
~~- ※議論している人が限定的かどうか確認する。~~
~~- ※GithubのInsightsあたりでアクティビティを確認する。~~
- ※Issue,PR,google docsあたりで動向を確認する。

## キーマン
- Jeremy Lewi (jlewi), Google
- Abhishek Gupta (abhi-g), Google


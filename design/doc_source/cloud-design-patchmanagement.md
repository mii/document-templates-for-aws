# パッチ管理

## 要件


## OS パッチ
Systems Manager Patch Manager を利用してパッチ適用を自動化する。  
管理対象となるEC2インスタンスに対して以下の設定が必要。  

* SSM Agentをインストール
* 必要な権限が付与されたIAM Roleをアタッチ

本番環境へのパッチ適用は以下のフローを採用する。  

1. 事前定義された or カスタム定義したベースラインをつかって Patch Manager で EC2 をスキャン
2. パッチ適用の要否を検討する
3. 開発検証環境にパッチを適用し動作確認を行う
4. 本番環境へのパッチ適用を計画する
5. 本番管渠へパッチを適用する


## RDS
RDS はメンテナンスという形で OS や DB エンジンバージョンの更新が行われる。  
インスタンス作成時に指定したメンテナンスウィンドウ中にメンテナンスが行われる。  

メンテナンスは以下の種類がある。  
実施タイミングを調整できるメンテナンスは調整して実施、調整できない「必須」のものは AWS が指定するタイミングでのメンテナンスに備える。  

|種類|説明|
|---|---|
|必須|メンテナンスが実行される。延期はできない。|
|利用可能|メンテナンスを手動実行できる。自動的には実行されない。|
|次のウィンドウ|次回のメンテナンスウィンドウ中に適用される。延期が可能。|


# OpenVZ
2025.2 時点では RHEL8/9ベースの独自ディストリビューションに変わった
(従来のようにRHEL/Debianにアドインする形ではない)

## OpenVZの管理コマンド
|コマンド|説明|
|--|--|
|create |コンテナ作成|
|exec/exec2|OS上任意のコマンド実行|
|start/stop|コンテナの起動/停止|
|enter/console|コンテナのセッションに接続|
|status|コンテナの情報|
|restart|コンテナの再起動|
|destroy/delete|コンテナの廃棄</br>他の基盤とdestroyの結果が異なることに注意|


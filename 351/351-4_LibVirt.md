# Libvirt

## virt-**コマンドの例

|コマンド|説明|
|--|--|
|virt-install |メディアから仮想マシンを作成する|
|virt-image|XMLファイルから仮想マシンを作成する|
|virt-clone|仮想マシンを複製する|
|virt-viewer|仮想マシンのGUIコンソールを表示</br>※要X環境|
|virt-manager|仮想マシンのGUI管理ツール</br>※要X環境|

## virsh のサブコマンド
|サブコマンド|説明|
|--|--|
|create|XMLファイルからゲストVMを作成|
|start|ゲストのVMを起動|
|shutdown/destroy|ゲストのVMを停止/強制停止|
|console|ゲストのVMに接続|
|dumpxml|ゲストVMの設定ファイルをXML形式で出力|
|dump|ゲストVMのコアダンプを出力|
|net-edit|ゲストVMのネットワーク設定をXML形式で編集|
|migrate [--live]|ゲストVMを別ホストに移行</br>--live:ライブマイグレーション|

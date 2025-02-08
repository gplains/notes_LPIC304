---
title: Keepalivedの構成サンプル
---
# Keepalivedの構成サンプル

## Keepalivedの最小ネットワーク構成

```
                  ┌──────────────────────────────────┐
                  │          192.168.2.0/24          │
                  │      ┌─────────┬──────────┐      │
                  │      │ 12      │ 13       │ 14   │
    ┌─────────┐   │ ┌────┴───┐ ┌───┴────┐ ┌───┴────┐ │
    │         │   │ │  Node1 │ │ Node2  │ │ Node3  │ │
    │ Console │   │ │   LB   │ │ Server1│ │ Server2│ │
    └────┬────┘   │ └────┬───┘ └────────┘ └────────┘ │
         │ 11     │   12 │                           │
         └────────┼──────┘                           │
 192.168.1.0/24   │          仮想化基盤               │
                  └──────────────────────────────────┘
```

## 作業手順

- 予めCentOS7 でminimal構成を構築し、それぞれnode1..node3とする
- node2、node3 にそれぞれhttpd を構築する
  ```
  yum install -y httpd ; systemctl enable httpd
  ```
- node1にてipvsadm と keepalived をインストールする
  ```
  yum install ipvsadm keepalived
  echo 'net.ipv4.ip_forward = 1' >> /etc/sysctl.conf
  systemctl enable ipvsadm keepalived
  ```
- Node1のコンソールで、以下の順にコマンドを実行する
  ```
  touch /etc/sysconfig/ipvsadm 
  systemctl start ipvsadm 
  ipvsadm -C ; ipvsadm –S   # テーブル初期化
  ipvsadm -A -t 192.168.1.12:80 -s wlc
  ipvsadm -a -t 192.168.1.12:80 -r 192.168.2.13:80 –m
  ipvsadm -a -t 192.168.1.12:80 -r 192.168.2.14:80 –m
  ipvsadm -S ; ipvsadm -ln # テーブルの確認
  ```
- curl http://192.168.1.12 の実行時に、Node2/Node3が表示される

## ipvsadm のサブコマンド

|サブコマンド|説明|
|---|---|
|A --add-service|仮想サーバの追加|
|a --add-server|仮想サーバのリアルサーバ(下位サーバ)定義追加|
|D --delete-service|仮想サーバの削除(下位サーバごと削除)|
|d --delete-server|仮想サーバのリアルサーバ定義削除|
|E --edit-service|仮想サーバの編集|
|e --edit-server|仮想サーバのリアルサーバ定義編集|
|--start-daemon|接続同期デーモンを起動|
|--stop-daemon|接続同期デーモンを停止|

## keepalivedのスケジューリングアルゴリズム

|記号|説明|
|---|---|
|rr / wrr|ラウンドロビン<br/>(wrrは重みつきラウンドロビン)|
|lc/wlc|最小コネクション<br/>(wlcは重みつき最小コネクション)<br/>※未指定の場合、wlc が選択される|
|lblc|ローカリティベース<br/>最小コネクション|
|lblcr|ローカリティベースレプリケーションつき<br/>最小コネクション|
|dh|宛先ハッシュ(宛先IPアドレス基準)|
|sh|送信元ハッシュ(送信元IPアドレス基準)|
|sed|最小遅延予測|
|nq|キューなしを優先、埋まっていれば最小遅延予測|


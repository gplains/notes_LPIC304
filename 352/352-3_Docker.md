
### Docker/Podman のインストール


- RHEL/Alma/Rocky
  
  ```
  sudo yum install -y yum-utils
  sudo yum-config-manager --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
  sudo yum install docker-ce docker-ce-cli containerd.io
  sudo systemctl start docker
  ```
    dnf install podman # podman

- Ubuntu

  apt install docker  #docker
  apt install podman podman-docker # podman

## Dockerの管理コマンド
サブコマンド|説明|
|--|--|
|build|イメージ作成|
|start/stop|コンテナ起動/停止|
|run|コンテナ作成＋実行|
|attach|起動中のコンテナに接続|
|rm|コンテナを削除|
|rmi|コンテナイメージを削除|
|pull/push|DockerHubからイメージを受信/送信|

## 用語
- dockerd
- /etc/docker/daemon.json
- /var/lib/docker/
- docker
- Dockerfile

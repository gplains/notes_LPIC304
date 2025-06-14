
### DevStack

- OpenStack を小規模でデプロイするキット

  https://docs.openstack.org/devstack/latest/

### MicroStack

- Sumbeamベースの小規模なOpenStack

  https://canonical.com/microstack

  ```
  sudo snap install openstack --channel 2024.1/beta
  sunbeam prepare-node-script | bash -x && newgrp snap_daemon
  sunbeam cluster bootstrap --accept-defaults
  sunbeam configure --accept-defaults --openrc demo-openrc
  sunbeam launch ubuntu --name test
  ```

  
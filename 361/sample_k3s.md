---
title: K3Sの構成サンプル
---
# K3Sの構成サンプル

## K3Sの最小ネットワーク構成


```
                   ┌──────────────────────────────────┐
                   │             10.x.y.z/24          │
                   │      ┌─────────┬──────────┐      │
                   │      │ L       │ M        │ N    │
     ┌─────────┐   │ ┌────┴───┐ ┌───┴────┐ ┌───┴────┐ │
     │         │   │ │  master│ │ Worker1│ │ Worker2│ │
     │ Console │   │ │        │ │        │ │        │ │
     └────┬────┘   │ └────┬───┘ └───┬────┘ └───┬────┘ │
          │ 11     │      │ 131     │132       │133   │
          └────────┼──────┴─────────┴──────────┘      │
  192.168.1.0/24   │                                  │
                   └──────────────────────────────────┘

```


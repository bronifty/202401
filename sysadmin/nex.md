
- [agent](https://github.com/synadia-io/nex/blob/main/agent) - kubelet
- [fc-image](https://github.com/synadia-io/nex/blob/main/agent/fc-image) -  container runtime (containerd)
- [node](https://github.com/synadia-io/nex/blob/main/internal/node) - control plane / kube-controller-manager and kube-scheduler
- [nex](https://github.com/synadia-io/nex/blob/main/nex) - kubectl / cli








Install NATS Server
```bash
curl -L https://github.com/nats-io/nats-server/releases/download/v2.10.9/nats-server-v2.10.9-linux-amd64.zip -o nats-server.zip

unzip nats-server.zip -d nats-server

sudo cp nats-server/nats-server-v2.10.9-linux-amd64/nats-server /usr/bin

curl -fsSL https://github.com/nats-io/natscli/releases/download/v0.1.1/nats-0.1.1-amd64.deb 
```



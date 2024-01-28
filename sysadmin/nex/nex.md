
- [agent](https://github.com/synadia-io/nex/blob/main/agent) - kubelet
- [fc-image](https://github.com/synadia-io/nex/blob/main/agent/fc-image) -  container runtime (containerd)
- [node](https://github.com/synadia-io/nex/blob/main/internal/node) - control plane / kube-controller-manager and kube-scheduler
- [nex](https://github.com/synadia-io/nex/blob/main/nex) - kubectl / cli








Install NATS Server and Golang
```bash
NATS_SERVER_VERSION="2.10.9"

# update image and install unzip
apt update && apt install unzip
#download nats-server unzip and cp to /usr/local/bin
curl -L https://github.com/nats-io/nats-server/releases/download/v"${NATS_SERVER_VERSION}"/nats-server-v"${NATS_SERVER_VERSION}"-linux-amd64.zip -o nats-server.zip
unzip nats-server.zip -d nats-server
sudo cp nats-server/nats-server-v"${NATS_SERVER_VERSION}"-linux-amd64/nats-server /usr/local/bin

curl -fsSL https://github.com/nats-io/natscli/releases/download/v0.1.1/nats-0.1.1-amd64.deb 
```



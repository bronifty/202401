
- [agent](https://github.com/synadia-io/nex/blob/main/agent) - kubelet
- [fc-image](https://github.com/synadia-io/nex/blob/main/agent/fc-image) -  container runtime (containerd)
- [node](https://github.com/synadia-io/nex/blob/main/internal/node) - control plane / kube-controller-manager and kube-scheduler
- [nex](https://github.com/synadia-io/nex/blob/main/nex) - kubectl / cli








Install NATS Server and Golang
```bash
#!/bin/bash
# bash variables
NATS_SERVER_VERSION="2.10.9"
NATS_CLI_VERSION="0.1.1"
GOLANG_VERSION="1.21.6"

# update image and install unzip
apt update && apt install unzip

#download nats-server unzip and cp to /usr/local/bin
curl -L https://github.com/nats-io/nats-server/releases/download/v"${NATS_SERVER_VERSION}"/nats-server-v"${NATS_SERVER_VERSION}"-linux-amd64.zip -o nats-server.zip
unzip nats-server.zip -d nats-server
sudo cp nats-server/nats-server-v"${NATS_SERVER_VERSION}"-linux-amd64/nats-server /usr/local/bin

# download and install nats client
curl -fsSL -o nats-cli.deb https://github.com/nats-io/natscli/releases/download/v"${NATS_CLI_VERSION}"/nats-"${NATS_CLI_VERSION}"-amd64.deb 
dpkg -i nats-cli.deb

# download and install go
curl -fsSL -o go"${GOLANG_VERSION}".linux-amd64.tar.gz https://go.dev/dl/go"${GOLANG_VERSION}".linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go"${GOLANG_VERSION}".linux-amd64.tar.gz

# add go to the path
cp ~/.bashrc ~/.bashrc.backup
{
echo ""
echo "export PATH=\$PATH:/usr/local/go/bin"
echo ""
} >> ~/.bashrc
source ~/.bashrc


```



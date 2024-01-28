



Install NATS Server
```bash
curl -L https://github.com/nats-io/nats-server/releases/download/v2.10.9/nats-server-v2.10.9-linux-amd64.zip -o nats-server.zip

unzip nats-server.zip -d nats-server

sudo cp nats-server/nats-server-v2.10.9-linux-amd64/nats-server /usr/bin

curl -fsSL https://github.com/nats-io/natscli/releases/download/v0.1.1/nats-0.1.1-amd64.deb 
```
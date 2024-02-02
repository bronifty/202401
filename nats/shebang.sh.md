
```bash
#!/bin/bash
# bash variables
export NATS_SERVER_VERSION="2.10.9"
export NATS_CLI_VERSION="0.1.1"
export GOLANG_VERSION="1.21.6"
export ARCH="$(uname -m)"

rm -rf $(dirname $(which nats-server))
rm -rf $(dirname $(which nats))
rm -rf $(dirname $(which go))


# Update and install necessary packages without interactive prompts
sudo DEBIAN_FRONTEND=noninteractive apt-get update -y && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y git unzip wget lsof build-essential gnupg software-properties-common python3-pip snapd

# setup github and ssh key (automatically without user interaction, using default file location, no passphrase)
git config --global user.name "bronifty"
git config --global user.email "bronifty@gmail.com"
echo -e "\n\n\n" | sudo ssh-keygen -t rsa -b 4096 -C "bronifty@gmail.com" -N ""

# terraform setup
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y terraform

# Add utility method for github
echo 'alias gitpushmain="git branch -M main && git add . && git commit -am '\''this'\'' && git push -u origin main"' >> ~/.bashrc

# Download and install nats-server
curl -L "https://github.com/nats-io/nats-server/releases/download/v${NATS_SERVER_VERSION}/nats-server-v${NATS_SERVER_VERSION}-linux-amd64.zip" -o nats-server.zip
sleep 5
sudo unzip -o nats-server.zip -d nats-server-dir
sudo cp nats-server-dir/nats-server-v"${NATS_SERVER_VERSION}"-linux-amd64/nats-server /usr/local/bin/
sudo rm -rf nats-server.zip nats-server-dir

# Download and install nats client
curl -fsSL -o nats-cli.deb "https://github.com/nats-io/natscli/releases/download/v${NATS_CLI_VERSION}/nats-${NATS_CLI_VERSION}-amd64.deb"
sudo dpkg -i nats-cli.deb
sudo rm nats-cli.deb

# Download and install Go
curl -fsSL -o go"${GOLANG_VERSION}".linux-amd64.tar.gz "https://go.dev/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go && tar -C /usr/local -xzf go"${GOLANG_VERSION}".linux-amd64.tar.gz
sudo rm go"${GOLANG_VERSION}".linux-amd64.tar.gz

# Set Go path
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc

# # Install fnm, rust, snapd services, git-lfs, and aws cli without user interaction
# curl -fsSL https://fnm.vercel.app/install | bash
# curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
# sudo systemctl enable snapd && sudo systemctl start snapd
# curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
# sudo DEBIAN_FRONTEND=noninteractive apt-get install -y git-lfs=3.4.0
# curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip && sudo ./aws/install



```
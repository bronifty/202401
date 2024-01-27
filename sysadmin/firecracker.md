propaganda:
everything you can do with containers plus multi-tenant isolation? - eg lambda functions
- multitenant containers
- dense utilization 
- efficient use of hardware resources

### Host
equinix metal - https://console.equinix.com/projects/e8a820c1-30fe-41ea-8afd-39a618b148a6
- log in and create an on-demand metal instance with ssh key
- clone firecracker repo
```bash
git clone https://github.com/firecracker-microvm/firecracker.git firecracker-repo
```

### Getting Started
https://github.com/firecracker-microvm/firecracker/blob/main/docs/getting-started.md
- check the host env to make sure it can run firecracker
	- this command is at the root of the firecracker github repo we downloaded in prev step
```bash
firecracker-repo/tools/devtool checkenv
```
- check ACLs to KVM
```bash
[ $(stat -c "%G" /dev/kvm) = kvm ] && sudo usermod -aG kvm ${USER} \
&& echo "Access granted."
```
- check privs on /dev/kvm
```bash
[ -r /dev/kvm ] && [ -w /dev/kvm ] && echo "OK" || echo "FAIL"
```

- download the kernel and rootfs
```bash
ARCH="$(uname -m)"

# Download a linux kernel binary
wget https://s3.amazonaws.com/spec.ccfc.min/firecracker-ci/v1.7/${ARCH}/vmlinux-5.10.204

# Download a rootfs
wget https://s3.amazonaws.com/spec.ccfc.min/firecracker-ci/v1.7/${ARCH}/ubuntu-22.04.ext4

# Download the ssh key for the rootfs
wget https://s3.amazonaws.com/spec.ccfc.min/firecracker-ci/v1.7/${ARCH}/ubuntu-22.04.id_rsa

# Set user read permission on the ssh key
chmod 400 ./ubuntu-22.04.id_rsa
```

- download latest firecracker binary 
```bash
ARCH="$(uname -m)"
release_url="https://github.com/firecracker-microvm/firecracker/releases"
latest=$(basename $(curl -fsSLI -o /dev/null -w  %{url_effective} ${release_url}/latest))
curl -L ${release_url}/download/${latest}/firecracker-${latest}-${ARCH}.tgz \
| tar -xz

# Rename the binary to "firecracker"
mv release-${latest}-$(uname -m)/firecracker-${latest}-${ARCH} firecracker
```



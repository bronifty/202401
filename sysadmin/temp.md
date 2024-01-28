- reset script
```bash

API_SOCKET="/tmp/firecracker.socket"
# Remove API unix socket
sudo rm -f $API_SOCKET
# Run firecracker
sudo ./firecracker --api-sock "${API_SOCKET}"

```


```bash


TAP_DEV="tap0"
TAP_IP="172.16.0.1"
MASK_SHORT="/30"

# Setup network interface
sudo ip link del "$TAP_DEV" 2> /dev/null || true
sudo ip tuntap add dev "$TAP_DEV" mode tap
sudo ip addr add "${TAP_IP}${MASK_SHORT}" dev "$TAP_DEV"
sudo ip link set dev "$TAP_DEV" up

# Enable ip forwarding
sudo sh -c "echo 1 > /proc/sys/net/ipv4/ip_forward"

HOST_IFACE="eth0"

# Set up microVM internet access
sudo iptables -t nat -D POSTROUTING -o "$HOST_IFACE" -j MASQUERADE || true
sudo iptables -D FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT \
    || true
sudo iptables -D FORWARD -i tap0 -o "$HOST_IFACE" -j ACCEPT || true
sudo iptables -t nat -A POSTROUTING -o "$HOST_IFACE" -j MASQUERADE
sudo iptables -I FORWARD 1 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
sudo iptables -I FORWARD 1 -i tap0 -o "$HOST_IFACE" -j ACCEPT

# The IP address of a guest is derived from its MAC address with
# `fcnet-setup.sh`, this has been pre-configured in the guest rootfs. It is
# important that `TAP_IP` and `FC_MAC` match this.
FC_MAC="06:00:AC:10:00:02"

# Set network interface
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/network-interfaces/net1' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d "{
        \"iface_id\": \"net1\",
        \"guest_mac\": \"$FC_MAC\",
        \"host_dev_name\": \"$TAP_DEV\"
    }" \
    
# log file
LOGFILE="./firecracker.log"
rm $LOGFILE
touch $LOGFILE
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/logger' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d "{
        \"log_path\": \"${LOGFILE}\",
        \"level\": \"Debug\",
        \"show_level\": true,
        \"show_log_origin\": true
    }"
    
# boot source
kernel_path=$(pwd)"/vmlinux-5.10.204"
curl --unix-socket /tmp/firecracker.socket -i \
	-X PUT 'http://localhost/boot-source' \
	-H 'Accept: application/json' \
	-H 'Content-Type: application/json' \
	-d "{
		\"kernel_image_path\": \"${kernel_path}\",
		\"boot_args\": \"console=ttyS0 reboot=k panic=1 pci=off\"
	}"


# rootfs
rootfs_path=$(pwd)"/ubuntu-22.04.ext4"
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/drives/rootfs' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d "{
	\"drive_id\": \"rootfs\",
	\"path_on_host\": \"${rootfs_path}\",
	\"is_root_device\": true,
	\"is_read_only\": false
}"

# set, before `InstanceStart`.
sleep 0.015s

# start firecracker
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/actions' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{
	"action_type": "InstanceStart"
}'


# API requests are handled asynchronously, it is important the microVM has been
# started before we attempt to SSH into it.
sleep 0.015s

# SSH into the microVM
ssh -i ./ubuntu-22.04.id_rsa root@172.16.0.2

# Use `root` for both the login and password.
# Run `reboot` to exit.
```



- manually set boot source
```bash
kernel_path=$(pwd)"/vmlinux-5.10.204"

curl --unix-socket /tmp/firecracker.socket -i \
	-X PUT 'http://localhost/boot-source' \
	-H 'Accept: application/json' \
	-H 'Content-Type: application/json' \
	-d "{
		\"kernel_image_path\": \"${kernel_path}\",
		\"boot_args\": \"console=ttyS0 reboot=k panic=1 pci=off\"
	}"
```

- manually set boot filesystem
```bash
rootfs_path=$(pwd)"/ubuntu-22.04.ext4"
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/drives/rootfs' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d "{
	\"drive_id\": \"rootfs\",
	\"path_on_host\": \"${rootfs_path}\",
	\"is_root_device\": true,
	\"is_read_only\": false
}"
```

- manually start firecracker
```bash
curl --unix-socket /tmp/firecracker.socket -i \
-X PUT 'http://localhost/actions' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{
	"action_type": "InstanceStart"
}'
```

```bash

# firecrackerapi.sh
API_SOCKET="/tmp/firecracker.socket"
# Remove API unix socket
sudo rm -f $API_SOCKET
# Run firecracker
firecracker --api-sock "${API_SOCKET}"

```
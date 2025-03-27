![Uploading Screenshot 2025-03-27 105128.png…]()


### 0GLABS-DA-CLIENT
<hr>

### Hardware Requirement
• RAM: 8 GB <br>
• CPU: 2 cores <br>
• Bandwidth: 100 MBps for Download / Upload <br>
<hr>

### 1. Install Docker
```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce
```
<hr>

### 2. Clone the DA Client Node Repo
```
git clone https://github.com/0glabs/0g-da-client.git
```
<hr>

### 3. Build the Docker Image:
```
cd 0g-da-client
docker build -t 0g-da-client -f combined.Dockerfile .
```
<hr>

### 4. Set Environment Variables
Create a file named `envfile.env` with the following content. Be sure you paste in your private key.
```
nano envfile.env
```
<hr>

### Copas this
```
COMBINED_SERVER_CHAIN_RPC=https://evmrpc-testnet.0g.ai
COMBINED_SERVER_PRIVATE_KEY=YOUR_PRIVATE_KEY
ENTRANCE_CONTRACT_ADDR=0x857C0A28A8634614BB2C96039Cf4a20AFF709Aa9

COMBINED_SERVER_RECEIPT_POLLING_ROUNDS=180
COMBINED_SERVER_RECEIPT_POLLING_INTERVAL=1s
COMBINED_SERVER_TX_GAS_LIMIT=2000000
COMBINED_SERVER_USE_MEMORY_DB=true
COMBINED_SERVER_KV_DB_PATH=/runtime/
COMBINED_SERVER_TimeToExpire=2592000
DISPERSER_SERVER_GRPC_PORT=51001
BATCHER_DASIGNERS_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001000
BATCHER_FINALIZER_INTERVAL=20s
BATCHER_CONFIRMER_NUM=3
BATCHER_MAX_NUM_RETRIES_PER_BLOB=3
BATCHER_FINALIZED_BLOCK_COUNT=50
BATCHER_BATCH_SIZE_LIMIT=500
BATCHER_ENCODING_INTERVAL=3s
BATCHER_ENCODING_REQUEST_QUEUE_SIZE=1
BATCHER_PULL_INTERVAL=10s
BATCHER_SIGNING_INTERVAL=3s
BATCHER_SIGNED_PULL_INTERVAL=20s
BATCHER_EXPIRATION_POLL_INTERVAL=3600
BATCHER_ENCODER_ADDRESS=DA_ENCODER_SERVER
BATCHER_ENCODING_TIMEOUT=300s
BATCHER_SIGNING_TIMEOUT=60s
BATCHER_CHAIN_READ_TIMEOUT=12s
BATCHER_CHAIN_WRITE_TIMEOUT=13s
```
### Note: <br>
### Change COMBINED_SERVER_PRIVATE_KEY=YOUR_PRIVATE_KEY
<hr>

### 5. Run Docker Node:
```
docker run -d --env-file envfile.env --name 0g-da-client -v ./run:/runtime -p 51001:51001 0g-da-client combined
```
<hr>

### 6. Check Logs:
```
docker logs -f 0g-da-client
```
<hr>

![Screenshot 2025-03-27 103103](https://github.com/user-attachments/assets/77c6bc63-be4c-49ad-b218-57aff55d51ed)

### ✅ Done!
<hr>

# DYNAX - Decentralized Layer 1 Blockchain

DYNAX is a fully decentralized Layer 1 blockchain with native smart contract support (DVM), built entirely from a single mobile phone with no corporate backing, no VC funding, and no central point of control.

> Public Testnet - Coins have no real value. Chain may reset during active development.

## Current Status

| Metric | Value |
|--------|-------|
| Blocks | 10,200+ |
| Consensus | Proof-of-Work (SHA3-256) |
| Max Supply | 11,000,000 DYX |
| Smart Contracts | DVM enabled |
| Network Access | Cloudflare Tunnel + Tor .onion (censorship-resistant) |

## Access the Network

- Website: https://redmi605900.github.io/dynax-website/
- Tor Hidden Service (no intermediary, works even if the web frontend is down):
  http://wjk6bqzdt6tto52jaacmkdtohjaf3s3re3zv4bjfmtjy67t24amwsyid.onion

## Run Your Own Node

Anyone can run a DYNAX node and join the network. There is no permission needed - this is the point.

### Requirements
- Python 3.9+
- pip

### 1. Clone the repository

    git clone https://github.com/Redmi605900/dynax-node.git
    cd dynax-node

### 2. Install dependencies

    pip install -r requirements.txt

If you want to connect via Tor (recommended for censorship resistance), also install and run Tor:

    # Debian/Ubuntu
    sudo apt install tor
    # Termux (Android)
    pkg install tor

Tor's default SOCKS proxy (127.0.0.1:9050) must be running for .onion peers to work. The node auto-detects .onion addresses and routes them through Tor automatically - no extra config needed.

### 3. Configure environment variables

| Variable | Required | Description |
|----------|----------|--------------|
| PORT | No (default 6001) | Port the node listens on |
| BOOTSTRAP_NODE | Recommended | The peer to connect to first. Use the .onion address above, or https://dynax-node.onrender.com |
| MY_URL | Recommended | Your own node's public URL, announced to the bootstrap peer |
| MINER_ADDRESS | Optional | Your wallet address to receive mining rewards |
| P2P_SECRET | No - leave default | Shared network secret. Do not change this - it must match the rest of the network (dynax_network_1337) |

### 4. Start the node

    BOOTSTRAP_NODE="http://wjk6bqzdt6tto52jaacmkdtohjaf3s3re3zv4bjfmtjy67t24amwsyid.onion" \
    MY_URL="https://your-node-url.example.com" \
    python3 dynax_node_v20.py

On first run, your node creates its own genesis block, connects to the bootstrap peer, and syncs the full chain automatically. No one needs to hand you a chain file - this is how a decentralized network is supposed to work.

### 5. Verify it worked

    curl http://127.0.0.1:6001/chain | python3 -c "import sys,json; print(len(json.load(sys.stdin)), 'blocks synced')"

## Key API Endpoints

| Endpoint | Description |
|----------|--------------|
| GET /chain | Full blockchain |
| GET /stats | Network summary |
| GET /peers | Connected peers |
| POST /peers/add | Add a peer manually |
| GET /sync | Force sync with peers |
| GET /dvm/contracts | List deployed smart contracts |
| POST /dvm/deploy | Deploy a new contract |
| POST /dvm/execute | Execute a contract method |
| GET /events/logs | Contract event logs |
| GET /health | Node health diagnostics |

## Technology

- Consensus: Proof-of-Work, SHA3-256, adjustable difficulty
- Signing: ECDSA (secp256k1)
- Smart Contracts: DYNAX Virtual Machine (DVM), custom
- P2P: HTTP-based peer gossip, HMAC-signed messages, Tor .onion support
- Backend: Python, Flask

## Roadmap

- [x] Blockchain core (PoW, ECDSA, validation)
- [x] Smart contract DVM
- [x] Web platform (wallet, explorer, faucet, DEX)
- [x] Tor .onion peer support - no single point of failure
- [ ] Multi-node network with independent operators
- [ ] Mining pool
- [ ] Mobile wallet app
- [ ] Governance system

## Why This Matters

Most "Layer 1" projects today run on corporate cloud infrastructure with a company behind them that can be pressured, sued, or shut down. DYNAX started as one person mining on a single Android phone. Every node that joins - yours included - makes it harder to censor and impossible to fully shut down. That's the whole point.

## License

MIT License

---

Built with love for the decentralized future - no intermediaries, no permission required.

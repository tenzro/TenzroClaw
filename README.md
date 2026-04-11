# TenzroClaw

[![License](https://img.shields.io/badge/license-Apache--2.0-green)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8+-blue)](https://python.org)
[![Tests](https://img.shields.io/badge/tests-87%20passed-brightgreen)]()

The official [OpenClaw](https://github.com/anthropics/openclaw) skill for interacting with [Tenzro Network](https://tenzro.com) — a full blockchain RPC toolkit for AI agents.

## Overview

TenzroClaw gives AI agents direct access to 185+ Tenzro blockchain operations through a single Python script. Agents can create wallets, send transactions, manage identities, trade on marketplaces, deploy contracts, bridge tokens, and more.

**Live testnet:** `https://rpc.tenzro.network`

## Quick Start

```bash
# Check node status
python3 tools/tenzro_rpc.py node_status

# Create a wallet
python3 tools/tenzro_rpc.py create_wallet

# Get block height
python3 tools/tenzro_rpc.py get_block_number

# Register an identity
python3 tools/tenzro_rpc.py register_identity human Alice

# List AI models
python3 tools/tenzro_rpc.py list_models

# List tokens
python3 tools/tenzro_rpc.py list_tokens

# Join as a MicroNode
python3 tools/tenzro_rpc.py join Alice
```

## Installation

No installation required. Just clone and run:

```bash
git clone https://github.com/tenzro/TenzroClaw.git
cd TenzroClaw
python3 tools/tenzro_rpc.py --help
```

Optional: install `requests` for better HTTP handling (falls back to `urllib` if not available):

```bash
pip install requests
```

## Configuration

Set environment variables to override defaults:

```bash
export TENZRO_RPC_URL=https://rpc.tenzro.network    # JSON-RPC endpoint
export TENZRO_API_URL=https://api.tenzro.network     # Web API endpoint
export TENZRO_RPC_TIMEOUT=120                         # Request timeout (seconds)
```

## Capabilities (185 commands)

### Wallet & Transactions
`create_wallet`, `get_balance`, `send_transaction`, `create_account`, `list_accounts`

### Identity (TDIP)
`register_identity`, `resolve_did`, `set_username`, `resolve_username`, `import_identity`, `list_identities`

### AI Models & Inference
`list_models`, `chat`, `inference_request`, `serve_model`, `stop_model`, `download_model`, `list_model_endpoints`

### Token Registry
`create_token`, `list_tokens`, `get_token_info`, `get_token_balance`, `wrap_tnzo`, `cross_vm_transfer`, `deploy_contract`

### Task & Agent Marketplace
`list_tasks`, `post_task`, `get_task`, `cancel_task`, `list_agent_templates`, `register_agent_template`, `spawn_agent_template`

### Staking & Governance
`stake`, `unstake`, `list_proposals`, `vote`, `get_voting_power`, `register_provider`

### Settlement & Payments
`settle`, `get_settlement`, `create_escrow`, `release_escrow`, `open_payment_channel`, `pay_mpp`, `pay_x402`

### Network & Node
`node_status`, `node_info`, `get_block_number`, `get_block`, `peer_count`, `syncing`

### EVM Compatibility
`eth_block_number`, `eth_get_balance`, `eth_call`, `eth_estimate_gas`, `eth_get_transaction_receipt`, `eth_get_logs`

See [SKILL.md](SKILL.md) for the complete reference with all 185 commands and curl examples.

## Using with OpenClaw

Add to your OpenClaw agent configuration:

```yaml
skills:
  - name: tenzroclaw
    source: github.com/tenzro/TenzroClaw
    tools:
      - tools/tenzro_rpc.py
```

## Tests

```bash
python3 -m unittest tools/test_tenzro_rpc.py -v
```

87 tests covering wallet, identity, verification, tokens, marketplace, staking, and more.

## Architecture

```
Your Agent
    |
    |-- python3 tenzro_rpc.py <command> [args...]
    |
    v
tenzro_rpc.py
    |
    |-- JSON-RPC POST --> rpc.tenzro.network (blockchain operations)
    |-- HTTP POST/GET --> api.tenzro.network (verification, faucet)
    |
    v
Tenzro Network (decentralized)
```

## Related

| Resource | URL |
|----------|-----|
| Tenzro Network | [tenzro.com](https://tenzro.com) |
| MCP Server | [github.com/tenzro/tenzro-mcp-server](https://github.com/tenzro/tenzro-mcp-server) |
| A2A Server | [github.com/tenzro/tenzro-a2a-server](https://github.com/tenzro/tenzro-a2a-server) |
| JSON-RPC | `https://rpc.tenzro.network` |
| Web API | `https://api.tenzro.network` |

## Contact

- Website: [tenzro.com](https://tenzro.com)
- Engineering: [eng@tenzro.com](mailto:eng@tenzro.com)
- GitHub: [github.com/tenzro](https://github.com/tenzro)

## License

Apache 2.0. See [LICENSE](LICENSE).

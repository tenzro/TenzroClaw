# TenzroClaw

[![License](https://img.shields.io/badge/license-Apache--2.0-green)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8+-blue)](https://python.org)
[![Tests](https://img.shields.io/badge/tests-87%20passed-brightgreen)]()

The official [OpenClaw](https://github.com/anthropics/openclaw) skill for interacting with [Tenzro Network](https://tenzro.com) — a full blockchain + multi-chain toolkit for AI agents.

## Overview

TenzroClaw gives AI agents direct access to **303 commands** across the Tenzro blockchain and 5 ecosystem chains (Solana, Ethereum, LayerZero, Chainlink, Canton) through a single Python script. Agents can create wallets, send transactions, manage identities, trade on marketplaces, deploy contracts, bridge tokens, swap on Jupiter/1inch, read Chainlink price feeds, and more.

**Live testnet:** `https://rpc.tenzro.network`

## Quick Start

```bash
# Tenzro blockchain
python3 tools/tenzro_rpc.py node_status
python3 tools/tenzro_rpc.py create_wallet
python3 tools/tenzro_rpc.py register_identity human Alice
python3 tools/tenzro_rpc.py list_models
python3 tools/tenzro_rpc.py join Alice

# Onboarding keys
python3 tools/tenzro_rpc.py issue_onboarding_key "my-agent" did:tenzro:machine:... 0xaddress machine
python3 tools/tenzro_rpc.py list_onboarding_keys
python3 tools/tenzro_rpc.py validate_onboarding_key tenzro_...
python3 tools/tenzro_rpc.py revoke_onboarding_key did:tenzro:machine:...

# Solana
python3 tools/tenzro_rpc.py solana_get_slot
python3 tools/tenzro_rpc.py solana_get_tps
python3 tools/tenzro_rpc.py solana_resolve_domain toly.sol

# Ethereum
python3 tools/tenzro_rpc.py eth_get_gas_price_ext
python3 tools/tenzro_rpc.py eth_resolve_ens vitalik.eth
python3 tools/tenzro_rpc.py chainlink_get_price ETH/USD

# LayerZero
python3 tools/tenzro_rpc.py lz_list_chains
python3 tools/tenzro_rpc.py lz_list_dvns

# Chainlink
python3 tools/tenzro_rpc.py chainlink_list_feeds
python3 tools/tenzro_rpc.py ccip_get_supported_chains
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

```bash
# Tenzro endpoints
export TENZRO_RPC_URL=https://rpc.tenzro.network
export TENZRO_API_URL=https://api.tenzro.network
export TENZRO_RPC_TIMEOUT=120

# Ecosystem MCP endpoints (optional — defaults to live testnet)
export SOLANA_MCP_URL=https://solana-mcp.tenzro.network/mcp
export ETHEREUM_MCP_URL=https://ethereum-mcp.tenzro.network/mcp
export LAYERZERO_MCP_URL=https://layerzero-mcp.tenzro.network/mcp
export CHAINLINK_MCP_URL=https://chainlink-mcp.tenzro.network/mcp
export CANTON_MCP_URL=https://canton-mcp.tenzro.network/mcp
```

## Capabilities (303 commands)

### Tenzro Blockchain (231 commands)

#### Wallet & Transactions
`create_wallet`, `get_balance`, `send_transaction`, `create_account`, `list_accounts`

#### Identity (TDIP)
`register_identity`, `resolve_did`, `set_username`, `resolve_username`, `import_identity`, `list_identities`

#### AI Models & Inference
`list_models`, `chat`, `inference_request`, `serve_model`, `stop_model`, `download_model`, `list_model_endpoints`

#### Token Registry
`create_token`, `list_tokens`, `get_token_info`, `get_token_balance`, `wrap_tnzo`, `cross_vm_transfer`, `deploy_contract`

#### NFTs
`create_nft_collection`, `mint_nft`, `transfer_nft`, `get_nft_info`, `list_nft_collections`

#### Task & Agent Marketplace
`list_tasks`, `post_task`, `get_task`, `cancel_task`, `list_agent_templates`, `register_agent_template`, `spawn_agent_template`

#### Staking & Governance
`stake`, `unstake`, `list_proposals`, `vote`, `get_voting_power`, `register_provider`

#### Settlement & Payments
`settle`, `get_settlement`, `create_escrow`, `release_escrow`, `open_payment_channel`, `pay_mpp`, `pay_x402`

#### Onboarding Keys
`issue_onboarding_key`, `list_onboarding_keys`, `revoke_onboarding_key`, `validate_onboarding_key`

#### Bridge & Cross-Chain
`bridge_tokens`, `bridge_quote`, `get_bridge_routes`, `list_bridge_adapters`, `crosschain_mint`, `crosschain_burn`

#### deBridge (5 commands)
`debridge_search_tokens`, `debridge_get_chains`, `debridge_get_instructions`, `debridge_create_tx`, `debridge_same_chain_swap`

#### Compliance
`check_compliance`, `register_compliance`, `freeze_address`

#### Events
`get_events`, `subscribe_events`, `register_webhook`

#### Network & Node
`node_status`, `node_info`, `get_block_number`, `get_block`, `peer_count`, `syncing`

#### Cryptography
`sign_message`, `verify_signature`, `encrypt_data`, `decrypt_data`, `derive_key`, `generate_keypair`, `hash_sha256`, `hash_keccak256`, `x25519_key_exchange`, `generate_vrf_proof`, `verify_vrf_proof` (RFC 9381 ECVRF-EDWARDS25519-SHA512-TAI)

#### TEE Security
`detect_tee`, `get_tee_attestation`, `verify_tee_attestation`, `seal_data`, `unseal_data`, `list_tee_providers`

#### ZK Proofs
`create_zk_proof`, `generate_proving_key`, `list_zk_circuits`

#### Key Custody
`create_mpc_wallet`, `export_keystore`, `import_keystore`, `get_key_shares`, `rotate_keys`, `set_spending_limits`, `get_spending_limits`, `authorize_session`, `revoke_session`

#### App/Paymaster
`register_app`, `create_user_wallet`, `fund_user_wallet`, `list_user_wallets`, `sponsor_transaction`, `get_usage_stats`

#### Contract ABI
`encode_function`, `decode_result`

#### Streaming
`chat_stream`, `subscribe_events_stream`

#### EVM Compatibility
`eth_block_number`, `eth_get_balance`, `eth_call`, `eth_estimate_gas`, `eth_get_transaction_receipt`, `eth_get_logs`

### Solana (14 commands)
`solana_swap`, `solana_get_price`, `solana_stake`, `solana_get_yield`, `solana_get_balance`, `solana_get_token_accounts`, `solana_transfer`, `solana_get_token_info`, `solana_get_nft`, `solana_get_nfts_by_owner`, `solana_get_slot`, `solana_get_tps`, `solana_get_transaction`, `solana_resolve_domain`

### Ethereum (16 commands)
`eth_get_price_chainlink`, `eth_get_gas_price_ext`, `eth_estimate_gas_ext`, `eth_get_fee_history`, `eth_get_erc20_balance`, `eth_get_tx`, `eth_get_block_info`, `eth_get_receipt`, `eth_resolve_ens`, `eth_lookup_ens`, `eth_call_contract`, `eth_encode_function`, `eth_register_agent_8004`, `eth_lookup_agent_8004`, `eth_get_attestation`

### LayerZero (13 commands)
`lz_quote_fee`, `lz_send_message`, `lz_track_message`, `lz_oft_quote`, `lz_oft_send`, `lz_list_chains`, `lz_get_chain_rpc`, `lz_list_dvns`, `lz_get_deployments`, `lz_transfer_quote`, `lz_transfer_build`, `lz_stargate_quote`, `lz_stargate_send`

### Chainlink (12 commands)
`chainlink_get_price`, `chainlink_list_feeds`, `ccip_get_fee`, `ccip_send_message`, `ccip_track_message`, `ccip_get_supported_chains`, `vrf_request_random`, `vrf_get_subscription`, `ds_get_report`, `ds_list_feeds`, `por_get_reserve`, `por_list_feeds`

### Canton (12 commands)
`canton_submit_command`, `canton_list_contracts`, `canton_get_events`, `canton_get_transaction`, `canton_allocate_party`, `canton_list_parties`, `canton_list_domains_ext`, `canton_get_health`, `canton_get_balance_ext`, `canton_transfer`, `canton_create_asset`, `canton_dvp_settle`

See [SKILL.md](SKILL.md) for the complete reference with all commands and curl examples.

## Using with OpenClaw

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
    |-- JSON-RPC POST ---------> rpc.tenzro.network    (Tenzro blockchain)
    |-- HTTP POST/GET ---------> api.tenzro.network    (verification, faucet)
    |-- MCP Streamable HTTP ---> solana-mcp.tenzro.network   (Solana)
    |                         -> ethereum-mcp.tenzro.network (Ethereum)
    |                         -> layerzero-mcp.tenzro.network (LayerZero)
    |                         -> chainlink-mcp.tenzro.network (Chainlink)
    |                         -> canton-mcp.tenzro.network   (Canton)
    |                         -> lifi-mcp.tenzro.network     (LI.FI)
    |
    v
Tenzro Network (decentralized) + External Chains
```

## Related

| Resource | URL |
|----------|-----|
| Tenzro Network | [tenzro.com](https://tenzro.com) |
| MCP Server | [github.com/tenzro/tenzro-mcp-server](https://github.com/tenzro/tenzro-mcp-server) |
| A2A Server | [github.com/tenzro/tenzro-a2a-server](https://github.com/tenzro/tenzro-a2a-server) |
| LI.FI MCP | `lifi-mcp.tenzro.network/mcp` |
| JSON-RPC | `https://rpc.tenzro.network` |
| Web API | `https://api.tenzro.network` |

## Contact

- Website: [tenzro.com](https://tenzro.com)
- Engineering: [eng@tenzro.com](mailto:eng@tenzro.com)
- GitHub: [github.com/tenzro](https://github.com/tenzro)

## License

Apache 2.0. See [LICENSE](LICENSE).

# ponsmcp-openclaw

> Python integration for PonsMCP — enables OpenClaw AI agents to make autonomous MPP payments settled on Robinhood Chain.

[![PyPI version](https://img.shields.io/pypi/v/ponsmcp-openclaw)](https://pypi.org/project/ponsmcp-openclaw/)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/python-3.9%2B-blue)](https://python.org)

---

## Installation

```bash
pip install ponsmcp-openclaw
```

---

## Quick Start

```python
from ponsmcp import PonsMCPClient

client = PonsMCPClient(
    rpc_url='https://rpc.mainnet.chain.robinhood.com',
    chain_id=4663,
    wallet=agent_wallet,
    policies={
        'max_per_transaction': 100_000_000,  # 100 USDG (6 decimals)
        'daily_limit': 1_000_000_000         # 1000 USDG
    }
)

result = await client.pay_for_resource(
    url='https://api.weather.com/premium/forecast',
    parameters={'location': 'SF', 'days': 7}
)

print(f"Payment finalized: {result.hash}")
```

---

## OpenClaw Agent Integration

```python
from openclaw import Agent
from ponsmcp import BasePaymentProvider

agent = Agent(
    name="research_assistant",
    payment_provider=BasePaymentProvider(
        client=PonsMCPClient(
            rpc_url='https://rpc.mainnet.chain.robinhood.com',
            chain_id=4663,
            wallet=agent_wallet,
        )
    ),
)
```

---

## Network

| Setting | Value |
|---------|-------|
| Chain | Robinhood Chain (chainId `4663`) |
| RPC | `https://rpc.mainnet.chain.robinhood.com` |
| Explorer | `https://robinhoodchain.blockscout.com` |
| Settlement | USDG (`0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168`, 6 decimals) |

---

## License

MIT — see [LICENSE](LICENSE).

# Algorithmic Trading Bot

## Overview

A production-grade Python-based algorithmic trading bot designed for Linux terminal environments. Integrates with Axiom trading platform and CCXT-compatible brokers, featuring automated TP/SL management, real-time risk monitoring, and CLI dashboard.

## Features

✅ **Real-Time Market Data** — Continuous pandas DataFrame updates
✅ **Axiom Synchronization** — Lock in TP/SL and presets before trading
✅ **Risk Management** — Due diligence engine with mandatory checks
✅ **TP/SL Automation** — Automatic order attachment and modification
✅ **CLI Dashboard** — Rich terminal UI with live metrics
✅ **Linux Native** — Fully CLI-controlled, zero GUI dependencies

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Configure your trading parameters
cp config_template.py config.py
# Edit config.py with your API keys and risk parameters

# Run the bot
python main.py --mode=live

# View dashboard
python main.py --dashboard
```

## Architecture

```
trading-bot/
├── config.py                 # Configuration & presets
├── risk_management.py        # Due diligence engine
├── agent_core.py             # Main trading logic
├── execute_trade.py          # Order execution with TP/SL
├── market_data.py            # Real-time data fetching
├── logger.py                 # Logging & error tracking
├── main.py                   # CLI entry point
├── requirements.txt          # Dependencies
└── README.md                 # This file
```

## System Requirements

- Python 3.11+
- Linux (Ubuntu 20.04+ recommended)
- Internet connection for market data
- Broker API credentials (CCXT-compatible)

## Configuration

Edit `config.py` to set:

- **Broker Details**: API key, secret, trading pair
- **Risk Parameters**:
  - Max daily drawdown: 5%
  - Risk per trade: 2%
  - Min account equity: $1000
- **Axiom Presets**: TP %, SL %, position sizing
- **Market Filters**: Min volume, min liquidity, volatility threshold

## Usage

### Start Live Trading
```bash
python main.py --mode=live
```

### Backtest Strategy
```bash
python main.py --mode=backtest --period=30d
```

### View Dashboard
```bash
python main.py --dashboard
```

### Check Account Status
```bash
python main.py --status
```

## Risk Management

Every trade passes through a mandatory **Due Diligence Check** before execution:

1. **Maximum Daily Drawdown** — Ensures losses don't exceed X% of starting balance
2. **Margin/Risk Check** — Risk per trade ≤ Y% of account equity
3. **Market Volatility Filter** — Blocks trading during high-impact news
4. **Trend/Liquidity Confirmation** — Validates MA crossovers and volume metrics
5. **Axiom Preset Sync** — Verifies TP/SL alignment with preset rules

If ANY check fails, the trade is aborted and logged to `trading_errors.log`.

## Logging

All errors, trades, and system events are logged to:
- `trading_errors.log` — Failed due diligence checks
- `trading_debug.log` — Detailed execution trace
- `trading_audit.log` — All trades executed

## Contributing

See `CONTRIBUTING.md` for guidelines.

## License

MIT

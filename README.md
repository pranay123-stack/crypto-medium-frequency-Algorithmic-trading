# Crypto Medium Frequency Algorithmic Trading

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)](https://numpy.org)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A production-grade medium-frequency algorithmic trading system for cryptocurrency markets, operating on timeframes from seconds to minutes across multiple exchanges.

---

## Overview

| Metric | Value |
|--------|-------|
| **Timeframe** | 1s - 15m |
| **Exchanges** | Binance, Bybit, OKX, Kraken |
| **Strategies** | Mean Reversion, Momentum, VWAP, Order Flow |
| **Language** | Python 3.10+ |

---

## Features

- **Multi-Exchange Support** - Unified API for Binance, Bybit, OKX, Kraken via CCXT
- **Strategy Framework** - Modular architecture for easy strategy development
- **Backtesting Engine** - Historical data replay with realistic order fills and slippage
- **Risk Management** - Position sizing, stop-loss, take-profit, max drawdown limits
- **Live Trading** - Paper trading and live execution modes
- **Performance Analytics** - Real-time PnL, Sharpe ratio, drawdown, win rate tracking
- **Order Management** - Limit, market, stop orders with smart routing

---

## Strategies

| Strategy | Timeframe | Description | Indicators |
|----------|-----------|-------------|------------|
| **Mean Reversion** | 1m - 15m | Statistical arbitrage on price deviations from moving average | Bollinger Bands, Z-Score |
| **Momentum** | 5m - 1h | Trend following with volume confirmation | RSI, MACD, Volume |
| **VWAP** | 1m - 5m | Volume-weighted average price strategies for optimal execution | VWAP, TWAP |
| **Order Flow** | Tick - 1m | Microstructure-based signals from order book imbalance | Delta, CVD, Footprint |
| **Pairs Trading** | 5m - 1h | Cointegrated pairs mean reversion | Correlation, Spread |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                      TRADING SYSTEM ARCHITECTURE                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                      DATA LAYER                              │   │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌──────────┐ │   │
│  │  │  Binance  │  │   Bybit   │  │    OKX    │  │  Kraken  │ │   │
│  │  │ WebSocket │  │ WebSocket │  │ WebSocket │  │ WebSocket│ │   │
│  │  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘  └────┬─────┘ │   │
│  │        └──────────────┴───────┬──────┴─────────────┘       │   │
│  └───────────────────────────────┼────────────────────────────┘   │
│                                  ▼                                 │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    PROCESSING LAYER                          │   │
│  │                                                              │   │
│  │  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐  │   │
│  │  │   Market     │    │   Signal     │    │    Risk      │  │   │
│  │  │   Data       │───▶│   Generator  │───▶│   Manager    │  │   │
│  │  │   Handler    │    │              │    │              │  │   │
│  │  └──────────────┘    └──────────────┘    └──────┬───────┘  │   │
│  │                                                  │          │   │
│  │  ┌────────────────────────────────────────────────────────┐│   │
│  │  │                  STRATEGY ENGINE                       ││   │
│  │  │  ┌────────────┐ ┌────────────┐ ┌────────────┐         ││   │
│  │  │  │   Mean     │ │  Momentum  │ │   VWAP     │   ...   ││   │
│  │  │  │ Reversion  │ │            │ │            │         ││   │
│  │  │  └────────────┘ └────────────┘ └────────────┘         ││   │
│  │  └────────────────────────────────────────────────────────┘│   │
│  └───────────────────────────────┬────────────────────────────┘   │
│                                  ▼                                 │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    EXECUTION LAYER                           │   │
│  │  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐  │   │
│  │  │    Order     │    │   Position   │    │  Performance │  │   │
│  │  │   Manager    │    │   Tracker    │    │   Analytics  │  │   │
│  │  └──────────────┘    └──────────────┘    └──────────────┘  │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Project Structure

```
crypto-medium-frequency-Algorithmic-trading/
│
├── src/
│   ├── strategies/
│   │   ├── base_strategy.py      # Abstract strategy class
│   │   ├── mean_reversion.py     # Mean reversion strategy
│   │   ├── momentum.py           # Momentum/trend following
│   │   ├── vwap.py               # VWAP execution strategy
│   │   └── order_flow.py         # Order flow/microstructure
│   │
│   ├── exchange/
│   │   ├── base_exchange.py      # Exchange interface
│   │   ├── binance.py            # Binance connector
│   │   ├── bybit.py              # Bybit connector
│   │   └── unified.py            # Unified exchange wrapper
│   │
│   ├── data/
│   │   ├── feed.py               # Real-time data feed
│   │   ├── historical.py         # Historical data loader
│   │   └── orderbook.py          # Order book manager
│   │
│   ├── risk/
│   │   ├── position_sizer.py     # Position sizing algorithms
│   │   ├── stop_loss.py          # Stop loss management
│   │   └── portfolio.py          # Portfolio risk limits
│   │
│   ├── backtest/
│   │   ├── engine.py             # Backtesting engine
│   │   ├── simulator.py          # Order fill simulator
│   │   └── metrics.py            # Performance metrics
│   │
│   └── utils/
│       ├── config.py             # Configuration management
│       ├── logger.py             # Logging utilities
│       └── indicators.py         # Technical indicators
│
├── config/
│   ├── config.yaml               # Main configuration
│   └── strategies/               # Strategy-specific configs
│
├── tests/
│   ├── test_strategies.py
│   ├── test_backtest.py
│   └── test_risk.py
│
├── notebooks/
│   ├── strategy_research.ipynb
│   └── backtest_analysis.ipynb
│
├── requirements.txt
├── setup.py
└── README.md
```

---

## Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/pranay123-stack/crypto-medium-frequency-Algorithmic-trading.git
cd crypto-medium-frequency-Algorithmic-trading

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt

# Configure API keys
cp config/config.example.yaml config/config.yaml
# Edit config.yaml with your API keys
```

### Run Backtest

```bash
# Backtest mean reversion strategy
python -m src.backtest.engine \
  --strategy mean_reversion \
  --pair BTC/USDT \
  --start 2024-01-01 \
  --end 2024-12-31

# Backtest with custom parameters
python -m src.backtest.engine \
  --strategy momentum \
  --pair ETH/USDT \
  --timeframe 5m \
  --config config/strategies/momentum.yaml
```

### Run Live Trading

```bash
# Paper trading mode
python -m src.main \
  --strategy mean_reversion \
  --mode paper \
  --exchange binance

# Live trading (use with caution)
python -m src.main \
  --strategy mean_reversion \
  --mode live \
  --exchange binance
```

---

## Configuration

```yaml
# config/config.yaml
exchange:
  name: binance
  testnet: true
  api_key: ${BINANCE_API_KEY}
  api_secret: ${BINANCE_API_SECRET}

trading:
  pairs:
    - BTC/USDT
    - ETH/USDT
  timeframe: 5m
  max_positions: 3

strategy:
  name: mean_reversion
  params:
    lookback_period: 20
    z_score_entry: 2.0
    z_score_exit: 0.5

risk:
  max_position_size: 0.1      # 10% of portfolio per trade
  max_portfolio_risk: 0.02    # 2% max portfolio risk
  stop_loss: 0.02             # 2% stop loss
  take_profit: 0.04           # 4% take profit
  max_drawdown: 0.10          # 10% max drawdown halt

performance:
  target_sharpe: 2.0
  min_win_rate: 0.45
```

---

## Performance Metrics

| Metric | Description |
|--------|-------------|
| **Sharpe Ratio** | Risk-adjusted return (target > 2.0) |
| **Sortino Ratio** | Downside risk-adjusted return |
| **Max Drawdown** | Largest peak-to-trough decline |
| **Win Rate** | Percentage of profitable trades |
| **Profit Factor** | Gross profit / Gross loss |
| **Average Trade** | Mean return per trade |
| **Calmar Ratio** | Annual return / Max drawdown |

---

## Risk Management

- **Position Sizing**: Kelly criterion, fixed fractional, volatility-based
- **Stop Loss**: Fixed percentage, ATR-based, trailing stops
- **Portfolio Limits**: Max positions, correlation limits, sector exposure
- **Circuit Breakers**: Daily loss limit, drawdown halt, volatility pause

---

## Coming Soon

- [ ] Strategy implementations
- [ ] Backtesting engine with realistic fills
- [ ] Multi-exchange execution
- [ ] Machine learning signal enhancement
- [ ] Web dashboard for monitoring
- [ ] Docker deployment

---

## Risk Warning

**Algorithmic trading involves substantial risk of loss.** Past performance does not guarantee future results. Only trade with capital you can afford to lose.

---

## License

MIT License

---

## Contact

**Pranay** - Quantitative Developer

[![GitHub](https://img.shields.io/badge/GitHub-pranay123--stack-181717?style=flat&logo=github)](https://github.com/pranay123-stack)

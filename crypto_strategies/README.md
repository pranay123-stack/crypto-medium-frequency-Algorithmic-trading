# Crypto Trading Strategies

A comprehensive collection of **16 cryptocurrency trading strategies** for medium-frequency algorithmic trading on **Phemex** and **HyperLiquid** exchanges.

---

## 📁 Folder Structure

```
crypto_strategies/
│
├── 📄 Config Files
│   ├── key_file.py              # Phemex API keys
│   ├── dontshare.py             # HyperLiquid private key
│   ├── dontshare_config.py      # Combined config
│   └── nice_funcs.py            # Shared utility functions
│
├── 📈 Single-File Strategies (Phemex)
│   ├── sma_strategy.py          # SMA20 crossover strategy
│   ├── rsi_strategy.py          # RSI + SMA combined strategy
│   ├── vwap_strategy.py         # VWAP-based trading
│   ├── mean_reversion_74_tickers.py  # Multi-symbol mean reversion (74 cryptos)
│   └── arbitrage_bot.py         # BTC/ETH statistical arbitrage
│
├── 📂 Multi-File Strategies (HyperLiquid DEX)
│   ├── bollinger_bands_bot/     # Bollinger Band tightness detection
│   ├── supply_demand_zones_bot/ # Supply & Demand zone trading
│   └── vwap_bot/                # VWAP probabilistic entries
│
├── 📂 Multi-File Strategies (Phemex)
│   ├── turtle_trending_algo/    # 55-bar breakout + ATR stops
│   ├── correlation_algo/        # ETH-altcoin correlation trading
│   ├── consolidation_pop_algo/  # Consolidation breakout strategy
│   ├── nadaraya_watson_algo/    # ML-based + Stochastic RSI
│   └── market_maker_bot/        # Market making with spread capture
│
└── 📂 ai_backtest_strategies/   # 13 backtesting strategies
    ├── bt_rsi_vwap.py
    ├── bt_macd.py
    ├── bt_bollinger_bands.py
    ├── bt_elliot_waves.py
    └── ... (9 more)
```

---

## 🚀 Strategies Overview

### Single-File Strategies

| Strategy | File | Description | Indicators |
|----------|------|-------------|------------|
| **SMA Strategy** | `sma_strategy.py` | Trades based on SMA20 crossover | SMA20 |
| **RSI Strategy** | `rsi_strategy.py` | Combines RSI overbought/oversold with SMA | RSI, SMA |
| **VWAP Strategy** | `vwap_strategy.py` | Volume-weighted average price trading | VWAP, SMA, RSI |
| **Mean Reversion** | `mean_reversion_74_tickers.py` | Scans 74 crypto pairs for mean reversion | SMA20 |
| **Arbitrage Bot** | `arbitrage_bot.py` | BTC/ETH statistical arbitrage | Funding rates, S&D zones |

### Multi-File Strategies (HyperLiquid)

| Strategy | Folder | Description |
|----------|--------|-------------|
| **Bollinger Bands Bot** | `bollinger_bands_bot/` | Enters when bands are tight (low volatility), exits on breakout |
| **Supply & Demand Zones** | `supply_demand_zones_bot/` | Identifies and trades S&D zones with SMA confirmation |
| **VWAP Bot** | `vwap_bot/` | Probabilistic entries (70% long above VWAP, 30% below) |

### Multi-File Strategies (Phemex)

| Strategy | Folder | Description |
|----------|--------|-------------|
| **Turtle Trending** | `turtle_trending_algo/` | Classic 55-bar breakout with 2x ATR stops |
| **Correlation Algo** | `correlation_algo/` | Trades lagging altcoins when ETH moves |
| **Consolidation Pop** | `consolidation_pop_algo/` | Breakout from low-volatility consolidation |
| **Nadaraya-Watson** | `nadaraya_watson_algo/` | ML kernel smoother + Stochastic RSI |
| **Market Maker** | `market_maker_bot/` | Spread capture with bid-ask quoting |

### AI Backtest Strategies

13 backtesting strategies using `backtesting.py` library:
- RSI + VWAP, MACD, Bollinger Bands, Elliott Waves
- ADX, Ichimoku, Pivot Lines, Quarter Theory
- Grid Trading + Fibonacci, EMA + Bollinger, and more

---

## ⚙️ Installation

### Prerequisites

```bash
pip install ccxt pandas pandas_ta ta pytz schedule eth_account hyperliquid-python-sdk backtesting
```

### Clone Repository

```bash
git clone https://github.com/pranay123-stack/crypto-medium-frequency-Algorithmic-trading.git
cd crypto-medium-frequency-Algorithmic-trading/crypto_strategies
```

---

## 🔑 Configuration - To Run Live Trading

### 1. Add Phemex API Keys

Edit `key_file.py`:
```python
# Phemex API Keys
xP_KEY = "your_phemex_api_key_here"
xP_SECRET = "your_phemex_api_secret_here"
```

Also update the `config.py` files in each strategy folder that uses Phemex.

### 2. Add HyperLiquid Private Key

Edit `dontshare.py`:
```python
# HyperLiquid Private Key (Ethereum wallet private key)
private_key = "your_hyperliquid_private_key_here"
```

Copy to HyperLiquid strategy folders:
```bash
cp dontshare.py bollinger_bands_bot/
cp dontshare.py supply_demand_zones_bot/
cp dontshare.py vwap_bot/
```

### 3. Ensure Network Connectivity

- Phemex API: `api.phemex.com`
- HyperLiquid API: `api.hyperliquid.xyz`
- Coinbase API: `api.coinbase.com` (for correlation_algo)

---

## 🏃 Running Strategies

### Single-File Strategies

```bash
# Run SMA Strategy
python sma_strategy.py

# Run RSI Strategy
python rsi_strategy.py

# Run VWAP Strategy
python vwap_strategy.py

# Run Mean Reversion (74 tickers)
python mean_reversion_74_tickers.py
```

### Multi-File Strategies

```bash
# Run Bollinger Bands Bot
cd bollinger_bands_bot && python main.py

# Run Turtle Trending Algo
cd turtle_trending_algo && python main.py

# Run Market Maker Bot
cd market_maker_bot && python main.py
```

### Backtesting Strategies

```bash
cd ai_backtest_strategies

# Run MACD Backtest
python bt_macd.py

# Run Bollinger Bands Backtest
python bt_bollinger_bands.py
```

---

## 📊 Strategy Details

### Risk Management Features

All strategies include:
- ✅ Position sizing and leverage management
- ✅ Stop loss / take profit logic
- ✅ PNL-based exit conditions
- ✅ Maximum position limits
- ✅ Kill switch for emergency closure

### Default Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Take Profit | 5-9% | Profit target |
| Stop Loss | 8-10% | Maximum loss |
| Leverage | 10x | Default leverage |
| Timeframe | 1m-1h | Varies by strategy |

---

## ⚠️ Disclaimer

**USE AT YOUR OWN RISK.** These trading strategies are for educational purposes only. Cryptocurrency trading involves substantial risk of loss. Past performance is not indicative of future results.

- Always test with paper trading first
- Never invest more than you can afford to lose
- Monitor your bots regularly
- Keep API keys secure and never share them

---

## 📝 License

MIT License - Feel free to use, modify, and distribute.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

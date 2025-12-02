# Multi-Agent Trading Floor Simulation

A fully modular, real-time trading floor simulation featuring autonomous trader agents, custom market microstructure, account management, and a live Gradio dashboard for monitoring trades, positions, balances, and tracer events.

This project brings together 15+ coordinated modules to emulate a lightweight trading ecosystem where multiple agents—each following a distinct financial trading theory—compete and interact in a programmatically controlled market.

## Key Features

* Four autonomous trader agents implementing unique financial models.
* Real-time order-book market simulation with price updates and fills.
* Dedicated accounts engine for balance, PnL, and holdings management.
* Unified push, tracer, and market servers for event-driven execution.
* Live Gradio dashboard showing trades, activity logs, and account state.

## System Architecture

### 1. Trader Agents (`traders.py`, `reset.py`)

Each agent follows a distinct financial theory:

* Momentum trader
* Mean reversion trader
* Risk parity trader
* Arbitrage-based trader

The theories are initialized via `reset.py`, defining baseline parameters, reaction thresholds, and strategy logic.

### 2. Market Engine (`market.py`, `market_server.py`)

* Simulates a real-time market with bid/ask updates.
* Maintains an internal order book.
* Matches incoming orders based on price and availability.
* Sends execution events to the trading floor.

### 3. Accounts System (`accounts.py`, `accounts_server.py`, `accounts_client.py`)

* Manages balances, open positions, share quantities, and transaction history.
* Updates holdings after each order fill.
* Ensures all trades are validated and recorded correctly.

### 4. Event & Push Infrastructure (`push_server.py`, `tracers.py`)

* Emits real-time stream updates for:

  * Executed trades
  * Price changes
  * Agent decisions
  * System events
* Tracers record internal agent reasoning and interactions for debugging.

### 5. Database Layer (`database.py`)

* Stores transaction history and relevant session metadata.
* Supports resets between simulation runs.

### 6. Trading Floor Orchestrator (`trading_floor.py`)

* Core controller that:

  * Initializes all traders
  * Connects market and account servers
  * Routes messages between components
  * Executes trading cycles

### 7. Gradio Dashboard (`app.py`)

* User interface for monitoring simulation.
* Shows:

  * Live trades
  * Agent tracer logs
  * Current holdings
  * Cash balance
  * Market price updates

## File Structure

```
project/
│── traders.py
│── reset.py
│── trading_floor.py
│── market.py
│── market_server.py
│── accounts.py
│── accounts_server.py
│── accounts_client.py
│── database.py
│── push_server.py
│── tracers.py
│── mcp_params.py
│── templates.py
│── util.py
│── app.py
│── README.md
```

## Installation

### Prerequisites

* Python 3.10+
* Gradio
* FastAPI / Uvicorn (if running servers independently)
* Any additional dependencies defined in requirements

### Install Dependencies

```
pip install -r requirements.txt
```

## Usage

### Start the Servers (Market, Accounts, Push)

Run each server in separate terminals:

```
python market_server.py
python accounts_server.py
python push_server.py
```

### Start the Trading Floor

```
python trading_floor.py
```

### Launch the Gradio Dashboard

```
python app.py
```

This opens a UI streaming real-time:

* Trades executed
* Trader reasoning traces
* Holdings and current balance
* Market price updates

## Customization

### Modify Trading Theories

Adjust parameters or behaviors in `reset.py`.

### Add New Trader Agents

* Create a new trader class in `traders.py`.
* Register it in `trading_floor.py`.

### Change Market Dynamics

Modify tick frequency, price volatility, and liquidity in `market.py`.

### Enhance Visualization

Extend `app.py` for:

* Graphs for price history
* Profit/loss charts
* Agent performance comparisons

## Example Output

The dashboard may display:

* 10,000+ trades per run
* Live table of positions (shares, cost basis)
* Real-time buy/sell executions with timestamps
* Tracer logs showing agent reasoning steps

## Contributing

Pull requests introducing new trading strategies, visualization components, or engine improvements are welcome.

## License

Apache 2.0 License

# Circles Subscription Indexer

A DappNode package that indexes, queries, and auto-redeems Circles subscription events on Gnosis Chain.

## Overview

This package provides a complete solution for monitoring and interacting with the Circles SubscriptionModule contract (`0xcEbE4B6d50Ce877A9689ce4516Fe96911e099A78`). It consists of three main services:

- **Indexer**: Uses [arak](https://github.com/bh2smith/arak) to index subscription events from Gnosis Chain
- **SQLite**: Simple file shared file between indexer and api server.
- **API**: REST API for querying redeemable subscriptions and automatically redeeming them

## Features

- 🔍 **Real-time Event Indexing**: Monitors SubscriptionCreated, Unsubscribed, Redeemed, and RecipientUpdated events
- 🔄 **Automated Redemption**: Configurable auto-redeemer that claims subscriptions at regular intervals
- 🌐 **REST API**: Query redeemable subscriptions via HTTP endpoint
- 📦 **DappNode Native**: Packaged as a DappNode service with easy setup and configuration
- 🔒 **Secure Key Management**: Private key configuration through DappNode's setup wizard

## Installation

### Via DappNode

1. Install the package from the DappNode store or upload the release file
2. Configure the setup wizard:
   - **Redeemer Private Key**: The private key that will be used to redeem subscriptions (required)
   - **Redeem Interval**: How often to redeem in seconds (default: 86400 = 24 hours)
   - **Gnosis RPC URL**: RPC endpoint for Gnosis Chain (default: local DappNode Gnosis node)

### Manual Build

```bash
# Build the DappNode package
dappnodesdk build

# Or build individual services
docker-compose build
```

## Configuration

### Environment Variables

The API service accepts the following environment variables:

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `REDEEMER_PK` | Private key for redemption transactions | - | Yes |
| `REDEEM_INTERVAL` | Seconds between auto-redemptions | `86400` | No |
| `GNOSIS_RPC_URL` | Gnosis Chain RPC endpoint | `http://execution.gnosis.dncore.dappnode:8545` | No |

## API Usage

### Get Redeemable Subscriptions

```bash
curl http://api.subindexer-gnosis.public.dappnode:3000/redeemable
```

The API is exposed on port `3030` and can be accessed through DappNode's exposable services feature.

## Architecture

```
┌─────────────────┐
│   Gnosis Chain  │
└────────┬────────┘
         │
         v
┌─────────────────┐
│     Indexer     │ (arak)
│  Port: Internal │
└────────┬────────┘
         │
         v
┌─────────────────┐
│    DB File      │ (SQLite)
└────────┬────────┘
         │
         v
┌─────────────────┐
│       API       │
│   Port: 3030    │
└─────────────────┘
```

## Development

### Project Structure

```
.
├── api/             # REST API service
│   └── Dockerfile
├── indexer/         # Blockchain indexer
│   ├── arak.toml    # Indexer configuration
│   └── Dockerfile
├── docker-compose.yml
└── dappnode_package.json
```

### Local Development

```bash
# Start all services
docker-compose up

# Test the API
curl http://localhost:3030/redeemable
```

## Indexed Events

The following events from the SubscriptionModule contract are indexed:

- **SubscriptionCreated**: New subscription created
- **Unsubscribed**: Subscription cancelled
- **Redeemed**: Subscription payment redeemed
- **RecipientUpdated**: Subscription recipient changed

Starting from block `41149803` on Gnosis Chain.

## License

GPL-3.0

## Author

@bh2smith

## Links

- [Homepage](https://github.com/deluXtreme/)
- [DappNode](https://dappnode.io)


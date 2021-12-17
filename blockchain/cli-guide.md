# CLI Guide

This section describes the commands available from `bitsongd`, the command line interface that connects a running `bitsongd` process.

### `add-genesis-account` <a href="#add-genesis-account" id="add-genesis-account"></a>

Adds a genesis account to `genesis.json`.

#### Syntax

```
bitsongd add-genesis-account <address-or-key-name> '<amount><coin-denominator>,<amount><coin-denominator>'
```

#### Example

```
bitsongd add-genesis-account acc1 '200000000ubtsg'
```

### `collect-gentxs` <a href="#add-genesis-account" id="add-genesis-account"></a>

Collects genesis transactions and outputs them to `genesis.json`.

#### Syntax

```
bitsongd collect-gentxs
```

Coming soon....

# Run with Docker
You can easily start [Token Balance with Docker](https://hub.docker.com/r/hunterlong/tokenbalance/builds/). Register for a free [Infura.io API Key](https://infura.io/signup) to use Token Balance without downloading the ethereum blockchain.
```
docker run -p 8080:8080 -e GETH_SERVER=https://mainnet.infura.io/APIKEY -d hunterlong/tokenbalance
```

# Use as Golang Package
You can use Token Balance as a typical Go Language package if you you like to implement ERC20 functionality into your own application.

```bash
go get github.com/hunterlong/tokenbalance
```

###### First you'll want to connect to your Geth server or IPC
```go
import (
    "github.com/hunterlong/tokenbalance"
)

func main() {
	// connect to your Geth Server
    configs = &tokenbalance.Config{
         GethLocation: "https://eth.coinapp.io",
         Logs:         true,
    }
    configs.Connect()

    // insert a Token Contract address and Wallet address
    contract := "0x86fa049857e0209aa7d9e616f7eb3b3b78ecfdb0"
    wallet := "0xbfaa1a1ea534d35199e84859975648b59880f639"

    // query the blockchain and wallet details
    token, err := tokenbalance.New(contract, wallet)

    // Token Balance will respond back useful things
    token.BalanceString()  // "600000.0"
    token.ETHString()      // "1.020095885777777767"
    token.Name             // "OmiseGO"
    token.Symbol           // "OMG"
    token.Decimals         // 18
    token.Balance          // big.Int() (token balance)
    token.ETH              // big.Int() (ether balance)
}
```

# Implement in Google Sheets
If your familiar with Google Sheets, you can easily fetch all of your cryptocurrency balances within 1 spreadsheet. All you need to do is make a cell with the value below.
```
=ImportData("https://api.tokenbalance.com/balance/0xd26114cd6EE289AccF82350c8d8487fedB8A0C07/0xf9578adc61d07671f536d50afc5800232fc9fd86")
```
Simple as that! Get creative an use Coin Market Cap's API to fetch the price and multiply with your balance to make a portfolio of your cryptocurrencies!

# Implement in your App
Feel free to use the TokenBalance API server to fetch ERC20 token balances and details. We do have a header set that will allow you to call the API via AJAX. `Access-Control-Allow-Origin "*"` The server may limit your requests if you do more than 60 hits per minute.

# Run Your Own Server
TokenBalance isn't just an API, it's an opensource HTTP server that you can run on your own computer or server.

<p align="center"><img width="85%" src="https://img.cjx.io/tokenbalanceunix.gif">
<img width="85%" src="https://img.cjx.io/tokenbalancewindows.gif">
</p>

## Installation
##### Ubuntu 16.04
```bash
git clone https://github.com/hunterlong/tokenbalance
cd tokenbalance
go get && go build ./cmd
```

## Start TokenBalance Server
```bash
tokenbalance start --geth="/ethereum/geth.ipc"
```
This will create a light weight HTTP server will respond balance information about a ethereum contract token.

## Optional Config
```bash
tokenbalance start --geth="/ethereum/geth.ipc" --port 8080 --ip 127.0.0.1
```

#### CURL Request
```bash
CONTRACT=0xa74476443119A942dE498590Fe1f2454d7D4aC0d
ETH_ADDRESS=0xda0aed568d9a2dbdcbafc1576fedc633d28eee9a

curl https://api.tokenbalance.com/token/$CONTRACT/$ETH_ADDRESS
```

#### Response
```bash
{
    "name": "Kin",
    "wallet": "0x393c82c7Ae55B48775f4eCcd2523450d291f2418",
    "symbol": "KIN",
    "decimals": 18,
    "balance": "15788648",
    "eth_balance": "0.217960852347180212",
    "block": 4274167
}
```

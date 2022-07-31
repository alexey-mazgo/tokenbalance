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

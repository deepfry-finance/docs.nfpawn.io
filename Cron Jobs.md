## :runner: load-nfts (hourly)

This is responsible to find every NFT on the blockchain and cache into our database.

```pseudocode
interestingContracts = database.nftContracts.get(status = "Supported")

for contract in interestingContracts
  lastEvent = null
  
  for event in Web3.getEvents(contract.address, contract.syncedUpTo, "now", "Transfer")
    pretty = switch contract {
      when: "0x923487CryptoKitties"
      then: "Kitty #" + event.nftId
    }
	  database.nfts.replace(contract.address, event.nftId, event.erc721Recipient)
	  lastEvent = event
	  
	database.nftContracts.update(contract.address, lastEvent.blockNumber)
	
database.query(statsOffersQuery) >> api.nfpawn.io/stats/offers.json
```



## :runner: load-value (daily)

This finds the total cash committed to our project.

```pseudocode
totalValue = {}
totalUSD = 0

interestingContracts = database.valueContracts(status = "Supported")

for contract in interestingContracts
  prices = http.get("compound.finance/prices.json#" + contract.account)
  database.valueContracts.update(contract.account, approximatePrice = prices.USD)
  
  totalValueForThisContract = database.offers.query("SUM(saleValue)", saleContract = contract.account)
  totalValue[contract.account] = totalValueForThisContract

  totalUSD += totalValueForThisContract * contract.approximatePrice
  
database.query(statsLiquidityQuery) >> api.nfpawn.io/stats/liquidity.json
```


### 1. What is the difference between private, internal, public and external functions?   
Private can only be used internally within the current contract, and cannot be called by derived contracts inheritance; internal can be called by the current contract and derived contracts; public public can be called by both inside and outside the contract and derived contracts; external is only provided for external calls and cannot be called from within the contract. All interface functions must be declared external.


### 6. Before EIP-1559, how was the cost of an Ethereum transaction calculated? 
In EIP-1559, the cost of previous transactions in Ethereum was determined by miners through an auction mechanism. The miner selects the transaction with the highest bid and includes it in the next block. The cost of a transaction is determined by two factors: Gas Price and Gas Limit. Gas Price is a unit of measurement in the Ethereum network used to simplify the complexity of transactions. Gas Limit refers to the maximum amount of Gas that can be used by a transaction. The cost of a transaction is equal to Gas Price multiplied by Gas Limit. Therefore, the cost of a transaction depends on the values ​​of Gas Price and Gas Limit, which are set by the sender of the transaction.
### 7. The underlying principle of ETH transfer
The underlying principle is to modify the data on the chain. The more detailed answer is what happens during the transaction process. The following is the detailed process of ETH transfer:
(1)First, you need to connect to the Ethereum network and load your private key. You can do this using the go-ethereum client.
(2)Then you need to get the nonce of the sending account. Each new transaction requires a nonce, which is a number that is used only once. If it is a new account sending the transaction, the nonce will be "0".
(3)Next, you need to convert ETH to wei as this is the unit of currency used by the Ethereum blockchain. Ethernet supports up to 18 decimal places, so 1 ETH is 1 plus 18 zeros.
(4)You then need to set the amount of ETH you will transfer, as well as the gas limit and gas price. The gas limit should be capped at "21000" units, and the gas price must be set in wei units.
(5)Then you need to decide which address you want to send your ETH to. This is the receiving address.
(6)Next, you need to generate an unsigned Ethereum transaction. This function needs to receive nonce, address, value, gas upper limit value, gas price and optional data. The data field for sending ETH is "nil" (nil is null in go language).
(7)You then need to sign the transaction using the sender's private key. To do this, you can use the SignTx method provided by the go-ethereum client, which accepts an unsigned transaction and the private key you constructed earlier.
(8)Finally, you can broadcast the signed transaction to the entire network by calling "SendTransaction" on the client. This will send the transaction to all nodes in the network and wait for miners to package it into a block.

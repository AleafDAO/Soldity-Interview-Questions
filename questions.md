### 1. What is the difference between private, internal, public and external functions?   
Private can only be used internally within the current contract, and cannot be called by derived contracts inheritance; internal can be called by the current contract and derived contracts; public public can be called by both inside and outside the contract and derived contracts; external is only provided for external calls and cannot be called from within the contract. All interface functions must be declared external.

### 2. Before EIP-1559, how was the cost of an Ethereum transaction calculated?
In EIP-1559, the cost of previous transactions in Ethereum was determined by miners through an auction mechanism. The miner selects the transaction with the highest bid and includes it in the next block. The cost of a transaction is determined by two factors: Gas Price and Gas Limit. Gas Price is a unit of measurement in the Ethereum network used to simplify the complexity of transactions. Gas Limit refers to the maximum amount of Gas that can be used by a transaction. The cost of a transaction is equal to Gas Price multiplied by Gas Limit. Therefore, the cost of a transaction depends on the values ​​of Gas Price and Gas Limit, which are set by the sender of the transaction.

### 3. The underlying principle of ETH transfer
The underlying principle is to modify the data on the chain. The more detailed answer is what happens during the transaction process. The following is the detailed process of ETH transfer:   
(1)First, you need to connect to the Ethereum network and load your private key. You can do this using the go-ethereum client.   
(2)Then you need to get the nonce of the sending account. Each new transaction requires a nonce, which is a number that is used only once. If it is a new account sending the transaction, the nonce will be "0".   
(3)Next, you need to convert ETH to wei as this is the unit of currency used by the Ethereum blockchain. Ethernet supports up to 18 decimal places, so 1 ETH is 1 plus 18 zeros.   
(4)You then need to set the amount of ETH you will transfer, as well as the gas limit and gas price. The gas limit should be capped at "21000" units, and the gas price must be set in wei units.   
(5)Then you need to decide which address you want to send your ETH to. This is the receiving address.   
(6)Next, you need to generate an unsigned Ethereum transaction. This function needs to receive nonce, address, value, gas upper limit value, gas price and optional data. The data field for sending ETH is "nil" (nil is null in go language).   
(7)You then need to sign the transaction using the sender's private key. To do this, you can use the SignTx method provided by the go-ethereum client, which accepts an unsigned transaction and the private key you constructed earlier.   
(8)Finally, you can broadcast the signed transaction to the entire network by calling "SendTransaction" on the client. This will send the transaction to all nodes in the network and wait for miners to package it into a block.   

### 4.How large can a smart contract approximately be?
After the Shanghai upgrade, the implementation of EIP-3860 is 48KB, originally 24KB, which expands the code size to solve the high gas cost problem of complex contracts calling each other after being split.
*ps:*
“Shanghai Upgrade” is the first major upgrade after the merger of Ethereum, signifying the activation of Ethereum’s staking withdrawal feature and ultimately severing its ties with crypto “mining”. This upgrade holds significant implications for the future development of DeFi (Decentralized Finance), advancing Ethereum’s decentralization process and paving the way for the DeFi 3.0 era of “Farming as a Service” (FaaS).

Specifically, the Ethereum “Shanghai Upgrade” allows stakers to withdraw billions of dollars’ worth of the native token, Ether (ETH). Prior to this upgrade, while stakers could participate in staking, they were unable to withdraw. This upgrade unlocks over 16 million ETH staked on the network for nearly two years, giving stakers the flexibility to decide whether to continue staking based on their needs and market conditions. This positively impacts Ethereum’s liquidity and scalability.

Furthermore, through the introduced “redemption mechanism,” the comprehensive operation of a Proof of Stake (PoS) blockchain becomes a reality, granting stakers eventual control over their individual funds. This upgrade fundamentally alters the way transactions are validated and network security is maintained, rendering Ethereum’s “mining” practices obsolete. Under the new PoS system, computational work no longer consumes substantial energy; instead, block packaging rights are obtained through token collateral, addressing energy consumption concerns.

In summary, the Ethereum “Shanghai Upgrade” marks a significant milestone in the blockchain’s development journey, attracting widespread attention in the market and potentially influencing the price of Ether. 🚀

### 5.What are the differences between create and create2?
*1.CREATE Opcode:*
The CREATE opcode is commonly used for contract creation in Ethereum.
It generates a new contract address based on the sender’s address and a nonce value.
The formula for calculating the contract address is：
`address = keccak256(0xff ++ senderAddress ++ nonce)[12:]`
in this code:
- `keccak256` is the hash function.:smiley:
- `++` denotes concatenation.:flushed:
- `senderAddress`is the address of the account creating the contract.:relaxed:
- `nonce` is a unique number associated with the sender’s account.:grinning:
- Use-case:
   - Creating new contracts within a contract dynamically.
   - More cost-effective for deploying multiple contracts.
   - When address predictability is not a requirement.
*CREATE2 Opcode:*
The CREATE2 opcode provides predictable contract addresses.
Key components:
- A fixed prefix (always 0xFF).
- The sender’s address (ensures the contract is tied to a specific creator).
- A chosen salt value (adds uniqueness to the contract address).
- The bytecode of the new contract to be deployed.
The formula for calculating the contract address is:
`address = keccak256(0xff ++ senderAddress ++ salt ++ initCode)[12:]`
in this code:
* `salt` is an arbitrary value chosen by the contract creator.:smiley:
* `initCode` is the bytecode of the contract.:grinning:
- Use-case:
   - Ensuring a deterministic and predictable address for a new contract.
   - Useful in state channels, contract wallets, and off-chain interactions.
   - Offers an added layer of security by checking for existing contracts before deployment.
In summary, while CREATE is straightforward, CREATE2 provides predictable addresses. The latter is particularly useful when you need to know the contract address before deployment. 🚀


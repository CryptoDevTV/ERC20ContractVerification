# ContractSafety

## Checklist

### 1. Contract:

#### 1.1 Is verified on Etherscan?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Smart contracts are stored on Ethereum blockchain in bytecode (mainly for optimization reasons) so to be sure that the source code of the contract stored on blockchain is the same as the one published on GitHub or on project page, project team should also verifiy it on Etherscan by providing the raw source code. Etherscan than compares the bytecode of this provided source code with bytecode stored on Ethereum blockchain.

#### 1.2 Is ERC-20 compatible?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > If the contract under reviewed is the token contract (not staking contract, dao etc.) it should be compatible with `ERC-20` standard to provide full functionality while using it.

#### 1.3 It is a proxy contract?
  * [ ] `YES`
  * [ ] `NO`
 
  ##### If yes, what is the address of the current main contract?
  
  ##### Why does it matter?
  > If the main contract is a proxy contract, its owner is able change contract functionality without changing contract address. While proxy contract is discovered during the review it is obligatory to also find the current contract behind this proxy.
  
#### 1.4 Allow for renounce ownership?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Renounce ownership is a good and common pattern for term called "burning keys". When contract owner is able to do this it is a good sign that he will do it in the future, after that no one will be able to interference with this how this smart contract works and no one will be able to call functions with `onlyOwner` modifier.
 
#### 1.5 Allow minting?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Function `mint` is part of `ERC20` standard and not always when the contract use it, it is bad sign, however it should always be checked manually to mitigate potential risk. Using this function in malicious manner might lead to increasing supply "on demand" by the contract owner.

#### 1.6 Allow burning?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Burning tokens also has two side and should always be checked manually to mitigate potential risk. Using this function in malicious manner might lead to decreasing balance on addresses.

#### 1.7 Is pauseable?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Pausable means that the contract might be paused by the contract owner. It might be caused by security reasons (someone is using contract in unwanted way - diluting it from money) but it might be caused by malicious behaviour of contract owner (when he is trying to block selling for other except him). This function if is present, should always be checked manually to mitigate potential risk.

#### 1.8 Is some kind of whitelist present?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Some times contract owners have ability to stand out some addresses (for example if contrac owner pause the contract, those addresses would be still able to trade), it is important to check the contract source code for such malicious features. Should always be checked manually to mitigate potential risk.

#### 1.9 Is some kind of blacklist present?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Some times contract owners have ability to stand out some addresses (for example if some addresses would not be able to trade), it is important to check the contract source code for such malicious features. Should always be checked manually to mitigate potential risk.

#### 1.10 It is generated contract?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Generated contract means that contract owner do not code it from scratch, it might mean that the owner do not have needed skills to deal it with his own. There are situation that generated contracts are good for some cases but definietly should not be used for collecting eths from community.
 
#### 1.11 How contract was funded (DEX, CEX, TornadoCash etc.)?
  * [ ] `DEX`
  * [ ] `CEX`
  * [ ] `TornadoCash`
  * [ ] `External address`
  * [ ] `Contract address`
  ##### Why does it matter?
  > Especially, from where contract owner received eths needed for contract deployment. If from CEX it might be possible to track him in case of rug pull, for example if contract owner address received funds from Tornado Cash (flow anonymizer) it might means that owner want to stay as anonymous as possbile (also for tracking in case of rug pull).

### 2. Owner:

#### 2.1 It is a contract or external address?
  * [ ] `contract (multisig, dao)`
  * [ ] `external address`
  ##### Why does it matter?
  > If the contract owner is also a contract, it might mean that some kind of decentralized management is used for this contract (still needs some manual checks). External address always mean centralized management and should not be considered as a good practice.

#### 2.2 Is deployer of this contract?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > If the contract owner address is different than deployer address it might mean that contract development was outsource outside the project. It is hard to define if it is good ar bad approach, this is information should be taken into account during further project research.

#### 2.3 Are management keys burnt?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > If private keys to the contract owner address are burnt no one could change anything in the contract and no one is able to call functions from this contract.

### 3. Liquidity:

#### 3.1 Available on Uniswap?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Availbility on DEXes like Uniswap is very important because confirms project liquidity and also means that someone have to put some part of his eths to provide liquidity on automated market maker service like DEX (Uniswap, Sushiswap etc.).

#### 3.2 Is locked (TeamFinance, UniCrypt)?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > Locked liquidity means that until some defined time nobody would be able to remove provided liquidity from DEX. It is worth to mention that if some token is available to trade on single DEX only, removing liquidity means that trades will not be possible anymore (token holders are left with worthless tokens).

### 4. Holders:

#### 4.1 Is Uniswap first?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > If Uniswap or other DEX is main hodler it mainly means that nobody is able to dump or pump the price. 

#### 4.2 Is owner a main holder?
  * [ ] `YES`
  * [ ] `NO`
  ##### Why does it matter?
  > When there is one main hodler (and the contract owner or some external address is) it is very likely that he will try to manipulate the price and for example sell holded tokens cheaper to dump the price and earn some eths.

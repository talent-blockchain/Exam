1. codebase

I attached the code with RewardToken.sol and Staker.sol.

- RewardToken.sol

Token name: RewardToken
Token symbol: RTOKEN
Decimal: 18
Protocol: ERC20

There is mint() function and it can be called by owner.
Once deploy the token in the main network or test network, you should transfer the token ownership to the Staker.sol contract address.
Becauses Staker contract should mint the token for reward to the stakers.

You mentioned users can claim the rewards and withdraw the deposit, but theose features should be implemented in the Staker.sol contract.

- Staker.sol

Staker.sol contract is a contract to mint the reward token to the stakers.
Before deploying this contract, you should deploy the RewardToken contract first.
When you deploy this contract, you should set the parameters such as RewardToken contract address, start block, RewardToken amount per block(you mentioned 100. If so, it should be 100000000000000000000 because you should consider token decimal 18) and treasury address(This is not necessary for now)
I will explain the necessary main functions of Staker.sol contract.

 * add()
 This function can be called by only Staker contract owner.
 This function adds pools(pool means that users can stake their funds. Funds can be lp token or single token).

 * set()
 This function can be called by only Staker contract owner.
 Owner can adjust the allocation point and deposit fee of the already added pool.

 * updatePool()
 This function mint the RewardToken for per block according to the allocation point of the pool for each user.

 * deposit()
 This function is called when users deposit their funds to the pool. If so, funds are stored in the user account.

 * withdraw()
 This function is called when users withdraw their funds.

 * updateEmissionRate()
 This function can be called by only Staker contract owner.
 Staker.sol contract owner can adjust the emission rate. Emission rate means the minting token amount per block.


2. Tools
I can deploy these contracts by using Remix.
https://remix.ethereum.org
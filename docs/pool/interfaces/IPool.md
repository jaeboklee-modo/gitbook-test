


## Functions
### handleDeposit
```solidity
  function handleDeposit(
    address account,
    uint256 amount,
    uint256 poolInterestIndex
  ) external
```
When user deposits, pool contract mints pool token equivalent to the deposit amount.
PoolTokens are backed by assets deposited in the pool in a 1:1 ratio.
This function is only callable by the core contract






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`account` | address | The address that will receive the PoolToken
|`amount` | uint256 | The amount being deposited
|`poolInterestIndex` | uint256 | The new interest index of the pool

### handleWithdraw
```solidity
  function handleWithdraw(
    address account,
    address receiver,
    uint256 amount,
    uint256 poolInterestIndex
  ) external
```
When user withdraw, pool contract burns pool tokens from `account`and transfer underlying asset to `receiver`
This function is only callable by the core contract






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`account` | address | The owner of the pool tokens
|`receiver` | address | The address that will receive the underlying asset
|`amount` | uint256 | The amount being burned
|`poolInterestIndex` | uint256 | The new interest index of the pool

### transferUnderlyingTo
```solidity
  function transferUnderlyingTo(
    address receiver,
    uint256 amount
  ) external
```
Transfers the underlying asset to receiver.






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`receiver` | address | The recipient of the underlying asset
|`amount` | uint256 | The amount getting transferred


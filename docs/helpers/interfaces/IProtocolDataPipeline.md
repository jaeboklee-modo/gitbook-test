


## Functions
### getUserData
```solidity
  function getUserData(
    address asset,
    address account
  ) external returns (uint256 poolTokenBalance, uint256 implicitPoolTokenBalance, uint256 debtTokenBalance, uint256 principalDebtTokenBalance, uint256 averageBorrowRate, uint256 lastUpdateTimestamp)
```
This function aggregates protocol user data






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of underlying asset of the pool
|`account` | address | The user address

#### Return Values:
| Name                           | Type          | Description                                                                  |
| :----------------------------- | :------------ | :--------------------------------------------------------------------------- |
|`poolTokenBalance`| address | The pool token balance of the user
|`implicitPoolTokenBalance`| address | The implicit pool token balance of the user
|`debtTokenBalance`|  | The current debt token balance of the user
|`principalDebtTokenBalance`|  | The principal debt token balance of the user
|`averageBorrowRate`|  | The average stable borrow rate of the user
|`lastUpdateTimestamp`|  | The user last update timestamp
### getPoolData
```solidity
  function getPoolData(
    address asset
  ) external returns (uint256 totalPoolTokenSupply, uint256 implicitPoolTokenSupply, uint256 poolInterestIndex, uint256 principalDebtTokenSupply, uint256 totalDebtTokenSupply, uint256 averageRealAssetBorrowRate, uint256 debtTokenLastUpdateTimestamp, uint256 borrowAPY, uint256 depositAPY, uint256 poolLastUpdateTimestamp, address poolTokenAddress, address debtTokenAddress)
```
This function aggregates protocol pool data for specific asset






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of underlying asset of the pool



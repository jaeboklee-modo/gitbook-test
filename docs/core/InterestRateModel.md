


## Functions
### calculateRates
```solidity
  function calculateRates(
    address asset,
    uint256 totalPoolTokenSupply,
    uint256 totalDebtTokenSupply,
    uint256 depositAmount,
    uint256 borrowAmount,
    uint256 poolFactor
  ) external returns (uint256 newBorrowAPY, uint256 newDepositAPY)
```
Calculates the interest rates based on the token balances.

Calculation Example
Case1: under optimal U
baseRate = 2%, util = 40%, optimalRate = 10%, optimalUtil = 80%
result = 2+40*(10-2)/80 = 4%
Case2: over optimal U
optimalRate = 10%, util = 90%, maxRate = 100%, optimalUtil = 80%
result = 10+(90-80)*(100-10)/(100-80) = 55%





#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address
|`totalPoolTokenSupply` | uint256 | Total pool token supply
|`totalDebtTokenSupply` | uint256 | Total debt token supply
|`depositAmount` | uint256 | The liquidity added during the operation
|`borrowAmount` | uint256 | The liquidity taken during the operation
|`poolFactor` | uint256 | The pool factor for reserve

#### Return Values:
| Name                           | Type          | Description                                                                  |
| :----------------------------- | :------------ | :--------------------------------------------------------------------------- |
|`newBorrowAPY`| address | Calculeted borrowAPY
|`newDepositAPY`| uint256 | Calculeted depositAPY
### addNewPoolInterestRateModel
```solidity
  function addNewPoolInterestRateModel(
    address asset,
    uint256 optimalUtilizationRate,
    uint256 borrowRateBase,
    uint256 borrowRateOptimal,
    uint256 borrowRateMax
  ) external
```
This function can be called when new pool added to add new interest rate model
Only callable by the core contract



#### Design
##### Check
Make sure that `msg.sender` is core contract
InterestRateModelParams with `asset` does not already exist

##### Effect
set `_interestRateModel[asset]` to given params

##### Interaction
emit `AddNewPoolInterestRateModel` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address to added
|`optimalUtilizationRate` | uint256 | The new optimalUtilizationRate
|`borrowRateBase` | uint256 | The new borrowRateBase
|`borrowRateOptimal` | uint256 | The new borrowRateOptimal
|`borrowRateMax` | uint256 | The new borrowRateMax

### updateOptimalUtilizationRate
```solidity
  function updateOptimalUtilizationRate(
    address asset,
    uint256 optimalUtilizationRate
  ) external
```
This function can be called by governance to update interest rate model param
Only callable by the governance contract



#### Design
##### Check
Make sure that `msg.sender` is core contract

##### Effect
update `_interestRateModel[asset].optimalUtilizationRate` to `optimalUtilizationRate`

##### Interaction
emit `UpdateOptimalUtilizationRate` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address to update model
|`optimalUtilizationRate` | uint256 | New optimalUtilizationRate to update

### updateBorrowRateBase
```solidity
  function updateBorrowRateBase(
    address asset,
    uint256 borrowRateBase
  ) external
```
This function can be called by governance to update interest rate model param
Only callable by the governance contract



#### Design
##### Check
Make sure that `msg.sender` is core contract

##### Effect
update `_interestRateModel[asset].borrowRateBase` to `borrowRateBase`

##### Interaction
emit `UpdateBorrowRateBase` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address to update model
|`borrowRateBase` | uint256 | New optimalUtilizationRate to update

### updateBorrowRateOptimal
```solidity
  function updateBorrowRateOptimal(
    address asset,
    uint256 borrowRateOptimal
  ) external
```
This function can be called by governance to update interest rate model param
Only callable by the governance contract



#### Design
##### Check
Make sure that `msg.sender` is core contract

##### Effect
update `_interestRateModel[asset].borrowRateOptimal` to `borrowRateOptimal`

##### Interaction
emit `UpdateBorrowRateOptimal` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address to update model
|`borrowRateOptimal` | uint256 | New optimalUtilizationRate to update

### updateBorrowRateMax
```solidity
  function updateBorrowRateMax(
    address asset,
    uint256 borrowRateMax
  ) external
```
This function can be called by governance to update interest rate model param
Only callable by the governance contract



#### Design
##### Check
Make sure that `msg.sender` is core contract

##### Effect
update `_interestRateModel[asset].borrowRateMax` to `borrowRateMax`

##### Interaction
emit `UpdateBorrowRateMax` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address to update model
|`borrowRateMax` | uint256 | New optimalUtilizationRate to update

### getInterestRateModelParam
```solidity
  function getInterestRateModelParam(
    address asset,
     optimalUtilizationRate,
     borrowRateBase,
     borrowRateOptimal,
     borrowRateMax
  ) external returns (uint256 optimalUtilizationRate, uint256 borrowRateBase, uint256 borrowRateOptimal, uint256 borrowRateMax)
```
This function returns interest rate model params for asset






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | Underlying asset address
|`optimalUtilizationRate` |  | When the pool utilization ratio exceeds this parameter, the kinked rates model adjusts interests.
|`borrowRateBase` |  | The interest rate when utilization ratio is zero.
|`borrowRateOptimal` |  | The interest rate when the pool utilization ratio is optimal.
|`borrowRateMax` |  | The interest rate when the pool utilization ratio is 1.

### getProtocolAddressProvider
```solidity
  function getProtocolAddressProvider(
  ) external returns (address protocolAddressProvider)
```
This function returns the address of protocolAddressProvider contract







#### Return Values:
| Name                           | Type          | Description                                                                  |
| :----------------------------- | :------------ | :--------------------------------------------------------------------------- |
|`protocolAddressProvider`|  | The address of protocolAddressProvider contract

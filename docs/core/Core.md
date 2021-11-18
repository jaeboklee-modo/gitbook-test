


## Functions
### deposit
```solidity
  function deposit(
    address asset,
    address account,
    uint256 amount
  ) external
```
By depositing assets in the pool and supply liquidity, depositors can receive
interest accruing from the pool. The return on the deposit arises from the interest on loans.
MoneyPool depositors who deposit certain assets receives pool token equivalent to
the deposit amount. Pool tokens are backed by assets deposited in the pool in a 1:1 ratio.



#### Design
##### Check
- make sure that pool is active and not paused
- `amount` is not 0

##### Effect
- update interest rate and pool state

##### Interaction
- call `pool.handleDeposit`
  - mint poolToken to `account`
- `asset.safeTransferFrom`
  - transfer underlying asset from `msg.sender` to `pool`
emit `Deposit` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset to deposit
|`account` | address | The address that will receive the LToken
|`amount` | uint256 | Deposit amount

### withdraw
```solidity
  function withdraw(
    address asset,
    address account,
    uint256 amount
  ) external
```
The depositors can seize their assets deposited in the pool whenever they wish.
User can withdraw an amount of underlying asset from the pool and burn the corresponding pool tokens.



#### Design
##### Check
- make sure that pool is active and not paused
- `amount` is not 0
- `amount` is less than pool available liquidity

##### Effect
- update interest rate and pool state

##### Interaction
- call `pool.handleWithdraw`
  - burn poolToken from `msg.sender` and transfer underlying asset to `account`
- emit `Withdraw` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset to withdraw
|`account` | address | The address that will receive the underlying asset
|`amount` | uint256 | Withdrawl amount

### borrow
```solidity
  function borrow(
    address asset,
    address borrower,
    address receiver,
    address tokenId,
    uint256 loanPrincipalAmount,
    uint256 dueTimestamp,
    uint256 description
  ) external
```
The user can take out a loan of value below to the principal
recorded in the asset bond data. As asset token is deposited as collateral in the Money Pool
and loans are made, financial services that link real assets and cryptoassets can be achieved.



#### Design
##### Check
- make sure that `msg.sender` is the council governance contract
- make sure that pool is active and not paused
- `amount` should be less than `asset.balanceOf(pool)`
- call `onERC721Received` and check that erc721 is whitelisted one

##### Effect
- update interest rate and pool state

##### Interaction
- call `loanManager.beginLoan`
  - hash loan and save loan data in the loanManager
- call `debtToken.mint`
  - mint debt token to borrower
- call `pool.transferUnderlyingTo`
  - transfer loan principal to `receiver`
- call `collateral.safeTransferFrom`
  - transfer asset token from `borrower` to `receiver`
  - asset token to be collateralized should be approved for core `address(this)`
- emit `Borrow` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset to borrow
|`borrower` | address | The address of account who will collateralize asset token and begin the loan
|`receiver` | address | The address of account who will receive the loan principal
|`tokenId` | address | The id of the token to collateralize
|`loanPrincipalAmount` | uint256 | The original sum of money transferred from lender to borrower at the beginning of the loan
|`dueTimestamp` | uint256 | The amount of time (measured in seconds) that can elapse before the lender can liquidate the loan
and seize the underlying collateral NFT
|`description` | uint256 | Description for the loan

### repay
```solidity
  function repay(
  ) external
```



#### Design
##### Check
call `loanManager.repayLoan`
  - loan must not be `DEFAULTED`

##### Effect
- update interest rate and pool state
  - burn debt token from `borrower` and transfer

##### Interaction
call `loanManager.repayLoan`
  - change loan state to `END`
- call `asset.safeTransferFrom`
  - transfer principal and interest from `msg.sender` to `pool`
- call `collateral.transfer` @TODO: Who will manage NFT?
  - transfer collateralized asset token to `borrower`
- call `debtToken.burn`
  - burn debt token from `borrower`




### liquidate
```solidity
  function liquidate(
  ) external
```



#### Design
##### Check
call `loanManager.repayLoan`
  - loan must be `DEFAULTED`

##### Effect
- update interest rate and pool state
  - burn debt token from `borrower` and transfer

##### Interaction
- call `asset.safeTransferFrom`
  - transfer principal and interest from `msg.sender` to `pool`
- call `collateral.transfer` @TODO: Who will manage NFT?
  - transfer collateralized asset token to `borrower`
- call `debtToken.burn`
  - burn debt token from `borrower`




### addNewPool
```solidity
  function addNewPool(
    address asset,
    uint256 optimalUtilizationRate,
    uint256 borrowRateBase,
    uint256 borrowRateOptimal,
    uint256 borrowRateMax
  ) external
```
This function can be called when new pool added
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
|`asset` | address | Underlying asset address to add
|`optimalUtilizationRate` | uint256 | The new optimalUtilizationRate
|`borrowRateBase` | uint256 | The new borrowRateBase
|`borrowRateOptimal` | uint256 | The new borrowRateOptimal
|`borrowRateMax` | uint256 | The new borrowRateMax

### getPoolData
```solidity
  function getPoolData(
    address poolInterestIndex,
     depositAPY,
     borrowAPY,
     lastUpdateTimestamp,
     poolFactor,
     poolTokenAddress,
     debtTokenAddress,
     isPaused,
     isActivated
  ) external returns (uint256 poolInterestIndex, uint256 borrowAPY, uint256 depositAPY, uint256 lastUpdateTimestamp, uint256 poolFactor, address poolTokenAddress, address debtTokenAddress, bool isPaused, bool isActivated)
```
Returns the state and configuration of the pool






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`poolInterestIndex` | address | data
|`depositAPY` |  | data
|`borrowAPY` |  | data
|`lastUpdateTimestamp` |  | data
|`poolFactor` |  | data
|`poolTokenAddress` |  | data
|`debtTokenAddress` |  | data
|`isPaused` |  | data
|`isActivated` |  | data

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
### getInterestRateModel
```solidity
  function getInterestRateModel(
  ) external returns (address interestRateModel)
```
This function returns the address of interestRateModel contract







#### Return Values:
| Name                           | Type          | Description                                                                  |
| :----------------------------- | :------------ | :--------------------------------------------------------------------------- |
|`interestRateModel`|  | The address of interestRateModel contract
### updateInterestRateModel
```solidity
  function updateInterestRateModel(
    address interestRateModel
  ) external
```
This function updates the address of interestRateModel contract



#### Design
##### Check
make sure that `msg.sender` is the governance contract

##### Effect
set `_interestRateModel`

##### Interaction
emit `UpdateInterestRateModel` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`interestRateModel` | address | The address of interestRateModel contract

### activatePool
```solidity
  function activatePool(
    address asset
  ) external
```
Activates a pool



#### Design
##### Check
make sure that `msg.sender` is the guardian address

##### Effect
set `poolData[asset].isActive` to true

##### Interaction
emit `ActivatePool` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset of the pool

### deactivatePool
```solidity
  function deactivatePool(
    address asset
  ) external
```
Deactivates a pool



#### Design
##### Check
make sure that `msg.sender` is the guardian address

##### Effect
set `poolData[asset].isActive` to false

##### Interaction
emit `DeactivatePool` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset of the pool

### pausePool
```solidity
  function pausePool(
    address asset
  ) external
```
Pause a pool. A paused pool doesn't allow any new deposit, borrow or rate swap
but allows repayments, liquidations, rate rebalances and withdrawals



#### Design
##### Check
make sure that `msg.sender` is the guardian address

##### Effect
set `poolData[asset].isPaused` to true

##### Interaction
emit `PausePool` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset of the pool

### unpausePool
```solidity
  function unpausePool(
    address asset
  ) external
```
Unpause a pool



#### Design
##### Check
make sure that `msg.sender` is the guardian address

##### Effect
set `poolData[asset].isPaused` to false

##### Interaction
emit `UnpausePool` event


#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`asset` | address | The address of the underlying asset of the pool


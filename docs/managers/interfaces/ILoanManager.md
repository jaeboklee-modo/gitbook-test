


## Functions
### beginLoan
```solidity
  function beginLoan(
    address interestRate
  ) external returns (uint256 loanId)
```






#### Parameters:
| Name | Type | Description                                                          |
| :--- | :--- | :------------------------------------------------------------------- |
|`interestRate` | address | The interest rate for the loan

#### Return Values:
| Name                           | Type          | Description                                                                  |
| :----------------------------- | :------------ | :--------------------------------------------------------------------------- |
|`loanId`| address | The id of loan initialized which is produced by hashing the loan struct
### repayLoan
```solidity
  function repayLoan(
  ) external
```
This function can be called when loan redeemed







### hashLoan
```solidity
  function hashLoan(
  ) external returns (uint256 loanId)
```








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

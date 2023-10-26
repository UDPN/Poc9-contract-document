# POC 9 FX Contracts

>The following sections document several interfaces required by service providers.

## Methods
**NOTES:**
  - The following specifications use syntax from Solidity 0.8.19 (or above).

**setFXRate**

Sets and update the foreign exchange rate between the specified two currencies.
```
function setFXRate(
        bytes32 rateId,
        uint256 rate,
        uint256 date,
        string memory comments
    ) public whenNotPaused returns (bool)
fxRateOf
Returns the specified foreign exchange rate information.
function fxRateOf(
        bytes32 rateId
    ) external view returns (FXRateInfo memory)
    
 
 // Structure definition
 struct FXRateInfo {
        bytes32 rateId;
        string from;
        string to;
        uint256 rate;
        uint256 date;
        bytes32 provider;
   }
   ```
**capitalPoolOf**

Returns the specified capitalpool account information.

```
 function capitalPoolOf(
        bytes32 provider,
        string memory coinName
    ) public view returns (CapitalPoolInfo memory) 
   
   // Structure definition
   struct CapitalPoolInfo {
        string coinName;
        address accountId;
        uint256 balance;
        bytes32 provider;
        uint256 modifyTime;
    }
```
**setCapitalPoolBalance**

Updates the capitalpool account balance with the specified currency.

```

function setCapitalPoolBalance(
        string memory coinName,
        address accountId,
        uint256 balance,
        string memory comments
    ) public whenNotPaused returns (bool)
```

**balanceOf**

Returns the capitalpool account balance of the specified currency.

```
function balanceOf(
        bytes32 provider,
        string memory coinName,
        address accountId
    ) public view returns (uint256)

```

## Events

**FXRateChanged**

Triggers on any successful call to setFXRate(bytes32 rateId, uint256 rate, uint256 date, string memory comments)()

```
event FXRateChanged(
        address indexed caller,
        bytes32 rateId,
        uint256 rate,
        uint256 originalRate,
        uint256 date,
        string comments
    );
```

**BalanceChanged**

Triggers on any successful call to setCapitalPoolBalance()

```
event BalanceChanged(
        address indexed caller,
        string coinName,
        address accountId,
        uint256 balance,
        uint256 originalBalance,
        string comments
    );
```

# POC 9 CBDC Contracts

> The following sections document several interfaces required by service providers.
Currently, the service provider must approve a certain amount of the capitalpool account with the specified currencies to FXContract account before providing the foreign exchange business.

**Methods**

**approve**

Allows _spender to withdraw from your account multiple times, up to the _value amount. If this function is called again, it overwrites the current allowance with _value.

```
function approve(address _spender, uint256 _value) public returns (bool success)
```
 
**allowance**

Returns the amount which _spender is still allowed to withdraw from _owner.

```
function allowance(address _owner, address _spender) public view returns (uint256 remaining)
```

## Events

**Approval**

Triggers on any successful call to approve(address _spender, uint256 _value)

```
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```


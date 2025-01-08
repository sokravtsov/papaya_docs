# Common Methods

***

### deposit

Enables the deposit of funds into the contract. To use this method, you must first approve the necessary amount of tokens for the Papaya contract.

```solidity
function deposit(uint256 amount, bool isPermit2)
```

***

### withdraw

Allows withdrawal of funds at any time. Upon invocation, your balance is synchronized, and any available amount can be withdrawn.

```solidity
function withdraw(uint256 amount)
```

***

### balanceOf

An enhanced ERC20 method that shows the real-time balance, accounting for per-second updates due to streaming, even without prior synchronization.

```solidity
function balanceOf(address account)
```

***

### depositFor

Facilitates depositing funds into another user's account, essential for integrating third-party payment systems, such as fiat on-ramp services.

```solidity
function depositFor(uint256 amount, address user, bool isPermit2)
```

***

### withdrawTo

Enables withdrawal of funds to a different wallet.

```solidity
function withdrawTo(address to, uint256 amount)
```

***

> Frequently Asked Question: Why don’t you use fund withdrawal from the user’s wallet upon request (i.e., transferFrom), but instead transfer them to the protocol?

Given the potential for permission revocation, we prefer to ensure clear liquidity visibility for all participants. This approach addresses the issue of unpaid payments. For instance, if a user retains permissions and a subscription for a month but revokes permission right before the subscription fee is collected, it could result in a loss for the author. Our method prevents such scenarios.

\

---
description: What the contract owner can and cannot do, and the risks to know.
---

# Security and custody

## Non-custodial

* Papaya never holds user private keys.
* Funds deposited into Papaya sit in the smart contract, not in a Papaya-controlled wallet.
* Users and merchants can withdraw their available balance at any time.

## What the contract owner can and cannot do

The contract owner **cannot** move user balances. The only owner function that moves tokens, `rescueFunds`, is limited to tokens sent to the contract by mistake: it cannot withdraw more than the amount above the sum of all user balances.

The contracts have no pause function and are not upgradeable. Rules cannot be changed for existing deployments.

## Risks to understand

* **Smart contract risk.** All balances for a stablecoin on a network sit in one contract. A bug in that contract would affect all of them.
* **Liquidation.** If a balance runs low and cannot be refilled, the account is liquidated: some or all of its subscriptions are cancelled so the balance can cover what remains. The caller receives a reward of about $0.01 to cover gas, and the rest of the balance stays with the user. Keep balances funded or set up an allowance for refill.
* **Price feeds.** In streaming mode, liquidation thresholds and refill rewards use Chainlink price feeds for the gas token and the stablecoin.
* **Stablecoin risk.** Papaya holds balances in the deposited stablecoin and inherits its risks (issuer, depeg, freezing).

## Audits and patents

* The core streaming contract was audited by Stronghold Security.
* Periodic subscriptions are in preview.
* The Papaya architecture is patent pending (USPTO).

## Responsible disclosure

If you find a vulnerability, please contact the team at support@papaya.finance before disclosing it publicly.

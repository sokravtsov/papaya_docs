---
description: Class for using writable methods of Papaya Contract
---

# PapayaBySigInteraction

***

### <mark style="color:blue;">constructor</mark>

#### description

"rpcUrl" is an address of your rpc

```typescript
constructor({chainId: number, papayaAddress: string, tokenAddress: string, provider?: JsonRpcProvider, secretKey?: string})
```

#### parameters

* `chainId(`<mark style="color:purple;">`number`</mark>`)` - id of selected blockchain
* `papayaAddress(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` - smart-contract address
* `tokenAddress(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` - token address
* `provider( JsonRpcProvider )` - jsonRpc blockchain provider from [**ethers.js**](https://docs.ethers.org/v5/api/providers/jsonrpc-provider/)
* `secretKey(`<mark style="color:purple;">`string`</mark>`)` - wallet private key

{% hint style="info" %}
**secretKey** and **rpcUrl** are mostly made for the NodeJS environment. It is not recommended to use them in browser.
{% endhint %}

#### usage

```typescript
import { PapayaBySigInteraction } from "@papaya-metaverse/papaya-sdk"

const papayaBySigInteraction = new PapayaBySigInteraction({
    chainId: 1,
    papayaAddress: "0x1c3E45F2D9Dd65ceb6a644A646337015119952ff",
    tokenAddress: "0x1234567890123456789012345678901234567890",
    provider:  new JsonRpcProvider("https://polygon.infura.io/v3/${INFURA_API_KEY}"),
    //secretKey: "<WALLET_PRIVATE_KEY>" - only when there is no way to allow users to connect their wallets
})
```

***

### <mark style="color:blue;">bySigDeposit</mark>

#### description

```typescript
async bySigDeposit(amount, deadline, isPermit2 = false)
```

#### parameters

* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;
* `isPermit2(`<mark style="color:purple;">`boolean`</mark>`)` - a flag indicating the specificity of the token

***

### <mark style="color:blue;">permitAndDeposit</mark>

#### description

```typescript
async permitAndDeposit(amount, deadline)
```

#### parameters

* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigDepositFor</mark>

#### description

```typescript
async bySigDepositFor(to, amount, deadline, isPermit2 = false)
```

#### parameters

* `to(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;
* `isPermit2(`<mark style="color:purple;">`boolean`</mark>`)` - a flag indicating the specificity of the token

***

### <mark style="color:blue;">permitAndBySigDepositFor</mark>

#### description

```typescript
async permitAndBySigDepositFor(to, amount, deadline, isPermit2 = false)
```

#### parameters

* `to(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;
* `isPermit2(`<mark style="color:purple;">`boolean`</mark>`)` - a flag indicating the specificity of the token

***

### <mark style="color:blue;">bySigWithdraw</mark>

#### description

```typescript
async bySigWithdraw(amount, deadline)
```

#### parameters

* `amount (`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigWithdrawTo</mark>

#### description

```typescript
async bySigWithdrawTo(to, amount, deadline)
```

#### parameters

* `to(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigPay</mark>

#### description

```typescript
async bySigPay(to, amount, deadline)
```

#### parameters

* `to(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigSubscribe</mark>

#### description

```typescript
async bySigSubscribe(author, subscriptionRate, projectId, deadline)
```

#### parameters

* `author(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `subscriptionRate(`<mark style="color:purple;">`number`</mark>`)` -
* `projectId(`<mark style="color:purple;">`number`</mark>`)` -&#x20;
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigUnsubscribe</mark>

#### description

```typescript
async bySigUnsubscribe(author, deadline)
```

#### parameters

* `author(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">bySigLiquidate</mark>

#### description

```typescript
async bySigLiquidate(account, deadline)
```

#### parameters

* `account(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `deadline(`<mark style="color:purple;">`number`</mark>`)` -&#x20;

***

### <mark style="color:blue;">buildBySigTraits</mark>

#### description

```typescript
async buildBySigTraits({ nonceType = 0n, deadline = 0n, relayer = constants.ZERO_ADDRESS.toString(), nonce = 0n, })
```

#### parameters

* `nonceType(`<mark style="color:purple;">`` `BigInt` ``</mark>`)` -&#x20;
* `subscriptionRate(`<mark style="color:purple;">`number`</mark>`)` -
* relayer`(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` -&#x20;
* `deadline(`<mark style="color:purple;">`BigInt`</mark>`)` -&#x20;

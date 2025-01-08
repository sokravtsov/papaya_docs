---
description: Class for using read-only methods of Papaya Contract
---

# PapayaGetter

***

### <mark style="color:blue;">constructor</mark>

```typescript
constructor({papayaAddress: string, provider?: JsonRpcProvider })
```

#### parameters

* `papayaAddress(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` - smart-contract address
* `provider( JsonRpcProvider )` - jsonRpc blockchain provider from [**ethers.js**](https://docs.ethers.org/v5/api/providers/jsonrpc-provider/)

#### usage

```typescript
import { PapayaGetter } from "@papaya-metaverse/papaya-sdk"

const papayaGetter = new PapayaGetter({
    papayaAddress: "0x1c3E45F2D9Dd65ceb6a644A646337015119952ff",
    provider:  new JsonRpcProvider("https://polygon.infura.io/v3/${INFURA_API_KEY}")
})
```

{% hint style="info" %}
When using in browser, there is no need to specify `rpcUrl` since the `window.ethereum` provider is taken internally.

```typescript
const papayaGetter = new PapayaGetter({
    papayaAddress: "0x1c3E45F2D9Dd65ceb6a644A646337015119952ff"
})
```
{% endhint %}

***

### <mark style="color:blue;">allSubscriptions</mark>

#### description

To know the subscriptions of a particular user, use the `allSubscription` method, which returns arrays of addresses and encoded subscription data (cost, author’s share, project number).

```typescript
allSubscriptions(user: string): Promise<{ address: string[]; encodedRates: BigInt[] }>
```

#### parameters

* `user(`<mark style="color:purple;">`string`</mark>`)` - address of certain user

#### usage

```typescript
//...

(async () => {
    const allSubscriptions = await papayaGetter.allSubscriptions(
        "0x1234567890123456789012345678901234567890"
    )
})()
```

***

### <mark style="color:blue;">balanceOf</mark>

#### description

The standard method for ERC 20 shows the balance, but with some changes. Due to the fact that streams change the balance every second, this method will show the current balance, even if there was no synchronization

```typescript
balanceOf(projectId: number): Promise<BigInt>
```

#### parameters

* `projectId(`<mark style="color:purple;">`number`</mark>`)` - unique number of project

#### usage

```typescript
//...

(async () => {
    const balance = await papayaGetter.balanceOf(
        "0x1234567890123456789012345678901234567890"
    )
})()
```

***

### <mark style="color:blue;">getUserSettings</mark>

#### description

If the settings of a specific user are set, you can familiarize yourself with them using this method

```typescript
getUserSettings(projectId: number, user: string): Promise<{ initialized: boolean; projectFee: BigInt }>
```

#### parameters

* `projectId(`<mark style="color:purple;">`number`</mark>`)` - number of certain projectId
* `user(`<mark style="color:purple;">`string`</mark>`)` - address of certain user

#### usage

```typescript
//...

(async () => {
    const userSettings = await papayaGetter.getUserSettings(
        "0",
        "0x1234567890123456789012345678901234567890"
    )
})()
```

***

### <mark style="color:blue;">getAllProjectOwners</mark>

#### description

This method returns an array of addresses that are the owners of the projects

```typescript
getAllProjectOwners(): Promise<string[]>
```

#### usage

```typescript
//...

(async () => {
    const allProjectOwners = await papayaGetter.getAllProjectOwners()
})()
```

***

### <mark style="color:blue;">getUser</mark>

#### description

This method returns four fields: balance, incoming stream, outgoing stream, last synchronization timestamp. Note: Since user balance synchronization occurs on request, balance data may be outdated.

```typescript
getUser(user: string): Promise<{ balance: BigInt; incomeRate: BigInt; outgoingRate: BigInt; updated: BigInt; }>
```

#### parameters

* `user(`<mark style="color:purple;">`string`</mark>`)` - address of certain user

#### usage

```typescript
//...

(async () => {
    const user = await papayaGetter.getUser(
        "0x1234567890123456789012345678901234567890"
    )
})()
```

***

### <mark style="color:blue;">FLOOR</mark>

#### description

This method returns the floor of every calculation, it is necessary to calculate the value of assets and fees

```typescript
FLOOR(): Promise<BigInt>
```

***

### <mark style="color:blue;">MAX\_PROTOCOL\_FEE</mark>

#### description

This method returns the maximum possible fee value

```typescript
MAX_PROTOCOL_FEE(): Promise<BigInt>
```

***

### <mark style="color:blue;">APPROX\_LIQUIDATE\_GAS</mark>

#### description

This method returns the approximate cost of completing the liquidation if the person does not have subscriptions.

```typescript
APPROX_LIQUIDATE_GAS(): Promise<BigInt>
```

***

### <mark style="color:blue;">APPROX\_SUBSCRIPTION\_GAS</mark>

#### description

This method returns the approximate cost of performing liquidation for each subscription

```typescript
APPROX_SUBSCRIPTION_GAS(): Promise<BigInt>
```

***

### <mark style="color:blue;">SUBSCRIPTION\_THRESHOLD</mark>

#### description

This method returns the maximum possible count of subcriptions per user

```typescript
SUBSCRIPTION_THRESHOLD(): Promise<BigInt>
```

***

### <mark style="color:blue;">COIN\_PRICE\_FEED</mark>

#### description

This method returns address of coin price feed, that used in smart-contract

```typescript
COIN_PRICE_FEED(): Promise<string>
```

***

### <mark style="color:blue;">TOKEN\_PRICE\_FEED</mark>

#### description

This method returns address of token price feed, that used in smart-contract

```typescript
TOKEN_PRICE_FEED(): Promise<string>
```

***

### <mark style="color:blue;">TOKEN</mark>

#### description

This method returns address of underlying token, because we masked it into pp\*, where \* is an asset name

```typescript
TOKEN(): Promise<string>
```

***

### <mark style="color:blue;">DECIMALS\_SCALE</mark>

#### description

This method returns the number for which the token was needed to be converted to the form 1e18

```typescript
DECIMALS_SCALE(): Promise<BigInt>
```

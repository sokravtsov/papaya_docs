---
description: Class for using writable methods of Papaya Contract
---

# PapayaInteraction

***

### <mark style="color:blue;">constructor</mark>

```typescript
constructor({papayaAddress: string, provider?: JsonRpcProvider, secretKey?: string}) 
```

#### parameters

* `papayaAddress(`<mark style="color:purple;">`` `0x{string}` ``</mark>`)` - smart-contract address
* `provider( JsonRpcProvider )` - jsonRpc blockchain provider from [**ethers.js**](https://docs.ethers.org/v5/api/providers/jsonrpc-provider/)
* `secretKey(`<mark style="color:purple;">`string`</mark>`)` - wallet private key

{% hint style="info" %}
**secretKey** and **rpcUrl** are mostly made for the NodeJS environment. It is not recommended to use them in browser.
{% endhint %}

#### usage

```typescript
import { PapayaInteraction } from "@papaya-metaverse/papaya-sdk"

const papayaInteraction = new PapayaInteraction({
    papayaAddress: "0x1c3E45F2D9Dd65ceb6a644A646337015119952ff",
    provider:  new JsonRpcProvider("https://polygon.infura.io/v3/${INFURA_API_KEY}"),
    //secretKey: "<WALLET_PRIVATE_KEY>" - only when there is no way to allow users to connect their wallets
})
```

***

### <mark style="color:blue;">claimProjectId</mark>

#### description

This method assigns a unique number to your wallet, it needed for current functionality of projects

```typescript
claimProjectId(): Promise<string>
```

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.claimProjectId()
})()
</code></pre>

***

### <mark style="color:blue;">setDefaultSettings</mark>

#### description

The default settings are the fee settings that will be set for all users of your project

#### parameters

```typescript
setDefaultSettings(initialized = true, projectFee: number, projectId: number): Promise<string>
```

* `initialized(`<mark style="color:purple;">`boolean`</mark>`)` - unambiguously determine that the settings have been set
* `projectFee(`<mark style="color:purple;">`number`</mark>`)` - the amount of fee
* `projectId(`<mark style="color:purple;">`number`</mark>`)` - unique number of project

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.setDefaultSettings(
        true,
        10,
        0
    )
})()
</code></pre>

***

### <mark style="color:blue;">setSettingsForUser</mark>

#### description

The settings of a specific user allow you to set up the fee more precisely in relation to a specific wallet, this is necessary, for example, in cases of interaction with opinion leaders

```typescript
setSettingsForUser(user: string, initialized = true, projectFee: number, projectId: number): Promise<string>
```

#### parameters

* `user(`<mark style="color:purple;">`string`</mark>`)` - address of certain user
* `initialized(`<mark style="color:purple;">`boolean`</mark>`)` - unambiguously determine that the settings have been set
* `projectFee(`<mark style="color:purple;">`number`</mark>`)` - the amount of fee
* `projectId(`<mark style="color:purple;">`number`</mark>`)` - unique number of project

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.setSettingsForUser(
        "0x1234567890123456789012345678901234567890",
        true,
        20,
        0
    )
})()
</code></pre>

***

### <mark style="color:blue;">deposit</mark>

#### description

Allows depositing funds into the contract. To use this method, you must first approve the necessary amount of tokens for the Papaya contract.

```typescript
deposit(amount: number, isPermit2 = false): Promise<string>
```

#### parameters

* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `isPermit2(`<mark style="color:purple;">`boolean`</mark>`)` - a flag indicating the specificity of the token

{% hint style="info" %}
This flag is usually set to false, due to the fact that there are quite a few tokens with permit2 support
{% endhint %}

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.deposit(1*(10**18), false)
})()
</code></pre>

***

### <mark style="color:blue;">depositFor</mark>

#### description

This method is used if you need to deposit funds into another user's account, this is necessary in case of integration of third-party paid systems, for example fiat on ramp

```typescript
depositFor(amount: number, to: string, isPermit2 = false): Promise<string>
```

#### parameters

* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds
* `to(`<mark style="color:purple;">`string`</mark>`)` - address of receiever
* `isPermit2(`<mark style="color:purple;">`boolean`</mark>`)` - a flag indicating the specificity of the token

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.depositFor(
        1*(10**18),
        "0x1234567890123456789012345678901234567890",
        false
    )
})()
</code></pre>

***

### <mark style="color:blue;">withdraw</mark>

#### description

Allows withdrawing your funds at any time. When this method is called, your balance will be synchronized, and you can withdraw any available amount.

```typescript
withdraw(amount: number): Promise<string>
```

#### parameters

* `amount (`<mark style="color:purple;">`number`</mark>`)` - amount of funds

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.withdraw(1*(10**18))
})()
</code></pre>

***

### <mark style="color:blue;">withdrawTo</mark>

#### description

This method is used if you want to withdraw your funds to another wallet

```typescript
withdrawTo(to: string, amount: number): Promise<string>
```

#### parameters

* `to(`<mark style="color:purple;">`string`</mark>`)` - address of receiver
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.withdrawTo(
    "0x1234567890123456789012345678901234567890",
    1*(10**18)
    )
})()
</code></pre>

***

### <mark style="color:blue;">pay</mark>

#### description

Allows sending funds without using the subscription mechanism, similar to the classic transfer method.

```typescript
pay(to: string, amount: number): Promise<string>
```

#### parameters

* `to(`<mark style="color:purple;">`string`</mark>`)` - address of receiver
* `amount(`<mark style="color:purple;">`number`</mark>`)` - amount of funds

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.pay(
    "0x1234567890123456789012345678901234567890",
    1*(10**18)
    )
})()
</code></pre>

***

### <mark style="color:blue;">subscribe</mark>

#### description

Responsible for creating and modifying subscriptions. Since it is impossible to efficiently predefine costs, users need to specify how much they want to pay monthly, for example.&#x20;

```typescript
subscribe(author: string, subscriptionRate: number, projectId: number): Promise<string>
```

#### parameters

* `author(`<mark style="color:purple;">`string`</mark>`)` - address of certain author
* `subscriptionRate(`<mark style="color:purple;">`number`</mark>`)` - the size of a per-second subscription
* `projectId(`<mark style="color:purple;">`number`</mark>`)` - unique number of project

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.subscribe(
        "0x1234567890123456789012345678901234567890",
        1*(10**18),
        0
    )
})()
</code></pre>

***

### <mark style="color:blue;">unsubscribe</mark>

#### description

Responsible for disabling a subscription. This method can be called at any time to stop payments from an individual user.

```typescript
unsubscribe(author: string): Promise<string>
```

#### parameters

* `author(`<mark style="color:purple;">`string`</mark>`)` - address of certain author

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.unsubscribe(
        "0x1234567890123456789012345678901234567890"
    )
})()
</code></pre>

***

### <mark style="color:blue;">liquidate</mark>

#### description

This method gives you access to liquidation mechanism. More information [here](../../protocol/liquidations.md)

#### parameters

```typescript
liquidate(target: string): Promise<string>
```

* `target(`<mark style="color:purple;">`string`</mark>`)` - address of user that would be liquidated

#### usage

<pre class="language-typescript"><code class="lang-typescript"><strong>//...
</strong><strong>
</strong><strong>(async () => {
</strong>    const transaction = await papayaInteraction.liquidate(
        "0x1234567890123456789012345678901234567890"
    )
})()
</code></pre>

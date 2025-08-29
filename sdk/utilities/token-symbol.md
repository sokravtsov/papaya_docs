---
description: Utility methods of the SDK for getting token information and configuration
---

# Token Symbol

### `getTokenSymbol()`

Gets the current token symbol used by the SDK instance.

```typescript
getTokenSymbol(): TokenSymbol
```

**Returns:** The current token symbol.

**Example:**

```typescript
const token = papaya.getTokenSymbol();
console.log(`Using token: ${token}`); // 'USDT'
```

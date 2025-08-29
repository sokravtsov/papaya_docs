---
description: Rate conversion functions of Papaya SDK for working with time periods
---

# Rate Conversion

{% hint style="info" %}
The Papaya Protocol stores subscription rates as per-second values (raw), but in applications, you'll typically want to display these as more human-readable periods like per month or per year.
{% endhint %}

### Rate Periods

The SDK exports a `RatePeriod` enum to represent different time periods:

```typescript
export enum RatePeriod {
  SECOND = 'second',
  HOUR = 'hour',
  DAY = 'day',
  WEEK = 'week',
  MONTH = 'month',
  YEAR = 'year'
}
```

These period values correspond to the following conversion factors (in seconds):

| Period | Seconds                 |
| ------ | ----------------------- |
| SECOND | 1                       |
| HOUR   | 3,600                   |
| DAY    | 86,400                  |
| WEEK   | 604,800                 |
| MONTH  | 2,628,000 (≈30.42 days) |
| YEAR   | 31,536,000 (365 days)   |

### `convertRatePerSecond()`

Converts an amount for a specific period (e.g., 10 USDT per month) to a per-second rate.

```typescript
function convertRatePerSecond(amount: string, period: RatePeriod): number
```

**Parameters:**

* `amount`: The rate amount as a string
* `period`: The time period for the rate (e.g., `RatePeriod.MONTH`)

**Returns:** The equivalent per-second rate as a number.

**Example:**

```typescript
// Convert 10 USDT per month to a per-second rate
const perSecondRate = convertRatePerSecond('10', RatePeriod.MONTH);
console.log(perSecondRate); // Very small number representing tokens per second
```

### `convertRateToPeriod()`

Converts a per-second rate to a rate for a specified period.

```typescript
function convertRateToPeriod(ratePerSecond: number, period: RatePeriod): number
```

**Parameters:**

* `ratePerSecond`: The per-second rate as a number
* `period`: The target time period (e.g., `RatePeriod.MONTH`)

**Returns:** The rate for the target period as a number.

**Example:**

```typescript
// Convert a per-second rate to a monthly rate
const monthlyRate = convertRateToPeriod(perSecondRate, RatePeriod.MONTH);
console.log(monthlyRate); // Approximately 10 (if perSecondRate was from previous example)
```

### Practical Example

```typescript
import { convertRatePerSecond, convertRateToPeriod, RatePeriod } from '@papaya_fi/sdk';

// User wants to subscribe to 25 USDT per month
const monthlyAmount = '25';
const perSecondRate = convertRatePerSecond(monthlyAmount, RatePeriod.MONTH);

// Use the per-second rate for subscription
await papaya.subscribe(creatorAddress, perSecondRate, RatePeriod.SECOND, projectId);

// Later, when getting subscription info
const userInfo = await papaya.getUserInfo();
const rawIncomeRate = userInfo.incomeRate;

// Convert back to human-readable format
const monthlyIncome = convertRateToPeriod(Number(rawIncomeRate), RatePeriod.MONTH);
console.log(`Monthly income: ${monthlyIncome} USDT`);
```

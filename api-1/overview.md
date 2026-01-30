# Overview

## What is Papaya Invoice Bot?

Papaya Bot is a Telegram-based cryptocurrency payment processing system that enables businesses and developers to accept recurring cryptocurrency payments through a simple API. The bot provides a seamless interface for users to pay for subscriptions and services using popular stablecoins like USDC and USDT on major blockchain networks such as Ethereum, Base, Polygon, BSC, etc.

## Key Features

* **API-based Invoice Creation**: Developers can create payment invoices programmatically through a REST API
* **Telegram Integration**: Users interact with the payment system directly through Telegram
* **Multi-chain Support**: Supports multiple blockchain networks including Polygon and Binance Smart Chain
* **Cryptocurrency Support**: Accepts popular stablecoins like USDC and USDT
* **Subscription Management**: Handles recurring payment subscriptions with automatic cancellation
* **Webhook Integration**: Sends real-time notifications when payments are processed
* **Security**: Implements HMAC signature verification for webhook security

## How It Works

### For Developers

{% stepper %}
{% step %}
#### Register your application

Register your application through the Telegram bot interface to get an API key.
{% endstep %}

{% step %}
#### Create invoices

Use the API to create payment invoices with specific amounts and billing periods.
{% endstep %}

{% step %}
#### Provide payment links

Share payment links with your users who can pay directly through Telegram.
{% endstep %}

{% step %}
#### Receive webhooks

Get notified when payments are processed through webhook callbacks.
{% endstep %}

{% step %}
#### Manage subscriptions

Track active subscriptions and handle cancellations via the API.
{% endstep %}
{% endstepper %}

### For Users

{% stepper %}
{% step %}
#### Receive a payment link

Get a payment link from a service provider.
{% endstep %}

{% step %}
#### Open in Telegram

Click the link to open the Papaya Bot.
{% endstep %}

{% step %}
#### Select payment method

Choose from supported cryptocurrencies and blockchain networks.
{% endstep %}

{% step %}
#### Connect wallet

Connect your cryptocurrency wallet via WalletConnect.
{% endstep %}

{% step %}
#### Complete payment

Approve the payment and complete the subscription setup.
{% endstep %}
{% endstepper %}

## Main Usage Flows

### Flow: Application Registration

{% stepper %}
{% step %}
#### Open the Telegram bot

User opens the Telegram bot.
{% endstep %}

{% step %}
#### Navigate to registration

Navigate to "Integrations" → "Register Application".
{% endstep %}

{% step %}
#### Provide application name

Provide the application name.
{% endstep %}

{% step %}
#### Set wallet address

Set the wallet address that will receive payments.
{% endstep %}

{% step %}
#### Configure webhook (optional)

Optionally configure a webhook URL for notifications.
{% endstep %}

{% step %}
#### Receive API key

Receive the API key for programmatic access.
{% endstep %}
{% endstepper %}

### Flow: Invoice Creation and Payment

{% stepper %}
{% step %}
#### Create invoice via API

Developer creates an invoice via the API with amount and period.
{% endstep %}

{% step %}
#### Receive invoice details

API returns an invoice ID and payment link.
{% endstep %}

{% step %}
#### Share payment link

Developer shares the payment link with the customer.
{% endstep %}

{% step %}
#### Open bot with pre-filled invoice

Customer clicks the link and opens the bot with a pre-filled invoice.
{% endstep %}

{% step %}
#### Select network and token

Customer selects blockchain network and token.
{% endstep %}

{% step %}
#### Connect wallet

Customer connects wallet via WalletConnect QR code.
{% endstep %}

{% step %}
#### Approve payment

Customer approves payment and completes subscription.
{% endstep %}

{% step %}
#### Webhook on blockchain event

A blockchain event triggers a webhook notification to the developer.
{% endstep %}
{% endstepper %}

### Flow: Subscription Management

{% stepper %}
{% step %}
#### Track subscriptions

Developer can track active subscriptions via the API.
{% endstep %}

{% step %}
#### Users view subscriptions

Users can view their subscriptions in the bot using "My Subscriptions".
{% endstep %}

{% step %}
#### Cancellation

Subscriptions can be canceled by the service provider or automatically when payments stop.
{% endstep %}

{% step %}
#### Webhook updates

Webhook notifications inform about subscription status changes.
{% endstep %}
{% endstepper %}

### Flow: Webhook Notifications

{% stepper %}
{% step %}
#### Identify application

When a payment is processed, the system identifies the associated application.
{% endstep %}

{% step %}
#### Send POST request

If a webhook URL is configured, the system sends a POST request with payment details.
{% endstep %}

{% step %}
#### Include HMAC signature

The request includes an HMAC signature for security verification.
{% endstep %}

{% step %}
#### Developer processes notification

Developer's system processes the notification and updates their records.
{% endstep %}

{% step %}
#### Handle cancellations

In case of subscription cancellation, appropriate actions are triggered.
{% endstep %}
{% endstepper %}

## Supported Cryptocurrencies and Networks

### Networks

* **Polygon**: Major blockchain network with low transaction fees
* **Binance Smart Chain**: High-performance blockchain with fast transactions

### Tokens

* **USDC**: USD Coin stablecoin
* **USDT**: Tether stablecoin

## Billing Periods

Invoices can be created with different billing periods:

* Daily
* Weekly
* Monthly (default)
* Yearly

## Security Features

* **API Key Authentication**: All API calls require a valid API key
* **HMAC Signatures**: Webhook requests include verifiable signatures
* **Wallet Verification**: Payment recipients are verified against registered applications
* **Transaction Tracking**: All payments are tracked with blockchain transaction hashes

## Integration Benefits

### For Developers

* Easy cryptocurrency payment integration without managing blockchain complexity
* Reliable payment processing with webhook notifications
* Flexible billing periods to match business models
* No need to manage cryptocurrency wallets directly

### For Users

* Familiar Telegram interface for payments
* Support for popular cryptocurrencies
* Secure wallet connection via WalletConnect
* Automatic subscription management

## Getting Started

{% stepper %}
{% step %}
#### Register

Start a chat with the Papaya Bot and register your application.
{% endstep %}

{% step %}
#### Configure

Set up your receiving wallet address and optional webhook URL.
{% endstep %}

{% step %}
#### Integrate

Use the API to create invoices in your application.
{% endstep %}

{% step %}
#### Test

Use test mode to verify your integration works correctly.
{% endstep %}

{% step %}
#### Go live

Switch to production mode when ready for real transactions.
{% endstep %}
{% endstepper %}

## Use Cases

* SaaS subscription payments in cryptocurrency
* Digital service payments
* Content access subscriptions
* Membership payments
* Any recurring payment scenario where cryptocurrency is preferred

This system provides a complete solution for businesses wanting to accept cryptocurrency payments without the complexity of direct blockchain integration.

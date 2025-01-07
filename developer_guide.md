
# **Developer Guide**

This guide provides detailed instructions for developers to integrate Papaya into their applications and services.

---

## **1. Getting Started**

### Prerequisites:
- Familiarity with blockchain technology and smart contracts.
- A crypto wallet (e.g., MetaMask) for testing.
- API credentials from the Papaya team (if required).

---

## **2. Integration Methods**

### **Payment Widget**
- Use Papaya’s pre-built widget for quick integration.
- Embed the widget on your checkout page with a few lines of code.

#### Example:
```html
<div id="papaya-widget"></div>
<script src="https://cdn.papaya.com/widget.js"></script>
<script>
  PapayaWidget.init({
    merchantId: "your-merchant-id",
    network: "ethereum",
  });
</script>
```

---

### **API Integration**
- For custom integrations, use Papaya’s REST API.

#### Example API Request:
**Endpoint**: `/create-stream`  
**Method**: `POST`  
**Payload**:
```json
{
  "merchantId": "your-merchant-id",
  "customerWallet": "0x123...",
  "amount": "100",
  "currency": "USDC",
  "frequency": "monthly"
}
```

**Response**:
```json
{
  "streamId": "stream_abc123",
  "status": "active",
  "nextPaymentDate": "2025-02-01T00:00:00Z"
}
```

---

## **3. Testing**

### **Using the Testnet**
- Configure your integration to work with testnet environments (e.g., Rinkeby for Ethereum).
- Test payment streams without real fund transfers.

### **Simulate Transactions**
- Use the Papaya dashboard to simulate customer subscriptions and ensure all functionalities work correctly.

---

## **4. Best Practices**

- **Secure Your API Keys**:  
  Always store API keys in a secure environment and avoid exposing them in your codebase.

- **Monitor Transactions**:  
  Use Papaya’s dashboard or API to monitor active payment streams and troubleshoot issues.

- **Stay Updated**:  
  Subscribe to Papaya’s developer newsletter to stay informed about API updates and new features.

---

## **5. Resources**

- **API Documentation**:  
  Access the full API documentation [here](https://docs.papaya.com/api).

- **Developer Support**:  
  Reach out to our support team for technical assistance or integration help.

- **Community Forum**:  
  Join the Papaya developer community [here](https://forum.papaya.com).

---

With Papaya’s developer tools and resources, integrating subscription payment streaming into your application is straightforward and scalable.

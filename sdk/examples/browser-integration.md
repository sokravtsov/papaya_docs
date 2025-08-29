---
description: Example of integrating Papaya SDK with a browser-based web application
---

# Browser Integration

{% hint style="info" %}
This example demonstrates how to integrate the Papaya SDK with a browser-based web application using a browser wallet like MetaMask.
{% endhint %}

```typescript
// App.tsx or App.jsx
import React, { useState, useEffect } from 'react';
import { ethers } from 'ethers';
import { PapayaSDK } from '@papaya_fi/sdk';

function App() {
  const [papaya, setPapaya] = useState(null);
  const [account, setAccount] = useState('');
  const [balance, setBalance] = useState('0');
  const [loading, setLoading] = useState(true);
  
  // Initialize SDK when the component mounts
  useEffect(() => {
    async function initializePapaya() {
      if (window.ethereum) {
        try {
          // Request account access
          await window.ethereum.request({ method: 'eth_requestAccounts' });
          
          const provider = new ethers.BrowserProvider(window.ethereum);
          const signer = await provider.getSigner();
          const userAddress = await signer.getAddress();
          
          // Create Papaya SDK instance
          const papayaInstance = PapayaSDK.create(signer, 'polygon', 'USDT');
          
          // Get user balance
          const userBalance = await papayaInstance.balanceOf();
          
          setPapaya(papayaInstance);
          setAccount(userAddress);
          setBalance(userBalance.toString());
          setLoading(false);
        } catch (error) {
          console.error('Error initializing Papaya SDK:', error);
          setLoading(false);
        }
      } else {
        console.log('Please install MetaMask!');
        setLoading(false);
      }
    }
    
    initializePapaya();
  }, []);
  
  // Function to handle deposits
  async function handleDeposit() {
    if (!papaya) return;
    
    try {
      const tx = await papaya.deposit(10); // Deposit 10 USDT
      await tx.wait();
      
      // Update balance
      const newBalance = await papaya.balanceOf();
      setBalance(newBalance.toString());
      
      alert('Deposit successful!');
    } catch (error) {
      console.error('Error depositing funds:', error);
      alert('Error depositing funds. See console for details.');
    }
  }
  
  return (
    <div className="App">
      <h1>Papaya SDK Demo</h1>
      
      {loading ? (
        <p>Loading...</p>
      ) : (
        <>
          <p>Connected account: {account}</p>
          <p>Your balance: {balance} USDT</p>
          
          <button onClick={handleDeposit}>
            Deposit 10 USDT
          </button>
        </>
      )}
    </div>
  );
}

export default App;
```

### Key Points

1. **Check for MetaMask**: Check for `window.ethereum` before initialization
2. **Request account access**: Use `eth_requestAccounts` to get permission
3. **Create provider**: Use `BrowserProvider` to connect to MetaMask
4. **Error handling**: Wrap all operations in try/catch blocks
5. **Update UI**: Update state after successful transactions

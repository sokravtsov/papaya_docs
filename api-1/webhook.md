# Webhook

## Overview

Webhooks are automated messages sent from our system to your application when specific events occur in your registered application. These events include successful payment processing, subscription creation, and subscription revocation.

Additionally, you can now retrieve subscription information using our new API endpoints (see API Reference documentation for details). When blockchain events occur for applications without a configured webhook URL, the system will still process the events (such as deactivating subscriptions when streams are revoked) but will not send webhook notifications.

## How Webhooks Work

{% stepper %}
{% step %}
### Register your app and configure webhook

You register your application with our system and configure a webhook URL.
{% endstep %}

{% step %}
### Events trigger HTTP POST

When specific blockchain events occur (like payments or subscription changes), our system sends an HTTP POST request to your configured webhook URL.
{% endstep %}

{% step %}
### Request contains event and signature

The request contains event data and a security signature for verification.
{% endstep %}

{% step %}
### Process the payload

Your application processes the webhook payload and takes appropriate action.
{% endstep %}
{% endstepper %}

## Event Types

The following events trigger webhook calls:

* **stream\_created**: Triggered when a new subscription payment stream is created (i.e., a user successfully pays for a subscription)
* **stream\_revoked**: Triggered when a subscription is revoked or canceled

Webhooks are only sent for events related to registered applications that have a webhook URL configured. Events for applications without a configured webhook URL will still be processed (e.g., subscriptions will be deactivated when streams are revoked), but no webhook will be sent.

## Webhook Configuration

### Setting Up Your Webhook URL

{% stepper %}
{% step %}
Register your application through the Papaya Telegram bot.
{% endstep %}

{% step %}
Navigate to your app details in the bot menu.
{% endstep %}

{% step %}
Select "Изменить Webhook URL" (Change Webhook URL).
{% endstep %}

{% step %}
Enter your webhook endpoint URL.
{% endstep %}

{% step %}
For production apps, HTTPS is required.
{% endstep %}
{% endstepper %}

### Webhook URL Requirements

* **Protocol**: HTTP or HTTPS (HTTPS required for Production mode)
* **Format**: Must be a valid URL (e.g., `https://yourdomain.com/webhook`)
* **Availability**: Must be publicly accessible from the internet
* **Security**: Should validate the HMAC signature in the request header

Note: Webhooks are only sent for blockchain events related to applications that have a webhook URL configured. Events for applications without a configured webhook URL will still be processed (e.g., subscriptions will be deactivated when streams are revoked), but no webhook notification will be sent.

## Webhook Payload Structure

Each webhook request contains a JSON payload with the following structure:

```json
{
  "updateId": "transaction-hash-string",
  "updateType": "stream_created|stream_revoked",
  "requestDate": "2023-12-23T10:00:00.0000000Z",
  "payload": {
    // Invoice object details
  }
}
```

### Payload Fields

* **updateId**: The blockchain transaction hash that triggered the event
* **updateType**: The type of event (`stream_created` or `stream_revoked`)
* **requestDate**: ISO 8601 formatted timestamp of when the webhook was sent
* **payload**: Complete invoice object containing payment details

## Security: Verifying Webhook Signatures

All webhook requests include an HMAC signature in the `X-Pay-Signature` header for security verification.

### Signature Generation

The signature is generated using the invoice's transaction hash as the data and your API key as the secret:

```
Signature = HMAC-SHA256(transaction_hash, api_key)
```

Where:

* `transaction_hash` is the `updateId` field from the webhook payload
* `api_key` is your application's API key

### Signature Verification Process

{% stepper %}
{% step %}
Receive the webhook request body as a raw string.
{% endstep %}

{% step %}
Extract the `updateId` field from the JSON payload.
{% endstep %}

{% step %}
Use your API key as the secret to generate an HMAC-SHA256 hash of the updateId.
{% endstep %}

{% step %}
Compare the generated signature with the one in the `X-Pay-Signature` header.
{% endstep %}
{% endstepper %}

### Examples Verification Code

#### .Net (C#)

```csharp
public class WebhookController : ControllerBase
{
    private readonly string _apiKey; // Your application's API key
    
    [HttpPost("webhook")]
    public async Task<IActionResult> HandleWebhook([FromBody] dynamic payload, [FromHeader] string xPaySignature)
    {
        // Extract the updateId from the payload
        var updateId = payload.updateId?.ToString();
        
        if (string.IsNullOrEmpty(updateId))
        {
            return BadRequest("Invalid payload: updateId is required");
        }
        
        // Generate expected signature using the updateId and your API key
        var expectedSignature = GenerateHmacSignature(updateId, _apiKey);
        
        // Verify the signature
        if (!VerifySignature(expectedSignature, xPaySignature))
        {
            return Unauthorized("Invalid signature");
        }
        
        // Process the webhook
        // ... your processing logic here ...
        
        return Ok();
    }
    
    private string GenerateHmacSignature(string data, string secret)
    {
        using var hmac = new HMACSHA256(Encoding.UTF8.GetBytes(secret));
        var hash = hmac.ComputeHash(Encoding.UTF8.GetBytes(data));
        return Convert.ToHexString(hash).ToLower();
    }
    
    private bool VerifySignature(string expected, string actual)
    {
        return expected.Equals(actual, StringComparison.OrdinalIgnoreCase);
    }
}
```

#### Node.js

```javascript
const crypto = require('crypto');

function verifySignature(updateId, signature, secret) {
  const expectedSignature = crypto
    .createHmac('sha256', secret)
    .update(updateId, 'utf8')
    .digest('hex');
    
  return crypto.timingSafeEqual(
    Buffer.from(expectedSignature, 'hex'),
    Buffer.from(signature, 'hex')
  );
}

app.post('/webhook', express.json(), (req, res) => {
  const signature = req.get('X-Pay-Signature');
  const { updateId } = req.body;
  
  if (!updateId) {
    return res.status(400).send('Invalid payload: updateId is required');
  }
  
  if (!verifySignature(updateId, signature, process.env.API_KEY)) {
    return res.status(401).send('Invalid signature');
  }
  
  // Process the webhook
  // ... your processing logic here ...
  
  res.status(200).send('OK');
});
```

#### FastAPI (Python)

```python
from fastapi import FastAPI, Request, HTTPException
from pydantic import BaseModel
import hashlib
import hmac
import json

app = FastAPI()

API_KEY = "your-api-key-here"  # Your application's API key

@app.post("/webhook")
async def handle_webhook(request: Request):
    # Get the raw body for signature verification
    body = await request.body()
    body_str = body.decode("utf-8")
    
    # Parse the JSON to extract updateId
    payload = json.loads(body_str)
    update_id = payload.get("updateId")
    
    if not update_id:
        raise HTTPException(status_code=400, detail="Invalid payload: updateId is required")
    
    # Get the signature from headers
    signature = request.headers.get("X-Pay-Signature")
    
    if not signature:
        raise HTTPException(status_code=401, detail="Missing signature")
    
    # Verify the signature
    expected_signature = hmac.new(
        API_KEY.encode("utf-8"),
        update_id.encode("utf-8"),
        hashlib.sha256
    ).hexdigest().lower()
    
    if not hmac.compare_digest(expected_signature, signature.lower()):
        raise HTTPException(status_code=401, detail="Invalid signature")
    
    # Process the webhook
    # ... your processing logic here ...
    
    return {"status": "success"}
```

#### Django (Python)

```python
import hashlib
import hmac
import json
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from django.views.decorators.http import require_http_methods

API_KEY = "your-api-key-here"  # Your application's API key

@csrf_exempt
@require_http_methods(["POST"])
def webhook_view(request):
    if request.content_type != 'application/json':
        return JsonResponse({'error': 'Invalid content type'}, status=400)
    
    try:
        # Get the raw body for signature verification
        body = request.body.decode('utf-8')
        payload = json.loads(body)
        update_id = payload.get('updateId')
        
        if not update_id:
            return JsonResponse({'error': 'Invalid payload: updateId is required'}, status=400)
        
        # Get the signature from headers
        signature = request.META.get('HTTP_X_PAY_SIGNATURE')
        
        if not signature:
            return JsonResponse({'error': 'Missing signature'}, status=401)
        
        # Verify the signature
        expected_signature = hmac.new(
            API_KEY.encode('utf-8'),
            update_id.encode('utf-8'),
            hashlib.sha256
        ).hexdigest().lower()
        
        if not hmac.compare_digest(expected_signature, signature.lower()):
            return JsonResponse({'error': 'Invalid signature'}, status=401)
        
        # Process the webhook
        # ... your processing logic here ...
        
        return JsonResponse({'status': 'success'})
        
    except json.JSONDecodeError:
        return JsonResponse({'error': 'Invalid JSON'}, status=400)
    except Exception as e:
        return JsonResponse({'error': str(e)}, status=500)
```

#### Java (Spring Boot)

```java
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import java.util.Map;

@RestController
public class WebhookController {
    
    private static final String API_KEY = "your-api-key-here"; // Your application's API key
    
    @PostMapping("/webhook")
    public ResponseEntity<String> handleWebhook(@RequestBody Map<String, Object> payload,
                                               @RequestHeader("X-Pay-Signature") String signature) {
        try {
            // Extract updateId from the payload
            Object updateIdObj = payload.get("updateId");
            if (updateIdObj == null) {
                return ResponseEntity.badRequest()
                    .body("{\"error\": \"Invalid payload: updateId is required\"}");
            }
            String updateId = updateIdObj.toString();
            
            // Verify the signature
            String expectedSignature = generateHmacSignature(updateId, API_KEY);
            
            if (!secureCompare(expectedSignature, signature)) {
                return ResponseEntity.status(401)
                    .body("{\"error\": \"Invalid signature\"}");
            }
            
            // Process the webhook
            // ... your processing logic here ...
            
            return ResponseEntity.ok("{\"status\": \"success\"}");
            
        } catch (Exception e) {
            return ResponseEntity.status(500)
                .body("{\"error\": \"" + e.getMessage() + "\"}");
        }
    }
    
    private String generateHmacSignature(String data, String secret) 
            throws NoSuchAlgorithmException, InvalidKeyException {
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec secretKeySpec = new SecretKeySpec(
            secret.getBytes(StandardCharsets.UTF_8), "HmacSHA256");
        mac.init(secretKeySpec);
        byte[] hash = mac.doFinal(data.getBytes(StandardCharsets.UTF_8));
        
        // Convert to hex string and convert to lowercase
        StringBuilder result = new StringBuilder();
        for (byte b : hash) {
            result.append(String.format("%02x", b));
        }
        return result.toString();
    }
    
    private boolean secureCompare(String expected, String actual) {
        return expected.equalsIgnoreCase(actual);
    }
}
```

## Example Webhook Payloads

### Stream Created Event

```json
{
  "updateId": "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  "updateType": "stream_created",
  "requestDate": "2023-12-23T10:00:00.0000000Z",
  "payload": {
    "id": 123,
    "recipient": "0x742d35Cc6634C0532925a3b844Bc454e443867b4",
    "rate": "10.50",
    "isPaid": true,
    "tx": "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
    "createdAt": "2023-12-23T09:30:00.0000000Z",
    "metadata": {
      "userId": 12345,
      "planId": "premium"
    }
  }
}
```

### Stream Revoked Event

```json
{
  "updateId": "0xabcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890",
  "updateType": "stream_revoked",
  "requestDate": "2023-12-23T11:00:00.0000000Z",
  "payload": {
    "id": 123,
    "recipient": "0x742d35Cc6634C0532925a3b844Bc454e443867b4",
    "rate": "10.50",
    "isPaid": true,
    "tx": "0xabcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890",
    "createdAt": "2023-12-23T09:30:00.0000000Z",
    "metadata": {
      "userId": 12345,
      "planId": "premium"
    }
  }
}
```

## Error Handling and Retries

Our system implements retry logic for webhook delivery:

* If your webhook endpoint returns a non-successful HTTP status code (not 2xx), the system will retry the request
* Retry attempts: 3 attempts with 1-minute intervals between attempts
* If all retries fail, the webhook will not be resent

When a `stream_revoked` event is received but no webhook URL is configured for the application, the system will automatically deactivate the corresponding subscription in the database without sending a webhook.

## Testing Webhooks

### Test Mode vs Production Mode

* **Test Mode**: Webhook URLs can use HTTP or HTTPS protocols
* **Production Mode**: Webhook URLs must use HTTPS protocol

### Testing Your Webhook

{% stepper %}
{% step %}
Register your application in the Telegram bot.
{% endstep %}

{% step %}
Set your webhook URL to a testing endpoint (like RequestBin or webhook.site).
{% endstep %}

{% step %}
Perform a test transaction.
{% endstep %}

{% step %}
Monitor your testing endpoint to see the webhook payload.
{% endstep %}
{% endstepper %}

## Troubleshooting

### Common Issues

{% stepper %}
{% step %}
Webhook not being received:

* Verify your URL is publicly accessible
* Check that your server is properly configured to handle POST requests
* Ensure your webhook URL is correctly set in the bot
{% endstep %}

{% step %}
Signature verification failing:

* Confirm you're using the correct API key
* Ensure you're hashing the raw request body, not a parsed version
* Check that your HMAC implementation matches the expected format
{% endstep %}

{% step %}
Webhook returning 404:

* Verify your endpoint path is correct
* Ensure your server is running and accessible
{% endstep %}
{% endstepper %}

### Debugging Tips

* Use logging to capture incoming webhook requests and their headers
* Verify that your endpoint accepts POST requests
* Check that your server handles JSON content type properly
* Monitor your server logs for any errors during webhook processing

## Best Practices

{% stepper %}
{% step %}
Always verify signatures to ensure webhook authenticity.
{% endstep %}

{% step %}
Respond quickly to webhook requests (within 10 seconds).
{% endstep %}

{% step %}
Use HTTPS endpoints in production environments.
{% endstep %}

{% step %}
Log webhook events for debugging and monitoring.
{% endstep %}

{% step %}
Handle duplicate events gracefully (the same event might be sent multiple times).
{% endstep %}

{% step %}
Validate payload data before processing.
{% endstep %}

{% step %}
Implement idempotency to prevent duplicate processing of the same event.
{% endstep %}
{% endstepper %}

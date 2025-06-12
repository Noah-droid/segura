# Segura Payment Gateway API Documentation

### Environment Endpoints
- **Test Environment:** `https://api-dev.segura-pay.com/api/v1/payment-gateway/initialize`
- **Production Environment:** `https://api.segura-pay.com/api/v1/payment-gateway/initialize`


### Initialize Payment Endpoint

```
POST https://api-dev.segura-pay.com/api/v1/payment-gateway/initialize
```

### Request Headers
| Key | Value |
|-----|-------|
| `AuthKey` | `<EncodedAuthKey>` |
| `Content-Type` | `application/json` |

### Request Body
```json
{
  "amount": "string",          // Compulsory: Payment amount
  "customerId": "string",      // Compulsory: Unique customer identifier
  "currency": "string",        // Compulsory: Currency code (e.g., USD)
  "country": "string",         // Compulsory: Country code (e.g., NG)
  "callbackUrl": "string",     // Optional: Callback URL
  "customerName": "string",        // Compulsory: Customer's full name
  "email": "string",           // Optional: Customer's email
  "phoneNumber": "string",     // Compulsory: Customer's phone with country code
  "clientReference": "string",
  "clientId": "Your Test Client ID"
}
```

### Sample Request
```bash
curl -X POST https://api-dev.segura-pay.com/api/v1/payment-gateway/initialize \
-H "AuthKey:  <EncodedAuthKey>" \
-H "Content-Type: application/json" \
-d '{
  "amount": "8",
  "customerId": "customer101",
  "currency": "USD",
  "country": "NG",
  "callbackUrl": "https://localhost:3000/secure/payments",
  "fullName": "Noah James",
  "email": "noah@yopmail.com",
  "phoneNumber": "+9876543210"
}'
```

### Response
```json
{
  "requestTime": "2025-02-27T14:43:40.015052495",
  "status": true,
  "code": 200,
  "message": "Payment initiated successfully",
  "data": {
    "reference": "35ca5fa9-2848-47c1-ad78-44127751a24e",
    "amount": 800,
    "currency": "USD",
    "redirectUrl": "https://segura-web-dev.segura-pay.com/secure/payments?orderreference=35ca5fa9-2848-47c1-ad78-44127751a24e"
  }
}
```

### Payment Flow
1. Initialize payment using the endpoint above
2. Redirect user to the `redirectUrl` received in the response:
![alt text](image-4.png)
3. User completes payment on the Segura payment page
![alt text](image-5.png)


### Here is a demo where a user tries to make payment via our API

<iframe width="560" height="315" src="https://www.youtube.com/embed/IWQKdWizVac" title="Segura Gateway Integration Video" frameborder="0" allowfullscreen></iframe>

<br>


### Webhook Notifications
After transaction completion, Segura sends a webhook notification to your `callbackUrl` if provided with the following details:

```json
{
  "reference": "35ca5fa9-2848-47c1-ad78-44127751a24e",
  "status": "successful", // or "failed"
  "amount": 800,
  "currency": "USD",
  "customerReference": "customer101",
  "transactionTime": "2025-02-27T14:43:40.015Z"
}
```

### Webhook Requirements
1. Your `callbackUrl` should be:
   - Publicly accessible
   - Non-authenticated (no authorization headers required)
   - Respond with HTTP 200 OK status



<br>

## Check Payment Status

### Status Check Endpoint
```
GET https://api-dev.segura-pay.com/api/v1/payment-gateway/status/{reference}
```

Replace `{reference}` with the reference received from payment initialization.

### Request Headers
| Key | Value |
|-----|-------|
| `AuthKey` | ` <EncodedAuthKey>` |

### Sample Status Check
```bash
curl -X GET https://api-dev.segura-pay.com/api/v1/payment-gateway/status/35ca5fa9-2848-47c1-ad78-44127751a24e \
-H "AuthKey:  <EncodedAuthKey>"
```

## Important Notes
- The `redirectUrl` is a secure Segura-hosted payment page where customers enter their payment details
- Always store the `reference` to check payment status later
- Monitor the payment status endpoint to confirm successful transactions
- All amounts are processed in the smallest currency unit (e.g., cents for USD)
- Use test environment for development and testing
- Switch to production environment for live transactions
- Always implement webhook handling for reliable payment status updates
- Webhook endpoints must be publicly accessible
- Return HTTP 200 OK to acknowledge webhook receipt

See [Test Cards](./cards.md) for test payment data to use during integration.

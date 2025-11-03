# Check Payment Status

## Endpoint
```
GET https://api-dev.segura-pay.com/api/v1/payment-gateway/status/{reference}
```

| Path Parameter | Description                    |
|----------------|--------------------------------|
| `reference`    | The payment reference obtained from the initialization step. |

## Request Headers
| Key             | Value                        |
|-----------------|------------------------------|
| `AuthKey` | `Basic <EncodedAuthKey>`     |
| `Content-Type`  | `application/json`           |

### Example Header:
```bash
AuthKey: Basic <EncodedAuthKey>
Content-Type: application/json
```

## Sample Curl Request
```bash
curl -X GET https://api-dev.segura-pay.com/api/v1/payment-gateway/status/{reference} \
-H "AuthKey: Basic <EncodedAuthKey>" \
-H "Content-Type: application/json"
```

Replace `{reference}` with the actual payment reference.

## Response Example
```json
{
    "requestTime": "2025-02-03T19:10:22.396617921",
    "status": true,
    "code": 200,
    "message": "Payment retrieved successfully",
    "data": {
        "currency": "GBP",
        "amount": 500,
        "paymentReference": "84b8f6e4-582b-4b7b-8eb7-3522b090914d",
        "status": "PENDING",
        "statusDescription": "3DS Payment"
    }
}
```

## Response Fields
| Field                | Type    | Description                                    |
|----------------------|---------|------------------------------------------------|
| `requestTime`         | string  | Timestamp of the request                      |
| `status`              | boolean | `true` if the request was successful          |
| `code`                | number  | Status code                                   |
| `message`             | string  | Response message                              |
| `data.currency`       | string  | Currency of the payment                       |
| `data.amount`         | number  | Payment amount                                |
| `data.paymentReference` | string | Payment reference                             |
| `data.status`         | string  | Payment status (e.g., `success`, `failed`)   |


## Status Reference

| **Category** | **Status** | **Meaning** | **What It’s *Not*** |
|---------------|-------------|--------------|-----------------------|
| **Payment** | `pending` | Transaction has been initialized but not yet confirmed by the processor or customer. Funds are not yet captured. | Not a success or failure — it’s still in progress. Do not deliver value or mark order complete. |
| **Payment** | `success` | Payment has been verified and funds are confirmed. | Not subject to further confirmation; this is final. Do not retry or poll unnecessarily. |
| **Payment** | `failed` | Payment was declined, expired, or could not be processed. | Not reversible via polling — merchant should reinitiate payment. |
| **Webhook** | `success` | Webhook successfully delivered to merchant endpoint (HTTP 200 OK). | Doesn’t guarantee merchant processed it correctly — only that it was received. |
| **Webhook** | `failed` | Webhook delivery failed after all retry attempts (network errors, bad response, or endpoint unavailable). | Doesn’t mean payment failed — only that merchant’s system didn’t acknowledge receipt. |




## Notes:
- Replace `<EncodedAuthKey>` with your Base64-encoded `clientId:secret` string.
- The `status` field inside `data` represents the current payment status (e.g., `approved`, `pending`, `failed`).

**Segura Payment Gateway API** to process a payment:

---

# Process Payment

## Endpoint
```
POST /api/v1/payment-gateway/process
```

## Request Headers
| Key             | Value                        |
|-----------------|------------------------------|
| `AuthKey`       | `Basic <EncodedAuthKey>`     |
| `Content-Type`  | `application/json`           |

### Example Header:
```bash
AuthKey: Basic <EncodedAuthKey>
Content-Type: application/json
```

## Request Body (JSON)
```json
{
  "pan": "string",
  "cvv": "string",
  "expiryDate": "string",
  "securityCode": "string",
  "reference": "string"
}
```

| Field          | Type   | Description                           |
|----------------|--------|----------------------------------------|
| `pan`          | string | Card number                           |
| `cvv`          | string | Card CVV code                         |
| `expiryDate`   | string | Card expiry date (MM/YY or MM/YYYY)   |
| `securityCode` | string | Additional security code if required  |
| `reference`    | string | Payment reference from initialization |

## Sample Curl Request
```bash
curl -X POST https://api.segura.com/api/v1/payment-gateway/process \
-H "AuthKey: Basic <EncodedAuthKey>" \
-H "Content-Type: application/json" \
-d '{
  "pan": "1234567812345678",
  "cvv": "123",
  "expiryDate": "12/27",
  "securityCode": "123456",
  "reference": "REF123456789"
}'
```

## Response Example
```json
{
  "requestTime": "2025-02-14T09:04:54.330Z",
  "status": true,
  "code": 0,
  "message": "string",
  "data": {
    "success": true,
    "jwt": "string"
  }
}
```

## Notes:
- Replace `<EncodedAuthKey>` with your Base64-encoded `clientId:secret` string.
- Ensure the `reference` value matches the one obtained from the payment initialization step.
**Payment status** via the **Segura Payment Gateway API**:

---

# Check Payment Status

## Endpoint
```
GET /api/v1/payment-gateway/{reference}/status
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
curl -X GET https://api.segura.com/api/v1/payment-gateway/{reference}/status \
-H "AuthKey: Basic <EncodedAuthKey>" \
-H "Content-Type: application/json"
```

Replace `{reference}` with the actual payment reference.

## Response Example
```json
{
  "requestTime": "2025-02-14T09:34:43.084Z",
  "status": true,
  "code": 0,
  "message": "string",
  "data": {
    "currency": "string",
    "amount": 0,
    "paymentReference": "string",
    "status": "string"
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
| `data.status`         | string  | Payment status (e.g., `approved`, `failed`)   |

## Notes:
- Replace `<EncodedAuthKey>` with your Base64-encoded `clientId:secret` string.
- The `status` field inside `data` represents the current payment status (e.g., `approved`, `pending`, `failed`).
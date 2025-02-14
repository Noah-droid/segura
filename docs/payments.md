**Segura Payment Gateway API** to initialize a payment:

---

# Initialize Payment Endpoint
```
POST /api/v1/payment-gateway/initialize
```

## Request Headers
| Key             | Value                        |
|-----------------|------------------------------|
| `AuthKey` | ` <EncodedAuthKey>`     |
| `Content-Type`  | `application/json`           |

### Example Header:
```bash
AuthKey:  <EncodedAuthKey>
Content-Type: application/json
```

## Request Body (JSON)
```json
{
  "customerId": 95,
  "customerName": "mycomp@yopmail.com",
  "email": "myrmail@yopmail.com",
  "phoneNumber": "080333332222",
  "country": "NG",
  "currency": "NGN",
  "callbackUrl": "https://yourcallbackurl.com",
  "amount": 3000
}
```

| Field         | Type   | Description                        |
|---------------|--------|-------------------------------------|
| `customerId`  | integer| Customer's Id                       |
| `customerName`| string | Customer's Username                 |
| `email`       | string | Customer's email address            |
| `phoneNumber` | string | Customer's phone number             |
| `country`     | string | Customer's country                  |
| `currency`    | string | Currency code (e.g., `USD`, `NGN`) |
| `callbackUrl` | string | URL to receive payment updates      |
| `amount`      | number | Payment amount                      |


## Sample Curl Request
```bash
curl -X POST https://api.segura.com/api/v1/payment-gateway/initialize \
-H "AuthKey: Basic <EncodedAuthKey>" \
-H "Content-Type: application/json" \
-d '{
  "customerId": 95,
  "customerName": "mycomp@yopmail.com",
  "email": "myrmail@yopmail.com",
  "phoneNumber": "0027748242",
  "country": "NG",
  "currency": "NGN",
  "callbackUrl": "https://yourcallbackurl.com",
  "amount": 3000
}'
```

## Response
```json
{
    "requestTime":"2025-02-14T08:43:16.848166329",
    "status":true,
    "code":200,
    "message":"Payment initiated successfully",
    "data":{

        "reference":"5ab7840a-76b1-46b3-91e0-4a6489cc2501",
        
        "amount":3000,

        "currency":"NGN"}
        
        }
```

## Notes:
- Replace `<EncodedAuthKey>` with your Base64-encoded `clientId:secret` string.
- Ensure your callback URL is publicly accessible.


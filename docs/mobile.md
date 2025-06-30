# Segura Payment Gateway (Mobile Money) API Documentation

### Environment Endpoints
- **Test Environment:** `https://api-dev.segura-pay.com/api/v1/payment-gateway/collection-link?isNative=true`
- **Production Environment:** `https://api.segura-pay.com/api/v1/payment-gateway/collection-link?isNative=true`


## Create Collection Link

### Endpoint
```
POST https://api-dev.segura-pay.com/api/v1/payment-gateway/collection-link?isNative={true|false}
```

- **isNative** (query param):  
  - `true`: Returns a payment code for direct mobile money payment.
  - `false`: Returns a payment link for customer-initiated payment.

### Request Headers
| Key | Value |
|-----|-------|
| `AuthKey` | `<EncodedAuthKey>` |
| `Content-Type` | `application/json` |

### Request Body
```json
{
  "amount": 200,
  "currency": "XOF",
  "customerName": "Noah",
  "customerEmail": "noah@yopmail.com",
  "customerPhone": "0987654123",
  "description": "New Description",
  "mobileMoneyNumber": "0987654123",
  "country": "BENIN",
  "carrierName": "mtn-benin",
  "clientId": "test_CORP-TBCC1V-997359-20250505",
  "expiresAt": "2025-06-30T19:11:04.167Z"
}
```

### Sample Response (`isNative=true`)
```json
{
  "requestTime": "2025-06-30T21:15:16.633455505",
  "status": true,
  "code": 200,
  "message": "Collection processed successfully",
  "data": {
    "mobileMoneyPaymentCode": "B8A75D872E9F",
    "amount": 200,
    "currency": "XOF"
  }
}
```

### Sample Response (`isNative=false`)
```json
{
  "requestTime": "2025-06-30T21:16:52.361820917",
  "status": true,
  "code": 200,
  "message": "Collection link created successfully",
  "data": {
    "link": "https://segura-web-dev.segura-pay.com/secure/payments?currency=XOF&mobileMoneyPaymentCode=2F2970E525BC&amount=200&customerName=Noah&email=noah@yopmail.com"
  }
}
```



## Check Collection Status

### Status Endpoint
```
GET https://api-dev.segura-pay.com/api/v1/payment-gateway/collection-link/{reference}?isNative={true|false}
```

- Replace `{reference}` with the `mobileMoneyPaymentCode` received from the collection initiation response.

### Request Headers
| Key | Value |
|-----|-------|
| `AuthKey` | `<EncodedAuthKey>` |

### Sample Request
```bash
curl -X GET https://api-dev.segura-pay.com/api/v1/payment-gateway/collection-link/B8A75D872E9F?isNative={true|false} \
-H "AuthKey: <EncodedAuthKey>"
```

### Sample Response
```json
{
  "requestTime": "2025-06-30T21:36:54.791Z",
  "status": true,
  "code": 0,
  "message": "string",
  "data": {
    "paymentStatus": "string"
  }
}
```

> **Note:**  
> Use the `isNative` query parameter to control the collection method.  
> - If `isNative` is `true`, you will receive a payment code for direct mobile money collection.  
> - If `isNative` is `false`, you will receive a payment link to share with the customer.
> Use the `mobileMoneyPaymentCode` as the reference to check the status of a mobile money collection.

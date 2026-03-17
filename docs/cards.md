### Test Cards for 3D Secure (3DSv2) Testing
## 3DS Test Cards
| Card | PAN | Result | Scenario |
|------|-------------------|--------|------------------------|
| Visa | 4900490000000501 | Success | Frictionless |
| Visa | 4900490000000519 | Fail | Frictionless failure |
| Visa | 4900490000000527 | Success | Attempts stand-in |
| Visa | 4900490000000535 | Success | Unavailable auth |
| Visa | 4900490000000543 | Fail | Rejected auth |
| MC | 5591390000000504 | Success | Frictionless |
| MC | 5591390000000520 | Fail | Frictionless failure |
| Amex | 340000000004001 | Success | Frictionless |
| Amex | 340000000004019 | Fail | Frictionless failure |
| Discover | 6573700000000009 | Success | Frictionless |


## 2DS Test Cards
| PAN | Result | Scenario |
|-----------------|-------------------|--------|
|4111111111111111	| Auth success | settle status 0
|4000000000000002	| Auth declined|
|4000000000000010 |	Auth success |


## Common Settings (All Cards)
- **Expiry Date:** Any valid future date (e.g., **12/2028**)
- **CVV / CVC:**
  - **123** for Visa / Mastercard / Discover
  - **1234** for Amex

## Control Amounts
| Amount | Result |
|--------|--------|
| Any (e.g., 10.50) | Success |
| 700.00 | Decline |
| 600.10 | Bank system error |



## Postman Test Example
Use the following values when running a manual Postman test:

- **PAN:** 4900490000000501 (Visa, frictionless success)
- **Expiry:** 12/2028
- **CVV:** 123
- **Amount:** 5000 (represents 50.00 in smallest unit)

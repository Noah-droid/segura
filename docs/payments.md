## Segura Gateway HTML + JavaScript Integration Guide

This documentation provides an example implementation of the Segura Gateway. Below is the sample frontend code:

### Example HTML + JavaScript Integration
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <meta name="viewport" content="initial-scale=1,width=device-width"/>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>

    <script src="https://keepfxdev-bucket.fra1.cdn.digitaloceanspaces.com/segura-gateway-v1.js"></script>

    <script>
      document.addEventListener("DOMContentLoaded", function () {
        // Initialize the SeguraGateway
        const gateway = new Segura({
          authKey: "d2FsbGV0X3Rlc3RfY2xpZW50OiRjbGllbnQzNDUwMDA5JA==", // Required
          callbackUrl: "https://yourwebsite.com/payment-callback", // Optional, but recommended for webhook notifications 
          isNative: true, // Optional, defaults to true - determines whether to use Segura's UI or handle it from your end
        });

        // Attach event listener to the payment button
        document.getElementById("payButton").addEventListener("click", async function () {
          await gateway.startPayment({
            amount: 10,
            customerId: "customer123",
            currency: "USD",
            country: "NG", 
            customerName: "Abayomi Chinedu", 
            email: "abayomichinedu@email.com", 
            phoneNumber: "08123121234",
            // pass card details if isNative is False
            cvv: "123",
            pan: "5591390000000504",
            expiry: "12/2025" //  MM/YYYY
           
          });
        });
      });
    </script>
  </head>
  <body class="choice st-inputs-style st-blocks-style st-notify-style">
    <button id="payButton">Pay Now</button>
  </body>
</html>
```


### Native UI Mode Configuration

The `isNative` parameter controls how card details are collected:

#### When isNative: true (Default)
```javascript
const gateway = new Segura({
  authKey: "d2FsbGV0X3Rlc3RfY2xpZW50OiRjbGllbnQzNDUwMDA5JA==",
  isNative: true  // Uses Segura's built-in UI
});

await gateway.startPayment({
  amount: 10,
  customerId: "customer123",
  currency: "USD",
  country: "NG", 
  customerName: "Abayomi Chinedu", 
  email: "abayomichinedu@email.com", 
  phoneNumber: "08123121234",
// No need to pass card details
});
```

#### When isNative: false (Custom UI)
```javascript
const gateway = new Segura({
  authKey: "d2FsbGV0X3Rlc3RfY2xpZW50OiRjbGllbnQzNDUwMDA5JA==",
  isNative: false  // Use your own UI
});

await gateway.startPayment({
  amount: 10,
  customerId: "customer123",
  currency: "USD",
  country: "NG", 
  customerName: "Abayomi Chinedu", 
  email: "abayomichinedu@email.com", 
  phoneNumber: "08123121234",
// Card details required
  cvv: "123",
  pan: "5591390000000504",
  expiry: "12/2025" //  MM/YYYY
}); 
```



### Notes
- The `<script src="https://keepfxdev-bucket.fra1.cdn.digitaloceanspaces.com/segura-gateway-v1.js"></script>` loads an external JavaScript library required for the Segura Gateway.
- The `authKey` is mandatory for initializing the Segura Gateway.
- The `callbackUrl` is optional but recommended. It acts as a webhook URL where payment notifications will be sent.
- Gateway is subject to changes, hence always refer back for updates.

## Segura Gateway Integration Guide

### Introduction
Segura Gateway is a secure and efficient payment gateway that allows businesses to integrate seamless payment solutions into their platforms. This documentation provides an example implementation of the Segura Gateway and highlights key features of the code.

### Example HTML + JavaScript Integration
```html
<html >
  <head>
    <meta name="viewport" content="initial-scale=1,width=device-width" />
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <script src="https://keepfxdev-bucket.fra1.cdn.digitaloceanspaces.com/segura-gateway.js" defer></script>
  </head>
  <body class="choice st-inputs-style st-blocks-style st-notify-style">
    <button id="payButton">Pay Now</button>

    <script>
      document.addEventListener("DOMContentLoaded", function () {
        // Initialize Segura Gateway
        const gateway = new SeguraGateway({
          authKey: 'dGVzdF9DT1JQLURRQlRSTi03MDc3MjctMjAyNTAyMTM6dGVzdF9nbjBHUWVNcDY1WWJaTjdTb0haSnMyTmswajZqWDhvZk9rUTR6MThaN3pPMmFBWGhCZl98MDk5NTE=',
          callbackUrl: 'https://your-callback-url.com',
        });

        // Attach event listener to the payment button
        document.getElementById("payButton").addEventListener("click", async function () {
          await gateway.initializePayment({
            amount: 10,
            customerId: 'customer123',
            currency: 'NGN',
            country: 'NG',
            email: 'temire@email.com',
            phoneNumber: '08123121234',
          });
        });
      });
    </script>
  </body>
</html>
```

### Key Features Demonstrated in the Code
1. **Responsive Design:**
   - The `<meta name="viewport" ...>` tag ensures that the payment page is responsive across different devices.

2. **Character Encoding:**
   - The `<meta http-equiv="Content-Type" ...>` tag ensures proper character encoding (UTF-8).

3. **Script Tags:**
   - The `<script src="https://keepfxdev-bucket.fra1.cdn.digitaloceanspaces.com/segura-gateway.js" defer></script>` loads an external JavaScript library required for the Segura Gateway. The `defer` attribute ensures the script is executed only after the HTML is fully parsed.
   - The inline `<script>` block initializes the gateway and attaches a click event listener to the payment button. This block ensures the payment functionality is ready once the page is loaded.

4. **Gateway Initialization:**
   - The `SeguraGateway` object is instantiated with authentication and callback URL details.

5. **Event Handling:**
   - `DOMContentLoaded` ensures the DOM is fully loaded before attaching event listeners.
   - A `click` event listener is attached to the payment button to initiate the payment process.

6. **Payment Initialization:**
   - `gateway.initializePayment()` is called with customer details such as `amount`, `customerId`, `currency`, `country`, `email`, and `phoneNumber`.

### Security Note
- Always keep your `authKey` confidential and avoid exposing it on the client side in production.
- Validate and sanitize all inputs on the server side before processing payments.

### Conclusion
This example showcases the basic integration steps for embedding Segura Gateway into your web application. Developers are encouraged to consult the official Segura Gateway documentation for advanced features and security practices.


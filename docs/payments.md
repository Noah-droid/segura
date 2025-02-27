## Segura Gateway Integration Guide

### Introduction
Segura Gateway is a secure and efficient payment gateway that allows businesses to integrate seamless payment solutions into their platforms. This documentation provides an example implementation of the Segura Gateway and highlights key features of the code. Below is th HTML integration:

### Example HTML + JavaScript Integration
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <meta name="viewport" content="initial-scale=1,width=device-width"/>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<script src="http://pario.ng/segura/segura-wrapper-v1.js"></script>
<script>
  document.addEventListener("DOMContentLoaded", function () {
    // Initialize the SeguraGateway
    const gateway = new Segura({
      authKey: "d2FsbGV0X3Rlc3RfY2xpZW50OiRjbGllbnQzNDUwMDA5JA==",
      callbackUrl: "https://yourwebsite.com/payment-callback"
    });

    // Attach event listener to the payment button
    document.getElementById("payButton").addEventListener("click", async function () {
      await gateway.startPayment({
        amount: 10,
        customerId: "customer123",
        currency: "USD",
		country: "NG", 
		customerName: "Temire Emmanuel", 
		email: "temire@email.com", 
		phoneNumber: "08123121234"
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


### Key Features Demonstrated in the Code
1. **Responsive Design:**
   - The `<meta name="viewport" ...>` tag ensures that the payment page is responsive across different devices.

2. **Character Encoding:**
   - The `<meta http-equiv="Content-Type" ...>` tag ensures proper character encoding (UTF-8).

3. **Script Tags:**
   - The `<script src="https://pario.ng/segura/segura-wrapper-v1.js"></script>` loads an external JavaScript library required for the Segura Gateway. 
   - The inline `<script>` block initializes the gateway and attaches a click event listener to the payment button. This block ensures the payment functionality is ready once the page is loaded.

4. **Gateway Initialization:**
   - The `Segura` object is instantiated with authentication key and callback URL details.

5. **Event Handling:**
   - `DOMContentLoaded` ensures the DOM is fully loaded before attaching event listeners.
   - A click event listener is attached to the payment button to initiate the payment process.

6. **Payment Initialization:**
   - `gateway.startPayment()` is called with customer details such as amount, customerId, currency, country, email, and phoneNumber.

### Notes
- Gateway is subject to changes, hence always refer to the updated documentation. 
- Always keep your authKey confidential and avoid exposing it on the client side in production.
- Validate and sanitize all inputs on the server side before processing payments.



### Conclusion
This example showcases the basic integration steps for embedding Segura Gateway into your web application. Developers are encouraged to consult the official Segura Gateway documentation for advanced features and security practices.


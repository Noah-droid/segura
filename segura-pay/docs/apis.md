# API Authorization Key

To access the Segura Payment Gateway API, you need to obtain your API keys from the email sent to you upon registration. Follow these steps to generate the authorization key:

## 1. Retrieve your API Keys
Obtain your `clientId` and `secret` from the registration email.

## 2. Concatenate the Keys
Combine your keys in the following format:

```
clientId:secret
```

## 3. Convert the Concatenated String to Base64
You can use any tool or programming language to convert the string to Base64. Below is a Java example:

```java
import java.nio.charset.StandardCharsets;
import java.util.Base64;

public class AuthKeyGenerator {
    public static void main(String[] args) {
        String clientId = "test_CORP-DQBTRN-707727-20250213";
        String secret = "test_gn0GQeMp65YbZN7SoHZJs2Nk0j6jX8ofOkQ4z18Z7zO2aAXhBf_|09951";

        String authKey = clientId + ":" + secret;

        System.out.println("Auth Key: " + authKey);

        String encodedAuthKey = Base64.getEncoder().encodeToString(authKey.getBytes(StandardCharsets.UTF_8));

        System.out.println("Encoded Auth Key: " + encodedAuthKey);
    }
}
```

## 4. Use the Encoded Authorization Key
Include the encoded authorization key in your API requests as a header:

```
Authorization: AuthKey <EncodedAuthKey>
```

Replace `<EncodedAuthKey>` with the Base64-encoded string generated from the steps above.
# Credential Management API

The **Credential Management API** simplifies creating, storing, and retrieving user credentials, delivering secure and seamless authentication experiences for websites.

---

## Supported Credential Types

The API supports a variety of credential types tailored for different authentication needs:

| **Credential Type**               | **Interface**                                            | **Description**                                                                                                           |
| --------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Password**                      | `PasswordCredential`                                     | Manages traditional username-password combinations for secure authentication.                                             |
| **Federated Identity**            | `IdentityCredential`, `FederatedCredential` (deprecated) | Enables login through third-party identity providers like Google or Facebook.                                             |
| **One-Time Password (OTP)**       | `OTPCredential`                                          | Facilitates single-use passcode authentication, commonly sent via SMS or email.                                           |
| **Web Authentication (WebAuthn)** | `PublicKeyCredential`                                    | Provides advanced passwordless authentication using public-key cryptography, such as biometric or hardware security keys. |

---

## Credential Hierarchy

All credential types inherit from the `Credential` interface. This unified design allows shared functionality while accommodating specialized features for each credential type.

### Subclasses of `Credential`

| **Credential Type**       | **Subclass**          | **Use Case**                                                                  |
| ------------------------- | --------------------- | ----------------------------------------------------------------------------- |
| **Password Credential**   | `PasswordCredential`  | Standard username/password authentication.                                    |
| **Federated Credential**  | `FederatedCredential` | Third-party identity provider login (e.g., Google, Facebook).                 |
| **Public Key Credential** | `PublicKeyCredential` | Passwordless authentication using WebAuthn (e.g., biometrics, security keys). |

![img](https://developer.mozilla.org/en-US/docs/Web/API/Credential_Management_API/Credential_types/credential-types.svg)

---

### Implementing `PasswordCredential`

#### **Step 1: Create and Store Credentials**

Use the `navigator.credentials.store()` method to securely save user credentials after login.

```javascript
// Collect user login details
const username = document.querySelector("#username").value;
const password = document.querySelector("#password").value;

// Create a PasswordCredential object
const credentials = new PasswordCredential({
  id: username,
  password: password,
});

// Store the credentials securely
navigator.credentials
  .store(credentials)
  .then(() => {
    console.log("Credentials stored successfully!");
  })
  .catch((error) => {
    console.error("Failed to store credentials:", error);
  });
```

![image](https://developer.mozilla.org/en-US/docs/Web/API/Credential_Management_API/Credential_types/password-create.svg)

---

#### **Step 2: Retrieve Stored Credentials**

Retrieve saved credentials to enable auto-login or pre-fill login forms.

```javascript
navigator.credentials
  .get({ password: true })
  .then((credentials) => {
    if (credentials) {
      console.log("Retrieved credentials:", credentials);
      // Use the credentials for automatic login
      loginUser(credentials.id, credentials.password);
    } else {
      console.log("No saved credentials found.");
    }
  })
  .catch((error) => {
    console.error("Failed to retrieve credentials:", error);
  });

// Mock login function
function loginUser(username, password) {
  console.log(`Logging in user: ${username} with password: ${password}`);
}
```

![iamge](https://developer.mozilla.org/en-US/docs/Web/API/Credential_Management_API/Credential_types/password-get.svg)

---

#### **Step 3: Handle Logout**

Prevent automatic login by calling `navigator.credentials.preventSilentAccess()` during logout.

```javascript
navigator.credentials
  .preventSilentAccess()
  .then(() => {
    console.log("Silent access disabled. User must log in again.");
  })
  .catch((error) => {
    console.error("Failed to prevent silent access:", error);
  });
```

---

### Best Practices

1. **Use HTTPS**: The API requires secure HTTPS connections for functionality.
2. **Seek User Consent**: Clearly communicate before storing user credentials.
3. **Fallbacks for Compatibility**: Since not all browsers support this API, provide alternative methods like traditional login forms.
4. **Regularly Update Credentials**: Encourage users to update their credentials periodically to enhance security.
5. **Handle Errors Gracefully**: Implement robust error handling to manage issues during credential storage and retrieval.

To know more, look at [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Credential_Management_API)

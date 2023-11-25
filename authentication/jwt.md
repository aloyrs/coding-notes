## What is JWT (JSON Web Token)?

- **Definition:**

  - JWT is a compact, URL-safe means of representing claims between two parties. It is often used for authentication and authorization in web development.

- **Structure:**
  JWTs consist of three parts separated by dots (`.`):
  - Header
  - Payload
  - Signature.
- **Header:**

  - Contains information about how the JWT is encoded, typically specifying the type (`"typ"`) and the signing algorithm (`"alg"`).

- **Payload:**

  - Carries the claims. Claims are statements about an entity (typically, the user) and additional data.
  - Standard claims include issuer (`"iss"`), subject (`"sub"`), expiration time (`"exp"`), and others.

- **Signature:**

  - Used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.
  - Created by encoding the header, payload, and a secret key using the specified algorithm.

- **Example JWT:**
  - `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`
- **Use Case:**

  - Commonly used for authentication by exchanging information between parties, often after a user logs in. The token is then sent in subsequent requests to validate the user's identity and access rights.

- **Advantages:**

  - Compact and self-contained.
  - Stateless and scalable.
  - Can be easily transmitted as a URL parameter, in an HTTP header, or as a cookie.

- **Security Considerations:**

  - Should be transmitted over HTTPS to prevent eavesdropping.
  - Use strong, unique secret keys for signing to prevent tampering.

- **Libraries:**
  - Various programming languages provide libraries for creating, decoding, and verifying JWTs.

## What is JWT?
* JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.

* Although JWTs can be encrypted to also provide secrecy between parties, we will focus on signed tokens. Signed tokens can verify the integrity of the claims contained within it, while encrypted tokens hide those claims from other parties. When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.

## When should you use JWT?
Here are some scenarios where JSON Web Tokens are useful:

* Authorization: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

* Information Exchange: JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

## What is the JWT structure?
In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

* Header
* Payload
* Signature

Therefore, a JWT typically looks like the following.

```<base64-encoded header>.<base64-encoded payload>.<HMACSHA256(base64-encoded signature)>```

`xxxxx.yyyyy.zzzzz`

### Header
* The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

For example:

```
{
  "alg": "HS256",
  "typ": "JWT"
}

encoded:
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

Then, this JSON is Base64Url encoded to form the first part of the JWT.

### Payload
The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: *registered*, *public*, and *private claims*.

* **Registered claims**: is the information specified in [IANA JSON Web Token Claims registry](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32#section-4.1).These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

* **Public claims**: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace. Example:

  ```json
  "https://www.techmaster.vn/jwt_claims/is_admin": true
  ```

* **Private claims**: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims. This is additional information used to transmit between member computers. For example:

  ```json
  {
    "sub": "1234567890",
    "name": "paduvi",
    "admin": true
  }
  ```

An example payload could be:

```
{
  "sub": "666666",
  "name": "Ming",
  "admin": true
}

encoded:
eyJzdWIiOiI2NjY2NjYiLCJuYW1lIjoiTWluZyIsImFkbWluIjp0cnVlfQ
```

The payload is then Base64Url encoded to form the second part of the JSON Web Token.

*Do note that for signed tokens this information, though protected against tampering, is readable by anyone. Do not put secret information in the payload or header elements of a JWT unless it is encrypted.*

## Signature
* To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)

encoded:
-G5wFGMRZqFsto_ONh4CDfBrtTVdHSWWifMwdgezceM
```

The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

### Example

The following shows a JWT that has the previous header and payload encoded, and it is signed with a secret.

```
// header
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
// payload
eyJzdWIiOiI2NjY2NjYiLCJuYW1lIjoiTWluZyIsImFkbWluIjp0cnVlfQ
// signature
-G5wFGMRZqFsto_ONh4CDfBrtTVdHSWWifMwdgezceM

// Combining the above 3 strings we will get a complete JWT string
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI2NjY2NjYiLCJuYW1lIjoiTWluZyIsImFkbWluIjp0cnVlfQ.-G5wFGMRZqFsto_ONh4CDfBrtTVdHSWWifMwdgezceM
```

Example of using JWT decoding tools

<p align="center">
<img src="https://github.com/themingw666/okay/blob/main/Week%209/images/1.png" width="666px">
</p>

## How do JSON Web Tokens work?
* In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned. Since tokens are credentials, great care must be taken to prevent security issues. In general, you should not keep tokens longer than required.

* You also should not store sensitive session data in browser storage due to lack of security.

* Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema. The content of the header should look like the following:

    `Authorization: Bearer <token>`

* This can be, in certain cases, a stateless authorization mechanism. The server's protected routes will check for a valid JWT in the Authorization header, and if it's present, the user will be allowed to access protected resources. If the JWT contains the necessary data, the need to query the database for certain operations may be reduced, though this may not always be the case.

* Note that if you send JWT tokens through HTTP headers, you should try to prevent them from getting too big. Some servers don't accept more than 8 KB in headers. If you are trying to embed too much information in a JWT token, like by including all the user's permissions, you may need an alternative solution, like Auth0 Fine-Grained Authorization.

* If the token is sent in the Authorization header, Cross-Origin Resource Sharing (CORS) won't be an issue as it doesn't use cookies.

* The following diagram shows how a JWT is obtained and used to access APIs or resources:

<p align="center">
<img src="https://github.com/themingw666/okay/blob/main/Week%209/images/2.png" width="666px">
</p>

*Do note that with signed tokens, all the information contained within the token is exposed to users or other parties, even though they are unable to change it. This means you should not put secret information within the token.*

## Why should we use JSON Web Tokens?
* Let's talk about the benefits of JSON Web Tokens (JWT) when compared to Simple Web Tokens (SWT) and Security Assertion Markup Language Tokens (SAML).

* As JSON is less verbose than XML, when it is encoded its size is also smaller, making JWT more compact than SAML. This makes JWT a good choice to be passed in HTML and HTTP environments.

* Security-wise, SWT can only be symmetrically signed by a shared secret using the HMAC algorithm. However, JWT and SAML tokens can use a public/private key pair in the form of a X.509 certificate for signing. Signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON.

* JSON parsers are common in most programming languages because they map directly to objects. Conversely, XML doesn't have a natural document-to-object mapping. This makes it easier to work with JWT than SAML assertions.

* Regarding usage, JWT is used at Internet scale. This highlights the ease of client-side processing of the JSON Web token on multiple platforms, especially mobile.

<p align="center">
<img src="https://github.com/themingw666/okay/blob/main/Week%209/images/3.png" width="666px">
</p>

*Comparison of the length of an encoded JWT and an encoded SAML*
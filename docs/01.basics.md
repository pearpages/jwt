# JWT

> An open standard: RFC 7519

+ A method for transferring claims (assertions) between two parties securely through a JSON payload.
+ A digitally signed and compact, self-contained package.
+ A great mechanism for **stateless** authentication.

## Structure

* Header (meta info)
  * algorithm
  * type of token
* Payload (information about the users)
* Signature (payload becomes secure here)

## Header

> JSON object that describes the token

At minimum it should include the token type and signing algorithm.

The signing algorithm is necessary for the token to be verified.

Commonly tokens are signed with **HS256** (symmetric) or **RS256** (asymmetric).

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

## Payload

JSON object which contains any claims (assertions) about the entity for which it was issued.

The JWT standard describes a set of reserved claims. (iss,sub,aud,exp,nbf,iat,jti)

The payload can also cotain any arbitrary claims defined at will.

```json
{
    "sub": "1234567890",
    "name": "John Doe",
    "admin": true
}
```

## Signature

JSON object produced by Base64 URL encoding the header and payload and then running them through a hashing algorithm with a secret key.

The signature is used as a means to digitally sign the token so that its validaty can be verified later.

If anything in the header or payload is modified, the token will be invalidated.

```js
HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload), <secret>
)
```
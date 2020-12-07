# JSON Web Tokens

Most non-trivial apps need to get data from a secured API. Many React apps get their data from an API that is secured using [JSON Web Tokens](https://jwt.io). A typical setup, especially for small apps, might look like this:

![](./images/react-api-diagram.jpeg)

If you have a setup that looks like the above, especially if you are running both the React app and the API on the same domain, it probably actually makes more sense to use traditional cookie and session authentication rather than JWT. Doing so eases some of the issues that come with using JWT as an authentication/authorization mechanism, including:

- Need to refresh tokens
- Inability to easily revoke tokens
- Potential for theft and misuse

However, you might be making use of a third-party auth provider like Auth0. If so, you're going to need to use JSON Web Tokens, regardless of your architecture. If you're using JWT, you'll get some of the benefits that they offer:

- Ability to use across different origins
- Reduction of database lookups

### How JWTs Protect Your API

You put a middleware on endpoints that should be protected. In that middleware, you verify the signature of the token and the claims in the payload. Valid tokens will pass through that middleware and on to the endpoint itself. Invalid tokens will immediately be rejected with a 401 error or similar.

### JWTs Are Not Sessions

Some developers treat JWTs as they would treat sessions, but they are distinctly different. A traditional session establishes a "link" between the client application and server such that the server more-or-less knows who the client is.

Since JWTs can be sent to servers from anywhere, there's no telling who the holder and sender of the token _actually_ is.

Using cookies and sessions for access is like trying to get into a club and all you have is your ID number. The person working the door needs to go to the back, look you up in their records, cross-check your photo ID with what's in the system, and then they come back to let you in.

Presenting a JWT for access is like trying to get into a club by showing a special card at the door. This special card was signed by the club owner a little while back and this signature proves that its authentic. The person working the door scans it and if its valid, they let you in.

### JWT and OAuth

The JWT spec was created to support OAuth. OAuth prescribes a very specific way of doing authentication and authorization. However, it has become very popular to use JWT outside of OAuth. There are many examples in the wild. One that I came across recently is [FlatFile](https://flatfile.io).

### The Anatomy of a JWT

A JWT has three parts: the **header**, the **payload**, and the **signature**.

The header and the payload are Base64 URL encoded.

In the most basic JWT setups, the signature is calculated by hashing the encoded header and encoded payload with a secret key.

The final JWT is composed of those three items tacked together by dots: `<header>.<payload>.<signature>`

## Exercise Instructions

This exercise helps us get a feel for how JSON Web Tokens are constructed.

**Prerequisites**

Open the "Anatomy of a JWT" Codesandbox here: https://codesandbox.io/s/anatomy-of-a-jwt-start-vneg8

**Exercise Steps**

The Codesandbox has an example header and payload. It also has a completed `encode` function for encoding objects in a URL safe fashion.

1. Display the encoded header and encoded payload on the page.
2. Complete the `makeSignature` and `getJwt` functions to display the completed signature and JWT respectively.

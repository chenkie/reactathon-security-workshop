# Accessing Protected Server Resources

The data that powers your application needs to be kept safe. By its nature, the browser is incapable of doing this. The only place your data can truly be kept safe is your server. It doesn't matter if you are using a full web server or if you're using a serverless function, you need a spot that is closed off from the public.

## Protecting Data on the Server

Before your endpoints give up data, the requests that come to them need to be checked for authorization information. For this workshop, that authorization information needs to be in the form of a JSON Web Token.

There are many ways to pass the JWT in the request to the server. The most common way, and the one we'll use here, is to include it as an `Authorization` header.

On the server, the JWT needs to have its signature verified before it should be allowed to proceed to the actual endpoint. The most common way to do this is with a **middleware**.

With express, you can define a middleware with something like this:

```js
app.use((req, res, next) => {
  // check some condition

  // pass control to the next function
  next();
});
```

We can use the **express-jwt** package as a middleware. It comes with the ability to verify tokens for us.

## Pre-Exercise

Check out the `06-start` branch.

Let's make a request to one of the endpoints with a REST client or just a browser tab. We should be able to get access to the data.

Let's also explore how middlewares work and how we can verify the token manually.

## Exercise Instructions

- Working in `orbit-api/server.js`, create a middleware which verifies the token from incoming requests.
- Apply the middleware to all of the endpoints that need it.

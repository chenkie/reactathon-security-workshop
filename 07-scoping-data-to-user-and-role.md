# Scoping Data to a User and Role

Most applications don't share all data to all users. Instead, data needs to be scoped down to a specific user. Going further, data may need to be scoped to both a specific user and specific organization.

Regardless of the needs, JSON Web Tokens allow us to easily query for data that belongs to specific users or organizations.

The payload in a JWT might look like this:

```json
{
  "sub": "12345",
  "iss": "acme.com",
  "aud": "acme.com",
  "exp": "1589391233"
}
```

The `sub` claim is most often a user ID. In our setup, it's the Mongo `ObjectId` for the user. We can use this to both query for data and write new data.

## Can We Trust the Payload

Recall that JWTs come with a security feature: if someone tampers with the payload of the token, it becomes invalid. For this reason, as long as the token was signed appropriately, the JWT payload that ends up back at our API when a user makes a request is the payload that was originally signed in the token. This means we can trust that data.

This is one of the reasons developers like working with JWTs. Since the token payload can be trusted when the request goes to the API, there's no need to do any additional lookups to see what the user has access to. This means fewer database lookups which can improve performance. This improved performance probably won't matter for your application because it only really becomes apparent at huge scale.

## Limiting Access Based on Role

It's common to need to limit access to users based on a specific role. The way roles are defined is at your discretion. Some common examples include: `user`, `admin`, `manager`, `superadmin` etc.

For endpoints which serve data that should be limited to a specific role, two checks need to be made: one that verifies the signature and another which verifies the role in the token payload is what is expected.

Checking for a role can be done in another middleware.

## Pre-Exercise

Let's explore the `attachUser` middleware to see how the token is received and decoded. Let's see how this info can then be used in the endpoint itself.

## Exercise Instructions

- Working in `orbit-api/server.js`, complete the `requireAdmin` middleware so that only requests with a `role` of `admin` in the token payload can proceed.
- Apply the `requireAdmin` middleware to the `inventory` routes.
- In the `inventory` routes, get the user ID from the JWT payload and use it in Mongo queries. Hint: check the mongoose docs for[ **finding**](https://mongoosejs.com/docs/api.html#model_Model.find) and [**creating**](https://mongoosejs.com/docs/models.html#constructing-documents) data.

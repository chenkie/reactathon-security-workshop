# Login and Signup

Most apps still require traditional login and signup forms and must support username and password login.

There are a bunch of options that are more secure and you should strongly consider them. These include:

- Relying on an OAuth provider
- Passwordless authentication
- Strong authenticators like TouchID

However, username and password authentication is mostly fine if implemented correctly.

## What Happens After Login/Signup

With cookie/session-based authentication, a successful login will result in a cookie being set that contains a session ID. This cookie is then sent back to the server on subsequent requests where it can be matched up with a session (if it exists).

With JWT-based authentication, the JWT can be returned to the browser after a successful login.

The JWT then needs to be stored in the browser somehow. The reasons it needs to be stored is so that it can be persisted on page refresh, tab closing, etc.

This is where we get to one of the biggest debates on the internet––where do you store JWTs?

There are roughly three options:

1. In local storage
2. In an HttpOnly cookie
3. In browser memory (React state)

Each of these options suffers from some problems.

Local storage is susceptible to XSS attacks.

Cookies are susceptible to XSS and CSRF attacks.

Browser memory doesn't persist when the page is refreshed.

There are ways to get around all of these issues, each requiring varying degrees of extra work.

For this workshop, we'll start out with local storage since it's the simplest way to get started. Let's make it work first, then make it more secure a bit later.

**Note:** Some argue that local storage is just fine

## Pre-Exercise

Let's look at how to implement the call to sign up for an account from the React app

## Exercise Instructions

- Implement the call to the `/authenticate` endpoint in `orbit-app/src/pages/Login.js`.
- There are three functions in `orbit-app/src/context/AuthContext.js` where the body is missing. They are `setAuthInfo`, `logout`, `isAuthenticated`. Implement the body for these functions.

# Lazy Loading Protected Routes

Once the code for your React app hits the user's browser, you have no way of controlling what they do with it. They can study it, see your business logic, try to figure out how your app works, and even try to see how they might force their way to a route or UI state they shouldn't be at.

So long as your API is properly secured and you're only serving data to your app from there, it shouldn't be that big of a deal if a user makes their way to a route they shouldn't be allowed to see.

We can do better though. We can split the React app's code bundles up based on route so that users are only served the code they should be allowed to see.

## What is Lazy Loading?

Lazy loading means waiting until code for the React app is actually needed before it is downloaded in the browser.

The main benefit it offers is that your initial app bundle remains small.

A side benefit is that it improves security. There's no reason an unauthenticated user should download code for part of the app they aren't able to access. There's also no reason a user with a role of `user` should get access to code that powers routes reserved for users with a role of `admin`.

## Pre-Exercise

Let's explore how the routes are currently imported and explore dev tools to see what's sent to the browser when the app loads

## Exercise Instructions

- Use the `React.lazy` function to lazily load the components which power the authenticatd routes
- Use `suspense` to properly handle these lazily loaded components. Provide a fallback component.

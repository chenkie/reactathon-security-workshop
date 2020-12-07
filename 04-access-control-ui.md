# Access Contorl for the UI

We often need to display certain parts of the UI only if the user is currently authenticated or only if they have certain access rights.

In a roundtrip app, enforcing this is straightforward. As you request new pages, the server is responsible for putting together the HTML to power them. The server can safely check whether the user is authenticated and/or has certain access rights and respond accordinly.

It's different in a single page app though. In a SPA, all the code that goes into powering the app lives in the browser. Since browsers are public clients, we have no way of knowing what users might do with our app code once it has been shipped. It's very conceivable that crafty users could force their way to a route/UI state that they shouldn't have access to.

## How to Think About SPAs and Public Clients

We need to accept the fact that our apps could be "hacked" on the front end if we're building a SPA. There are things we can do to make it more difficult for users to get to a route/UI state they shouldn't be at, but it's impossible to prevent it completely.

The important part is that the **data** that powers are app is protected on the server. This is the only safe place for data to come from. You would never want to include sensitive info/data in your code bundle and ship that to users.

## How Do We Know If a User Is "Authenticated"

In roundtrip apps this is easy. The server can check the user's session and lookup their access rights in a database before construting the HTML that gets shipped back to the browser on each move through the app.

In a SPA, all we have are **clues**.

There are several reasonable choices to use as a "clue":

- Token expiry time
- Simple boolean
- Presence of a token

## Pre-Exercise

Let's look at the application and reason about which parts should be hidden under which circumstances. We'll also look at our `AuthContext` to see what we can use to help us out.

## Exercise Instructions

- Working from `orbit-app/src/pages/Home.js`, adjust the "Login" and "Get Started" link to redirect the user to `/dashboard` if they are currently authenticated or `/login` if they aren't.
- Working from `orbit-app/src/components/Sidebar.js`, adjust the list of available routes to include a key to scope them down to certain access levels. Then adjust the way `<NavItem>` is rendered such that it is only displayed to users with the appropriate access levels.

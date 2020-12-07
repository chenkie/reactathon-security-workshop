# Access Control for Front End Routes

Our apps will most likely have entire routes that only authenticated users should see. Likewise, some routes should only be accessible to users who have a certain access level.

As previously discussed, there's no true way of "protecting" these routes. The code for these routes lives in the users' browser and as such can be tampered with. It's very feasible for a user to force their way to a route they shouldn't be at.

As long as the data that goes into powering these routes comes from a protected endpoint on your server, this likely isn't a big deal. The user will only see a broken looking page at worst or an "access denied" screen at best.

## React Router

The `<Route>` component that comes with React router makes it easy to compose different kinds of routes that you might need as they pertain to authentication and authorization. You can create routes that are specific to authenticated users and others that are specific to users with an "admin" role, for example.

What you do with dissallowed navigation attempts to these routes is up to you. A common pattern is to send the user to the login page or the home page.

## Pre-Exercise

Let's have a look at how routing is currently shaped in the app. Let's also have a look at the React Router docs to see [how they recommend composing routes](https://reacttraining.com/react-router/web/example/auth-workflow) for this purpose.

## Exercise Instructions

- Working from `orbit-app/src/App.js`, complete the `UnauthenticatedRoutes`, `AuthenticatedRoute`, and `AdminRoute` components. These routes should redirect to the `/login` route if the user shouldn't be allowed to get there.

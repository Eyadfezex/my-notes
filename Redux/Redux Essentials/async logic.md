# Async logic

Imagine Redux as a big filing cabinet for your app's data. Part 5 of the Redux Essentials guide is all about how to deal with stuff that's not already in the cabinet, like info from the internet.

Here's the gist:

- **Special Helpers (Middleware):** Redux normally likes to handle things right away, but fetching data from the web takes time. Middleware acts like an assistant in the filing cabinet. It catches certain requests (like data fetching) and handles the waiting game for you.

- **Async Thunks: Imagine these as fancy to-do lists.** You write down instructions for what data to grab and what to do with it once it arrives. These instructions can involve waiting for the data to come in (like waiting for a delivery).

- **A Common Pattern:** There's a kind of routine for grabbing data:
  1. Tell everyone a request is starting (like saying "downloading..." on the screen).
  2. Ask the internet for the data (like placing an order online).
  3. Once it arrives, update the filing cabinet with the new info (like putting the delivered package away).
  4. If there's a problem, you take care of it (like dealing with a missing item).

Here's what that data flow looks like visually:

![Async logic](https://redux.js.org/assets/images/ReduxAsyncDataFlowDiagram-d97ff38a0f4da0f327163170ccc13e80.gif)

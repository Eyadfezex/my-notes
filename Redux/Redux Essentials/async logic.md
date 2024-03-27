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

![Async logic]([https://redux.js.org/assets/images/ReduxAsyncDataFlowDiagram-d97ff38a0f4da0f327163170ccc13e80.gif](https://camo.githubusercontent.com/79eb282f3949943c160f1851da08e069d082d618faf22fc4248f49dc88f36766/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6d656469612d702e736c69642e65732f75706c6f6164732f3336343831322f696d616765732f323438343739302f415243482d5265647578322d657874656e6465642d7265616c2d6465636c657261746976652e676966)https://camo.githubusercontent.com/79eb282f3949943c160f1851da08e069d082d618faf22fc4248f49dc88f36766/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6d656469612d702e736c69642e65732f75706c6f6164732f3336343831322f696d616765732f323438343739302f415243482d5265647578322d657874656e6465642d7265616c2d6465636c657261746976652e676966)

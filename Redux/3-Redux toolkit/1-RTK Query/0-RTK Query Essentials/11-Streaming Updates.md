# RTK Query and Streaming Updates

RTK Query (Redux Toolkit Query) doesn't directly support full streaming updates like websockets. However, you can:

1. Use useQuery with pollingInterval for limited real-time updates.
2. Manually trigger updates with refetch on specific events.
3. Customize RTK Query behavior with queryFn and infiniteQueryFn to integrate streaming libraries for data updates, requiring advanced knowledge of RTK Query internals.

**For example:**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

const chatApi = createApi({
  reducerPath: "chat",
  baseQuery: fetchBaseQuery({ baseUrl: "https://api.example.com/chat" }),
  endpoints: (builder) => ({
    getMessages: builder.query({
      query: () => "/messages",
      // ... other query options
      onCacheEntryAdded: async (arg, { cacheDataLoaded, dispatch }) => {
        await cacheDataLoaded; // Wait for initial data
        const socket = new WebSocket("wss://api.example.com/chat/ws");
        socket.onmessage = (event) => {
          const newMessage = JSON.parse(event.data);
          // Update cache entry with new message data using dispatch
        };
      },
    }),
  }),
});
```

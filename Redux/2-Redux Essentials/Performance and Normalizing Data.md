# Understanding the Performance Impact of Denormalized State Shape

When building applications like online chat rooms, data often becomes nested, resulting in complex structures. Consider the following data structure:

```javascript
const chatRooms = [
  {
    id: "chatRoom1",
    name: "general",
    users: [
      {
        id: "user1",
        name: "John",
        belongToRooms: [
          { id: "chatRoom1", name: "general" },
          { id: "chatRoom2", name: "random" },
        ],
      },
      // More users...
    ],
  },
  // More chat rooms...
];
```

While intuitive, this structure can pose performance challenges, especially when updating or deleting entities. For example, let's see how deleting a chat room might be handled in a reducer:

```javascript
export default function (state = initialState, action) {
  switch (action.type) {
    case DELETE_CHAT_ROOM: {
      const { roomId } = action.payload;
      const { chatRooms } = state;

      const indexOfChatRoomToBeDeleted = chatRooms.findIndex(
        (chatRoom) => chatRoom.id === roomId
      );

      // Delete Chat room

      chatRooms.splice(indexOfChatRoomToBeDeleted, 1);

      // Delete Chat room from the users

      chatRooms.forEach((chatRoom) => {
        chatRoom.users.forEach((user) => {
          const index = user.belongToRooms.findIndex(
            (chatRoom) => chatRoom.id === roomId
          );
          if (index != -1) {
            user.belongToRooms.splice(index, 1);
          }
        });
      });
    }
  }
}
```

However, this denormalized approach has several drawbacks:

- Duplicated data across entities leads to complexity in ensuring data consistency.
- Updating deeply nested data requires complex reducers that parse the entire state tree.
- Unrelated UI components may re-render unnecessarily if a deep data object is updated.

Normalization, akin to database design principles, addresses these issues by separating entities into distinct slices of state. Let's see how normalization would transform the state:

```javascript
const chatRooms = {
  byId: {
    chatRoom1: { id: "chatRoom1", name: "general" },
    chatRoom2: { id: "chatRoom2", name: "random" },
  },
};

const users = {
  byId: {
    user1: { id: "user1", name: "John" },
    user2: { id: "user2", name: "Smith" },
  },
};

const chatRoomUsers = {
  byId: {
    chatRoomUser1: {
      id: "chatRoomUser1",
      chatRoomId: "chatRoom1",
      userId: "user1",
    },
    chatRoomUser2: {
      id: "chatRoomUser2",
      chatRoomId: "chatRoom2",
      userId: "user2",
    },
  },
};
```

With normalization:

- Updates are limited to specific slices of state, avoiding parsing of the entire state tree.
- Lookup becomes simple, akin to a dictionary, resulting in O(1) complexity.
- Reduction in complex reducers as each entity is managed separately.
- Updates affect only relevant portions of the state, minimizing unnecessary re-renders.

In conclusion, normalizing state structure significantly enhances performance and simplifies state management, particularly in scenarios with nested data structures.

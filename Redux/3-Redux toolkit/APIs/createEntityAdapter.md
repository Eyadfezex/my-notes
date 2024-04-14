# createEntityAdapter

`createEntityAdapter` is a utility function in Redux Toolkit that simplifies managing collections of entities (data objects) in your application state.
It provides pre-built reducers and selectors for common CRUD (Create, Read, Update, Delete) operations on a normalized data structure.

**Benefits of Using createEntityAdapter:**

- Efficient Data Management:
  - Stores entities in a normalized format, reducing redundancy and improving performance.
  - Easier to update specific entities without affecting the entire collection.
- Pre-built Reducers and Selectors:
  - Saves you time by providing pre-written functions for CRUD operations.
  - Reduces boilerplate code and potential errors in writing custom logic.
- Improved Code Readability:
  - Clear and concise code for managing entity data.
  - Makes it easier to understand how state is updated.

**How it Works:**

1. Normalized Data Structure:
   - `createEntityAdapter` creates two properties in your state slice:
     - `byId`: An object that maps entity IDs to their corresponding entity objects.
       `allIds`: An array containing the IDs of all entities in the collection.
2. Reducers:
   - The function generates pre-built reducer functions for CRUD operations:
     - `addOne`: Adds a new entity to the state.
     - `updateOne`: Updates an existing entity.
     - `addMany`: Adds multiple entities to the state.
     - `setAll`: Sets the entire collection of entities.
     - `upsertOne`: Adds or updates an entity based on its ID.
     - `removeOne`: Removes an entity from the state by ID.
     - `removeMany`: Removes multiple entities by their IDs.
     - `upsertMany`: Adds or updates multiple entities.
3. Selectors:
   - It also provides pre-built selector functions for accessing entity data:
     - `selectAll`: Selects all entities as an array.
     - `selectById`: Selects a specific entity by its ID.
     - `selectIds`: Selects an array of all entity IDs.

**Example Usage:**

```jsx
import { createSlice, createEntityAdapter } from "@reduxjs/toolkit";

// 1. Create an adapter for managing product entities
const productsAdapter = createEntityAdapter({
  // Optional configuration for entity ID selection, sorting, etc.
});

// 2. Define the initial state using the adapter's getter
const initialState = productsAdapter.getInitialState();

// 3. Create a slice for managing product data
const productsSlice = createSlice({
  name: "products", // Identify the slice in the Redux store
  initialState,
  reducers: {
    addProduct: productsAdapter.addOne, // Pre-built reducer for adding a product
    updateProduct: productsAdapter.updateOne, // Pre-built reducer for updating a product
    removeProduct: productsAdapter.removeOne, // Pre-built reducer for removing a product
  },
});

// 4. Export actions for dispatching from components
export const { addProduct, updateProduct, removeProduct } =
  productsSlice.actions;

// 5. Export selectors for retrieving product data
export const selectAllProducts = productsAdapter.getSelectors(
  productsSlice.state
).selectAll;
export const selectProductById = productsAdapter.getSelectors(
  productsSlice.state
).selectById;

// 6. Example usage in a component
// (Assuming you have setup useDispatch and useSelector)
const dispatch = useDispatch();

dispatch(addProduct({ id: 1, name: "Product 1" })); // Dispatch action to add a product
const product = useSelector(selectProductById(1)); // Get product by ID using selector
```

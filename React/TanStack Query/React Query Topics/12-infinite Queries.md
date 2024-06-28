# Infinite Queries

Rendering lists that can additively "load more" data onto an existing set of data or "infinite scroll" is also a very common UI pattern. TanStack Query supports a useful version of `useQuery` called `useInfiniteQuery` for querying these types of lists.

When using `useInfiniteQuery`, there are some key differences:

1. **Data Structure**:

   - `data` is an object containing:
     - `data.pages`: an array of fetched pages.
     - `data.pageParams`: an array of page parameters used for fetching.

2. **Functions**:

   - `fetchNextPage` and `fetchPreviousPage` are now available, with `fetchNextPage` being required.

3. **Options**:

   - `initialPageParam`: Specifies the initial page parameter (required).
   - `getNextPageParam` and `getPreviousPageParam`: Determine if there is more data to load and provide the necessary information for fetching it. This info is also passed as an additional parameter in the query function.

4. **Booleans**:
   - `hasNextPage`: `true` if `getNextPageParam` returns a value other than `null` or `undefined`.
   - `hasPreviousPage`: `true` if `getPreviousPageParam` returns a value other than `null` or `undefined`.
   - `isFetchingNextPage` and `isFetchingPreviousPage`: Distinguish between a background refresh state and a loading more state.

**For Example:**

```tsx
import React from "react";
import { useInfiniteQuery } from "@tanstack/react-query";

function Projects() {
  // Function to fetch projects data from the API
  const fetchProjects = async ({ pageParam = 0 }) => {
    const res = await fetch(`/api/projects?cursor=${pageParam}`);
    return res.json();
  };

  // Use useInfiniteQuery hook to fetch and manage paginated project data
  const {
    data, // The data returned from the query
    error, // The error object in case of an error
    fetchNextPage, // Function to fetch the next page of data
    hasNextPage, // Boolean indicating if there is a next page
    isFetching, // Boolean indicating if data is being fetched
    isFetchingNextPage, // Boolean indicating if the next page is being fetched
    status, // The status of the query ('pending', 'error', 'success')
  } = useInfiniteQuery({
    queryKey: ["projects"], // Unique key for the query
    queryFn: fetchProjects, // Function to fetch data
    initialPageParam: 0, // Initial cursor value
    getNextPageParam: (lastPage, pages) => lastPage.nextCursor, // Function to get the next cursor value from the last fetched page
  });

  // Render the component based on the query status
  return status === "pending" ? (
    <p>Loading...</p> // Display loading message while fetching data
  ) : status === "error" ? (
    <p>Error: {error.message}</p> // Display error message if fetching failed
  ) : (
    <>
      {/* Map through the pages and projects to render them */}
      {data.pages.map((group, i) => (
        <React.Fragment key={i}>
          {group.data.map((project) => (
            <p key={project.id}>{project.name}</p> // Render each project's name
          ))}
        </React.Fragment>
      ))}
      <div>
        {/* Button to load more data */}
        <button
          onClick={() => fetchNextPage()} // Fetch the next page when clicked
          disabled={!hasNextPage || isFetchingNextPage} // Disable button if there's no next page or data is being fetched
        >
          {isFetchingNextPage
            ? "Loading more..." // Show loading message while fetching next page
            : hasNextPage
            ? "Load More" // Show 'Load More' if there's a next page
            : "Nothing more to load"}{" "}
          // Show message if there's no more data to load
        </button>
      </div>
      <div>
        {/* Show fetching indicator while data is being fetched */}
        {isFetching && !isFetchingNextPage ? "Fetching..." : null}
      </div>
    </>
  );
}

export default Projects;
```

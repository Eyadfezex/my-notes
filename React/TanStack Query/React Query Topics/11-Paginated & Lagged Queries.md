# Paginated / Lagged Queries

Rendering paginated data is common, and in TanStack Query, it works by including the page info in the query key:

```tsx
const result = useQuery({
  queryKey: ["projects", page],
  queryFn: fetchProjects,
});
```

**The UI jumps between `success` and `pending` states because each new page is treated like a new query.**

## Smoother Pagination with `placeholderData`

TanStack Query's `placeholderData` feature improves this experience:

- The last successful fetch's data stays available while new data is requested.
- The previous data is seamlessly swapped for the new data when it arrives.
- `isPlaceholderData` indicates if the query is using placeholder data.

### Example with `placeholderData`

```tsx
import { keepPreviousData, useQuery } from "@tanstack/react-query"; // Import libraries for data fetching and caching
import React from "react";

function Todos() {
  // State to keep track of the current page number
  const [page, setPage] = React.useState(0);

  // Function to fetch projects data from the API
  const fetchProjects = (page = 0) =>
    fetch("/api/projects?page=" + page).then((res) => res.json()); // Fetch data and parse JSON response

  // Use React Query to fetch and manage project data
  const {
    isPending, // Flag indicating data is being fetched
    isError, // Flag indicating an error occurred
    error, // Error object in case of error
    data, // Fetched project data
    isFetching, // Flag indicating if data is being fetched (within query lifecycle)
    isPlaceholderData, // Flag indicating if placeholder data is used
  } = useQuery({
    queryKey: ["projects", page], // Unique key for the query (based on page)
    queryFn: () => fetchProjects(page), // Function to fetch data for the specific page
    placeholderData: keepPreviousData, // Use previous data as placeholder while fetching
  });

  return (
    <div>
      {isPending ? (
        <div>Loading...</div> // Display loading message while fetching data
      ) : isError ? (
        <div>Error: {error.message}</div> // Display error message if fetching failed
      ) : (
        <div>
          {data.projects.map((project) => (
            <p key={project.id}>{project.name}</p> // Render each project name
          ))}
        </div>
      )}
      <span>Current Page: {page + 1}</span>
      <button
        onClick={() => setPage((old) => Math.max(old - 1, 0))} // Handle Previous Page click, prevent going below page 0
        disabled={page === 0} // Disable Previous button on page 0
      >
        Previous Page
      </button>
      <button
        onClick={() => {
          if (!isPlaceholderData && data.hasMore) {
            // Only enable Next button if data is not placeholder and has more pages
            setPage((old) => old + 1);
          }
        }}
        disabled={isPlaceholderData || !data?.hasMore} // Disable Next button until data is loaded and has more pages
      >
        Next Page
      </button>
      {isFetching ? <span> Loading...</span> : null}{" "}
      {/* Display loading message during query fetching */}
    </div>
  );
}
```

This example uses `useQuery` to fetch paginated data and `keepPreviousData` to maintain previous data while fetching new data, ensuring a smooth and responsive UI during pagination.

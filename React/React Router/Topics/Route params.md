# Route params

1- route parameters are used to define dynamic parts of the URL within your application.

2- These parameters are specified in the route definition using a colon followed by the parameter name.

3- React Router then parses these parameters from the URL and makes them available to your components.

- Example :

```jsx
<Route path="/wiki/:topicId" element={<Article />} />
```

Now whenever anyone visits a URL that matches the `/wiki/:topicId` pattern (`/wiki/javascript`, `/wiki/Brendan_Eich`, `/wiki/anything`) , the Article component is rendered. And to access the dynamic portion of the URL - in this case, `topicId` we use a react router hook called [`useParams`](../Router%20Hooks/useParams.md) :

```jsx
import * as React from 'react'
import { useParams } from 'react-router-dom'
import { getArticle } from '../utils'

function Article () {
  const [article, setArticle] = React.useState(null)
  const { topicId } = useParams()

 React.useEffect(() => {
   getArticle(topicId)
     .then(setUser)
 }, [topicId])

 return (
   ...
 )
}
```

## purpose

- Route parameters are useful for creating dynamic routes in React applications, especially when dealing with scenarios like displaying user profiles, accessing specific resources, or filtering content based on dynamic criteria.

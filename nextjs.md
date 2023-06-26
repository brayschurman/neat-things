# NextJS

## Data Fetching

- Make sure data "catching" logic goes _after_ all hooks... (useState, TRPC) I kept making this mistake and was getting weird rendering error.

Ok, I made this doc after having 3 Space Invaders, bear with me.

### getServerSideProps()

Will pre-render the page at **request time**, using the data returned by it as props.

This is _only run on server-side_ which allows for writing database queries **directly** (instead of an API route, and _then_ fetching).

#### When to use getServerSideProps()

Fetch one time things like authorization or geo-location.

```javascript
function Page({ data }) {
  // Render data...
}

// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`);
  const data = await res.json();

  // Pass data to the page via props
  return { props: { data } };
}

export default Page;
```

### getStaticProps() aka Static Site Generation

Will pre-render the page at **build time**, meaning when the `npm run build` function runs, the page is statically generated. This is good for optimizing since page can be statically generated on build.

This is also _only run on server-side_.

#### When to use getStaticProps()

- Data required to render is available at build time. This enables the page to be static HTML when rendered.

- Data can be cached publicly.

```javascript
// posts will be populated at build time by getStaticProps()
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  );
}

// This function gets called at build time on server-side.
// It won't be called on client-side, so you can even do
// direct database queries.
export async function getStaticProps() {
  // Call an external API endpoint to get posts.
  // You can use any data fetching library
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  };
}

export default Blog;
```

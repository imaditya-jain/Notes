# Rendering Strategies in Next.js

## 1. Client-Side Rendering (CSR)

The browser loads a minimal HTML shell, downloads the JavaScript bundle, and renders the UI on the client. Fast navigation but slower first load and not SEO-friendly because the initial HTML is empty.

**Best for:** Dashboards, SaaS apps, internal tools.

```
// CSR example – simply fetch inside useEffect
import { useEffect, useState } from "react";

export default function Home() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("/api/data").then(res => res.json()).then(setData);
  }, []);

  return <div>{data ?? "Loading..."}</div>;
}

```

## 2. Server-Side Rendering (SSR)

HTML is rendered on the server on every request, improving SEO and initial load speed. But increases server load because each request regenerates the page.

**Best for:** SEO pages with dynamic data (product pages, dashboards with real-time data).

```
// SSR example using getServerSideProps
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com/products");
  const data = await res.json();

  return { props: { data } };
}

export default function Page({ data }) {
  return <div>{JSON.stringify(data)}</div>;
}

```
## 3. Static Site Generation (SSG)
Pages are generated once at build time. Super fast, SEO-friendly, low server load. Not ideal for frequently changing content unless rebuilt.

**Best for:** Blogs, documentation, marketing pages.

```
// SSG example using getStaticProps
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();

  return { props: { posts } };
}

export default function Blog({ posts }) {
  return <div>{JSON.stringify(posts)}</div>;
}

```

## 4. Incremental Static Regeneration (ISR)

HTML is generated at build time like SSG, but can auto-update after a given revalidate interval.

How it works:
- User receives cached static HTML instantly.
- After ```revalidate``` seconds, the next request triggers background regeneration.
- Updated page is cached and served to all future users.

**Best for:** Content sites needing frequent updates without full rebuilds.

```
// ISR example → SSG + revalidate
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/news");
  const news = await res.json();

  return {
    props: { news },
    revalidate: 60, // regenerate every 60 seconds
  };
}

export default function News({ news }) {
  return <div>{JSON.stringify(news)}</div>;
}

```
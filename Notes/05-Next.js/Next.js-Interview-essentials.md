# 🔺 Next.js Interview Essentials

> A complete, beginner-friendly reference guide covering every Next.js concept you need to ace frontend and full-stack developer interviews. Written in simple, easy English with clear code examples, real-world patterns, and honest explanations of when and why to use each feature.

---

## 📌 Table of Contents

- [What is Next.js?](#what-is-nextjs)
- [App Router vs Pages Router](#app-router-vs-pages-router)
- [Project Structure](#project-structure)
- [File-Based Routing](#file-based-routing)
- [Pages and Layouts](#pages-and-layouts)
- [Server Components vs Client Components](#server-components-vs-client-components)
- [Data Fetching](#data-fetching)
- [Caching in Next.js](#caching-in-nextjs)
- [Server Actions](#server-actions)
- [API Routes](#api-routes)
- [Static Generation (SSG)](#static-generation-ssg)
- [Server-Side Rendering (SSR)](#server-side-rendering-ssr)
- [Incremental Static Regeneration (ISR)](#incremental-static-regeneration-isr)
- [Dynamic Routes](#dynamic-routes)
- [Route Groups and Parallel Routes](#route-groups-and-parallel-routes)
- [Intercepting Routes](#intercepting-routes)
- [Middleware](#middleware)
- [Image Optimization](#image-optimization)
- [Font Optimization](#font-optimization)
- [Metadata and SEO](#metadata-and-seo)
- [Environment Variables](#environment-variables)
- [Next.js Link and Navigation](#nextjs-link-and-navigation)
- [Loading and Error States](#loading-and-error-states)
- [Streaming and Suspense](#streaming-and-suspense)
- [Authentication Patterns](#authentication-patterns)
- [Next.js with TypeScript](#nextjs-with-typescript)
- [Deployment](#deployment)
- [Performance Best Practices](#performance-best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is Next.js?

Next.js is a **React framework** built on top of React that adds powerful features out of the box. If React is like raw ingredients, Next.js is the full recipe with all the tools ready to go.

Plain React gives you just the UI layer. Next.js adds:

- **File-based routing** — your folder structure becomes your URL structure
- **Server-side rendering** — render HTML on the server for better SEO and performance
- **API routes** — build backend endpoints right inside your Next.js app
- **Automatic code splitting** — each page only loads the JavaScript it needs
- **Image and font optimization** — built-in performance tools
- **TypeScript support** — out of the box, no configuration needed
- **Full-stack capability** — one codebase for frontend and backend

### When to use Next.js instead of plain React

Use Next.js when you need:
- SEO (blog, e-commerce, marketing pages)
- Fast initial page loads
- Server-side data fetching
- A backend API in the same project
- Built-in performance optimizations

Use plain React (with Vite) when:
- You are building a private dashboard that does not need SEO
- You want full control over your tooling
- The app is purely client-side

---

## App Router vs Pages Router

Next.js has two routing systems. This is one of the most asked interview topics.

| Feature | App Router (`/app`) | Pages Router (`/pages`) |
|---|---|---|
| Introduced | Next.js 13 (stable in 13.4) | Next.js since v1 |
| Default in new projects | Yes | No (still supported) |
| React Server Components | Yes | No |
| Layouts | Nested, per folder | `_app.js` only |
| Data fetching | `fetch()` in components | `getServerSideProps`, `getStaticProps` |
| Streaming | Built-in with Suspense | Limited |
| Learning curve | Higher | Lower |
| Status | Future of Next.js | Stable, being maintained |

> **Interview Tip:** Most new projects use the App Router. Most existing production apps still use Pages Router. Know both, but focus on App Router since that is what interviewers want to hear about.

---

## Project Structure

```
my-app/
├── app/                    ← App Router (new way)
│   ├── layout.tsx          ← Root layout (wraps all pages)
│   ├── page.tsx            ← Home page "/"
│   ├── globals.css         ← Global styles
│   ├── about/
│   │   └── page.tsx        ← "/about" page
│   ├── blog/
│   │   ├── page.tsx        ← "/blog" page
│   │   └── [slug]/
│   │       └── page.tsx    ← "/blog/my-post" dynamic page
│   ├── api/
│   │   └── users/
│   │       └── route.ts    ← API endpoint "/api/users"
│   └── dashboard/
│       ├── layout.tsx      ← Dashboard-specific layout
│       ├── page.tsx        ← "/dashboard"
│       ├── settings/
│       │   └── page.tsx    ← "/dashboard/settings"
│       └── loading.tsx     ← Loading UI for dashboard
├── components/             ← Reusable React components
├── lib/                    ← Utility functions, db connections
├── hooks/                  ← Custom React hooks
├── types/                  ← TypeScript types
├── public/                 ← Static files (images, fonts, favicon)
│   ├── logo.png
│   └── favicon.ico
├── next.config.js          ← Next.js configuration
├── tailwind.config.js      ← TailwindCSS config
├── tsconfig.json           ← TypeScript config
└── .env.local              ← Environment variables (secret)
```

### Special File Names in App Router

| File | Purpose |
|---|---|
| `page.tsx` | The UI for a route, makes the route publicly accessible |
| `layout.tsx` | Wraps pages, persists across navigation (like a shell) |
| `loading.tsx` | Shown while the page or data is loading (uses Suspense) |
| `error.tsx` | Shown when something goes wrong in the route |
| `not-found.tsx` | Shown for 404 errors |
| `route.ts` | API endpoint (no UI) |
| `template.tsx` | Like layout but creates a new instance on every navigation |
| `default.tsx` | Fallback for parallel routes |

---

## File-Based Routing

In Next.js, you do not write route configuration files. The folder structure inside `/app` IS your routes.

```
app/
├── page.tsx                → "/"
├── about/
│   └── page.tsx            → "/about"
├── blog/
│   ├── page.tsx            → "/blog"
│   └── [slug]/
│       └── page.tsx        → "/blog/anything-here"
├── shop/
│   └── [...categories]/
│       └── page.tsx        → "/shop/a" or "/shop/a/b/c" (catch-all)
├── (marketing)/            → Route group, does NOT appear in URL
│   ├── about/
│   │   └── page.tsx        → "/about"
│   └── contact/
│       └── page.tsx        → "/contact"
├── dashboard/
│   ├── @notifications/     → Parallel route slot
│   │   └── page.tsx
│   └── page.tsx
```

### URL patterns

```
/                    → app/page.tsx
/about               → app/about/page.tsx
/blog                → app/blog/page.tsx
/blog/hello-world    → app/blog/[slug]/page.tsx    (slug = "hello-world")
/shop/men/shoes      → app/shop/[...categories]/page.tsx  (categories = ["men", "shoes"])
```

---

## Pages and Layouts

### page.tsx — The actual page content

```tsx
// app/page.tsx — Home page at "/"
export default function HomePage() {
  return (
    <main>
      <h1>Welcome to my app!</h1>
      <p>This is the home page.</p>
    </main>
  );
}
```

### layout.tsx — Shared wrapper that stays across navigation

```tsx
// app/layout.tsx — Root layout (required, wraps EVERYTHING)
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";

const inter = Inter({ subsets: ["latin"] });

// Metadata for SEO
export const metadata: Metadata = {
  title: "My App",
  description: "The best app ever built",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <Header />
        <main>{children}</main>
        <Footer />
      </body>
    </html>
  );
}
```

### Nested Layouts

Layouts can be nested. Each folder can have its own layout that wraps its pages and inherits from the parent layout.

```tsx
// app/dashboard/layout.tsx
// Adds a sidebar specifically for dashboard pages
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div className="dashboard-shell">
      <aside className="sidebar">
        <DashboardNav />
      </aside>
      <div className="content">{children}</div>
    </div>
  );
}

// Now every page inside /dashboard/ gets the sidebar automatically
// app/dashboard/page.tsx       → has sidebar
// app/dashboard/settings/page.tsx  → has sidebar
// app/dashboard/billing/page.tsx   → has sidebar
```

> **Interview Tip:** Layouts are great because they do not re-mount when you navigate between pages within the same layout. So a sidebar in a dashboard layout stays rendered and does not flash or reset when you go from `/dashboard` to `/dashboard/settings`. This is one of the biggest advantages over the old Pages Router.

---

## Server Components vs Client Components

This is the most important concept in the App Router and almost always comes up in interviews.

### Server Components (default in App Router)

By default, every component in the App Router is a **Server Component**. It runs only on the server. The user never gets this JavaScript.

```tsx
// app/users/page.tsx
// No "use client" at the top = Server Component by default

// You can do these things ONLY in Server Components:
// - async/await directly in the component
// - Access databases, file system, secrets
// - No useState, useEffect, event handlers

async function UsersPage() {
  // Fetch data directly — no useEffect, no loading state needed
  const users = await fetch("https://api.example.com/users").then(r => r.json());

  return (
    <ul>
      {users.map((user: any) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default UsersPage;
```

### Client Components

Add `"use client"` at the top of the file to make it a Client Component. These work like regular React components — they run in the browser and can use hooks, events, and browser APIs.

```tsx
"use client";

import { useState } from "react";

// You can do these things ONLY in Client Components:
// - useState, useEffect, useContext, and other hooks
// - Event handlers (onClick, onChange)
// - Browser APIs (window, localStorage, geolocation)
// - Third-party libraries that use browser features

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>Increment</button>
    </div>
  );
}
```

### The Most Important Rule: Push Client Components to the Leaves

The best pattern is to keep as much as possible as Server Components and only make the small interactive parts Client Components.

```tsx
// app/dashboard/page.tsx — Server Component (good!)
// Fetches data on the server, passes to a small client component

async function DashboardPage() {
  // This runs on the server — fast, no client bundle cost
  const stats = await getStats();
  const user = await getCurrentUser();

  return (
    <div>
      <h1>Welcome, {user.name}</h1>

      {/* Static parts rendered on server */}
      <StatsGrid stats={stats} />

      {/* Only the interactive button is a client component */}
      <RefreshButton />
    </div>
  );
}
```

```tsx
// components/RefreshButton.tsx — small Client Component at the "leaf"
"use client";

export default function RefreshButton() {
  return (
    <button onClick={() => window.location.reload()}>
      Refresh Dashboard
    </button>
  );
}
```

### Server vs Client: Quick Reference

| Feature | Server Component | Client Component |
|---|---|---|
| `"use client"` directive | Not needed | Required at top of file |
| Runs on | Server only | Browser (and server during SSR) |
| Can use hooks | No | Yes |
| Can use event handlers | No | Yes |
| Can fetch data directly (async) | Yes | No (use useEffect) |
| Access to secrets / DB | Yes | Never (exposed to browser) |
| Included in JS bundle | No (great for performance) | Yes |
| Can render Server Components inside | Yes | No |

---

## Data Fetching

### In Server Components (recommended)

```tsx
// app/products/page.tsx
async function ProductsPage() {
  // Simple fetch — runs on server
  const products = await fetch("https://api.example.com/products")
    .then(res => {
      if (!res.ok) throw new Error("Failed to fetch");
      return res.json();
    });

  return (
    <div>
      {products.map((p: any) => (
        <ProductCard key={p.id} product={p} />
      ))}
    </div>
  );
}

// Parallel data fetching (faster — both requests start at the same time)
async function DashboardPage() {
  // Start both requests simultaneously
  const [user, posts] = await Promise.all([
    fetch("/api/user").then(r => r.json()),
    fetch("/api/posts").then(r => r.json()),
  ]);

  return (
    <div>
      <UserCard user={user} />
      <PostList posts={posts} />
    </div>
  );
}
```

### In Client Components

```tsx
"use client";

import { useState, useEffect } from "react";

function ClientDataComponent({ id }: { id: string }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(`/api/items/${id}`)
      .then(r => r.json())
      .then(data => {
        setData(data);
        setLoading(false);
      });
  }, [id]);

  if (loading) return <p>Loading...</p>;
  return <div>{JSON.stringify(data)}</div>;
}

// Better: use React Query or SWR for client-side fetching
import useSWR from "swr";

const fetcher = (url: string) => fetch(url).then(r => r.json());

function ClientDataComponent({ id }: { id: string }) {
  const { data, isLoading, error } = useSWR(`/api/items/${id}`, fetcher);

  if (isLoading) return <p>Loading...</p>;
  if (error)     return <p>Error!</p>;
  return <div>{data.name}</div>;
}
```

---

## Caching in Next.js

Next.js 14+ has a powerful caching system. Understanding this is key to explaining why Next.js apps are so fast.

### Request Memoization

If you call the same `fetch` URL multiple times during one render pass, Next.js automatically deduplicates them — only one actual network request is made.

```tsx
// These two components both fetch the same URL
// Next.js only makes ONE real HTTP request

async function UserName() {
  const user = await fetch("/api/me").then(r => r.json()); // fetches
  return <span>{user.name}</span>;
}

async function UserAvatar() {
  const user = await fetch("/api/me").then(r => r.json()); // returns cached result
  return <img src={user.avatar} alt="avatar" />;
}
```

### Data Cache

Next.js caches fetch responses between requests. You control this with `cache` and `next.revalidate`.

```tsx
// Cache forever (like SSG — build time only)
const data = await fetch(url, { cache: "force-cache" });

// Never cache (like SSR — fresh on every request)
const data = await fetch(url, { cache: "no-store" });

// Cache and revalidate every 60 seconds (like ISR)
const data = await fetch(url, { next: { revalidate: 60 } });

// Cache with a tag (revalidate on demand)
const data = await fetch(url, { next: { tags: ["products"] } });
```

### Revalidating the Cache on Demand

```tsx
// app/api/revalidate/route.ts
import { revalidateTag, revalidatePath } from "next/cache";
import { NextRequest } from "next/server";

export async function POST(request: NextRequest) {
  const { tag, secret } = await request.json();

  // Protect with a secret
  if (secret !== process.env.REVALIDATE_SECRET) {
    return Response.json({ error: "Unauthorized" }, { status: 401 });
  }

  // Revalidate all fetches with this tag
  revalidateTag(tag);

  // Or revalidate a specific page path
  // revalidatePath("/products");

  return Response.json({ revalidated: true });
}
```

---

## Server Actions

Server Actions are **async functions that run on the server** but can be called directly from Client or Server Components. They are the Next.js way of handling form submissions and mutations without writing a separate API endpoint.

```tsx
// app/actions.ts
"use server";  // everything in this file runs on the server

import { revalidatePath } from "next/cache";
import { redirect } from "next/navigation";

// Server Action for creating a post
export async function createPost(formData: FormData) {
  const title   = formData.get("title") as string;
  const content = formData.get("content") as string;

  // Validate
  if (!title || title.length < 3) {
    return { error: "Title must be at least 3 characters" };
  }

  // Save to database
  await db.posts.create({ data: { title, content } });

  // Revalidate the posts page so it shows the new post
  revalidatePath("/posts");

  // Redirect to the posts page
  redirect("/posts");
}
```

### Using Server Actions in Forms

```tsx
// app/posts/new/page.tsx — Server Component
import { createPost } from "@/app/actions";

export default function NewPostPage() {
  return (
    <form action={createPost}>  {/* just pass the server action */}
      <input name="title"   placeholder="Post title" required />
      <textarea name="content" placeholder="Post content" />
      <button type="submit">Create Post</button>
    </form>
  );
}
```

### Server Actions with useFormState (for error handling)

```tsx
"use client";

import { useFormState, useFormStatus } from "react-dom";
import { createPost } from "@/app/actions";

// Show pending state on the submit button
function SubmitButton() {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Creating..." : "Create Post"}
    </button>
  );
}

export default function NewPostForm() {
  const [state, formAction] = useFormState(createPost, null);

  return (
    <form action={formAction}>
      {state?.error && <p className="error">{state.error}</p>}
      <input name="title" placeholder="Post title" />
      <textarea name="content" />
      <SubmitButton />
    </form>
  );
}
```

### Server Actions called programmatically

```tsx
"use client";

import { deletePost } from "@/app/actions";

export function DeleteButton({ postId }: { postId: string }) {
  const handleDelete = async () => {
    await deletePost(postId);  // calls server action directly
  };

  return <button onClick={handleDelete}>Delete</button>;
}
```

---

## API Routes

API Routes let you build backend endpoints inside your Next.js app. In the App Router, these are called **Route Handlers** and live in `route.ts` files.

```tsx
// app/api/users/route.ts

import { NextRequest, NextResponse } from "next/server";

// GET /api/users
export async function GET(request: NextRequest) {
  const { searchParams } = new URL(request.url);
  const page = searchParams.get("page") || "1";

  const users = await db.users.findMany({
    skip: (parseInt(page) - 1) * 10,
    take: 10,
  });

  return NextResponse.json({ users, page });
}

// POST /api/users
export async function POST(request: NextRequest) {
  const body = await request.json();

  // Validate
  if (!body.name || !body.email) {
    return NextResponse.json(
      { error: "Name and email are required" },
      { status: 400 }
    );
  }

  const user = await db.users.create({ data: body });

  return NextResponse.json(user, { status: 201 });
}
```

### Dynamic API Routes

```tsx
// app/api/users/[id]/route.ts

// GET /api/users/123
export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await db.users.findUnique({ where: { id: params.id } });

  if (!user) {
    return NextResponse.json({ error: "User not found" }, { status: 404 });
  }

  return NextResponse.json(user);
}

// PATCH /api/users/123
export async function PATCH(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const body = await request.json();
  const user = await db.users.update({
    where: { id: params.id },
    data: body,
  });
  return NextResponse.json(user);
}

// DELETE /api/users/123
export async function DELETE(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  await db.users.delete({ where: { id: params.id } });
  return new Response(null, { status: 204 });
}
```

### Route Handler with Headers and Cookies

```tsx
import { cookies, headers } from "next/headers";

export async function GET(request: NextRequest) {
  // Read headers
  const authHeader = request.headers.get("authorization");

  // Read cookies
  const cookieStore = cookies();
  const token = cookieStore.get("session_token")?.value;

  // Set response headers
  return NextResponse.json(
    { data: "protected data" },
    {
      headers: {
        "Cache-Control": "no-store",
        "X-Custom-Header": "my-value",
      },
    }
  );
}
```

---

## Static Generation (SSG)

Static Generation means Next.js **builds the HTML at build time** — once, when you run `next build`. The same HTML is served to every user. This is the fastest option because the page is just a static file.

```tsx
// App Router: a Server Component that fetches at BUILD TIME by default
// (when you do NOT use { cache: "no-store" })

// app/blog/page.tsx
async function BlogPage() {
  // This fetch is cached by default — runs at build time
  const posts = await fetch("https://api.example.com/posts", {
    cache: "force-cache"  // explicitly static (this is the default)
  }).then(r => r.json());

  return (
    <div>
      {posts.map((post: any) => (
        <article key={post.id}>
          <h2>{post.title}</h2>
        </article>
      ))}
    </div>
  );
}

// Pages Router equivalent (older way)
// export async function getStaticProps() {
//   const posts = await fetchPosts();
//   return { props: { posts } };
// }
```

### When to use SSG

- Blog posts, documentation, marketing pages
- Data that does not change often
- Pages that need the best possible performance and SEO
- E-commerce category pages that update infrequently

---

## Server-Side Rendering (SSR)

SSR means Next.js **renders the HTML on the server for every single request**. Fresh data every time, but slightly slower than SSG because it has to render on each request.

```tsx
// App Router: opt into SSR by using no-store cache
// app/dashboard/page.tsx

async function DashboardPage() {
  // { cache: "no-store" } = always fetch fresh, never cache = SSR behavior
  const data = await fetch("https://api.example.com/live-data", {
    cache: "no-store"
  }).then(r => r.json());

  return <Dashboard data={data} />;
}

// You can also use cookies() or headers() — using these
// automatically makes the route dynamic (SSR)
import { cookies } from "next/headers";

async function UserDashboard() {
  const cookieStore = cookies();
  const sessionToken = cookieStore.get("session")?.value;

  const user = await getUserFromSession(sessionToken);
  return <div>Welcome, {user.name}</div>;
}

// Pages Router equivalent (older way)
// export async function getServerSideProps(context) {
//   const data = await fetchData();
//   return { props: { data } };
// }
```

### When to use SSR

- User-specific pages (dashboard, account)
- Real-time data (stock prices, live scores)
- Pages that need request info (cookies, headers, query params)
- Content that changes very frequently

---

## Incremental Static Regeneration (ISR)

ISR is the best of both worlds. The page is **statically generated** (fast like SSG) but Next.js **automatically rebuilds it in the background** after a set time. Users always get a fast response, and data stays reasonably fresh.

```tsx
// App Router: use revalidate option
// app/products/page.tsx

async function ProductsPage() {
  // Cache this response and revalidate it in the background every 60 seconds
  const products = await fetch("https://api.example.com/products", {
    next: { revalidate: 60 }  // seconds
  }).then(r => r.json());

  return (
    <div>
      {products.map((p: any) => <ProductCard key={p.id} product={p} />)}
    </div>
  );
}

// You can also set revalidate at the route segment level
export const revalidate = 3600; // revalidate this page every hour

// Pages Router equivalent (older way)
// export async function getStaticProps() {
//   const products = await fetchProducts();
//   return { props: { products }, revalidate: 60 };
// }
```

### SSG vs SSR vs ISR Summary

| | SSG | SSR | ISR |
|---|---|---|---|
| When HTML is generated | Build time | Every request | Build time + background refresh |
| Data freshness | Build time only | Always fresh | Fresh within revalidate window |
| Speed | Fastest | Slower (per request) | Fast (like SSG) |
| Best for | Blogs, docs, marketing | Dashboards, user pages | E-commerce, news |
| Cache option | `force-cache` | `no-store` | `revalidate: N` |

---

## Dynamic Routes

Dynamic routes let one file handle many different URLs.

```tsx
// app/blog/[slug]/page.tsx
// Handles: /blog/hello-world, /blog/my-post, /blog/anything

interface PageProps {
  params: { slug: string };
}

async function BlogPostPage({ params }: PageProps) {
  const post = await fetch(`/api/posts/${params.slug}`).then(r => r.json());

  if (!post) {
    notFound();  // shows not-found.tsx
  }

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}

export default BlogPostPage;

// Pre-generate specific slugs at build time (for SSG)
export async function generateStaticParams() {
  const posts = await fetch("/api/posts").then(r => r.json());

  return posts.map((post: any) => ({
    slug: post.slug,
  }));
  // Generates: /blog/hello-world, /blog/my-post, etc.
}
```

### Catch-All Routes

```tsx
// app/docs/[...slug]/page.tsx
// Handles: /docs/intro, /docs/api/users, /docs/api/users/create

interface PageProps {
  params: { slug: string[] };  // array of segments
}

async function DocsPage({ params }: PageProps) {
  const path = params.slug.join("/");  // "api/users/create"
  const doc = await getDoc(path);
  return <DocContent doc={doc} />;
}

// Optional catch-all: app/docs/[[...slug]]/page.tsx
// Also handles /docs itself (slug is undefined)
```

### Dynamic Metadata

```tsx
// app/blog/[slug]/page.tsx

export async function generateMetadata({ params }: PageProps) {
  const post = await fetch(`/api/posts/${params.slug}`).then(r => r.json());

  return {
    title: post.title,
    description: post.excerpt,
    openGraph: {
      title: post.title,
      description: post.excerpt,
      images: [{ url: post.coverImage }],
    },
  };
}
```

---

## Route Groups and Parallel Routes

### Route Groups

Parentheses `(groupName)` in folder names create a **route group** — the folder name does not appear in the URL. Use this to organize files or apply different layouts to different sections.

```
app/
├── (marketing)/
│   ├── layout.tsx      ← marketing layout (header, hero, etc.)
│   ├── page.tsx        → "/"
│   ├── about/
│   │   └── page.tsx    → "/about"
│   └── pricing/
│       └── page.tsx    → "/pricing"
├── (app)/
│   ├── layout.tsx      ← app layout (sidebar, etc.) — different from marketing!
│   ├── dashboard/
│   │   └── page.tsx    → "/dashboard"
│   └── settings/
│       └── page.tsx    → "/settings"
└── (auth)/
    ├── login/
    │   └── page.tsx    → "/login"
    └── register/
        └── page.tsx    → "/register"
```

### Parallel Routes

Parallel routes let you render **multiple pages in the same layout at the same time**. You define "slots" with `@folderName`.

```
app/
└── dashboard/
    ├── layout.tsx
    ├── page.tsx
    ├── @analytics/
    │   └── page.tsx    ← analytics slot
    └── @team/
        └── page.tsx    ← team slot
```

```tsx
// app/dashboard/layout.tsx
export default function DashboardLayout({
  children,
  analytics,
  team,
}: {
  children: React.ReactNode;
  analytics: React.ReactNode;  // @analytics slot
  team: React.ReactNode;       // @team slot
}) {
  return (
    <div className="dashboard">
      <div className="main">{children}</div>
      <div className="right-panel">
        {analytics}
        {team}
      </div>
    </div>
  );
}
```

---

## Intercepting Routes

Intercepting routes let you **show a route inside the current layout** while keeping the URL updated. The classic use case is a photo feed where clicking a photo shows a modal, but if you open the direct URL you see the full page.

```
app/
├── feed/
│   └── page.tsx              → /feed (the photo feed)
└── photos/
    ├── [id]/
    │   └── page.tsx          → /photos/123 (full page view)
    └── (..)photos/           ← intercept /photos/* when coming from /feed
        └── [id]/
            └── page.tsx      → shows modal instead of full page
```

```tsx
// app/feed/(..)photos/[id]/page.tsx
// When navigating from /feed to /photos/123, shows this modal
// When directly visiting /photos/123, shows the full page instead

export default function PhotoModal({ params }: { params: { id: string } }) {
  return (
    <Modal>
      <Photo id={params.id} />
    </Modal>
  );
}
```

---

## Middleware

Middleware runs **before every request** is processed. It is perfect for authentication, redirects, A/B testing, and request modification.

```typescript
// middleware.ts (in the root of your project, next to /app)

import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  const pathname = request.nextUrl.pathname;

  // 1. Authentication: protect dashboard routes
  const token = request.cookies.get("session_token")?.value;

  if (pathname.startsWith("/dashboard")) {
    if (!token) {
      // Redirect to login, remember where they were going
      const loginUrl = new URL("/login", request.url);
      loginUrl.searchParams.set("callbackUrl", pathname);
      return NextResponse.redirect(loginUrl);
    }
  }

  // 2. Redirect old URLs
  if (pathname === "/old-about") {
    return NextResponse.redirect(new URL("/about", request.url));
  }

  // 3. Add custom headers to every response
  const response = NextResponse.next();
  response.headers.set("X-App-Version", "2.0.0");
  return response;

  // 4. Rewrite (change URL internally without redirect)
  // return NextResponse.rewrite(new URL("/new-path", request.url));
}

// Only run middleware on these paths (not on _next/static, api, etc.)
export const config = {
  matcher: [
    "/dashboard/:path*",
    "/profile/:path*",
    "/old-about",
  ],
};
```

---

## Image Optimization

Next.js has a built-in `<Image>` component that automatically optimizes images — resizing, converting to WebP, lazy loading, and preventing layout shift.

```tsx
import Image from "next/image";

// Local image (Next.js knows the dimensions automatically)
import heroPhoto from "@/public/hero.jpg";

function HeroSection() {
  return (
    <Image
      src={heroPhoto}
      alt="Hero photo"
      priority  // loads immediately (above the fold)
    />
  );
}

// Remote image (you provide width and height)
function UserAvatar({ user }: { user: any }) {
  return (
    <Image
      src={user.avatarUrl}
      alt={`${user.name}'s avatar`}
      width={64}
      height={64}
      className="rounded-full"
    />
  );
}

// Fill container (use when you do not know dimensions)
function CoverImage({ src }: { src: string }) {
  return (
    <div style={{ position: "relative", width: "100%", height: "400px" }}>
      <Image
        src={src}
        alt="Cover image"
        fill
        style={{ objectFit: "cover" }}
        sizes="(max-width: 768px) 100vw, 50vw"
      />
    </div>
  );
}
```

### Allowing Remote Image Domains

```javascript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "res.cloudinary.com",
      },
      {
        protocol: "https",
        hostname: "images.unsplash.com",
      },
    ],
  },
};

module.exports = nextConfig;
```

---

## Font Optimization

Next.js automatically downloads fonts and serves them from your own server — no request to Google Fonts at runtime, which is faster and more private.

```tsx
// app/layout.tsx
import { Inter, Roboto_Mono } from "next/font/google";
import localFont from "next/font/local";

// Google Font
const inter = Inter({
  subsets: ["latin"],
  display: "swap",           // show fallback font while loading
  variable: "--font-inter",  // CSS variable for use in Tailwind or CSS
});

// Monospace font for code blocks
const robotoMono = Roboto_Mono({
  subsets: ["latin"],
  variable: "--font-mono",
});

// Local font
const myFont = localFont({
  src: "./fonts/MyFont.woff2",
  variable: "--font-custom",
});

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${inter.variable} ${robotoMono.variable}`}>
      <body className={inter.className}>
        {children}
      </body>
    </html>
  );
}
```

---

## Metadata and SEO

Next.js has a built-in Metadata API for managing `<head>` tags, og:image, Twitter cards, and more.

```tsx
// app/layout.tsx — static metadata (applied to all pages unless overridden)
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: {
    default: "My App",
    template: "%s | My App",  // page titles become "About | My App"
  },
  description: "The best app ever built",
  keywords: ["nextjs", "react", "web development"],
  authors: [{ name: "Haseeb Javed" }],
  creator: "Haseeb Javed",

  // Open Graph
  openGraph: {
    type: "website",
    locale: "en_US",
    url: "https://myapp.com",
    siteName: "My App",
    title: "My App",
    description: "The best app ever",
    images: [
      {
        url: "https://myapp.com/og-image.png",
        width: 1200,
        height: 630,
        alt: "My App",
      },
    ],
  },

  // Twitter / X
  twitter: {
    card: "summary_large_image",
    title: "My App",
    description: "The best app ever",
    images: ["https://myapp.com/twitter-image.png"],
    creator: "@haseebjaved4212",
  },

  // Robots
  robots: {
    index: true,
    follow: true,
    googleBot: {
      index: true,
      follow: true,
    },
  },

  // Icons
  icons: {
    icon: "/favicon.ico",
    apple: "/apple-touch-icon.png",
  },
};
```

```tsx
// app/blog/[slug]/page.tsx — dynamic metadata per page
export async function generateMetadata({
  params,
}: {
  params: { slug: string };
}): Promise<Metadata> {
  const post = await getPost(params.slug);

  if (!post) return { title: "Post Not Found" };

  return {
    title: post.title,  // becomes "Post Title | My App" due to template
    description: post.excerpt,
    openGraph: {
      title: post.title,
      description: post.excerpt,
      type: "article",
      publishedTime: post.publishedAt,
      images: [{ url: post.coverImage }],
    },
  };
}
```

---

## Environment Variables

```bash
# .env.local (never commit this to git)
# Available on the SERVER only (safe for secrets)
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb
NEXTAUTH_SECRET=my-super-secret-key-32-chars-long
STRIPE_SECRET_KEY=sk_live_...
OPENAI_API_KEY=sk-...

# Available in the BROWSER (never put secrets here!)
# Must start with NEXT_PUBLIC_
NEXT_PUBLIC_APP_URL=https://myapp.com
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_...
NEXT_PUBLIC_GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX
```

```tsx
// Server Component or API route — can access all env vars
async function ServerComponent() {
  const dbUrl = process.env.DATABASE_URL;        // works
  const secret = process.env.NEXTAUTH_SECRET;    // works
  return <div>...</div>;
}

// Client Component — can only access NEXT_PUBLIC_ vars
"use client";
function ClientComponent() {
  const appUrl = process.env.NEXT_PUBLIC_APP_URL;  // works
  const dbUrl  = process.env.DATABASE_URL;          // undefined! (never exposed)
  return <div>...</div>;
}
```

```javascript
// next.config.js — expose to browser explicitly (alternative to NEXT_PUBLIC_)
module.exports = {
  env: {
    CUSTOM_KEY: process.env.CUSTOM_KEY,  // now available client-side
  },
};
```

---

## Next.js Link and Navigation

```tsx
import Link from "next/link";
import { useRouter, usePathname, useSearchParams } from "next/navigation";

// Basic link — prefetches the page when visible in viewport
<Link href="/about">About</Link>

// Styled active link
function NavLink({ href, children }: { href: string; children: React.ReactNode }) {
  const pathname = usePathname();
  const isActive = pathname === href;

  return (
    <Link
      href={href}
      className={isActive ? "font-bold text-blue-600" : "text-gray-600"}
    >
      {children}
    </Link>
  );
}

// Disable prefetching (for links the user rarely clicks)
<Link href="/rarely-visited" prefetch={false}>Rarely Visited</Link>

// Programmatic navigation (in Client Components)
"use client";

function GoBackButton() {
  const router = useRouter();

  return (
    <div>
      <button onClick={() => router.push("/dashboard")}>Go to Dashboard</button>
      <button onClick={() => router.replace("/login")}>Replace with Login</button>
      <button onClick={() => router.back()}>Go Back</button>
      <button onClick={() => router.refresh()}>Refresh Page</button>
    </div>
  );
}

// Read current path and search params
"use client";

function SearchBar() {
  const pathname     = usePathname();      // "/products"
  const searchParams = useSearchParams();  // URLSearchParams object
  const query        = searchParams.get("q");

  return <p>Searching for "{query}" on {pathname}</p>;
}
```

---

## Loading and Error States

### loading.tsx — Automatic loading UI

```tsx
// app/dashboard/loading.tsx
// Next.js automatically shows this while the dashboard page is loading

export default function DashboardLoading() {
  return (
    <div className="animate-pulse">
      <div className="h-8 bg-gray-200 rounded w-1/3 mb-4" />
      <div className="grid grid-cols-3 gap-4">
        {[1, 2, 3].map(i => (
          <div key={i} className="h-32 bg-gray-200 rounded" />
        ))}
      </div>
    </div>
  );
}
```

### error.tsx — Error UI

```tsx
// app/dashboard/error.tsx
"use client";  // Error components must be Client Components

import { useEffect } from "react";

export default function DashboardError({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    // Log the error to an error reporting service
    console.error(error);
  }, [error]);

  return (
    <div className="error-page">
      <h2>Something went wrong in the dashboard!</h2>
      <p>{error.message}</p>
      <button onClick={reset}>Try Again</button>
    </div>
  );
}
```

### not-found.tsx — 404 page

```tsx
// app/not-found.tsx — global 404 page
import Link from "next/link";

export default function NotFound() {
  return (
    <div className="not-found">
      <h1>404 — Page Not Found</h1>
      <p>The page you are looking for does not exist.</p>
      <Link href="/">Go Home</Link>
    </div>
  );
}

// Trigger it programmatically
import { notFound } from "next/navigation";

async function ProductPage({ params }: { params: { id: string } }) {
  const product = await getProduct(params.id);
  if (!product) notFound();  // shows not-found.tsx
  return <Product product={product} />;
}
```

---

## Streaming and Suspense

Streaming lets Next.js **send parts of the page to the browser as they are ready** instead of waiting for everything to load before sending anything. This makes the page feel much faster.

```tsx
// app/dashboard/page.tsx
import { Suspense } from "react";

// Each component fetches its own data
async function RevenueChart() {
  const data = await fetchRevenue();  // slow query
  return <Chart data={data} />;
}

async function RecentSales() {
  const sales = await fetchRecentSales();
  return <SalesTable sales={sales} />;
}

async function CardsSummary() {
  const summary = await fetchCardSummary();  // fastest
  return <Cards summary={summary} />;
}

// Dashboard page streams components as they become ready
export default async function DashboardPage() {
  return (
    <main>
      <h1>Dashboard</h1>

      {/* This resolves fast, shown immediately */}
      <Suspense fallback={<CardsSkeleton />}>
        <CardsSummary />
      </Suspense>

      {/* These are independent — stream in parallel */}
      <div className="grid grid-cols-2">
        <Suspense fallback={<ChartSkeleton />}>
          <RevenueChart />
        </Suspense>

        <Suspense fallback={<SalesSkeleton />}>
          <RecentSales />
        </Suspense>
      </div>
    </main>
  );
}
```

> **Interview Tip:** Without streaming, the whole page has to wait for the slowest data fetch before anything is shown. With streaming, the user sees parts of the page instantly and the slower parts pop in as they load. This dramatically improves the Largest Contentful Paint (LCP) metric.

---

## Authentication Patterns

### NextAuth.js (Auth.js) — most popular choice

```typescript
// app/api/auth/[...nextauth]/route.ts
import NextAuth from "next-auth";
import GitHub from "next-auth/providers/github";
import Credentials from "next-auth/providers/credentials";

const handler = NextAuth({
  providers: [
    // OAuth provider
    GitHub({
      clientId: process.env.GITHUB_ID!,
      clientSecret: process.env.GITHUB_SECRET!,
    }),

    // Email + password
    Credentials({
      credentials: {
        email: { type: "email" },
        password: { type: "password" },
      },
      async authorize(credentials) {
        const user = await getUserByEmail(credentials.email);
        if (!user) return null;

        const isValid = await bcrypt.compare(credentials.password, user.hashedPassword);
        if (!isValid) return null;

        return { id: user.id, email: user.email, name: user.name };
      },
    }),
  ],

  callbacks: {
    async session({ session, token }) {
      session.user.id = token.sub!;
      return session;
    },
  },

  pages: {
    signIn: "/login",   // custom login page
    error: "/auth/error",
  },
});

export { handler as GET, handler as POST };
```

```tsx
// Protect routes in middleware (cleanest approach)
// middleware.ts
import { getToken } from "next-auth/jwt";

export async function middleware(request: NextRequest) {
  const token = await getToken({ req: request });
  const isAuthPage = request.nextUrl.pathname.startsWith("/login");

  if (!token && !isAuthPage) {
    return NextResponse.redirect(new URL("/login", request.url));
  }

  if (token && isAuthPage) {
    return NextResponse.redirect(new URL("/dashboard", request.url));
  }

  return NextResponse.next();
}

export const config = {
  matcher: ["/dashboard/:path*", "/login"],
};
```

```tsx
// Get session in Server Component
import { getServerSession } from "next-auth";

async function ProfilePage() {
  const session = await getServerSession();
  if (!session) redirect("/login");

  return <h1>Hello, {session.user.name}</h1>;
}

// Get session in Client Component
"use client";
import { useSession, signIn, signOut } from "next-auth/react";

function AuthButton() {
  const { data: session, status } = useSession();

  if (status === "loading") return <p>Loading...</p>;

  if (!session) {
    return <button onClick={() => signIn()}>Sign In</button>;
  }

  return (
    <div>
      <p>Signed in as {session.user.email}</p>
      <button onClick={() => signOut()}>Sign Out</button>
    </div>
  );
}
```

---

## Next.js with TypeScript

TypeScript works out of the box in Next.js. Here are the most useful types.

```tsx
// Page props
interface PageProps {
  params: { id: string; slug: string };
  searchParams: { [key: string]: string | string[] | undefined };
}

export default function Page({ params, searchParams }: PageProps) {
  const query = searchParams.q as string;
  return <div>{params.id}</div>;
}

// Layout props
interface LayoutProps {
  children: React.ReactNode;
  params: { lang: string };
}

// API Route Handler
import { NextRequest, NextResponse } from "next/server";

export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
): Promise<NextResponse> {
  return NextResponse.json({ id: params.id });
}

// Server Action
"use server";

import { z } from "zod";

// Validate with Zod schema
const CreatePostSchema = z.object({
  title: z.string().min(3).max(100),
  content: z.string().min(10),
  published: z.boolean().default(false),
});

export async function createPost(formData: FormData) {
  const rawData = {
    title:     formData.get("title"),
    content:   formData.get("content"),
    published: formData.get("published") === "on",
  };

  const validated = CreatePostSchema.safeParse(rawData);

  if (!validated.success) {
    return { errors: validated.error.flatten().fieldErrors };
  }

  await db.posts.create({ data: validated.data });
  revalidatePath("/posts");
}

// next.config.js types
import type { NextConfig } from "next";

const config: NextConfig = {
  images: {
    remotePatterns: [{ protocol: "https", hostname: "*.cloudinary.com" }],
  },
};

export default config;
```

---

## Deployment

### Deploying to Vercel (easiest — made by the Next.js team)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy from your project folder
vercel

# Or connect your GitHub repo to vercel.com
# Every push to main auto-deploys
```

### Self-Hosting with Docker

```dockerfile
# Dockerfile
FROM node:20-alpine AS base

# Install dependencies
FROM base AS deps
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci

# Build the app
FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# Run the app
FROM base AS runner
WORKDIR /app
ENV NODE_ENV production

COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public

EXPOSE 3000
CMD ["node", "server.js"]
```

```javascript
// next.config.js — enable standalone output for Docker
module.exports = {
  output: "standalone",
};
```

### Deploying to a Node.js Server

```bash
# Build for production
npm run build

# Start the production server
npm start

# The server runs on port 3000 by default
# Use nginx or a load balancer in front of it
```

### next.config.js Common Options

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  // Enable React strict mode
  reactStrictMode: true,

  // Standalone output (for Docker)
  output: "standalone",

  // Image domains
  images: {
    remotePatterns: [
      { protocol: "https", hostname: "res.cloudinary.com" },
    ],
  },

  // Redirect
  async redirects() {
    return [
      { source: "/old-page", destination: "/new-page", permanent: true },
    ];
  },

  // Headers
  async headers() {
    return [
      {
        source: "/api/:path*",
        headers: [
          { key: "Access-Control-Allow-Origin", value: "*" },
        ],
      },
    ];
  },

  // Environment variables
  env: {
    APP_VERSION: "1.0.0",
  },
};

module.exports = nextConfig;
```

---

## Performance Best Practices

```tsx
// 1. Use Server Components by default, Client Components only when needed
// Every "use client" adds to the JavaScript bundle

// 2. Fetch data as close to where it is used as possible
// Instead of fetching in a parent and drilling props down:
async function ParentPage() {
  return (
    <div>
      <UserInfo />    {/* UserInfo fetches its own data */}
      <PostList />    {/* PostList fetches its own data */}
    </div>
  );
}

// 3. Parallel data fetching
const [a, b] = await Promise.all([fetchA(), fetchB()]);

// 4. Use next/image for all images
import Image from "next/image";

// 5. Use next/font for all fonts
import { Inter } from "next/font/google";

// 6. Stream slow parts with Suspense
<Suspense fallback={<Skeleton />}>
  <SlowComponent />
</Suspense>

// 7. Use generateStaticParams for dynamic routes you know ahead of time
export async function generateStaticParams() {
  const posts = await getPosts();
  return posts.map(p => ({ slug: p.slug }));
}

// 8. Route segment config for fine-grained control
// app/products/page.tsx
export const dynamic    = "force-static";   // always static
export const dynamic    = "force-dynamic";  // always SSR
export const revalidate = 3600;             // ISR: every hour

// 9. Lazy load heavy Client Components
import dynamic from "next/dynamic";

const HeavyChart = dynamic(() => import("@/components/HeavyChart"), {
  ssr: false,          // do not render on server (browser-only library)
  loading: () => <ChartSkeleton />,
});

// 10. Bundle analysis to find what is making your bundle large
// next.config.js
const withBundleAnalyzer = require("@next/bundle-analyzer")({
  enabled: process.env.ANALYZE === "true",
});
module.exports = withBundleAnalyzer(nextConfig);

// Run: ANALYZE=true npm run build
```

---

## Common Interview Questions

### Q1. What is Next.js and how is it different from plain React?
React is a UI library — it only handles the view layer. Next.js is a full framework built on React that adds file-based routing, server-side rendering, static generation, API routes, image optimization, font optimization, and much more. It lets you build full-stack applications in one codebase instead of setting up a separate backend.

### Q2. What is the difference between the App Router and Pages Router?
The App Router (introduced in Next.js 13) uses the `/app` directory and supports React Server Components, nested layouts, streaming with Suspense, and Server Actions. The Pages Router uses the `/pages` directory and uses special functions like `getServerSideProps` and `getStaticProps` for data fetching. New projects should use the App Router, but many existing apps still use Pages Router.

### Q3. What are React Server Components and why do they matter?
Server Components run only on the server — their code never goes to the browser. This means you can safely access databases, file systems, and secrets directly inside them. They also reduce the JavaScript bundle size because the component code itself is never sent to the client. They are the default in the App Router and are one of the biggest performance wins in Next.js 13+.

### Q4. What is the difference between SSG, SSR, and ISR?
SSG (Static Site Generation) builds the page at build time — fastest, great for content that does not change often. SSR (Server-Side Rendering) builds the page on the server for every single request — always fresh, but slower. ISR (Incremental Static Regeneration) is a hybrid — pages are statically generated but automatically rebuilt in the background after a set time. In the App Router, you control this with the `cache` and `revalidate` options on fetch calls.

### Q5. How does caching work in Next.js App Router?
Next.js has multiple cache layers. Request memoization deduplicates identical fetch calls within one render. The Data Cache persists fetch responses across requests, controlled by `cache: "force-cache"` (static), `cache: "no-store"` (no cache, always fresh), or `next: { revalidate: N }` (ISR). There is also the Router Cache on the client side that caches visited routes.

### Q6. What are Server Actions?
Server Actions are async functions marked with `"use server"` that run on the server but can be called directly from components. They let you handle form submissions and data mutations without writing a separate API endpoint. They integrate with React's form action prop and work with `useFormState` for handling errors and pending states.

### Q7. When should you use `"use client"` in App Router?
Use `"use client"` only when you actually need browser-specific features — `useState`, `useEffect`, event handlers (`onClick`, `onChange`), browser APIs like `localStorage` or `window`, or third-party libraries that require the browser. Keep as much of your component tree as possible as Server Components and push the client boundary to the smallest possible leaf components.

### Q8. What does Middleware do in Next.js?
Middleware runs before a request reaches your page or API route. It is perfect for authentication checks (redirect unauthenticated users to login), A/B testing, redirect rules, request header modification, rate limiting, and locale detection. It runs at the Edge, which means it is extremely fast. You define it in `middleware.ts` at the root of your project.

### Q9. How does the Next.js Image component improve performance?
The `next/image` component automatically resizes images to the correct dimensions, converts them to modern formats like WebP, adds lazy loading by default, prevents Cumulative Layout Shift (CLS) by reserving space before the image loads, and serves images through a CDN. All of this happens with zero configuration.

### Q10. What is `generateStaticParams` used for?
`generateStaticParams` tells Next.js which dynamic route values to pre-generate at build time. For example, if you have `/blog/[slug]` and 100 blog posts, you return all 100 slugs from `generateStaticParams` and Next.js builds all 100 pages as static HTML at build time. Without it, dynamic routes are rendered on-demand (SSR).

### Q11. What is the difference between `layout.tsx` and `template.tsx`?
Both wrap page content. A layout persists across navigation — it does not re-mount when you go between pages in the same layout, so its state is preserved. A template creates a fresh instance on every navigation — it re-mounts every time, which is useful when you want to reset state or run enter/exit animations on every page change.

### Q12. How do you handle environment variables in Next.js?
Variables in `.env.local` are available on the server only. Any variable you need in the browser must start with `NEXT_PUBLIC_`. Never put secrets, API keys, or database URLs in `NEXT_PUBLIC_` variables because they will be included in the client-side JavaScript and visible to anyone.

### Q13. What is streaming in Next.js and how does it help performance?
Streaming allows the server to send HTML to the browser in chunks as it is generated, instead of waiting for everything to finish. Combined with Suspense, you can wrap slow components in `<Suspense fallback={<Skeleton />}>` and the rest of the page renders immediately while the slow parts stream in when ready. This significantly improves Time to First Byte (TTFB) and Largest Contentful Paint (LCP).

### Q14. What are parallel routes and when would you use them?
Parallel routes let you render multiple pages simultaneously in the same layout using `@folder` slot syntax. The layout receives each slot as a prop and can show them at the same time. Classic use cases include dashboards where you want to show a stats panel and a feed side by side, each independently loading their own data. They also support independent error and loading states per slot.

### Q15. How do you protect routes in Next.js?
The best way is using Middleware — check for a session token in the request cookies and redirect to login if it is missing. This happens at the edge before the page even starts rendering, so it is fast and secure. For more fine-grained control inside a page, you can use `getServerSession` (NextAuth) in a Server Component and call `redirect("/login")` if the user is not authenticated.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Next.js, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).
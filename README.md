## What exactly is Next.js? 
**Next.js is like a supercharged version of React** that makes building websites easier and faster.  

### In Simple Terms:  
- **Makes React Better** – Handles tricky things like SEO, speed, and routing for you.  
- **Pre-renders Pages** – Loads instantly (like a brochure) or fetches fresh data (like a live feed).  
- **No Complicated Setup** – Just drop files in folders, and the routes work automatically.  
- **Backend + Frontend** – Lets you write server code (APIs) in the same project.  

### Why Use It?  
Want a **fast, SEO-friendly, full-stack website** without headaches? Next.js does the heavy lifting.  

**Example:**  
- Without Next.js → Your React site might load slow and struggle with SEO.  
- With Next.js → Pages load instantly, and Google loves them.  

#### Perfect for blogs, e-commerce, dashboards, and more! 🚀

---
---
---

## **React vs. Next.js**  

#### **React**  
- A **JavaScript library** for building dynamic and reusable user interfaces.  
- Focuses solely on the **view layer** (UI components).  
- Requires additional configurations for routing, data fetching, and SSR/SSG.  
- Ideal for **SPAs (Single-Page Applications)** where SEO is not a priority.  

#### **Next.js**  
- A **production-ready framework** built on top of React.  
- Extends React with powerful features like:  
  - Built-in **file-based routing**  
  - **Server-Side Rendering (SSR)** & **Static Site Generation (SSG)**  
  - API routes (**backend endpoints** within the same project)  
  - Automatic **code splitting** & **optimized performance**  
- Simplifies deployment with **zero-config optimizations** (image, font, script loading).  
- Perfect for **SEO-friendly websites, e-commerce, dashboards, and full-stack apps**.  

**Key Takeaway:**  
- Use **React** when you need full control over configurations.  
- Use **Next.js** when you want a **batteries-included** solution for fast, scalable, and SEO-optimized apps.  

### Why need to learn Next.js :

Learning Next.js is important because:  

1. **Faster Performance** – Built-in features like SSR, SSG, and ISR improve speed & SEO.  
2. **SEO-Friendly** – Better search engine visibility with server-side rendering.  
3. **Simplified Routing** – File-based routing makes navigation easy.  
4. **Full-Stack Capability** – Supports API routes for backend functionality.  
5. **React Optimization** – Enhances React with better rendering & performance.  
6. **Great Developer Experience** – Hot reloading, easy deployment, and strong community support.  

Ideal for modern, scalable web apps! 🚀

---
---
---

## Project structure

### 📁 **Top-Level Folders**  
These folders help organize your project files and static content.

| **Folder** | **Used For** |
|------------|--------------|
| `app`      | Main folder for pages and layouts using App Router |
| `pages`    | For routing using the older Pages Router (optional) |
| `public`   | For images, fonts, and other static files users can see |
| `src`      | (Optional) A folder to keep all your code in one place |


### 📄 **Top-Level Files**  
These files help in project setup, configuration, and environment handling.

| **File** | **Simple Explanation** |
|---------|------------------------|
| `next.config.js` | Settings for how Next.js works |
| `package.json` | Keeps list of packages (dependencies) and run scripts |
| `instrumentation.ts` | Used for performance tracking (monitoring tools) |
| `middleware.ts` | Runs code on each request before reaching pages |
| `.env` | File for secret keys or settings (for all environments) |
| `.env.local` | Your own machine’s local secret keys or settings |
| `.env.production` | Settings for live/production environment |
| `.env.development` | Settings for development/testing environment |
| `.eslintrc.json` | Rules for code quality checking (ESLint) |
| `.gitignore` | Tells Git which files/folders to ignore |
| `next-env.d.ts` | Helps TypeScript work with Next.js properly |
| `tsconfig.json` | Settings for TypeScript |
| `jsconfig.json` | Settings for JavaScript |


### 📂 **Routing Files**  
These files are used inside the `app/` folder to control how pages look and behave.

| **File Name** | **Used For** |
|---------------|--------------|
| `layout.js/.jsx/.tsx` | Defines layout — header, footer, sidebar etc. |
| `page.js/.jsx/.tsx` | Creates a webpage (like home, about, etc.) |
| `loading.js/.jsx/.tsx` | Shows loading spinner or message |
| `not-found.js/.jsx/.tsx` | Page shown when something isn’t found (404) |
| `error.js/.jsx/.tsx` | Shows an error message for that page |
| `global-error.js/.jsx/.tsx` | Handles app-wide errors (not just one page) |
| `route.js/.ts` | Used for building custom API routes |
| `template.js/.jsx/.tsx` | Helps re-render a layout with fresh data |
| `default.js/.jsx/.tsx` | Fallback page in parallel routing |

---
---
---

### React Server Components (RSCs)  
**React Server Components** allow rendering components *on the server* instead of the client, reducing bundle size and improving performance.  


### **Key Differences**  
| Feature               | Client Components (`'use client'`) | Server Components (Default) |
|-----------------------|-----------------------------------|----------------------------|
| **Rendering**         | Browser (Client-side)             | Server                     |
| **Interactivity**     | ✅ (useState, useEffect)          | ❌ (No hooks)              |
| **Bundle Size**       | Larger (JS sent to browser)       | Zero JS (HTML only)        |
| **Data Fetching**     | Client-side (e.g., `fetch`)       | Direct server access       |
| **SEO**               | Lower (CSR)                       | Higher (SSR/SSG)           |


### **How It Works**  
1. **Server** renders components → Sends lightweight HTML/JSON to client.  
2. **Client** hydrates only interactive parts (`'use client'`).  

### **Example: Server + Client Components**  
#### 1. **Server Component** (`app/page.js`)  
```jsx
// Server Component (No 'use client')
export default function Page() {
  // Fetch data DIRECTLY on server (no API call needed)
  const data = await fetch('https://api.example.com/posts').then(res => res.json());

  return (
    <div>
      <h1>Posts</h1>
      {/* Static list (Server-rendered) */}
      {data.map(post => (
        <Post key={post.id} post={post} />
      ))}
      {/* Interactive part (Client-rendered) */}
      <LikeButton />
    </div>
  );
}
```

#### 2. **Client Component** (`app/LikeButton.js`)  
```jsx
'use client'; // Opt into client-side interactivity
import { useState } from 'react';

export default function LikeButton() {
  const [likes, setLikes] = useState(0);
  return <button onClick={() => setLikes(likes + 1)}>👍 {likes}</button>;
}
```

### **Why Use Server Components?**  
- **Faster Loads**: No client-side JS for static parts.  
- **Secure**: Database/API keys stay server-side.  
- **Simpler Code**: Fetch data directly in components.  

**When to Avoid**:  
- Need `useState`, `useEffect`, or browser APIs (use `'use client'`).  

---
---
---

## Next.js File-System Routing

Next.js uses **folders & files** to define routes in your app. No manual setup needed!  

#### **Basic Rules**  
| Folder/File          | Becomes This Route  | Notes                          |
|----------------------|---------------------|--------------------------------|
| `app/page.js`        | `/` (Homepage)      | Required for each route.       |
| `app/about/page.js`  | `/about`            | Folders create the URL path.   |
| `app/blog/[id]/page.js` | `/blog/123`       | `[id]` = Dynamic segment.      |
| `app/(auth)/login/page.js` | `/login`   | `(auth)` = Route group (hidden in URL). |

#### **Special Files**  
- `layout.js` → Shared UI (e.g., navbar).  
- `loading.js` → Shows while page loads.  
- `error.js` → Displays if something breaks.  

#### **Example Structure**  
```
app/
├── (dashboard)/          ← Route Group
│   ├── settings/page.js  → /settings
│   └── layout.js        ← Shared layout
├── shop/
│   ├── [id]/page.js     → /shop/42
│   └── page.js          → /shop
└── page.js              → Homepage (/)
```

**Why It’s Awesome?**  
🚀 **No config needed** – Just add files!  
📂 **Clean organization** – Folders = URLs.  

---
---
---

## File-Based Routing

In the latest version of Next.js (using the `/app` directory), routing is **based on the file and folder structure** inside the `/app` folder.

#### 🧱 Basic Concept:
Each folder = one route segment  
Each special file = controls part of the page (e.g. `page.tsx`, `layout.tsx`)

### 📂 Simple Example:

```
app/
├── page.tsx          → route: `/`
├── about/
│   └── page.tsx      → route: `/about`
└── blog/
    ├── page.tsx      → route: `/blog`
    └── [id]/
        └── page.tsx  → route: `/blog/:id`
```


| File/Folder            | URL             | Description                        |
|------------------------|------------------|------------------------------------|
| `app/page.tsx`         | `/`              | Homepage                           |
| `app/about/page.tsx`   | `/about`         | Static route                       |
| `app/blog/page.tsx`    | `/blog`          | Blog listing page                  |
| `app/blog/[id]/page.tsx` | `/blog/123`    | Dynamic route for blog post ID     |


### 🧠 Special Files:
- `page.tsx`: defines a route’s page content.
- `layout.tsx`: wraps multiple pages with common layout (e.g., sidebar).
- `loading.tsx`: shows a loading screen while the page loads.
- `error.tsx`: custom error page for the route.
- `[param]`: dynamic route segments.

---
---
---

## Nested Routes

Let’s look at **nested routes** in the **Next.js App Router** with **2 easy examples**:

### ✅ Example 1: Dashboard and Settings Page

```
app/
└── dashboard/
    ├── layout.tsx
    └── settings/
        └── page.tsx
```

- `dashboard/layout.tsx` → Shared layout for all dashboard pages  
- `dashboard/settings/page.tsx` → Renders at **`/dashboard/settings`**

This is a **nested route** where the `settings` page lives inside the `dashboard` section and uses its layout.


### ✅ Example 2: Blog with Dynamic Post

```
app/
└── blog/
    ├── layout.tsx
    ├── page.tsx
    └── [slug]/
        └── page.tsx
```

- `blog/page.tsx` → Renders blog list at `/blog`
- `blog/[slug]/page.tsx` → Renders individual blog post at `/blog/some-title`

This is a nested + dynamic route. Each blog post page uses the blog layout and supports URLs like `/blog/hello-world`.

---
---
---

## Dynamic Routes

**Dynamic routes** let you create pages that work for multiple URLs based on a parameter (like an ID or slug). You create them using **square brackets** in folder names inside the `app/` directory.


### ✅ Example

```
export default async function Page({
  params,
}: {
  params: Promise<{ slug: string }>
}) {
  const { slug } = await params
  return <div>My Post: {slug}</div>
}
```

```
app/
└── product/
    └── [id]/
        └── page.tsx
```

➡️ This will match URLs like:

- `/product/123`
- `/product/shoes`
- `/product/any-value`

Inside the page, you can use `params` to access the dynamic value.

📘 Docs: [Dynamic Routes – Next.js](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes)

---
---
---

## Nested Dynamic Route

A **nested dynamic route** means you have a dynamic segment **inside a folder**, and that folder is also inside another route folder. This helps you build URLs like:

```
/products/product1/reviews/review2
```


### ✅ Example Folder Structure:

```
app/
└── products/
    └── [productId]/
          └── reviews/
                └── [reviewId]/
                        └── page.tsx
```

This structure matches URLs like:

- `/products/120/reviews/2024`
- `/products/234/reviews/394`

### 🔍 How It Works:

In `page.tsx`, you can access both dynamic parts using `params`:

```tsx
// Import Next.js navigation utilities and React
import { notFound } from "next/navigation";
import React from "react";

// Define TypeScript interface for component props
interface IProductReviewPageProps {
  params: Promise<{ productId: string; reviewId: string }>;
}

/**
 * ProductReviewPage Component
 * 
 * A dynamic page that displays product review information.
 * Handles both the product ID and review ID from the URL parameters.
 * 
 * @param {IProductReviewPageProps} props - Component props containing route parameters
 * @returns {Promise<React.JSX.Element>} - The rendered product review page
 */
const ProductReviewPage = async ({ params }: IProductReviewPageProps) => {
  // Destructure and await the route parameters
  const { productId, reviewId } = await params;

  // Validate reviewId - show 404 page if reviewId is greater than 1000
  if(parseInt(reviewId) > 1000) {
    notFound(); // Next.js function to show 404 page
  }

  // Render the product review information
  return (
    <div>
      <h1>Product Review Page</h1>
      <h2>Product Id: {productId}</h2>  {/* Display product ID */}
      <h2>Review Id: {reviewId}</h2>   {/* Display review ID */}
    </div>
  );
};

export default ProductReviewPage;

```

---
---
---

## Catch-All Segments

**Catch-all segments** let you match **multiple parts of a URL** in a single dynamic route — perfect for deeply nested or unknown URL structures.

---

### 🧩 Example:

Folder structure:

```
app/
  └── docs/
        └── [...slug]/
              └── page.tsx
```

Matches:

- `/docs`
- `/docs/intro`
- `/docs/2024/nextjs/app-router`

In `page.tsx`, the `params.slug` will be an **array** of the path segments.

For optional catch-all, use `[[...slug]]`.

```typescript
// Import React (required for JSX)
import React from "react";

// TypeScript interface defining the expected props structure
interface IDocsNestedPageProps {
  params: Promise<{ slug: string[] }>; // Accepts a Promise containing slug array
}

/**
 * DocsNestedPage Component
 * 
 * A dynamic nested documentation page handler that renders different content
 * based on the number of slug parameters in the URL path.
 * 
 * @param {IDocsNestedPageProps} props - Component props containing route parameters
 * @returns {Promise<React.JSX.Element>} - Rendered content based on slug length
 */
const DocsNestedPage = async ({ params }: IDocsNestedPageProps) => {
  // Await and destructure the slug array from route parameters
  const { slug } = await params;

  // Conditional rendering based on slug array length
  if (slug?.length === 1) {
    // Case 1: Single slug parameter (e.g., /docs/features)
    return <div>DocsNestedPage for {slug[0]}</div>;
  } else if (slug?.length === 2) {
    // Case 2: Two slug parameters (e.g., /docs/features/advanced)
    return (
      <div>
        DocNested Page for {slug[0]} and {slug[1]}
      </div>
    );
  }

  // Default case: No slug parameters (e.g., /docs)
  return <div>DocsNestedPage</div>;
};

export default DocsNestedPage;
```

If you use [...slug], the /docs route will not work unless you have a separate docs/page.tsx file. To make the slug optional and also handle /docs, use [[...slug]] instead. With this setup, when a user visits /docs, the catch-all route will still be triggered, and based on the example logic, the output will be: DocsNestedPage.

**Usage Examples**:
   - `/docs/api` → Shows "DocsNestedPage for api"
   - `/docs/api/v2` → Shows "DocNested Page for api and v2"
   - `/docs` → Shows "DocsNestedPage"

**Async Component**:
   - Uses `async/await` to handle Promise-wrapped params
   - Required for Server Components that need to process route params

This pattern is commonly used for:
- Documentation systems
- Nested category pages
- Hierarchical content structures
- Multi-segment dynamic routing

---
---
---

## 🚫 404 Not Found Page

To create a **custom 404 page** in the latest Next.js (using the `app/` directory), simply add a `not-found.tsx` file at the appropriate level:

#### 📁 Example:

```
app/
├── page.tsx
├── not-found.tsx ← ✅ custom 404 page
```

Then use the `notFound()` function from `next/navigation` inside your code to manually trigger it.

Here’s a proper example of using `notFound()` in the latest Next.js (App Router) to show a custom 404 page:

### 📁 Folder Structure

```
app/
├── product/
│     └── [id]/
│           ├── page.tsx
│           └── not-found.tsx
```

### 📄 `page.tsx`

```tsx
import { notFound } from 'next/navigation';

export default function ProductPage({ params }) {
  const { id } = params;

  const product = getProductById(id); // pretend function

  if (!product) {
    notFound(); // 👈 redirects to not-found.tsx
  }

  return <h1>{product.name}</h1>;
}
```

### 📄 `not-found.tsx`

```tsx
export default function NotFound() {
  return <h1>Product not found</h1>;
}
```

---
---
---

## What is File Colocation in Next.js (App Router)?

**File colocation** means keeping all files related to a route — like its `page.tsx`, `loading.tsx`, `error.tsx`, `layout.tsx`, and `components` — **in the same folder**. This keeps your project organized and modular.

### ✅ Example:

```
app/
└── dashboard/
    ├── page.tsx         ← main page
    ├── loading.tsx      ← loading state
    ├── error.tsx        ← error UI
    ├── layout.tsx       ← layout wrapper
    └── Chart.tsx        ← component used only by this route
```

Everything needed for the `/dashboard` route stays together.

🔗 [Official Docs](https://nextjs.org/docs/app/getting-started/project-structure#colocation)

---
---
---

## 🔒 What are Private Folders in Next.js?

In the **App Router** of Next.js, **private folders** are folder names that start with an underscore (`_`). These folders **won’t become routes**, and they are ignored by the routing system. You can use them to store reusable components, utilities, or logic related to a route — without exposing them in the URL.

---

#### ✅ Example:

```
app/
└── dashboard/
    ├── page.tsx
    └── _components/
        └── Chart.tsx
```

The `Chart.tsx` is used in `/dashboard`, but `/dashboard/_components` is **not accessible** via browser.

#### 📁 Folder Structure Example

```
app/
└── dashboard/
      ├── page.tsx
      └── _components/
            ├── Sidebar.tsx
            └── AnalyticsChart.tsx
```

#### 🔍 What’s Happening

- `page.tsx` is the main UI for `/dashboard`.
- `_components/` holds helper components like `Sidebar` and `AnalyticsChart` that are **only used inside dashboard**.
- Since the folder starts with `_`, **it won’t create a route** like `/dashboard/_components`.

➡️ Keeps your route folders clean and prevents accidental routing.

📘 [Next.js Docs – Private Folders](https://nextjs.org/docs/app/getting-started/project-structure#private-folders)

---
---
---

## 🧩 What are Route Groups in Next.js?

**Route Groups** in the Next.js App Router help you organize your folder structure **without affecting the URL path**.

You create a route group using parentheses:

#### 🏗️ Folder Structure

```
app/
├── (marketing)/
│   ├── home/
│   │   └── page.tsx
│   └── about/
│       └── page.tsx
├── (auth)/
│   ├── login/
│   │   └── page.tsx
│   └── register/
│       └── page.tsx
```


### 🔍 What URLs will look like:

| Folder Path                    | URL Path     |
|-------------------------------|--------------|
| `(marketing)/home/page.tsx`   | `/home`      |
| `(marketing)/about/page.tsx`  | `/about`     |
| `(auth)/login/page.tsx`       | `/login`     |
| `(auth)/register/page.tsx`    | `/register`  |


### ✅ Benefits:
- Keeps **marketing** and **auth** sections organized in separate groups.
- Doesn’t change the user-facing URL.
- Useful for applying **separate layouts** or middlewares to groups.

---
---
---

## 📐 What are Layouts in Next.js?

In the latest Next.js App Router, **layouts** are special React components that wrap around pages and **persist across route changes**. They’re used for shared UI like navigation bars, footers, sidebars, etc.

### ✅ Key Features:
- Defined using `layout.tsx`
- Can be nested at any level
- Don’t re-render on navigation unless their path changes
- Great for consistent design and structure

### 🎯 Real-World Use Case: Admin Dashboard

You have these routes:

- `/admin`
- `/admin/users`
- `/admin/settings`

And you want a **sidebar** and **top navigation** to stay visible across all admin pages.

### 📁 Folder Structure:

```
app/
└── admin/
    ├── layout.tsx       ← shared layout for all admin pages
    ├── page.tsx         ← main admin dashboard
    ├── users/
    │   └── page.tsx     ← users page
    └── settings/
        └── page.tsx     ← settings page
```

---

### 🧱 `layout.tsx`

```tsx
export default function AdminLayout({ children }) {
  return (
    <div className="flex">
      <Sidebar />
      <div className="flex-1">
        <TopNav />
        <main>{children}</main>
      </div>
    </div>
  );
}
```

### ✅ Result:

- All `/admin` routes use this layout.
- Layout is **persistent** – it doesn’t re-render on navigation within `/admin`.

---
---
---

## 🧱 What Are Nested Layouts in Next.js?

**Nested layouts** let you have multiple layers of layouts — each applying to a different part of your app. This is useful when different sections (like dashboard, profile, etc.) need their **own layout inside a shared layout**.

---

### 📁 Folder Structure:

```
app/
├── layout.tsx            ← Root layout (used everywhere)
├── dashboard/
│   ├── layout.tsx        ← Dashboard-specific layout
│   ├── page.tsx
│   └── settings/
│       └── page.tsx
```

---

### 🧩 How It Works:

1. `/dashboard/settings` will use:
   - `app/layout.tsx` (global)
   - `app/dashboard/layout.tsx` (section-specific)
   - `app/dashboard/settings/page.tsx` (page content)

---

### 💡 Example Code:

#### `app/layout.tsx` (global)

```tsx
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <Header />
        {children}
      </body>
    </html>
  );
}
```

#### `app/dashboard/layout.tsx` (nested layout)

```tsx
export default function DashboardLayout({ children }) {
  return (
    <div className="dashboard-layout">
      <Sidebar />
      <div>{children}</div>
    </div>
  );
}
```

#### `app/dashboard/settings/page.tsx`

```tsx
export default function SettingsPage() {
  return <h1>Settings</h1>;
}
```

---
---
---

## What Are Multiple Root Layouts in Next.js?

In Next.js, you can define **multiple root layouts** to create **completely separate sections of your app**—each with its own HTML structure, `<head>`, and layout logic. This is helpful for areas like:

- A marketing website
- A docs section
- A dashboard with login
- A blog

Each section can work independently, almost like mini apps inside your main app.

---

### 📁 Example Folder Structure:

```
app/
├── (marketing)/
│   ├── layout.tsx     → Root layout for marketing
│   └── page.tsx       → /
├── (dashboard)/
│   ├── layout.tsx     → Root layout for dashboard
|   └── dashboard
│          └── page.tsx       → /dashboard
```

In this setup:
- `/` uses `marketing/layout.tsx`
- `/dashboard` uses `dashboard/layout.tsx`

Each layout can have a **different HTML structure**: different `<html>`, `<head>`, themes, styles, or even script behavior.

---

### ✅ Use Cases:
- Different user roles (admin vs customer)
- Authenticated vs public sections
- Distinct branding/themes

---
---
---

## 📌 What is **Routing Metadata** in Next.js?

In the **App Router** of Next.js (latest versions), you can add **metadata** to any route — such as `<title>`, `<meta name="description">`, Open Graph tags, Twitter cards, icons, and more — **without touching `_document.tsx` or custom Head code**.

This helps improve **SEO**, **social sharing**, and **browser experience**, **per page or per layout**.

---

### 🔧 How to Add Metadata

Next.js provides 2 ways to define metadata:

#### 1. **Static Metadata** (basic usage)
Add a `metadata` object directly in your layout or page file.

```tsx
// app/about/page.tsx

export const metadata = {
  title: "About Us",
  description: "Learn more about our company and mission",
};
```

---

#### 2. **Dynamic Metadata** (when title or meta depends on dynamic data)

```tsx
// app/blog/[slug]/page.tsx

export async function generateMetadata({ params }) {
  const post = await getPost(params.slug);

  return {
    title: post.title,
    description: post.excerpt,
  };
}
```

---

### 📁 Metadata File Locations

| File Type      | Use Case                                         |
|----------------|--------------------------------------------------|
| `metadata` object in page.tsx or layout.tsx | Per route metadata |
| `icon.png`, `favicon.ico` in `/app` or `/public` | Icons and favicons |
| `manifest.webmanifest` in `/app` | PWA and web metadata |

---

### 🧪 Example with Open Graph and Twitter

```tsx
export const metadata = {
  title: "My Blog Post",
  description: "This is a blog post about Next.js routing.",
  openGraph: {
    title: "My Blog Post",
    description: "Open Graph description here",
    url: "https://example.com/blog/my-post",
    siteName: "Example Blog",
    images: [
      {
        url: "https://example.com/og-image.png",
        width: 800,
        height: 600,
      },
    ],
    locale: "en_US",
    type: "article",
  },
  twitter: {
    card: "summary_large_image",
    title: "My Blog Post",
    description: "Twitter card description",
    images: ["https://example.com/twitter-image.png"],
  },
};
```

This auto-injects SEO and social tags in the page's `<head>`.

---

### 📌 Benefits:

- Built-in TypeScript support
- Automatic `<head>` injection
- No need to manually use `<Head>` from `next/head`
- Scales across nested layouts/pages

---

### ✅ Use Cases

- Different `<title>` and `<description>` per page
- Dynamic meta tags for blog/news/product pages
- SEO + social media integration (OpenGraph/Twitter)

---
---
---

## 🏷️ What is title metadata?

Let’s go step by step to understand the different ways you can define **`title` metadata** in **Next.js App Router**, especially using:  

- **`default`**
- **`template`**
- **`absolute`**

---

### 🧠 First, What's `title` in Metadata?

The `title` defines the text that appears in:

- The **browser tab**
- **Search engines** like Google
- When **sharing on social media**

---

### 🧩 3 Ways to Define `title` Metadata in Next.js

### 1. ✅ **`default` title**
Used as a fallback when a page doesn’t define its own title.

```tsx
// app/layout.tsx

export const metadata = {
  title: {
    default: 'MySite',
  },
};
```

🟢 If a page doesn’t provide a title, "MySite" will be used.

---

### 2. 🧩 **`template` title**
Used to format all titles consistently.

```tsx
// app/layout.tsx

export const metadata = {
  title: {
    default: 'MySite',
    template: '%s | MySite',
  },
};
```

If a page sets:

```tsx
export const metadata = {
  title: 'About',
};
```

🟢 Final output:

```html
<title>About | MySite</title>
```

If a page doesn’t set a title, it uses the `default`, so:

```html
<title>MySite</title>
```

---

### 3. 🛑 **`absolute` title**
If you want to **bypass the template**, just return a string instead of using the object format.

```tsx
// app/special/page.tsx

export const metadata = {
  title: {
   absolute: 'Custom Landing Page Title', // Absolute title
  }
};
```

🟢 This will **not** use the `template` from layout. It’s a direct override.

```html
<title>Custom Landing Page Title</title>
```

---

### ✅ Summary Table

| Type       | Where to Use          | Behavior                                              |
|------------|------------------------|--------------------------------------------------------|
| `default`  | In `layout.tsx`        | Used if page doesn't define a title                   |
| `template` | In `layout.tsx`        | Formats all titles like `"About | MySite"`            |
| `absolute` | In individual `page.tsx` | Overrides the layout and uses plain title             |

---

### 🧪 Real-life Example

```tsx
// app/layout.tsx
export const metadata = {
  title: {
    default: 'Docs App',
    template: '%s - Docs App',
  },
};

// app/home/page.tsx
export const metadata = {
  title: 'Home',
}; 
// Result: <title>Home - Docs App</title>

// app/contact/page.tsx
export const metadata = {
  title: 'Contact Us',
};
// Result: <title>Contact Us - Docs App</title>

// app/landing/page.tsx
export const metadata = {
  title: '🚀 Welcome to Our Landing Page', // absolute
};
// Result: <title>🚀 Welcome to Our Landing Page</title>
```

---
---
---

### 🔗 What is the `Link` Component?

In **Next.js**, the `Link` component is used to **navigate between pages** in your app **without refreshing the page** (client-side navigation).

This makes navigation **faster and smoother**, just like in single-page applications (SPAs).

---

### 🧱 Basic Example

```tsx
// app/page.tsx or any React component

import Link from 'next/link';

export default function HomePage() {
  return (
    <div>
      <h1>Welcome</h1>
      <Link href="/about">Go to About Page</Link>
    </div>
  );
}
```

✅ Clicking the link takes you to `/about` **without reloading the whole page**.

---

### 💡 Why use `Link` instead of `<a>`?

| Feature                          | `<a>` tag           | `Link` component         |
|----------------------------------|----------------------|---------------------------|
| Full page reload?                | Yes                  | ❌ No                     |
| Preserves app state              | No                   | ✅ Yes                    |
| Optimized for Next.js routing    | ❌ No                | ✅ Yes                    |
| Preloads the linked page (lazy) | ❌ No                | ✅ Yes (on hover or view) |

---

### 🧭 With Dynamic Routes

```tsx
<Link href={`/blog/${slug}`}>Read More</Link>
```

If your folder structure is like:

```
app/
└── blog/
    └── [slug]/
        └── page.tsx
```

It’ll correctly link to the right blog post.

---

### 🎯 Adding Styling

You can wrap any element with `Link`, like a styled button or card:

```tsx
<Link href="/about">
  <button className="text-blue-500 underline">About Us</button>
</Link>
```

---

Let’s go through the **attributes (props)** you can use with the **`Link` component** in **Next.js** (latest App Router version) — explained in **simple English** with examples 🚀


### 🧩 Link Component Attributes

| Attribute      | Type     | Description                                                                 | Example                                                                 |
|----------------|----------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `href`         | `string` | ✅ **Required.** The path to navigate to.                                   | `<Link href="/about">About</Link>`                                     |
| `replace`      | `boolean`| Replaces the current history entry instead of adding a new one.             | `<Link href="/about" replace>About</Link>`                             |
| `prefetch`     | `boolean`| Preloads the page in the background when visible (enabled by default).      | `<Link href="/about" prefetch={false}>About</Link>`                    |
| `scroll`       | `boolean`| Controls whether to scroll to top of page after navigation.                 | `<Link href="/about" scroll={false}>About</Link>`                      |
| `shallow`      | `boolean`| Updates the URL without running `getServerSideProps` / data fetching again.| (Used in Pages Router only)                                            |
| `legacyBehavior` | `boolean` | Renders an anchor (`<a>`) tag as a child (older behavior).                | `<Link href="/about" legacyBehavior><a>About</a></Link>`              |
| `locale`       | `string` or `false` | Controls which locale is used when navigating (for i18n).         | `<Link href="/about" locale="fr">About (FR)</Link>`                   |
| `passHref`     | `boolean`| Ensures `href` is passed to the child. Used with `legacyBehavior`.         | `<Link href="/about" passHref legacyBehavior><a>About</a></Link>`     |

---

## ✅ Examples for Key Attributes

### 1. 🔁 `replace`

```tsx
<Link href="/profile" replace>
  Go to Profile
</Link>
```

This won’t add a new entry to browser history — it **replaces** the current one.

---

### 2. 💤 `prefetch`

```tsx
<Link href="/contact" prefetch={false}>
  Contact Us
</Link>
```

Disables automatic background preloading (useful if the page is rarely visited).

---

### 3. 🎯 `scroll`

```tsx
<Link href="/faq" scroll={false}>
  FAQ
</Link>
```

Prevents auto scroll to top after navigation. Keeps current scroll position.

---

### 4. 🌐 `locale`

```tsx
<Link href="/about" locale="de">
  Über uns (German)
</Link>
```

Will navigate to the German version of the page if internationalization is enabled.

---

### ⚠️ Note

- `shallow` only works with the **Pages Router**, not App Router.
- Most of the time, just using `href` is enough.
- `prefetch`, `replace`, and `scroll` are the most commonly used optional props.

---

### ✅ Summary

- `Link` is used for **client-side navigation**
- It replaces traditional `<a>` in most cases
- Helps with **faster page transitions**
- Works with **dynamic routes** too
- Supports **preloading** of pages

---
---
---

## 🔗 What is an Active Link?

An **Active Link** is the navigation link that points to the **current route/page** the user is on.

👉 It’s commonly used to **highlight the current page** in a navigation bar.  


## 🧠 How to Create Active Links in Next.js App Router?

Next.js doesn't highlight active links automatically. You need to do it **manually using the `usePathname()` hook** from `next/navigation`.

---

## ✅ Step-by-Step Example

### 1. 🧩 Setup Links

```tsx
// app/components/NavLink.tsx
'use client';

import Link from 'next/link';
import { usePathname } from 'next/navigation';
import clsx from 'clsx'; // Optional: helps handle conditional classNames

type NavLinkProps = {
  href: string;
  children: React.ReactNode;
};

export default function NavLink({ href, children }: NavLinkProps) {
  const pathname = usePathname();

  const isActive = pathname === href;

  return (
    <Link
      href={href}
      className={clsx(
        'px-4 py-2 rounded',
        isActive ? 'bg-blue-600 text-white' : 'text-gray-700'
      )}
    >
      {children}
    </Link>
  );
}
```

> 🛠️ We're using `clsx` to manage conditional class names. You can use plain JS `? :` too.

---

### 2. 🧭 Use in Your Layout or Header

```tsx
// app/components/Navbar.tsx

import NavLink from './NavLink';

export default function Navbar() {
  return (
    <nav className="flex space-x-4 p-4 border-b">
      <NavLink href="/">Home</NavLink>
      <NavLink href="/about">About</NavLink>
      <NavLink href="/blog">Blog</NavLink>
    </nav>
  );
}
```

---

## 🧠 Logic Behind It

- `usePathname()` gives you the **current route** (like `/about`).
- You compare it to each `Link`'s `href`.
- If they match → it’s active → apply special styling.

---

## 🧪 Optional: Partial Matching

If you want `/blog/post-1` to still highlight `/blog`, use:

```tsx
const isActive = pathname.startsWith(href);
```

Just be careful: `/blog` will also match `/blog123`. You can customize logic as needed.

---

## ✅ Final Output

Your navbar will **automatically highlight the current page**, no matter where the user is in your app — and it works **client-side** without refreshes.

---
---
---

## 🧾 What are `params` and `searchParams`?

| Name           | What it means                            | Where it comes from                     |
|----------------|------------------------------------------|------------------------------------------|
| `params`       | Dynamic parts of the **URL path**        | Comes from the **file name** or **folder** |
| `searchParams` | Query parameters after `?` in the URL    | Comes from the **URL's query string**     |

---

## 🔹 `params` — (for dynamic routes)

**URL:**  
```
/blog/hello-world
```

**Folder structure:**
```
app/
  blog/
    [slug]/
      page.tsx
```

### 👉 Usage

```tsx
// app/blog/[slug]/page.tsx

type Props = {
  params: { slug: string };
};

export default function BlogPost({ params }: Props) {
  return <h1>Blog Slug: {params.slug}</h1>;
}
```

✅ `params.slug` will be `'hello-world'`

---

## 🔸 `searchParams` — (for query strings)

**URL:**  
```
/products?category=shoes&sort=price
```

### 👉 Usage

```tsx
// app/products/page.tsx

type Props = {
  searchParams: { [key: string]: string | string[] | undefined };
};

export default function Products({ searchParams }: Props) {
  const category = searchParams.category;
  const sort = searchParams.sort;

  return (
    <div>
      <p>Category: {category}</p>
      <p>Sort By: {sort}</p>
    </div>
  );
}
```

✅ Outputs:
```
Category: shoes  
Sort By: price
```

---

## ✅ Summary Table

| Feature         | `params`                     | `searchParams`                          |
|-----------------|------------------------------|------------------------------------------|
| Location        | URL **path**                 | URL **query string**                     |
| Source          | From folder/file name like `[slug]` | From `?key=value` in the URL          |
| Usage example   | `/blog/abc` → `params.slug = abc` | `/blog?lang=en` → `searchParams.lang = en` |

---
---
---

## `useParams()` – Get Dynamic Route Segments
`useParams()` is a **React hook** from `next/navigation` that gives access to **dynamic route segments** (like `[id]`, `[slug]`) inside **client components**.

### 📁 Example Route:
```
/app/product/[id]/page.tsx
```

### 🔗 URL:
```
/product/42
```

### 📄 Client Component:
```tsx
'use client';
import { useParams } from 'next/navigation';

const ProductClient = () => {
  const params = useParams();

  return (
    <div>
      <h2>Product ID: {params.id}</h2>
    </div>
  );
};

export default ProductClient;
```

### 🧠 Output:
```
Product ID: 42
```

---
---
---

## `useSearchParams()` – Get Query String Parameters
`useSearchParams()` is another hook from `next/navigation`. It gives access to the **query parameters** in the URL (the part after `?`).


### 🔗 URL:
```
/product/42?ref=homepage&sort=asc
```

### 📄 Client Component:
```tsx
'use client';
import { useSearchParams } from 'next/navigation';

const SearchClient = () => {
  const searchParams = useSearchParams();
  const ref = searchParams.get('ref');
  const sort = searchParams.get('sort');

  return (
    <div>
      <p>Referrer: {ref}</p>
      <p>Sort: {sort}</p>
    </div>
  );
};

export default SearchClient;
```

### 🧠 Output:
```
Referrer: homepage
Sort: asc
```

---

## 📋 Comparison Table

| Feature               | `useParams()`                        | `useSearchParams()`                         |
|----------------------|---------------------------------------|---------------------------------------------|
| What it reads         | Dynamic path segments (e.g., `[id]`) | URL query string (e.g., `?sort=asc`)         |
| Returns               | Object `{ id: 'value' }`             | `URLSearchParams` object                    |
| Example               | `/blog/123` → `{ id: '123' }`        | `/blog?ref=google` → `.get('ref')` = google |
| Where to use          | Only in client components            | Only in client components                   |
| Import from           | `next/navigation`                    | `next/navigation`                           |

---

## 💡 Pro Tips

- These only work in **client components** (`'use client'` required at top).
- You can **combine** both in a single component if needed.
- `useParams()` returns values as **strings**, even if it looks like a number.

----
----
----

## Navigating programmatically in Next.js App Router

Navigating **programmatically** in **Next.js App Router** is super easy and powerful using the `useRouter()` hook from `next/navigation`. Let me walk you through it step-by-step with examples 👇

### ✅ `useRouter()` – Navigate with JavaScript

#### 🔁 1. **Navigate to another route**

```tsx
'use client';
import { useRouter } from 'next/navigation';

export default function ButtonComponent() {
  const router = useRouter();

  const handleClick = () => {
    router.push('/about'); // Navigate to /about
  };

  return <button onClick={handleClick}>Go to About Page</button>;
}
```

> ✅ `router.push('/route')` → Navigates to the specified route

---

#### 🔄 2. **Navigate with dynamic route & query params**

```tsx
'use client';
import { useRouter } from 'next/navigation';

export default function ProductButton() {
  const router = useRouter();

  const goToProduct = () => {
    const id = 101;
    router.push(`/product/${id}?ref=homepage`);
  };

  return <button onClick={goToProduct}>View Product</button>;
}
```

---

#### 🔙 3. **Go Back / Forward in History**

```tsx
'use client';
import { useRouter } from 'next/navigation';

export default function NavButtons() {
  const router = useRouter();

  return (
    <div>
      <button onClick={() => router.back()}>⬅️ Go Back</button>
      <button onClick={() => router.forward()}>➡️ Go Forward</button>
    </div>
  );
}
```

---

#### ✏️ 4. **Replace URL (without pushing new history)**

```tsx
router.replace('/dashboard'); // No history entry added
```

---

#### 💥 5. **Refresh the current route**

```tsx
router.refresh(); // Useful after data mutation
```

---

#### 🚀 Summary of `useRouter()` methods

| Method              | Purpose                                |
|---------------------|-----------------------------------------|
| `push(url)`         | Navigate to a new route                 |
| `replace(url)`      | Navigate without adding to history      |
| `back()`            | Go back in browser history              |
| `forward()`         | Go forward in history                   |
| `refresh()`         | Re-fetch server components on the page  |

#### ✅ router.push() with Object (Query Params)

🔧 Syntax:
```tsx
Copy
Edit
router.push({
  pathname: '/products/101',
  query: {
    ref: 'demo',
    campaign: 'summer'
  }
});
```

**This results in the URL: /products/101?ref=demo&campaign=summer**


---
---
---


# 💱 FINANCIAL DASHBOARD WITH NEXT.JS 💰

## 🚩 Creating the project

- To create a Next.js app, open your terminal,
- cd into the folder you’d like to keep your project,
- and run the following command:
- This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

```bash
npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"
cd nextjs-dashboard
```

- This command uses create-next-app, a Command Line Interface (CLI) tool that sets up a Next.js application for you.
- In the command above, you’re also using the --example flag with the [starter example](https://github.com/vercel/next-learn/tree/main/dashboard/starter-example) for this course.

## 📂 FOLDER STRUCTURE

- `/app:` Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
- `/app/lib:` Contains functions used in your application, such as reusable utility functions and data fetching functions.
- `/app/ui:` Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
- `/public:` Contains all the static assets for your application, such as images.
- `/scripts/:` Contains a file that you'll use to populate your database in a later chapter.
- `Config Files:` You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

## 📝 PLACEHOLDER DATA:

When you're building user interfaces, it helps to have some placeholder data. If a database or API is not yet available, you can:

- Use placeholder data in JSON format or as JavaScript objects.
- Use a 3rd party service like [mockAPI](https://mockapi.io/).

For this project, we’ve provided some placeholder data in `app/lib/placeholder-data.js.` Each JavaScript object in the file represents a table in your database. For example, for the `invoices table`:

```javascript
const invoices = [
  {
    customer_id: customers[0].id,
    amount: 15795,
    status: 'pending',
    date: '2022-12-06',
  },
  {
    customer_id: customers[1].id,
    amount: 20348,
    status: 'pending',
    date: '2022-11-14',
  },
  // ...
];
```

## 🛡️ TYPESCRIPT

- Take a look at the `/app/lib/definitions.ts` file. 
- Here, we manually define the types that will be returned from the database.
- For example, the invoices table has the following types:

```typescript
export type Invoice = {
  id: string;
  customer_id: string;
  amount: number;
  date: string;
  // In TypeScript, this is called a string union type.
  // It means that the "status" property can only be one of the two strings: 'pending' or 'paid'.
  status: 'pending' | 'paid';
};
```

### 🛑 By using TypeScript, you can ensure you don't accidentally pass the wrong data format to your components or database, like passing a string to amount instead of a number

## 🖥️ Running the development server

```bash
npm i
npm run dev
```

- `npm run dev` starts your Next.js development server on port 3000.
- Let’s check to see if it’s working. Open http://localhost:3000 on your browser.

# 🚩 CSS STYLING

## 🛑 Global Styles

- If you look inside the `/app/ui` folder, you'll see a file called `global.css.`
- You can use this file to add CSS rules to all the routes in your application - such as CSS reset rules, site-wide styles for HTML elements like links, and more.
- You can import `global.css` in any component in your application, but it's usually good practice to add it to your TOP-LEVEL component.
- In Next.js, this is the `ROOT LAYOUT` (more on this later).
- Add global styles to your application by navigating to `/app/layout.tsx` and importing the `global.css` file:

```typescript
import '@/app/ui/global.css';
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

### ⁉️ But wait a second, you didn't add any CSS rules, where did the styles come from?

- If you take a look inside `global.css`, you'll notice some `@tailwind` directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 🛑 TAILWIND

- Tailwind is a CSS framework that speeds up the development process by allowing you to quickly write utility classes directly in your JSX markup.
- The CSS styles are shared globally, but each utility is singularly focused and applied to each individual element.
- This means you don't have to worry about style collisions, maintaining separate stylesheets, or your CSS bundle size growing as your application grows.
- In Tailwind, you add style elements by adding class names.
- For example, adding the class "text-blue-500" will turn the `<h1>` text blue:

```javascript
<h1 className="text-blue-500">I'm blue!</h1>
```

- When you use `create-next-app` to start a new project, Next.js will ask if you want to use Tailwind. If you select yes, it will automatically install the necessary packages and configure Tailwind in your application.

- If you look at `/app/page.tsx`, you'll see that we're using Tailwind classes in the example.

```typescript
import AcmeLogo from '@/app/ui/acme-logo';
import Link from 'next/link';
 
export default function Page() {
  return (
    // These are Tailwind classes:
    <main className="flex min-h-screen flex-col p-6">
      <div className="flex h-20 shrink-0 items-end rounded-lg bg-blue-600 p-4 md:h-52">
    // ...
  )
}
```

### 🔍 Let's play with Tailwind! Copy the code below and paste it above the `<p>` element in `/app/page.tsx`

```typescript
<div className="h-0 w-0 border-b-[30px] border-l-[20px] border-r-[20px] border-b-black border-l-transparent border-r-transparent"/>
```

## 🛑 CSS MODULES

- If you prefer writing traditional CSS rules or keeping your styles separate from your JSX, CSS Modules are a great alternative.

- CSS Modules allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about name collisions.

- Here's how you could create the same shape from the quiz above using CSS modules. You can experiment with using these modules in the following way if you like, but we'll continue using Tailwind in this course:

- Inside `/app/ui` you would create a new file called `home.module.css` and add the following CSS rules:

```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

- Then, inside your `/app/page.tsx` file import the styles and replace the tailwind class names from the `<div>`, and pass `styles.shape` instead:

```typescript
import styles from '@/app/ui/home.module.css';
 
//...
<div className={styles.shape}></div>;
```

✅ Save your changes and preview them in the browser. You should see the same shape as before.

❇️ Tailwind and CSS modules are the two most common ways of styling Next.js applications. Whether you use one or the other is a matter of preference - you can even use both in the same application!

## 🛑 Using the clsx Library to toggle class names

- There may be cases where you may need to conditionally style an element based on state or some other condition.

- [clsx](https://www.npmjs.com/package/clsx) is a library that lets you toggle class names easily. We recommend taking a look at [documentation](https://github.com/lukeed/clsx) for more details, but here's the basic usage:

  + Suppose that you want to create an InvoiceStatus component which accepts status.
  + The status can be 'pending' or 'paid'.
  + If it's 'paid', you want the color to be <span style="color:green;">green> </span>.
  + If it's 'pending', you want the color to be <span style="color:gray;">gray> </span>.

- You can use clsx to conditionally apply the classes in `/app/ui/invoices/status.tsx`, like this:

```typescript
import clsx from 'clsx';
 
export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```

## 🛑 Other styling solutions

In addition to the approaches we've discussed, you can also style your Next.js application with:

  + Sass which allows you to import .css and .scss files.
  + CSS-in-JS libraries such as styled-jsx, styled-components, and emotion.

Take a look at the CSS documentation for more information.

## 🛑 Optimizing Fonts and Images

### ⁉️ Why optimize fonts?

- Fonts play a significant role in the design of a website, but using custom fonts in your project can affect performance if the font files need to be fetched and loaded.

- [Cumulative Layout Shift](https://web.dev/articles/cls?hl=tr) is a metric used by `Google` to evaluate the performance and user experience of a website.
- With fonts, layout shift happens when the browser initially renders text in a fallback or system font and then swaps it out for a custom font once it has loaded.
- This swap can cause the text size, spacing, or layout to change, shifting elements around it.
- Next.js automatically optimizes fonts in the application when you use the `next/font` module.
- It does so by downloading font files at build time and hosting them with your other static assets.
- This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

Let's add a custom Google font to your application to see how this works!

### 🚩 Adding a primary font

- In your `/app/ui` folder, create a new file called `fonts.ts`
- You'll use this file to keep the fonts that will be used throughout your application.
- Import the `Inter` font from the `next/font/google module` - this will be your primary font.

```typescript
import { Inter } from 'next/font/google';
```

- Then, specify what [subset](https://fonts.google.com/knowledge/glossary/subsetting) you'd like to load. In this case, `latin`:

```typescript
import { Inter } from 'next/font/google';

export const inter = Inter({ subsets: ['latin'] });
```

- Finally, add the font to the `<body>` element in `/app/layout.tsx`:

```typescript
import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

- By adding Inter to the `<body>` element, the font will be applied throughout your application.
- Here, you're also adding the Tailwind [antialiased](https://tailwindcss.com/docs/font-smoothing) class which smooths out the font. It's not necessary to use this class, but it adds a nice touch to your fonts.

- Navigate to your browser, open `dev tools` and select the body element. You should see `Inter` and `Inter_Fallback` are now applied under styles. You can also add fonts to specific elements of your application.

## 🚩 To add another custom fonts; customize `fonts.ts` and `page.tsx` file:

```typescript
import { Inter, Lusitana } from 'next/font/google';
 
export const inter = Inter({ subsets: ['latin'] });
 
export const lusitana = Lusitana({
  weight: ['400', '700'],
  subsets: ['latin'],
});
```

```typescript
import AcmeLogo from '@/app/ui/acme-logo';
import Link from 'next/link';
import styles from '@/app/ui/home.module.css';
import { lusitana } from '@/app/ui/fonts';


export default function Page() {
  return (
    <main className="flex min-h-screen flex-col p-6">
      <div className={`${lusitana.className} text-xl text-gray-800 md:text-3xl md:leading-normal`}>
        {/* <AcmeLogo /> */}
      </div>
      <div className="mt-4 flex grow flex-col gap-4 md:flex-row">
        <div className="flex flex-col justify-center gap-6 rounded-lg bg-gray-50 px-6 py-10 md:w-2/5 md:px-20">
          <div className={styles.shape}/>
          <p className={`text-xl text-gray-800 md:text-3xl md:leading-normal`}>
            <strong>Welcome to Acme.</strong> This is the example for the{' '}
            <a href="https://nextjs.org/learn/" className="text-blue-500">
              Next.js Learn Course
            </a>
            , brought to you by Vercel.
          </p>
          <Link
            href="/login"
            className="flex items-center gap-5 self-start rounded-lg bg-blue-500 px-6 py-3 text-sm font-medium text-white transition-colors hover:bg-blue-400 md:text-base"
          >
            <span>Log in</span>
          </Link>
        </div>
        <div className="flex items-center justify-center p-6 md:w-3/5 md:px-28 md:py-12">
          {/* Add Hero Images Here */}
        </div>
      </div>
    </main>
  );
}
```

## 🚩 The `<Image>` component

- Instead of manually handling these optimizations, you can use the `next/image` component to automatically optimize your images.

- The `<Image>` Component is an extension of the HTML `<img>` tag, and comes with automatic image optimization, such as:

  + Preventing layout shift automatically when images are loading.
  + Resizing images to avoid shipping large images to devices with a smaller viewport.
  + Lazy loading images by default (images load as they enter the viewport).
  + Serving images in modern formats, like [WebP](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types#webp) and [AVIF](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types#avif_image), when the browser supports it.

## ❇️ Adding the desktop hero image

- Let's swap the `<img>` tag for an `<Image>` component.

- In your `/app/page.tsx` file, import the component from `next/image`.

- Then, add the image under the comment in `/app/page.tsx`:

```typescript
import Image from 'next/image';
 
export default function Page() {
  return (
    // ...
    <div className="flex items-center justify-center p-6 md:w-3/5 md:px-28 md:py-12">
      {/* Add Hero Images Here */}
      <Image
        src="/hero-desktop.png"
        width={1000}
        height={760}
        className="hidden md:block"
        alt="Screenshots of the dashboard project showing desktop and mobile versions"
      />
    </div>
    //...
  );
}
```

- Here, you're setting the `width` to 1000 and `height` to 760 pixels.
- It's good practice to set the width and height of your images to avoid layout shift, these should be an aspect ratio identical to the source image.
- You'll also notice the class `hidden` to remove the image from the DOM on mobile screens, and `md:block` to show the image on desktop screens.

### 🚩 Add another hero images for mobile devices in `page.tsx`

```typescript
  <Image
    src="/hero-mobile.png"
    width={560}
    height={620}
    className="block md:hidden"
    alt="Screenshots of the dashboard project showing mobile versions"
  />
```

- 👆 It will be shown on mobile screens, and hidden on desktop with `block md:hidden`

## ✅ Recommended reading

- [Image Optimization Docs](https://nextjs.org/docs/app/building-your-application/optimizing/images)
- [Font Optimization Docs](https://nextjs.org/docs/app/building-your-application/optimizing/fonts)
- [Improving Web Performance with Images (MDN)](https://developer.mozilla.org/en-US/docs/Learn/Performance/Multimedia)
- [Web Fonts (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)

<hr>

## 🚩 Creating Layouts and Pages

### ❇️ Nested routing

- Next.js uses file-system routing where folders are used to create nested routes.
- Each folder represents a route segment that maps to a URL segment 👇

  + acme.com/`dashboard`/`incoices`

- `page.tsx` is a special Next.js file that exports a React component containing the UI for the route.
- In your application, you already have a page file: `/app/page.tsx` - this is the `home page` which is associated with the route `/`.

- ✅ To create a nested route, you can nest folders inside each other with their own `page.tsx` files. For example:
  + `/app/login/page.tsx` is associated with the `/login` path. Let's create the page to see how it works!

## 🚩 CREATING THE DASHBOARD PAGE

- Create a new folder called `dashboard` inside `/app.`
- Then, create a new `page.tsx` file inside the dashboard folder with the following content:

```typescript
export default function Page() {
  return <p>Dashboard Page</p>;
}
```

- Now, make sure that the development server is running and visit `http://localhost:3000/dashboard`.

- This is how you can create different pages in Next.js 👉 `create a new route segment using a folder, and add a page file inside it.`

- By having a special name for `page` files, Next.js allows you to [colocate](https://nextjs.org/docs/app/building-your-application/routing#colocation) UI components, test files, and other related code with your routes.

- Only the content inside the `page` file will be publicly accessible.

## 📂 In your dashboard, create two more pages named `customers` and `invoices`

- The customers page should be accessible on `http://localhost:3000/dashboard/customers`.

- The invoices page should be accessible on `http://localhost:3000/dashboard/invoices`.

## 🚩 CREATING THE DASHBOARD LAYOUT

- Dashboards also have some sort of navigation that is shared across multiple pages.
- In `Next.js`, you can use a special `layout.tsx` file to create UI that is shared between multiple pages.
- Let's create a layout for the dashboard!

- Inside the `/dashboard` folder, add a new file called `layout.tsx` and paste the following code:

```typescript
import SideNav from '@/app/ui/dashboard/sidenav';
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
      <div className="w-full flex-none md:w-64">
        <SideNav />
      </div>
      <div className="flex-grow p-6 md:overflow-y-auto md:p-12">{children}</div>
    </div>
  );
}
```

### ⁉️ A few things are going on in this code, so let's break it down:

- First, you're importing the `<SideNav/>` component into your layout from `app/ui/dashboard/sidenav`.
- Any components you import into this file will be part of the layout.
- The `Layout` component receives a `children` prop.
- The child can either be a page or another layout.
- In your case, the pages inside `/dashboard` will automatically be nested inside a `Layout`.

- You can check everything is working correctly by accessing the pages you've created here 👉 http://localhost:3000/dashboard:

✅ One benefit of using layout is that on navigation, only the page components update while the layout won't re-render.
✅ In Next.js, this is called [partial rendering](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#3-partial-rendering):

## 🚩 ROOT LAYOUT

- `/app/layout.tsx.` layout is required and is called a [root layout](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#root-layout-required).
- Any UI you add to the root layout will be shared across all pages in your application.
- You can use the root layout to modify your `<html>` and `<body>` tags, and add metadata.
- Since the new layout you've just created `(/app/dashboard/layout.tsx)` is unique to the dashboard pages, you don't need to add any UI to the root layout above.

## 🚩 NAVIGATING BETWEEN PAGES

### 🔍 The `<Link>` component

- In Next.js, you can use the `Link` Component to link between pages in your application.
- `<Link>` allows you to do `client-side navigation` with JavaScript.
- Although parts of your application are rendered on the server, navigation is faster and there's `NO FULL PAGE REFRESH` - making it feel more like a web app.

<hr>

### ❇️ Here's how to use the `<Link>` Component:

- 👉 Open `/app/ui/dashboard/nav-links.tsx`, and import the `Link` component from `next/link`:

```typescript
import Link from 'next/link';
```

- 👉 Find the `<a>` tag and replace it with `<Link>`:

✅ Save and check how to navigate between the pages `without seeing a full refresh`.

## 🚩 PATTERN: SHOWING ACTIVE LINKS

- A common UI pattern is to show an active link to indicate to the user what page they are currently on.
- To do this, you need to get the user's current path from the URL.
- Next.js provides a hook called [usePathname()](https://nextjs.org/docs/app/api-reference/functions/use-pathname) that you can use to check the path.

- Since usePathname() is a hook, you'll need to turn `nav-links.tsx` into a Client Component.
- Add React's `"use client"` directive to the top of the file, then import `usePathname()` from `next/navigation`:

```typescript
import { usePathname } from 'next/navigation';
```

- Next, assign the path to a variable called `pathname` inside your component:

```typescript
'use client';
//...
import { usePathname } from 'next/navigation';
// ...
export default function NavLinks() {
  const pathname = usePathname();
  // ...
}
```

- You can use the clsx library to conditionally apply class names when the link is active.
- When `link.href` matches the pathname, the link should displayed with blue text and a light blue background.

- Here's the final code for `nav-links.tsx`:

```typescript
'use client';

import {
  UserGroupIcon,
  HomeIcon,
  DocumentDuplicateIcon,
} from '@heroicons/react/24/outline';

import Link from 'next/link';
import { usePathname } from 'next/navigation';
import clsx from 'clsx';

// Map of links to display in the side navigation.
// Depending on the size of the application, this would be stored in a database.
const links = [
  { name: 'Home', href: '/dashboard', icon: HomeIcon },
  {
    name: 'Invoices',
    href: '/dashboard/invoices',
    icon: DocumentDuplicateIcon,
  },
  { name: 'Customers', href: '/dashboard/customers', icon: UserGroupIcon },
];

export default function NavLinks() {
  const pathname = usePathname();

  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className={clsx(
              'flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3',
              {
                'bg-sky-100 text-blue-600': pathname === link.href,
              },
            )}
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}
```

✅ Save and check your localhost. You should now see the active link highlighted in blue.

### 🔍 Automatic code-splitting and prefetching

- In addition to client-side navigation, `Next.js` automatically code splits your application by route segments. This is different from a traditional [SPA](https://developer.mozilla.org/en-US/docs/Glossary/SPA), where the browser loads all your application code on initial load.

- Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.

- Furthermore, in production, whenever `<Link>` components appear in the browser's viewport, Next.js `AUTOMATİCALLY PREFETCHES THE CODE` for the linked route in the background. By the time the user clicks the link, the code for the destination page will already be loaded in the background, and the page transition will be near-instant!

- Learn more about [how navigation works](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works).

## 🚩 SETTING UP YOUR DATABASE

### ❇️ Create a Postgres database

- To set up a database, on your `VERCEL` account; click Continue to `Dashboard` and select the `Storage` tab from your project dashboard.
- Select `Connect Store` 👉 `Create New` 👉 `Postgres` 👉 `Continue`.
- Accept the terms, assign a name to your database, and ensure your database region is set to Washington D.C (iad1) - this is also the [default region](https://vercel.com/docs/functions/configuring-functions/region#select-a-default-serverless-region) for all new Vercel projects.
- And click `Create&Continue`
- By placing your database in the same region or close to your application code, you can reduce [latency](https://developer.mozilla.org/en-US/docs/Web/Performance/Understanding_latency) for data requests.

<hr>

- Once connected, navigate to the `.env.local` tab, click `Show secret` and `Copy Snippet`.

- 🚩 Navigate to your code editor and rename the `.env.example` file to `.env`. Paste in the copied contents from Vercel.

#### 🛑 `Important:` Go to your `.gitignore` file and make sure `.env` is in the ignored files to prevent your database secrets from being exposed when you push to GitHub.

- Finally, run `npm i @vercel/postgres` in your terminal to install the [Vercel Postgres SDK](https://vercel.com/docs/storage/vercel-postgres/sdk).

### ❇️ SEED YOUR DATABASE

- Now that your database has been created, let's seed it with some initial data. This will allow you to have some data to work with as you build the dashboard.

- In the `/scripts` folder of your project, there's a file called `seed.js`. This script contains the instructions for creating and seeding the invoices, customers, user, revenue tables.

- Don't worry if you don't understand everything the code is doing, but to give you an overview, the script uses SQL to create the tables, and the data from `placeholder-data.js` file to populate them after they've been created.

- Next, in your `package.json` file, add the following line to your scripts:

```json
"scripts": {
  "seed": "node -r dotenv/config ./scripts/seed.js"
},
```

- 👆 This is the command that will execute the `seed.js`.

🖥️ Now, run `npm run seed`. You should see some console.log messages in your terminal to let you know the script is running.

<hr>

### ⁉️ What is 'seeding' in the context of databases?

#### 👉 Populating the database with an initial set of data

<hr>


## 🚩 EXPLORING YOUR DATABASE

- Let's see what your database looks like. Go back to `Vercel`, and click `Data` in the sidenav.

- In this section, you'll find the four new tables: `users, customers, invoices, revenue`.

- By selecting each table, you can view its records and ensure the entries align with the data from `placeholder-data.js` file.

## EXECUTING QUERIES

- You can switch to the `"query"` tab to interact with your database.
- This section supports standard SQL commands.
- For instance, inputting `DROP TABLE customers` will delete "customers" table along with all its data - `so be careful!`

- Let's run your first database query. Paste and run the following SQL code into the Vercel interface:

```sql
SELECT invoices.amount, customers.name
FROM invoices
JOIN customers ON invoices.customer_id = customers.id
WHERE invoices.amount = 666;
```

## 🚩 FETCHING DATA

  Now that you've created and seeded your database, let's discuss the different ways you can fetch data for your application, and choose the most appropriate one for the dashboard overview page.

### 🔍 CHOOSING HOW TO FETCH DATA

#### 1️⃣ API layer

- APIs are an intermediary layer between your application code and database. There are a few cases where you might use an API:

  + If you're using 3rd party services that provide an API.
  + If you're fetching data from the client, you want to have an API layer that runs on the server to avoid exposing your database secrets to the client.

- In Next.js, you can create API endpoints using [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).

#### 2️⃣ Database queries

- When you're creating a full-stack application, you'll also need to write logic to interact with your database.
- For [relational databases](https://aws.amazon.com/tr/relational-database/) like `Postgres`, you can do this with `SQL` or an [ORM](https://vercel.com/docs/storage/vercel-postgres/using-an-orm#) like [Prisma](https://www.prisma.io/).

- There are a few cases where you have to write database queries:

  + When creating your API endpoints, you need to write logic to interact with your database.
  + If you are using React Server Components (fetching data on the server), you can skip the API layer, and query your database directly without risking exposing your database secrets to the client.
  + ‼️ you should not query your database directly when fetching data on the client as this would expose your database secrets.

#### 3️⃣ Using Server Components to fetch data

- By default, Next.js applications use `React Server Components`, and you can opt into `Client Components` when needed.
- There are a few benefits to fetching data with React Server Components:

  + Server components allow you fetch data directly from your database.
  + Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
  + Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use `async/await` syntax without reaching out for `useEffect`, `useState` or data fetching libraries.
  + Since Server Components execute on the server, you can query the database directly without an additional API layer.

<hr>

#### 4️⃣ Using SQL

- For the dashboard project, you'll write database queries using the [Vercel Postgres SDK](https://vercel.com/docs/storage/vercel-postgres/sdk) and SQL.
- There are a few reasons why we'll be using SQL:

  + SQL is the industry standard for querying relational databases (e.g. ORMs generate SQL under the hood).
  + Having a basic understanding of SQL can help you understand the fundamentals of relational databases, allowing you to apply your knowledge to other tools.
  + SQL is versatile, allowing you to fetch and manipulate specific data.
  + SQL allows you to write targeted queries to fetch and manipulate specific data.
  + The Vercel Postgres SDK provides protection against [SQL injections](https://vercel.com/docs/storage/vercel-postgres/sdk#preventing-sql-injections).

<hr>

### 🚩 Go to `/app/lib/data.ts`

- Here you'll see that we're importing the sql function from `@vercel/postgres`.
- This function allows you to query your database:

```typescript
import { sql } from '@vercel/postgres';

// ...
```

- You can call `sql` inside any Server Component.
- But to allow you to navigate the components more easily, we've kept all the data queries in the `data.ts` file, and you can import them into the components.

### 🚩 Fetching data for the dashboard overview page

- Now that you understand different ways of fetching data,
- Let's fetch data for the dashboard overview page.
- Navigate to `/app/dashboard/page.tsx`, paste the following code, and spend some time exploring it:

```typescript
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
 
export default async function Page() {
  return (
    <main>
      <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Dashboard
      </h1>
      <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        {/* <Card title="Collected" value={totalPaidInvoices} type="collected" /> */}
        {/* <Card title="Pending" value={totalPendingInvoices} type="pending" /> */}
        {/* <Card title="Total Invoices" value={numberOfInvoices} type="invoices" /> */}
        {/* <Card
          title="Total Customers"
          value={numberOfCustomers}
          type="customers"
        /> */}
      </div>
      <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        {/* <RevenueChart revenue={revenue}  /> */}
        {/* <LatestInvoices latestInvoices={latestInvoices} /> */}
      </div>
    </main>
  );
}
```

- In the code above:

  + Page is an `async` component. This allows you to use await to fetch data.
  + There are also 3 components which receive data: `<Card>`, `<RevenueChart>`, and `<LatestInvoices>`.
  + They are currently commented out to prevent the application from erroring.

### 🚩 Fetching data for `<RevenueChart/>`

- To fetch data for the `<RevenueChart/>` component, import the `fetchRevenue` function from `data.ts` and call it inside your component:

```typescript
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import { fetchRevenue } from '@/app/lib/data';
 
export default async function Page() {
  const revenue = await fetchRevenue();
  // ...
}
```

- Then, uncomment the `<RevenueChart/>` component and anything inside the `RevenueChart()` function in `@/app/ui/dashboard/revenue-chart';`. Check your localhost, you're now using the revenue data in your component.

### 🚩 Fetching data for `<LatestInvoices/>`

- For the `<LatestInvoices />` component, we need to get the latest 5 invoices, sorted by date.

- You could fetch all the invoices and sort through them using JavaScript. This isn't a problem as our data is small, but as your application grows, it can significantly increase the amount of data transferred on each request and the JavaScript required to sort through it.

- Instead of sorting through the latest invoices in-memory, you can use an SQL query to fetch only the last 5 invoices. For example, this is the SQL query from your `data.ts` file:

```typescript
// Fetch the last 5 invoices, sorted by date
const data = await sql<LatestInvoiceRaw>`
  SELECT invoices.amount, customers.name, customers.image_url, customers.email
  FROM invoices
  JOIN customers ON invoices.customer_id = customers.id
  ORDER BY invoices.date DESC
  LIMIT 5`;
```

- In your page (/app/dashboard/page.tsx), import the `fetchLatestInvoices` function:

```typescript
// ..
import { fetchRevenue, fetchLatestInvoices } from '@/app/lib/data';

export default async function Page() {
  const revenue = await fetchRevenue();
  const latestInvoices = await fetchLatestInvoices();
  // ...
}
```

- Then, uncomment the `<LatestInvoices />` component in (/app/ui/dashboard/latest-invoices.tsx).

If you visit your localhost, you should see that only the last 5 are returned from the database. Hopefully, you're beginning to see the advantages of querying your database directly!


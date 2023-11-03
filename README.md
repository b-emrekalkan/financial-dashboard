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



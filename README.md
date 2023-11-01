# 💱 FINANCIAL DASHBOARD WITH NEXT.JS 💰

## 🚩 Creating the project:

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

## 📂 FOLDER STRUCTURE:

- <b>/app:</b> Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
- <b>/app/lib:</b> Contains functions used in your application, such as reusable utility functions and data fetching functions.
- <b>/app/ui:</b> Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
- <b>/public:</b> Contains all the static assets for your application, such as images.
- <b>/scripts/:</b> Contains a file that you'll use to populate your database in a later chapter.
- <b>Config Files:</b> You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

## 📝 PLACEHOLDER DATA:

When you're building user interfaces, it helps to have some placeholder data. If a database or API is not yet available, you can:

- Use placeholder data in JSON format or as JavaScript objects.
- Use a 3rd party service like [mockAPI](https://mockapi.io/).
For this project, we’ve provided some placeholder data in "app/lib/placeholder-data.js." Each JavaScript object in the file represents a table in your database. For example, for the invoices table:

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

## 🛡️ TYPESCRIPT:

- Take a look at the "/app/lib/definitions.ts" file. 
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

### 🛑 By using TypeScript, you can ensure you don't accidentally pass the wrong data format to your components or database, like passing a string to amount instead of a number.

## 🖥️ Running the development server:

```bash
npm i
npm run dev
```

- "npm run dev" starts your Next.js development server on port 3000.
- Let’s check to see if it’s working. Open http://localhost:3000 on your browser.
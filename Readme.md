# Learn Next.js
### 1. Getting Started
> #### Creating a new project
>> pnpm is recommended as the package manager as it is faster and more efficient than npm or yarn. Install it by running the following in the terminal:
>> 
>>> ```npm install -g pnpm```
>>> 
>> After installing pnpm, change your directory(cd) into the folder where you would like to place your project and run the following in the terminal:
>> 
>>> ```npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm```
> #### Running the development server
>> Run the following in the terminal to install the project's package:
>> 
>>> ```pnpm i```
>>> 
>> Then, run this to start the development server:
>> 
>>> ```pnpm dev```
>>>
>> ```pnpm dev``` starts the development server on port ```3000```. Open http://localhost:3000 to check if it is working.
### 2. CSS Styling
> #### Global styles
>> In the application, ```global.css``` is given and this is the root layout. It can be added by importing the file to ```/app/layout.tsx```:
>> 
>>> ```import '@/app/ui/global.css';```
>>>
>> As you can see in the ```global.css```, no CSS rules are given, yet styles are made. It is because of the ```@tailwind``` directives.
>>
>>> ```@tailwind base;```
>>> ```@tailwind components;```
>>> ```@tailwind utilities;```
>>>
> #### Tailwind
>> Tailwind is a CSS framework that speeds up the development process by allowing you to quickly write utility classes directly in your TSX markup.
> #### CSS modules
>> CSS Modules allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions as well.
### 3. Optimizing Fonts and Images

### 4. Creating Layouts and Pages

### 5. Navigating Between Pages

### 6. Setting Up Your Database
> #### Create a GitHub repository
>> Create a GitHub account and push the project to the repository after making one.
> #### Create a Vercel account
>> Create a Vercel account, choose the free "hobby" plan and select Continue with GitHub to connect two accounts you have made.
> #### Connect and deploy your project
>> Import the GitHub repository to the Vercel account, name it, and deploy it; Framework Preset should be set to Next.js as well.
> #### Create a Postgres database
>> Click Continue to Dashboard on the current screen and select Storage tab. Then, Connect Store -> Create New -> Postgres -> Continue. Your database region should be set to your nearest to improve latency and requests. Once connected, navigate to ```.env.local``` and click Show secret and Copy Snippet. Paste the copied contents into your project under ```.env.example``` file and rename the file to ```.env```. Finally, run ```pnpm i @vercel/postgres```to install the Vercel Postgres SDK.
> #### Seed your database
>> Under ```/app``` directory, there is a folder called ```seed```. Uncomment ```route.ts``` inside the folder that will be used to seed your database. Run the development server with ```pnpm run dev``` and navigate to https://localhost:3000/seed. When finished, you will see a message "Database seeded successfully" in the browser; optionally, you can delete this file after completion.
### 7. Fetching Data
> #### Choosing how to fetch data.
>> ##### API layer
>>> APIs are an intermediary layer between your application code and database. There are a few cases where you might use an API:
>>> + If you're using 3rd party services that provide an API.
>>> + If you're fetching data from the client, you want an API layer that runs on the server to avoid exposing your database secrets to the client.
>> ##### Database queries
>>> When creating a full-stack application, you must write logic to interact with your database. You can do relational databases like Postgres with SQL or ORM.
There are a few cases where you have to write database queries:
>>> + When creating your API endpoints, you must write logic to interact with your database.
>>> + Suppose you are using React Server Components (fetching data on the server). In that case, you can skip the API layer and query your database directly without risking exposing your database secrets to the client.
>> ##### Using server components to fetch data
>>> By default, Next.js applications use React Server Components. Fetching data with Server Components is a relatively new approach and there are a few benefits of using them:
>>> + Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use async/await syntax without reaching out for useEffect, useState or data fetching libraries.
>>> + Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
>>> + As mentioned before, since Server Components execute on the server, you can query the database directly without an additional API layer.
> #### Fetching data for the dashboard overview page
>> Navigate to ```/app/dashboard/page.tsx``` and add the following code.
>>
```tsx import { Card } from '@/app/ui/dashboard/cards';
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
>>
> #### Fetching data for ```<RevenueChart/>```
>> To fetch data for the <RevenueChart/> component, import the fetchRevenue function from data.ts and call it inside your component:
>>
```tsx
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
>> Then, uncomment the ```<RevenueChart/>``` component, navigate to the component file (```/app/ui/dashboard/revenue-chart.tsx```) and uncomment the code inside it. Check https://localhost:3000/dashboard. You should be able to see a chart that uses revenue data.
> #### Fetching data for ```<LatestInvoices/>```
>> You could fetch all the invoices and sort through them using JavaScript. This isn't a problem as our data is small, but as your application grows, it can significantly increase the amount of data transferred on each request and the JavaScript required to sort through it.
Instead of sorting through the latest invoices in-memory, you can use an SQL query to fetch only the last 5 invoices. For example, this is the SQL query from your data.ts file:
>>
```tsx
// Fetch the last 5 invoices, sorted by date
const data = await sql<LatestInvoiceRaw>`
  SELECT invoices.amount, customers.name, customers.image_url, customers.email
  FROM invoices
  JOIN customers ON invoices.customer_id = customers.id
  ORDER BY invoices.date DESC
  LIMIT 5`;
```
>>
>> In the ```/app/dashboard/page.tsx```, import the ```fetchLatestInvoices``` function:
>>
```tsx
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import { fetchRevenue, fetchLatestInvoices } from '@/app/lib/data';
 
export default async function Page() {
  const revenue = await fetchRevenue();
  const latestInvoices = await fetchLatestInvoices();
  // ...
}
```
>>
>>　Then, uncomment the ```<LatestInvoices />``` component. You will also need to uncomment the relevant code in the ```<LatestInvoices />``` component itself, located at ```/app/ui/dashboard/latest-invoices```.
> #### Fetch data for the ```<Card>``` components
>>
```tsx
/*'@/app/dashboard/page.tsx'*/
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import {
  fetchRevenue,
  fetchLatestInvoices,
  fetchCardData,
} from '@/app/lib/data';
 
export default async function Page() {
  const revenue = await fetchRevenue();
  const latestInvoices = await fetchLatestInvoices();
  const {
    numberOfInvoices,
    numberOfCustomers,
    totalPaidInvoices,
    totalPendingInvoices,
  } = await fetchCardData();
 
  return (
    <main>
      <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Dashboard
      </h1>
      <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        <Card title="Collected" value={totalPaidInvoices} type="collected" />
        <Card title="Pending" value={totalPendingInvoices} type="pending" />
        <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
        <Card
          title="Total Customers"
          value={numberOfCustomers}
          type="customers"
        />
      </div>
      <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        <RevenueChart revenue={revenue} />
        <LatestInvoices latestInvoices={latestInvoices} />
      </div>
    </main>
  );
}
```
>>However... there are two things you need to be aware of:
>> + The data requests unintentionally block each other, creating a request waterfall.
>> + By default, Next.js prerenders routes to improve performance, which is called Static Rendering. So, if your data changes, it won't be reflected in your dashboard.
> #### What are request waterfalls?
>> A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests. In the case of data fetching, each request can only begin once the previous request has returned data.
>> For example, we need to wait for fetchRevenue() to execute before fetchLatestInvoices() can start running, and so on.
>>
```tsx
const revenue = await fetchRevenue();
const latestInvoices = await fetchLatestInvoices(); // wait for fetchRevenue() to finish
const {
  numberOfInvoices,
  numberOfCustomers,
  totalPaidInvoices,
  totalPendingInvoices,
} = await fetchCardData(); // wait for fetchLatestInvoices() to finish
```
>> This pattern is not necessarily bad. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the next request. For example, you might want to fetch a user's ID and profile information first. Once you have the ID, you might then proceed to fetch their list of friends. In this case, each request is contingent on the data returned from the previous request.
>> However, this behavior can also be unintentional and impact performance.
> #### Parallel data fetching
>> A common way to avoid waterfalls is to initiate all data requests at the same time - in parallel.
>> In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData() function:
>>
```ts
export async function fetchCardData() {
  try {
    const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;
    const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;
    const invoiceStatusPromise = sql`SELECT
         SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",
         SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"
         FROM invoices`;
 
    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);
    // ...
  }
}
```
>>By using this pattern, you can:
>> + Start executing all data fetches at the same time, which can lead to performance gains.
>> + Use a native JavaScript pattern that can be applied to any library or framework.
>> However, there is one disadvantage of relying only on this JavaScript pattern: what happens if one data request is slower than all the others?

### 8. Static and Dynamic Rendering
> #### What is Static Rendering?
>> With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or when revalidating data.
>> Whenever a user visits your application, the cached result is served. There are a couple of benefits of static rendering:
>> + Faster Websites - Prerendered content can be cached and globally distributed. This ensures that users around the world can access your website's content more quickly and reliably.
>> + Reduced Server Load - Because the content is cached, your server does not have to dynamically generate content for each user request.
>> + SEO - Prerendered content is easier for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.
>> Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data which is regularly updated.
>> The opposite of static rendering is dynamic rendering.
> #### What is Dynamic Rendering?
>> With dynamic rendering, content is rendered on the server for each user at request time (when the user visits the page). There are a couple of benefits of dynamic rendering:
>> + Real-Time Data - Dynamic rendering allows your application to display real-time or frequently updated data. This is ideal for applications where data changes often.
>> + User-Specific Content - It's easier to serve personalized content, such as dashboards or user profiles, and update the data based on user interaction.
>> + Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or the URL search parameters.
> #### Simulating a Slow Data Fetch
>> The dashboard application we're building is dynamic.
>> However, one problem is still mentioned in the previous chapter. What happens if one data request is slower than all the others?
>> Let's simulate a slow data fetch. In your data.ts file, uncomment the console.log and setTimeout inside fetchRevenue():
>>>
```ts
export async function fetchRevenue() {
  try {
    // We artificially delay a response for demo purposes.
    // Don't do this in production :)
    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 3000));
 
    const data = await sql<Revenue>`SELECT * FROM revenue`;
 
    console.log('Data fetch completed after 3 seconds.');
 
    return data.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }
}
```
### 9. Streaming
> #### What is streaming?
>> Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.
> #### Streaming a whole page with ```loading.tsx```
>> Create a new file ```/app/dashboard/loading.tsx```
>>
```tsx
export default function Loading() {
  return <div>Loading...</div>;
}
```
>> A few things are happening here:
>> + loading.tsx is a special Next.js file built on top of Suspense, it allows you to create fallback UI to show as a replacement while page content loads.
>> + Since <SideNav> is static, it's shown immediately. The user can interact with <SideNav> while the dynamic content is loading.
>> + The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).
> #### Adding loading skeletons
>> A loading skeleton is a simplified version of the UI. Many websites use them as a placeholder (or fallback) to indicate to users that the content is loading. Any UI you add in loading.tsx will be embedded as part of the static file and sent first. Then, the rest of the dynamic content will be streamed from the server to the client.
>> Inside your loading.tsx file, import a new component called ```<DashboardSkeleton>```:
>>
```tsx
import DashboardSkeleton from '@/app/ui/skeletons';
 
export default function Loading() {
  return <DashboardSkeleton />;
}
```
> #### Fixing the loading skeleton bug with route groups
>> Right now, your loading skeleton will apply to the invoices and customers pages as well.
>> Since loading.tsx is a level higher than /invoices/page.tsx and /customers/page.tsx in the file system, it's also applied to those pages.
>> We can change this with Route Groups. Create a new folder called /(overview) inside the dashboard folder. Then, move your loading.tsx and page.tsx files inside the folder:
>> + ```'/dashboard/(overview)/loading.tsx```
>> + ```'/dashboard/(overview)/page.tsx```
>> Now, the ```loading.tsx``` file will only apply to your dashboard overview page.
>> Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses ```()```, the name won't be included in the URL path. So ```/dashboard/(overview)/page.tsx``` becomes ```/dashboard```.
>> Here, you're using a route group to ensure ```loading.tsx``` only applies to your dashboard overview page. However, you can also use route groups to separate your application into sections (e.g. ```(marketing)``` routes and ```(shop)``` routes) or by teams for larger applications.
> #### Streaming a component
>> So far, you're streaming a whole page. However, you can also be more granular and stream specific components using React Suspense.
>> Suspense allows you to defer rendering parts of your application until some condition is met (e.g. data is loaded). You can wrap your dynamic components in Suspense. Then, pass it a fallback component to show while the dynamic component loads.
>> If you remember the slow data request, ```fetchRevenue()``` is the request slowing down the whole page. Instead of blocking your whole page, you can use Suspense to stream only this component and immediately show the rest of the page's UI.
>> To do so, you'll need to move the data fetch to the component. Let's update the code to see what that'll look like:
>> Delete all instances of ```fetchRevenue()``` and its data from ```/dashboard/(overview)/page.tsx```:
>>
```
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import { fetchLatestInvoices, fetchCardData } from '@/app/lib/data'; // remove fetchRevenue
 
export default async function Page() {
  const revenue = await fetchRevenue() // delete this line
  const latestInvoices = await fetchLatestInvoices();
  const {
    numberOfInvoices,
    numberOfCustomers,
    totalPaidInvoices,
    totalPendingInvoices,
  } = await fetchCardData();
 
  return (
    // ...
  );
}
```
>> 
### 10. Partial Prerendering

### 11. Adding Search and Pagination

### 12. Mutating Data

### 13. Handling Errors

### 14. Improving Accessibility

### 15. Adding Authentication

### 16. Adding Metadata

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
>> Then, import ```<Suspense>``` from React, and wrap it around ```<RevenueChart />```. You can pass it a fallback component called ```<RevenueChartSkeleton>```.
>>
```tsx
/*/app/dashboard/(overview)/page.tsx*/
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import { fetchLatestInvoices, fetchCardData } from '@/app/lib/data';
import { Suspense } from 'react';
import { RevenueChartSkeleton } from '@/app/ui/skeletons';
 
export default async function Page() {
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
        <Suspense fallback={<RevenueChartSkeleton />}>
          <RevenueChart />
        </Suspense>
        <LatestInvoices latestInvoices={latestInvoices} />
      </div>
    </main>
  );
}
>>
>> Finally, update the ```<RevenueChart>``` component to fetch its own data and remove the prop passed to it:
>>
```tsx
import { generateYAxis } from '@/app/lib/utils';
import { CalendarIcon } from '@heroicons/react/24/outline';
import { lusitana } from '@/app/ui/fonts';
import { fetchRevenue } from '@/app/lib/data';
 
// ...
 
export default async function RevenueChart() { // Make component async, remove the props
  const revenue = await fetchRevenue(); // Fetch data inside the component
 
  const chartHeight = 350;
  const { yAxisLabels, topLabel } = generateYAxis(revenue);
 
  if (!revenue || revenue.length === 0) {
    return <p className="mt-4 text-gray-400">No data available.</p>;
  }
 
  return (
    // ...
  );
}
```
>>
> #### Streaming ```<LatestInvoices>```
>>
```tsx
/*'/app/dashboard/(overview)/page.tsx'*/
import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
import { fetchCardData } from '@/app/lib/data'; // Remove fetchLatestInvoices
import { Suspense } from 'react';
import {
  RevenueChartSkeleton,
  LatestInvoicesSkeleton,
} from '@/app/ui/skeletons';
 
export default async function Page() {
  // Remove `const latestInvoices = await fetchLatestInvoices()`
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
        <Suspense fallback={<RevenueChartSkeleton />}>
          <RevenueChart />
        </Suspense>
        <Suspense fallback={<LatestInvoicesSkeleton />}>
          <LatestInvoices />
        </Suspense>
      </div>
    </main>
  );
}
```
>>
>>
```tsx
/*'/app/ui/dashboard/latest-invoices.tsx'*/
import { ArrowPathIcon } from '@heroicons/react/24/outline';
import clsx from 'clsx';
import Image from 'next/image';
import { lusitana } from '@/app/ui/fonts';
import { fetchLatestInvoices } from '@/app/lib/data';
 
export default async function LatestInvoices() { // Remove props
  const latestInvoices = await fetchLatestInvoices();
 
  return (
    // ...
  );
}
```
>>
> #### Grouping components
>> Now you need to wrap the <Card> components in Suspense. You can fetch data for each individual card, but this could lead to a popping effect as the cards load in, this can be visually jarring for the user.
>> To create more of a staggered effect, you can group the cards using a wrapper component. This means the static <SideNav/> will be shown first, followed by the cards, etc.
>> In your page.tsx file:
>> 1. Delete your <Card> components.
>> 2. Delete the fetchCardData() function.
>> 3. Import a new wrapper component called <CardWrapper />.
>> 4. Import a new skeleton component called <CardsSkeleton />.
>> 5. Wrap ```<CardWrapper />``` in Suspense.
>>
```tsx
/*'/app/dashboard/page.tsx'*/
import CardWrapper from '@/app/ui/dashboard/cards';
// ...
import {
  RevenueChartSkeleton,
  LatestInvoicesSkeleton,
  CardsSkeleton,
} from '@/app/ui/skeletons';
 
export default async function Page() {
  return (
    <main>
      <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Dashboard
      </h1>
      <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        <Suspense fallback={<CardsSkeleton />}>
          <CardWrapper />
        </Suspense>
      </div>
      // ...
    </main>
  );
}
```
>>
>>
```
/*'/app/ui/dashboard/cards.tsx'*/
// ...
import { fetchCardData } from '@/app/lib/data';
 
// ...
 
export default async function CardWrapper() {
  const {
    numberOfInvoices,
    numberOfCustomers,
    totalPaidInvoices,
    totalPendingInvoices,
  } = await fetchCardData();
 
  return (
    <>
      <Card title="Collected" value={totalPaidInvoices} type="collected" />
      <Card title="Pending" value={totalPendingInvoices} type="pending" />
      <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
      <Card
        title="Total Customers"
        value={numberOfCustomers}
        type="customers"
      />
    </>
  );
}
```
>>
### 10. Partial Prerendering
> #### Static vs. Dynamic Routes
>> For most web apps built today, you either choose between static and dynamic rendering for your entire application, or for a specific route. And in Next.js, if you call a dynamic function in a route (like querying your database), the entire route becomes dynamic.
>> However, most routes are not fully static or dynamic. For example, consider an ecommerce site. You might want to statically render the majority of the product information page, but you may want to fetch the user's cart and recommended products dynamically, this allows you show personalized content to your users.
> #### What is Partial Prerendering
>> A new rendering model that allows you to combine the benefits of static and dynamic rendering in the same route.
>> When a user visits a route:
>> + A static route shell that includes the navbar and product information is served, ensuring a fast initial load.
>> + The shell leaves holes where dynamic content like the cart and recommended products will load in asynchronously.
>> + The async holes are streamed in parallel, reducing the overall load time of the page.
> #### How does Partial Prerendering work?
>> Partial Prerendering uses React's Suspense (which you learned about in the previous chapter) to defer rendering parts of your application until some condition is met (e.g. data is loaded).
>> The Suspense fallback is embedded into the initial HTML file along with the static content. At build time (or during revalidation), the static content is prerendered to create a static shell. The rendering of dynamic content is postponed until the user requests the route.
>> Wrapping a component in Suspense doesn't make the component itself dynamic, but rather Suspense is used as a boundary between your static and dynamic code.
> #### Implementing Partial Prerendering
>> Enable PPR for your Next.js app by adding the ppr option to your ```next.config.mjs``` file:
>>
```mjs
/*next.config.mjs*/
/** @type {import('next').NextConfig} */
 
const nextConfig = {
  experimental: {
    ppr: 'incremental',
  },
};
 
export default nextConfig;
```
>>
>> The 'incremental' value allows you to adopt PPR for specific routes.
>> Next, add the experimental_ppr segment config option to your dashboard layout:
>>
```tsx
/*/app/dashboard/layout.tsx*/
import SideNav from '@/app/ui/dashboard/sidenav';
 
export const experimental_ppr = true;
 
// ...
```
>>
### 11. Adding Search and Pagination
> #### Starting code
>>
```tsx
/*/app/dashboard/invoices/page.tsx*/
import Pagination from '@/app/ui/invoices/pagination';
import Search from '@/app/ui/search';
import Table from '@/app/ui/invoices/table';
import { CreateInvoice } from '@/app/ui/invoices/buttons';
import { lusitana } from '@/app/ui/fonts';
import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
import { Suspense } from 'react';
 
export default async function Page() {
  return (
    <div className="w-full">
      <div className="flex w-full items-center justify-between">
        <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
      </div>
      <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
        <Search placeholder="Search invoices..." />
        <CreateInvoice />
      </div>
      {/*  <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
        <Table query={query} currentPage={currentPage} />
      </Suspense> */}
      <div className="mt-5 flex w-full justify-center">
        {/* <Pagination totalPages={totalPages} /> */}
      </div>
    </div>
  );
}
```
>>
>> 1. ```<Search/>``` allows users to search for specific invoices.
>> 2. ```<Pagination/>``` allows users to navigate between pages of invoices.
>> 3. ```<Table/>``` displays the invoices.
>>
> #### Why use URL search params?
>> There are a couple of benefits of implementing search with URL params:
>> + Bookmarkable and Shareable URLs: Since the search parameters are in the URL, users can bookmark the current state of the application, including their search queries and filters, for future reference or sharing.
>> + Server-Side Rendering and Initial Load: URL parameters can be directly consumed on the server to render the initial state, making it easier to handle server rendering.
>> + Analytics and Tracking: Having search queries and filters directly in the URL makes it easier to track user behaviour without requiring additional client-side logic.
>>
> #### Adding the search functionality
>> These are the Next.js client hooks that you'll use to implement the search functionality:
>> + ```useSearchParams```- Allows you to access the parameters of the current URL. For example, the search params for this URL ```/dashboard/invoices?page=1&query=pending``` would look like this: {```page: '1', query: 'pending'}```.
>> + ```usePathname``` - Lets you read the current URL's pathname. For example, for the route ```/dashboard/invoices```, ```usePathname``` would return ```'/dashboard/invoices'```.
>> + ```useRouter``` - Enables programmatically navigation between routes within client components. There are multiple methods you can use.
>> ##### Implementation steps:
>>> ##### 1. Capture the user's input
>>>> Create a new handleSearch function, and add an onChange listener to the <input> element. onChange will invoke handleSearch whenever the input value changes.
>>>>
```tsx
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
 
export default function Search({ placeholder }: { placeholder: string }) {
  function handleSearch(term: string) {
    console.log(term);
  }
 
  return (
    <div className="relative flex flex-1 flex-shrink-0">
      <label htmlFor="search" className="sr-only">
        Search
      </label>
      <input
        className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
        placeholder={placeholder}
        onChange={(e) => {
          handleSearch(e.target.value);
        }}
      />
      <MagnifyingGlassIcon className="absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
    </div>
  );
}
```
>>>> 
>>> ##### 2. Update the URL with the search params.
>>>> Import the ```useSearchParams``` hook from ```'next/navigation'```, and assign it to a variable:
>>>>
```
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
 
  function handleSearch(term: string) {
    console.log(term);
  }
  // ...
}
```
>>>>
>>>> Inside ```handleSearch```, create a new ```URLSearchParams``` instance using your new ```searchParams``` variable.
>>>>
```
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
  }
  // ...
}
```
>>>>
>>>> ```URLSearchParams``` is a Web API that provides utility methods for manipulating the URL query parameters. Instead of creating a complex string literal, you can use it to get the params string like ```?page=1&query=a```.
>>>> Next, ```set``` the params string based on the user’s input. If the input is empty, you want to ```delete``` it:
>>>>
```
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
  }
  // ...
}
```
>>>>
>>>> You can use Next.js's ```useRouter``` and ```usePathname``` hooks to update the URL.
>>>>Import ```useRouter``` and ```usePathname``` from ```'next/navigation'```, and use the ```replace``` method from ```useRouter()``` inside ```handleSearch```:
>>>>
```
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams, usePathname, useRouter } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }
}
```
>>>>
>>>> Here's a breakdown of what's happening:
>>>> + ```${pathname}``` is the current path, in your case, ```"/dashboard/invoices"```.
>>>> + As the user types into the search bar, ```params.toString()``` translates this input into a URL-friendly format.
>>>> + ```replace(${pathname}?${params.toString()})``` updates the URL with the user's search data. For example, ```/dashboard/invoices?query=lee``` if the user searches for "Lee."
>>>> + The URL is updated without reloading the page, thanks to Next.js's client-side navigation (which you learned about in the chapter on navigating between pages.
>>> ##### 3. Keeping the URL and input in sync
>>>> To ensure the input field is in sync with the URL and will be populated when sharing, you can pass a ```defaultValue``` to input by reading from ```searchParams```:
>>>>
```
/*/app/ui/search.tsx*/
<input
  className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
  placeholder={placeholder}
  onChange={(e) => {
    handleSearch(e.target.value);
  }}
  defaultValue={searchParams.get('query')?.toString()}
/>
```
>>>>
>>> ##### 4. Updating the table
>>>> Page components accept a prop called ```searchParams```, so you can pass the current URL params to the ```<Table>``` component.
>>>>
```
/*/app/dashboard/invoices/page.tsx*/
import Pagination from '@/app/ui/invoices/pagination';
import Search from '@/app/ui/search';
import Table from '@/app/ui/invoices/table';
import { CreateInvoice } from '@/app/ui/invoices/buttons';
import { lusitana } from '@/app/ui/fonts';
import { Suspense } from 'react';
import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
 
export default async function Page({
  searchParams,
}: {
  searchParams?: {
    query?: string;
    page?: string;
  };
}) {
  const query = searchParams?.query || '';
  const currentPage = Number(searchParams?.page) || 1;
 
  return (
    <div className="w-full">
      <div className="flex w-full items-center justify-between">
        <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
      </div>
      <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
        <Search placeholder="Search invoices..." />
        <CreateInvoice />
      </div>
      <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
        <Table query={query} currentPage={currentPage} />
      </Suspense>
      <div className="mt-5 flex w-full justify-center">
        {/* <Pagination totalPages={totalPages} /> */}
      </div>
    </div>
  );
}
```
>>>>
>>>> If you navigate to the ```<Table```> Component, you'll see that the two props, ```query``` and ```currentPage```, are passed to the ```fetchFilteredInvoices()``` function which returns the invoices that match the query.
>>>>
```
/*/app/ui/invoices/table.tsx*/
// ...
export default async function InvoicesTable({
  query,
  currentPage,
}: {
  query: string;
  currentPage: number;
}) {
  const invoices = await fetchFilteredInvoices(query, currentPage);
  // ...
}
```
>>>>
> #### Debouncing
>> Inside your ```handleSearch``` function, add the following ```console.log```:
>>
```
/*/app/ui/search.tsx*/
function handleSearch(term: string) {
  console.log(`Searching... ${term}`);
 
  const params = new URLSearchParams(searchParams);
  if (term) {
    params.set('query', term);
  } else {
    params.delete('query');
  }
  replace(`${pathname}?${params.toString()}`);
}
```
>> The URL is updated on every keystroke. This isn't a problem as our application is small, but imagine if your application had thousands of users, each sending a new request to your database on each keystroke.
>> 
>> Debouncing is a programming practice that limits the rate at which a function can fire. In our case, you only want to query the database when the user has stopped typing.
>> 
>> You can implement debouncing in a few ways, including manually creating your own debounce function.
>> 
>> Install ```use-debounce```:
>> ```pnpm i use-debounce```
>> 
>> In your ```<Search>``` Component, import a function called ```useDebouncedCallback```:
>>
```
/*/app/ui/search.tsx*/
// ...
import { useDebouncedCallback } from 'use-debounce';
 
// Inside the Search Component...
const handleSearch = useDebouncedCallback((term) => {
  console.log(`Searching... ${term}`);
 
  const params = new URLSearchParams(searchParams);
  if (term) {
    params.set('query', term);
  } else {
    params.delete('query');
  }
  replace(`${pathname}?${params.toString()}`);
}, 300);
```
>>
>> This function will wrap the contents of ```handleSearch``` and only run the code after a specific time once the user has stopped typing (300ms).
> #### Adding pagination
>> After introducing the search feature, you'll notice the table displays only 6 invoices at a time. This is because the ```fetchFilteredInvoices()``` function in ```data.ts``` returns a maximum of 6 invoices per page.
>> 
>> Adding pagination allows users to navigate through the different pages to view all the invoices. Let's see how you can implement pagination using URL params, just like you did with search.
>> 
>> Navigate to the ```<Pagination/>``` component and you'll notice that it's a Client Component. You don't want to fetch data on the client as this would expose your database secrets (remember, you're not using an API layer). Instead, you can fetch the data on the server, and pass it to the component as a prop.
>> 
>> In ```/dashboard/invoices/page.tsx```, import a new function called ```fetchInvoicesPages``` and pass the ```query``` from ```searchParams``` as an argument:
>>
```
/*/app/dashboard/invoices/page.tsx*/
// ...
import { fetchInvoicesPages } from '@/app/lib/data';
 
export default async function Page({
  searchParams,
}: {
  searchParams?: {
    query?: string,
    page?: string,
  },
}) {
  const query = searchParams?.query || '';
  const currentPage = Number(searchParams?.page) || 1;
 
  const totalPages = await fetchInvoicesPages(query);
 
  return (
    // ...
  );
}
```
>>
>> ```fetchInvoicesPages``` returns the total number of pages based on the search query. For example, if there are 12 invoices that match the search query, and each page displays 6 invoices, then the total number of pages would be 2.
>>
>> Next, pass the ```totalPages``` prop to the ```<Pagination/>``` component:
>>
```
/*/app/dashboard/invoices/page.tsx*/
// ...
 
export default async function Page({
  searchParams,
}: {
  searchParams?: {
    query?: string;
    page?: string;
  };
}) {
  const query = searchParams?.query || '';
  const currentPage = Number(searchParams?.page) || 1;
 
  const totalPages = await fetchInvoicesPages(query);
 
  return (
    <div className="w-full">
      <div className="flex w-full items-center justify-between">
        <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
      </div>
      <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
        <Search placeholder="Search invoices..." />
        <CreateInvoice />
      </div>
      <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
        <Table query={query} currentPage={currentPage} />
      </Suspense>
      <div className="mt-5 flex w-full justify-center">
        <Pagination totalPages={totalPages} />
      </div>
    </div>
  );
}
```
>>
>> Navigate to the ```<Pagination/>``` component and import the ```usePathname``` and ```useSearchParams``` hooks. We will use this to get the current page and set the new page. Make sure to also uncomment the code in this component. Your application will break temporarily as you haven't implemented the ```<Pagination/>``` logic yet. Let's do that now!
>>
```
/*/app/ui/invoices/pagination.tsx*/
'use client';
 
import { ArrowLeftIcon, ArrowRightIcon } from '@heroicons/react/24/outline';
import clsx from 'clsx';
import Link from 'next/link';
import { generatePagination } from '@/app/lib/utils';
import { usePathname, useSearchParams } from 'next/navigation';
 
export default function Pagination({ totalPages }: { totalPages: number }) {
  const pathname = usePathname();
  const searchParams = useSearchParams();
  const currentPage = Number(searchParams.get('page')) || 1;
 
  // ...
}
```
>>
>> Next, create a new function inside the ```<Pagination>``` Component called ```createPageURL```. Similarly to the search, you'll use ```URLSearchParams``` to set the new page number, and pathName to create the URL string.
>>
```
/*/app/ui/invoices/pagination.tsx*/
'use client';
 
import { ArrowLeftIcon, ArrowRightIcon } from '@heroicons/react/24/outline';
import clsx from 'clsx';
import Link from 'next/link';
import { generatePagination } from '@/app/lib/utils';
import { usePathname, useSearchParams } from 'next/navigation';
 
export default function Pagination({ totalPages }: { totalPages: number }) {
  const pathname = usePathname();
  const searchParams = useSearchParams();
  const currentPage = Number(searchParams.get('page')) || 1;
 
  const createPageURL = (pageNumber: number | string) => {
    const params = new URLSearchParams(searchParams);
    params.set('page', pageNumber.toString());
    return `${pathname}?${params.toString()}`;
  };
 
  // ...
}
```
>>
>> Here's a breakdown of what's happening:
>>
>> + ```createPageURL``` creates an instance of the current search parameters.
>> + Then, it updates the "page" parameter to the provided page number.
>> + Finally, it constructs the full URL using the pathname and updated search parameters.
>>
>> Finally, when the user types a new search query, you want to reset the page number to 1. You can do this by updating the ```handleSearch``` function in your ```<Search>``` component:
>>
```
/*/app/ui/search.tsx*/
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { usePathname, useRouter, useSearchParams } from 'next/navigation';
import { useDebouncedCallback } from 'use-debounce';
 
export default function Search({ placeholder }: { placeholder: string }) {
  const searchParams = useSearchParams();
  const { replace } = useRouter();
  const pathname = usePathname();
 
  const handleSearch = useDebouncedCallback((term) => {
    const params = new URLSearchParams(searchParams);
    params.set('page', '1');
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }, 300);
 
```
>>
### 12. Mutating Data
> #### What are Server Actions?
>> React Server Actions allow you to run asynchronous code directly on the server. They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.
> #### Creating an invoice
>> Here are the steps you'll take to create a new invoice:
>> 1. Create a form to capture the user's input.
>> 2. Create a Server Action and invoke it from the form.
>> 3. Inside your Server Action, extract the data from the formData object.
>> 4. Validate and prepare the data to be inserted into your database.
>> 5. Insert the data and handle any errors.
>> 6. Revalidate the cache and redirect the user back to invoices page.
>> ##### 1. Create a new route and form
>>>
```
/*/dashboard/invoices/create/page.tsx*/
import Form from '@/app/ui/invoices/create-form';
import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
import { fetchCustomers } from '@/app/lib/data';
 
export default async function Page() {
  const customers = await fetchCustomers();
 
  return (
    <main>
      <Breadcrumbs
        breadcrumbs={[
          { label: 'Invoices', href: '/dashboard/invoices' },
          {
            label: 'Create Invoice',
            href: '/dashboard/invoices/create',
            active: true,
          },
        ]}
      />
      <Form customers={customers} />
    </main>
  );
}
```
>> ##### 2. Create a server action
>>> In your ```actions.ts``` file, create a new async function that accepts ```formData```:
>>>
```
/*/app/lib/action.ts*/
'use server';
 
export async function createInvoice(formData: FormData) {}
```
>>>
>>> By adding the 'use server,' you mark all the exported functions within the file as Server Actions. These server functions can then be imported and used in Client and Server components.
>>>
>>> Then, in your ```<Form>``` component, import the createInvoice from ```your actions.ts``` file. Add a ```action``` attribute to the ```<form>``` element, and call the createInvoice action.
>>>
```
/app/ui/invoices/create-form.tsx*/
import { customerField } from '@/app/lib/definitions';
import Link from 'next/link';
import {
  CheckIcon,
  ClockIcon,
  CurrencyDollarIcon,
  UserCircleIcon,
} from '@heroicons/react/24/outline';
import { Button } from '@/app/ui/button';
import { createInvoice } from '@/app/lib/actions';
 
export default function Form({
  customers,
}: {
  customers: customerField[];
}) {
  return (
    <form action={createInvoice}>
      // ...
  )
}
```
>>>
>> ##### 3. Extract the data from ```formData```
>>> Back in your ```actions.ts``` file, you'll need to extract the values of ```formData```, there are a couple of methods you can use.
>>>
```
/*/app/lib/actions.ts*/
'use server';
 
export async function createInvoice(formData: FormData) {
  const rawFormData = {
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  };
  // Test it out:
  console.log(rawFormData);
}
```
>>>
>> ##### 4. Validate and prepare the data
>>> ###### Type validation and coercion
>>> It's important to validate that the data from your form aligns with the expected types in your database. For instance, if you add a ```console.log``` inside your action:
>>>
```console.log(typeof rawFormData.amount);```
>>>
>>> You'll notice that amount is of type string and not number. This is because input elements with ```type="number"``` actually return a string
>>>
>>> In your ```actions.ts``` file, import Zod and define a schema that matches the shape of your form object. This schema will validate the ```formData``` before saving it to a database.
>>>
```
/*/app/lib/actions.ts*/
'use server';
 
import { z } from 'zod';
 
const FormSchema = z.object({
  id: z.string(),
  customerId: z.string(),
  amount: z.coerce.number(),
  status: z.enum(['pending', 'paid']),
  date: z.string(),
});
 
const CreateInvoice = FormSchema.omit({ id: true, date: true });
 
export async function createInvoice(formData: FormData) {
  // ...
}
```
>>>
>>> You can then pass your ```rawFormData``` to ```CreateInvoice``` to validate the types:
>>>
```
/*/app/lib/actions.ts*/
// ...
export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
}
```
>>>
>>> ###### Storing values in cents
>>>
```
/*/app/lib/actions.ts*/
// ...
export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
  const amountInCents = amount * 100;
}
```
>>>
>>> ###### Creating new dates
>>>
```
/*/app/lib/actions.ts*/
// ...
export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
  const amountInCents = amount * 100;
  const date = new Date().toISOString().split('T')[0];
}
```
>>>
>> ##### 5. Inserting the data into your database
>> Now that you have all the values you need for your database, you can create an SQL query to insert the new invoice into your database and pass in the variables:
>>
```
/*/app/lib/actions.ts*/
import { z } from 'zod';
import { sql } from '@vercel/postgres';
 
// ...
 
export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
  const amountInCents = amount * 100;
  const date = new Date().toISOString().split('T')[0];
 
  await sql`
    INSERT INTO invoices (customer_id, amount, status, date)
    VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
  `;
}
```
>>
>> ##### 6. Revalidate and redirect
>> Next.js has a Client-side Router Cache that stores the route segments in the user's browser for a time. Along with prefetching, this cache ensures that users can quickly navigate between routes while reducing the number of requests made to the server.
>>
>> Since you're updating the data displayed in the invoices route, you want to clear this cache and trigger a new request to the server. You can do this with the revalidatePath function from Next.js:
>>
```
/*/app/lib/actions.ts*/
'use server';
 
import { z } from 'zod';
import { sql } from '@vercel/postgres';
import { revalidatePath } from 'next/cache';
 
// ...
 
export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
  const amountInCents = amount * 100;
  const date = new Date().toISOString().split('T')[0];
 
  await sql`
    INSERT INTO invoices (customer_id, amount, status, date)
    VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
  `;
 
  revalidatePath('/dashboard/invoices');
}
```
>>
>> At this point, you also want to redirect the user back to the ```/dashboard/invoices``` page. You can do this with the ```redirect``` function from Next.js:
>>
```
/*/app/lib/actions.ts*/
'use server';
 
import { z } from 'zod';
import { sql } from '@vercel/postgres';
import { revalidatePath } from 'next/cache';
import { redirect } from 'next/navigation';
 
// ...
 
export async function createInvoice(formData: FormData) {
  // ...
 
  revalidatePath('/dashboard/invoices');
  redirect('/dashboard/invoices');
}
```
>>
> #### Updating an invoice
>> These are the steps you'll take to update an invoice:
>> ##### 1. Create a new dynamic route segment with the invoice id
>> In your <Table> component, notice there's a <UpdateInvoice /> button that receives the invoice's id from the table records.
>>
```
/*/app/ui/invoices/table.tsx*/
export default async function InvoicesTable({
  query,
  currentPage,
}: {
  query: string;
  currentPage: number;
}) {
  return (
    // ...
    <td className="flex justify-end gap-2 whitespace-nowrap px-6 py-4 text-sm">
      <UpdateInvoice id={invoice.id} />
      <DeleteInvoice id={invoice.id} />
    </td>
    // ...
  );
}
```
>>
>> Navigate to your <UpdateInvoice /> component, and update the href of the Link to accept the id prop. You can use template literals to link to a dynamic route segment:
>>
```
/*/app/ui/invoices/buttons.tsx*/
import { PencilIcon, PlusIcon, TrashIcon } from '@heroicons/react/24/outline';
import Link from 'next/link';
 
// ...
 
export function UpdateInvoice({ id }: { id: string }) {
  return (
    <Link
      href={`/dashboard/invoices/${id}/edit`}
      className="rounded-md border p-2 hover:bg-gray-100"
    >
      <PencilIcon className="w-5" />
    </Link>
  );
}
```
>>
>> ##### 2. Read the invoice id from the page params
>>
```
/*/app/dashboard/invoices/[id]/edit/page.tsx*/
import Form from '@/app/ui/invoices/edit-form';
import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
import { fetchCustomers } from '@/app/lib/data';
 
export default async function Page() {
  return (
    <main>
      <Breadcrumbs
        breadcrumbs={[
          { label: 'Invoices', href: '/dashboard/invoices' },
          {
            label: 'Edit Invoice',
            href: `/dashboard/invoices/${id}/edit`,
            active: true,
          },
        ]}
      />
      <Form invoice={invoice} customers={customers} />
    </main>
  );
}
```
>>
> >Notice how it's similar to your ```/create``` invoice page, except it imports a different form (from the edit-form.tsx file). This form should be pre-populated with a ```defaultValue``` for the customer's name, invoice amount, and status. To pre-populate the form fields, you need to fetch the specific invoice using ```id```.
>>
>> In addition to ```searchParams```, page components also accept a prop called ```params``` which you can use to access the ```id```. Update your ```<Page>``` component to receive the prop:
>>
```
/*/app/dashboard/invoices/[id]/edit/page.tsx*/
import Form from '@/app/ui/invoices/edit-form';
import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
import { fetchCustomers } from '@/app/lib/data';
 
export default async function Page({ params }: { params: { id: string } }) {
  const id = params.id;
  // ...
}
```
>>
>> ##### 3. Fetch the specific invoice from your database
>> + Import a new function called fetchInvoiceById and pass the id as an argument.
>> + Import fetchCustomers to fetch the customer names for the dropdown.
>>
>> You can use ```Promise.all``` to fetch both the invoice and customers in parallel:
>>
```
/*/dahsboard/invoices/[id]/edit/page.tsx*/
import Form from '@/app/ui/invoices/edit-form';
import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
 
export default async function Page({ params }: { params: { id: string } }) {
  const id = params.id;
  const [invoice, customers] = await Promise.all([
    fetchInvoiceById(id),
    fetchCustomers(),
  ]);
  // ...
}
```
>>
>> ##### 4. Pass the ```id``` to the Server Action
>> You can pass ```id``` to the Server Action using JS ```bind```. This will ensure that any values passed to the Server Action are encoded.
>>
```
/*/app/ui/invoices/edit-form.tsx*/
// ...
import { updateInvoice } from '@/app/lib/actions';
 
export default function EditInvoiceForm({
  invoice,
  customers,
}: {
  invoice: InvoiceForm;
  customers: CustomerField[];
}) {
  const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
 
  return (
    <form action={updateInvoiceWithId}>
      <input type="hidden" name="id" value={invoice.id} />
    </form>
  );
}
```
>>
>> Then, in your ```actions.ts``` file, create a new action, ```updateInvoice```:
>>
```
/*/app/lib/actions.ts*/
// Use Zod to update the expected types
const UpdateInvoice = FormSchema.omit({ id: true, date: true });
 
// ...
 
export async function updateInvoice(id: string, formData: FormData) {
  const { customerId, amount, status } = UpdateInvoice.parse({
    customerId: formData.get('customerId'),
    amount: formData.get('amount'),
    status: formData.get('status'),
  });
 
  const amountInCents = amount * 100;
 
  await sql`
    UPDATE invoices
    SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
    WHERE id = ${id}
  `;
 
  revalidatePath('/dashboard/invoices');
  redirect('/dashboard/invoices');
}
```
>>
> #### Deleting an invoice
>> To delete an invoice using a Server Action, wrap the delete button in a ```<form>``` element and pass the ```id``` to the Server Action using ```bind```:
>>
```
/*/app/ui/invoices/buttons.tsx*/
import { deleteInvoice } from '@/app/lib/actions';
 
// ...
 
export function DeleteInvoice({ id }: { id: string }) {
  const deleteInvoiceWithId = deleteInvoice.bind(null, id);
 
  return (
    <form action={deleteInvoiceWithId}>
      <button type="submit" className="rounded-md border p-2 hover:bg-gray-100">
        <span className="sr-only">Delete</span>
        <TrashIcon className="w-4" />
      </button>
    </form>
  );
}
```
>>
>> Inside your ```actions.ts``` file, create a new action called ```deleteInvoice```.
>>
```
export async function deleteInvoice(id: string) {
  await sql`DELETE FROM invoices WHERE id = ${id}`;
  revalidatePath('/dashboard/invoices');
}
```
>>
### 13. Handling Errors

### 14. Improving Accessibility

### 15. Adding Authentication
> #### Creaint the login route
>> Start by creating a new route in your application called /login and paste the following code:
>>
```
/*/app/login/page.tsx*/
import AcmeLogo from '@/app/ui/acme-logo';
import LoginForm from '@/app/ui/login-form';
 
export default function LoginPage() {
  return (
    <main className="flex items-center justify-center md:h-screen">
      <div className="relative mx-auto flex w-full max-w-[400px] flex-col space-y-2.5 p-4 md:-mt-32">
        <div className="flex h-20 w-full items-end rounded-lg bg-blue-500 p-3 md:h-36">
          <div className="w-32 text-white md:w-36">
            <AcmeLogo />
          </div>
        </div>
        <LoginForm />
      </div>
    </main>
  );
}
```
>>
> #### Setting up the NextAuth.js
>> Install NextAuth.js by running the following command in your terminal: ```pnpm i next-auth@beta```
>> 
>> Next, generate a secret key for your application. This key is used to encrypt cookies, ensuring the security of user sessions. You can do this by running the following command in your terminal: ```openssl ran -base64 32```
>>
>> Then,in your ```.env``` file, add your generated key to the AUTH_SECRET variable: ```AUTH_SECRET=your-secret-key```
>>
>> ##### Adding the pages option
>> Create an ```auth.config.ts``` file at the root of our project that exports an ```authConfig``` object. This object will contain the configuration options for ```NextAuth.js```.
>>
```
/*/auth/config.ts*/
import type { NextAuthConfig } from 'next-auth';
 
export const authConfig = {
  pages: {
    signIn: '/login',
  },
} satisfies NextAuthConfig;
```
>>
>> ##### Protecting your routes with Next.js Middleware
>> Next, add the logic to protect your routes. This will prevent users from accessing the dashboard pages unless they are logged in.
>>
```
/*/auth.config.ts*/
import type { NextAuthConfig } from 'next-auth';
 
export const authConfig = {
  pages: {
    signIn: '/login',
  },
  callbacks: {
    authorized({ auth, request: { nextUrl } }) {
      const isLoggedIn = !!auth?.user;
      const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
      if (isOnDashboard) {
        if (isLoggedIn) return true;
        return false; // Redirect unauthenticated users to login page
      } else if (isLoggedIn) {
        return Response.redirect(new URL('/dashboard', nextUrl));
      }
      return true;
    },
  },
  providers: [], // Add providers with an empty array for now
} satisfies NextAuthConfig;
```
>>
>> The ```authorized``` callback is used to verify if the request is authorized to access a page via Next.js Middleware. It is called before a request is completed, and it receives an object with the auth and ```request``` properties. The ```auth``` property contains the user's session, and the ```request``` property contains the incoming request.
>>
>> The ```providers``` option is an array where you list different login options. For now, it's an empty array to satisfy NextAuth config. You'll learn more about it in the Adding the Credentials provider section.
>>
>> Next, you will need to import the ```authConfig``` object into a Middleware file.
>>
```
/*/middleware.ts*/
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';
 
export default NextAuth(authConfig).auth;
 
export const config = {
  // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
  matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
};
```
>>
>> Here you're initializing NextAuth.js with the ```authConfig``` object and exporting the ```auth``` property. You're also using the ```matcher``` option from Middleware to specify that it should run on specific paths.
>>
>> ##### Password having
>> In your seed.js file, you used a package called bcrypt to hash the user's password before storing it in the database. You will use it again later in this chapter to compare that the password entered by the user matches the one in the database. However, you will need to create a separate file for the bcrypt package. This is because bcrypt relies on Node.js APIs not available in Next.js Middleware.
>>
>> Create a new file called ```auth.ts``` that spreads your ```authConfig``` object:
>>
```
/*/auth.ts*/
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';
 
export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
});
```
>>
>> ##### Adding the Credentials provider
>> Next, you will need to add the ```providers``` option for NextAuth.js. providers is an array where you list different login options such as Google or GitHub. For this course, we will focus on using the Credentials provider only.
>>
```
/*/auth.ts*/
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';
import Credentials from 'next-auth/providers/credentials';
 
export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [Credentials({})],
});
```
>>
>> ##### Adding the sign-in functionality
>> You can use the ```authorize``` function to handle the authentication logic. Similarly to Server Actions, you can use ```zod``` to validate the email and password before checking if the user exists in the database:
>>
```ts
/*/auth.ts*/
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';
import Credentials from 'next-auth/providers/credentials';
import { z } from 'zod';
 
export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [
    Credentials({
      async authorize(credentials) {
        const parsedCredentials = z
          .object({ email: z.string().email(), password: z.string().min(6) })
          .safeParse(credentials);
      },
    }),
  ],
});
```
>>
>> After validating the credentials, create a new ```getUser``` function that queries the user from the database. Then, call bcrypt.compare to check if the passwords match:
>>
```ts
/*/auth.ts*/
import NextAuth from 'next-auth';
import Credentials from 'next-auth/providers/credentials';
import { authConfig } from './auth.config';
import { z } from 'zod';
import { sql } from '@vercel/postgres';
import type { User } from '@/app/lib/definitions';
import bcrypt from 'bcrypt';
 
async function getUser(email: string): Promise<User | undefined> {
  try {
    const user = await sql<User>`SELECT * FROM users WHERE email=${email}`;
    return user.rows[0];
  } catch (error) {
    console.error('Failed to fetch user:', error);
    throw new Error('Failed to fetch user.');
  }
}
 
export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [
    Credentials({
      async authorize(credentials) {
        const parsedCredentials = z
          .object({ email: z.string().email(), password: z.string().min(6) })
          .safeParse(credentials);
 
        if (parsedCredentials.success) {
          const { email, password } = parsedCredentials.data;
          const user = await getUser(email);
          if (!user) return null;
          const passwordsMatch = await bcrypt.compare(password, user.password);
 
          if (passwordsMatch) return user;
        }

        console.log('Invalid credentials');
        return null;
      },
    }),
  ],
});
```
>>
>> ##### Updating the login form
>> Now, you need to connect the auth logic with your login form. In your ```actions.ts``` file, create a new action called ```authenticate```. This action should import the ```signIn``` function from ```auth.ts```:
>>
```ts
/*/app/lib/actions.ts*/
'use server';
 
import { signIn } from '@/auth';
import { AuthError } from 'next-auth';
 
// ...
 
export async function authenticate(
  prevState: string | undefined,
  formData: FormData,
) {
  try {
    await signIn('credentials', formData);
  } catch (error) {
    if (error instanceof AuthError) {
      switch (error.type) {
        case 'CredentialsSignin':
          return 'Invalid credentials.';
        default:
          return 'Something went wrong.';
      }
    }
    throw error;
  }
}
```
>>
>> Finally, in your ```login-form.tsx``` component, you can use React's ```useActionState``` to call the server action, handle form errors, and display the form's pending state:
>>
```tsx
/*/app/ui/login-form.tsx*/
'use client';
 
import { lusitana } from '@/app/ui/fonts';
import {
  AtSymbolIcon,
  KeyIcon,
  ExclamationCircleIcon,
} from '@heroicons/react/24/outline';
import { ArrowRightIcon } from '@heroicons/react/20/solid';
import { Button } from '@/app/ui/button';
import { useActionState } from 'react';
import { authenticate } from '@/app/lib/actions';
 
export default function LoginForm() {
  const [errorMessage, formAction, isPending] = useActionState(
    authenticate,
    undefined,
  );
 
  return (
    <form action={formAction} className="space-y-3">
      <div className="flex-1 rounded-lg bg-gray-50 px-6 pb-4 pt-8">
        <h1 className={`${lusitana.className} mb-3 text-2xl`}>
          Please log in to continue.
        </h1>
        <div className="w-full">
          <div>
            <label
              className="mb-3 mt-5 block text-xs font-medium text-gray-900"
              htmlFor="email"
            >
              Email
            </label>
            <div className="relative">
              <input
                className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
                id="email"
                type="email"
                name="email"
                placeholder="Enter your email address"
                required
              />
              <AtSymbolIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
            </div>
          </div>
          <div className="mt-4">
            <label
              className="mb-3 mt-5 block text-xs font-medium text-gray-900"
              htmlFor="password"
            >
              Password
            </label>
            <div className="relative">
              <input
                className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
                id="password"
                type="password"
                name="password"
                placeholder="Enter password"
                required
                minLength={6}
              />
              <KeyIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
            </div>
          </div>
        </div>
        <Button className="mt-4 w-full" aria-disabled={isPending}>
          Log in <ArrowRightIcon className="ml-auto h-5 w-5 text-gray-50" />
        </Button>
        <div
          className="flex h-8 items-end space-x-1"
          aria-live="polite"
          aria-atomic="true"
        >
          {errorMessage && (
            <>
              <ExclamationCircleIcon className="h-5 w-5 text-red-500" />
              <p className="text-sm text-red-500">{errorMessage}</p>
            </>
          )}
        </div>
      </div>
    </form>
  );
}
```
>
> #### Adding the logout functionality
>> To add the logout functionality to ```<SideNav />```, call the ```signOut``` function from ```auth.ts``` in your ```<form>``` element:
>>
```tsx
/*/ui/dashboard/sidenav.tsx*/
import Link from 'next/link';
import NavLinks from '@/app/ui/dashboard/nav-links';
import AcmeLogo from '@/app/ui/acme-logo';
import { PowerIcon } from '@heroicons/react/24/outline';
import { signOut } from '@/auth';
 
export default function SideNav() {
  return (
    <div className="flex h-full flex-col px-3 py-4 md:px-2">
      // ...
      <div className="flex grow flex-row justify-between space-x-2 md:flex-col md:space-x-0 md:space-y-2">
        <NavLinks />
        <div className="hidden h-auto w-full grow rounded-md bg-gray-50 md:block"></div>
        <form
          action={async () => {
            'use server';
            await signOut();
          }}
        >
          <button className="flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3">
            <PowerIcon className="w-6" />
            <div className="hidden md:block">Sign Out</div>
          </button>
        </form>
      </div>
    </div>
  );
}
```
>> 
### 16. Adding Metadata

# Learn Next.js
### 1. Getting Started
#### Creating a new project
> pnpm is recommended as the package manager as it is faster and more efficient than npm or yarn. Install it by running the following in the terminal:
> 
> ```npm install -g pnpm```
> 
> After installing pnpm, change your directory(cd) into the folder where you would like to place your project and run the following in the terminal:
> 
> ```npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm```
 #### Running the development server
> Run the following in the terminal to install the project's package:
> 
> ```pnpm i```
> 
> Then, run this to start the development server:
> 
> ```pnpm dev```
>
> ```pnpm dev``` starts the development server on port ```3000```. Open http://localhost:3000 to check if it is working.
> 
### 2. CSS Styling
#### Global styles
> In the application, ```global.css``` is given and this is the root layout. It can be added by importing the file to ```/app/layout.tsx```:
> 
> ```import '@/app/ui/global.css';```
>
> As you can see in the ```global.css```, no CSS rules are given, yet styles are made. It is because of the ```@tailwind``` directives.
>
> ```@tailwind base;```
> ```@tailwind components;```
> ```@tailwind utilities;```
>
#### Tailwind
> Tailwind is a CSS framework that speeds up the development process by allowing you to write utility classes directly in your TSX markup quickly.
#### CSS modules
> CSS Modules will enable you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions.
> 
### 3. Optimizing Fonts and Images

### 4. Creating Layouts and Pages

### 5. Navigating Between Pages


### 6. Setting Up Your Database
#### Create a GitHub repository
> Create a GitHub account and push the project to the repository after making one.
> 
#### Create a Vercel account
> Create a Vercel account, choose the free "hobby" plan and select Continue with GitHub to connect two accounts you have made.
> 
#### Connect and deploy your project
> Import the GitHub repository to the Vercel account, name it, and deploy it; Framework Preset should be set to Next.js as well.
> 
#### Create a Postgres database
> Click Continue to Dashboard on the current screen and select Storage tab. Then, Connect Store -> Create New -> Postgres -> Continue. Your database region should be set to your nearest to improve latency and requests. Once connected, navigate to ```.env.local``` and click Show secret and Copy Snippet. Paste the copied contents into your project under ```.env.example``` file and rename the file to ```.env```. Finally, run ```pnpm i @vercel/postgres```to install the Vercel Postgres SDK.
> 
#### Seed your database
> Under ```/app``` directory, there is a folder called ```seed```. Uncomment ```route.ts``` inside the folder that will be used to seed your database. Run the development server with ```pnpm run dev``` and navigate to https://localhost:3000/seed. When finished, you will see a message "Database seeded successfully" in the browser; optionally, you can delete this file after completion.


### 7. Fetching Data
#### Choosing how to fetch data.
> ##### API layer
>> APIs are an intermediary layer between your application code and database. Here are a few cases where you might use an API:
>> + If you're using 3rd party services that provide an API.
>> + If you're fetching data from the client, you want an API layer that runs on the server to avoid exposing your database secrets to the client.
>>
> ##### Database queries
>> When creating a full-stack application, you must write logic to interact with your database. You can do relational databases like Postgres with SQL or ORM.
There are a few cases where you have to write database queries:
>> + When creating your API endpoints, you must write logic to interact with your database.
>> + Suppose you are using React Server Components (fetching data on the server). In that case, you can skip the API layer and query your database directly without risking exposing your database secrets to the client.
>>
> ##### Using server components to fetch data
>> By default, Next.js applications use React Server Components. Fetching data with Server Components is a relatively new approach, and there are a few benefits of using them:
>> + Server Components provide a more straightforward solution for asynchronous tasks that you can use async/await syntax without reaching out for useEffect, useState or data fetching libraries.
>> + Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
>> + As mentioned before, since Server Components execute on the server, you can query the database directly without an additional API layer.
>>
#### Fetching data for the dashboard overview page
> Navigate to ```/app/dashboard/page.tsx``` and add the following code.
>
> ```tsx:page.tsx
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
>  
> export default async function Page() {
>   return (
>     <main>
>       <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
>         Dashboard
>       </h1>
>       <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
>         {/* <Card title="Collected" value={totalPaidInvoices} type="collected" /> */}
>         {/* <Card title="Pending" value={totalPendingInvoices} type="pending" /> */}
>         {/* <Card title="Total Invoices" value={numberOfInvoices} type="invoices" /> */}
>         {/* <Card
>           title="Total Customers"
>           value={numberOfCustomers}
>           type="customers"
>         /> */}
>       </div>
>       <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
>         {/* <RevenueChart revenue={revenue}  /> */}
>         {/* <LatestInvoices latestInvoices={latestInvoices} /> */}
>       </div>
>     </main>
>   );
> }
> ```
>
#### Fetching data for ```<RevenueChart/>```
> To fetch data for the <RevenueChart/> component, import the fetchRevenue function from data.ts and call it inside your component:
>
> ```tsx
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchRevenue } from '@/app/lib/data';
>  
> export default async function Page() {
>   const revenue = await fetchRevenue();
>   // ...
> }
> ```
>
> Then, uncomment the ```<RevenueChart/>``` component, navigate to the component file (```/app/ui/dashboard/revenue-chart.tsx```), and uncomment the code inside it. Check https://localhost:3000/dashboard. You should be able to see a chart that uses revenue data.
> 
#### Fetching data for ```<LatestInvoices/>```
> You could fetch and sort all the invoices using JavaScript. This isn't a problem as our data is small, but as your application grows, it can significantly increase the amount of data transferred on each request, and the JavaScript required to sort through it.
> 
> Instead of sorting the latest invoices in-memory, you can use an SQL query to fetch only the last five invoices. For example, this is the SQL query from your data.ts file:
>
> ```tsx
> // Fetch the last 5 invoices, sorted by date
> const data = await sql<LatestInvoiceRaw>`
>   SELECT invoices.amount, customers.name, customers.image_url, customers.email
>   FROM invoices
>   JOIN customers ON invoices.customer_id = customers.id
>   ORDER BY invoices.date DESC
>   LIMIT 5`;
> ```
>
> In the ```/app/dashboard/page.tsx```, import the ```fetchLatestInvoices``` function:
>
> ```tsx:page.tsx
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchRevenue, fetchLatestInvoices } from '@/app/lib/data';
>  
> export default async function Page() {
>   const revenue = await fetchRevenue();
>   const latestInvoices = await fetchLatestInvoices();
>   // ...
> }
> ```
>
> Then, uncomment the ```<LatestInvoices />``` component. You must also uncomment the relevant code in the ```<LatestInvoices />``` component, located at ```/app/ui/dashboard/latest-invoices```.
>
#### Fetch data for the ```<Card>``` components
>
> ```tsx:page.tsx
> /*'@/app/dashboard/page.tsx'*/
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import {
>   fetchRevenue,
>   fetchLatestInvoices,
>   fetchCardData,
> } from '@/app/lib/data';
>  
> export default async function Page() {
>   const revenue = await fetchRevenue();
>   const latestInvoices = await fetchLatestInvoices();
>   const {
>     numberOfInvoices,
>     numberOfCustomers,
>     totalPaidInvoices,
>     totalPendingInvoices,
>   } = await fetchCardData();
>  
>   return (
>     <main>
>       <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
>         Dashboard
>       </h1>
>       <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
>         <Card title="Collected" value={totalPaidInvoices} type="collected" />
>         <Card title="Pending" value={totalPendingInvoices} type="pending" />
>         <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
>         <Card
>           title="Total Customers"
>           value={numberOfCustomers}
>           type="customers"
>         />
>       </div>
>       <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
>         <RevenueChart revenue={revenue} />
>         <LatestInvoices latestInvoices={latestInvoices} />
>       </div>
>     </main>
>   );
> }
> ```
> 
> However, there are two things you need to be aware of:
> + The data requests unintentionally block each other, creating a request waterfall.
> + By default, Next.js prerenders routes to improve performance, called Static Rendering. So, if your data changes, it won't be reflected in your dashboard.
>
#### What are request waterfalls?
> A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests. In the case of data fetching, each request can only begin once the previous request has returned data.
> For example, we need to wait for fetchRevenue() to execute before fetchLatestInvoices() can start running, and so on.
>
> ```tsx
> const revenue = await fetchRevenue();
> const latestInvoices = await fetchLatestInvoices(); // wait for fetchRevenue() to finish
> const {
>   numberOfInvoices,
>   numberOfCustomers,
>   totalPaidInvoices,
>   totalPendingInvoices,
> } = await fetchCardData(); // wait for fetchLatestInvoices() to finish
> ```
> 
> This pattern is not necessarily wrong. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the subsequent request. For example, you should first fetch a user's ID and profile information. Once you have the ID, you might fetch their list of friends. In this case, each request is contingent on the data returned from the previous request.
> 
> However, this behaviour can also be unintentional and impact performance.
> 
#### Parallel data fetching
> A common way to avoid waterfalls is to initiate all data requests simultaneously.
> In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData() function:
>
> ```ts:data.ts
> export async function fetchCardData() {
>   try {
>     const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;
>     const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;
>     const invoiceStatusPromise = sql`SELECT
>          SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",
>          SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"
>          FROM invoices`;
>  
>     const data = await Promise.all([
>       invoiceCountPromise,
>       customerCountPromise,
>       invoiceStatusPromise,
>     ]);
>     // ...
>   }
> }
> ```
> 
> By using this pattern, you can:
> + Start executing all data fetches simultaneously, which can lead to performance gains.
> + Use a native JavaScript pattern that can be applied to any library or framework.
> 
> However, there is one disadvantage of relying only on this JavaScript pattern: what happens if one data request is slower than all the others?

### 8. Static and Dynamic Rendering
#### What is Static Rendering?
> With static rendering, data fetching and rendering happen on the server at build time (when you deploy) or when revalidating data.
> 
> Whenever a user visits your application, the cached result is served. There are a couple of benefits of static rendering:
> + Faster Websites - Prerendered content can be cached and globally distributed. This ensures that users worldwide can access your website's content more quickly and reliably.
> + Reduced Server Load - Because the content is cached, your server does not have to generate content for each user request dynamically.
> + SEO - Prerendered content is more manageable for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.
> 
> Static rendering is helpful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard with personalized data regularly updated.
> 
> The opposite of static rendering is dynamic rendering.
> 
#### What is Dynamic Rendering?
> With dynamic rendering, content is rendered on the server for each user at the request time (when the user visits the page). There are a couple of benefits of dynamic rendering:
> + Real-Time Data - Dynamic rendering allows your application to display real-time or frequently updated data. This is ideal for applications where data changes often.
> + User-Specific Content - It's easier to serve personalized content, such as dashboards or user profiles, and update the data based on user interaction.
> + Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or URL search parameters.
>
#### Simulating a Slow Data Fetch
> The dashboard application we're building is dynamic.
> 
> Let's simulate a slow data fetch. In your data.ts file, uncomment the console.log and setTimeout inside fetchRevenue():
>
> ```ts
> export async function fetchRevenue() {
>   try {
>     // We artificially delay a response for demo purposes.
>     // Don't do this in production :)
>     console.log('Fetching revenue data...');
>     await new Promise((resolve) => setTimeout(resolve, 3000));
>  
>     const data = await sql<Revenue>`SELECT * FROM revenue`;
>  
>     console.log('Data fetch completed after 3 seconds.');
>  
>     return data.rows;
>   } catch (error) {
>     console.error('Database Error:', error);
>     throw new Error('Failed to fetch revenue data.');
>   }
> }
> ```
>
> Now open http://localhost:3000/dashboard/ in a new tab. You will notice, in your terminal, you should see the following messages:
>
> ```
> Fetching revenue data...
> Data fetch completed after 3 seconds.
> ```
>
> With dynamic rendering, your application is as fast as your slowest data fetch.
> 
### 9. Streaming
#### What is streaming?
> Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.
> 
#### Streaming a whole page with ```loading.tsx```
> Create a new file ```/app/dashboard/loading.tsx```
>
> ```tsx
> export default function Loading() {
>   return <div>Loading...</div>;
> }
> ```
> 
> A few things are happening here:
> + loading.tsx is a particular Next.js file built on top of Suspense; it allows you to create a fallback UI to show as a replacement while page content loads.
> + Since <SideNav> is static, it's shown immediately. The user can interact with <SideNav> while the dynamic content is loading.
> + The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).
>
#### Adding loading skeletons
> A loading skeleton is a simplified version of the UI. Many websites use them as a placeholder (or fallback) to indicate to users that the content is loading. Any UI you add in loading.tsx will be embedded as part of the static file and sent first. Then, the rest of the dynamic content will be streamed from the server to the client.
> 
> Inside your loading.tsx file, import a new component called ```<DashboardSkeleton>```:
>
> ```tsx
> import DashboardSkeleton from '@/app/ui/skeletons';
>  
> export default function Loading() {
>   return <DashboardSkeleton />;
> }
> ```
>
#### Fixing the loading skeleton bug with route groups
> Currently, your loading skeleton will also apply to the invoices and customers pages.
> 
> Since loading.tsx is higher than /invoices/page.tsx and /customers/page.tsx in the file system, the skeleton is also applied to those pages.
> 
> We can change this with Route Groups. Create a new folder called /(overview) inside the dashboard folder. Then, move your loading.tsx and page.tsx files inside the folder.
> ![image](https://github.com/user-attachments/assets/4fff3b65-a502-4222-ae29-346101d2a7fc)
> Now, the ```loading.tsx``` file will only apply to your dashboard overview page.
> 
> Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses ```()```, the name won't be included in the URL path. So ```/dashboard/(overview)/page.tsx``` becomes ```/dashboard```.
> 
> Here, you're using a route group to ensure ```loading.tsx``` only applies to your dashboard overview page. However, you can also use route groups to separate your application into sections (e.g. ```(marketing)``` routes and ```(shop)``` routes) or by teams for larger applications.
> 
#### Streaming a component
> So far, you're streaming a whole page. However, you can also be more granular and stream specific components using React Suspense.
> 
> Suspense allows you to defer rendering parts of your application until some condition is met (e.g. data is loaded). You can wrap your dynamic components in Suspense. Then, pass it a fallback component to show while the dynamic component loads.
>
> If you remember the slow data request, ```fetchRevenue()``` is the request slowing down the whole page. Instead of blocking your whole page, you can use Suspense to stream only this component and immediately show the rest of the page's UI.
> 
> To do so, you need to move the data fetch to the component. Let's update the code to see what that'll look like:
> Delete all instances of ```fetchRevenue()``` and its data from ```/dashboard/(overview)/page.tsx```:
>
> ```tsx
> /*/app/dashboard/(overview)/page.tsx*/
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchLatestInvoices, fetchCardData } from '@/app/lib/data'; // remove fetchRevenue
>  
> export default async function Page() {
>   const revenue = await fetchRevenue() // delete this line
>   const latestInvoices = await fetchLatestInvoices();
>   const {
>     numberOfInvoices,
>     numberOfCustomers,
>     totalPaidInvoices,
>     totalPendingInvoices,
>   } = await fetchCardData();
>  
>   return (
>     // ...
>   );
> }
> ```
>
> Then, import ```<Suspense>``` from React, and wrap it around ```<RevenueChart />```. You can pass it a fallback component called ```<RevenueChartSkeleton>```.
>
> ```tsx
> /*/app/dashboard/(overview)/page.tsx*/
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchLatestInvoices, fetchCardData } from '@/app/lib/data';
> import { Suspense } from 'react';
> import { RevenueChartSkeleton } from '@/app/ui/skeletons';
>  
> export default async function Page() {
>   const latestInvoices = await fetchLatestInvoices();
>   const {
>     numberOfInvoices,
>     numberOfCustomers,
>     totalPaidInvoices,
>     totalPendingInvoices,
>   } = await fetchCardData();
>  
>   return (
>     <main>
>       <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
>         Dashboard
>       </h1>
>       <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
>         <Card title="Collected" value={totalPaidInvoices} type="collected" />
>         <Card title="Pending" value={totalPendingInvoices} type="pending" />
>         <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
>         <Card
>           title="Total Customers"
>           value={numberOfCustomers}
>           type="customers"
>         />
>       </div>
>       <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
>         <Suspense fallback={<RevenueChartSkeleton />}>
>           <RevenueChart />
>         </Suspense>
>         <LatestInvoices latestInvoices={latestInvoices} />
>       </div>
>     </main>
>   );
> }
> ```
> 
> Finally, update the ```<RevenueChart>``` component to fetch its data and remove the prop passed to it:
>
> ```tsx
> /*/app/ui/dashboard/revenue-chart.tsx*/
> import { generateYAxis } from '@/app/lib/utils';
> import { CalendarIcon } from '@heroicons/react/24/outline';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchRevenue } from '@/app/lib/data';
>  
> // ...
>  
> export default async function RevenueChart() { // Make component async, remove the props
>   const revenue = await fetchRevenue(); // Fetch data inside the component
>  
>   const chartHeight = 350;
>   const { yAxisLabels, topLabel } = generateYAxis(revenue);
>  
>   if (!revenue || revenue.length === 0) {
>     return <p className="mt-4 text-gray-400">No data available.</p>;
>   }
>  
>   return (
>     // ...
>   );
> }
> ```
>
> You should now see the dashboard information almost immediately, while a fallback skeleton is shown for ```<RevenueChart>```.
> 
#### Streaming ```<LatestInvoices>```
>
> ```tsx
> /*'/app/dashboard/(overview)/page.tsx'*/
> import { Card } from '@/app/ui/dashboard/cards';
> import RevenueChart from '@/app/ui/dashboard/revenue-chart';
> import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchCardData } from '@/app/lib/data'; // Remove fetchLatestInvoices
> import { Suspense } from 'react';
> import {
>   RevenueChartSkeleton,
>   LatestInvoicesSkeleton,
> } from '@/app/ui/skeletons';
>  
> export default async function Page() {
>   // Remove `const latestInvoices = await fetchLatestInvoices()`
>   const {
>     numberOfInvoices,
>     numberOfCustomers,
>     totalPaidInvoices,
>     totalPendingInvoices,
>   } = await fetchCardData();
>  
>   return (
>     <main>
>       <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
>         Dashboard
>       </h1>
>       <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
>         <Card title="Collected" value={totalPaidInvoices} type="collected" />
>         <Card title="Pending" value={totalPendingInvoices} type="pending" />
>         <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
>         <Card
>           title="Total Customers"
>           value={numberOfCustomers}
>           type="customers"
>         />
>       </div>
>       <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
>         <Suspense fallback={<RevenueChartSkeleton />}>
>           <RevenueChart />
>         </Suspense>
>         <Suspense fallback={<LatestInvoicesSkeleton />}>
>           <LatestInvoices />
>         </Suspense>
>       </div>
>     </main>
>   );
> }
> ```
>
> Wrap ```<LatestInvoices />``` by a Suspense component and pass it a fallback component ```<LatestInvoicesSkeleton />```.
>
> ```tsx
> /*'/app/ui/dashboard/latest-invoices.tsx'*/
> import { ArrowPathIcon } from '@heroicons/react/24/outline';
> import clsx from 'clsx';
> import Image from 'next/image';
> import { lusitana } from '@/app/ui/fonts';
> import { fetchLatestInvoices } from '@/app/lib/data';
>  
> export default async function LatestInvoices() { // Remove props
>   const latestInvoices = await fetchLatestInvoices();
>  
>   return (
>     // ...
>   );
> }
> ```
>
#### Grouping components
> Now, you need to wrap the <Card> components in Suspense. You can fetch data for each card, but this could lead to a popping effect as the cards load in. This can be visually jarring for the user.
> 
> To create more of a staggered effect, you can group the cards using a wrapper component. This means the static <SideNav/> will be shown first, followed by the cards, etc.
> 
> In your page.tsx file:
> 1. Delete your <Card> components.
> 2. Delete the fetchCardData() function.
> 3. Import a new wrapper component called <CardWrapper />.
> 4. Import a new skeleton component called <CardsSkeleton />.
> 5. Wrap ```<CardWrapper />``` in Suspense.
>
> ```tsx
> /*'/app/dashboard/page.tsx'*/
> import CardWrapper from '@/app/ui/dashboard/cards';
> // ...
> import {
>   RevenueChartSkeleton,
>   LatestInvoicesSkeleton,
>   CardsSkeleton,
> } from '@/app/ui/skeletons';
>  
> export default async function Page() {
>   return (
>     <main>
>       <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
>         Dashboard
>       </h1>
>       <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
>         <Suspense fallback={<CardsSkeleton />}>
>           <CardWrapper />
>         </Suspense>
>       </div>
>       // ...
>     </main>
>   );
> }
> ```
>
>
> ```tsx
> /*'/app/ui/dashboard/cards.tsx'*/
> // ...
> import { fetchCardData } from '@/app/lib/data';
>  
> // ...
>  
> export default async function CardWrapper() {
>   const {
>     numberOfInvoices,
>     numberOfCustomers,
>     totalPaidInvoices,
>     totalPendingInvoices,
>   } = await fetchCardData();
>  
>   return (
>     <>
>       <Card title="Collected" value={totalPaidInvoices} type="collected" />
>       <Card title="Pending" value={totalPendingInvoices} type="pending" />
>       <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
>       <Card
>         title="Total Customers"
>         value={numberOfCustomers}
>         type="customers"
>       />
>     </>
>   );
> }
> ```
>
>
### 10. Partial Prerendering
> #### Static vs. Dynamic Routes
>> For most web apps built today, you choose between static and dynamic rendering for your entire application or a specific route. And in Next.js, if you call a dynamic function in a route (like querying your database), the whole route becomes dynamic.
>> 
>> However, most routes are not fully static or dynamic. For example, consider an e-commerce site. You might want to render the majority of the product information page statically, but you may want to fetch the user's cart and recommended products dynamically, this allows you show personalized content to your users.
>> 
> #### What is Partial Prerendering
>> A new rendering model that combines the benefits of static and dynamic rendering in the same route.
>> 
>> When a user visits a route:
>> + A static route shell that includes the navbar and product information is served, ensuring a fast initial load.
>> + The shell leaves holes where dynamic content like the cart and recommended products will load asynchronously.
>> + The async holes are streamed in parallel, reducing the page's overall load time.
>>
> #### How does Partial Prerendering work?
>> Partial Prerendering uses React's Suspense (which you learned about in the previous chapter) to defer rendering parts of your application until some condition is met (e.g. data is loaded).
>> 
>> The Suspense fallback and static content are embedded into the initial HTML file. At build time (or during revalidation), the static content is prerendered to create a static shell. The rendering of dynamic content is postponed until the user requests the route.
>> 
>> Wrapping a component in Suspense doesn't make the component itself dynamic, but rather, Suspense is used as a boundary between your static and dynamic code.
>> 
> #### Implementing Partial Prerendering
>> Enable PPR for your Next.js app by adding the ppr option to your ```next.config.mjs``` file:
>>
>> ```mjs
>> /*next.config.mjs*/
>> /** @type {import('next').NextConfig} */
>>  
>> const nextConfig = {
>>   experimental: {
>>     ppr: 'incremental',
>>   },
>> };
>>  
>> export default nextConfig;
>> ```
>>
>> The 'incremental' value allows you to adopt PPR for specific routes.
>>
>> Next, add the experimental_ppr segment config option to your dashboard layout:
>>
>> ```tsx
>> /*/app/dashboard/layout.tsx*/
>> import SideNav from '@/app/ui/dashboard/sidenav';
>>  
>> export const experimental_ppr = true;
>>  
>> // ...
>> ```
>>
>>

### 11. Adding Search and Pagination
> #### Starting code
>>
>> ```tsx
>> /*/app/dashboard/invoices/page.tsx*/
>> import Pagination from '@/app/ui/invoices/pagination';
>> import Search from '@/app/ui/search';
>> import Table from '@/app/ui/invoices/table';
>> import { CreateInvoice } from '@/app/ui/invoices/buttons';
>> import { lusitana } from '@/app/ui/fonts';
>> import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
>> import { Suspense } from 'react';
>>  
>> export default async function Page() {
>>   return (
>>     <div className="w-full">
>>       <div className="flex w-full items-center justify-between">
>>         <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
>>       </div>
>>       <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
>>         <Search placeholder="Search invoices..." />
>>         <CreateInvoice />
>>       </div>
>>       {/*  <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
>>         <Table query={query} currentPage={currentPage} />
>>       </Suspense> */}
>>       <div className="mt-5 flex w-full justify-center">
>>         {/* <Pagination totalPages={totalPages} /> */}
>>       </div>
>>     </div>
>>   );
>> }
>> ```
>>
>> Code Explanation:
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
>>
>> ##### Implementation steps:
>>> ##### 1. Capture the user's input
>>>> Create a new handleSearch function, and add an onChange listener to the <input> element. onChange will invoke handleSearch whenever the input value changes.
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> 'use client';
>>>>  
>>>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>>>>  
>>>> export default function Search({ placeholder }: { placeholder: string }) {
>>>>   function handleSearch(term: string) {
>>>>     console.log(term);
>>>>   }
>>>>  
>>>>   return (
>>>>     <div className="relative flex flex-1 flex-shrink-0">
>>>>       <label htmlFor="search" className="sr-only">
>>>>         Search
>>>>       </label>
>>>>       <input
>>>>         className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
>>>>         placeholder={placeholder}
>>>>         onChange={(e) => {
>>>>           handleSearch(e.target.value);
>>>>         }}
>>>>       />
>>>>       <MagnifyingGlassIcon className="absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
>>>>     </div>
>>>>   );
>>>> }
>>>> ```
>>>> 
>>> ##### 2. Update the URL with the search params.
>>>> Import the ```useSearchParams``` hook from ```'next/navigation'```, and assign it to a variable:
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> 'use client';
>>>>  
>>>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>>>> import { useSearchParams } from 'next/navigation';
>>>>  
>>>> export default function Search() {
>>>>   const searchParams = useSearchParams();
>>>>  
>>>>   function handleSearch(term: string) {
>>>>     console.log(term);
>>>>   }
>>>>   // ...
>>>> }
>>>> ```
>>>>
>>>> Inside ```handleSearch```, create a new ```URLSearchParams``` instance using your new ```searchParams``` variable.
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> 'use client';
>>>>  
>>>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>>>> import { useSearchParams } from 'next/navigation';
>>>>  
>>>> export default function Search() {
>>>>   const searchParams = useSearchParams();
>>>>  
>>>>   function handleSearch(term: string) {
>>>>     const params = new URLSearchParams(searchParams);
>>>>   }
>>>>   // ...
>>>> }
>>>> ```
>>>>
>>>> ```URLSearchParams``` is a Web API that provides utility methods for manipulating the URL query parameters. Instead of creating a complex string literal, you can use it to get the params string like ```?page=1&query=a```.
>>>>
>>>> Next, ```set``` the params string based on the user’s input. If the input is empty, you want to ```delete``` it:
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> 'use client';
>>>>  
>>>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>>>> import { useSearchParams } from 'next/navigation';
>>>>  
>>>> export default function Search() {
>>>>   const searchParams = useSearchParams();
>>>>  
>>>>   function handleSearch(term: string) {
>>>>     const params = new URLSearchParams(searchParams);
>>>>     if (term) {
>>>>       params.set('query', term);
>>>>     } else {
>>>>       params.delete('query');
>>>>     }
>>>>   }
>>>>   // ...
>>>> }
>>>> ```
>>>>
>>>> You can use Next.js's ```useRouter``` and ```usePathname``` hooks to update the URL.
>>>>
>>>> Import ```useRouter``` and ```usePathname``` from ```'next/navigation'```, and use the ```replace``` method from ```useRouter()``` inside ```handleSearch```:
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> 'use client';
>>>>  
>>>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>>>> import { useSearchParams, usePathname, useRouter } from 'next/navigation';
>>>>  
>>>> export default function Search() {
>>>>   const searchParams = useSearchParams();
>>>>   const pathname = usePathname();
>>>>   const { replace } = useRouter();
>>>>  
>>>>   function handleSearch(term: string) {
>>>>     const params = new URLSearchParams(searchParams);
>>>>     if (term) {
>>>>       params.set('query', term);
>>>>     } else {
>>>>       params.delete('query');
>>>>     }
>>>>     replace(`${pathname}?${params.toString()}`);
>>>>   }
>>>> }
>>>> ```
>>>>
>>>> Here's a breakdown of what's happening:
>>>> + ```${pathname}``` is the current path, in your case, ```"/dashboard/invoices"```.
>>>> + As the user types into the search bar, ```params.toString()``` translates this input into a URL-friendly format.
>>>> + ```replace(${pathname}?${params.toString()})``` updates the URL with the user's search data. For example, ```/dashboard/invoices?query=lee``` if the user searches for "Lee."
>>>> + The URL is updated without reloading the page, thanks to Next.js's client-side navigation (which you learned about in the chapter on navigating between pages.
>>>>
>>> ##### 3. Keeping the URL and input in sync
>>>> To ensure the input field is in sync with the URL and will be populated when sharing, you can pass a ```defaultValue``` to input by reading from ```searchParams```:
>>>>
>>>> ```tsx
>>>> /*/app/ui/search.tsx*/
>>>> <input
>>>>   className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
>>>>   placeholder={placeholder}
>>>>   onChange={(e) => {
>>>>     handleSearch(e.target.value);
>>>>   }}
>>>>   defaultValue={searchParams.get('query')?.toString()}
>>>> />
>>>> ```
>>>>
>>> ##### 4. Updating the table
>>>> Page components accept a prop called ```searchParams```, so you can pass the current URL params to the ```<Table>``` component.
>>>>
>>>> ```tsx
>>>> /*/app/dashboard/invoices/page.tsx*/
>>>> import Pagination from '@/app/ui/invoices/pagination';
>>>> import Search from '@/app/ui/search';
>>>> import Table from '@/app/ui/invoices/table';
>>>> import { CreateInvoice } from '@/app/ui/invoices/buttons';
>>>> import { lusitana } from '@/app/ui/fonts';
>>>> import { Suspense } from 'react';
>>>> import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
>>>>  
>>>> export default async function Page({
>>>>   searchParams,
>>>> }: {
>>>>   searchParams?: {
>>>>     query?: string;
>>>>     page?: string;
>>>>   };
>>>> }) {
>>>>   const query = searchParams?.query || '';
>>>>   const currentPage = Number(searchParams?.page) || 1;
>>>>  
>>>>   return (
>>>>     <div className="w-full">
>>>>       <div className="flex w-full items-center justify-between">
>>>>         <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
>>>>       </div>
>>>>       <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
>>>>         <Search placeholder="Search invoices..." />
>>>>         <CreateInvoice />
>>>>       </div>
>>>>       <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
>>>>         <Table query={query} currentPage={currentPage} />
>>>>       </Suspense>
>>>>       <div className="mt-5 flex w-full justify-center">
>>>>         {/* <Pagination totalPages={totalPages} /> */}
>>>>       </div>
>>>>     </div>
>>>>   );
>>>> }
>>>> ```
>>>>
>>>> If you navigate to the ```<Table```> Component, you'll see that the two props, ```query``` and ```currentPage```, are passed to the ```fetchFilteredInvoices()``` function which returns the invoices that match the query.
>>>>
>>>> ```tsx
>>>> /*/app/ui/invoices/table.tsx*/
>>>> // ...
>>>> export default async function InvoicesTable({
>>>>   query,
>>>>   currentPage,
>>>> }: {
>>>>   query: string;
>>>>   currentPage: number;
>>>> }) {
>>>>   const invoices = await fetchFilteredInvoices(query, currentPage);
>>>>   // ...
>>>> }
>>>> ```
>>>>
> #### Debouncing
>> Inside your ```handleSearch``` function, add the following ```console.log```:
>>
>> ```tsx
>> /*/app/ui/search.tsx*/
>> function handleSearch(term: string) {
>>   console.log(`Searching... ${term}`);
>>  
>>   const params = new URLSearchParams(searchParams);
>>   if (term) {
>>     params.set('query', term);
>>   } else {
>>     params.delete('query');
>>   }
>>   replace(`${pathname}?${params.toString()}`);
>> }
>> ```
>> The URL is updated on every keystroke. This isn't a problem as our application is small, but imagine if your application had thousands of users, each sending a new request to your database on each keystroke.
>> 
>> Debouncing is a programming practice that limits the rate at which a function can fire. In our case, you only want to query the database when the user has stopped typing.
>> 
>> You can implement debouncing in a few ways, including manually creating your debounce function.
>> 
>> Install ```use-debounce```:
>> ```pnpm i use-debounce```
>> 
>> In your ```<Search>``` Component, import a function called ```useDebouncedCallback```:
>>
>> ```tsx
>> /*/app/ui/search.tsx*/
>> // ...
>> import { useDebouncedCallback } from 'use-debounce';
>>  
>> // Inside the Search Component...
>> const handleSearch = useDebouncedCallback((term) => {
>>   console.log(`Searching... ${term}`);
>>  
>>   const params = new URLSearchParams(searchParams);
>>   if (term) {
>>     params.set('query', term);
>>   } else {
>>     params.delete('query');
>>   }
>>   replace(`${pathname}?${params.toString()}`);
>> }, 300);
>> ```
>>
>> This function will wrap the contents of ```handleSearch``` and only run the code after a specific time once the user has stopped typing (300ms).
>> 
> #### Adding pagination
>> After introducing the search feature, the table displays only six invoices simultaneously. This is because the ```fetchFilteredInvoices()``` function in ```data.ts``` returns a maximum of 6 invoices per page.
>> 
>> Adding pagination allows users to navigate the different pages to view all the invoices. Let's see how you can implement pagination using URL params, just like you did with search.
>> 
>> Navigate to the ```<Pagination/>``` component and you'll notice it's a Client Component. You don't want to fetch data on the client as this would expose your database secrets (remember, you're not using an API layer). Instead, you can fetch the data on the server, and pass it to the component as a prop.
>> 
>> In ```/dashboard/invoices/page.tsx```, import a new function called ```fetchInvoicesPages``` and pass the ```query``` from ```searchParams``` as an argument:
>>
>> ```tsx
>> /*/app/dashboard/invoices/page.tsx*/
>> // ...
>> import { fetchInvoicesPages } from '@/app/lib/data';
>>  
>> export default async function Page({
>>   searchParams,
>> }: {
>>   searchParams?: {
>>     query?: string,
>>     page?: string,
>>   },
>> }) {
>>   const query = searchParams?.query || '';
>>   const currentPage = Number(searchParams?.page) || 1;
>>  
>>   const totalPages = await fetchInvoicesPages(query);
>>  
>>   return (
>>     // ...
>>   );
>> }
>> ```
>>
>> ```fetchInvoicesPages``` returns the total number of pages based on the search query. For example, if 12 invoices match the search query, and each page displays six invoices, the total number of pages would be 2.
>>
>> Next, pass the ```totalPages``` prop to the ```<Pagination/>``` component:
>>
>> ```tsx
>> /*/app/dashboard/invoices/page.tsx*/
>> // ...
>>  
>> export default async function Page({
>>   searchParams,
>> }: {
>>   searchParams?: {
>>     query?: string;
>>     page?: string;
>>   };
>> }) {
>>   const query = searchParams?.query || '';
>>   const currentPage = Number(searchParams?.page) || 1;
>>  
>>   const totalPages = await fetchInvoicesPages(query);
>>  
>>   return (
>>     <div className="w-full">
>>       <div className="flex w-full items-center justify-between">
>>         <h1 className={`${lusitana.className} text-2xl`}>Invoices</h1>
>>       </div>
>>       <div className="mt-4 flex items-center justify-between gap-2 md:mt-8">
>>         <Search placeholder="Search invoices..." />
>>         <CreateInvoice />
>>       </div>
>>       <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
>>         <Table query={query} currentPage={currentPage} />
>>       </Suspense>
>>       <div className="mt-5 flex w-full justify-center">
>>         <Pagination totalPages={totalPages} />
>>       </div>
>>     </div>
>>   );
>> }
>> ```
>>
>> Navigate to the ```<Pagination/>``` component and import the ```usePathname``` and ```useSearchParams``` hooks. We will use this to get the current page and set the new page. Make sure to also uncomment the code in this component. Your application will break temporarily as you haven't implemented the ```<Pagination/>``` logic yet. Let's do that now!
>>
>> ```tsx
>> /*/app/ui/invoices/pagination.tsx*/
>> 'use client';
>>  
>> import { ArrowLeftIcon, ArrowRightIcon } from '@heroicons/react/24/outline';
>> import clsx from 'clsx';
>> import Link from 'next/link';
>> import { generatePagination } from '@/app/lib/utils';
>> import { usePathname, useSearchParams } from 'next/navigation';
>>  
>> export default function Pagination({ totalPages }: { totalPages: number }) {
>>   const pathname = usePathname();
>>   const searchParams = useSearchParams();
>>   const currentPage = Number(searchParams.get('page')) || 1;
>>  
>>   // ...
>> }
>> ```
>>
>> Next, create a new function inside the ```<Pagination>``` Component called ```createPageURL```. Similarly to the search, you'll use ```URLSearchParams``` to set the new page number, and pathName to create the URL string.
>>
>> ```tsx
>> /*/app/ui/invoices/pagination.tsx*/
>> 'use client';
>>  
>> import { ArrowLeftIcon, ArrowRightIcon } from '@heroicons/react/24/outline';
>> import clsx from 'clsx';
>> import Link from 'next/link';
>> import { generatePagination } from '@/app/lib/utils';
>> import { usePathname, useSearchParams } from 'next/navigation';
>>  
>> export default function Pagination({ totalPages }: { totalPages: number }) {
>>   const pathname = usePathname();
>>   const searchParams = useSearchParams();
>>   const currentPage = Number(searchParams.get('page')) || 1;
>>  
>>   const createPageURL = (pageNumber: number | string) => {
>>     const params = new URLSearchParams(searchParams);
>>     params.set('page', pageNumber.toString());
>>     return `${pathname}?${params.toString()}`;
>>   };
>>  
>>   // ...
>> }
>> ```
>>
>> Here's a breakdown of what's happening:
>>
>> + ```createPageURL``` creates an instance of the current search parameters.
>> + Then, it updates the "page" parameter to the provided page number.
>> + Finally, it constructs the full URL using the pathname and updated search parameters.
>>
>> Finally, when the user types a new search query, you want to reset the page number to 1. You can do this by updating the ```handleSearch``` function in your ```<Search>``` component:
>>
>> ```tsx
>> /*/app/ui/search.tsx*/
>> 'use client';
>>  
>> import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
>> import { usePathname, useRouter, useSearchParams } from 'next/navigation';
>> import { useDebouncedCallback } from 'use-debounce';
>>  
>> export default function Search({ placeholder }: { placeholder: string }) {
>>   const searchParams = useSearchParams();
>>   const { replace } = useRouter();
>>   const pathname = usePathname();
>>  
>>   const handleSearch = useDebouncedCallback((term) => {
>>     const params = new URLSearchParams(searchParams);
>>     params.set('page', '1');
>>     if (term) {
>>       params.set('query', term);
>>     } else {
>>       params.delete('query');
>>     }
>>     replace(`${pathname}?${params.toString()}`);
>>   }, 300);
>>  
>> ```
>>

### 12. Mutating Data
#### What are Server Actions?
> React Server Actions allow you to run asynchronous code directly on the server. They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.
> 
#### Creating an invoice
> Here are the steps you'll take to create a new invoice:
> 1. Create a form to capture the user's input.
> 2. Create a Server Action and invoke it from the form.
> 3. Inside your Server Action, extract the data from the formData object.
> 4. Validate and prepare the data to be inserted into your database.
> 5. Insert the data and handle any errors.
> 6. Revalidate the cache and redirect the user back to the invoices page.
> 7. 
> ##### 1. Create a new route and form
>>
>> ```tsx
>> /*/dashboard/invoices/create/page.tsx*/
>> import Form from '@/app/ui/invoices/create-form';
>> import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
>> import { fetchCustomers } from '@/app/lib/data';
>>  
>> export default async function Page() {
>>   const customers = await fetchCustomers();
>>  
>>   return (
>>     <main>
>>       <Breadcrumbs
>>         breadcrumbs={[
>>           { label: 'Invoices', href: '/dashboard/invoices' },
>>           {
>>             label: 'Create Invoice',
>>             href: '/dashboard/invoices/create',
>>             active: true,
>>           },
>>         ]}
>>       />
>>       <Form customers={customers} />
>>     </main>
>>   );
>> }
>> ```
>> 
> ##### 2. Create a server action
>> In your ```actions.ts``` file, create a new async function that accepts ```formData```:
>>
>> ```ts
>> /*/app/lib/action.ts*/
>> 'use server';
>>  
>> export async function createInvoice(formData: FormData) {}
>> ```
>>
>> By adding the 'use server,' you mark all the exported functions within the file as Server Actions. These server functions can be imported and used in Client and Server components.
>>
>> Then, in your ```<Form>``` component, import the createInvoice from ```your actions.ts``` file. Add a ```action``` attribute to the ```<form>``` element, and call the createInvoice action.
>>
>> ```tsx
>> /app/ui/invoices/create-form.tsx*/
>> import { customerField } from '@/app/lib/definitions';
>> import Link from 'next/link';
>> import {
>>   CheckIcon,
>>   ClockIcon,
>>   CurrencyDollarIcon,
>>   UserCircleIcon,
>> } from '@heroicons/react/24/outline';
>> import { Button } from '@/app/ui/button';
>> import { createInvoice } from '@/app/lib/actions';
>>  
>> export default function Form({
>>   customers,
>> }: {
>>   customers: customerField[];
>> }) {
>>   return (
>>     <form action={createInvoice}>
>>       // ...
>>   )
>> }
>> ```
>>
> ##### 3. Extract the data from ```formData```
>> Back in your ```actions.ts``` file, you'll need to extract the values of ```formData```, there are a couple of methods you can use.
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> 'use server';
>>  
>> export async function createInvoice(formData: FormData) {
>>   const rawFormData = {
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   };
>>   // Test it out:
>>   console.log(rawFormData);
>> }
>> ```
>>
> ##### 4. Validate and prepare the data
>> ###### Type validation and coercion
>> It's important to validate that the data from your form aligns with the expected types in your database. For instance, if you add a ```console.log``` inside your action:
>>
>> ```console.log(typeof rawFormData.amount);```
>>
>> You'll notice that the amount is of type string, not number. This is because input elements with ```type="number"``` actually return a string
>>
>> In your ```actions.ts``` file, import Zod and define a schema that matches the shape of your form object. This schema will validate the ```formData``` before saving it to a database.
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> 'use server';
>>  
>> import { z } from 'zod';
>>  
>> const FormSchema = z.object({
>>   id: z.string(),
>>   customerId: z.string(),
>>   amount: z.coerce.number(),
>>   status: z.enum(['pending', 'paid']),
>>   date: z.string(),
>> });
>>  
>> const CreateInvoice = FormSchema.omit({ id: true, date: true });
>>  
>> export async function createInvoice(formData: FormData) {
>>   // ...
>> }
>> ```
>>
>> You can then pass your ```rawFormData``` to ```CreateInvoice``` to validate the types:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> // ...
>> export async function createInvoice(formData: FormData) {
>>   const { customerId, amount, status } = CreateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>> }
>> ```
>>
>> ###### Storing values in cents
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> // ...
>> export async function createInvoice(formData: FormData) {
>>   const { customerId, amount, status } = CreateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>   const amountInCents = amount * 100;
>> }
>> ```
>>
>> ###### Creating new dates
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> // ...
>> export async function createInvoice(formData: FormData) {
>>   const { customerId, amount, status } = CreateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>   const amountInCents = amount * 100;
>>   const date = new Date().toISOString().split('T')[0];
>> }
>> ```
>>
> ##### 5. Inserting the data into your database
>> Now that you have all the values you need for your database, you can create an SQL query to insert the new invoice into your database and pass in the variables:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> import { z } from 'zod';
>> import { sql } from '@vercel/postgres';
>>  
>> // ...
>>  
>> export async function createInvoice(formData: FormData) {
>>   const { customerId, amount, status } = CreateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>   const amountInCents = amount * 100;
>>   const date = new Date().toISOString().split('T')[0];
>>  
>>   await sql`
>>     INSERT INTO invoices (customer_id, amount, status, date)
>>     VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
>>   `;
>> }
>> ```
>>
> ##### 6. Revalidate and redirect
>> Next.js has a Client-side Router Cache that stores the route segments in the user's browser for a time. Along with prefetching, this cache ensures that users can quickly navigate between routes while reducing the number of requests made to the server.
>>
>> Since you're updating the data displayed in the invoices route, you want to clear this cache and trigger a new request to the server. You can do this with the revalidatePath function from Next.js:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> 'use server';
>>  
>> import { z } from 'zod';
>> import { sql } from '@vercel/postgres';
>> import { revalidatePath } from 'next/cache';
>>  
>> // ...
>>  
>> export async function createInvoice(formData: FormData) {
>>   const { customerId, amount, status } = CreateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>   const amountInCents = amount * 100;
>>   const date = new Date().toISOString().split('T')[0];
>>  
>>   await sql`
>>     INSERT INTO invoices (customer_id, amount, status, date)
>>     VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
>>   `;
>>  
>>   revalidatePath('/dashboard/invoices');
>> }
>> ```
>>
>> At this point, you also want to redirect the user to the ```/dashboard/invoices``` page. You can do this with the ```redirect``` function from Next.js:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> 'use server';
>>  
>> import { z } from 'zod';
>> import { sql } from '@vercel/postgres';
>> import { revalidatePath } from 'next/cache';
>> import { redirect } from 'next/navigation';
>>  
>> // ...
>>  
>> export async function createInvoice(formData: FormData) {
>>   // ...
>>  
>>   revalidatePath('/dashboard/invoices');
>>   redirect('/dashboard/invoices');
>> }
>> ```
>>
>>

#### Updating an invoice
> These are the steps you'll take to update an invoice:
> ##### 1. Create a new dynamic route segment with the invoice id
>> In your ```<Table>``` component, notice there's a <UpdateInvoice /> button that receives the invoice's id from the table records.
>>
>> ```tsx
>> /*/app/ui/invoices/table.tsx*/
>> export default async function InvoicesTable({
>>   query,
>>   currentPage,
>> }: {
>>   query: string;
>>   currentPage: number;
>> }) {
>>   return (
>>     // ...
>>     <td className="flex justify-end gap-2 whitespace-nowrap px-6 py-4 text-sm">
>>       <UpdateInvoice id={invoice.id} />
>>       <DeleteInvoice id={invoice.id} />
>>     </td>
>>     // ...
>>   );
>> }
>> ```
>>
>> Navigate to your <UpdateInvoice /> component, and update the link's href to accept the id prop. You can use template literals to link to a dynamic route segment:
>>
>> ```tsx
>> /*/app/ui/invoices/buttons.tsx*/
>> import { PencilIcon, PlusIcon, TrashIcon } from '@heroicons/react/24/outline';
>> import Link from 'next/link';
>>  
>> // ...
>>  
>> export function UpdateInvoice({ id }: { id: string }) {
>>   return (
>>     <Link
>>       href={`/dashboard/invoices/${id}/edit`}
>>       className="rounded-md border p-2 hover:bg-gray-100">
>>       <PencilIcon className="w-5" />
>>     </Link>
>>   );
>> }
>> ```
>>
> ##### 2. Read the invoice ID from the page params
>>
>> ```tsx
>> /*/app/dashboard/invoices/[id]/edit/page.tsx*/
>> import Form from '@/app/ui/invoices/edit-form';
>> import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
>> import { fetchCustomers } from '@/app/lib/data';
>>  
>> export default async function Page() {
>>   return (
>>     <main>
>>       <Breadcrumbs
>>         breadcrumbs={[
>>           { label: 'Invoices', href: '/dashboard/invoices' },
>>           {
>>             label: 'Edit Invoice',
>>             href: `/dashboard/invoices/${id}/edit`,
>>             active: true,
>>           },
>>         ]}
>>       />
>>       <Form invoice={invoice} customers={customers} />
>>     </main>
>>   );
>> }
>> ```
>>
>> Notice how it's similar to your ```/create``` invoice page, except it imports a different form (from the edit-form.tsx file). This form should be pre-populated with a ```defaultValue``` for the customer's name, invoice amount, and status. To pre-populate the form fields, fetch the specific invoice using ```id```.
>>
>> In addition to ```searchParams```, page components also accept a prop called ```params``` which you can use to access the ```id```. Update your ```<Page>``` component to receive the prop:
>>
>> ```tsx
>> /*/app/dashboard/invoices/[id]/edit/page.tsx*/
>> import Form from '@/app/ui/invoices/edit-form';
>> import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
>> import { fetchCustomers } from '@/app/lib/data';
>>  
>> export default async function Page({ params }: { params: { id: string } }) {
>>   const id = params.id;
>>   // ...
>> }
>> ```
>>
> ##### 3. Fetch the specific invoice from your database
>> + Import a new fetchInvoiceById function and pass the id as an argument.
>> + Import fetchCustomers to fetch the customer names for the dropdown.
>>
>> You can use ```Promise.all``` to fetch both the invoice and customers in parallel:
>>
>> ```tsx
>> /*/dahsboard/invoices/[id]/edit/page.tsx*/
>> import Form from '@/app/ui/invoices/edit-form';
>> import Breadcrumbs from '@/app/ui/invoices/breadcrumbs';
>> import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
>>  
>> export default async function Page({ params }: { params: { id: string } }) {
>>   const id = params.id;
>>   const [invoice, customers] = await Promise.all([
>>     fetchInvoiceById(id),
>>     fetchCustomers(),
>>   ]);
>>   // ...
>> }
>> ```
>>
> ##### 4. Pass the ```id``` to the Server Action
>> You can pass ```id``` to the Server Action using JS ```bind```. This will ensure that any values passed to the Server Action are encoded.
>>
>> ```tsx
>> /*/app/ui/invoices/edit-form.tsx*/
>> // ...
>> import { updateInvoice } from '@/app/lib/actions';
>>  
>> export default function EditInvoiceForm({
>>   invoice,
>>   customers,
>> }: {
>>   invoice: InvoiceForm;
>>   customers: CustomerField[];
>> }) {
>>   const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
>>  
>>   return (
>>     <form action={updateInvoiceWithId}>
>>       <input type="hidden" name="id" value={invoice.id} />
>>     </form>
>>   );
>> }
>> ```
>> 
>> Then, in your ```actions.ts``` file, create a new action, ```updateInvoice```:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> // Use Zod to update the expected types
>> const UpdateInvoice = FormSchema.omit({ id: true, date: true });
>>  
>> // ...
>>  
>> export async function updateInvoice(id: string, formData: FormData) {
>>   const { customerId, amount, status } = UpdateInvoice.parse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>  
>>   const amountInCents = amount * 100;
>>  
>>   await sql`
>>     UPDATE invoices
>>     SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
>>     WHERE id = ${id}
>>   `;
>>  
>>   revalidatePath('/dashboard/invoices');
>>   redirect('/dashboard/invoices');
>> }
>> ```


### 13. Handling Errors
#### Adding ```try/catch``` to Server Actions
> JavaScript's ```try/catch``` allows you to handle errors gracefully.
>
> ```ts
> /*/app/lib/actions.ts*/
> export async function createInvoice(formData: FormData) {
>   const { customerId, amount, status } = CreateInvoice.parse({
>     customerId: formData.get('customerId'),
>     amount: formData.get('amount'),
>     status: formData.get('status'),
>   });
>  
>   const amountInCents = amount * 100;
>   const date = new Date().toISOString().split('T')[0];
>  
>   try {
>     await sql`
>       INSERT INTO invoices (customer_id, amount, status, date)
>       VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
>     `;
>   } catch (error) {
>     return {
>       message: 'Database Error: Failed to Create Invoice.',
>     };
>   }
>  
>   revalidatePath('/dashboard/invoices');
>   redirect('/dashboard/invoices');
> }
> export async function updateInvoice(id: string, formData: FormData) {
>   const { customerId, amount, status } = UpdateInvoice.parse({
>     customerId: formData.get('customerId'),
>     amount: formData.get('amount'),
>     status: formData.get('status'),
>   });
>  
>   const amountInCents = amount * 100;
>  
>   try {
>     await sql`
>         UPDATE invoices
>         SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
>         WHERE id = ${id}
>       `;
>   } catch (error) {
>     return { message: 'Database Error: Failed to Update Invoice.' };
>   }
>  
>   revalidatePath('/dashboard/invoices');
>   redirect('/dashboard/invoices');
> }
> export async function deleteInvoice(id: string) {
>   try {
>     await sql`DELETE FROM invoices WHERE id = ${id}`;
>     revalidatePath('/dashboard/invoices');
>     return { message: 'Deleted Invoice.' };
>   } catch (error) {
>     return { message: 'Database Error: Failed to Delete Invoice.' };
>   }
> }
> ```
>
> Redirect is being called outside of the try/catch block because redirect works by throwing an error, which the catch block would catch. To avoid this, you can call redirect after try/catch. Redirect would only be reachable if try is successful.
>
#### Handling all errors with ```error.tsx```
> The ```error.tsx``` file can be used to define a UI boundary for a route segment. It serves as a catch-all for unexpected errors and allows you to display a fallback UI to your users.
>
> ```tsx
> /*/dashboard/invoices/error.tsx
> 'use client';
>  
> import { useEffect } from 'react';
>  
> export default function Error({
>   error,
>   reset,
> }: {
>   error: Error & { digest?: string };
>   reset: () => void;
> }) {
>   useEffect(() => {
>     // Optionally log the error to an error reporting service
>     console.error(error);
>   }, [error]);
>  
>   return (
>     <main className="flex h-full flex-col items-center justify-center">
>       <h2 className="text-center">Something went wrong!</h2>
>       <button
>         className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
>         onClick={
>           // Attempt to recover by trying to re-render the invoices route
>           () => reset()
>         }
>       >
>         Try again
>       </button>
>     </main>
>   );
> }
> ```
>
> Code explanation:
> + "use client" - ```error.tsx``` needs to be a Client Component.
> + It accepts two props:
>   + error: This object is an instance of JavaScript's native Error object.
>   + reset: This is a function to reset the error boundary. When executed, the function will try to re-render the route segment.
>
#### Handling 404 errors with the ```notFound``` function
> Another way you can handle errors gracefully is by using the ```notFound``` function. While ```error.tsx``` is useful for catching all errors, ```notFound``` can be used when you try to fetch a resource that doesn't exist.
> 
> You can confirm that the resource hasn't been found by going into your fetchInvoiceById function in data.ts, and console logging the returned invoice:
>
> ```ts
> /*/app/lib/data.ts*/
> export async function fetchInvoiceById(id: string) {
>   noStore();
>   try {
>     // ...
>  
>     console.log(invoice); // Invoice is an empty array []
>     return invoice[0];
>   } catch (error) {
>     console.error('Database Error:', error);
>     throw new Error('Failed to fetch invoice.');
>   }
> }
> ```
>
> Now that you know the invoice doesn't exist in your database, let's use ```notFound``` to handle it. Navigate to ```/dashboard/invoices/[id]/edit/page.tsx```, and import ```{ notFound }``` from ```'next/navigation'```.
>
> ```tsx
> /*/dashboard/invoices/[id]/edit/page.tsx*/
> import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
> import { updateInvoice } from '@/app/lib/actions';
> import { notFound } from 'next/navigation';
> 
> export default async function Page({ params }: { params: { id: string } }) {
>   const id = params.id;
>   const [invoice, customers] = await Promise.all([
>     fetchInvoiceById(id),
>     fetchCustomers(),
>   ]);
>  
>   if (!invoice) {
>     notFound();
>   }
> 
>   // ...
> }
> ```
>
> ```<Page>``` will now throw an error if a specific invoice is not found. To show an error UI to the user. Create a ```not-found.tsx``` file inside the ```/edit``` folder.
> ![image](https://github.com/user-attachments/assets/f361fc8d-4ccc-40b2-985d-301c9c95d816)
> Then, inside the not-found.tsx file, paste the following code:
>
> ```tsx
> /*/dashboard/invoices/[id]/edit/not-found.tsx*/
> import Link from 'next/link';
> import { FaceFrownIcon } from '@heroicons/react/24/outline';
> 
> export default function NotFound() {
>   return (
>     <main className="flex h-full flex-col items-center justify-center gap-2">
>       <FaceFrownIcon className="w-10 text-gray-400" />
>       <h2 className="text-xl font-semibold">404 Not Found</h2>
>       <p>Could not find the requested invoice.</p>
>       <Link
>         href="/dashboard/invoices"
>         className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
>       >
>         Go Back
>       </Link>
>     </main>
>   );
> }
> ```
>

### 14. Improving Accessibility
#### What is accessibility?
> Accessibility refers to designing and implementing web applications that everyone can use, including those with disabilities. It's a vast topic that covers many areas, such as keyboard navigation, semantic HTML, images, colours, videos, etc.

#### Improving form accessibility
> + Semantic HTML: Using semantic elements (```<input>```, ```<option>```, etc) instead of <div>. This allows assistive technologies (AT) to focus on the input elements and provide appropriate contextual information to the user, making the form easier to navigate and understand.
> + Labelling: Including ```<label>``` and the ```htmlFor``` attribute ensures that each form field has a descriptive text label. This improves AT support by providing context and also enhances usability by allowing users to click on the label to focus on the corresponding input field.
> + Focus Outline: The fields are appropriately styled to show an outline when they are in focus. This is critical for accessibility as it visually indicates the active element on the page, helping both keyboard and screen reader users to understand where they are on the form. You can verify this by pressing ```tab```.

#### Form validation
> ##### Client-side validation
>> The simplest would be to rely on the form validation provided by the browser by adding the ```required``` attribute to the ```<input>``` and ```<select>``` elements in your forms. For example:
>>
>> ```tsx
>> /*/app/ui/invoices/create-form.tsx*/
>> <input
>>   id="amount"
>>   name="amount"
>>   type="number"
>>   placeholder="Enter USD amount"
>>   className="peer block w-full rounded-md border border-gray-200 py-2 pl-10 text-sm outline-2 placeholder:text-gray-500"
>>   required
>> />
>> ```
>> 
> ##### Server-side validation
>> By validating forms on the server, you can:
>> + Ensure your data is in the expected format before sending it to your database.
>> + Reduce the risk of malicious users bypassing client-side validation.
>> + Have one source of truth for valid data.
>> In your ```create-form.tsx``` component, import the ```useActionState``` hook from ```react```. Since ```useActionState``` is a hook, you will need to turn your form into a Client Component using ```"use client"``` directive:
>>
>> ```tsx
>> /*/app/ui/invoices/create-form.tsx*/
>> 'use client';
>>  
>> // ...
>> import { useActionState } from 'react';
>> ```
>> 
>> Inside your Form Component, the useActionState hook:
>> + Takes two arguments: ```(action, initialState)```.
>> + Returns two values: ```[state, formAction]``` - the form state and a function to be called when the form is submitted.
>>
>> Pass your ```createInvoice``` action as an argument of ```useActionState```, and inside your ```<form action={}>``` attribute, call formAction.
>> The ```initialState``` can be anything you define, in this case, create an object with two empty keys: ```message``` and ```errors```, and import the ```State``` type from your ```actions.ts``` file:
>> 
>> ```tsx
>> /*/app/ui/invoices/create-form.tsx*/
>> // ...
>> import { createInvoice, State } from '@/app/lib/actions';
>> import { useActionState } from 'react';
>>  
>> export default function Form({ customers }: { customers: CustomerField[] }) {
>>   const initialState: State = { message: null, errors: {} };
>>   const [state, formAction] = useActionState(createInvoice, initialState);
>>  
>>   return <form action={formAction}>...</form>;
>> }
>> ```
>>
>> In your action.ts file, you can use Zod to validate form data. Update your FormSchema as follows:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> const FormSchema = z.object({
>>   id: z.string(),
>>   customerId: z.string({
>>     invalid_type_error: 'Please select a customer.',
>>   }),
>>   amount: z.coerce
>>     .number()
>>     .gt(0, { message: 'Please enter an amount greater than $0.' }),
>>   status: z.enum(['pending', 'paid'], {
>>     invalid_type_error: 'Please select an invoice status.',
>>   }),
>>   date: z.string(),
>> });
>> ```
>>
>> + ```customerId``` - Zod already throws an error if the customer field is empty as it expects a type ```string```. But let's add a friendly message if the user doesn't select a customer.
>> + ```amount``` - Since you are coercing the amount type from ```string``` to ```number```, it'll default to zero if the string is empty. Let's tell Zod we always want the amount greater than 0 with the ```.gt()``` function.
>> + ```status``` - Zod already throws an error if the status field is empty as it expects "pending" or "paid." Let's add a friendly message if the user doesn't select a status.
>>
>> Next, update your ```createInvoice``` action to accept two parameters - ```prevState``` and ```formData```. Then, change the Zod ```parse()``` function to ```safeParse()```:
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> export type State = {
>>   errors?: {
>>     customerId?: string[];
>>     amount?: string[];
>>     status?: string[];
>>   };
>>   message?: string | null;
>> };
>>  
>> export async function createInvoice(prevState: State, formData: FormData) {
>>   // Validate form fields using Zod
>>   const validatedFields = CreateInvoice.safeParse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>
>>   // If form validation fails, return errors early. Otherwise, continue.
>>   if (!validatedFields.success) {
>>     return {
>>       errors: validatedFields.error.flatten().fieldErrors,
>>       message: 'Missing Fields. Failed to Create Invoice.',
>>     };
>>   }
>>
>>   // Prepare data for insertion into the database
>>   const { customerId, amount, status } = validatedFields.data;
>>   const amountInCents = amount * 100;
>>   const date = new Date().toISOString().split('T')[0];
>>  
>>   // Insert data into the database
>>   try {
>>     await sql`
>>       INSERT INTO invoices (customer_id, amount, status, date)
>>       VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
>>     `;
>>   } catch (error) {
>>     // If a database error occurs, return a more specific error.
>>     return {
>>       message: 'Database Error: Failed to Create Invoice.',
>>     };
>>   }
>>  
>>   // Revalidate the cache for the invoices page and redirect the user.
>>   revalidatePath('/dashboard/invoices');
>>   redirect('/dashboard/invoices');
>>   // ...
>> }
>> ```
>>
>> + ```formData``` - same as before.
>> + ```prevState``` - contains the state passed from the ```useActionState``` hook. You won't be using it in the action in this example, but it's a required prop.
>> + ```safeParse()``` - returns an object containing either a ```success``` or ```error``` field. This will help handle validation more gracefully without putting this logic inside the ```try/catch``` block.
>> If ```validatedFields``` isn't successful, we return the function early with the error messages from Zod.
>>
>> Add a ternary operator that checks for each specific error. For example, after the customer's field, you can add:
>>
>> ```tsx
>> /*/app/ui/invoices/create-form.tsx*/
>> <form action={formAction}>
>>   <div className="rounded-md bg-gray-50 p-4 md:p-6">
>>     {/* Customer Name */}
>>     <div className="mb-4">
>>       <label htmlFor="customer" className="mb-2 block text-sm font-medium">
>>         Choose customer
>>       </label>
>>       <div className="relative">
>>         <select
>>           id="customer"
>>           name="customerId"
>>           className="peer block w-full rounded-md border border-gray-200 py-2 pl-10 text-sm outline-2 placeholder:text-gray-500"
>>           defaultValue=""
>>           aria-describedby="customer-error"
>>         >
>>           <option value="" disabled>
>>             Select a customer
>>           </option>
>>           {customers.map((name) => (
>>             <option key={name.id} value={name.id}>
>>               {name.name}
>>             </option>
>>           ))}
>>         </select>
>>         <UserCircleIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500" />
>>       </div>
>>       <div id="customer-error" aria-live="polite" aria-atomic="true">
>>         {state.errors?.customerId &&
>>           state.errors.customerId.map((error: string) => (
>>             <p className="mt-2 text-sm text-red-500" key={error}>
>>               {error}
>>             </p>
>>           ))}
>>       </div>
>>     </div>
>>     // ...
>>   </div>
>> </form>
>> ```
>>
>> + ```aria-describedby="customer-error"```: This establishes a relationship between the ```select``` element and the error message container. It indicates that the container with ```id="customer-error"``` describes the ```select``` element. Screen readers will read this description when the user interacts with the ```select``` box to notify them of errors.
>> + ```id="customer-error"```: This ```id``` attribute uniquely identifies the HTML element that holds the error message for the select input. This is necessary for ```aria-describedby``` to establish the relationship.
>> + ```aria-live="polite"```: The screen reader should politely notify the user when the error inside the ```div``` is updated. When the content changes (e.g. when a user corrects an error), the screen reader will announce these changes, but only when the user is idle so as not to interrupt them.
>>
>> Example of Edit form validation
>>
>> ```tsx
>> /*/app/ui/invoices/edit-form.tsx*/
>> // ...
>> import { updateInvoice, State } from '@/app/lib/actions';
>> import { useActionState } from 'react';
>>  
>> export default function EditInvoiceForm({
>>   invoice,
>>   customers,
>> }: {
>>   invoice: InvoiceForm;
>>   customers: CustomerField[];
>> }) {
>>   const initialState: State = { message: null, errors: {} };
>>   const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
>>   const [state, formAction] = useActionState(updateInvoiceWithId, initialState);
>>  
>>   return <form action={formAction}></form>;
>> }
>> ```
>>
>> ```ts
>> /*/app/lib/actions.ts*/
>> export async function updateInvoice(
>>   id: string,
>>   prevState: State,
>>   formData: FormData,
>> ) {
>>   const validatedFields = UpdateInvoice.safeParse({
>>     customerId: formData.get('customerId'),
>>     amount: formData.get('amount'),
>>     status: formData.get('status'),
>>   });
>>  
>>   if (!validatedFields.success) {
>>     return {
>>       errors: validatedFields.error.flatten().fieldErrors,
>>       message: 'Missing Fields. Failed to Update Invoice.',
>>     };
>>   }
>>  
>>   const { customerId, amount, status } = validatedFields.data;
>>   const amountInCents = amount * 100;
>>  
>>   try {
>>     await sql`
>>       UPDATE invoices
>>       SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
>>       WHERE id = ${id}
>>     `;
>>   } catch (error) {
>>     return { message: 'Database Error: Failed to Update Invoice.' };
>>   }
>>  
>>   revalidatePath('/dashboard/invoices');
>>   redirect('/dashboard/invoices');
>> }
>> ```
>>
>> 
### 15. Adding Authentication
#### Creating the login route
> Start by creating a new route in your application called /login and paste the following code:
>
> ```tsx
> /*/app/login/page.tsx*/
> import AcmeLogo from '@/app/ui/acme-logo';
> import LoginForm from '@/app/ui/login-form';
>  
> export default function LoginPage() {
> return (
>     <main className="flex items-center justify-center md:h-screen">
>       <div className="relative mx-auto flex w-full max-w-[400px] flex-col space-y-2.5 p-4 md:-mt-32">
>         <div className="flex h-20 w-full items-end rounded-lg bg-blue-500 p-3 md:h-36">
>           <div className="w-32 text-white md:w-36">
>             <AcmeLogo />
>           </div>
>         </div>
>         <LoginForm />
>       </div>
>     </main>
>   );
> }
> ```
> 
#### Setting up the NextAuth.js
> Install NextAuth.js by running the following command in your terminal: ```pnpm i next-auth@beta```
> 
> Next, generate a secret key for your application. This key is used to encrypt cookies, ensuring the security of user sessions. You can do this by running the following command in your terminal: ```openssl ran -base64 32```
>
> Then,in your ```.env``` file, add your generated key to the AUTH_SECRET variable: ```AUTH_SECRET=your-secret-key```
>
> ##### Adding the pages option
> Create an ```auth.config.ts``` file at the root of our project that exports an ```authConfig``` object. This object will contain the configuration options for ```NextAuth.js```.
>
> ```ts
> /*/auth/config.ts*/
> import type { NextAuthConfig } from 'next-auth';
>  
> export const authConfig = {
>   pages: {
>     signIn: '/login',
>   },
> } satisfies NextAuthConfig;
> ```
>
> ##### Protecting your routes with Next.js Middleware
> Next, add the logic to protect your routes. This will prevent users from accessing the dashboard pages unless they are logged in.
>
> ```ts
> /*/auth.config.ts*/
> import type { NextAuthConfig } from 'next-auth';
>  
> export const authConfig = {
>   pages: {
>     signIn: '/login',
>   },
>   callbacks: {
>     authorized({ auth, request: { nextUrl } }) {
>       const isLoggedIn = !!auth?.user;
>       const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
>       if (isOnDashboard) {
>         if (isLoggedIn) return true;
>         return false; // Redirect unauthenticated users to login page
>       } else if (isLoggedIn) {
>         return Response.redirect(new URL('/dashboard', nextUrl));
>       }
>       return true;
>     },
>   },
>   providers: [], // Add providers with an empty array for now
> } satisfies NextAuthConfig;
> ```
>
> The ```authorized``` callback is used to verify if the request is authorized to access a page via Next.js Middleware. It is called before a request is completed, and it receives an object with the auth and ```request``` properties. The ```auth``` property contains the user's session, and the ```request``` property contains the incoming request.
>
> The ```providers``` option is an array where you list different login options. For now, it's an empty array to satisfy NextAuth config. You'll learn more about it in the Adding the Credentials provider section.
>
> Next, you will need to import the ```authConfig``` object into a Middleware file.
>
> ```ts
> /*/middleware.ts*/
> import NextAuth from 'next-auth';
> import { authConfig } from './auth.config';
>  
> export default NextAuth(authConfig).auth;
>  
> export const config = {
>   // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
>   matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
> };
> ```
>
> Here you're initializing NextAuth.js with the ```authConfig``` object and exporting the ```auth``` property. You're also using the ```matcher``` option from Middleware to specify that it should run on specific paths.
>
> ##### Password having
> In your seed.js file, you used a package called bcrypt to hash the user's password before storing it in the database. You will use it again later in this chapter to compare that the password entered by the user matches the one in the database. However, you must create a separate file for the bcrypt package. This is because bcrypt relies on Node.js APIs that are not available in Next.js Middleware.
>
> Create a new file called ```auth.ts``` that spreads your ```authConfig``` object:
>
> ```ts
> /*/auth.ts*/
> import NextAuth from 'next-auth';
> import { authConfig } from './auth.config';
>  
> export const { auth, signIn, signOut } = NextAuth({
>   ...authConfig,
> });
> ```
>
> ##### Adding the Credentials provider
> Next, you will need to add the ```providers``` option for NextAuth.js. providers is an array where you list different login options such as Google or GitHub. For this course, we will focus on using the Credentials provider only.
>
> ```ts
> /*/auth.ts*/
> import NextAuth from 'next-auth';
> import { authConfig } from './auth.config';
> import Credentials from 'next-auth/providers/credentials';
>  
> export const { auth, signIn, signOut } = NextAuth({
>   ...authConfig,
>   providers: [Credentials({})],
> });
> ```
>
> ##### Adding the sign-in functionality
> You can use the ```authorize``` function to handle the authentication logic. Similarly to Server Actions, you can use ```zod``` to validate the email and password before checking if the user exists in the database:
>
> ```ts
> /*/auth.ts*/
> import NextAuth from 'next-auth';
> import { authConfig } from './auth.config';
> import Credentials from 'next-auth/providers/credentials';
> import { z } from 'zod';
>  
> export const { auth, signIn, signOut } = NextAuth({
>   ...authConfig,
>   providers: [
>     Credentials({
>       async authorize(credentials) {
>         const parsedCredentials = z
>           .object({ email: z.string().email(), password: z.string().min(6) })
>           .safeParse(credentials);
>       },
>     }),
>   ],
> });
> ```
>
> After validating the credentials, create a new ```getUser``` function that queries the user from the database. Then, call bcrypt.compare to check if the passwords match:
>
> ```ts
> /*/auth.ts*/
> import NextAuth from 'next-auth';
> import Credentials from 'next-auth/providers/credentials';
> import { authConfig } from './auth.config';
> import { z } from 'zod';
> import { sql } from '@vercel/postgres';
> import type { User } from '@/app/lib/definitions';
> import bcrypt from 'bcrypt';
>  
> async function getUser(email: string): Promise<User | undefined> {
>   try {
>     const user = await sql<User>`SELECT * FROM users WHERE email=${email}`;
>     return user.rows[0];
>   } catch (error) {
>     console.error('Failed to fetch user:', error);
>     throw new Error('Failed to fetch user.');
>   }
> }
>  
> export const { auth, signIn, signOut } = NextAuth({
>   ...authConfig,
>   providers: [
>     Credentials({
>       async authorize(credentials) {
>         const parsedCredentials = z
>           .object({ email: z.string().email(), password: z.string().min(6) })
>           .safeParse(credentials);
>  
>         if (parsedCredentials.success) {
>           const { email, password } = parsedCredentials.data;
>           const user = await getUser(email);
>           if (!user) return null;
>           const passwordsMatch = await bcrypt.compare(password, user.password);
>  
>           if (passwordsMatch) return user;
>         }
> 
>         console.log('Invalid credentials');
>         return null;
>       },
>     }),
>   ],
> });
> ```
>
> ##### Updating the login form
> Now, you need to connect the auth logic with your login form. In your ```actions.ts``` file, create a new action called ```authenticate```. This action should import the ```signIn``` function from ```auth.ts```:
>
> ```ts
> /*/app/lib/actions.ts*/
> 'use server';
>  
> import { signIn } from '@/auth';
> import { AuthError } from 'next-auth';
>  
> // ...
>  
> export async function authenticate(
>   prevState: string | undefined,
>   formData: FormData,
> ) {
>   try {
>     await signIn('credentials', formData);
>   } catch (error) {
>     if (error instanceof AuthError) {
>       switch (error.type) {
>         case 'CredentialsSignin':
>           return 'Invalid credentials.';
>         default:
>           return 'Something went wrong.';
>       }
>     }
>     throw error;
>   }
> }
> ```
>
> Finally, in your ```login-form.tsx``` component, you can use React's ```useActionState``` to call the server action, handle form errors, and display the form's pending state:
>
> ```tsx
> /*/app/ui/login-form.tsx*/
> 'use client';
>  
> import { lusitana } from '@/app/ui/fonts';
> import {
>   AtSymbolIcon,
>   KeyIcon,
>   ExclamationCircleIcon,
> } from '@heroicons/react/24/outline';
> import { ArrowRightIcon } from '@heroicons/react/20/solid';
> import { Button } from '@/app/ui/button';
> import { useActionState } from 'react';
> import { authenticate } from '@/app/lib/actions';
>  
> export default function LoginForm() {
>   const [errorMessage, formAction, isPending] = useActionState(
>     authenticate,
>     undefined,
>   );
>  
>   return (
>     <form action={formAction} className="space-y-3">
>       <div className="flex-1 rounded-lg bg-gray-50 px-6 pb-4 pt-8">
>         <h1 className={`${lusitana.className} mb-3 text-2xl`}>
>           Please log in to continue.
>         </h1>
>         <div className="w-full">
>           <div>
>             <label
>               className="mb-3 mt-5 block text-xs font-medium text-gray-900"
>               htmlFor="email">
>               Email
>             </label>
>             <div className="relative">
>               <input
>                 className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
>                 id="email"
>                 type="email"
>                 name="email"
>                 placeholder="Enter your email address"
>                 required
>               />
>               <AtSymbolIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
>             </div>
>           </div>
>           <div className="mt-4">
>             <label
>               className="mb-3 mt-5 block text-xs font-medium text-gray-900"
>               htmlFor="password">
>               Password
>             </label>
>             <div className="relative">
>               <input
>                 className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
>                 id="password"
>                 type="password"
>                 name="password"
>                 placeholder="Enter password"
>                 required
>                 minLength={6}
>               />
>               <KeyIcon className="pointer-events-none absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
>             </div>
>           </div>
>         </div>
>         <Button className="mt-4 w-full" aria-disabled={isPending}>
>           Log in <ArrowRightIcon className="ml-auto h-5 w-5 text-gray-50" />
>         </Button>
>         <div
>           className="flex h-8 items-end space-x-1"
>           aria-live="polite"
>           aria-atomic="true">
>           {errorMessage && (
>             <>
>               <ExclamationCircleIcon className="h-5 w-5 text-red-500" />
>               <p className="text-sm text-red-500">{errorMessage}</p>
>             </>
>           )}
>         </div>
>       </div>
>     </form>
>   );
> }
> ```
>
#### Adding the logout functionality
> To add the logout functionality to ```<SideNav />```, call the ```signOut``` function from ```auth.ts``` in your ```<form>``` element:
>
> ```tsx
> /*/ui/dashboard/sidenav.tsx*/
> import Link from 'next/link';
> import NavLinks from '@/app/ui/dashboard/nav-links';
> import AcmeLogo from '@/app/ui/acme-logo';
> import { PowerIcon } from '@heroicons/react/24/outline';
> import { signOut } from '@/auth';
>  
> export default function SideNav() {
>   return (
>     <div className="flex h-full flex-col px-3 py-4 md:px-2">
>       // ...
>       <div className="flex grow flex-row justify-between space-x-2 md:flex-col md:space-x-0 md:space-y-2">
>         <NavLinks />
>         <div className="hidden h-auto w-full grow rounded-md bg-gray-50 md:block"></div>
>         <form
>           action={async () => {
>             'use server';
>             await signOut();
>           }}>
>           <button className="flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3">
>             <PowerIcon className="w-6" />
>             <div className="hidden md:block">Sign Out</div>
>           </button>
>         </form>
>       </div>
>     </div>
>   );
> }
> ```
> 
### 16. Adding Metadata

- ## What is Next.js?
	- Next.js is a React framework for building full-stack web applications. You use React Components to build user interfaces, and Next.js for additional features and optimizations.
- ## What does Next.js have that React doesn't?
	- In simple terms:
		- Next.js simplifies the development process.
		- On top of that it optimizes our web apps.
- ## Features of Next.js
	- It does that through it's **primary features**:
		- ##### 1. Rendering
			- We know that **React** renders User Interface on the ***Client Side*** while **Next.js** performs ***Server Side Rendering***.
			- However Next.js offers flexibility in rendering options. We can choose to render the UI on Client Side or Server Side depending on our needs.
			- ##### Client Side Rendering or Browser Rendering:
				- CSR happens on the client side i.e. the browser.
				- ==When the user requests a Web page:== 
					- 1.) The server sends a basic HTML document and JavaScript code, and this HTML is usually almost empty
					- 2.) The browser then downloads and executes the JavaScript code which leads to the rendering of the components and finally the display of the website.
				- ##### Server Side Rendering:
					- SSR involves rendering the Web page on the server before transmitting it to the client's device/browser.
					- When the user requests a Web page:
						- 1.) The server processes the request and renders the component on the server side.
						- 2.) The server then sends back the fully rendered HTML to the client's browser enabling immediate display.
						- This distinction highlights an essential aspect of **Web Dev**.
							- ##### SEO - Search Engine Optimization
								- Search Engine Crawlers face difficulties indexing pages dynamically rendered on the client's side as a result the SEO performance of such pages may suffer and not rank them appropriately.
								- By using Next.js, this issue is resolved by sending pre-rendered code directly to the client. This enables:
									- **Easy Crawling**
									- **Indexing**
		- ##### 2. Routing
			- In React, we use external package called React Router DOM and then create routes.
			- But in Next.js, we create file based routing system which means the routing is handled by the file system. Each folder in the `app directory` becomes a route and the folder name becomes the routes path. For example - `/blog`, `/about`, `/profile`, `/services` as - `http://localhost:3000/about`.
				 ![[Pasted image 20260202193942.png]]
		- ##### 3. FullStack
			- `API routes` --> Enabling the creation of serverless functions to handle API requests.
		- ##### 4. Automatic Code Splitting
			- Code splitting is a technique that breaks down large bundles of JavaScript code int smaller, more manageable chunks that can be loaded as needed.
- ## Data Fetching in Next.js
	- There are `3 ways` to `fetch data` in Next.js:
		1. Server Side Rendering (SSR)
		2. Static Site Generation (SSG)
		3. Incremental Static Regeneration (ISR)
	- #### 1. Server Side Rendering (SSR)
		- ##### What it is
			- Data is fetched **on every request**.
			- The page is rendered on the **server at request time**.
			- A new HTML page is generated for **each user request**.
		- ##### When to use
			- Data changes frequently
			- User-specific data (dashboards, profiles)
		- ##### Flow (easy to remember)
			1. User requests page
			2. Server fetches data
			3. Server renders HTML
			4. Browser receives ready HTML

	- #### 2. Static Site Generation (SSG)
		- ##### What it is
			- Data is fetched **at build time**.
			- HTML is generated **once** during build.
			- Same HTML is served to **all users**.
			##### When to use
			- Data does not change often
			- Blogs, documentation, landing pages
		- ##### Flow
			1. App builds
			2. Data is fetched
			3. HTML is generated
			4. Users receive pre-built HTML

	- #### 3. Incremental Static Site Regeneration (ISR)
		- ##### What it is
			- Like SSG, but **can update after deployment**.
			- Page is regenerated **in the background** after a fixed time.
			- Users get **fast static pages** + **fresh data**.
		- ##### When to use
			- Data updates occasionally
			- Product listings, news pages
		- ##### Flow
			1. Page is built statically
			2. User requests page
			3. After 10 seconds, Next.js regenerates page
			4. New users get updated HTML
- ## Metadata
	- We can define Metadata in `two` ways: `Static` and `Dynamic`.
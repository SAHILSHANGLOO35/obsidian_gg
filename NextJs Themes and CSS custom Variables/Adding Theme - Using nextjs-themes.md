## Dark and Light mode
- We will use nextjs-themes as they hepls us to persist the theme in users' system.
- We will use `<ThemeProvider>` component for this feature and wrap our `<main>{children}</main>` in the `layout.tsx `file with that Provider as shown -
- ```
	  <ThemeProvider
		  attribute="class"
		  defaultTheme="system"
		  enableSystem
		  disableTransitionOnChange
	  >
		  <Navbar />
          <main className="bg-background text-foreground">{children}</main>
       </ThemeProvider>
  ```
- In the `<main>` tag, we have written `bg-background` `text-foreground` classes. This comes from globals.css file where we define our custom CSS properties or variables and use them like this.
- Then we make `toggle.tsx` component where we actually write the logic of `switching themes` using `next-themes` and some UI.

## Making Container Wrapper
- Also k/as `resuable Container` (`layout wraper`) component. This is done so our whole landing page / Website content remains within specified layout and width by making the `children` that we pass in this for example the `<Hero />` component as shown below -
- ```
	  <Container>
        <Heading as="h1">
          Agents that do the work <br /> Approvals that keep you safe.
        </Heading>
        <SubHeading className="py-8">
          Deploy AI agents that plan, act through your tools, and report
          outcomes-without changing how your teams work.
        </SubHeading>
        <div className="flex items-center gap-6">
          <Button className="shadow-brand">Start your free trial</Button>
          <Button asChild variant="outline">
            <Link href="#">View role based demos</Link>
          </Button>
        </div>
        <LandingImages />
      </Container>
  ```
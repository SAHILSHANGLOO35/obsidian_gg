Earlier, When we used to create React App using ==Functional Components==, then we didn't have access to the ==state management and lifecycle methods==.

To access these features we had to add class components.

But after introducing React Hooks from version 16.8, we can now use state management and other react features without writing class components.

Simply, ==Hooks== are special type of magical function use to perform some specific tasks.

#### Benefits of React Hooks?
- React hooks -
	- simplify the code,
	- improves the readability,
	- reusability and
	- overall performance of the application.
	
## 1.) useState Hook
- useState is a react hook, which creates a "state variable" which helps us to track state in components and updates the user interface when state changes.
- ==Batching in React==
 ```
	setCount(count + 1); // 0 + 1 = 1
	setCount(count + 1); // 0 + 1 => Still the original initial value
	setCount(count + 1); // 0 + 1 => Still the original initial value
	setCount(count + 1); // 0 + 1 => Still the original initial value,
	because-
		it is still in running state and the function has not completed yet
		Hence it will update the count only by 1 not by 4 as React processes
		the request in batches for better performance and for it the count
		has still not updated yet.
```
- Using Previous values to update new latest value
```
Car Object example using (...prev):

  const [car, setCar] = useState({
    brand: "Ferrari",
    model: "Roma",
    year: "2025",
    color: "Red",
  });

  const changeColor = () => {
    if (car.color === "Red") {
      setCar((prev) => {
        return { ...prev, color: "Blue" };
      });
    } else {
      setCar((car) => {
        return { ...car, color: "Red" };
      });
    }
  };
```

## 2.) useEffect Hook
- The useEffect Hook allows us to perform side effects in our components.
- Some examples of side effects are:
	- Fetching data from API,
	- Directly updating the DOM,
	- Timers like SetTimeOut and SetInterval.
- There are 3 ways of using useEffect():
	- Without dependency:
		- In this case, the useEffect will run for any state change that is in the component.  
	- Empty dependency array:
		- In this case, the useEffect will run only for the 1st time when the component is loaded on the browser.
	- Using variables in dependency array:
		- In this case, the useEffect will run when the component first loads on the browser and when the variable in the dependency array changes state.

## 3.) useRef Hook
- useRef is a react Hook that allow us to create ==mutable variables==, which will not re-render the component.
	- We use this when we don't want the component to re-render when the value of any state changes like it does in useState as shown below.
		- ```
			  const [value, setValue] = useState(0);
			  const count = useRef(0);
			  
			  useEffect(() => {
				  count.current += 1;
			  }
			  
			  return (
				  <>
					  <button
						  className="border rounded-md px-5 py-2"
						  onClick={() => {
						  setValue((prev) => prev - 1);
						  }}
					  >		
						  -1
					  </button>
					  <h1 className="text-white">{value}</h1>
					  <button
						  className="border rounded-md px-5 py-2"
						  onClick={() => {
						  setValue((prev) => prev + 1);
						  }}
					  >		
						  +1
					  </button>
					  <h1>Render Count: {count.current}</h1>
				  </>
				  );
			  });
		  ```
- useRef is also used for accessing DOM elements.
	- ```
			const inputElem = useRef<HTMLInputElement | null>(null);
				const btnClicked = () => {
				  if (inputElem.current) {
				  console.log(inputElem.current);
				  inputElem.current.style.backgroundColor = "blue";
				}
				
			  return (
				  <div className="flex gap-10">
				  <input
				  ref={inputElem}
				  className="border pl-4"
				  type="text"
				  placeholder="Enter"
				  />
				  <button onClick={btnClicked}>Click here</button>
				  </div>
			  );
	  ```

- Real-world examples:
	- ### Digital Stop Watch
		- What changes on screen?
		- Timer value (seconds)
	 This must update the UI → **useState**
	- What do we store silently?
		- Interval ID (used to stop/start timer)  
		- User doesn’t see it → **useRef**
## 4.) useMemo Hook
- The React useMemo Hook returns a ==memoized value==. (it's like caching a value so that it doesn't need to be recalculated.)
- The useMemo Hook only runs when one of its dependencies gets updated. This can ==improve the performance== of the application. There is one more hook in react to improve performance, that is ==useCallback== hook.
- The useMemo and useCallback Hooks are similar. The main difference is:
	- useMemo returns a memoized value.
	- useCallback returns a memoized function.
- Simple rule to remember while using this and to differentiate between useMemo and useEffect is that - "==useMemo== decides whether to recompute a value before render using dependencies, while ==useEffect== runs after render and cannot prevent recalculations."
- ==Simply, useEffect runs after render and useMemo runs during render==
- Code Snippet showing use of useMemo for heavy calc:
	- ```
	  const [number, setNumber] = useState(0);
	  const [count, setCount] = useState(0);
	  
	  function cubeNum(num: number) {
		  console.log("Calculation done!");
		  return Math.pow(num, 3);
		}
		
		return (
	    <>
	      <input
	        type="number"
	        className="text-white border pl-2"
	        onChange={(e) => setNumber(Number(e.target.value))}
		        value={number
		     />
		     <h1 className="text-white">Cube of the number: {result}</h1>
		     <button onClick={() => setCount(count + 1)}>Counter++</button>
		     <h1>Counter: {count}</h1>
	    </>
	  );
	  ```

**==NOTE: When a parent re-renders, all children re-render by default==**
## 5.) useCallback Hook
- useCallback is a React Hook that lets us ==cache a function definition== between re-renders.
- It means, when we use useCallback Hook, it does not create multiple instance of same function when re-render happens.
- **Referential Equality in React**:
	- It refers to whether two variables, specifically non-primitive values like **objects, arrays, and functions**, point to the **exact same location in memory.**
	- For example - In the following example, there are two functions which are returning the same statement, but when we check ***fn1 === fn2***, it's false - because both functions are created on different memory locations, so these aare not same functions and hence giving false.
		- ```
			const fn1 = () => return "Hello";
			const fn2 = () => return "Hello";
		  ```
- So, When we re-render the following component with the newfn prop, React is thinking of it as a different function and creating new instance of it every time and so the  new function as a prop every time, hence re-rendering the ==<Header /> component== again.
	- ```
		  "use client";
		  import { useState } from "react";
		  import Header from "../components/header";
		  
		  export const UseCallback = () => {
		  const [count, setCount] = useState(0);
		  
		  const newfn = () => {};
		  return (
			  <>
				  <Header newfn={newfn} />
				  <h1 className="text-4xl font-semibold">{count}</h1>
				  <button
					  onClick={() => setCount((prevCount) => prevCount + 1)}
					  className="border px-3 py-1 rounded-md cursor-pointer
					  active:scale-90 transition duration-200"
				  >
					  Click here
				  </button>
			  </>
			);
		};
	  ```
- **Solution -** Therefore, We can solve this by using ==useCallback Hook== which caches the function in memory and uses that only preventing re-rendering of the ==<Header /> component== as shown below:
	- ```
		  "use client";
		  import { useCallback, useState } from "react";
		  import Header from "../components/header";
		  
		  export const UseCallback = () => {
		  const [count, setCount] = useState(0);
		  
		  const newfn = useCallback(() => {}, []);
		  
		  return (
			  <>
				  <Header newfn={newfn} />
				  <h1 className="text-4xl font-semibold">{count}</h1>
				  <button
					  onClick={() => setCount((prevCount) => prevCount + 1)}
					  className="border px-3 py-1 rounded-md cursor-pointer
					  active:scale-90 transition duration-200"
				  >
					  Click here
				  </button>
			  </>
			);
		};
	  ```
- To create new function (when dependencies change), we use dependency array: 
	- **caching the function but creating the new function when the count changes by passing the dependency.**
		- ```
			const newfn = useCallback(() => {
				console.log(count);
			}, [count]);
		  ```

## 6.) useContext Hook
- useContext is a React Hook that allows us to access data from any component without explicitly passing it down through props at every level.
- Simply, useContext is used to manage Global Data in React App.
- We can use useContext Hook in 3 steps:
	- 1.) Creating the Context
		- ```
			  "use client";
			  import React, { createContext } from "react";
			  
			  // 1.) Creating the Context
			  export const AppContext = createContext<string | undefined
			  (undefined);
		  ```
	- 2.) Providing the Context
		- ```
			  // 2.) Providing the context
			  export const ContextProvider = ({children}:
			  {children:React.ReactNode}) => {
				  const phone = "+91 6006";
				  return <AppContext.Provider value={phone}>{children
				  </AppContext.Provider>;
				  };
		  ```
	- 3.) Consuming the Context.
		- ```
			  "use client";
			  import { useContext } from "react";
			  import { AppContext } from "../context/appContext";
			  
			  export const Footer = () => {
				  // 3.) Consuming the Context
				  const phone = useContext(AppContext);
				  return (
					  <>
						  <div>Footer</div>
						  <h3>Phone: {phone}</h3>
					  </>
				  );
			  };
		  ```
- The image shows the prop drilling from top level APP > ["Footer", ["Profile" > "Contact"]] ![[Pasted image 20260108011436.png]]
- The most common use of Context API is: 
	- To share current theme of our App,
	- To share the authenticated user,
	- To share the result of an API call with all of its components in our App.
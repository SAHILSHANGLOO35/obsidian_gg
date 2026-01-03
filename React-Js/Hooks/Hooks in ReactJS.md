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
	setCount(count + 1); // 0 + 1 => Still the original initial value, because-
	
	it is still in running state and the function has not completed yet! Hence
	it will update the count only by 1 not by 4 as React processes the request
	in batches for better performance and for it the count has still not
	updated yet.
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
- 
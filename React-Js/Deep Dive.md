###  [[ReactJS]] => In 2013 - By Facebook developer - Jordan Walke
==Componenet based aarchitecture ==

### Library vs Framework
- ##### Library
	- GSAP
	- Lenis
	- ReactJS
- ##### Framework
	- NextJS
	- Angular

- Library is used for one particular feature. A library is a collection of reusable code components that perform specific tasks or offer particular functionalities.
- A framework provides a structured environment and a set of predefined rules and guidelines for building an application.

### Real DOM vs Virtual DOM
- Real DOM is the actual DOM - in the form of a tree that is made using HTML.
	![[Pasted image 20251107200717.png]]
- Virtual DOM is the copy of the original Real DOM.
	- The concept is that if we want to change an element in the DOM like by clicking a button then it compares it with the Real DOM and then the element that is differed gets changed in Real DOM.
	- Therefore, it just changes single element not the whole DOM and thus prevents whole re-render of the Real DOM and thus no extra reload of the page.

### JSX
- JSX = HTML + [[Javascript]]

### Vite
- Vite is a bundler- a build tool.
- Vite takes our React JSX code and transforms it into raw HTML, CSS, and JS files that can be run by most browsers. Those files are then hosted and served to end users.
- It will also expose scripts for running a dev server.

### Hooks
- Special type of magical function use to perform some specific tasks.
	- useState - For managing states.
	- useEffect - For performing side effects - like function call (API Call mostly, mounting / unmounting of components, event listener).
	- useRef - Used to select any specific DOM element to access DOM, it usually takes a reference of that element. It holds mutable values so that they don't re-render.
	- useContext - Used to manage and consume the Global context. It solves the problem of Prop Drilling.
	- useReducer - Used to manage complex logics (small version of Redux).
	- useMemo & useCallback - Used for memoization - basically optimization to avoid re-renders.

### useState
- useState runs **asynchronously**. That's why if we do some state update and log it, then it will show us the previous value not the latest one in the console, although it will update the UI.
- You might expect `num` to increase by **3**, but it only increases by **1**.
	- That's because React updates the state in **==batches==**.
	- ==**Batching** means **React groups multiple state updates together** and processes them in one go — instead of re-rendering after every single `setState`.==
	- When we call multiple `setNum()` inside the same event (like a button click), React doesn't update the state immediately each time.
	- Instead, it **waits until the event handler finishes**, then **applies all the state updates at once** - based on the **same old value** of `num`.
	- As **useState** is **asynchronous** as said earlier :
		- When we click the button, React sees all the three `setNum(num + 1)` calls.
		- But since `num` has not been updated yet (it still holds the old value), all three use the same `num`.
		- After batching, React only applies the final result --> `num+1`
	- ```
		  function handleIncrement() {
			  setNum(num + 1);
			  setNum(num + 1);
			  setNum(num + 1);
		  }
	  ```


### Form Handling
- Form has a default behavior that when we submit it the page gets reload.
- To prevent this, we use **preventDefault()** method and with this the form gets submitted and the page doesn't reloads as well.

### Two way binding
- Simply - `Ek teer se do nishane`
- We don't directly interact with the form input. We use React's useState to handle that with onChange function to set the input value in the state and then use that value  in the form. This is called **TWO WAY BINDING.** Below is the simplest example:
- ```
	  import { useState } from "react";
	  
	  export function App() {

	  const [title, setTitle] = useState("");
	
	  const submitHandler = (e) => {
	    e.preventDefault();
	    console.log("Form Submitted");
	  };
	  
	  return (
	    <div>
	      <form onSubmit={(e) => submitHandler(e)}>
	        <input
	          type="text"
	          placeholder="Enter your name"
	          onChange={(e) => {
	            setTitle(e.target.value);
	          }}
	          value={title}
	        />
	        <button>Submit</button>
	      </form>
	    </div>
	  );
	}
  ```

### useEffect
- 
  `useEffect(() => {}) => If no dependency array is given, then it will run everytime even if any state changes. So we avoid it.`
  
  `useEffect(() => {}, []) => If dependency array is empty, then it will
  `only runs once when the component is first very first time.`
  
  `useEffect(() => {}, [num]) => Now if some state variable is given here
  `in the dependency array then useEffect will only run when this state
  `changes`.`


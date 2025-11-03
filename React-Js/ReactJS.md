1.) What is Babel?
- Babel is a JS compiler. It translates any other languages into JS( [[Javascript]] ).

2.) Why do we need Babel?
- When using React, we don't use normal JS, we use an enhanced version of JS - JSX called Javascript XML. It's same as JS, but we can also write HTML directly in out JS code.

3.) Problem with JSX :
- Our web browser doesn't understand JSX, it only understands normal JS.
- In order to use JSX we need to translate JSX into JS.
- To do that we use an external JS library called 'Babel':
	1.) Load the Babel external library
	- <script src=""></script>
	2.) To translate JSX into JS, we have to give script element an attribute - "text/babel"
	- <script type="text/babel"></script>

===React = external library that helps us create websites easier.===

4.) How React helps us create websites easier?
- It's more natural
- Find errors easily
- We can insert JS code into our elements.

5.) State
- State is data that is connected to the HTML and we use it to save data that changes over time.
- When we update this data, it will update the HTML
- React.useState() returns an array -
	1.) The current data: array[0]
	2.) Function that updates the data: array[1]
		And only if we use this update function in react then only react will update the HTML.

==Spread Operator (...) in [[Javascript]] - It takes the original array and copies them into the new array.==

==onChange = runs a function when we change the text inside an <input> element.==

==<body>element in CSS has a margin of 8px from all vertical and horizontal sides.==

6.) Hooks
- Hooks let us insert React features into our components.
- useEffect :
	- It runs some code after the component is created or updated.
	```
	useEffect(() => { }, [ ]);
	[ ] = Dependancy array.
	[ ] = empty => useEffect only runs once, after the component is created.
	[chatMessages] => useEffect runs everytime the chatMessages changes.
	
	```
- useRef :
	- ref = basically a container wth special React features.
	- It automatically saves an HTML element from the component.
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

React = external library that helps us create websites easier.

4.) How React helps us create websites easier?
- It's more natural
- Find errors easily
- We can insert JS code into our elements.
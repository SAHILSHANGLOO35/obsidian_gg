### React => In 2013 - By Facebook developer - Jordan Walke
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
- JSX = HTML + Javascript
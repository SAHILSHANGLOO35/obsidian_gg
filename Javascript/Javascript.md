**Closure Property:**
	A closure lets a function remember variables from where it was created.
	Example - If I return an inner function from another function, the inner one can still access the outer variables even after the outer function has finished.
	
---

**Data Attribute:**
	The purpose of a data attribute is to attach any information to an element.
	Eg - "data-product-name=${ }" in the example to attach product's name to the add to cart **button**.
```
<button class="add-to-cart-button button-primary js-add-to-cart" data-product-name="${
	product.name
}">Add to Cart</button>
```

---

#amazon-project
**Main idea of Javascript:**
	1.) Save the data
	2.) Generate the HTML
	3.) Make it interactive.

---

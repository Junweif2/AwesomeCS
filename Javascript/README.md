

# Data Structure
## Array
- `.map()`
	- `.map(()=>)`: transform array to another array
	- `.map(()=>{});`: transform array to other elments


# Conditional 
- Directly use varibale / function which return has return value
- Combine several conditions together, e.g. `&&`, `||`, `!`
``` javascript
if ( squares[i] || calculaterWinenr(squares)) {
	return;
}
```


# Immutablity
- Replace the data with a new copy which has the desired changes
	- Benefits #1: makes complex features much easier to implement, avoiding direct data mutation lets you keep previous versions of the data intact, and reuse them later.
	-  Benefits #2: cheap for components to compare whether their data has changed or not



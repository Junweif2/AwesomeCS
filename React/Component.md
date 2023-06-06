# Pure
- Return the same JSX given the same inputs
- Not _change_ any variables outside of the function’s scope or objects that were created before the call, only change the variables and objects created inside the components
- To update the screen, “set” state instead of mutating preexisting objects.


# Organization
1. Break UI apart into pieces called _components_. One component should ideally only do one thing. Establish the hierarchy, top-down for simple project, bottom-up for large ones. Wrap different componet together, and level up gradually, the default is the highest level in one file. And one file is one modules, and combine modules into one page. Cant' define component in another component.
2. Build a static version, with static value
3. Connect your components together so that the data flows through them, 
5. Describe the different visual states for each of your components, use state of component. Figure out the absolute minimal representation of the state
6. Add interactivity and inverser data flow upwards


# Structure
- `function Xxxx(){}`: component start with a ***capital letter***
- `<Xxxx />`: call the component


# Props
- Parameter & Functions & JSX that passed into the component
	- using `{xxx}` in the component structure, `function Xxxx({value1, value2, ..}){}`
	- default value, putting the normal `function Xxxx({value1, value2 = }){}`
	- passing the number in the upper component, `<Xxxx value = "" />`;  passing the value of a variable in the upper component, `<Xxxx value = {}/>`, can also use it to passing the number `{100}`
	- spread syntax when child component doesn't use any of the props directly, `function Xxxx(props){ <Xxxx {...props} /> }`
	- passing the function without parameter as a prop, passing the function with parameter is directly calling it. 
	- passing the component JSX as props when nest components, usually for visual wrapper, `<Xxx><Yyy /></Xxx>`, then construct a children in components, `function Xxxx({children}){}`

# State: as a snapshot
- React state behaves more like a snapshot. Setting it does not change the state variable you already have, but instead triggers a re-render
- Criteria:
	- Not remain unchanged
	- Not passed from parent via props
	- Not results computed from existing props or state
- State can store the value in the component independently, lets components keep track of information and change it in response to interactions
	- `import { useState } from 'react'`: import the `useState`
	- `const [xxx, setXxx] = useState(xxx);` initiate the value, and setup the function `setXxx`
	- `setXxx('')`: set the value of `xxx` directly
- Parents and Child Component: 
	- Parents can declare a shared state and pass to child components, make child component communicate and sync with each other.
	- State is private to the component, can't directly update state of parent component in child component.
	- Typically, pass down a function from parent to child component through prop, but the function can't pass the function with parameter, because directly pass the function will call the funcation to render the component, leading to infinity render. *Need to constrcut a medium function to call the function with parameters needed, like a warpped function*, simple way is to use arrow function `() => xxxXxx(xxx)`
	- 

# Render
- Parents or Self State Changes
- Conditional Rendering: `if (isTrue) {return xxx; } return yyy;` wrap `()` for multiple JSX
	- the concise way to write : `{isTrue ? xxx : yyy}`, to constructe more complicated rendering,  `{isTrue ? (xxx) : (yyy)}`
	- the concise way when only render condition is true: `{isTrue && xxx}`
	- the verbose but flexible way, asssign the *JSX* to a variable, then embed the variable with `{}` to render it: `if (isTrue) {xXXX = yYYY}...return {xXXX}`
- Rendering List
	- `.filter(element => xxx === "")` /  `.map(element => )` to filter or transform array data into array of components, the `=>` implicily return; but when `=>` followed by `{}`, muet explictly write `{}`
	- when map to a list, then use `key={}` to keep in order, the key is either the id in data struture or the directly using `{index}` when the order is fixed
	- for structured array, use multiple `map` to resolve it 


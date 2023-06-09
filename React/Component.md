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
	- passing the function without parameter as a prop, passing the function with parameter/() is directly calling it, will execute every time it renders
	- passing the component JSX as props when nest components, usually for visual wrapper, `<Xxx><Yyy /></Xxx>`, then construct a children in components, `function Xxxx({children}){}`
## Event Handler
- Event handlers are the best place to _change_ something
- it is common to name event handlers as `handle` followed by the event name, e.g. `handleClick`, `handleMouseEnter`
	- Syntax 1: define the event handler function outside, passing the function as a prop, `function handleClick(){}; <button onClick={handleClick}></button>`
	- Syntax 2: define the event handler function inside the prop, `<button onClick={function handleClick (){...}}></button>`, more concise with arrow function, `<button onClick={ ()=>{...}}></button>`
- To specific different handler for different same kine of component, abstract a general component
- Event handlers receive an **event object** as their only argument. By convention, it’s usually called `e`, can be omitted in simple cases
- Each event propagates in three phases:
	1. It travels down, calling all `onClickCapture` handlers.
	2. It runs the clicked element’s `onClick` handler. use the e.stopPropagation() to stop at here
	3. It travels upwards, calling all `onClick` handlers.
- Some event has default behavior, `e.preventDefault()` on the event object to stop this from happening:


# State: as a snapshot
- State can store the value in the component independently, lets components keep track of information and change it in response to interactions. 
	- `import { useState } from 'react'`: import the `useState`
	- `const [xxx, setXxx] = useState(xxx);` initiate the value, and setup the function `setXxx`
	- `setXxx('')`: set the value of `xxx` directly
- Criteria:
	- Not remain unchanged
	- Not passed from parent via props
	- Not results computed from existing props or state
- Compared to local variable
	- Local Variable:
		- Don’t persist between renders, which means it change the variable in current render, but the render, it disappear
		- Changes of local variables won’t trigger renders
	- State
		- Retain the data between renders.
		- Trigger React to render the component with new data (re-rendering).
- React state behaves more like a snapshot. ***Setting it does not change the state variable you already have, but instead triggers a re-render.*** If update an object and array, you need to create a new one (or make a copy of an existing one), and then update the state to use that copy. A state variable is only necessary to keep information between re-renders of a component. Within a single event handler, a regular variable will do fine.
- ***Setting state only changes it for the next render. A state variable’s value never changes within a render. Re-render will trigger after all state set is done***. A great example here
	- `setNumber(number + 1);  setNumber(number + 1);  setNumber(number + 1);` the value of `number` is still `0` even after `setNumber(number + 1)` was called, the state in this render is always 1, so you actually set number from `0` to `1` three times. React prepares to change `number` to `1` on the next render in all three sets. 
- **Updater Function**: update the same state variable multiple times before the next render, It’s common to name the updater function argument by the first letters of the corresponding state variable
	- `setNumber(n => n + 1); setNumber(n => n + 1); setNumber(n => n + 1); ` 
	- `setFriendCount(fc => fc * 2);`
- Parents and Child Component: 
	- Parents can declare a shared state and pass to child components, make child component communicate and sync with each other.
	- State is private to the component, can't directly update state of parent component in child component.
	- Typically, pass down a function from parent to child component through prop, but the function can't pass the function with parameter, because directly pass the function will call the function to render the component, leading to infinity render. *Need to constrcut a medium function to call the function with parameters needed, like a warpped function*, simple way is to use arrow function `() => xxxXxx(xxx)`
- Object's state
	- create a new object and pass it to the state setting function。 e.g. `setPosition({ x: e.clientX,  y: e.clientY });`
	- `...` object spread syntax so that you don’t need to copy every property separately, especially when you only update part of the object. e.g. `setPerson({  ...person, firstName: e.target.value});``



# Render
- Initial Render: Call the root component,  `appendChild()` DOM API to put all the DOM nodes it has created on screen.
- Re-renders: Parents or Self State Changes, does not touch the DOM if the rendering result is the same as last time
	1. Triggering a render 
	2. Rendering the component
	3. Committing to the DOM
- Conditional Rendering: `if (isTrue) {return xxx; } return yyy;` wrap `()` for multiple JSX
	- the concise way to write : `{isTrue ? xxx : yyy}`, to constructe more complicated rendering,  `{isTrue ? (xxx) : (yyy)}`
	- the concise way when only render condition is true: `{isTrue && xxx}`
	- the verbose but flexible way, asssign the *JSX* to a variable, then embed the variable with `{}` to render it: `if (isTrue) {xXXX = yYYY}...return {xXXX}`
- Rendering List
	- `.filter(element => xxx === "")` /  `.map(element => )` to filter or transform array data into array of components, 
		- the  => implictly a return
		- when => is followed by a {}, must explicitly write return 
	- when map to a list, then use `key={}` to keep in order, the key is either the id in data structure or the directly using `{index}` when the order is fixed
	- for structured array, use multiple `map` to resolve it 


# Hooks
- Hooks—functions starting with `use`—can only be called at the top level of your components or your own Hooks
- Hooks must be called unconditionally and always in the same order
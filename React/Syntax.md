
# JSX in React
- JSX element: combination of JavaScript code and HTML tags that describes what you’d like to display
- JSX and React are two separate things. JSX is a syntax extension, while React is a JavaScript library.
- Tags must be explicitly closed, e.g. `<img />`, `<li></li>`
- camelCase HTML and SVG attributes. e.g. `className="xxx"`
- `{}` can directly using the javascript variable in it, and any JavaScript expression and self wroted function
- For JS objects or inline CSS style, using double curlies `{{}}`  to distingush
- Converter Tools: https://transform.tools/html-to-jsx

# General
- `export`: makes the function accessible outside of this file, can export other component except the default one
- `default`: tells other files using your code that it’s the main function in your file
- `return`: returned to the caller of the function
	- fragments `(<> </>)` to wrap the multiple JSX elements
- `import xxx from './xxx.js'`: js can be neglected, import the default component
- `import {xxx} from './xxx.js'`: js can be neglected, import the other exported component
- `Component` start with capital letter, `someFunction` function use lower camel case
- `onSomething` names the events, `handleSomething` names the function handle the events
	- `onClick`: `<button>`'s built-in attribute


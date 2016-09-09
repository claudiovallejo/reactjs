## Chapter 1: Hello World

To get started, download the React library from the [React.js](https://facebook.github.io/react/) website. To get started with this example, you only need to do three things:

  1. Create an `.html`
  2. Include the `react` and `react-dom`libraries using `<script>`s
  3. Create an initial `<div id="app"></div>` where you're application will render

*NOTE* — You can use other libraries as well as other React applications within a web app / website.

---

The code for the first application was the following:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello React</title>
  </head>
  <body>
    <div id="app">
      <!-- My app renders here -->
    </div>
    <script src="react/build/react.js"></script>
    <script src="react/build/react-dom.js"></script>
    <script>
      ReactDOM.render(
        React.DOM.h1(null, "Hello World!"),
        document.getElementById('app')
      );
    </script>
  </body>
</html>
```

The `React` object gives access to React's APIs. The `ReactDOM` object gives access to methods that take care of rendering the app onto the document. _Components_ are the building blocks of a React application. Components are discrete, reusable blocks of code.

For this 'Hello World' application, we built a component that contains `<h1>Hello World!</h1>` that renders inside the document's `<div id="app"></div>`.

The `React.DOM` object has many properties which correspond to DOM HTML nodes. For example the `.h1`, which corresponds to an `<h1></h1>`. The `.h1()` takes two parameters:

  1. Property object
  2. Children

The property object contains DOM attribute equivalents, for example `id`, `style`, and `className`. The second parameter, the children, can contain another `React.DOM` call to nest more components or it can contain a simple text child. It's important to note that since `class` and `for` are reserved words in JavaScript, so when adding a class to a component in React, `className` and `htmlFor` must be used. Another important thing to note is that in order to pass a style property object, the JavaScript API names must be used when defining CSS properties. For example:

```javascript
React.DOM.h1(
  {
    style: {
      backgroundColor: "#0800ff"
    }
  },
  "Hello World!"
);
```

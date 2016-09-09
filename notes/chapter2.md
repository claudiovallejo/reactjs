## Chapter 2: Life of a Component

Creating your own components is easy. Here is a simple example of a custom component:

```javascript
var CustomComponent = React.createClass({
  render: function() {
    return React.DOM.h1(null, 'Chapter 2: Life of a Component');
  }
});
```

To create custom components, your custom component  _must_ use the `render: function() {∙∙∙}` method, which must return a React component. `React.createElement()` is one method of creating an instance of your custom component:

```javascript
ReactDOM.render(
  React.createElement(CustomComponent),
  document.getElementById('app')
);
```

You can use `React.createFactory(ComponentName)` to encapsulate the creation of a component, like this:

```javascript
var ComponentFactory = React.createFactory(CustomComponent);

ReactDOM.render(
  ComponentFactory(),
  document.getElementById('app')
);
```

Another way of rendering React components is to create a React component inside the `ReactDOM.render()` call, for example:

```javascript
ReactDOM.render(
  React.createElement('h1', null, 'Chapter 2: Life of a Component'),
  document.getElementById('app')
);
```

---

You can configure your components to render or behave in a specific way by using _properties_. Properties are passed down from parent to children or passed up from children to parent. A component has access to its properties via `this.props`. For example:

```javascript
var CustomComponent = React.createClass({
  render: function() {
    return React.DOM.h1(null, this.props.chapterName);
  }
});

ReactDOM.render


(;
  React.createElement(CustomComponent, { chapterName: 'Chapter 2: Life of a Component' }),
  document.getElementById('app')
);
```

Its important to note that `this.props` are read-only. To have access to settable properties, you can always create variables or declare more properties within the custom component.

`propTypes` are a way to declare the properties the component accepts. Declaring `propTypes` is optional, but using `propTypes` makes it easy for other developers to understand and work with your app. Using `propTypes` also helps you while developing because it ensures your components are always declared with the necessary properties.

When creating your components, some properties may be required while others may not. To prevent errors with non-required properties, React offers the use of the `getDefaultProps()` method. This method is used to return default values for properties that aren't required.

Here is an example of declaring `propTypes` and using the `getDefaultProps()` when creating a custom component:

```javascript
var CustomComponent = React.createClass({
  propTypes: {
    chapter: React.PropTypes.number.isRequired,
    name: React.PropTypes.string.isRequired,
    completed: React.PropTypes.bool
  },

  getDefaultProps: function() {
    return { completed: false };
  },

  return: function() {∙∙∙}
});
```

---

In React, _state_ refers to the current values your component uses to render itself. When a component's state changes, React automatically re-renders your component.

You access the state of a component by `this.state`. To update the state by `this.setState()`.

### Creating a Stateful Textarea Component
First, create a stateless version of the `textarea` component:

```javascript
var TextAreaCounter = React.createClass({
  propTypes: {
    text: React.PropTypes.string
  },

  getDefaultProps: function() {
    return { text: '' };
  },

  render: function() {
    return React.DOM.div(null,
      React.DOM.textarea({
        defaultValue: this.props.text
      }),
      React.DOM.h3(null, this.props.text.length)
    );
  }
});

ReactDOM.render(
  React.createElement(TextAreaCounter, {
    text: "Bob"
  }),
  document.getElementById('app'))
);
```

Now, create a `getInitialState()` method in `TextAreaCounter` which will take care of setting the component's initial state to the component's `this.props.text` value. After that, create a helper method, `_textChange`, which will take care of updating the value of the `textarea` whenever the text inside the text area changes. Finally, update the `render()` method to use `this.state` instead of `this.props.text`

```javascript
var TextAreaCounter = React.createClass({
  getInitialState: function() {
    return {
      text: this.props.text
    }
  },

  _textChange: function(e) {
    this.setState({
      text: e.target.value
    });
  },
  // propTypes,
  // getDefaultProps,
  render: function() {
    return React.DOM.div(null,
      React.DOM.textarea({
        value: this.state.text,
        onChange: this._textChange
      }),
      React.DOM.h3(null, this.state.text.lengthd)
    );
  }
});
```

`this.setState()` is always in charge of updating the component's state. `this.setState()` takes an object and merges the object with the existing data in `this.state`. `_textChange()` is an event listener that accepts an `e` object and takes care of placing the object's value in the state's text property.

# Goal

Use React.createClass to create Hello Component, combine those Components to create page then link to DOM by React.render.

- React.createClass -> create Hello components.
- Combine those components to create pages.
- React.render -> link components with DOM to display.


## JS

```js
// Create Hello component
var Hello = React.createClass({
  render: function() {
    return React.DOM.div({className: 'container'}, 'Hello ' + this.props.name);
  }
})
// link Hello component with DOM
React.render(
  //
  React.createFactory(Hello)({name: 'React'}), document.getElementById("app")
);


```

## Using JSX

```js
var React = require('react');

var Hello = React.createClass({
  render: function() {
    return (
      <div className="container">Hello {this.props.name}</div>
      );
    }
    })

    React.render(<Hello name="React" />, document.getElementById("app"));
```

JSX = JS + XML

## JSX + ES6,7 syntax

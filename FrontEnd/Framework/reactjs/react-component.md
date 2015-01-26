# Overview

## Render

render() method that takes input data and returns what to display

```js
var Hello = React.createClass({
  render() {
    return (
      <div><span>hello</span></div>
    )
  }
})
```

## Separation of concerns?

Markup and View logic is writing in Component. It is difference with other frameworks that separate View logic (JS) and Markup (HTML, Mustache...), this confuse someone who
want to separate View logic and Markup.

## Component IF

Input data that is passed into the component can be accessed by render() via this.props.

```js
var Hello = React.createClass({
  render: function() {
    return <div>Hello {this.props.name}</div>;
  }
  });

  React.render(<Hello name="John" />, mountNode);
```

## Dynamicaly Update

In addition to taking input data (accessed via this.props), a component can maintain internal state data (accessed via this.state). When a component's state data changes, the rendered markup will be updated by re-invoking render().

- input data: this.props
- maintain internal data: this.state
- when state data changes: use this.setState to updated

```js
<script type="text/jsx">

var Counter = React.createClass({

  getInitialState: function() {
    return {
      count: 0
    };
  },

  onClick: function() {
    this.setState({count: this.state.count + 1});
  },

  render: function() {
    return (
      <div>
      <div>count:{this.state.count}</div>
      <button onClick={this.onClick}>click!</button>
      </div>
    );
  }

});

React.render(<Counter />, document.getElementById("app"));

</script>
```

## React.createClass

- React.createClass return Component.
- To create React Element:

  ```js
  React.createElement(Component, {name: 'xxx'})
  ```
  or
  ```js
  React.createFactory(Component)
  ```

  then pass it to React.render().

- But if using JSX, you can pass directly to React.render() as Component.

  ```js

  React.render(<Component />);
  ```\

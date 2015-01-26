# React-Prop

Prop is an attribute of Component. We can use Prop as Object or Function.
Prop take place as scope in Angularjs (?)

```js
var Avatar = React.createClass({
  render() {
    var avatarImg = `/img/avatar_${this.props.user.id}.png`;
    return(
      <div>
      <span>{this.props.user.name}</span>
      <img src={avatarImg} />
      </div>
    );
  };
});

var user = {
  id: 10,
  name: "Hoge"
};

// <Avatar user={user} />
```

## Prop is IF

Prop is transfer value for component, so you can change Prop.
If you want to update, should use state

## PropTypes

When you want to validate, use PropTypes to do it.
React.PropTypes exports a range of validators that can be used to make sure the data you receive is valid.

```js
var Avatar = React.createClass({
  propTypes: {
    name:   React.PropTypes.string.isRequired,
    id:     React.PropTypes.number.isRequired,
    width:  React.PropTypes.number.isRequired,
    height: React.PropTypes.number.isRequired,
    alt:    React.PropTypes.string
  },
  render() {
    var src = `/img/avatar/${this.props.id}.png`;
    return (
      <div>
      <img src={src} width={this.props.width} height={this.props.height} alt={this.props.alt} />
      <span>{this.props.name}</span>
      </div>
    );
  }
});

<Avatar name="foo" width={100} height={100} />
```

Note (for current React Version)

- Production environment: no check validation
- Development environment: it only output console.warn not error

## Default Prop Values

React lets you define default values for your props in a very declarative way:

```js

var Hello = React.createClass({
  getDefaultProps() {
    return {
      name: "React"
    };  
  },
  render() {
    return <div>Hello {this.props.name}</div>
  }
});

// <Hello />
```

## setProps & replaceProps

You may want to signal a change to a React component rendered with React.render(), you can also call setProps() to change its properties and trigger a re-render.
In addition, you can supply an optional callback function that is executed once setProps is completed and the component is re-rendered.

```js
<script type="text/jsx">

var Avatar = React.createClass({
  propTypes: {
    name: React.PropTypes.string.isRequired,
    width: React.PropTypes.number.isRequired,
    height: React.PropTypes.number.isRequired
  },
  render: function() {
    var src='/img/avatar/1.png';
    return (
      <div>
      <img src={src} width={this.props.width} height={this.props.height} alt="alt" />
      <span>{this.props.name}</span>
      </div>
    );
  }

});

var component = React.render(<Avatar name="Foo" width="100" height={100}/>, document.getElementById("app"));

component.setProps({name: "Bar"}, function(){
  console.log("Changed name from Foo to Bar");
});

component.replaceProps({name: "Foo-Bar"}, function(){
  console.log("Replaced name from Bar to Foo-Bar")
});

</script>
```

replaceProps like setProps but deletes any pre-existing props instead of merging the two objects.
Above example will output console.warn when execute ```component.replaceProps```

```
Warning: Required prop `width` was not specified in `Avatar`.
Warning: Required prop `height` was not specified in `Avatar`.
```

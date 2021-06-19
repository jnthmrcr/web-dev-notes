React uses and extention of JavaScript called JSX

because JSX is a syntactic extension of JavaScript, you can actually write JavaScript directly within JSX. To do this, you simply include the code you want to be treated as JavaScript within curly braces: `{ 'this is treated as JavaScript code' }`.

However, because JSX is not valid JavaScript, JSX code must be compiled into JavaScript. The transpiler Babel is a popular tool for this process.

`ReactDOM.render(JSX, document.getElementById('root'))` This function call is what places your JSX into React's own lightweight representation of the DOM. React then uses snapshots of its own DOM to optimize updating only specific parts of the actual DOM.

JSX must return a single element.

Valid JSX:
```jsx
<div>
  <p>Paragraph One</p>
  <p>Paragraph Two</p>
  <p>Paragraph Three</p>
</div>
```
Invalid JSX:
```jsx
<p>Paragraph One</p>
<p>Paragraph Two</p>
<p>Paragraph Three</p>
```
When rendering multiple elements like this, you can wrap them all in parentheses, but it's not strictly required.

# comments
To put comments inside JSX, you use the syntax `{/* */}` to wrap around the comment text.

# ReactDOM
With React, we can render JSX directly to the HTML DOM using React's rendering API known as ReactDOM

ReactDOM offers a simple method to render React elements to the DOM which looks like this: `ReactDOM.render(componentToRender, targetNode)`, where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.

As you would expect, `ReactDOM.render()` must be called after the JSX element declarations, just like how you must declare variables before using them.
```jsx
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
ReactDOM.render(JSX, document.getElementById('challenge-node'));
```
# HTML vs JSX
## HTML class in jsx
class is className in jsx
all attributes in jsx are camelCase
```jsx
const JSX = (
  <div className="myDiv">
    <h1>Add a class to this div</h1>
  </div>
);
```
## self closing JSX Tags
Any JSX element can be written with a self-closing tag, and every element must be closed. The line-break tag, for example, must always be written as `<br />` in order to be valid JSX that can be transpiled. A `<div>`, on the other hand, can be written as `<div />` or `<div></div>`. The difference is that in the first syntax version there is no way to include anything in the `<div />`

# Components

Components are the core of React. Everything in React is a component and here you will learn how to create one.

There are two ways to create a React component:

## JS function

The first way is to use a JavaScript function. Defining a component in this way creates a stateless functional component.

a stateless component is one that can receive data and render it, but does not manage or track changes to that data.

To create a component with a function, you simply write a JavaScript function that returns either JSX or null. One important thing to note is that React requires your function name to begin with a capital letter. 
```jsx
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```
## ES6 Class

The other way to define a React component is with the ES6 `class` syntax. In the following example, `Kitten` extends `React.Component`:
```jsx
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```
`Kitten` class now has access to many useful React features, such as local state and lifecycle hooks.

Also notice the `Kitten` class has a `constructor` defined within it that calls `super()`. It uses `super()` to call the constructor of the parent class, in this case `React.Component`. The constructor is a special method used during the initialization of objects that are created with the `class` keyword. It is best practice to call a component's constructor with `super`, and pass `props` to both. This makes sure the component is initialized properly.

# Creating Components with Composition

Imagine you are building an app and have created three components: a `Navbar`, `Dashboard`, and `Footer`

To compose these components together, you could create an `App` parent component which renders each of these three components as children. To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. For example, in the `render` method you could write:
```jsx
return (
 <App>
  <Navbar />
  <Dashboard />
  <Footer />
 </App>
)
```
When React encounters a custom HTML tag that references another component (a component name wrapped in < /> like in this example), it renders the markup for that component in the location of the tag.

can nest stuff within stuff
```jsx
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
      <TypesOfFruit />
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
      </div>
    );
  }
};
```

`class` components are nested the same as regular function components

# Render a Class Component to the DOM
its similar to vanilla jsx
```jsx
///in jsx
ReactDOM.render(componentToRender, targetNode)
```
> The first argument is the React component that you want to render. The second argument is the DOM node that you want to render that component within.

However, for React components, you need to use the same syntax as if you were rendering a nested component, for example
```jsx
/// componets
ReactDOM.render(<ComponentToRender />, targetNode)
```
You use this syntax for both ES6 class components and functional components

``` jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>My First React Component!</h1>
      </div>
    )
  }
}

ReactDOM.render(<MyComponent />, document.getElementById("challenge-node"))
```

# Pass Props to a Stateless Functional Component

In React, you can pass props, or properties, to child components. Say you have an `App` component which renders a child component called `Welcome` which is a stateless functional component. You can pass `Welcome` a `user` property by writing:
```jsx
<App>
  <Welcome user='Mark' />
</App>
```
In this case, the created property `user` is passed to the component `Welcome`. Since `Welcome` is a stateless functional component, it has access to this value like so:
``` jsx
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```
It is standard to call this value `props` and when dealing with stateless functional components, you basically consider it as an argument to a function which returns JSX. You can access the value of the argument in the function body. With class components, you will see this is a little different.

# pass an Array as Props

To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.
```jsx
<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

Array methods such as `join()` can be used when accessing the property.
```jsx
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```
This will join all colors array items into a comma separated string and produce: `<p>green, blue, red</p>`
```jsx
const List = (props) => {
  return <p>{props.tasks.join(', ')}</p>
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        <List tasks={["nap", "clothes"]}/>
        <h2>Tomorrow</h2>
        <List tasks={["eat", "sleep", "tv"]}/>
      </div>
    );
  }
};
```

# Default Props

ou can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if no value is explicitly provided. For example, if you declare 
```jsx
MyComponent.defaultProps = { location: 'San Francisco' }
```
you have defined a location prop that's set to the string `San Francisco`, unless you specify otherwise. React assigns default props if props are undefined, but if you pass `null` as the value for a prop, it will remain `null`

# override default props

you can override default props :/
> numbers must be wrapped in braces
```jsx
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity = {10}/>
  }
};
```

# PropTypes to Define the Props You Expect

React provides useful type-checking features to verify that components receive props of the correct type.

You can set `propTypes` on your component to require the data to be of a specific type. This will throw a useful warning when the data is of any other type.

set `propTypes` when you know the type of a prop ahead of time. You can define a `propTypes` property for a component in the same way you defined `defaultProps`. Doing this will check that props of a given key are present with a given type. Here's an example to require the type `function` for a prop called `handleClick`:
```jsx
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```

In the example above, the `PropTypes.func` part checks that `handleClick` is a function. Adding `isRequired` tells React that `handleClick` is a required property for that component. You will see a warning if that prop isn't provided. Also notice that `func` represents `function`. Among the seven JavaScript primitive types, function and `boolean` (written as `bool`) are the only two that use unusual spelling. In addition to. the primitive types, there are other types available. For example, you can check that a prop is a React element

Note: As of React v15.5.0, `PropTypes` is imported independently from React, like this: 
```jsx
import PropTypes from 'prop-types';
```

# this.props

The ES6 class component uses a slightly different convention to access props.

Anytime you refer to a class component within itself, you use the `this` keyword.

For example, if an ES6 class component has a prop called `data`, you write `{this.props.data}` in JSX.

```jsx
class ReturnTempPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            <p>Your temporary password is: <strong>{this.props.tempPassword}</strong></p>
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
          <h2>Reset Password</h2>
          <h3>We've generated a new temporary password for you.</h3>
          <h3>Please reset this password from your account settings ASAP.</h3>
          <ReturnTempPassword tempPassword = "ur mom dad"/>
        </div>
    );
  }
};
```

- A *stateless functional component* is any function you write which accepts props and returns JSX

- A *stateless component*, on the other hand, is a class that extends `React.Component`, but does not use internal state

- a *stateful component* is a class component that does maintain its own internal state. You may see stateful components referred to simply as components or React components.

A common pattern is to try to minimize statefulness and to create stateless functional components wherever possible. makes stuff simpler.

```jsx
class CampSite extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Camper/>
      </div>
    );
  }
};

const Camper = (props) => {
  return <p>{props.name}</p>;
}

Camper.defaultProps = {
  name: 'CamperBot'
}

Camper.propTypes = {
  name: PropTypes.string.isRequired
}
```

# Stateful Component
`state` consists of any data your application needs to know about, that can change over time. You want your apps to respond to state changes and present an updated UI when necessary

You create state in a React component by declaring a `state` property on the component class in its `constructor` This initializes the component with state when it is created. The state property must be set to a JavaScript object
```jsx
this.state = {
}
```

you must create a class component by extending `React.Component` in order to create `state` like this
```jsx
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'jenith'
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

# Render State in the User Interface

If a component is stateful, it will always have access to the data in `state` in its `render()` method. You can access the data with `this.state`

`state` allows you to track important data in your app and render a UI in response to changes in this data. If your data changes, your UI will change. React uses what is called a virtual DOM, to keep track of changes behind the scenes. When state data updates, it triggers a re-render of the components using that data - including child components that received the data as a prop. React updates the actual DOM, but only where necessary. This means syou don't have to worry about changing the DOM. You simply declare what the UI should look like.

you can also access `state` before the return statement
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    const name = this.state.name;
    return (
      <div>
          <h1>{name}</h1>
      </div>
    );
  }
};
```

# this.setState

React provides a method for updating component state called setState. You call the setState method within your component class like so: this.setState(), passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data.
```jsx
this.setState({ username: 'Lewis' });
```

React expects you to never modify state directly, instead always use `this.setState()` when state changes occur.

Also, you should note that React may batch multiple state updates in order to improve performance. What this means is that state updates through the setState method can be asynchronous. There is an alternative syntax for the setState method which provides a way around this problem.
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({name:"React Rocks"})
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

# bind `this` to method class

A class method typically needs to use the this keyword so it can access properties on the class (such as state and props) inside the scope of the method. There are a few ways to allow your class methods to access this.

One common way is to explicitly bind this in the constructor so this becomes bound to the class methods when the component is initialized. You may have noticed the last challenge used `this.handleClick = this.handleClick.bind(this)` for its handleClick method in the constructor. Then, when you call a function like `this.setState()` within your class method, this refers to the class and will not be undefined

dont do this
```jsx
this.setState({
  counter: this.state.counter + this.props.increment
});
```
state updates may be asynchronous - this means React may batch multiple `setState()` calls into a single update. can't rely on `this.state` SO: pass `setState()` a function which accesses state and props:
```jsx
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
or this
```jsx
this.setState(state => ({
  counter: state.counter + 1
}));
```
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
    this.toggleVisibility = this.toggleVisibility.bind(this);
  }
  toggleVisibility() {
    this.setState(state => ({visibility: !state.visibility}));
  }
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
}
```
# simple counter
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
    this.reset = this.reset.bind(this);
  }
  increment() {
    this.setState(state => ({count: state.count + 1}));
  }
  decrement() {
    this.setState(state => ({count: state.count - 1}));
  }
  reset() {
    this.setState(state => ({count: 0}));
  }
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```


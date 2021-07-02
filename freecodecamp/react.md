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

# controlled input

```jsx
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    // Change code below this line
    this.handleChange = this.handleChange.bind(this);
    // Change code above this line
  }
  // Change code below this line
  handleChange(event) {
    this.setState({input: event.target.value});
  }
  // Change code above this line
  render() {
    return (
      <div>
        { /* Change code below this line */}
        <input value={this.state.input} onChange={this.handleChange} />
        { /* Change code above this line */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

# controlled form
```jsx
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    // Change code below this line
    event.preventDefault()
    this.setState({submit: this.state.input });
    // Change code above this line
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          {/* Change code below this line */}
          <input value={this.state.input} onChange = {this.handleChange}/>
          {/* Change code above this line */}
          <button type='submit'>Submit!</button>
        </form>
        {/* Change code below this line */}
        <h1>{this.state.submit}</h1>
        {/* Change code above this line */}
      </div>
    );
  }
}
```

# Pass State as Props to Child Components
you can pass state info to children via the children's props. yeah idk. makes sense?

This pattern illustrates some important paradigms in React. The first is unidirectional data flow. State flows in one direction down the tree of your application's components, from the stateful parent component to child components. The child components only receive the state data they need.
# Pass a Callback as Props

You can also pass handler functions or any method that's defined on a React component to a child component.
This is how you allow child components to interact with their parent components.
```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        { /* Change code below this line */ }
        <GetInput input={this.state.inputValue} handleChange={this.handleChange}/>
        <RenderInput input={this.state.inputValue}/>
        { /* Change code above this line */ }
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```

# Lifecycle Methods

lifecycle methods, or lifecycle hooks, and allow you to catch components at certain points in time. This can be before they are rendered, before they update, before they receive props, before they unmount, and so on. Here is a list of some of the main lifecycle methods: 

## ```componentWillMount()```
called before the render() method when a component is being mounted to the DOM
will be deprecated in a future version of 16.X and removed in version 17

## ```componentDidMount()```
The best practice with React is to place API calls or any calls to your server in this lifecycle method. This method is called after a component is mounted to the DOM. Any calls to `setState()` here will trigger a re-rendering of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

The `componentDidMount()` method is also the best place to attach any event listeners you need to add for specific functionality. React provides a synthetic event system which behaves exactly the same regardless of the user's browser - even if the native events may behave differently between different browsers.

React's synthetic event system is great to use for most interactions you'll manage on DOM elements. However, if you want to attach an event handler to the document or window objects, you have to do this directly.
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }
  // Change code below this line
  componentDidMount() {
    document.addEventListener("keydown", this.handleKeyPress)
  }
  componentWillUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress)
  }
  // Change code above this line
  handleEnter() {
    this.setState((state) => ({
      message: state.message + 'You pressed the enter key! '
    }));
  }
  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```
## ```shouldComponentUpdate()```
a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not (instead of automatically upon state or prop change) it takes `nextProps` and `nextState` as parameters. This method is a useful way to optimize performance. You can compare the current props (`this.props`) to the next props (`nextProps`) to determine if you need to update or not, and return true or false accordingly.
```jsx
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    // Change code below this line
    return (parseInt(nextProps.value) % 2) == 0;
    // Change code above this line
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>;
  }
}

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState(state => ({
      value: state.value + 1
    }));
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value} />
      </div>
    );
  }
}
```
## ```componentDidUpdate()```

## ```componentWillUnmount()```


# Inline Styles
JSX elements use the `style` attribute, but because of the way JSX is transpiled, you can't set the value to a `string`. Instead, you set it equal to a JavaScript `object`:
```jsx
<div style={{color: "yellow", fontSize: 16}}>Mellow Yellow</div>
```
Notice how we camelCase the fontSize property? This is because React will not accept kebab-case keys in the style object. React will apply the correct property name for us in the HTML.
```jsx
class Colorful extends React.Component {
  render() {
    return (
      <div style={{color: "red", fontSize: "72px"}}>Big Red</div>
    );
  }
};
```
All property value length units (like `height`, `width`, and `fontSize`) are assumed to be in `px` unless otherwise specified. If you want to use `em`, for example, you wrap the value and the units in quotes, like `{fontSize: "4em"}`. Other than the length values that default to `px`, all other property values should be wrapped in quotes.

If you have a large set of styles, you can assign a style object to a constant to keep your code organized.
```jsx
const styles = {
  color: "purple",
  fontSize: 40,
  border: "2px solid purple"
}
class Colorful extends React.Component {
  render() {
    return (
      <div style={styles}>Style Me!</div>
    );
  }
};
```
# Use Advanced JavaScript in React Render Method
You can also write JavaScript directly in your `render` methods, before the `return` statement, without inserting it inside of curly braces. This is because it is not yet within the JSX code. When you want to use a variable later in the JSX code inside the `return` statement, you place the variable name inside curly braces.
```jsx
const inputStyle = {
  width: 235,
  margin: 5
};

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    };
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt',
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      "Don't count on it",
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
    const answer = possibleAnswers[this.state.randomIndex]; // Change this line
    return (
      <div>
        <input
          type='text'
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle}
        />
        <br />
        <button onClick={this.ask}>Ask the Magic Eight Ball!</button>
        <br />
        <h3>Answer:</h3>
        <p>
          {/* Change code below this line */}
          {answer}
          {/* Change code above this line */}
        </p>
      </div>
    );
  }
}
```

# Conditional (if else) with JSX
## &&
```{condition && <p>markup</p>}```
If the `condition` is `true`, the markup will be returned. If the condition is `false`, the operation will immediately return `false` after evaluating the condition and return nothing.

``` jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState(state => ({
      display: !state.display
    }));
  }
  render() {
    // Change code below this line
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display && <h1>Displayed!</h1>}
       </div>
    );
  }
};
```

## ?: (ternary)
Ternary expressions can be an excellent alternative if you want to implement conditional logic within your JSX.
```jsx
const inputStyle = {
  width: 235,
  margin: 5
};

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      userAge: ''
    }
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: ''
    });
  }
  submit() {
    this.setState(state => ({
      userAge: state.input
    }));
  }
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type='number'
          value={this.state.input}
          onChange={this.handleChange}
        />
        <br />
        {(this.state.userAge == "")?buttonOne:(this.state.userAge < 18)?buttonThree:buttonTwo}
      </div>
    );
  }
}
```
# Render Conditionally from Props
```jsx
class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    {/* Change code below this line */}
    return <h1>{this.props.fiftyFifty?"You Win!":"You Lose!"}</h1>;
    {/* Change code above this line */}
  }
}

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState(prevState => {
      // Complete the return statement:
      return {
        counter: prevState.counter + 1
      }
    });
  }
  render() {
    const expression = Math.random() >= 0.5; // Change this line
    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        {/* Change code below this line */}
        <Results fiftyFifty={expression}/>
        {/* Change code above this line */}
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
}
```
can modify css directy via react css objects yeah
```jsx
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ input: event.target.value })
  }
  render() {
    let inputStyle = {
      border: '1px solid black'
    };
    if (this.state.input.length > 15) {
      inputStyle = {
        border: '3px solid red'
      }
    }
    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange} />
      </div>
    );
  }
};
```
# map() with jsx idk
```jsx
const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    // Change code below this line
    this.state = {
      userInput: '',
      toDoList: []
    }
    // Change code above this line
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleSubmit() {
    const itemsArray = this.state.userInput.split(',');
    this.setState({
      toDoList: itemsArray
    });
  }
  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }
  render() {
    const items = this.state.toDoList.map(x => <li>{x}</li>)
    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder='Separate Items With Commas'
        />
        <br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>{items}</ul>
      </div>
    );
  }
}
```
# Give Sibling Elements a Unique Key Attribute
When you create an array of elements, each one needs a key attribute set to a unique value.
Keys only need to be unique between sibling elements, they don't need to be globally unique in your application.
```jsx
const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  const renderFrameworks = frontEndFrameworks.map(x => <li key={x}>{x}</li>)
  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
};
```
> avoid using the index idk

# using filter with jsx

# Render React on the Server with renderToString
Since React is a JavaScript view library and you can run JavaScript on the server with Node, you can render a React component on the server. React provides a `renderToString()` method you can use for this purpose.

sending rendered html helps with search engines and keeps size down and initial load speed up.
```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div/>
  }
};

// Change code below this line
ReactDOMServer.renderToString(<App/>);
```
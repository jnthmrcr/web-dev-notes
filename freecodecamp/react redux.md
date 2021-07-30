`React` is a view library that you provide with data, then it renders the view in an efficient, predictable way.

`Redux` is a state management framework that you can use to simplify the management of your application's state.

Typically, in a `React Redux` app, you create a single `Redux store` that manages the state of your entire app. Your `React` components subscribe to only the pieces of data in the store that are relevant to their role. Then, you dispatch actions directly from `React components`, which then trigger `store` updates.

Although `React components` can manage their own state locally, when you have a complex app, it's generally better to keep the app state in a single location with `Redux`. There are exceptions when individual components may have local state specific only to them. Finally, because `Redux` is not designed to work with `React` out of the box, you need to use the `react-redux` package. It provides a way for you to pass `Redux` state and dispatch to your `React components` as `props`.

we gon make a simple React component which allows you to input new text messages.

# React Component:
```js
class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({input: event.target.value});
  }
  submitMessage(event) {
    this.setState(
      {
        input: '',
        messages: this.state.messages.concat(this.state.input)
      }
    );
  }

  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input value={this.state.input} onChange={this.handleChange}></input>
        <button onClick={this.submitMessage}>Submit Message</button>
        <ul>
			{this.state.messages.map((x,i) => {
			return <li key={i}>{x}</li>
			})}
        </ul>
      </div>
    );
  }
};
```
# Redux store
```js
// Define ADD, addMessage(), messageReducer(), and store here:
const ADD = 'ADD'

function addMessage(message) {
  return {type: ADD, message}
}

function messageReducer(state = [], action) {
  if (action.type === ADD) {
    return state.concat(action.message);
  }
  return state;
}

const store = Redux.createStore(messageReducer);
```

# Use Provider to Connect Redux to React
`React Redux` provides a small API with two key features: `Provider` and `connect`.

The `Provider` is a wrapper component from `React Redux` that wraps your `React app`. This wrapper then allows you to access the Redux `store` and `dispatch` functions throughout your component tree. `Provider` takes two props, the Redux store and the child components of your app. Defining the `Provider` for an App component might look like this:
```js
<Provider store={store}>
  <App/>
</Provider>
```
heres the last couple things combined within `React.Provider`
```js
  // Redux Code:
  const ADD = 'ADD';

  const addMessage = (message) => {
    return {
      type: ADD,
      message
    }
  };

  const messageReducer = (state = [], action) => {
    switch (action.type) {
      case ADD:
        return [
          ...state,
          action.message
        ];
      default:
        return state;
    }
  };

  const store = Redux.createStore(messageReducer);

  // React Code:
  class DisplayMessages extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        input: '',
        messages: []
      }
      this.handleChange = this.handleChange.bind(this);
      this.submitMessage = this.submitMessage.bind(this);
    }
    handleChange(event) {
      this.setState({
        input: event.target.value
      });
    }
    submitMessage() {
      const currentMessage = this.state.input;
      this.setState({
        input: '',
        messages: this.state.messages.concat(currentMessage)
      });
    }
    render() {
      return (
        <div>
          <h2>Type in a new Message:</h2>
          <input
            value={this.state.input}
            onChange={this.handleChange}/><br/>
          <button onClick={this.submitMessage}>Submit</button>
          <ul>
            {this.state.messages.map( (message, idx) => {
                return (
                   <li key={idx}>{message}</li>
                )
              })
            }
          </ul>
        </div>
      );
    }
  };

  const Provider = ReactRedux.Provider;

  class AppWrapper extends React.Component {
    // Below is the code required to pass the test
    render() {
      return (
        <Provider store={store}>
          <DisplayMessages />
        </Provider>
      );
    }
    // Above is the code required to pass the test
  };
```

# Map State to Props
>observe state from react component

The `Provider` component allows you to provide `state` and `dispatch` to your React components, but you must specify exactly what state and actions you want. This way, you make sure that each component only has access to the state it needs. You accomplish this by creating two functions: `mapStateToProps()` and `mapDispatchToProps()`.

In these functions, you declare what pieces of state you want to have access to and which action creators you need to be able to dispatch. Once these functions are in place, you'll see how to use the React Redux `connect` method to connect them to your components in another challenge.

Note: Behind the scenes, React Redux uses the `store.subscribe()` method to implement `mapStateToProps()`.
```js
const state = [];

const mapStateToProps = (state) => {
  return {messages: state}
}
```

# Map Dispatch to Props
>change state from react component

The `mapDispatchToProps()` function is used to provide specific action creators to your React components so they can dispatch actions against the Redux store. It's similar in structure to the `mapStateToProps()` function you wrote in the last challenge. It returns an object that maps dispatch actions to property names, which become component `props`. However, instead of returning a piece of `state`, each property returns a function that calls `dispatch` with an action creator and any relevant action data. You have access to this `dispatch` because it's passed in to `mapDispatchToProps()` as a parameter when you define the function, just like you passed `state` to `mapStateToProps()`. Behind the scenes, React Redux is using Redux's `store.dispatch()` to conduct these dispatches with `mapDispatchToProps()`. This is similar to how it uses `store.subscribe()` for components that are mapped to `state`.

For example, you have a `loginUser()` action creator that takes a `username` as an action payload. The object returned from `mapDispatchToProps()` for this action creator would look something like:
```js
{
  submitLoginUser: function(username) {
    dispatch(loginUser(username));
  }
}
```

```js
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

const mapDispatchToProps = (dispatch) => {
  return {submitNewMessage: (message) =>
    dispatch(addMessage(message))
  };
}
```
# Connect Redux to React
Now that you've written both the `mapStateToProps()` and the `mapDispatchToProps()` functions, you can use them to map `state` and `dispatch` to the `props` of one of your React components. The `connect` method from React Redux can handle this task. This method takes two optional arguments, `mapStateToProps()` and `mapDispatchToProps()`. They are optional because you may have a component that only needs access to `state` but doesn't need to dispatch any actions, or vice versa.

To use this method, pass in the functions as arguments, and immediately call the result with your component. This syntax is a little unusual and looks like:
```
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```
>god i barely understand what any of these words mean

Note: If you want to omit one of the arguments to the `connect` method, you pass `null` in its place.
```js
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

const mapStateToProps = (state) => {
  return {
    messages: state
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message));
    }
  }
};

class Presentational extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h3>This is a Presentational Component</h3>
  }
};

const connect = ReactRedux.connect;
// Change code below this line
const ConnectedComponent = connect(mapStateToProps, mapDispatchToProps)(Presentational)
```
# Connect Redux to the Messages App

`Presentational` *generally* refers to React components that are not directly connected to Redux. They are simply responsible for the presentation of UI and do this as a function of the props they receive. By contrast, container components are connected to Redux. These are typically responsible for dispatching actions to the store and often pass store state to child components as props.

```js
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    this.setState((state) => {
      const currentMessage = state.input;
      return {
        input: '',
        messages: state.messages.concat(currentMessage)
      };
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.state.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

// React-Redux:
const mapStateToProps = (state) => {
  return { messages: state }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (newMessage) => {
       dispatch(addMessage(newMessage))
    }
  }
};

const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

// Define the Container component here:
const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational)

class AppWrapper extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    // Complete the return statement:
    return (
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};
```

# Extract Local State into Redux
You're almost done! Recall that you wrote all the Redux code so that Redux could control the state management of your React messages app. Now that Redux is connected, you need to extract the state management out of the `Presentational` component and into Redux. Currently, you have Redux connected, but you are handling the state locally within the `Presentational` component.
>i thought thats what container did!!! wtf does container do?!??!
```js
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

// Change code below this line
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      // messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
	//submitNewMessage() exposed in props cause we connect()'d it
    this.props.submitNewMessage(this.state.input);
    this.setState((state) => ({
      input: '',
      // messages: state.messages.concat(state.input)
    }));
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
		{/props not this.state/} 
          {this.props.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};
// Change code above this line

const mapStateToProps = (state) => {
  return {messages: state}
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message))
    }
  }
};

const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational);

class AppWrapper extends React.Component {
  render() {
    return (
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};
```
>okay. container *does* allow us to do that, we just weren't yet :/

# Moving Forward From Here
## aka the browser editor lied to you yada yada

```js
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider, connect } from 'react-redux'
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'

import rootReducer from './redux/reducers'
import App from './components/App'

const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

ReactDOM.render(
  <Provider store={store}>
    <App/>
  </Provider>,
  document.getElementById('root')
);


// Only change code below this line
console.log('Now I know React and Redux!');
console.log('as if...');
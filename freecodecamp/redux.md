# Create a Redux Store
Redux is a state management framework that can be used with a number of different web technologies, including React.

The Redux `store` is an object which holds and manages application `state`. All components' states are stored in this `store` object. Any time any piece of your app wants to update state, it must do so through the Redux store.

`createStore()` is used to create the Redux store. This method takes a `reducer` function as a required argument.
```js
const reducer = (state = 5) => {
  return state;
}
const store = Redux.createStore(reducer);
```
# Get State from the Redux Store
you can retrieve the current `state` held in the Redux store object with the `getState()` method
```js
const store = Redux.createStore(
  (state = 5) => state
);
const currentState = store.getState();
```
# redux actions
In Redux, all state updates are triggered by dispatching actions. An action is simply a JavaScript object that contains information about an action event that has occurred.

actions may contain data (such as usernames) but they must carry a `type` property that specifies the 'type' of action that occurred.

actions are just objects

```js
const action = {
  type: 'LOGIN'
}
```
# Action Creator

After creating an action, the next step is sending the action to the Redux store so it can update its state. In Redux, you define action creators to accomplish this. An action creator is simply a JavaScript function that returns an action. In other words, action creators create objects that represent action events.
```js
const action = {
  type: 'LOGIN'
}

function actionCreator() {
  return action;
}
```
# Dispatch an Action Event
`dispatch` method is what you use to dispatch actions to the Redux store. Calling `store.dispatch()` and passing the value returned from an action creator sends an action back to the store.

thus, these two are equivelant:
```js
store.dispatch(actionCreator()); // actionCreator returns action object
store.dispatch({ type: 'LOGIN' }); // action object
```
```js
const store = Redux.createStore(
  (state = {login: false}) => state
);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};

store.dispatch(loginAction());
```

# Handle an Action in the Store
`reducer` functions or Reducers in Redux are responsible for the state modifications that take place in response to actions. A `reducer` takes `state` and `action` as arguments, and it always returns a new `state` The reducer is simply a pure function that takes state and action, then returns new state. no api calls or anything weird

Another key principle in Redux is that `state` is read-only. In other words, the `reducer` function must always return a new copy of `state` and never modify state directly. Redux does not enforce state immutability, however, you are responsible for enforcing it in the code of your reducer functions. You'll practice this in later challenges.

> fuck this shit, if its immutable it should be immutable fuck you
```js
const defaultState = {
  login: false
};

const reducer = (state = defaultState, action) => {
  if (action.type == 'LOGIN') {
    return {
      login: true
    }
  }
  return state;
};

const store = Redux.createStore(reducer);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};
```

switch/case is a standard pattern for reducers
```js
const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {
  switch(action.type){
  case 'LOGIN':
    return {authenticated: true}
  case 'LOGOUT':
    return {authenticated: false}
  default:
    return state;
  }
};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: 'LOGIN'
  }
};

const logoutUser = () => {
  return {
    type: 'LOGOUT'
  }
};
```

# Use const for Action Types

A common practice when working with Redux is to assign action types as read-only constants, then reference these constants wherever they are used. You can refactor the code you're working with to write the action types as `const` declarations.
```js
const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {

  switch (action.type) {
    case LOGIN: 
      return {
        authenticated: true
      }
    case LOGOUT: 
      return {
        authenticated: false
      }
    default:
      return state;
  }
};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: LOGIN
  }
};

const logoutUser = () => {
  return {
    type: LOGOUT
  }
};
```

# Register a Store Listener

`store.subscribe()` allows you to subscribe listener functions to the store, which are called whenever an action is dispatched against the store. One simple use for this method is to subscribe a function to your store that simply logs a message every time an action is received and the store is updated.
```js
const ADD = 'ADD';

const reducer = (state = 0, action) => {
  switch(action.type) {
    case ADD:
      return state + 1;
    default:
      return state;
  }
};

const store = Redux.createStore(reducer);

let count = 0;

// Change code below this line
store.subscribe(() => {
  count ++;
})
// Change code above this line

store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
```

# Combine Multiple Reducers

all app state is held in a single state object in the store. Therefore, Redux provides reducer composition as a solution for a complex state model. You define multiple reducers to handle different pieces of your application's state, then compose these reducers together into one root reducer. The root reducer is then passed into the Redux `createStore()` method.

In order to let us combine multiple reducers together, Redux provides the `combineReducers()` method. This method accepts an object as an argument in which you define properties which associate keys to specific reducer functions. The name you give to the keys will be used by Redux as the name for the associated piece of state.

Typically, it is a good practice to create a reducer for each piece of application state when they are distinct or unique in some way. For example, in a note-taking app with user authentication, one reducer could handle authentication while another handles the text and notes that the user is submitting. For such an application, we might write the `combineReducers()` method like this:
```js
const rootReducer = Redux.combineReducers({
  auth: authenticationReducer,
  notes: notesReducer
});
```

Now, the key `notes` will contain all of the state associated with our notes and handled by our `notesReducer`. This is how multiple reducers can be composed to manage more complex application state. In this example, the state held in the Redux store would then be a single object containing auth and `notes` properties.
```js
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};

const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const authReducer = (state = {authenticated: false}, action) => {
  switch(action.type) {
    case LOGIN:
      return {
        authenticated: true
      }
    case LOGOUT:
      return {
        authenticated: false
      }
    default:
      return state;
  }
};

const rootReducer = Redux.combineReducers({
  count: counterReducer,
  auth: authReducer
});

const store = Redux.createStore(rootReducer);
```


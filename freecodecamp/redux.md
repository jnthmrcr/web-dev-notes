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
    
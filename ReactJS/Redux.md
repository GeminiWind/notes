# Redux

## Data flow in Redux

The typical Redux flow is as follows:

1.  A user interacts with the View to trigger a state update
2.  When a state update is required, the View dispatches an action
3.  The reducers receive the action from the dispatch and updates the state in the Store according to what is described by the action
4.  The View is subscribed to the Store to listen for state changes. The changes are notified via the subscription methods and the View updates its UI accordingly
![[data-flow-in-redux.png]]

## Implementation
- Configure store

```js
const ADD_TO_DO = "ADD_TO_DO";

// A list of strings representing tasks to do:
const todos = [
  "Go to the store",
  "Clean the house",
  "Cook dinner",
  "Learn to code"
];


// reducer
const immutableReducer = (state = todos, action) => {
  switch (action.type) {
    case ADD_TO_DO:
      // don't mutate state here

      return state.concat(action.todo);
    // or return [...state, action.todo]

    default:
      return state;
  }
};

// dispatcher
const addToDo = todo => {
  return {
    type: ADD_TO_DO,
    todo
  };
};

const store = Redux.createStore(immutableReducer);
```

**Best practices**
- Use *selector* to prevent uncessary re-render when the value of store is changed
- In case of needing to store various kind of information, you can split reducer by domain in your store like `postReducer` for `post`, `userReducer` for `user`, then use `combineReducer` to merge them
- Use redux-persist if you need to persist your store
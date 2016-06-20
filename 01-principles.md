# Principles

## Principle #1
**Always represent the whole state of your app as a single javascript Object or State (State Tree).**

## Principle #2
**All State Trees in Redux is redundant. You cannot modify or add to it.  Only way to change the state is by dispatching an action.**

Action is a plain javascript object that describes the change.  Action is the minimal representation of the change in the data.  **Actions has to have a `type` property**

```javascript
{
   type: "INCREMENT"
}
```

Originating Component dispatches the action (when someone clicks a button for example)

## Pure Functions
Functions are pure if the output solely depends on the inputs.  Pure functions have no side-effects.  **Many functions in Redux are pure functions.**

## Principle #3
**To describe state mutations, you have to write a function that takes the previous state of the app, and the action dispatched, and returns the next state of the app.  This function has to be pure.  The function is called a Reducer**

State mutations that needs to be pure functions.  The function needs to take the current state and the action dispatched and return a new state.  It has to be pure so it has to return a new state object.

## Undefined State
**If the state that is passed into the reducer is `undefined`, the reducer should return the initial state of the app.**

```javascript
const counter = (state = 0, action) => {
    switch (action.type) {
    	case 'INCREMENT':
    	  return state + 1;
    	case 'DECREMENT':
    	  return state - 1;
    	default:
    	  return state;
    }
}
```

## Store
The store binds all three principles of Redux together.  When creating a store, it takes in the reducer that specifies how the state will change.

```javascript
// previous counter function

import {createStore} from 'redux';

const store = createStore(counter);

console.log(store.getState());

store.dispatch({type: 'INCREMENT'});

const render = () => {
    document.body.innerText = store.getState();
};

store.subscribe(render);
render();

document.addEventListener('click', () => {
	store.dispatch({type: 'INCREMENT'});
});

```

### Recreating Store
```javascript

const createStore = (reducer) => {
   let state;
   let listeners = [];
   
   const getState = () => state;
   
   const dispatch = (action) => {
       state = reducer(state, action);
       listeners.forEach(listener => listener());
   };
   
   const subscribe = (listener) => {
       listeners.push(listener);
       return () => {
           listeners = listeners.filter(l => l !== listener);
       };
   };
   
   dispatch({}); // get the reducer to return the initial state;
   
   return { getState, dispatch, subscribe };
}

```

### Don't Mutate your arrays
#### Concate an array
*don't use `push` on array*  

`[...arr, 0]` or `arr.concat(0)` to return a new array with an added `0` at the end.

#### Remove Item from array at given index
*don't use `splice` on array*  

`[...arr.slice(0,index), ...list.slice(index + 1)]` or `arr.slice(0, index).concat(arr.slice(index+1))`

#### Change Item from array at given index
*don't just replace the value in array*

`[...arr.slice(0,index), arr[index] + 1 , ...arr.slice(index+1)]`

### Don't Mutate your objects
#### Change a Property Value

```javascript
Object.assign({}, todo, { // first param is the target object to be mutated
	completed: !todo.completed;
});
```

OR

```javascript
{
   ...todo,
   completed: !todo.completed
}
```

### Reducer Composition
Different reducers specifiy different parts of the state tree based on different actions.  Reducers are pure functions so other reducers can call other reducers.

there can be a top-level reducers that calls other reducers which are values of the properties of the top state tree object.

### `combineReducers`
generates the top-level reducer.

```javascript
const todoApp = combineReducer({
    todos,  //the name of the property in the State, and the name of the reducer that handles todos
    visibilityFilter
});
```

#### Creating `combineReducer` from scratch
```javascript
const combineReducers = (reducers) => {
	return (state = {}, action) {
		return Object.keys(reducers).reduce(
			(nextState, key) => {
			    nextState[key] = reducers[key](
			        state[key],
			        action
			    );
			    return nextState;
			},
			{}
		);
	};
};
```

### Extracting Presentational Components
**Presentational components are ones that do not determine its own behavior**

### Extracting Container Components
**container components decouples its component from its parent components saving them from passing the required props down to the components that needs them**

* First separate the components into presentational components
* If it get too complex, then refactor the components to have a container component that handles the behavior and the data

## Store and Props
### Explicitly
**Every components has to have the `store` as a prop**

### Implicity using `context`
```javascript
class Provider extends Component() {
    getChildContext() {
    	return {
    		store: this.props.store
    	};
    }
    
    render() {
    	return this.props.children;
    }
}

```

Have to include:
```javascript
Provider.childContextTypes = {
    store: React.PropTypes.object
};

```

Have to declare what context to receive:
```javascript
VisibleTodoList.contextTypes = {
	store: React.PropTypes.object
};
```

## `reach-redux` library

### `Provider` component
```javascript	
import {Provider} from 'react-redux'

```

## Next
[Getting Started](02-getting-started.md)

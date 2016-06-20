# Create some components 
Let's create some components

## Create a `components` directory inside the `app` directory
* Create two directories named `App` and `Title` inside `components` directory
* Create two files named `index.js` for each newly created directories

it will look like:
```
app
└components
  ├App
  | └index.js
  └Title
    └index.js
```

## For `index.js` under `Title`
```js
import React, { Component } from 'react';
import styles from './styles.css';

class Title extends Component {
  render() {
    return (
      <h1 className={ styles.title } { ...this.props } />
    )
  }
}

export default Title;

```


## For `index.js` under `app/components/App`

```js
import React, { Component } from 'react';
import Title from '../Title';

class App extends Component {
  render() {
    return (
      <div>
        <Title>Hello World</Title>
      </div>)
  }
}

export default App;
```

### Note: Stateless components
While React since v13 supports Stateless components.  In order for Redux Hot Loading to work, it has to be a full React Component.

## For `index.js` under `app`

```js
import { createStore } from 'redux'
import appReducer from './reducers'
// Enable React and the newly created component
import React from 'react'    
import App from './components/App'
import { Provider } from 'react-redux'
import { render } from 'react-dom'

// From Before
let initialState = {
}

// From Before
let store = createStore(appReducer, initialState)

// Render the App with the store we created from before
render(
    <Provider store={store}>
        <App />
    </Provider>
    , document.getElementById('root'));
```

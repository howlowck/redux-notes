# React Router with Redux
Let's add some routes to our SPA

## Install React Router and React Router Redux Package

```bash
npm install --save-dev react-router react-router-redux
```

## Add some common React Router components
Create `components/NavLink/index.js`:

```jsx
import React from 'react'
import { Link } from 'react-router'

export default React.createClass({
  render() {
    return <Link {...this.props} activeClassName="active"/>
  }
})
```

## Change index.js

```jsx
import { Router, Route, hashHistory IndexRoute } from 'react-router'
import App from './modules/App'
import About from './modules/About'
import Repos from './modules/Repos'
import Repo from './modules/Repo'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      <IndexRoute component={Home}/>
      <Route path="/repos" component={Repos}>
        <Route path="/repos/:userName/:repoName" component={Repo}/>
      </Route>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

## Add some name for `components/App/index.js`

```html
<ul role="nav">
  <li><IndexLink to="/" activeClassName="active">Home</IndexLink></li>
  <li><NavLink to="/about">About</NavLink></li>
  <li><NavLink to="/repos">Repos</NavLink></li>
</ul>
```

## Add Redux Router in `index.js`

```js
import { syncHistoryWithStore, routerReducer } from 'react-router-redux'

// Add the reducer to your store on the `routing` key
const store = createStore(
  combineReducers({
    ...reducers,
    routing: routerReducer
  })
)

// Create an enhanced history that syncs navigation events with the store
const history = syncHistoryWithStore(browserHistory, store)

ReactDOM.render(
  <Provider store={store}>
    { /* Tell the Router to use our enhanced history */ }
    <Router history={history}>
      <Route path="/" component={App}>
        <Route path="foo" component={Foo}/>
        <Route path="bar" component={Bar}/>
      </Route>
    </Router>
  </Provider>,
  document.getElementById('mount')
)
```

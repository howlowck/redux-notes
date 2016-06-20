# Redux Chrome Plugin
Let's do some time travel!

## Install Redux Devtools Package
```bash
npm install --save-dev redux-devtools
```

## Enable Devtools
Inside `app/index.js`, add this to the `createStore` function
```js
let store = createStore(appReducer, initialState, window.devToolsExtension && window.devToolsExtension())
```

# Getting Started

## NPM packages absolutely necessary
Here are the npm packages needed just to start development

### React
```bash
npm install --save-dev react react-dom
```

### Redux
```bash
npm install --save-dev redux redux-react
```

### Asset Assembler
```bash
npm install --save-dev webpack
```

### Some processors
```bash
npm install --save-dev babel-loader babel-preset-es2015 babel-preset-react
```

### Enable Babel

create a `.babelrc` file in the root directory and put

```json
{
  "presets": ["es2015", "react"]
}
```

### Enable webpack
create a `webpack.config.js` and put

```js
var webpack = require('webpack');
var path = require('path');

var BUILD_DIR = path.resolve(__dirname, 'dist');
var APP_DIR = path.resolve(__dirname, 'app');

var config = {
    devtool: 'eval',
    entry: [
        './app/index.js'
    ],
    output: {
        path: BUILD_DIR,
        filename: 'bundle.js'
    },
    module : {
        loaders : [
            {
                test : /\.js$/,
                include : APP_DIR + '/',
                loader: 'babel'
            }
        ]
    },
    plugins: [
        new webpack.DefinePlugin({
            'process.env.NODE_ENV': '"production"'
        })
    ]
};

module.exports = config;
```

### Add Script to npm
add to `scripts` in `package.json`
```json
{
    "dev": "webpack -d --watch",
    "build": "webpack -p"
}
```

### Create a `index.html` and put
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div id="root">
    </div>
    <script src="/dist/bundle.js" type="text/javascript"></script>
  </body>
</html>
```

### Create a `app` folder and create a `index.js` in it, and put:
```javascript
import { createStore } from 'redux'
import appReducer from './reducers'

let initialState = {
}

let store = createStore(appReducer, initialState)
```

### Create a `reducers` folder inside the `app` folder, and create a `index.js` in it.
```javascript
const reducer = (action, state) => {
  return state
}

export default reducer
```

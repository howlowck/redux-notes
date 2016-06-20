# Getting more dev tools

## Create a quick server for development
```bash
npm install --save-dev webpack-dev-server
```

## Create a `server.js` and put
```js
var webpack = require('webpack');
var WebpackDevServer = require('webpack-dev-server');
var config = require('./webpack.config');

new WebpackDevServer(webpack(config))
  .listen(3000, '0.0.0.0', function (err, result) {
    if (err) {
        return console.log(err);
    }
    console.log('Listening at http://localhost:3000/');
});
```

## Add npm start script in `package.json`
```json
{
...
"start": "node server.js"
}
```

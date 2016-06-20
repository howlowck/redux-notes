# Component Hot Loading
Let's add some hot loading!!  Hot loading is different than live reloading which was popular in the past few years.  

The advantage of hot loading is even if you change the state of the app, when you change the code, it doesn't just simply refresh the browser.  The app stays put, and reflects the changes that you've made!!

## Add npm packages
```bash
npm install --save-dev react-hot-loader
```

## Add Config for hot loading to `server.js`
```js
new WebpackDevServer(webpack(config), { //add this object
    publicPath: config.output.publicPath,
    hot: true,
    historyApiFallback: true
});
```

## Add publicPath to `webpack.config.js` like so:
```js
...
output: {
        path: BUILD_DIR,
        filename: 'bundle.js',
        publicPath: '/static/' // Add this line
    }
...
```

## Also add two more entries under `entry` in `webpack.config.js` like so:
```js
entry: [
    'webpack-dev-server/client?http://0.0.0.0:3000', // add this line
    'webpack/hot/only-dev-server', // add this line
    './app/index.js'
]
```

## Add `react-hot` to js loader in `webpack.config.js`
```js
{
  test : /\.js$/,
  include : APP_DIR + '/',
  loader: 'react-hot!babel' // Add react-hot! to this line
}
```

## Add Hot Module Replace to `plugins` in `webpack.config.js`
```js
plugins: [
    new webpack.HotModuleReplacementPlugin(), // Add this line
    new webpack.DefinePlugin({
        'process.env.NODE_ENV': '"development"'
    })
]
```

## Change js directory in `index.html`
point the javascript to `/static/bundle.js`

## Now run `npm start` and change some styles.

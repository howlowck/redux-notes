# Enable CSS Modules
Let's add some styles!!

## Install CSS Modules
```bash
npm install --save-dev style-loader css-loader postcss-loader
```

## Add Css Loader to webpack
Under `module > loaders`, add the object:
```js
{
    test : /\.css$/,
    include : APP_DIR + '/',
    loader: 'style!css?module!postcss'
}
```

## Add a `styles.css` under `app/components/Title`, and put some css:

```css
.title {
  color: green;
}
```

## Import the css into Title Component in `app/components/Title/index.js`
This is amazing! you can import css like it's javascript code!

CSS Module sets the className to something unique, so you don't have to worry about undeterminist effects, common in CSS

```js
import styles from './styles.css';
function Title(props) {
  return (
    <h1 className={ styles.title } { ...props } />
...
```

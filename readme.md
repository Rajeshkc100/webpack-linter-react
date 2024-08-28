
# Setting Up a React App with Webpack and ESLint

## 1. Project Initialization

```bash
mkdir my-react-app
cd my-react-app
npm init -y
```

Install React and ReactDOM:

```bash
npm install react react-dom
```

## 2. Configuring Webpack

Install Webpack and related dependencies:

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server babel-loader @babel/core @babel/preset-env @babel/preset-react html-webpack-plugin
```

Create a `webpack.config.js` file in the root of your project directory with the following content:

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react']
          }
        }
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  devServer: {
    contentBase: path.join(__dirname, 'public'),
    compress: true,
    port: 8081
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html'
    })
  ]
};
```

## 3. Setting Up ESLint

Install ESLint and related plugins:

```bash
npm install --save-dev eslint eslint-plugin-jsx-a11y eslint-config-airbnb-base
```

Create an `.eslintrc.json` file in the root of your project directory with the following content:

```json
{
  "extends": [
    "airbnb-base",
    "plugin:jsx-a11y/recommended"
  ],
  "env": {
    "browser": true,
    "es2021": true
  },
  "parserOptions": {
    "ecmaVersion": 2021,
    "sourceType": "module"
  },
  "plugins": [
    "jsx-a11y"
  ],
  "rules": {
    "quotes": "off",
    "semi": ["error", "always"],
    "no-unused-vars": ["warn"],
    "linebreak-style": "off",
    "eol-last": "off"
  }
}
```

## 4. Running the Project

To start the development server and see your project in action, add the following script to your `package.json`:

```json
"scripts": {
  "start": "webpack-dev-server --config ./webpack.config.js"
}
```

Run the development server:

```bash
npm start
```

Your project should now be running at `http://localhost:8081/`.

## 5. Demo Code and Explanation

### `src/index.js`

Create a file named `index.js` inside the `src` directory with the following content:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

### `src/App.js`

Create a file named `App.js` inside the `src` directory with the following content:

```javascript
import React from 'react';

const App = () => (
  <div>
    <h1>Hello, React!</h1>
  </div>
);

export default App;
```

### `public/index.html`

Create an `index.html` file inside the `public` directory with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React App</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

## Explanation

- **Webpack Configuration (`webpack.config.js`)**: This file sets up Webpack to bundle your React application, including handling JavaScript (using Babel) and CSS files. The `HtmlWebpackPlugin` generates an HTML file that includes your bundled JavaScript.

- **ESLint Configuration (`.eslintrc.json`)**: This file configures ESLint to use the Airbnb style guide and the `jsx-a11y` plugin for accessibility checks. It also customizes some rules, such as disabling quotes enforcement and linebreak-style checks.

- **Demo Code**: The demo code includes a simple React component (`App`) and renders it to the DOM. The HTML file includes a root div where the React app is mounted.

For more details on Webpack and ESLint, refer to their official documentation:

- Webpack Documentation
- [ESLint Documentation](https://eslint.org/)

Happy coding!

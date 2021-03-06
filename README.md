# laravel-elixir-react-hmr

> Working demo : [laravel-elixir-react-hmr-demo](https://github.com/eumentis/laravel-elixir-react-hmr-demo)

*This is for development only. Should not be used on production servers.*

For one of my projects, I planned to use Laravel for backend and React for frontend. I decided to use Webpack for bundling all my JS files (to use features like [HMR](https://webpack.github.io/docs/hot-module-replacement.html
) and [React Hot Loader](https://github.com/gaearon/react-hot-loader) for development) and Laravel Elixir for all other assets (css, images, fonts, etc.). I also wanted to use BrowserSync for laravel livereloads and multi-device testing. Thus, I wanted to connect Webpack bundler with Laravel and serve it using BrowserSync. 

Jeffery Way has created official Webpack and BrowserSync extensions for Laravel. His Webpack extension does not support webpack-dev-server, HMR and React Hot Loader. Also there is no support for connecting the Webpack output to BrowserSync. I was not able to find any article or package that achieved this. Therefore I decided to develop a Laravel Elixir extension for it.

I am a self-learned programmer/developer and this is my first public package.

## Features
* Laravel 5+ backend server and React frontend
* Webpack for Javascript compilation and Laravel Elixir for all non-JS assets
* Multiple input JS files supported (for multi-page application)
* BrowserSync support (LiveReload non-JS assets, multi-device testing)
* ES6 and React compilation using Babel
* Webpack hot module replacement and hot loading of React components (React Hot Loader 3)

## Usage
At the moment, users cannot change or provide custom Webpack and BrowserSync configuration.

### Step 1 : Install
```bash
npm i -D laravel-elixir-react-hmr
```
### Step 2 : Setup
```javascript
// Add to gulpfile.js
require('laravel-elixir-react-hmr');
```
Use just like any other Laravel Elixir tasks [i.e. mix.taskName(options)]
```javascript
elixir(function(mix) {
    mix.react(options);
});
```
The config options are provided in the form of Javascript object.
#### Options
```javascript
// The values given below are the default values
{
    // The URL of your Laravel dev server
    proxy: 'homestead.app',
    
    // List of relative paths (w.r.t '/resources/assets/js') of the input Javascript files
    inputFiles: [
        './app.js'
    ],
    
    // The relative path (w.r.t '/public/js') of the bundled JS output folder
    // The output dir must always be inside the '/public' directory as the application is served from the '/public' dir
    outputDir: './',
    
    // OPTIONAL
    // IP address to use for BrowserSync external URL (used for multi-device access)
    //      Sometimes BrowserSync sets the wrong IP address and external URL doesn't work.
    host: ''
}
```

### Step 3 : Running
To start the BrowserSync server
```bash
gulp watch
```
Open `http://localhost:3000` in your browser to load the app.
*Does not work in IE*

## Notes
* Wrapper must be added to the root React component for hot reloading to work ([read details](https://github.com/gaearon/redux-devtools/commit/64f58b7010a1b2a71ad16716eb37ac1031f93915))
   * Have a look at `/resources/assets/js/app.js` in the demo : [laravel-elixir-react-hmr-demo](https://github.com/eumentis/laravel-elixir-react-hmr-demo)
   
* Changes to PHP files will reload the page and the React state would be lost.

## Future features
* Bundling JS for production
* Custom Webpack config
* Custom BrowserSync config


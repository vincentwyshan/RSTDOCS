=======================================
Introduction to reactjs programing
=======================================

.. Contents::
    :depth: 3


Background knowledge
==========================

You must have knowledges as below:

#. javascript
#. html
#. css

Since 2015, ES6 was geting popular, usually we are writing
react.js in ES6 syntax, and it's great helpful to write high
quality source code. So it's better to have knowledge of ES6.

If you don't know much about ES6, at least you must understand 
the ES6 keywords ``import``, ``export``, cause it's important
for the modularized programing. Also, you must understand the
AMD function ``require``.


reactjs
============

I would like to recommend the 
`react offcial tutorial <http://facebook.github.io/react/docs/getting-started.html>`_ to start. 
Also, following are some simplest examples to present the basic concept.



Hello world
------------

Following snippet is hello world scripts, you can copy that 
to a txt file and save it as test.html, open it via a modern
browser, and see what happens.

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8" />
        <title>Hello React!</title>
        <script src="http://facebook.github.io/react/js/react.js"></script>
        <script src="http://facebook.github.io/react/js/react-dom.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
      </head>
      <body>
      
        <div id="example"></div>

        <script type="text/babel">
          ReactDOM.render(<h1>Hello, world!</h1>, document.getElementById('example') );
        </script>
      </body>
    </html>

Note:
    - Line 6, including the react.js library
    - Line 7, including the react-dom library
    - Line 8, including the babel compiler, which compile ``JSX`` 
      source code to javascript code. Babel is a great tool for 
      web frontend development
    - Line 12, a blank container div
    - Line 14, noticing the *type="text/babel"*, it's not a 
      regular label like *type="text/javascript"*, that means
      scripts should be compiled by babel
    - Line 15, JSX scripts


.. note::

    We'll present more examples later, the hello world html source code will be
    the default context html source code, you should replacing line 15 with example
    source code.


JSX basic
----------

The official JSX guide `JSX in Depth <http://facebook.github.io/react/docs/jsx-in-depth.html>`_ .

Play with jsx by following JSX scripts(replacing line 15 in example hello world
with following example code).

Variable
~~~~~~~~~~~~~~~~~~

.. code-block:: jsx
    :linenos:

    ReactDOM.render(
        <h1>Time is&nbsp;
            <small>{new Date().toLocaleString()}</small>
        </h1>
    , document.getElementById('example'))

Note: 
    - the variable was wraped by ``{}``


Style
~~~~~~~~~~~

.. code-block:: jsx
    :linenos:

    var style = {color: '#2980B9', fontSize: '60%'};
    ReactDOM.render(
        <h1>Time is&nbsp;
            <small style={style}>{new Date().toLocaleString()}</small>
        </h1>
    , document.getElementById('example'))

Note:
    - variable style was wraped by ``{}``    
    - *fontSize* was camelCased form of font-size, it's common specification
      of css style


CSS class
~~~~~~~~~~~

.. code-block:: css
    :linenos:

    .myFont{color: #2980B9; font-size: 60%};


.. code-block:: jsx
    :linenos:

    ReactDOM.render(
        <h1>Time is&nbsp;
            <small className='myFont'>{new Date().toLocaleString()}</small>
        </h1>
    , document.getElementById('example'))

Note:
    - className is equal with HTML attribute class


Custom attributes
~~~~~~~~~~~~~~~~~~~~

If you pass properties to HTML elements that do not exist in the HTML 
specification, React will not render them. If you want to use a custom 
attribute, you should prefix it with ``data-`` or ``aria-``.

.. code-block:: jsx
    :linenos:

    ReactDOM.render(
        <h1>Time is&nbsp;
            <small className='myFont' data-name="william" aria-name="oneil" 
                   test-name="this isn't gonna be shown">
                {new Date().toLocaleString()}
            </small>
        </h1>
    , document.getElementById('example'))


Component
-----------

.. code-block:: jsx
    :linenos:

    const Timer = React.createClass({
        render: function(){
            return (
                <h1>Time is&nbsp;
                    <small className='myFont' data-name="william" aria-name="oneil" 
                           test-name="this isn't gonna be shown">
                        {new Date().toLocaleString()}
                    </small>
                </h1>
            );
        }
    });

    ReactDOM.render(<Timer />, document.getElementById('example'))

Note:
    - React.createClass create a react component
    - render is predefined key function


State, properties
-------------------

Refactoring source code of `Component`_, add state and props usage example.

.. code-block:: jsx
    :linenos:

    const TimerClock = React.createClass({
        getInitialState: function(){
            return {now: new Date().toLocaleString()}
        },
        render: function(){
            return (
                <small className='myFont' data-name="william" aria-name="oneil" 
                       test-name="this isn't gonna be shown">
                    {this.state.now}
                </small>
            );
        }
    });

    const Timer = React.createClass({
        render: function(){
            return (
                <h1>{this.props.name} is&nbsp;
                    {this.props.children}
                </h1>
            )
        }
    });

    ReactDOM.render(
        <Timer name="Time">
            <TimerClock/>
        </Timer>
    , document.getElementById('example'))


Note:
    - We have 2 components, one is TimerClock, another is Timer. 
    - Timer is container of TimerClock
    - ``this.props.name`` is from line:26 ``name="Time"``, ``this.props.children``
      is the reference of ``<TimerClock/>``
    - ``this.state.now`` is from line:3 ``getInitialState``
    - A simple conclusion: props are variables from outer scope of component, 
      state are variables from inner scope of component


componentDidMount
-------------------

Add a function componentDidMount, acting like its name, it was called when component 
mounted to UI page.

.. code-block:: jsx
    :linenos:

    const TimerClock = React.createClass({
        getInitialState: function(){
            // now return null
            return {now: null}
        },
        componentDidMount: function(){
            console.log('component mounted')
            // display time in 2 seconds
            setTimeout(()=>{this.setState({now: new Date().toLocaleString()})}, 2000)
        },
        render: function(){
            return (
                <small className='myFont' data-name="william" aria-name="oneil" 
                       test-name="this isn't gonna be shown">
                    {this.state.now}
                </small>
            );
        }
    });

    const Timer = React.createClass({
        render: function(){
            return (
                <h1>{this.props.name} is&nbsp;
                    {this.props.children}
                </h1>
            )
        }
    });

    ReactDOM.render(
        <Timer name="Time">
            <TimerClock/>
        </Timer>
    , document.getElementById('example'))


Note:
    - Line 4, return now null, so when page loaed, it shows "Time is"
    - Line 6, add function componentDidMount, it's a callback after component mounted to page
    - Line 9, ``this.setState``, only this API can modify ``this.state``


mixins
-------

Mixin is common use function, it's kind of like inheritence.


.. code-block:: jsx
    :linenos:

    // add mixins source code
    const IntervalMixin = {
        getInitialState: function(){
            return {intervals: []}
        },
        addInterval: function(callback){
            this.state.intervals.push(callback);
        },
        componentDidMount: function(){
            console.log('IntervalMixin loaded.');
            var intervalId = setInterval(function(){
                for(var i=0; i<this.state.intervals.length; i++){
                    this.state.intervals[i]();
                }
            }.bind(this), 1000);
            this.setState({intervalId: intervalId});
        },
        componentWillUnmount: function(){
            clearInterval(this.state.intervalId);
        }
    };

    const TimerClock = React.createClass({
        mixins: [ IntervalMixin ],
        getInitialState: function(){
            return {now: null}
        },
        componentDidMount: function(){
            console.log('component mounted')
            // setTimeout(()=>{this.setState({now: new Date().toLocaleString()})}, 2000)
            this.addInterval(()=>{this.setState({now: new Date().toLocaleString()})});
        },
        render: function(){
            return (
                <small className='myFont' data-name="william" aria-name="oneil" 
                       test-name="this isn't gonna be shown">
                    {this.state.now}
                </small>
            );
        }
    });

    const Timer = React.createClass({
        render: function(){
            return (
                <h1>{this.props.name} is&nbsp;
                    {this.props.children}
                </h1>
            )
        }
    });

    ReactDOM.render(
        <Timer name="Time">
            <TimerClock/>
        </Timer>
    , document.getElementById('example'))


Note:
    - IntervalMixin supply a interval manager, it can be simplely call the 
      ``addInterval`` to add interval callback, also it removes setInterval 
      automatically when component was unmounted from page
    - Line 2, define mixin in the form of object
    - Line 3, 9, 18, getInitialState, componentDidMount, componentWillUnmount,
      these will be combine with class method, via configuring mixin by Line 24 
    - Line 31, adding interval callback via ``addInterval``
    - Line 10, 29, noticing the log message in console, see which ``componentDidMount``
      was called first


Conclusion      
-----------

You must understand concepts:
    - `this.state <./#state-properties>`_
    - `this.props <./#state-properties>`_
    - getInitialState, render, componentDidMount

You should know that:
    - ``this.props`` was not modifiable
    - Do not modify ``this.state`` directly, always call the ``this.setState`` 
      to change value of ``this.state``


Set up development environment with npm and webpack
========================================================

npm
------

npm is depend on nodejs, installing latest nodejs, then you'll get latest npm.

For more information, https://docs.npmjs.com/


webpack
--------

webpack is a javascript bundler, it's great helpful to modularized our javascript
source code.

For more information, http://webpack.github.io/docs/what-is-webpack.html


Start a project
----------------

#. Create a directory ``test``, and enter the directory
#. Add a file ``package.json``:

   .. code-block:: js
       :linenos:
       :caption: package.json

       {
          "name": "test",
          "version": "0.0.0",
          "description": "",
          "scripts": {
          },
          "author": "",
          "license": "",
       }    
#. Run: ``npm install webpack webpack-dev-server webpack-hot-middleware --save-dev`` in terminal
#. Run: ``npm install babel-core babel-loader babel-preset-react --save-dev``
#. Run: ``npm install babel-preset-es2015 babel-preset-react-hmre babel-register --save-dev``
#. Run: ``npm install react react-dom --save``
#. Notice above ``--save``, ``--save-dev``, those options save your installed packages 
   to ``package.json``
#. Add a file ``webpack.config.js``:

   .. code-block:: js
       :linenos:
       :caption: webpack.config.js

        var path = require('path');
        var webpack = require('webpack');

        module.exports = {
            context: path.join(__dirname, "app"),
            entry: [
                './main.jsx',
            ],
            output: {
                path: path.join(__dirname, 'dist'),
                filename: '[name].bundle.js',
                publicPath: '/static/'
            },
            plugins: [
                new webpack.optimize.OccurrenceOrderPlugin(),
                new webpack.HotModuleReplacementPlugin()
            ],
            module: {
                loaders: [
                    {test: /\.jsx?$/, exclude: /node_modules/, loader: "babel", query: {presets: ['es2015', 'react']}},
                    {test: /\.html$/, loader: "file?name=[name].[ext]", },

                    {test: /\.css$/, loader: "style-loader!css-loader"},
                    {test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'},
                ]
            }
        };
#. Add a file ``index.html``        

   .. code-block:: html
       :linenos:
       :caption: index.html

       <!DOCTYPE html>
       <html>
         <head>
           <title>test</title>
         </head>
         <body>
           <div id="root">
           </div>
           <script src="/static/main.bundle.js"></script>
         </body>
       </html>
#. Add a file ``app/main.jsx``:

   .. code-block:: jsx
       :linenos:
       :caption: main.jsx

       import React from "react";
       import ReactDOM from "react-dom";

       class Test extends React.Component {
           constructor(props){
               super(props);
           }
           render(){
               return (<h1>Hello</h1>);
           }
       }

       ReactDOM.render(
           <Test/>, document.getElementById('root')
       );
#. Directory structure:

   .. code-block:: jsx
       :linenos:

        .
        ├── app
        │   └── main.jsx
        ├── index.html
        ├── package.json
        └── webpack.config.js
#. Run: ``npm start``, and open http://127.0.0.1:3001/


You may find the syntax in ``main.jsx`` is difference with `reactjs`_, because 
here is ES6 ``class`` syntax,
`online tutorial for react in ES6 <https://babeljs.io/blog/2015/06/07/react-on-es6-plus>`_. 
Both ``react.createClass`` and ``class`` do the same thing, but ``class`` in ES6 
doesn't support `mixins`_.


Reflux 
========


react-router
==============

Redux
=======


Scaffold
==========
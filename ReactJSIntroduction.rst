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

In this document, mostly I will show you simple source code examples, 
and explain how they work. You can read the source codes and try 
to run it. You'll understand reactjs quickly by making these simple 
examples clear. `In the end <./ReactJSIntroduction.html#scaffold>`_, 
I list the react-router+reflux scaffold and react-router+redux scaffold 
source repository, it may help to start up a new project quickly.


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


Setting up development environment with npm and webpack
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



react-router
==============

I recommend reading the `offcial guide <https://github.com/reactjs/react-router/tree/master/docs>`_
to learn full react-router knowledges. Here I'll show you a simple routing example to quickly start.

All examples code based on `start a project`_.

At first, install react-router: ``npm install react-router --save``.
then clear the file *main.jsx*, and put following codes into it:

   .. code-block:: jsx
       :linenos:

        import React from "react";
        import ReactDOM from "react-dom";

        import { Route, Router, IndexRoute } from "react-router";
        import { hashHistory } from "react-router";

        class Page1 extends React.Component {
            constructor(props){
                super(props);
            }
            render(){
                return (<h1>Page1</h1>);
            }
        }


        class Page2 extends React.Component {
            constructor(props){
                super(props);
            }
            render(){
                return (<h1>Page2</h1>);
            }
        }


        class Page3 extends React.Component {
            constructor(props){
                super(props);
            }
            render(){
                return (<h1>Page3</h1>);
            }
        }


        class AppContainer extends React.Component {
            constructor(props){
                super(props);
            }
            gotoPage1(event){
                hashHistory.push('/page1');
                event.preventDefault();
            }
            gotoPage2(event){
                hashHistory.push('/page2');
                event.preventDefault();
            }
            gotoPage3(event){
                hashHistory.push('/page3');
                event.preventDefault();
            }
            render(){
                return (
                    <div>
                        <ul>
                            <li><a onClick={this.gotoPage1} href="">go page 1</a></li>
                            <li><a onClick={this.gotoPage2} href="">go page 2</a></li>
                            <li><a onClick={this.gotoPage3} href="">go page 3</a></li>
                        </ul>
                        <div>
                            {this.props.children}
                        </div>
                    </div>
                );
            }
        }


        const routes = (
            <Router history={hashHistory} >
                <Route path="/" component={AppContainer} >
                    <IndexRoute component={Page1} />
                    <Route path="page1" component={Page1} />
                    <Route path="page2" component={Page2} />
                    <Route path="page3" component={Page3} />
                </Route>
            </Router>
        );


        ReactDOM.render(
            routes, document.getElementById('root')
        );


Notes:
    - Line 4, 5: import react-router functions, hashHistory means we use browser 
      hash to hold the location information
    - Line 7, 17, 27: we defined 3 pages
    - Line 37: AppContainer is container of page content, Line 56: list of navigators
    - Line 62: ``this.props.children`` is page content
    - Line 70: define locations of all pages 
    - Line 73: Page1 is index page

Try ``npm start`` to see the demo page.



Reflux 
========

Reading the `official guide <https://github.com/reflux/refluxjs>`_, understanding 
the basic concepts **action**, **store**, **view(component)**, after then following 
below simplest tutorial will make you quickly understand how reflux works.

Examples codes based on `start a project`_.

At first, install reflux: ``npm install reflux --save``.
then clear the file *main.jsx*, and put following codes into it:


.. code-block:: jsx
   :linenos:

    import React from "react";
    import ReactDOM from "react-dom";

    import Reflux from "reflux";


    const Actions = Reflux.createActions(['loadData', 'flushData']);


    const dataStore = Reflux.createStore({
        init: function(){
            this.listenTo(Actions.loadData, this.onLoadData);
            this.listenTo(Actions.flushData, this.onFlushData);
        },
        dataTemplate: JSON.stringify({
            name: '--',
            age: '--',
            status: '--'
        }),
        onLoadData: function(){
            var data = localStorage.getItem('test') || this.dataTemplate;
            this.trigger(JSON.parse(data));
        },
        onFlushData: function(params){
            var data = JSON.parse(localStorage.getItem('test') || this.dataTemplate);
            Object.assign(data, params);
            localStorage.setItem('test', JSON.stringify(data));
            Actions.loadData();
        },
        getInitialState: function(){
            return JSON.parse(localStorage.getItem('test') || this.dataTemplate);
        }
    });


    const TestApp = React.createClass({
        mixins: [ Reflux.connect(dataStore,"data") ],
        handleNameChange: function(event){
            Actions.flushData({"name": event.target.value});
        },
        handleAgeChange: function(event){
            Actions.flushData({"age": event.target.value});
        },
        handleStatusChange: function(event){
            Actions.flushData({"status": event.target.value});
        },
        render: function(){
            return (
                <div>
                    <label>Name:</label><input onChange={this.handleNameChange} value={this.state.data.name} /><br/>
                    <label>age:</label><input onChange={this.handleAgeChange} value={this.state.data.age} /><br/>
                    <label>status:</label><input onChange={this.handleStatusChange} value={this.state.data.status} /><br/>
                </div>
            );
        }
    });


    ReactDOM.render(
        <TestApp/>, document.getElementById('root')
    );

Remember that: the flow path of reflux is

    ::

        ╔═════════╗       ╔════════╗       ╔═════════════════╗
        ║ Actions ║──────>║ Stores ║──────>║ View Components ║
        ╚═════════╝       ╚════════╝       ╚═════════════════╝
             ^                                      │
             └──────────────────────────────────────┘

The core source structure are action/store/view.

Note:
    - As I mentioned in `Start a project`_ that component created in ES6 ``class`` 
      way can't support mixin, and using Reflux with mixin is very convenience, so 
      I recommend using ``React.createClass`` to create component
    - Line 4: import reflux
    - Line 7: create actions, define loadData(read)/flushData(write)
    - Line 10: create store
    - Line 12, 13: binding store and action, it's same with calling ``this.onLoadData`` 
      when call ``Actions.loadData``, also ``flushData``
    - Line 11, 30: ``init``, called when store was initialized, getInitialState, called 
      when the store's binding component was mounted
    - Line 37, binding the store to component's state, referenced by the name ``data``,
      ``this.state.data`` is coming from ``this.trigger`` in dataStore, also returned by
      ``getInitialState`` in dataStore


Redux
=======

Reading the `official guide <http://redux.js.org/docs/introduction/index.html>`_, 
You should understand the basic concepts **action**, **reducer**, **store**, **component**, 
**dispatch**, after then trying to run following simple example, and understanding
how it works.

The redux offcial guide does not just explain to reactjs user, it was explained as
a individual javascript component. So I'd like to recommend you just know the basic 
concepts and learn redux in reactjs by following example.

Examples codes based on `start a project`_, and it implements the completely same 
input-UI with `Reflux`_.

At first, install redux and react-redux: ``npm install redux react-redux --save``.
then clear the file *main.jsx*, and put following codes into it:


.. code-block:: jsx
   :linenos:

    import React, { Component, PropTypes } from 'react';
    import ReactDOM from "react-dom";

    import { createStore } from 'redux';
    import { connect } from 'react-redux';
    import { Provider } from 'react-redux';


    // create action constants
    const EDIT_NAME = 'EDIT_NAME';
    const EDIT_AGE = 'EDIT_AGE';
    const EDIT_STATUS = 'EDIT_STATUS';

    // create actions
    const editName = function(text){
        return {
            type: EDIT_NAME,
            text
        };
    };

    const editAge = function(text){
        return {
            type: EDIT_AGE,
            text
        };
    };

    const editStatus = function(text){
        return {
            type: EDIT_STATUS,
            text
        };
    };

    // create reducers, state is { name, status, age }
    const stateKey = 'test';
    var initialState = {
        name: '--',
        status: '--',
        age: '--'
    };
    if (localStorage.getItem(stateKey) != null){
        initialState = JSON.parse(localStorage.getItem(stateKey));
    }

    const reducer = function(state=initialState, action){
        var data = state;
        switch(action.type){
            case EDIT_NAME:
                data = Object.assign({}, state, {"name": action.text});
                break;
            case EDIT_AGE:
                data = Object.assign({}, state, {"age": action.text});
                break;
            case EDIT_STATUS:
                data = Object.assign({}, state, {"status": action.text});
                break;
        }
        localStorage.setItem(stateKey, JSON.stringify(data));
        return data;
    };

    // create store
    let store = createStore(reducer);

    // create component
    class TestApp extends React.Component{
        constructor(props){
            super(props);
        }
        handleChange(event){
            var name = event.target.name;
            var value = event.target.value;
            const { dispatch } = this.props; // same with dispatch = this.props.dispatch
            if(name == 'name'){
                dispatch(editName(value));
            }   
            else if(name == 'age'){
                dispatch(editAge(value));
            }
            else if(name == 'status'){
                dispatch(editStatus(value));
            }
        }
        render(){
            const { data } = this.props;
            return (
                <div>
                    <label>Name:</label><input onChange={this.handleChange.bind(this)} name="name" value={data.name} /><br/>
                    <label>age:</label><input onChange={this.handleChange.bind(this)} name="age" value={data.age} /><br/>
                    <label>status:</label><input onChange={this.handleChange.bind(this)} name="status" value={data.status} /><br/>
                </div>
            );
        }
    }

    TestApp.propTypes = {
        data: PropTypes.object.isRequired,
    };

    // connect store and component
    const select = function(state){
        return {data: state};
    };

    TestApp = connect(select)(TestApp);

    // render
    ReactDOM.render(
        <Provider store={store}><TestApp/></Provider>, 
        document.getElementById('root')
    );   

Note:
    - Remember the source code order, it's helpful when we start writing source code
        #. design action types
        #. create actions
        #. create reducers
        #. create store 
        #. create component
        #. connect store and component
    - Line 4, 5, 6: import the shortcut functions from redux
    - Line 43, 60: persistence data
    - Line 51, 54, 57, 61: reducer always return a new state or the old state, DO 
      NOT change it
    - Line 87: ES6 spread syntax
    - Line 98: `properties validation <https://facebook.github.io/react/docs/reusable-components.html>`_
    - Line 107: bind the data which was returned from reducer and stored in store into component's props
    - Line 111: bind store and component via Provider


Scaffold
==========

I create 2 scaffolds with simple source code structure, you can keep the structure
and changing/adding any source files/codes to that. They are both have no animations, mixins,
ets, Only the react-router, so I think it's easy to get clear with these scaffolds.


reflux, react-router
---------------------

https://github.com/vincentwyshan/react-scaffold/tree/master/reflux

Repository structure:
    - actions: reflux actions
    - containers: containers(pages)
    - components: common components
    - mock: create mock data
    - stores: reflux stores
    - routes.jsx: routes
    - main.jsx: entry point

Clone the source code, run ``npm install`` and ``npm start`` to start development server.


redux, react-router
---------------------

https://github.com/vincentwyshan/react-scaffold/tree/master/redux

Repository structure:
    - actions: action types and actions
    - components: common components
    - containers: containers(pages)
    - mock: create mock data
    - reducers: reducers
    - store: store configuring
    - routes.jsx: routes
    - main.jsx: entry point

Clone the source code, run ``npm install`` and ``npm start`` to start development server.


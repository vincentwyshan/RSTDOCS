=========================
Won Chart
=========================

.. Contents::


Target
=======
- Easy to maintain (add new features)
    - Architecture documentation
    - Correlation technology documentation
    - Usage cases (examples)
- Easy to use
    - Make the charting element concepts clear, such as line/candlestick path/symbol/
      column/axis/tooltip/canvas. And we have a documentation to describe what they are 
      and how they works together
    - Like open source/commercial chart libraries(highchart, chart.js, fusionchart):
      `everything is configured <./ChartCore.html#usage>`_


Source code structure
==================

A introduction to current ChartCore.

- View
- Coordinating
- Template
- Graphic



Release
========
Released to several js libraries, to support ``require``, es6 module, jquery, 
native javascript, etc.

- wonchart.{version}.js
- wonchart.jquery.{version}.js
- wonchart.backbone.{version}.js
- wonchart.angular.{version}.js

Js bundles packaged by the tools like gulp/browserify/webpack, I recommend 
webpack.


Usage
======= 


.. code-block:: javascript
    :linenos:

    var options = {
    	chart: {
    		renderAt: 'chartId',
    		background: {
    			color: '#fff'
    		}
    	},
    	priceCandleStick: {
    		timeseries: timeseries, // [{time, value}]
    		frequency: 'Daily',
    		upColor: 'green',
    		downColor: 'red'
    	},
    	volumeColumn: {
    		timeseries: timeseries,
    		upColor: 'green',
    		downColor: 'red'
    	},
    	tooltip: {
    		disable: false,
    		htmlTemplate: "underscore template"
    	}
    };
    var chart = new WONChart(options);



Options
----------

- chart: { crosshairs: {disable, color, width, }, background: {color, }, renderAt, }
- priceCandleStick: { timeseries: [{time, open, high, low, close}], frequency, upColor, downColor}
- volumeColumn: { timeseries: [{time, value, upColor, downColor}] }
- lines: [{color, width, timeseries}]
- symbols: [{color, timeseries, defaultSymbolUrl}]
- yAxis: {grids: [{gridHeight, gridLineWidth, gridLineColor}], label: {disable, align, fontSize, color}}
- xAxis: {grids: [{gridHeight, gridLineWidth, gridLineColor}], label: {disable, align, fontSize, color}}
- tooltip: {htmlTemplate, disable}, 


Planning
========

Phase 1
-------------
- Project involved: MS Global, MS HK
- Using git submodule to manage ChartCore repository, online documentations:
    + https://git-scm.com/book/en/v2/Git-Tools-Submodules
    + http://www.kafeitu.me/git/2012/03/27/git-submodule.html
    + The traps of submodule: http://blog.devtang.com/2013/05/08/git-submodule-issues/
- ChartCore documentation, describing the architecture, apis, usage examples
- Source code control rule: no one can push source code to repository unless he is 
  member of chartcore maintainers or authorized to submit code


Phase 2
--------
- Interface design:
    + keep current interfaces
    + redesign interfaces to use chartcore by configration, 
      `highcharts API <http://api.highcharts.com/highcharts>`_ 
      for reference, above `Usage`_ is a sample
    + keep current interfaces, and support config style usage
- Add more features, including the features MS Tool already have
# Plugins

Starting with v2.1.0, you can create plugins for chart.js. To register your plugin, simply call `Chart.plugins.register` and pass your plugin in.


```javascript
var myplugin = { ... };
Chart.plugins.register(myplugin);
```
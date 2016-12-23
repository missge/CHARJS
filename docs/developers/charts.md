# New Charts

Chart.js 2.0 introduces the concept of controllers for each dataset. Like scales, new controllers can be written as needed.

```javascript
Chart.controllers.MyType = Chart.DatasetController.extend({

});


// Now we can create a new instance of our chart, using the Chart.js API
new Chart(ctx, {
    // this is the string the constructor was registered at, ie Chart.controllers.MyType
    type: 'MyType',
    data: data,
    options: options
});
```

## Dataset Controller Interface

Dataset controllers must implement the following interface.

```javascript
{
    // Create elements for each piece of data in the dataset. Store elements in an array on the dataset as dataset.metaData
    addElements: function() {},

    // Create a single element for the data at the given index and reset its state
    addElementAndReset: function(index) {},

    // Draw the representation of the dataset
    // @param ease : if specified, this number represents how far to transition elements. See the implementation of draw() in any of the provided controllers to see how this should be used
    draw: function(ease) {},

    // Remove hover styling from the given element
    removeHoverStyle: function(element) {},

    // Add hover styling to the given element
    setHoverStyle: function(element) {},

    // Update the elements in response to new data
    // @param reset : if true, put the elements into a reset state so they can animate to their final values
    update: function(reset) {},
}
```

The following methods may optionally be overridden by derived dataset controllers
```javascript
{
    // Initializes the controller
    initialize: function(chart, datasetIndex) {},

    // Ensures that the dataset represented by this controller is linked to a scale. Overridden to helpers.noop in the polar area and doughnut controllers as these
    // chart types using a single scale
    linkScales: function() {},

    // Called by the main chart controller when an update is triggered. The default implementation handles the number of data points changing and creating elements appropriately.
    buildOrUpdateElements: function() {}
}
```

## Extending Existing Chart Types

Extending or replacing an existing controller type is easy. Simply replace the constructor for one of the built in types with your own.

The built in controller types are:
* `Chart.controllers.line`
* `Chart.controllers.bar`
* `Chart.controllers.radar`
* `Chart.controllers.doughnut`
* `Chart.controllers.polarArea`
* `Chart.controllers.bubble`

### Bar Controller
The bar controller has a special property that you should be aware of. To correctly calculate the width of a bar, the controller must determine the number of datasets that map to bars. To do this, the bar controller attaches a property `bar` to the dataset during initialization. If you are creating a replacement or updated bar controller, you should do the same. This will ensure that charts with regular bars and your new derived bars will work seamlessly.
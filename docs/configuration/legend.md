# Legend Configuration

The chart legend displays data about the datasets that area appearing on the chart.

## Configuration options
The legend configuration is passed into the `options.legend` namespace. The global options for the chart legend is defined in `Chart.defaults.global.legend`.

### display
**Type:** Boolean
**Default:** `true`
Is the legend displayed.

### position
**Type:** String
**Default:** `'top'`
Position of the legend. Options are:
* `'top'`
* `'left'`
* `'bottom'`
* `'right'`

### fullWidth
**Type:** Boolean
**Default:** `true`
Marks that this box should take the full width of the canvas (pushing down other boxes). This is unlikely to need to be changed in day-to-day use.

### onClick
**Type:** Function
**Default:** `function(event, legendItem) {}`
A callback that is called when a 'click' event is registered on top of a label item.

### onHover
**Type:** Function
**Default:** `function(event, legendItem) {}`
A callback that is called when a 'mousemove' event is registered on top of a label item

### labels
**Type:** Object
See the [Legend Label Configuration](#legend-label-configuration) section below.

### reverse
**Type:** Boolean
**Default:** `false`
Legend will show datasets in reverse order.

## Legend Label Configuration

The legend label configuration is nested below the legend configuration using the `labels` key.

### boxWidth
**Type:** Number
**Boolean:** `40`
Width of coloured box.

### fontSize
**Type:** Number
**Boolean:** `12`
Font size of text in legend.

### fontStyle
**Type:** String
**Boolean:** `'normal'`
Font style of text in the legend.

### fontColor
**Type:** Color
**Boolean:** `'#666'`
Font color of text in legend.

### fontFamily
**Type:** String
**Boolean:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family of legend text.

### padding
**Type:** Number
**Boolean:** `10`
Padding between rows of colored boxes.

### generateLabels
**Type:** Function
**Boolean:** `function(chart) {  }`
Generates legend items for each thing in the legend. Default implementation returns the text + styling for the color box. See [Legend Item](#chart-configuration-legend-item-interface) for details.

### filter
**Type:** Function
**Boolean:** `null`
Filters legend items out of the legend. Receives 2 parameters, a [Legend Item](#chart-configuration-legend-item-interface) and the chart data.

### usePointStyle
**Type:** Boolean
**Boolean:** `false`
Label style will match corresponding point style (size is based on fontSize, boxWidth is not used in this case).

## Legend Item Interface

Items passed to the legend `onClick` function are the ones returned from `labels.generateLabels`. These items must implement the following interface.

```javascript
{
    // Label that will be displayed
    text: String,

    // Fill style of the legend box
    fillStyle: Color,

    // If true, this item represents a hidden dataset. Label will be rendered with a strike-through effect
    hidden: Boolean,

    // For box border. See https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/lineCap
    lineCap: String,

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash
    lineDash: Array[Number],

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset
    lineDashOffset: Number,

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin
    lineJoin: String,

    // Width of box border
    lineWidth: Number,

    // Stroke style of the legend box
    strokeStyle: Color

    // Point style of the legend box (only used if usePointStyle is true)
    pointStyle: String
}
```

## Example

The following example will create a chart with the legend enabled and turn all of the text red in color.

```javascript
var chart = new Chart(ctx, {
    type: 'bar',
    data: data,
    options: {
        legend: {
            display: true,
            labels: {
                fontColor: 'rgb(255, 99, 132)'
            }
        }
}
});
```

## Custom On Click Actions

It can be common to want to trigger different behaviour when clicking an item in the legend. This can be easily achieved using a callback in the config object.

The default legend click handler is:
```javascript
function(e, legendItem) {
    var index = legendItem.datasetIndex;
    var ci = this.chart;
    var meta = ci.getDatasetMeta(index);

    // See controller.isDatasetVisible comment
    meta.hidden = meta.hidden === null? !ci.data.datasets[index].hidden : null;

    // We hid a dataset ... rerender the chart
    ci.update();
}
```

Lets say we wanted instead to link the display of the first two datasets. We could change the click handler accordingly.

```javascript
var defaultLegendClickHandler = Chart.defaults.global.legend.onClick;
var newLegendClickHandler = function (e, legendItem) {
    var index = legendItem.datasetIndex;

    if (index > 1) {
        // Do the original logic
        defaultLegendClickHandler(e, legendItem);
    } else {
        let ci = this.chart;
        [ci.getDatasetMeta(0),
         ci.getDatasetMeta(1)].forEach(function(meta) {
            meta.hidden = meta.hidden === null? !ci.data.datasets[index].hidden : null;
        });
        ci.update();
    }
};

var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        legend: {

        }
    }
});
```

Now when you click the legend in this chart, the visibility of the first two datasets will be linked together.

## HTML Legends

Sometimes you need a very complex legend. In these cases, it makes sense to generate an HTML legend. Charts provide a `generateLegend()` method on their prototype that returns an HTML string for the legend.

To configure how this legend is generated, you can change the `legendCallback` config property.

```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        legendCallback: function(chart) {
            // Return the HTML string here.
        }
    }
});
```
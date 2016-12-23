# Line
A line chart is a way of plotting data points on a line. Often, it is used to show trend data, or the comparison of two data sets.

## Example Usage
```javascript
var myLineChart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: options
});
```

## Dataset Properties

The line chart allows a number of properties to be specified for each dataset. These are used to set display properties for a specific dataset. For example, the colour of a line is generally set this way.

All point* properties can be specified as an array. If these are set to an array value, the first value applies to the first point, the second value to the second point, and so on.

### label
**Type:** String
The label for the dataset which appears in the legend and tooltips.

### xAxisID
**Type:** String
The ID of the x axis to plot this dataset on. If not specified, this defaults to the ID of the first found x axis

### yAxisID
**Type:** String
The ID of the y axis to plot this dataset on. If not specified, this defaults to the ID of the first found y axis.

### backgroundColor
**Type:** Color
The fill color under the line. See [Colors](../general/colors.md#colors)

### borderColor
**Type:** Color
The color of the line. See [Colors](../general/colors.md#colors)

### borderWidth
**Type:** Number
The width of the line in pixels.

### borderDash
**Type:** Number[]
Length and spacing of dashes. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash)

### borderDashOffset
**Type:** Number
Offset for line dashes. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset)

### borderCapStyle
**Type:** String
Cap style of the line. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineCap)

### borderJoinStyle
**Type:** String
Line joint style. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin)

### cubicInterpolationMode
**Type:** String
Algorithm used to interpolate a smooth curve from the discrete data points. 

Options are:
* 'default'
* 'monotone'. 

The 'default' algorithm uses a custom weighted cubic interpolation, which produces pleasant curves for all types of datasets. 

The 'monotone' algorithm is more suited to `y = f(x)` datasets : it preserves monotonicity (or piecewise monotonicity) of the dataset being interpolated, and ensures local extremums (if any) stay at input data points. 

If left untouched (`undefined`), the global `options.elements.line.cubicInterpolationMode` property is used.

### fill
**Type:** Boolean or String
If `true`, fill the area under the line. The line is filled to the baseline. If the y axis has a 0 value, the line is filled to that point. If the axis has only negative values, the line is filled to the highest value. If the axis has only positive values, it is filled to the lowest value.

String values to fill to specific locations are:
* `'zero'`
* `'top'`
* `'bottom'`

### lineTension
**Type** Number
Bezier curve tension of the line. Set to 0 to draw straightlines. This option is ignored if monotone cubic interpolation is used.

### pointBackgroundColor
**Type:** Color or Color[]
The fill color for points.

### pointBorderColor
**Type:** Color or Color[]
The border color for points.

### pointBorderWidth
**Type:** Number Number[]
The width of the point border in pixels.

### pointRadius
**Type:** Number Number[]
The radius of the point shape. If set to 0, the point is not rendered.

### pointStyle
**Type:** String, String[], Image, Image[]
The style of point. Options are:
* 'circle'
* 'cross'
* 'crossRot'
* 'dash'. 
* 'line'
* 'rect'
* 'rectRounded'
* 'rectRot'
* 'star'
* 'triangle'

If the option is an image, that image is drawn on the canvas using [drawImage](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/drawImage).

### pointHitRadius
**Type:** Number or Number[]
The pixel size of the non-displayed point that reacts to mouse events.

### pointHoverBackgroundColor
**Type:** Color or Color[]
Point background color when hovered.

### pointHoverBorderColor
**Type:** Color or Color[]
Point border color when hovered.

### pointHoverBorderWidth
**Type:** Number or Number[]
Border width of point when hovered.

### pointHoverRadius
**Type:** Number or Number[]
The radius of the point when hovered.

### showLine
**Type:** `Boolean`
If false, the line is not drawn for this dataset.

### spanGaps
**Type:** `Boolean`
If true, lines will be drawn between points with no or null data. If false, points with `NaN` data will create a break in the line

### steppedLine
**Type:** `Boolean`
If true, the line is shown as a stepped line and 'lineTension' will be ignored.

## Configuration Options

The line chart defines the following configuration options. These options are merged with the global chart configuration options, `Chart.defaults.global`, to form the options passed to the chart.

### showLines
**Type:** Boolean
**Default:** `true`
If false, the lines between points are not drawn.

### spanGaps
**Type:** Boolean
**Default:** `false`
If false, NaN data causes a break in the line.

## Default Options

It is common to want to apply a configuration setting to all created line charts. The global line chart settings are stored in `Chart.defaults.line`. Changing the global options only affects charts created after the change. Existing charts are not changed.

For example, to configure all line charts with `spanGaps = true` you would do:
```javascript
Chart.defaults.line.spanGaps = true;
```

## Data Structure

The `data` property of a dataset for a line chart can be passed in two formats. 

### Number[]
```javascript
data: [20, 10]
```

When the `data` array is an array of numbers, the x axis is generally a [category](../axes/cartesian/category.md#Category Axis). The points are placed onto the axis using their position in the array.

### Point[]

```javascript
data: [{
        x: 10,
        y: 20
    }, {
        x: 15,
        y: 10
    }]
```

This alternate is used for sparse datasets, such as those in [scatter charts](./scatter.md#scatter-chart). Each data point is specified using an object containing `x` and `y` properties.

# Stacked Area Chart

Line charts can be configured into stacked area charts by changing the settings on the y axis to enable stacking. Stacked area charts can be used to show how one data trend is made up of a number of smaller pieces.

```javascript
var stackedLine = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        scales: {
            yAxes: [{
                stacked: true
            }]
        }
    }
});


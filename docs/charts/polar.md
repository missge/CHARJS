# Polar Area

Polar area charts are similar to pie charts, but each segment has the same angle - the radius of the segment differs depending on the value.

This type of chart is often useful when we want to show a comparison data similar to a pie chart, but also show a scale of values for context.

## Example Usage

```javascript
new Chart(ctx, {
    data: data,
    type: 'polarArea',
    options: options
});
```

## Dataset Properties

The following options can be included in a polar area chart dataset to configure options for that specific dataset.

### label
**Type:** String
The label for the dataset which appears in the legend and tooltips.

### backgroundColor
**Type:** Color[]
The fill color of the arcs in the dataset. See [Colors](../general/colors.md#colors)

### borderColor
**Type:** Color[]
The border color of the arcs in the dataset. See [Colors](../general/colors.md#colors)

### borderWidth
**Type:** Number[]
The border width of the arcs in the dataset.

### hoverBackgroundColor
**Type:** Color[]
The fill colour of the arcs when hovered.

### hoverBorderColor
**Type:** Color[]
The stroke colour of the arcs when hovered.

### hoverBorderWidth
**Type:** Number[]
The stroke width of the arcs when hovered.

## Config Options

These are the customisation options specific to Polar Area charts. These options are merged with the [global chart configuration options](#global-chart-configuration), and form the options of the chart.

### startAngle
**Type:** Number
**Default:** `-0.5 * Math.PI`
Starting angle to draw arcs for the first item in a dataset.

### animateRotate
**Type:** Boolean
**Default:** `true`
If true, the chart will animate in with a rotation animation. This property is in the `options.animation` object.

```javascript
options = {
    animation: {
        animateRotate: false
    }
};
```

### animateScale
**Type:** Boolean
**Default:** `true`
If true, will animate scaling the chart from the center outwards. This property is in the `options.animation` object.

```javascript
options = {
    animation: {
        animateScale: true
    }
};
```

## Default Options

We can also change these defaults values for each PolarArea type that is created, this object is available at `Chart.defaults.polarArea`. Changing the global options only affects charts created after the change. Existing charts are not changed.

For example, to configure all new polar area charts with `animateScale = false` you would do:
```javascript
Chart.defaults.polarArea.animation.animateScale = false;
```

## Data Structure

For a polar area chart, datasets need to contain an array of data points. The data points should be a number, Chart.js will total all of the numbers and calculate the relative proportion of each.

You also need to specify an array of labels so that tooltips appear correctly for each slice.

```javascript
data = {
    datasets: [{
        data: [10, 20, 30]
    }],

    // These labels appear in the legend and in the tooltips when hovering different arcs
    labels: [
        'Red',
        'Yellow',
        'Blue'
    ]
};
```
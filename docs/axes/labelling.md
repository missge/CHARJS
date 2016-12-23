# Labeling Axes

When creating a chart, you want to tell the viewer what data they are viewing. To do this, you need to label the axis.

## Scale Title Configuration

The scale label configuration is nested under the scale configuration in the `scaleLabel` key. It defines options for the scale title. Note that this only applies to cartesian axes.

### display
**Type:** Boolean
**Default:** `false`
If true, display the axis title.

### labelString
**Type:** String
**Default:** `''`
The text for the title. (i.e. "# of People" or "Respone Choices").

### fontColor
**Type:** Color
**Default:** `'#666`
Font color for scale title.

### fontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family for the scale title, follows CSS font-family options.

### fontSize
**Type:** Number
**Default:** `12`
Font size for scale title.

### fontStyle
**Type:** String
**Default:** `'normal'`
Font style for the scale title, follows CSS font-style options (i.e. normal, italic, oblique, initial, inherit).

## Creating Custom Tick Formats

It is also common to want to change the tick marks to include information about the data type. For example, adding a dollar sign ('$'). To do this, you need to override the `ticks.callback` method in the axis configuration.
In the following example, every label of the Y axis would be displayed with a dollar sign at the front..

If the callback returns `null` or `undefined` the associated grid line will be hidden.

```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    // Include a dollar sign in the ticks
                    callback: function(value, index, values) {
                        return '$' + value;
                    }
                }
            }]
        }
    }
});
```
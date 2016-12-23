# Linear Radial Axis

The linear scale is use to chart numerical data. As the name suggests, linear interpolation is used to determine where a value lies in relation the center of the axis.

The following additional configuration options are provided by the radial linear scale.

## Configuration Options

The axis has configuration properties for ticks, angle lines (line that appear in a radar chart outward from the center), pointLabels (labels around the edge in a radar chart). The following sections define each of the properties in those sections.

## Tick Options
The following options are provided by the linear scale. They are all located in the `ticks` sub options.

### backdropColor
**Type:** Color
**Default:** `'rgba(255, 255, 255, 0.75)'`
Color of label backdrops.

### backdropPaddingX
**Type:** Number
**Default:** 2
Horizontal padding of label backdrop.

### backdropPaddingY
**Type:** Number
**Default:** 2
Vertical padding of label backdrop.

### beginAtZero
**Type:** Boolean
if true, scale will include 0 if it is not already included.

```javascript
let options = {
    scales: {
        yAxes: [{
            ticks: {
                beginAtZero: true
            }
        }]
    }
}
```

### min
**Type:** Number
User defined minimum number for the scale, overrides minimum value from data.

```javascript
let options = {
    scales: {
        yAxes: [{
            type: 'linear',
            ticks: {
                // y axis now starts at -100
                min: -100 
            }
        }]
    }
};
```

### max
**Type:** Number
User defined maximum number for the scale, overrides maximum value from data.

```javascript
let options = {
    scales: {
        yAxes: [{
            type: 'linear',
            ticks: {
                // y axis now ends at 250
                max: 250 
            }
        }]
    }
};
```

### maxTicksLimit
**Type:** Number
**Default:** 11
Maximum number of ticks and gridlines to show.

### stepSize
**Type:** Number
User defined fixed step size for the scale. If set, the scale ticks will be enumerated by multiple of stepSize, having one tick per increment. If not set, the ticks are labeled automatically using the nice numbers algorithm.

This example sets up a chart with a y axis that creates ticks at `0, 0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5, 5`.

```javascript
let options = {
    scales: {
        yAxes: [{
            ticks: {
                max: 5,
                min: 0,
                stepSize: 0.5
            }
        }]
    }
};
```

### suggestedMax
**Type:** Number
Adjustment used when calculating the maximum data value. This can be used to extend the range of the axis while maintaing the auto fit behaviour.

```javascript
let maxDataValue = Math.max(mostPositiveValue, options.ticks.suggestedMax);
```

In this example, the largest positive value is 50, but the data maximum is expanded out to 100.

```javascript
let chart = new Chart(ctx, {
    type: 'line',
    data: {
        datasets: [{
            label: 'First dataset',
            data: [0, 20, 40, 50]
        }],
        labels: ['January', 'February', 'March', 'April']
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    suggestedMax: 100
                }
            }]
        }
    }
});
```

### suggestedMin
**Type:** Number
Adjustment used when calculating the maximum data value. This can be used to extend the range of the axis while maintaing the auto fit behaviour.

```javascript
let minDataValue = Math.min(mostNegativeValue, options.ticks.suggestedMin);
```

### showLabelBackdrop
**Type:** Boolean
**Default:** `true`
If true, draw a background behind the tick labels.

## Angle Line Options

The following options are used to configure angled lines that radiate from the center of the chart to the point labels. They can be found in the `angleLines` sub options. Note that these options only apply if `lineArc` is false.

### display
**Type:** Boolean
**Default:** `true`
If true, angle lines are shown.

### color
**Type:** Color
**Default:** `rgba(0, 0, 0, 0.1)`
Color of angled lines

### lineWidth
**Type:** Number
**Default:** `1`
Width of angled lines

## Point Label Options

The following options are used to configure the point labels that are shown on the perimeter of the scale. They can be found in the `pointLabels` sub options. Note that these options only apply if `lineArc` is false.

### callback
**Type:** Function
Callback function to transform data labels to point labels. The default implementation simply returns the current string.

### fontColor
**Type:** Color
**default:** `'#666'`
Font color for point labels.

To render the point labels in red text, one would do:
```javascript
let radar = new Chart(ctx, {
    type: 'radar',
    data: data,
    options: {
        scale: {
            pointLabels: {
                fontColor: 'rgb(255, 0, 0)'
            }
        }
    }
})
```

### fontFamily
**Type:** String
**default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family to use when rendering labels.

### fontSize
**Type:** Number
**default:** 10
Font size in pixels.

### fontStyle
**Type:** String
**default:** 'normal'
Font style to use when rendering point labels.
# Linear Cartesian Axis

The linear scale is use to chart numerical data. It can be placed on either the x or y axis. The scatter chart type automatically configures a line chart to use one of these scales for the x axis. As the name suggests, linear interpolation is used to determine where a value lies on the axis.

## Tick Configuration Options

The following options are provided by the linear scale. They are all located in the `ticks` sub options.

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
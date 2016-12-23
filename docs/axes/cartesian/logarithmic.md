# Logarithmic Cartesian Axis

The logarithmic scale is use to chart numerical data. It can be placed on either the x or y axis. As the name suggests, logarithmic interpolation is used to determine where a value lies on the axis.

## Tick Configuration Options

The following options are provided by the logarithmic scale. They are all located in the `ticks` sub options.

### min
**Type:** Number
User defined minimum number for the scale, overrides minimum value from data.

```javascript
let options = {
    scales: {
        yAxes: [{
            type: 'logarithmic',
            ticks: {
                // y axis now starts at 1e-03
                min: 0.001 
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
                // y axis now ends at 1e06
                max: 1e06
            }
        }]
    }
};
```
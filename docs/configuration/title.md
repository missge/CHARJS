# Title

The chart title defines text to draw at the top of the chart.

## Title Configuration
The title configuration is passed into the `options.title` namespace. The global options for the chart title is defined in `Chart.defaults.global.title`.

### display
**Type:** Boolean
**Default:** `false`
If true, the title block is displayed.

### position
**Type:** String
**Default:** `'top'`
Position of the title. Possible values are:
* `'top'`
* `'left'`
* `'bottom'`
* `'right'`

### fontSize
**Type:** Number
**Default:** `12`
Font size of the title text.

### fontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family for the title text.

### fontColor
**Type:** Color
**Default:** `'#666`
Font color inherited from global configuration.

### fontStyle
**Type:** String
**Default:** `'bold`
Font styling of the title text.

### padding
**Type:** Number
**Default:** `10`
Number of pixels to add above and below the title text.

### text
**Type:** String
**Default:** `''`
The title text to display.

## Example Usage

The example below would enable a title of 'Custom Chart Title' on the chart that is created.

```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        title: {
            display: true,
            text: 'Custom Chart Title'
        }
    }
})
```

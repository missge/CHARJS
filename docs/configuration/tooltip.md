# Tooltips

## Tooltip Configuration

The tooltip configuration is passed into the `options.tooltips` namespace. The global options for the chart tooltips is defined in `Chart.defaults.global.tooltips`.

### enabled
**Type:** Boolean
**Default:** `true`
Are tooltips enabled.

### custom
**Type:** Function
**Default:** `null`
See [custom tooltip](#custom-tooltips) section.

### mode
**Type:** String
**Default:** `'nearest'`
Sets which elements appear in the tooltip. See [Interaction Modes](../general/interactions/modes.md#interaction-modes) for details.

### intersect
**Type:** Boolean
**Default:** `true`
if true, the tooltip mode applies only when the mouse position intersects with an element. If false, the mode will be applied at all times.

### position
**Type:** String
**Default:** `'average'`
The mode for positioning the tooltip. Possible modes are:
* 'average'
* 'nearest'

'average' mode will place the tooltip at the average position of the items displayed in the tooltip. 'nearest' will place the tooltip at the position of the element closest to the event position. 

New modes can be defined by adding functions to the Chart.Tooltip.positioners map.

### itemSort
**Type:** Function
**Default:** `undefined`
Allows sorting of [tooltip items](#chart-configuration-tooltip-item-interface). Must implement at minimum a function that can be passed to [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort).  This function can also accept a third parameter that is the data object passed to the chart.

### filter
**Type:** Function
**Default:** `undefined`
Allows filtering of [tooltip items](#chart-configuration-tooltip-item-interface). Must implement at minimum a function that can be passed to [Array.prototype.filter](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter). This function can also accept a second parameter that is the data object passed to the chart.

### backgroundColor
**Type:** Color
**Default:** `'rgba(0,0,0,0.8)'`
Background color of the tooltip.

### titleFontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family for tooltip title inherited from global font family.

### titleFontSize
**Type:** Number
**Default:** `12`
Font size for tooltip title inherited from global font size

### titleFontStyle
**Type:** String
**Default:** `'bold'`
Font style for the tooltip title.

### titleFontColor
**Type:** Color
**Default:** `'#fff'`
Font color for tooltip title

### titleSpacing
**Type:** Number
**Default:** `2`
Spacing to add to top and bottom of each title line.

### titleMarginBottom
**Type:** Number
**Default:** `6`
Margin to add on bottom of title section.

### bodyFontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family for tooltip items inherited from global font family

### bodyFontSize
**Type:** Number
**Default:** `12`
Font size for tooltip items inherited from global font size.

### bodyFontStyle
**Type:** String
**Default:** `'normal'`
Font style for the body lines of the tooltip.

### bodyFontColor
**Type:** Color
**Default:** `'#fff'`
Font color for tooltip items.

### bodySpacing
**Type:** Number
**Default:** `2`
Spacing to add to top and bottom of each tooltip item.

### footerFontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family for tooltip footer inherited from global font family.

### footerFontSize
**Type:** Number
**Default:** `12`
Font size for tooltip footer inherited from global font size.

### footerFontStyle
**Type:** String
**Default:** `'bold'`
Font style for tooltip footer.

### footerFontColor
**Type:** Color
**Default:** `'#fff'`
Font color for tooltip footer.

### footerSpacing
**Type:** Number
**Default:** `2`
Spacing to add to top and bottom of each footer line.

### footerMarginTop
**Type:** Number
**Default:** `6`
Margin to add before drawing the footer.

### xPadding
**Type:** Number
**Default:** `6`
Padding to add on left and right of tooltip.

### yPadding
**Type:** Number
**Default:** `6`
Padding to add on top and bottom of tooltip.

### caretSize
**Type:** Number
**Default:** `5`
Size, in px, of the tooltip arrow.

### cornerRadius
**Type:** Number
**Default:** `6`
Radius of tooltip corner curves.

### multiKeyBackground
**Type:** Color
**Default:** `'#fff'`
Color to draw behind the colored boxes when multiple items are in the tooltip

### displayColors
**Type:** Boolean
**Default:** `true`
if true, color boxes are shown in the tooltip

## Tooltip Callbacks

The tooltip label configuration is nested below the tooltip configuration using the `callbacks` key. The tooltip has the following callbacks for providing text. For all functions, 'this' will be the tooltip object created from the Chart.Tooltip constructor.

All functions are called with the same arguments: a [tooltip item](#chart-configuration-tooltip-item-interface) and the data object passed to the chart. All functions must return either a string or an array of strings. Arrays of strings are treated as multiple lines of text.

### beforeTitle
**Arguments:** `Array[tooltipItem], data`
Returns the text to render before the title.

### title
**Arguments:** `Array[tooltipItem], data`
Returns text to render as the title of the tooltip.

### afterTitle
**Arguments:** `Array[tooltipItem], data`
Returns text to render after the title.

### beforeBody
**Arguments:** `Array[tooltipItem], data`
Returns text to render before the body section.

### beforeLabel
**Arguments:** `tooltipItem, data`
Returns text to render before an individual label. This will be called for each item in the tooltip.

### label
**Arguments:** `tooltipItem, data`
Returns text to render for an individual item in the tooltip.

### labelColor
**Arguments:** `tooltipItem, chartInstance`
Returns the colors to render for the tooltip item. Return as an object containing two parameters: `borderColor` and `backgroundColor`.

For example, to return a red box for each item in the tooltip you could do:
```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        tooltips: {
            callbacks: {
                labelColor: function(tooltipItem, chartInstance) {
                    return {
                        borderColor: 'rgb(255, 0, 0)',
                        backgroundColor: 'rgb(255, 0, 0)'
                    }
                }
            }
        }
    }
});
```

### afterLabel
**Arguments:** `tooltipItem, data`
Returns text to render after an individual label.

### afterBody
**Arguments:** `Array[tooltipItem], data`
Returns text to render after the body section

### beforeFooter
**Arguments:** `Array[tooltipItem], data`
Returns text to render before the footer section.

### footer
**Arguments:** `Array[tooltipItem], data`
Returns text to render as the footer of the tooltip.

### afterFooter
**Arguments:** `Array[tooltipItem], data`
Text to render after the footer section

### Tooltip Item Interface

The tooltip items passed to the tooltip callbacks implement the following interface.

```javascript
{
    // X Value of the tooltip as a string
    xLabel: String,

    // Y value of the tooltip as a string
    yLabel: String,

    // Index of the dataset the item comes from
    datasetIndex: Number,

    // Index of this data item in the dataset
    index: Number,

    // X position of matching point
    x: Number,

    // Y position of matching point
    y: Number,
}
```

## External (Custom) Tooltips

Custom tooltips allow you to hook into the tooltip rendering process so that you can render the tooltip in your own custom way. Generally this is used to create an HTML tooltip instead of an oncanvas one. You can enable custom tooltips in the global or chart configuration like so:

```javascript
var myPieChart = new Chart(ctx, {
    type: 'pie',
    data: data,
    options: {
        tooltips: {
            custom: function(tooltipModel) {
                // Tooltip Element
                var tooltipEl = document.getElementById('chartjs-tooltip');

                // Create element on first render
                if (!tooltipEl) {
                    tooltipEl = document.createElement('div');
                    tooltipEl.id = 'chartjs-tooltip';
                    tooltipEl.innerHTML = "<table></table>"
                    document.body.appendChild(tooltipEl);
                }

                // Hide if no tooltip
                if (tooltipModel.opacity === 0) {
                    tooltipEl.style.opacity = 0;
                    return;
                }

                // Set caret Position
                tooltipEl.classList.remove('above', 'below', 'no-transform');
                if (tooltipModel.yAlign) {
                    tooltipEl.classList.add(tooltipModel.yAlign);
                } else {
                    tooltipEl.classList.add('no-transform');
                }

                function getBody(bodyItem) {
                    return bodyItem.lines;
                }

                // Set Text
                if (tooltipModel.body) {
                    var titleLines = tooltipModel.title || [];
                    var bodyLines = tooltipModel.body.map(getBody);

                    var innerHtml = '<thead>';

                    titleLines.forEach(function(title) {
                        innerHtml += '<tr><th>' + title + '</th></tr>';
                    });
                    innerHtml += '</thead><tbody>';

                    bodyLines.forEach(function(body, i) {
                        var colors = tooltipModel.labelColors[i];
                        var style = 'background:' + colors.backgroundColor;
                        style += '; border-color:' + colors.borderColor;
                        style += '; border-width: 2px'; 
                        var span = '<span class="chartjs-tooltip-key" style="' + style + '"></span>';
                        innerHtml += '<tr><td>' + span + body + '</td></tr>';
                    });
                    innerHtml += '</tbody>';

                    var tableRoot = tooltipEl.querySelector('table');
                    tableRoot.innerHTML = innerHtml;
                }

                // `this` will be the overall tooltip
                var position = this._chart.canvas.getBoundingClientRect();

                // Display, position, and set styles for font
                tooltipEl.style.opacity = 1;
                tooltipEl.style.left = position.left + tooltipModel.caretX + 'px';
                tooltipEl.style.top = position.top + tooltipModel.caretY + 'px';
                tooltipEl.style.fontFamily = tooltipModel._fontFamily;
                tooltipEl.style.fontSize = tooltipModel.fontSize;
                tooltipEl.style.fontStyle = tooltipModel._fontStyle;
                tooltipEl.style.padding = tooltipModel.yPadding + 'px ' + tooltipModel.xPadding + 'px';
            }
        }
    }
});
```

See `samples/tooltips/line-customTooltips.html` for examples on how to get started.

## Tooltip Model
The tooltip model contains parameters that can be used to render the tooltip.

```javascript
{
    // The items that we are rendering in the tooltip. See Tooltip Item Interface section
    dataPoints: TooltipItem[],

    // Positioning
    xPadding: Number,
    yPadding: Number,
    xAlign: String,
    yAlign: String,

    // X and Y properties are the top left of the tooltip
    x: Number, 
    y: Number,
    width: Number,
    height: Number,
    // Where the tooltip points to
    caretX: Number,
    caretY: Number,

    // Body
    // The body lines that need to be rendered
    // Each pbject contains 3 parameters
    // before: String[] // lines of text before the line with the color square
    // lines: String[], // lines of text to render as the main item with color square
    // after: String[], // lines of text to render after the main lines
    body: Object[],
    // lines of text that appear after the title but before the body 
    beforeBody: String[],
    // line of text that appear after the body and before the footer
    afterBody: String[],
    bodyFontColor: Color,
    _bodyFontFamily: String,
    _bodyFontStyle: String,
    _bodyAlign: String,
    bodyFontSize: Number,
    bodySpacing: Number,

    // Title
    // lines of text that form the title
    title: String[],
    titleFontColor: Color,
    _titleFontFamily: String,
    _titleFontStyle: String,
    titleFontSize: Number,
    _titleAlign: String,
    titleSpacing: Number,
    titleMarginBottom: Number,

    // Footer
    // lines of text that form the footer
    footer: String[],
    footerFontColor: Color,
    _footerFontFamily: String,
    _footerFontStyle: String,
    footerFontSize: Number,
    _footerAlign: String,
    footerSpacing: Number,
    footerMarginTop: Number,

    // Appearance
    caretSize: Number,
    cornerRadius: Number,
    backgroundColor: Color,

    // colors to render for each item in body[]. This is the color of the squares in the tooltip
    labelColors: Color[],

    // 0 opacity is a hidden tooltip
    opacity: Number,
    legendColorBackground: Color,
    displayColors: Boolean,
}
```

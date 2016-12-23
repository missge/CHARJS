# Line Configuration

Line elements are used to represent the line in a line chart. The global line options are stored in `Chart.defaults.global.elements.line`.

## tension
**Type:** Number
**Default:** `0.4`
Default bezier curve tension. Set to `0` for no bezier curves.

## backgroundColor
**Type:** Color
**Default:** `'rgba(0, 0, 0, 0.1)'`
Default line fill color.

## borderWidth
**Type:** Number
**Default:** `3`
Default line stroke width.

## borderColor
**Type:** Color
**Default:** `'rgba(0,0,0,0.1)'`
Default line stroke color.

## borderCapStyle
**Type:** String
**Default:** `'butt'`
Default line cap style. See [MDN](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/lineCap).

## borderDash
**Type:** Array
**Default:** `[]`
Default line dash. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash).

## borderDashOffset
**Type:** Number
**Default:** `0`
Default line dash offset. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset).

## borderJoinStyle
**Type:** String
**Default:** `'miter`
Default line join style. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin).

## capBezierPoints
**Type:** Boolean
**Default:** `true`
If true, bezier control points are kept inside the chart. If false, no restriction is enforced..

## fill
**Type:** Boolean or String
**Default:** `true`
If true, the fill is assumed to be to zero. String values are 'zero', 'top', and 'bottom' to fill to different locations. If `false`, no fill is added.

## stepped
**Type:** Boolean
**Default:** `false`
If true, the line is shown as a stepped line and 'tension' will be ignored.
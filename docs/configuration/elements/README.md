# Elements

While chart types provide settings to configure the styling of each dataset, you sometimes want to style all datasets the same way. A common example would be to stroke all of the bars in a bar chart with the same colour but change the fill per dataset.

Options can be configured for four different types of elements: arc, lines, points, and rectangles. When set, these options apply to all objects of that type unless specifically overridden by the configuration attached to a dataset.

* [point](./point.md#point-configuratio )
* [line](./line.md#line-configuration)
* [rectangle / bar](./bar.md#rectangle-configuration)
* [arc](./arc.md#arc-configuration)

## Global Configuration

The element options can be specified per chart or globally. The global options for elements are defined in `Chart.defaults.global.elements`. For example, to set the border width of all bar charts globally you would do:

```javascript
Chart.defaults.global.elements.rectangle.borderWidth = 2;
```
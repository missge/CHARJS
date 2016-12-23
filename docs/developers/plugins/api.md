# Plugin API

Plugins must implement the `IPlugin` interface.
```javascript
{
    /**
     * Plugin extension hooks.
     * @interface IPlugin
     * @since 2.1.0
     */

    /**
     * @method IPlugin#beforeInit
     * @desc Called before initializing `chart`.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    beforeInit: function(chart, options) {},

    /**
     * @method IPlugin#afterInit
     * @desc Called after `chart` has been initialized and before the first update.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    afterInit: function(chart, options) {},

    /**
     * @method IPlugin#beforeUpdate
     * @desc Called before updating `chart`. If any plugin returns `false`, the update
     * is cancelled (and thus subsequent render(s)) until another `update` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} `false` to cancel the chart update.
     */
    beforeUpdate(chart, options) {},

    /**
     * @method IPlugin#afterUpdate
     * @desc Called after `chart` has been updated and before rendering. Note that this
     * hook will not be called if the chart update has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    afterUpdate: funciotn(chart, options) {},

    /**
     * @method IPlugin#beforeDatasetsUpdate
     * @desc Called before updating the `chart` datasets. If any plugin returns `false`,
     * the datasets update is cancelled until another `update` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} false to cancel the datasets update.
     * @since version 2.1.5
     */
    beforeDatasetsUpdate: function(chart, options) {},

    /**
     * @method IPlugin#afterDatasetsUpdate
     * @desc Called after the `chart` datasets have been updated. Note that this hook
     * will not be called if the datasets update has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     * @since version 2.1.5
     */
    afterDatasetsUpdate: function(chart, options) {},

    /**
     * @method IPlugin#beforeLayout
     * @desc Called before laying out `chart`. If any plugin returns `false`,
     * the layout update is cancelled until another `update` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} `false` to cancel the chart layout.
     */
    beforeLayout: function(chart, options) {},

    /**
     * @method IPlugin#afterLayout
     * @desc Called after the `chart` has been layed out. Note that this hook will not
     * be called if the layout update has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    afterLayout: function(chart, options) {},

    /**
     * @method IPlugin#beforeRender
     * @desc Called before rendering `chart`. If any plugin returns `false`,
     * the rendering is cancelled until another `render` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} `false` to cancel the chart rendering.
     */
    beforeRender: function(chart, options) {},

    /**
     * @method IPlugin#afterRender
     * @desc Called after the `chart` has been fully rendered (and animation completed). Note
     * that this hook will not be called if the rendering has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    afterRender: function(chart, options) {},

    /**
     * @method IPlugin#beforeDraw
     * @desc Called before drawing `chart` at every animation frame specified by the given
     * easing value. If any plugin returns `false`, the frame drawing is cancelled until
     * another `render` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Number} easingValue - The current animation value, between 0.0 and 1.0.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} `false` to cancel the chart drawing.
     */
    beforeDraw: function(chart, easingValue, options) {},

    /**
     * @method IPlugin#afterDraw
     * @desc Called after the `chart` has been drawn for the specific easing value. Note
     * that this hook will not be called if the drawing has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Number} easingValue - The current animation value, between 0.0 and 1.0.
     * @param {Object} options - The plugin options.
     */
    afterDraw: function(chart, easingValue, options) {},

    /**
     * @method IPlugin#beforeDatasetsDraw
     * @desc Called before drawing the `chart` datasets. If any plugin returns `false`,
     * the datasets drawing is cancelled until another `render` is triggered.
     * @param {Chart} chart - The chart instance.
     * @param {Number} easingValue - The current animation value, between 0.0 and 1.0.
     * @param {Object} options - The plugin options.
     * @returns {Boolean} `false` to cancel the chart datasets drawing.
     */
    beforeDatasetsDraw: function(chart, easingValue, options) {},

    /**
     * @method IPlugin#afterDatasetsDraw
     * @desc Called after the `chart` datasets have been drawn. Note that this hook
     * will not be called if the datasets drawing has been previously cancelled.
     * @param {Chart} chart - The chart instance.
     * @param {Number} easingValue - The current animation value, between 0.0 and 1.0.
     * @param {Object} options - The plugin options.
     */
    afterDatasetsDraw: function(chart, easingValue, options) {},

    /**
     * @method IPlugin#beforeEvent
     * @desc Called before processing the specified `event`. If any plugin returns `false`,
     * the event will be discarded.
     * @param {Chart} chart - The chart instance.
     * @param {IEvent} event - The event object.
     * @param {Object} options - The plugin options.
     */
    beforeEvent: function(chart, event, options) {},

    /**
     * @method IPlugin#afterEvent
     * @desc Called after the `event` has been consumed. Note that this hook
     * will not be called if the `event` has been previously discarded.
     * @param {Chart} chart - The chart instance.
     * @param {IEvent} event - The event object.
     * @param {Object} options - The plugin options.
     */
    afterEvent: function(chart, event, options) {},

    /**
     * @method IPlugin#resize
     * @desc Called after the chart as been resized.
     * @param {Chart} chart - The chart instance.
     * @param {Number} size - The new canvas display size (eq. canvas.style width & height).
     * @param {Object} options - The plugin options.
     */
    resize: function(chart, size, options) {},

    /**
     * @method IPlugin#destroy
     * @desc Called after the chart as been destroyed.
     * @param {Chart} chart - The chart instance.
     * @param {Object} options - The plugin options.
     */
    destroy: function(chart, options) {},
}
```
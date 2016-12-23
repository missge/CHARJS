# Animations

Chart.js animates charts out of the box. A number of options are provided to configure how the animation looks and how long it takes

## Animation Configuration

The following animation options are available. The global options for are defined in `Chart.defaults.global.animation`.

### duration
**Type:** Number
**Default:** `1000`
The number of milliseconds an animation takes.

### easing
**Type:** String
**Default:** `'easeOutQuart`
Easing function to use. Available options are: 
* `'linear'`
* `'easeInQuad'`
* `'easeOutQuad'`
* `'easeInOutQuad'`
* `'easeInCubic'`
* `'easeOutCubic'`
* `'easeInOutCubic'`
* `'easeInQuart'`
* `'easeOutQuart'`
* `'easeInOutQuart'`
* `'easeInQuint'`
* `'easeOutQuint'`
* `'easeInOutQuint'`
* `'easeInSine'`
* `'easeOutSine'`
* `'easeInOutSine'`
* `'easeInExpo'`
* `'easeOutExpo'`
* `'easeInOutExpo'`
* `'easeInCirc'`
* `'easeOutCirc'`
* `'easeInOutCirc'`
* `'easeInElastic'`
* `'easeOutElastic'`
* `'easeInOutElastic'`
* `'easeInBack'`
* `'easeOutBack'`
* `'easeInOutBack'`
* `'easeInBounce'`
* `'easeOutBounce'`
* `'easeInOutBounce'`

See [Robert Penner's easing equations](http://robertpenner.com/easing/).

### onProgress
**Type:** Function
**Default:** `null`
Callback called on each step of an animation. Passed a single argument, an object, containing the chart instance and an object with details of the animation.

### onComplete
**Type:** Function
**Default:** `null`
Callback called at the end of an animation. Passed the same arguments as `onProgress`.

## Animation Callbacks

The `onProgress` and `onComplete` callbacks are useful for synchronizing an external draw to the chart animation. The callback is passed an object that implements the following interface. An example usage of these callbacks can be found on [Github](https://github.com/chartjs/Chart.js/blob/master/samples/animation/progress-bar.html). This sample displays a progress bar showing how far along the animation is.

```javascript
{
    // Chart object
    chartInstance,

    // Contains details of the on-going animation
    animationObject,
}
```


The following example fills a progress bar during the chart animation. 
```javascript
var chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        animation: {
            onProgress: function(animation) {
                progress.value = animation.animationObject.currentStep / animation.animationObject.numSteps;
            }
        }
    }
});
```

### Animation Object

The animation object passed to the callbacks is of type `Chart.Animation`. The object has the following parameters.

```javascript
{
    // Current Animation frame number
    currentStep: Number,

    // Number of animation frames
    numSteps: Number,

    // Animation easing to use
    easing: String,

    // Function that renders the chart
    render: Function,

    // User callback
    onAnimationProgress: Function,

    // User callback
    onAnimationComplete: Function
}
```
# HtmlCanvasQuestions
As you know, canvas technique is a special part in web development unlike 
normal data read and write or page construction. We need some prerequisites which
in connection with math and graphic and more, but it will not prevent you from being
a good javascript developer if you don't master all of them. Don't worry and be confident.

There also have examples for questions which are needed.

---

### Q1:
#### What's the difference between setting canvas's attribute width(height) and canvas css's property width(height)?
A: In default, canvas element was rendered with a 300px height and 150px width in browser, that mean there are 300 pixel cells
and 150 pixel cells respectively in horizontal and vertical directions. If you put a image width 300 * 200 in it with 
top-left corner origin, the bottom part will be clipped, which revealing that pixels were 'not enough'. And if you set css property,
it seems not work, see below:
```html
<canvas id="scene"></canvas>
```
```css
#scene {
    // not solve the 'clipped' question
    width:  300px;
    height: 200px;
}
```
It's because setting `css property` for canvas element only scale the `display size`, and the nums of pixels were not changed.

The correct way is setting the `attribute` for canvas element and change the `rendered area` along with the nums of pixels.
Both of them are valid:
```html
<!--use inline attribute-->
<canvas id="scene" width="300" height="200"></canvas>
```
```js
// with dom api in javascript
const canvas = document.querySelector('#scene');
canvas.width = '300px';
canvas.height = '200px';
```

### Q2: 
#### How to draw a half-pixel in canvas on devices with different resolution?
A: In general, half-pixel on screen is very thin and not easy to recognize. Unless you need to implement some special
effects or else it's not suggested to do that(at least i don't think it's necessary). Anyway, you can do this by scale
down the element's display size, so that the visible pixels will be 'squeezed'. See below:
```html
<canvas id="scene"></canvas>

<style>
    #scene {
        // or you can set the css property 'width' and 'height' for canvas element explicitly
        transform: scale(0.5);
    }
</style>
```

### Q3:
#### What are the differences between `setInterval` and `requestAnimationFrame`?
A: They all tell browser to do something on a regular basis, `setInterval` receive two arguments and `requestAnimationFrame`
receive only one, and there are canceled functions for both of them.
```js
const intervalId = setInterval(callback, delay);
clearInterval(intervalId);

const animationId = requestAnimationFrame(timestamp => {});
cancelAnimationFrame(animationId);
```
Developer can specify a period to `setInterval`, and it follows the `Event Loop` principle, that means if there
are many javascript tasks in the queue before your callback, you have to wait until the queue is empty, which mean the `delay`
arguments don't represent the real period but a minimum interval.

However, `requestAnimationFrame` is handled automatically by the browser, that means browser will execute the given callback
function 60 times a minute, which can insure the animation be smooth. Besides, there is an argument which represents the timestamp
pass to the callback function, and developer can calculate the processing of animation or do something control.

In conclusion, `requesetAnimationFrame` is better than `setTimeInterval` when making animation.
>TODO: `MDN` said requestAnimationFrame on high-resolution screen will execute faster than on other screens. I created a simple
> demo but found that there was subtle difference between the time shift on different resolutions of screen.

### Q4:
#### What is `devicePixelRatio` and when to utilize it? 
A: this property is on the global object `window`, and it represents the ratio of physical pixel to css pixel, or you can
say the pixel 'density'. High resolution devices usually have higher `devicePixelRatio` than other devices with regular resolution.

A way to resolve the fuzzy canvas on screen is as below(something similar to half pixel issue):
```html
<canvas id="scene"></canvas>
```
```js
// you can specify more render pixels to the canvas, and give it original display size
const canvas = document.querySelector('#scene');
const size = 200;
canvas.style.width = `${size}px`;
canvas.style.height = `${size}px`;

if(window.devicePixelRatio > 1) {
    // use Math.floor casue devicePixelRatio is a double-precision floating point number
    canvas.width = Math.floor(size * window.devicePixelRatio); 
    canvas.height = Math.floor(size * window.devicePixelRatio); 
}
```

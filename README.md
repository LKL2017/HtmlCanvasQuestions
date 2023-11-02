# HtmlCanvasQuestions
As you know, canvas technique is a special part in web development unlike 
normal data read and write or page construction. We need some prerequisites which
in connection with math and graphic and more, but it will not prevent you from being
a good javascript developer if you don't master all of them. Don't worry and be confident.

There also have examples for questions which are needed.

---

### #1
#### Q: What's the difference between setting canvas's attribute width(height) and canvas css's property width(height)?
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

### #2 
#### Q: How to draw a half-pixel in canvas on devices with different resolution?
> TODO 

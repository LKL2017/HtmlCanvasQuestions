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
#### What are the differences between `setTimeout` and `requestAnimationFrame`?
> TODO

### Q4:
#### What is `devicePixelRatio` and when to utilize it? 
> TODO

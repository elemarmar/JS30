# 02 - CSS & JS Clock

![cover](cover.png)

The purpose of this project was to build a simple clock with CSS and plain JavaScript. 



## Learning

S

- `Date()` method
- `transform` property



<br>



## Structure and goal

The clock has three `div` that represent each hand of the clock:

- `<div class="hand hour-hand">`
- `<div class="hand min-hand">`
- `<div class="hand second-hand">`



🎯 We want to rotate each `div` depending on what time it currently is.



## Process

- We want the hands to rotate on the end and not from the middle -> we transform the origin (from where it is going to apply alll transformations, including rotate)

```css
.hand {
  width: 50%;
  height: 6px;
  background: black;
  position: absolute; 
  top: 50%;
  transform-origin: 100%; 👈🏻
  transform: rotate(90deg); /* so all hands start at 12:00 */
}
```

By default, `transform-origin` is 50%. 10% along the X axis, puts it on the right side.





Adding a transition so that the change is more "clock-like". We use `transition-timing-function` to make the movement more real

```css
.hand {
  ...
  transition: all 0.05s;
  transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
}
```



JAVASCRIPT part



Second hand:

```js
const elements = {
  secondHand = document.querySelector('.second-hand');
}
```

Create a function that gets all elements 

```js
function setDate() {
  const now = new Date();
  const seconds = now.getSeconds();
  const secondsDegrees = ((seconds / 60) * 360) + 90; // because we set original deg to 90deg
  
  elements.secondHand.style.transform = `rotate(${secondsDegrees}deg);
}

setInterval(setDate, 1000);
```

We want the function that sets the date to run every second so that we can update our clock every second

Seconds now will go from 0  to 59



---

<br>


ℹ️ This project was based on one of Wes Bos' [JavaScript 30](https://javascript30.com/) challenges.
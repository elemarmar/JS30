# 01 - Drum Kit 

- data-* attributes

* keyCode s
* this
* Listen to transitionend event
* `this` keyword in events
* 





1. We listen for keydown event on the window

```js
window.addEventListener('keydown', (ev) => {
  // Is there an audio element on the page that has a `data-key` of ev.keyCode?
	const pressedKey = ev.keyCode;
  const audio = document.querySelector(`audio[data-key=" ${pressedKey}"]`);
  if(!audio) return; // stop frunction frmo running
  audio.currentTime = 0; // rewind to the start
  audio.play();
});
```

- Want to find out if there is an audio element on the page that has a data-key of èv.keyCode` which is the code of the key that we pressed.

- `id(!audio) return` stops the function from running altogether
- We can play the audio element with `audio.play()` ⚠️ if you play on an audio that is already play, it won't play --> we want to rewind it to the start `audio.currentTime = 0;



2. Taking care of the classes change

```js
function playSound(ev) {
  const pressedKey = ev.keyCode;
  const audio = document.querySelector(`audio[data-key="${pressedKey}`);
  const key = document.querySelector(`.key[data-key="${pressedKey}`);

  if (!audio) return; // stop function from running

  // Play audio
  audio.currentTime = 0;
  audio.play();

  // Change class
  key.classList.add('playing');
}

function removeTransition(ev) {
  if (ev.propertyName !== 'transform') return; // skip funciton if it's not 'transform'
  this.classList.remove('playing');
}

// Event listeners
window.addEventListener('keydown', playSound);
const keys = document.querySelectorAll('.key');
keys.forEach((key) =>
	key.addEventListener('transitionend', removeTransition)
;
```

- We select the key element that we see on the screen (different from the audio element) 
- Transition end event that fires when it has stopped animating itself
  - Listen on in each key for when the transition end happens
  - We normally take the longest one -> transform
  - We use `this` which in this case is the element that the event was run in





Why is this that and not the window object? It's a regular function



----



Changes introduced:

- Gradient animated background with stars that changes colours every time a key is pressed
  - Start on black -> each time user presses a key, start animation and change color



- [ ] Change title font and make it responsive
- [ ] Change style of keys (circles? Border collars, transition color)
- [ ] Add description and link top left/right
- [ ] Add copyright footer
- [ ] Move stars from background




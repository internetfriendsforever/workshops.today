# Interactive animations

Building on the previous tutorial [Making interactions](02-making-interactions.md), we will learn how to make simple interactive animations (☞☟☜) using HTML and plain JavaScript.


## Our starting point

Create a new HTML document and copy/paste the following code:  

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)
    document.body.style.margin = 0

    canvas.width = window.innerWidth
    canvas.height = window.innerHeight

    var distance = 0

    function draw (time) {
      var x = Math.sin(time)
      var y = canvas.height / 2

      context.beginPath()
      context.arc(x, y, 10, 0, Math.PI * 2)

      context.fillStyle = 'white'
      context.fill()

      context.strokeStyle = 'black'
      context.stroke()
      
      window.requestAnimationFrame(draw)
    }

    canvas.addEventListener('mousemove', function (event) {
      distance = event.clientY
    })

    draw(0)
  </script>
</body>
```

Most of this should be familiar to you from based on the previous tutorial. Running the code in your browser should produce a blank `canvas` streched as wide and tall as our browser window.


## Listening for user input

To make our `canvas` interactive, we first need to listen for user input. In the browser, user input comes in the form of _events_.

Let's add our first event listener:

```js
canvas.addEventListener('mousedown', function (event) {
  console.log(event)
})
```

Here, we are using a special function called `addEventListener` on our `canvas`. We are passing in two arguments:

- The first argument specifies what type of event to listen for. In this case we are listening for when the mouse pointer is pressed down: this event is called `'mousedown'`
- The second argument specifies a function that will run every time the event occurs

Let's save our file and reload the page in our browser.

Every time you press your mouse pointer down on the `canvas`, you should see an event object being logged to the developer console.

We've made our first interactive program!


## Reacting to user input

In order to close the feedback loop, we should react to the user's input. This can be done in many ways, but since we already know how to draw on the canvas, let's create something visual:

```js
canvas.addEventListener('mousedown', function (event) {
  console.log(event)
  context.strokeRect(event.clientX, event.clientY, 10, 10)
})
```

Your program should now draw a black rectangle wherever you press the mouse pointer on the `canvas`. How is this done?

The event object has lots of information about what just happened. In our example we are using `event.clientX` and `event.clientY` to draw a rectangle where the mouse pointer was pressed.

Try changing `'mousedown'` to `'mousemove'` and see what happens.

### Events and values

All [mouse event](https://developer.mozilla.org/en-US/docs/Web/Events#Mouse_events) objects can tell us the position of the mouse pointer in relation to the browser window as `event.clientX` and `event.clientY`.

They can also tell us whether the shift, alt, control or command/meta key have been held during the event: `event.shiftKey`, `event.altKey`, `event.ctrlKey`, `event.metaKey`.

There are other events and values that might be interesting to experiment with:

The `'mousedown'` and `'mouseup'`, `'click'` and `'dblclick'` events can tell us which mouse button was pressed with the `event.button` value.

The `'wheel'` event can tell us which direction and how much the user scrolled since the last event with the values `event.deltaX` and `event.deltaY`.

```js
canvas.addEventListener('mousemove', function (event) {
  console.log(event.clientX, event.clientY)
})

canvas.addEventListener('wheel', function (event) {
  console.log(event.deltaX, event.deltaY)
})
```

When you move your mouse and scroll you should see some values logged out in your developer console.

### Combining events

Using events together can open up for new variations in you program. We can for example change the size of our rectangle when the user scrolls:

```js
var x = 0
var y = 0
var size = 5

function draw () {
  context.strokeRect(x, y, size, size)
}

canvas.addEventListener('mousemove', function (event) {
  x = event.clientX
  y = event.clientY
  draw()
})

canvas.addEventListener('wheel', function (event) {
  size = size + event.deltaY
  draw()
})
```

Since we want to draw both when `'mousemove'` and `'wheel'` happens, we have separated our drawing code into a draw function. We can then tell our program to `draw()` every time each of the events happen.

Instead of drawing our rectangle with a fixed size and position, we are storing `size`, `x` and `y` as variables and using them to draw with.

Every time the `'wheel'` event happens, we change the `size` by adding the `event.deltaY` value to it. And every time the `'mousemove'` event happens, we are changing the `x` and `y` variables.

As we can see in our example:
- _variables_ enable us to store and use values in different parts of our program
- _functions_ enable us to group code together and run it in different parts of our program


## A complete example

By using events, functions, variables and feedback we can create complex interactive systems:

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)
    document.body.style.margin = 0

    canvas.width = window.innerWidth
    canvas.height = window.innerHeight

    var x = 0
    var y = 0
    var size = 5
    var circle = false

    function draw () {
      if (circle) {
        context.beginPath()
        context.arc(x, y, Math.abs(size), 0, Math.PI * 2)
        context.stroke()
      } else {
        context.strokeRect(x, y, size, size)
      }
    }

    canvas.addEventListener('mousemove', function (event) {
      x = event.clientX
      y = event.clientY
      draw()
    })

    canvas.addEventListener('wheel', function (event) {
      size = size + event.deltaY
      draw()
    })

    canvas.addEventListener('click', function (event) {
      circle = !circle
      draw()
    })
  </script>
</body>
```

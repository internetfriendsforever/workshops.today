# Making interactions

Building on the previous tutorial [Drawing graphics](01-drawing-graphics.md), we will learn how to make simple interactions (☞☟☜) using HTML and plain JavaScript.

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

- The first argument specifies what type of event to listen for. In this case we are listening for when the mouse pointer is pressed down: this event is called `mousedown`
- The second argument specifies a function that will run every time the event occurs

Let's save our file and reload the page in our browser.

Every time you press your mouse pointer down on the `canvas`, you should see an event object being logged to the developer console.

We've made our first interactive program!

<!-- ## Closing the feedback loop

To make something visual

The next natural step is reacting to the user's input.

To make our program exciting to use.... -->


## Reacting to user input

In order to close the feedback loop, we should react to the user's input. This can be done in many ways, but since we already know how to draw on the canvas, let's create something visual:

```js
canvas.addEventListener('mousedown', function (event) {
  console.log(event)
  context.fillRect(event.clientX, event.clientY, 10, 10)
})
```

Your program should now draw a black square wherever you press the mouse pointer on the `canvas`. How is this done?

The event object has lots of information about what just happened. In our example we are using `event.clientX` and `event.clientY` to draw a square where the mouse pointer was pressed.

Try changing `mousedown` to `mousemove` and see what happens.

<!-- There are many types of events, let's try changing `mousedown` to `mousemove` and see what happens. -->



<!-- ### Events

In the example above we tell the document function `addEventListener` to listen to the `mousedown` event, and then we pass in a second argument which is a new function (that we make up) that will be able to do something every time `mousedown` happens.

#### What does an event look like?

If you look closely, you'll see that in our example, we draw a rectangle with `context.fillRect(event.clientX, event.clientY, 10, 10)` but instead of defining the position (`x` and `y`) manually, we are using the values `event.clientX` and `event.clientY` that come from the event.

We happen to know that these values gives us the current position of the mouse cursor. But maybe the event has other values? Let's look under the hood.

Inside of your event listener function, add our trusty old helper the `console.log()` function, passing `event` as the first argument.

```js
document.addEventListener('mousedown', function (event) {
  console.log(event)
  context.fillRect(event.clientX, event.clientY, 10, 10)
})
```

This will log out the event object in your browser's web inspector, feel free to have a little look at the different values.

When you click your mouse again, you'll see that it logs another `event` object to the console. -->

## Other types of events

There are types of events for touch, keyboard, stylus, sensor, and more, but in this tutorial, we will be focusing on a few mouse-specific events: `mousedown`, `mousemove`, `mouseup` and `wheel`.

MDN has a [full list of mouse events](https://developer.mozilla.org/en-US/docs/Web/Events#Mouse_events) and descriptions.

We can try to change our code to listen to the `mousemove` event instead:

```js
document.addEventListener('mousemove', function (event) {
  console.log(event)
  context.fillRect(event.clientX, event.clientY, 10, 10)
})
```

Reload your file in the browser. You've made your first drawing program!

From programming drawings, to programming programs for drawing drawings.

## ....
And for fun, we are also changing the color of our rectangle to sea green by writing `context.fillStyle = 'seagreen'`. This could be any [named color](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#colors_table) or a hexadecimal value like '#f00'.

If you refresh the browser you should now be able to draw using the whole window as a surface.

## Drawing with a mirror

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)
    document.body.style.margin = 0
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight

    document.addEventListener('mousemove', function (event) {
      context.fillStyle = 'seagreen'
      context.fillRect(event.clientX, event.clientY, 10, 10)
      context.fillRect(window.innerWidth-event.clientX, event.clientY, 10, 10)
    })
  </script>
</body>
```

By drawing two rectangles at the same time, one opposite the other, we create an interesting mirror effect.

This affects the way we interact with our program quite a lot. Go to your browser to refresh and try for yourself!



## More interaction

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)
    document.body.style.margin = 0
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight

    var color = 'seagreen'

    document.addEventListener('mousemove', function (event) {
      context.fillStyle = color
      context.fillRect(event.clientX, event.clientY, 10, 10)
      context.fillRect(window.innerWidth-event.clientX, event.clientY, 10, 10)
    })

    document.addEventListener('mousedown', function (event) {
      if (color === 'seagreen') {
        color = 'black'
      } else {
        color = 'seagreen'
      }
    })
  </script>
</body>
```


## What else can you think of?

# Making interactions

Building on the previous tutorial [Drawing graphics](01-drawing-graphics.md), we will learn how to make simple interactions (☞☟☜) using HTML and plain JavaScript.

## A simple example
Simple example copy/paste and run in browser

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)

    canvas.width = 500
    canvas.height = 500

    document.addEventListener('mousedown', function (event) {
      context.fillRect(event.clientX, event.clientY, 10, 10)
    })
  </script>
</body>
```

What is going on in this piece of code?

You're already be familiar with variables. You know how to change the size of your `canvas`.

You've at least heard about the omnipresent `document` object, and maybe you remember that it has lots of useful functions for doing things (to our document).

To make interactions possible we need to know about events.

### Events

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

When you click your mouse again, you'll see that it logs another `event` object to the console.

#### Kinds of events

There are types of events for touch, keyboard, stylus, sensor, and more but for the sake of simplicity, we will be focusing on some mouse-specific events like: `mousedown`, `mousemove`, `mouseup` and `wheel`.

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

## Making our canvas window sized

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
    })
  </script>
</body>
```

A few different things have changed here:

We are setting `document.body.style.margin` to `0` so we get rid of the little border around our `canvas`.

Then, we are specifying the width and height of our `canvas` to be the same as the `window.innerWidth` and `window.innerHeight`. This makes the `canvas` as big as the window.

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

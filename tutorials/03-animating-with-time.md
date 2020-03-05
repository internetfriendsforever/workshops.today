# Animating with time

Building on the previous tutorials [Drawing graphics](01-drawing-graphics.md) and [Making interactions](02-making-interactions.md), we will learn how to animate our programs with time (↻⤸⤾⟳) using HTML and plain JavaScript.

If we introduce the concept of time, or a clock into our program, we can make things move independently of interaction.

A nice way to get a clock tick into your code is a function called `window.requestAnimationFrame`. This will send in a clock tick as the first argument to your function every time the browser is ready to update. On modern computers this aims to be around every 60th of a second or every ~16.67ms.

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)
    document.body.style.margin = 0

    canvas.width = window.innerWidth
    canvas.height = window.innerHeight

    var x = canvas.width / 2
    var y = canvas.height / 2
    var size = 10

    function draw (tick = 0) {
      var positionY = Math.sin(tick / 300) * 50
      var positionX = Math.cos(tick / 300) * 150

      context.clearRect(0, 0, canvas.width, canvas.height)
      context.beginPath()
      context.arc(x + positionX, y + positionY, Math.abs(size), 0, Math.PI * 2)
      context.fill()

      window.requestAnimationFrame(draw)
    }

    draw()
  </script>
</body>
```

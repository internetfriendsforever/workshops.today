# Drawing graphics

We will learn how to draw elementary graphic forms (▲ ◼ ●) using HTML and plain JavaScript.

## Prepare your tools

Download and install the following tools on your computer:

- We write code using a _text editor_. You can use any plain text editor. In these tutorials we will be using  [Atom](https://atom.io/).
- Our programs will run in a _web browser_. You can use any modern web browser, but for this tutorial we are using [Google Chrome](https://www.google.com/chrome/). If you've already installed it, make sure it is up-to-date.

## Create an HTML document

1. Make a folder on your computer called `ppp`
2. Open the folder in the text editor
3. Create a new file in `ppp` called `index.html`
  - Right-click `ppp` in the left-hand column
  - Click _New file_
  - Type in `index.html` and press return on your keyboard
4. Write the following into the right-hand column:

```html
<body>
  Hello, this is a html document
</body>
```

5. Save the file (keyboard shortcut `⌘ + s` on Mac, `ctrl + s` on Windows or Linux)
6. Go to the `ppp` folder on your computer
7. Open the `index.html` file in the web browser
8. You should see your HTML document presented in the web browser

HTML is code used to describe a document. In it we use a standard set of _elements_. An HTML element looks like `<em>this</em>` it has an opening _tag_ and a closing _tag_. Content written in HTML is static – meaning the document doesn't change by itself.

## Writing our first program

The `script` element is a special element where we can write programs to dynamically change our document while it is open in a browser. These programs are written in a language called JavaScript. With it we can (amongst other things):

- create and manipulate document elements
- do calculations
- listen and react to user interaction

1. Let's add a `script` element to our document:
```html
<body>
  <script>
  </script>
</body>
```

2. Save
3. Reload the page in the web browser (nothing happens)
4. In order to see that the script is actually running, we can use the _console_. In Mozilla Firefox: `Tools -> Web Developer -> Web Console` (keyboard shortcut `⌥ + ⌘ + k`)
5. Write a message to the console:
```html
<body>
  <script>
    console.log('hello javascript')
  </script>
</body>
```

6. Save and reload the browser
7. You should see the message in the console

Although we're going to be writing programs that produce a visual output, sometimes, the program just doesn't do what we wanted or thought it would do. The console is a great way to check what's going on in the code. Examples can be: is my code even running? How many times is this happening? When is this happening? What is the value of this variable? and so on.

The console is also the main place to check for errors in your code, sometimes it can be a simple typo, and other times you'll be trying to do something that isn't possible. The console is your friend, keep it open all the time, while writing your programs. If the output is too cryptic, you can copy the error message and search online or ask one of us.

Let's make an error:

8. Go back to Atom and remove the closing bracket `)` from your code
9. Save and reload the page
10. You should see the red error in the console

## Drawing on a canvas

To make something visual, we will draw on an element called `canvas`. It is a special element for generating graphics.

1. Let's create a `canvas` element and add it to our document:

```html
<body>
  <script>
    var canvas = document.createElement('canvas')

    document.body.appendChild(canvas)

    console.log(canvas)
  </script>
</body>
```

2. In the console of the browser, mouse over `<canvas />` to see an outline of the element in the document
3. The `canvas` element has two different ways to draw: `2d` and `webgl`. We will focus on the `2d` context, and fill a rectangle:

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)

    context.rect(10, 10, 50, 50)
    context.fill()
  </script>
</body>
```

4. Save, reload your browser and see a black square!

So, what is going on here?

### Variables

When we write `var canvas = ...`, we are declaring a _variable_. A variable is a reference to something. Like a name is for a person. Examples of things a variable can reference can be: numbers, text (strings), lists (arrays), elements, objects. In this case, we are creating a variable called `canvas`. You could call it almost anything, as long as it does not contain any spaces.

### Functions

When there's a word followed by round brackets `()`, it means that we're using a function.

When we write `document.createElement('canvas')`, the `document` part is a variable referencing the _HTML document_. The `document` object has many functions that we can use, for example for creating elements.

Let us try a metaphor:

Imagine the `document` to be a building. Inside the building, there are many different machines. There is a particular vending machine called `createElement`. We're interested in drawing, so we press the button that reads `canvas`. Moments later, the vending machine does what it does best, and vends a stretched canvas, fully assembled and ready for us to use!

So, in order to make a _canvas element_ we are using a _function_ called `createElement`, available to us from the omnipresent _document_ object.

#### Arguments

Some functions require special instructions to do their job. In the case of `rect`, it needs to know what position and what size it should be. We give these instructions, or _arguments_ inside the round brackets.

Arguments need to be passed to the function in order, and for `rect` that order happens to be `x, y, width, height`.

Writing `rect(10, 10, 50, 50)` is telling the function to start at position `10`, `10`, and make it `50` wide and `50` tall.

## Drawing more shapes

We can draw more shapes by using a few other functions

A line:
```javascript
context.beginPath()
context.moveTo(100, 0)
context.lineTo(200, 100)
context.stroke()
```

A triangle:
```javascript
context.beginPath()
context.moveTo(100, 50)
context.lineTo(125, 100)
context.lineTo(75, 100)
context.closePath()
context.stroke()
```

A circle:
```javascript
context.beginPath()
context.arc(200, 20, 15, 0, Math.PI * 2)
context.fill()
```


## Loops

When programming, it is very useful to be able to tell the computer to do something many times. Instead of writing it over and over, we can use a `for` loop:

```javascript
for (var column = 0; column < 8; column += 1) {
  console.log(column)
}
```

In your console, you will see that the `console.log` is running eight times, from 0 to 7. In essence, it is a counting machine!

The `for` loop is described in three parts separated by the `;` sign:
1. Declare a variable called `column` with a start value of `0`
2. Loop while `column` is less than `8`
3. At the end of each loop, increment `column` by `1`

With it, we can make eight rectangles in a sequence:

```javascript
for (var column = 0; column < 8; column += 1) {
  var x = column * 20
  context.rect(x, 0, 15, 15)
  context.fill()
}
```

If we make another loop around our first loop, we can make a grid:

```javascript
for (var row = 0; row < 7; row += 1) {
  for (var column = 0; column < 8; column += 1) {
    var x = column * 20
    var y = row * 20
    context.rect(x, y, 15, 15)
    context.fill()
  }
}
```

Now, we have a neat 8x7 grid of black squares!

## Variation

We will use two different ways of adding variation to our grid:

### Calculations

As you may already have noticed, we have defined the position of each black square to be:

```javascript
var x = column * 20
var y = row * 20
```

We make the variable `x` to be whatever `column * 20` is. In order to see what the calculation is, you can log the variable to the console:

```javascript
console.log(x)
```

All basic math operators are available to us using the following signs:
- `+` Add
- `-` Subtract
- `*` Multiply
- `/` Divide
- `**` Exponent
- `%` Modulo

There are also several interesting math functions that we can use:

- `Math.random()` — Returns a random number between 0–1. Useful for creating noise
- `Math.sin(number)` — Returns the sine of a number. Useful for creating waves
- `Math.round(number)` — Returns the closest whole number of a decimal number
- `Math.floor(number)` – Rounds *down* to a whole number
- `Math.ceil(number)` – Rounds *up* to a whole number

Be creative, experiment with different equations, even if you don't know what you're doing:

```javascript
var x = column * 20 + Math.sin(row) * 50 + 70
var y = row * 20
var size = Math.random() * 10 + 2

context.rect(x, y, size, size)
```

### If/else conditions

Another way of adding variation is to not always do the same thing:

```js
context.beginPath()

if (row < 2) {
  context.rect(x, y, size, size)
} else {
  context.arc(x, y, size, 0, Math.PI * 2)
}

context.fill()
```

So, _if_ the variable `row` is less than `2`, we draw a rectangle — _else_, we draw a circle.

The part `row < 2` is called a _condition_.

We can use some special symbols in conditions:

- `===` is equal to
- `<` is less than
- `>` is greater than
- `<=` is less than or equal to
- `>=` is greater than or equal to
- `&&` which means _and_
- `||` which means _or_

Other examples:

```
if (row < 2 && column === 3)
```
if `row` is less than `2` _and_ `column` is equal to `3`

```
if (row === 0 || row === 3)
```
if `row` is equal to `0` _or_ if `row` is equal to `3`

## A complete example

```html
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)

    canvas.width = 500
    canvas.height = 500

    for (var row = 0; row < 30; row += 1) {
      for (var column = 0; column < 20; column += 1) {
        var x = column * 20 + Math.sin(row / 2) * 20 + 10
        var y = row * 20
        var width = 10
        var height = Math.random() * 10

        if (column === 8 || column === 9 || row < 7) {
          x = x - Math.random() * 70
        }

        context.beginPath()

        if (row < 5 || row > 16) {
          context.rect(x, y, width, height)
        } else {
          context.arc(x, y, 2, 0, Math.PI * 2)
        }

        context.fill()
      }
    }
  </script>
</body>
```

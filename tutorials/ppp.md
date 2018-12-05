# Posters, Patterns, Programs

We will learn how to draw elementary graphic forms (▲ ◼ ●) using HTML and plain JavaScript

## Prepare your tools

Download and install the following tools on your computer:

- We write code using a _text editor_. You can use any plain text editor. In these tutorials we will be using  [Atom](https://atom.io/).
- Our programs will run in a _web browser_. You can use any modern web browser, but for this tutorial we are using [Google Chrome](https://www.google.com/chrome/). If you've already installed it, make sure it is up-to-date.

## Create a HTML document

1. Make a folder on your computer called `ppp`
2. Open the folder in the text editor
3. Create a new file in `ppp` called `index.html`
  - Right-click `ppp` in the lef-hand column
  - Click `New file`
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

## JavaScript and the console

1. We can use JavaScript in our document by adding a `script` element:
```html
<body>
  <script>
  </script>
</body>
```

3. Save
2. Reload the page in the web browser (nothing happens)
3. In order to see that the script is actually running, we can use the _console_. In Google Chrome: `View -> Developer -> JavaScript console` (keyboard shortcut `alt + cmd + j`)
4. Write a message to the console:
```html
<body>
  <script>
    console.log('hello javascript')
  </script>
</body>
```

5. Save and reload the browser
6. You should see the message in the console

Although we're going to be writing programs that produce a visual output, sometimes, the program just doesn't do what we wanted or thought it would do. The console is a great way to check what's going on in the code. Examples can be: is my code even running? How many times is this happening? When is this happening? What is the value of this variable? and so on.

The console is also the main place to check for errors in your code, sometimes it can be a simple typo, and other times you'll be trying to do something that isn't possible. The console is your friend, keep it open all the time, while writing your programs. If the output is too cryptic, you can copy the error message and search online or ask one of us.

Let's make an error:

1. Go back to Atom and remove the closing bracket `)` from your code
2. Save and reload the page
3. You should see the red error in the console

## Drawing on a canvas

To make something visual, we will draw on an element called `canvas`

1. Let's create a `canvas` element and add it to the document:

```javascript
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

```javascript
<body>
  <script>
    var canvas = document.createElement('canvas')
    var context = canvas.getContext('2d')

    document.body.appendChild(canvas)

    context.fillRect(10, 10, 50, 50)
  </script>
</body>
```

TODO: Explain variables, functions and parameters

TODO: Explain html-javascript-canvas relationship (diagram?)

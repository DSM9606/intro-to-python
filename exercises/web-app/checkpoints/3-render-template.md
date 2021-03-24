
# Web App Checkpoint 3 - Rendering HTML Templates

So far our app is just displaying some simple text when we visit each route. But we have the opportunity to display entire pages written in HTML.

Let's update the home routes to use the `render_template` function from Flask, and choose which files to render.

```py
# web_app/routes/home_routes.py

from flask import Blueprint, render_template

home_routes = Blueprint("home_routes", __name__)

@home_routes.route("/")
def index():
    print("VISITED THE HOME PAGE")
    #return "Welcome Home (TODO)"
    return render_template("home.html")

@home_routes.route("/about")
def about():
    print("VISITED THE ABOUT PAGE")
    #return "About Me (TODO)"
    return render_template("about.html")

@home_routes.route("/users/new")
def register():
    print("VISITED THE REGISTRATION PAGE")
    return "Sign Up for our Product! (TODO)" # we'll make an HTML template for this later!
```

Here we are referencing two HTML files, called "home.html" and "about.html". Flask wants to look in a specific directory called "templates" for these files. So let's create a new directory in the "web_app" directory called "templates" and insert the following files inside:

Inside "web_app/templates/home.html":

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My App</title>
</head>
<body>

    <h1>This is a heading</h1>

    <p>This is a paragraph text</p>

    <ul>
        <li>First list item</li>
        <li>Second list item</li>
        <li>Third list item</li>
    </ul>

</body>
</html>
```

Inside "web_app/templates/about.html":


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My App</title>
</head>
<body>

    <h1>About Me</h1>

    <p>todo write some stuff here</p>

</body>
</html>
```


> FYI: we actually created the code in both of these HTML files by leveraging the auto-completion capabilities of our text editor. When we create a file with a ".html" extension, if we start to write the word "html" in that file, we'll see the ability to generate an entire "html:5" document skeleton (which you see above).

Restart your server and view the app in the browser and see the complete HTML pages!

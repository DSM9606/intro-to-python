# Web App Checkpoint 6 - Web Forms, POST Requests, and Flash Messaging


Our web app is looking good, but its functionality is still basic. Let's take full advantage of our data capture capabilities via a web form.

In the templates directory, add a new HTML file called "new_user_form.html" and place inside the following contents:

```html
{% extends "bootstrap_layout.html" %}
{% set active_page = "new_user" %}

{% block content %}

    <h1>New User Registration Form</h1>

    <p>Please use the form below to register...</p>

    <form action="/users/create" method="POST">

        <label>Full Name:</label>
        <input type="text" name="full_name" placeholder="Example User" value="Example User">
        <br>

        <label>Email Address:</label>
        <input type="text" name="email_address" placeholder="me@example.com" value="me@example.com">
        <br>

        <label>Country:</label>
        <select name="country">
            <option value="US" selected="true">United States</option>
            <option value="UK">United Kingdom</option>
            <option value="Japan">Japan</option>
            <option value="UAE">United Arab Emirates</option>
        </select>
        <br>

        <button>Submit</button>
    </form>

{% endblock %}
```

The HTML `<form>` elements are kind of magical. We can use them to issue HTTP requests to a given URL when the user clicks the `<button>` element inside the form. Focus on the form's `action` and `method` attributes. Here, we're saying that when the user submits the form, we'll send their data via POST request to a new route called "/users/create". So let's update our routes now:

```py
# web_app/routes/home_routes.py

from flask import Blueprint, render_template, redirect, request, flash

# ...

@home_routes.route("/users/new")
def register():
    print("VISITED THE REGISTRATION PAGE")
    return render_template("new_user_form.html")

@home_routes.route("/users/create", methods=["POST"])
def create_user():
    print("FORM DATA:", dict(request.form))
    # FYI: we are able to access the form data via the "request" object we import from flask
    # ... these keys correspond with the "name" attributes of each <input> element in the form!
    #> {'full_name': 'Example User', 'email_address': 'me@example.com', 'country': 'US'}

    user = dict(request.form)
    # todo: store in a database or google sheet!

    # FYI: "warning", "primary", "danger", "success", etc. are bootstrap color classes
    # ... see https://getbootstrap.com/docs/4.3/components/alerts/
    # ... and the flash messaging section of the "bootstrap_layout.html" file for more details
    flash(f"User '{user['full_name']}' created successfully! (TODO)", "warning")
    return redirect("/")
```

Right now this route is demonstrating its ability to print the captured user registration information, but not doing much else with it. Maybe in the future we could store it in a database, or send it in an email to a systems administrator, to facilitate the user's ability to use our system in certain ways.

But in the meantime, we are displaying a success message to the user, and redirecting them to the homepage, for an example experience that a user might be expecting. This is primarily just to demonstrate flash messaging and redirection capabilities.

Restart the server and visit "localhost:5000/users/new" to begin the registration flow! And check the server logs to verify everything is working as desired.

# SENDING FORM DATA

This article looks at what happens when a user submits a form — where does the data go, and how do we handle it when it gets there?

First, we'll discuss what happens to the data when a form is submitted.

## Client/server architecture

At its most basic, the web uses a client/server architecture that can be summarized as follows: a client (usually a web browser) sends a request to a server using the HTTP protocol. The server answers the request using the same protocol.

## On the client side: defining how to send the data

The \<form\> element defines how the data will be sent. All of its attributes are designed to let you configure the request to be sent when a user hits a submit button. The two most important attributes are `action` and `method`.

### The action attribute

The `action` attribute defines where the data gets sent. Its value must be a valid relative or absolute URL.

When specified with no attributes, the \<form\> data is sent to the same page that the form is present on.

The names and values of the non-file form controls are sent to the server as `name=value` pairs joined with ampersands. The `action` value should be a file on the server that can handle the incoming data, including ensuring server-side validation. The server then responds.

### The method attribute

The method attribute defines how data is sent. The HTTP protocol provides several ways to perform a request; HTML form data can be transmitted via a number of different methods, the most common being the `GET` method and the `POST` method.

#### The GET method

The GET method is the method used by the browser to ask the server to send back a given resource: "Hey server, I want to get this resource." In this case, the browser sends an empty body. Because the body is empty, if a form is sent using this method the data sent to the server is appended to the URL.

Consider the following form:

    <form action="http://www.foo.com" method="GET">
    <div>
        <label for="say">What greeting do you want to say?</label>
        <input name="say" id="say" value="Hi" />
    </div>
    <div>
        <label for="to">Who do you want to say it to?</label>
        <input name="to" id="to" value="Mom" />
    </div>
    <div>
        <button>Send my greetings</button>
    </div>
    </form>

Since the GET method has been used, you'll see the URL www.foo.com/?say=Hi&to=Mom appear in the browser address bar when you submit the form.

![image](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data/url-parameters.png)

#### The POST method

The `POST` method is a little different. It's the method the browser uses to talk to the server when asking for a response that takes into account the data provided in the body of the HTTP request: "Hey server, take a look at this data and send me back an appropriate result." If a form is sent using this method, the data is appended to the body of the HTTP request.

Let's look at an example — this is the same form we looked at in the `GET` section above, but with the method attribute set to `POST`.

    <form action="http://www.foo.com" method="POST">
    <div>
        <label for="say">What greeting do you want to say?</label>
        <input name="say" id="say" value="Hi" />
    </div>
    <div>
        <label for="to">Who do you want to say it to?</label>
        <input name="to" id="to" value="Mom" />
    </div>
    <div>
        <button>Send my greetings</button>
    </div>
    </form>

When the form is submitted using the POST method, you get no data appended to the URL, and the HTTP request looks like so, with the data included in the request body instead:

    POST / HTTP/2.0
    Host: foo.com
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 13

    say=Hi&to=Mom

## On the server side: retrieving the data

Whichever HTTP method you choose, the server receives a string that will be parsed in order to get the data as a list of key/value pairs. The way you access this list depends on the development platform you use and on any specific frameworks you may be using with it.

## Want to read full article, [here it is][1]

[1]: <https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data>
















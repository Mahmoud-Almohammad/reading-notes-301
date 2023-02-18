# What Is Node and When Should I Use It?

**So you’ve heard of Node.js, but aren’t quite sure what it is or where it fits into your development workflow. Or maybe you’ve heard people singing Node’s praises and now you’re wondering if it’s something you need to learn. Perhaps you’re familiar with another back-end technology and want to find out what’s different about Node.**

In this article, I’ll take a beginner-friendly, high-level look at Node.js and its main paradigms. I’ll examine Node’s main use cases, as well as the current state of the Node landscape, and offer you a wide range of jumping off points (for further reading) along the way.

## What Is Node.js?

Node.js is an event-based, non-blocking, asynchronous I/O runtime that uses Google’s V8 JavaScript engine and libuv library.

### Node Is Built on Google Chrome’s V8 JavaScript Engine

The V8 engine is the open-source JavaScript engine that runs in Google Chrome and other Chromium-based web browsers, including Brave, Opera, and Vivaldi. It was designed with performance in mind and is responsible for compiling JavaScript directly to native machine code that your computer can execute.

This means that Node.js is a program we can use to execute JavaScript on our computers. In other words, it’s a JavaScript runtime.

## How Do I Install Node.js?

In this next section, we’ll install Node and write a couple of simple programs. We’ll also look at npm, a package manager that comes bundled with Node.

### Node Binaries vs Version Manager

Many websites will recommend that you head to the official Node download page and grab the Node binaries for your system. While that works, I would suggest that you use a version manager instead. This is a program that allows you to install multiple versions of Node and switch between them at will. There are various advantages to using a version manager. For example, it negates potential permission issues when using Node with npm and lets you set a Node version on a per-project basis.

If you fancy going the version manager route, please consult our quick tip: [Install Multiple Versions of Node.js using nvm][1]. Otherwise, grab the correct binaries for your system from the link above and install those.

### “Hello, World!” the Node.js Way

You can check that Node is installed on your system by opening a terminal and typing `node -v`. If all has gone well, you should see something like `v19.6.1` displayed. This is the current LTS version at the time of writing.

Next, create a new file `hello.js` and copy in the following code:

    console.log("Hello, World!");

This uses Node’s built-in console module to display a message in a terminal window. To run the example, enter the following command:

    node hello.js

If Node.js is configured properly, “Hello, World!” will be displayed.

## Introducing npm, the JavaScript Package Manager

As I mentioned earlier, Node comes bundled with a package manager called npm. To check which version you have installed on your system, type `npm -v`.

In addition to being the package manager for JavaScript, npm is also the world’s largest software registry. There are over 1,000,000 packages of JavaScript code available to download, with billions of downloads per week.

### Working with the package.json File

If you open the `package.json` file, you’ll see lodash listed under the `dependencies` field. By specifying your project’s dependencies in this way, you allow any developer anywhere to clone your project and use npm to install whatever packages it needs to run.

## What Is Node.js Used For?

Now that we know what Node and npm are and how to install them, we can turn our attention to the first of their common uses: installing (via npm) and running (via Node) various build tools — designed to automate the process of developing a modern JavaScript application.

These build tools come in all shapes and sizes, and you won’t get far in a modern JavaScript landscape without bumping into them. They can be used for anything from bundling your JavaScript files and dependencies into static assets, to running tests, or automatic code linting and style checking.

If you want to start developing apps with any modern JavaScript framework (for example, React or Angular), you’ll be expected to have a working knowledge of Node and npm (or maybe **Yarn**). This isn’t because you need a Node back end to run these frameworks. You don’t. Rather, it’s because these frameworks (and many, many related packages) are all available via npm and rely on Node to create a sensible development environment in which they can run.

## Node.js Lets Us Run JavaScript on the Server

### The Node.js Execution Model

In very simplistic terms, when you connect to a traditional server, such as Apache, it will spawn a new thread to handle the request. In a language such as PHP or Ruby, any subsequent I/O operations (for example, interacting with a database) block the execution of your code until the operation has completed. That is, the server has to wait for the database lookup to complete before it can move on to processing the result. If new requests come in while this is happening, the server will spawn new threads to deal with them. This is potentially inefficient, as a large number of threads can cause a system to become sluggish — and, in the worst case, for the site to go down. The most common way to support more connections is to add more servers.

Node.js, however, is single-threaded. It’s also **event-driven**, which means that everything that happens in Node is in reaction to an event. For example, when a new request comes in (one kind of event) the server will start processing it. If it then encounters a blocking I/O operation, instead of waiting for this to complete, it will register a callback before continuing to process the next event. When the I/O operation has finished (another kind of event), the server will execute the callback and continue working on the original request. Under the hood, Node uses the libuv library to implement this asynchronous (that is, non-blocking) behavior.

Node’s execution model causes the server very little overhead, and consequently it’s capable of handling a large number of simultaneous connections. The traditional approach to scaling a Node app is to clone it and have the cloned instances share the workload. Node.js even has a built-in module to help you implement a cloning strategy on a single server.

The following image depicts Node’s execution model:

![example describe Node’s execution model](https://uploads.sitepoint.com/wp-content/uploads/2012/10/1516152673node_event_loop.png)

### “Hello, World!” — Server Version

Let’s have a quick look at a “Hello, World!” example HTTP server:

    const http = require('http');

    http.createServer((request, response) => {
    response.writeHead(200);
    response.end('Hello, World!');
    }).listen(3000);

    console.log('Server running on http://localhost:3000');

Now let’s have a look at the code.

We start by requiring Node’s native **HTTP module**. We then use its **createServer** method to create a new web server object, to which we pass an anonymous function. This function will be invoked for every new connection that’s made to the server.

The anonymous function is called with two arguments (`request` and `response`). These contain the request from the user and the response, which we use to send back a 200 HTTP status code, along with our “Hello World!” message.

Finally, we tell the server to listen for incoming requests on port 3000, and output a message to the terminal to let us know it’s running.

## What Kind of Apps Is Node.js Suited To?

Node is particularly suited to building applications that require some form of real-time interaction or collaboration — for example, chat sites, or apps such as CodeShare, where you can watch a document being edited live by someone else. It’s also a good fit for building APIs where you’re handling lots of requests that are I/O driven (such as those needing to perform operations on a database), or for sites involving data streaming, as Node makes it possible to process files while they’re still being uploaded.

## What Are the Advantages of Node.js?

Aside from speed and scalability, an often-touted advantage of using JavaScript on a web server — as well as in the browser — is that your brain no longer needs to switch modes. You can do everything in the same language, which, as a developer, makes you more productive (and hopefully, happier). For example, you can easily share code between the server and the client.

Another of Node’s big pluses is that it speaks JSON. JSON is probably the most important data exchange format on the Web, and the lingua franca for interacting with object databases (such as MongoDB). JSON is ideally suited for consumption by a JavaScript program, meaning that when you’re working with Node, data can flow neatly between layers without the need for reformatting. You can have one syntax from browser to server to database.

Finally, JavaScript is ubiquitous: most of us are familiar with JavaScript, or have used it at some point. This means that transitioning to Node development is potentially easier than to other server-side languages. To quote Craig Buckler in his Node vs PHP Smackdown, JavaScript might remain the world’s most misunderstood language — but, once the concepts click, it makes other languages seem cumbersome.

## Conclusion

JavaScript is everywhere, and Node is a vast and expansive subject. Nonetheless, I hope that in this article I’ve offered you the beginner-friendly, high-level look at Node.js and its main paradigms that I promised at the beginning. I also hope that when you re-read the definitions we looked at previously, things will make a lot more sense.

## And we done! thank you for reading, if you want to read the full article, you can click [here][2].

[1]: <https://www.sitepoint.com/quick-tip-multiple-versions-node-nvm/>
[2]: <https://www.sitepoint.com/an-introduction-to-node-js/>

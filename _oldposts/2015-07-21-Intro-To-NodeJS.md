---
layout: post
title: Intro to Node.js
tags:
- Node.js
- JavaScript
- Web Development
published: true
date: 2015-07-21 11:16:00
---

Node.js is amazing new platform for writing network and web applications.

## Running Node.js
After installing node.js into your system from [here](https://nodejs.org/download/) we are good to use node from our terminal.
There are actually two ways of using Node.js on you system: by using node shell, or by running already saved JavaScript files.

### Node shell
To launch node shell put ```node``` into terminal

```
$ node
```
Then ```>``` symbol will appear instead of your computer name. After seeing that symbol you can immediately type JavaScript code.

```
console.log("Hello World!");
Hello World!
undefined
```

The last line of the output (undefined) is always the resulting value of the preceding statement. If there is no evaluated expression value or the called function does not return any particular value, the special value ```undefined``` is returned instead.

To exit the REPL(```Read-Eval-Print-Loop```), you simply press CTRL-D

If you see three dots (```...```) in the Node REPL, that means REPL expecting more input from you to complete the current expression, statement or function. If you want to break it use ```.break```.


### Editing and Running JavaScript Files
Other option to use Node.js is to simply write some code on text editor save it as JavaScript file and then compile and run that code via the terminal using the ```node``` command.

Let's make a file called ```hello.js```

```js
/* This is a command that JavaScript will ignore */

console.log("Hello World!");
```

Save as ```hello.js``` and run command on terminal ```node hello.js```. And you should see an output like ```Hello World!```


## First Web Server
It's time to create a little web server. You will see how easy to create a web server with Node. Let's create a file called ```web.js```

```js
var http= require("http");

function process_request(req, res){
  var body = "Thanks for calling!\n";
  var content_length = body.length;
  res.writeHead(200, {
    'Content-Length': content_length,
    'Content-Type': 'text/plain'
  })
  res.end(body);
}

var s = http.createServer(process_request);
s.listen(8080);
```
To run your first web server simply type ```node web.js```

Now your computer has a web server on port 8080. You will see nothing on the terminal, to check if it is working or not. Open another window of terminal and write this.
```curl -i http://localhost:8080```

Then you should see something very similar to this:

```
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: text/plain
Date: Tue, 21 Jul 2015 16:04:02 GMT
Connection: keep-alive

Thanks for calling!
```

Node.js provides a lot of powerful functionality right out of the box, and in the first line of the preceding program, you use one of these built-in modules (http module), which allows your program to act as a web server. The ```require``` function includes this module, and you have the variable ```http``` refer to it.

The ```createServer``` function takes only one argument of connection to your server.

To stop the server Ctrl+C.

## Debugging
To debug your code if you are experiencing problems, you should add ```debug``` flag before the name of your program: ```node debug web.js```

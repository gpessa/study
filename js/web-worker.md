## Web worker

Web Workers are a simple means for web content to run scripts in background threads. The worker thread can perform tasks without interfering with the user interface.

A worker is an object created using a constructor (e.g. Worker()) that runs a named JavaScript file:

#### How to use it in the main page

Initializing a worker is a pretty easy thing:

```js
var myWorker = new Worker("worker.js");
```

Communication between page and worker happen througha message system.
If the page want to send a message it will use the `postMessage` methode on the worker instance:

```js
myWorker.postMessage("Ciao worker!");
console.log("Message posted to worker");
```

If the page wants to listen to message from the worker, it can use the `onmessage` methode on the worker instance:

```js
myWorker.onmessage = function(e) {
  result.textContent = e.data;
  console.log("Message received from worker");
};
```

#### How to use it in the worker

In the worker we can listen to messages, or send message with by declaring the method `onmessage` to listen to communication or use the method `postMessage` to send one.

```js
onmessage = function(e) {
  console.log("Message received from main script");
  var workerResult = "Result: " + e.data;
  console.log("Posting message back to main script");
  postMessage(workerResult);
};
```

### Termination

If you need to immediately terminate a running worker from the main thread, you can do so by calling the worker's `terminate` method:

```js
myWorker.terminate();
};

#### Limitations

A webworker do not have no access to:

- `window` object
- `Document` object
- Parent object
```

---
title: Node.js threads
tags:
  - Backend
  - Node.js
categories:
  - [Node.js, Basics]
date: 2021-06-30
---
# Backgrounds
* The virtual machine and the operating system run the I/O in parallel for us, and when it’s time to send data back to our JavaScript code, the JavaScript part is the one that runs in a single thread. So everything runs in parallel except for our JavaScript code:
```js
let flag = false
function doSomething() {
  flag = true
  // More code (that doesn't change `flag`)...

  // We can be sure that `flag` here is true.
  // There's no way another code block could have changed
  // `flag` since this block is synchronous.
}
```
* For example, in Java, even some numeric types are not atomic; if you don’t synchronize their access, you could end up having two threads change the value of a variable. The result would be that after both threads have accessed the variable, it has a few bytes changed by one thread and a few bytes changed by the other thread — and, thus, not resulting in any valid value.
* Worker pool is an execution model that spawns and handles separate threads, which then synchronously perform the task and return the result to the event loop. The event loop then executes the provided callback with said result. A worker pool is a given number of previously created workers sitting and listening for the message event. Eight workers created below:
```js
const pool = new WorkerPool(path.join(__dirname, './test-worker.js'), 8);
```
* In short, main event pool takes care of asynchronous I/O operations — primarily, interactions with the system’s disk and network. It is mainly used by modules such as `fs` (I/O-heavy) or `crypto` (CPU-heavy). Worker pool is implemented in libuv.
[source 1](https://blog.logrocket.com/node-js-multithreading-what-are-worker-threads-and-why-do-they-matter-48ab102f8b10/)
[source 2](https://blog.logrocket.com/a-complete-guide-to-threads-in-node-js-4fa3898fe74f/)

# `worker_threads` module
* A thread worker is a piece of code (usually taken out of a file) spawned in a separate thread.
* Here’s an example of a file that contains a worker that is spawned, executed, and then closed:
```js
import { parentPort } from 'worker_threads';
const collection = [];
for (let i = 0; i < 10; i += 1) {
 collection[i] = i;
}
parentPort.postMessage(collection);
```
* Here’s an example of a worker that can wait for a long period of time before it is given a task:
```js
import { parentPort } from 'worker_threads';
parentPort.on('message', (data: any) => {
 const result = doSomething(data);
 parentPort.postMessage(result);
});
```
[source](https://blog.logrocket.com/a-complete-guide-to-threads-in-node-js-4fa3898fe74f/)

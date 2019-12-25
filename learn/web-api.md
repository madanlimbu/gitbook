# Web API

#### Channel Messaging API

Channel Messaging API allows two different scripts in different contexts \(Workers/IFrames\) to communicate by passing messages between them in bi-directional channels with port in each end.  

* `MessageChannel()` contains 2 properties `port1` & `port2` 
* `port1` & `port2` both returns `MessagePort` objects
* Creator of channel uses `port1` & receiver uses `port2` 
* use `postMessage(data, port2)`  to send over message & transfer ownership of port `MessagePort` object over to other browsing context
* Receiver \(other browsing context\) can listen using `MessagePort.onmessage` or `message` Event & respond by using `MessagePort.postMessage` 



#### Web Workers

Due to JS single threaded limitation, web workers were created to allow parallel execution. 

* is a `Worker()` Object which runs a separate JS file
* Doesn't have browsing context \(No access to DOM / Window Objects \)
* `WorkerGlobalScope` is the global scope \(global context\)
* Uses built-in `postMessage()` with `onmessage` / `message` Event  or **Channel Messaging API** to communicate between main thread 

Web Worker Thread are closed once code runs & if there is no event listener present. Can use `terminate()` \(from main thread\) or `close()` to end thread.



#### Service Worker

Service worker are special kind of `Worker()` that acts as a proxy between web app, browser & network. 

#### Helpful links

* [Web Workers API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
* [Channel Messaging API](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API)


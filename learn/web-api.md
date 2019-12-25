# Web API

### Channel Messaging API

Channel Messaging API allows two different scripts in different contexts \(Workers/IFrames\) to communicate by passing messages between them in bi-directional channels with port in each end.  

* `MessageChannel()` contains 2 properties `port1` & `port2` 
* `port1` & `port2` both returns `MessagePort` objects
* Creator of channel uses `port1` & receiver uses `port2` 
* use `postMessage(data, port2)`  to send over message & transfer ownership of port `MessagePort` object over to other browsing context
* Receiver \(other browsing context\) can listen using `MessagePort.onmessage` or `message` Event & respond by using `MessagePort.postMessage` 



### Web Workers

Due to JS single threaded limitation, web workers were created to allow parallel execution. 

* is a `Worker()` Object which runs a separate JS file
* Doesn't have browsing context \(No access to DOM / Window Objects \)
* `WorkerGlobalScope` is the global scope \(global context\)
* Uses built-in `postMessage()` with `onmessage` / `message` Event  or **Channel Messaging API** to communicate between main thread 

Web Worker Thread are closed once code runs & if there is no event listener present. Can use `terminate()` \(from main thread\) or `close()` to end thread.



### Service Worker

Service worker are special kind of `Worker()` that acts as a proxy between web app, browser & network. 

* Fully async, hence Sync Web API \(XHR & localStorage\) can't be used inside service worker. 
* `navigator.serviceWorker` returns `ServiceWorkerContainer` which can be used to `register('/my-service-worker.js')`  &  get service worker. 
* listen to `install` or `activate` event & run appropriate functions
* _Install_ : Good time to prepare the Service worker 
* _Activate_ : Good time to clean up stuff from old version of service worker

#### Life Cycle 

* **Register** \(download service worker to client & attempt install/activate\)
* **Install** \(fires if new service worker or first service worker encountered\)
* **Activate** \(if installed & there is no other service worker then activate\)

Service worker can listen to requests using `FetchEvent` event & provide respond using `FetchEvent.respondWith()`. we can listen to `fetch` event & respond accordingly_, for example we can use Cache API to check if we have cache for requested page & respond the cache instead of requesting server._ 



#### Helpful links

* [Web Workers API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
* [Channel Messaging API](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API)
* [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) 
* [Service Worker Registration](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration)


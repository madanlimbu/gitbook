# Web API

### Channel Messaging API

Channel Messaging API allows two different scripts in different contexts (Workers/IFrames) to communicate by passing messages between them in bi-directional channels with port in each end. &#x20;

* `MessageChannel()` contains 2 properties `port1` & `port2`&#x20;
* `port1` & `port2` both returns `MessagePort` objects
* Creator of channel uses `port1` & receiver uses `port2`&#x20;
* use `postMessage(data, port2)`  to send over message & transfer ownership of port `MessagePort` object over to other browsing context
* Receiver (other browsing context) can listen using `MessagePort.onmessage` or `message` Event & respond by using `MessagePort.postMessage`&#x20;



### Web Workers

Due to JS single threaded limitation, web workers were created to allow parallel execution.&#x20;

* is a `Worker()` Object which runs a separate JS file
* Doesn't have browsing context (No access to DOM / Window Objects )
* `WorkerGlobalScope` is the global scope (global context)
* Uses built-in `postMessage()` with `onmessage` / `message` Event  or **Channel Messaging API** to communicate between main thread&#x20;

Web Worker Thread are closed once code runs & if there is no event listener present. Can use `terminate()` (from main thread) or `close()` to end thread.



### Service Worker

Service worker are special kind of `Worker()` that acts as a proxy between web app, browser & network.&#x20;

* Fully async, hence Sync Web API (XHR & localStorage) can't be used inside service worker.&#x20;
* `navigator.serviceWorker` returns `ServiceWorkerContainer` which can be used to `register('/my-service-worker.js')`  &  get service worker.&#x20;
* listen to `install` or `activate` event & run appropriate functions
* _Install_ : Good time to prepare the Service worker&#x20;
* _Activate_ : Good time to clean up stuff from old version of service worker

#### Life Cycle&#x20;

* **Register** (download service worker to client & attempt install/activate)
* **Install** (fires if new service worker or first service worker encountered)
* **Activate** (if installed & there is no other service worker then activate)

Service worker can listen to requests using `FetchEvent` event & provide respond using `FetchEvent.respondWith()`. we can listen to `fetch` event & respond accordingly_, for example we can use Cache API to check if we have cache for requested page & respond the cache instead of requesting server._&#x20;

### Fetch API

Mordern api to make request for a resource from network.

Some of the less known but usefull options on fetch() method are given bellow:

#### keepalive

The `keepalive` option can be used to allow the request to outlive the page. Fetch with the `keepalive` flag is a replacement for the [`Navigator.sendBeacon()`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) API.&#x20;

This can be usefull for analaytics or when we don't need to worry about the response from long running process in server.

#### signal

An [`AbortSignal`](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) object instance; allows you to communicate with a fetch request and abort it if desired via an [`AbortController`](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).

This is really handy when there is fetch request being made with changing request param and if we want to cancel the previous request so we only get response for latest version of request.

```
// common example usecase on react with useeffect

const [searchInput, setSearchInput] = useState('');

useEffect(() => {
    const controller = new AbortController();
    
    fetch(url, {
        data: searchInput,
        signal: controller.signal
    });
    
    return () => {
        // cancel request when searchInput is updated
        controller.abort();
    }
}, [searchInput])
```





#### Helpful links

* [Web Workers API](https://developer.mozilla.org/en-US/docs/Web/API/Web\_Workers\_API)
* [Channel Messaging API](https://developer.mozilla.org/en-US/docs/Web/API/Channel\_Messaging\_API)
* [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service\_Worker\_API)&#x20;
* [Service Worker Registration](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration)
* [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch\_API)

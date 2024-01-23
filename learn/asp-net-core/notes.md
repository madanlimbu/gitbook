---
description: Quick notes on ASP Net Core
coverY: 0
---

# Notes

## Intro - Overview

* Asp.Net Core FOSS
* 2002 - (Webforms - Event driven - No Cloud support)
* 2006 - (Asp.Net Mvc - MVC - Partial Cloud support)
* 2016 - (Asp.Net Core - MVC - Fully Cloud support)
* Cross platform (i.e Windows/Linux/Mac) after Asp.Net Core V6
* Cross platform server Kestrel by default
* Can use extra server (reverse proxy) on the gateway for production
  * i.e REQ -> (PROXY SERVER) -> (Kestrel) -> Application
  * Proxy server examples - IIS / Nginx/ Apache
    * Note: IIS Express (Light weight version of IIS) & IIS are only supported on windows
* JSON configuration file for server
  * launchSettings.json
  * Contains configuration for different (profiles) server
    * profiles
      * IIS or Project (Kestrel)
      * env variables, port, http/https

## Middleware

Bunch of functions to help with application request

We can can chain number of middleware functions on .Net WebApplication

Takes in `req` Obj & `next` Function in the chain to run

Type of Extension avaialble&#x20;

* `app.Use()-`Can pass req to next middleware or short cirut it
* `app.Run` - Doesn't foward req
* `app.UseWhen` - Branching middleware using conditional logic
* `app.UseMiddleWare<T>()` - Use Class instead of lamda

## Routing

.Net Core provides routing capability out of the box

`UseRouting()`&#x20;

* &#x20;Middleware to enable routing
* Point in middleware where  routing desion are made and an Endpoint is associated with a Req

`UseEndPoints()`

* Executes appropriate endpoint created on routing middleware
* We can define out endpoint to map a specific path and req type
* `app.UseEndPoints(e => e.Map('/abc',(ctx) => {..})`&#x20;
* Can use contrainst on Url itself or Define custom Contraint Class (IRouteContraint) with logic and add it to Routing Service

&#x20;`UseStaticFiles()` - Map/Configure static files

## Controller

* Classname Suffixed with "Controller" (i.e TestController)
* or Use Controller attribute on the class `[Controller]`&#x20;

This way .Net should be able to detect any controller class

There are few helper method to make use of controller method as endpoint.

Instead of manually adding a controller to service & maping them to a endpoint. We can use:

* `builder.Services.AddControllers()` - Adds all controller as service which can be later used for a specific endpoint
* `app.MapControllers()` - Adds controller methods as endpoints so a specific route specified in attribute (i.e `[Route('/abc/')]` above method is mapped to it

Action/Method on controller can return various type. Some of the useful ones extends the `IActionResult` interface.&#x20;

<figure><img src="../../.gitbook/assets/IActionResult.png" alt=""><figcaption></figcaption></figure>

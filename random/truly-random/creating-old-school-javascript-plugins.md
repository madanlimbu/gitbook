# Creating Old School Javascript Plugins

I like to watch the video ( mostly anime/drama ) while reading or working on something. However, when watching the video in half screen of the window, the random stuff from the video page is very distracting. Hence, I wanted to create simple JS script to hide random stuff and only show video which can be injected to the website using any of browser JS/CSS add-ons/extensions. Consequently, I wanted to write some reusable JS Plugin/Module. Here is my adventure of creating one.\


My Plan, Simple JS Plugin Template which can be reused for my future project. I will be making an extra element that will hide all unwanted stuff from the page and put the element under video player so only video player will be visible. To make webpage usable I will put an event listener when the mouse is over the webpage to show hidden element that way the user can navigate when they finish watching the video. Finally, I will expose the video player selector definable through argument so that the plugin can be used on different websites.

**This can be used not just with watching the video but also any other webpage where we only want to show a certain part and hide other. Almost like an adblocker but not just ad but everything unwanted.**

#### _**Here is my finish product in github.**_ [_**https://github.com/madan95/binger**_](https://github.com/madan95/binger)

#### Firstly, I will be using [UMD](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/) wrapping pattern to wrap my plugin to support both AMD, CommonJS and Traditional Module Pattern.

```
(function(root, factory){
    if(typeof define === 'function' && define.amd){
        // AMD
        define([], factory(root));
    }else if (typeof exports === 'object'){
        // Node, CommonjS
        module.exports = factory(root);
    }else{
        // Browser globals
        root.binger = factory(root);
    }
})(typeof global !== 'undefined' ? global : this.window || this.global, function (root) {
    // Plugin/Module Code
});
```

Next, I have created a simple template for a plugin which can be used to create our own plugin.

```
(function(root, factory){
    if(typeof define === 'function' && define.amd){
        // AMD
        define([], factory(root));
    }else if (typeof exports === 'object'){
        // Node, CommonjS
        module.exports = factory(root);
    }else{
        // Browser globals
        root.binger = factory(root);
    }
})(typeof global !== 'undefined' ? global : this.window || this.global, function (root) {
    // Plugin/Module Code

    'use strict';

    //Object for public APIs
    var binger = {};

    //Global Variables Used across the plugin
    var settings;

    //Default settings
    var defaults = {
        videoPlayerId : 'video_player',
        videoWrapperClass : 'cinematic-wrapper-col'
    };

    /**
     * Initialize Plugin
     * @public
     * @param options
     */
    binger.init = function (options) {
        //Code to run on Initialization of Plugin

        utilReady(function () {
            //Merge default and passed argument to set settings
            if(arguments[0] && typeof arguments[0] === 'object'){
                settings = utilExtendSettings(settings, arguments[0]);
            }

            //Listen for mouseover and mouseleave event to hide and show other contents
            ['mouseover', 'mouseleave'].forEach((e) => {
                document.addEventListener(e, eventHandler, false);
            });
        })
    };

    /**
     * Util function to Merge defaults and passed property from argument
     * @param defaults
     * @param extra
     * @returns {*}
     */
    var utilExtendSettings = function (defaults, extra) {
        var property;
        for(property in extra){
            if(extra.hasOwnProperty(property)){
                defaults[property] = extra[property];
            }
        }
        return defaults;
    };


    /**
     * Util function to wait till DOM is ready to run the passed function
     * @param fn
     * @returns {*}
     */
    var utilReady = function(fn){
        //Check to make sure function is passed
        if(typeof fn !== 'function') return;

        //if document is already loaded, run function
        if(document.readyState === 'complete'){
            return fn();
        }

        //Else, wait till document is loaded
        document.addEventListener('DOMContentLoaded', fn, false);
    };

    /**
     * Event Handler
     * @private
     * @param event
     */
    var eventHandler = function(event) {
        //Check Type of Event and Element to handle event
        if(event.type === 'mouseover'){
            //Show Hidden Content
        }
        if(event.type === 'mouseleave'){
            //Hide Content Other Content
        }
    };


    //Return Object to be accessed from outside
    return binger;
});
```

There are different part to this plugin. I will briefly describe a different part of it below.

We have created a variable that will be used across the module at the top. we have also created an Object that will be returned at the end which can have its own function that is accessible from outside. For my module, I have 2 element selector class/id in default variable that can be changed from outside to reuse the plugin on different video webpage.

Next, we also have some private Util functions. One of them is used to make sure that the code only runs once the DOM is ready. Another one is used to merge the passed on argument property with default variable property that we created at the top.

We also have Event Handler Method that can be used to listen to event and type of element to run the code once the event fires.  For my module, I will be listening to mouseover and mouseleave to hide and show elements that are not video so that I can still use the video webpage when I want to change video or do other things in the page.

Finally, init function which is exposed to the outside and which we can call to run our plugin.\

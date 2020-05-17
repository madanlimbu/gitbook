# JS

#### Drupal.behaviour 

Drupal Core Library provide behaviours property where we can attach our custom methods.

```text
Drupal.behaviors.myBehavior = {
  attach: function (context, settings) {
    console.log('our function');
  }
};
```

It's `attach()` method is called both when DOM is loaded & after any AJAX call which is why it is preferred over jQuery or VanillaJS on document load listener.

In summary, within Drupal JS they have implemented `$(document).ready` function which calls `Drupal.attachBehaviors()` which will go through each `Drupal.behaviors` object and call every one of its properties. 

document will be passed in as `context` & `drupalSettings` as settings, however during AJAX load the `context` will be only new content loaded by AJAX call.

{% embed url="https://www.drupal.org/docs/8/theming/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-theme" %}

{% embed url="https://www.drupal.org/docs/8/api/javascript-api/javascript-api-overview" %}




# Render Arrays

#### Render Arrays Intro

Render array is an associative array which follow structures used in Drupal's theme rendering system.

Render array and Form arrays share many properties but Form API array must be transformed into Render API array to render it. 

> Note: Rendering in Drupal means turning structured "render" arrays into HTML.

#### Reason behind render array

Makes rendering flexible. We can now use hook like  `hook_page_alter()` at the last minute to change page layout or content before it is rendered. 


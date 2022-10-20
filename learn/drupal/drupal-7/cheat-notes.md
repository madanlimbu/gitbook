# Cheat Notes

####

#### Drupal 7 Turn off caching

```
$conf['cache'] = 0;                       // Page cache
$conf['page_cache_maximum_age'] =  0;     // External cache TTL
$conf['preprocess_css'] = FALSE;          // Optimize css
$conf['preprocess_js'] = FALSE;           // Optimize javascript
$conf['views_skip_cache'] = TRUE;         // Views caching
```

Or

```
drush @docker vset cache 0; drush @docker vset preprocess_css 0; drush @docker vset preprocess_js 0; drush @docker vset page_cache_maximum_age 0; drush @docker vset views_skip_cache TRUE;
```

#### Enable Theme debug mode for theme hook suggestions

```
drush @docker vset theme_debug 1
```

#### Drupal 7 Update good practice

* Backup (code/files/database) (_Not needed if updating locally_) `drush archive-dump`
* Maintenance mode (_Not needed if updating locally_) `drush vset --exact maintenance_mode 1`&#x20;
* Clear Cache `drush cc all`&#x20;
* Update the site code base ( Using drush-make or config or composer or drush )
* Update database `drush updb -y`&#x20;
* Test site&#x20;
*   Release maintenance mode (_Not needed if updating locally_)&#x20;

    &#x20;`drush vset --exact maintenance_mode 0`&#x20;
* Clear Cache `drush cc all`

#### &#x20;&#x20;




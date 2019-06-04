# Cheat Notes

#### 

#### Drupal 7 Turn off caching

```text
$conf['cache'] = 0;                       // Page cache
$conf['page_cache_maximum_age'] =  0;     // External cache TTL
$conf['preprocess_css'] = FALSE;          // Optimize css
$conf['preprocess_js'] = FALSE;           // Optimize javascript
$conf['views_skip_cache'] = TRUE;         // Views caching
```

Or

```text
drush @docker vset cache 0; drush @docker vset preprocess_css 0; drush @docker vset preprocess_js 0; drush @docker vset page_cache_maximum_age 0; drush @docker vset views_skip_cache TRUE;
```




# Drupal / PHP Thangs

### Composer Installers

`composer/installers` - Useful when we want to install composer package in a specific location \( in framework like Drupal , Wordpress \)

{% embed url="https://getcomposer.org/doc/faqs/how-do-i-install-a-package-to-a-custom-path-for-my-framework.md" %}

{% embed url="https://getcomposer.org/doc/articles/custom-installers.md" %}

{% embed url="https://github.com/composer/installers" %}

### Scaffold \(drupal/core-composer-scaffold\) ^8.8.0

Different flavour of Drupal -&gt; Uses `drupal/core` -&gt; that provides core & Drupal scaffold assets \( i.e `index.php`, `.htacess`, `robot.txt` \)

Composer plugin that will automatically scaffold Drupal files.

#### Allowed Packages

Define `project/module/profile` that can scaffold - core by default.

```text
  "extra": {
    "drupal-scaffold": {
      "allowed-packages": [
        "drupal/core"
      ]
    }
```

```text
"locations": { "web-root" : "./docroot" } #define web-root location
```

#### Mapping scaffold files

Placement of scaffold assets is under the control of the project that provides them, but the location is always relative to some directory defined by the root project.

![Drupal/Core - put scaffold to root/web dir](../../.gitbook/assets/screenshot-2020-01-18-at-3.34.39-pm.png)

#### Alter scaffold files

Alter scaffold files by patching or appends additional data.

```text
  "extra": {
    "drupal-scaffold": {
      "file-mapping": {
        "[web-root]/robots.txt": {
          "append": "assets/my-robots-additions.txt",
        }
      }
    }
  }
```

Different hooks can be used to add patch

```text
  "scripts": {
    "post-drupal-scaffold-cmd": [
      "cd docroot && patch -p1 <../patches/htaccess-ssl.patch"
    ]
  }
```

_**Other feature : excluding, overwriting, symlink.**_

{% embed url="https://github.com/drupal/core-composer-scaffold" %}




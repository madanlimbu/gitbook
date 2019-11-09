# Permissions

Initially, when setting up the site we will need  loose access so we can make changes.

From public\_html or wordpress directory:

```text
chown www-data:www-data -R * #Apache owner
find . -type d -exec chmod 755 {} \; #Directory permission rwxr-xr-x
find . -type f -exec chmod 644 {} \; #File permission rw-r--r--
```

Once the wordpress site set up is done. We need to tighten the access rights. wp-content must be writable by www-data.

```text
chown <username>:<username> -R * #User account should be the owner
chown www-data:www-data wp-content #Apache owner of wp-content
```


# Cheats/Hacks

Sometimes when debugging a php project, it can take time to setup proper debugging tools and we might not have enough time. In such case I personally resort to using php `error_log` [function](https://www.php.net/manual/en/function.error-log.php).

{% code title="some\_file\_to\_debug.php" %}
```php
function someRandomFunctionToDebug($variables) {
    $log = "Time : " . date('Y-m-d H:i:s') . " | Detail : " . $variables . "\r\n";
    error_log($log, 3, "/var/tmp/debug-errors.log");
}
```
{% endcode %}

Above is the simple example of code to put my log of code that I want to debug. Then in terminal I can watch for the output of the error log.

{% code title="Terminal cmd to watch log file" %}
```bash
tail -f /var/tmp/debug-errors.log
```
{% endcode %}




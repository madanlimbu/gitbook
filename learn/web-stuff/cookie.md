# Cookie

#### Basic structure:

`<name>=<value> <max-age> <expire-date> <domain> <path> <secure> <httponly> <samesite>`

* **name value pairs** \(key value\)
* **expires** - expire date \(client date\) of cookie
* **max-age** - number of seconds to expire _\(max-age has precedence over expires\)_
* **domain** - Hosts to where the cookie will be sent
* **path** - path that must exist to send cookie 
* **secure** - only send cookie when requested with _https_
*  **httpsonly** - forbids client JS from accessing cookie
* **samesite** - control when to send cookie

#### SameSite

_**possible values**_: `'strict', 'lax', or 'none'` 

1. _**lax**: first-party context \(will be included when coming/request from external site\)_
2. _**strict**: first-party context but won't be included if coming/requested from external site_
3. **none**: _cookie to be shared with third-party \(need `secure` attribute as-well\)_ 

By default `same-site=lax` , Chrome 80 - both `same-site=none` and `secure` needs to set or cookies can only be used within first-party context

{% embed url="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie" %}

Any cookies from different domain used by the site will be considered as third-party cookies when the site is displayed within the iframe.

{% embed url="https://blog.chromium.org/2019/10/developers-get-ready-for-new.html" %}

{% embed url="https://adzerk.com/blog/chrome-samesite/" %}

{% embed url="https://web.dev/samesite-cookie-recipes/" %}

{% embed url="https://web.dev/samesite-cookies-explained/" %}




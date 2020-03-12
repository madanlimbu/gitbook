# Cookie

#### SameSite

_**possible values**_: `'strict', 'lax', or 'none'` 

_**lax**: first-party context \(will be included when coming/request from external site\)_

_**strict**: first-party context but won't be included if coming/requested from external site_

**none**: _cookie to be shared with third-party \(need `secure` attribute\)_

By default `same-site=lax` , Chrome 80 - both `same-site=none` and `secure` needs to set or cookies can only be us

{% embed url="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie" %}

ed within first-party context




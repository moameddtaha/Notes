---
tags: 
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions
---

# `SameSite` cookie
---
- `SameSite` is a browser security mechanism that determines when a website's cookies are included in requests originating from other websites.
- Since 2021, Chrome applies `Lax` `SameSite` restrictions by default if the website that issues the cookie doesn't explicitly set its own restriction level.

## What is a site in the context of `SameSite` cookies?
---

In the context of `SameSite` cookie restrictions, a site is defined as two things:
1. Top-level domain (TLD) usually something like `.com` or `.net`
2. Plus one additional level of the domain name. This is often referred to as the TLD+1.

When determining whether a request is same-site or not, the URL scheme is also taken into consideration. This means that a link from `http://app.example.com` to `https://app.example.com` is treated as cross-site by most browsers.

![[Pasted image 20240114213525.png]]

> [!NOTE] NOTE
> You may come across the term "effective top-level domain" (eTLD). This is just a way of accounting for the reserved multipart suffixes that are treated as top-level domains in practice, such as `.co.uk`.

## What's the difference between a site and an origin?
---

The difference between a site and an origin is their scope; ==**a site encompasses multiple domain names, whereas an origin only includes one.**==

Two URLs are considered to have the same origin if they share the exact **same scheme**, **domain name**, and **port**. Although note that the port is often inferred from the scheme.

![[Pasted image 20240114214141.png]]

As you can see from this example, the term "site" is much less specific as it only accounts for the scheme and last part of the domain name. Crucially, this means that **==a cross-origin request can still be same-site, but not the other way around.==**

![[Pasted image 20240114214338.png]]
## How does `SameSite` work?
---
Before the `SameSite` mechanism was introduced, browsers sent cookies in every request to the domain that issued them, even if the request was triggered by an unrelated third-party website. **`SameSite` works by enabling browsers and website owners to limit which cross-site requests, if any, should include specific cookies.**

All major browsers currently support the following `SameSite` restriction levels:
- **[[Same-Site cookie#Strict|Strict]]**
- **[[Same-Site cookie#Lax |Lax]]** : If a website doesn't include a `SameSite` attribute when setting a cookie, Chrome automatically applies `Lax` restrictions by default.
- **[[Same-Site cookie#None|None]]**

Developers can manually configure a restriction level for each cookie they set, giving them more control over when these cookies are used. To do this, they just have to include the `SameSite` attribute in the `Set-Cookie` response header, along with their preferred value:

```
Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=Strict
```

> [!attention] Attention
> Although this offers some protection against CSRF attacks, none of these restrictions provide guaranteed immunity

> [!important] important
> If the website issuing the cookie doesn't explicitly set a `SameSite` attribute, **Chrome** automatically applies `Lax` restrictions by default. This means that the cookie is only sent in cross-site requests that meet specific criteria, even though the developers never configured this behavior. As this is a proposed new standard, we expect other major browsers to adopt this behavior in future.

### Strict
---
 If a cookie is set with the `SameSite=Strict` attribute, browsers will not send it in any cross-site requests. In simple terms, this means that if the target site for the request does not match the site currently shown in the browser's address bar, it will not include the cookie.
 
### Lax
---
`Lax` `SameSite` restrictions mean that browsers will send the cookie in cross-site requests, but only if both of the following conditions are met:
1. The request uses the `GET` method.
2. The request resulted from a top-level navigation by the user, such as clicking on a link.

This means that the cookie is not included in background requests, such as those initiated by scripts, `iframes`, or references to images and other resources.

> [!attention] Attention
> As mentioned earlier, if a website doesn't include a `SameSite` attribute when setting a cookie, Chrome automatically applies `Lax` restrictions by default. However, **==to avoid breaking single sign-on (SSO) mechanisms, it doesn't actually enforce these restrictions for the first 120 seconds on top-level POST requests. As a result, there is a two-minute window in which users may be susceptible to cross-site attacks.==**
> 

> [!NOTE] NOTE
> This two-minute window does not apply to cookies that were explicitly set with the `SameSite=Lax` attribute.

### None
---
 **If a cookie is set with the `SameSite=None` attribute, this effectively disables `SameSite` restrictions altogether, regardless of the browser.** As a result, browsers will send this cookie in all requests to the site that issued it, even those that were triggered by completely unrelated third-party sites.
- When setting a cookie with `SameSite=None`, the website must also include the `Secure` attribute, which ensures that the cookie is only sent in encrypted messages over HTTPS. Otherwise, browsers will reject the cookie and it won't be set.
	```
	Set-Cookie: trackingId=0F8tgdOhi9ynR1M9wa3ODa; SameSite=None; Secure
	```


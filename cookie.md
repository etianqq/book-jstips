#Cookie

* 默认情况下，同一个主域名不同子域名下，cookie不共享(domain属性)；
* 同一个主域名，不同的path下，cookie不共享(path属性)。

例子：
```
document.cookie =
  'ppkcookie2=another test; expires=Fri, 3 Aug 2001 20:47:11 UTC; path=/'
```

####Domain

Each cookie also has a domain and a path. 

The domain tells the browser to which domain the cookie should be sent. If you don't specify it, it becomes the domain of the page that sets the cookie, in the case of this ```pagewww.quirksmode.org```.

Please note that the purpose of the domain is to allow cookies to cross sub-domains. My cookie will not be read by ```search.quirksmode.org``` because its domain is ```www.quirksmode.org``` . When I set the domain to ```quirksmode.org```, the search sub-domain may also read the cookie.

I cannot set the cookie domain to a domain I'm not in, I cannot make the domain ```www.microsoft.com``` . Only ```quirksmode.org``` is allowed, in this case.

####Path

The path gives you the chance to specify a directory where the cookie is active. 

So if you want the cookie to be only sent to pages in the directory cgi-bin, set the path to ```/cgi-bin```. Usually the path is set to ```/```, which means the cookie is valid throughout the entire domain.

This script does so, so the cookies you can set on this page will be sent to any page in the ```www.quirksmode.org``` domain (though only this page has a script that searches for the cookies and does something with them).


####Expiry date

Each cookie has an expiry date after which it is trashed. If you don't specify the expiry date the cookie is trashed when you close the browser. This expiry date should be in UTC (Greenwich) time.


# MrBeast Burger Source Code
The source version can be pretty buggy. The list can see known bugs and quirks when using the source version:
* CORS must be disabled, otherwise, you will not be able to accept the cookies.
* The links on the header might point to the original version instead of the source version.
* If the accessibility tools are applied, they would not be able to restore to the default settings.
* The locations page does not function properly.

The following workarounds can be used to fix those bugs &amp; quirks:
1. Install the <a href="https://chrome.google.com/webstore/detail/cors-unblock/lfhmikememgdcahcdlaciloancbhjino">CORS Unblock</a> extension. Go back to the page that is experiencing the problem, and reload the page for the changes to take effect.
2. Manually go the following pages: <a href="https://joseernestoongithub.github.io/mrbeastburger.com-src/www.mrbeastburger.com/about/index.html">About Us</a>, <a href="https://joseernestoongithub.github.io/mrbeastburger.com-src/www.mrbeastburger.com/index.html">Home</a>, <a href="https://joseernestoongithub.github.io/mrbeastburger.com-src/www.mrbeastburger.com/menu/index.html">Menu</a> and <a href="https://joseernestoongithub.github.io/mrbeastburger.com-src/www.mrbeastburger.com/locations/index.html">Locations</a>.
3. Clear the cookies and refresh the page.
4. N/A

If Step 1 didn't work, try disabling CSP. <a href="https://chrome.google.com/webstore/detail/disable-content-security/ieelmcmcagommplceebfedjlakkhpden">Install this extension</a>, go back to the faulty page, and reload. It should fix this problem.

## Why is the Locations page not working?
In the following code in main.min.js (beautified), we can see the following:
```
t.sent.forEach(function (t) {

var e = n.restaurants.find(function (e) {
return e.id === t.id;
});
```
t.sent.forEach is supposed to be interpreted as a function, but it is not, causing a TypeError exception to be thrown with the message `t.sent.forEach is not a function`. This causes the locations page to fail to load. <br/><br/>
The stack trace of the exception can be seen below.
```
 at t.<anonymous> (main.min.js?ver=v1.0.2:1:13573)
    at p (main.min.js?ver=v1.0.2:1:922)

    at Generator.<anonymous> (main.min.js?ver=v1.0.2:1:2258)
    at Generator.next (main.min.js?ver=v1.0.2:1:1347)
    at asyncGeneratorStep (main.min.js?ver=v1.0.2:1:6842)
    at i (main.min.js?ver=v1.0.2:1:7060)
```
<br/>
![Screenshot 2023-11-16 131000](https://github.com/JoseErnestoOnGithub/mrbeastburger.com-src/assets/115112109/d06f91e8-da66-41f7-a743-af90d1fd51db)
In this screenshot, i attempted to compare these two files, which are versions 1.0.2 to 1.0.3, but unfortunately, i got no difference, because the versions 1.0.2 and 1.0.3 i was trying to compare have 1.0.3, which does not exist in the URL of the script.
![Screenshot 2023-11-16 131756](https://github.com/JoseErnestoOnGithub/mrbeastburger.com-src/assets/115112109/78324575-6617-4af4-b413-ecee6cc97ecd)
In the original version, the locations page is fully functioning.

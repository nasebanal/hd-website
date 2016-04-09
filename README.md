# Hacker Dojo Web-Site for Global

Hacker Dojo is non-profit coworking space originated in Mountain View, California. Hacker Dojo distributes the source code for their operation software, and this is folked project in order to internationalize their assets with continuous integration environment.


[Prerequisite]

* Install Google App Engine SDK


[How to Use]

Step.1) Download the source code

 $ git clone https://github.com/nasebanal/hd-website.git


Step.2) If you want to use other locale than English, change local variable "LOCALE". If you don't have corresponding translate.py, you will see in English by default.

Step.3) Test-run the software in your local environment.

 $ dev_appserver.py .

Then you can access this software through http://localhost:8080.
If you are using virtual machine technology, and want to forward the request and get response, you can use the following command instead.

 $ dev_appserver.py --host=0.0.0.0 .


[Technical Notes]

The Dojo Website CMS is extremely simple (less than 100 lines of code), but offers some really slick performance tricks:

* The content is pulled from a PBworks wiki, and cached aggressively.  When a page is edited on the wiki, a webhook is fired from PBworks to the App Engine app with the specific purpose of clearing the cache key.  This hyper efficient design means the app can serve pages from memory with a PERFECT cache efficiency, yet magically updates from the wiki appear _realtime_ on the website.
* The main HTML is served from app engine, but every other asset (js, css, images, etc) are served from a CDN.  The cdn is located at http://cdn.hackerdojo.com/static and simply mirrors everything from the website on a pull basis.  The CDN also uses gzip compression on appropriate files.  (I'm paying for the CDN personally, it is cheap and one I have used for years and trust.)
* All JS and CSS have been optimized and packed into one file each.  (And only the index page requires Javascript, to animate the hero image.)
* The JS and CSS will be cached by the CDN, so the URLs are versioned automatically by App Engine.  Deploying a new version automatically increments the version.
* HTML is space-optimized .. view source on it ;)
* When debugging locally, the CDN and wiki cache are disabled.

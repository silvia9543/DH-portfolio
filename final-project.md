---
layout: page
title: Final Project
permalink: /final-project/
---

```python
#Step 1: Webscrape the top ten songs of each decade from Dave's Music Database
import requests
response = requests.get("https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html")
type(response)
```




    requests.models.Response




```python
response_text = response.text
type(response_text)
response_text[:500]
```




    "<!DOCTYPE html>\n<html class='v2' dir='ltr' lang='en'>\n<head>\n<link href='https://www.blogger.com/static/v1/widgets/2975350028-css_bundle_v2.css' rel='stylesheet' type='text/css'/>\n<meta content='width=1100' name='viewport'/>\n<meta content='text/html; charset=UTF-8' http-equiv='Content-Type'/>\n<meta content='blogger' name='generator'/>\n<link href='https://davesmusicdatabase.blogspot.com/favicon.ico' rel='icon' type='image/x-icon'/>\n<link href='https://davesmusicdatabase.blogspot.com/2012/04/top-s"




```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(response_text)
print(type(soup))
```

    <class 'bs4.BeautifulSoup'>



```python
soup
```




    <!DOCTYPE html>
    <html class="v2" dir="ltr" lang="en">
    <head>
    <link href="https://www.blogger.com/static/v1/widgets/2975350028-css_bundle_v2.css" rel="stylesheet" type="text/css"/>
    <meta content="width=1100" name="viewport"/>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
    <meta content="blogger" name="generator"/>
    <link href="https://davesmusicdatabase.blogspot.com/favicon.ico" rel="icon" type="image/x-icon"/>
    <link href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html" rel="canonical"/>
    <link href="https://davesmusicdatabase.blogspot.com/feeds/posts/default" rel="alternate" title="Dave's Music Database - Atom" type="application/atom+xml"/>
    <link href="https://davesmusicdatabase.blogspot.com/feeds/posts/default?alt=rss" rel="alternate" title="Dave's Music Database - RSS" type="application/rss+xml"/>
    <link href="https://www.blogger.com/feeds/1443292966174170672/posts/default" rel="service.post" title="Dave's Music Database - Atom" type="application/atom+xml"/>
    <link href="https://davesmusicdatabase.blogspot.com/feeds/6640189637110144996/comments/default" rel="alternate" title="Dave's Music Database - Atom" type="application/atom+xml"/>
    <!--Can't find substitution for tag [blog.ieCssRetrofitLinks]-->
    <link href="https://musiccanada.files.wordpress.com/2017/06/decades.jpg?w=350&amp;h=200&amp;crop=1" rel="image_src"/>
    <meta content="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html" property="og:url"/>
    <meta content="The Top Songs by Decade, 1890-2019" property="og:title"/>
    <meta content="  image from musiccanada.files.wordpress.com   Top Songs by Decade:  1890-2019  Dave’s Music Database has compiled the best songs of all-tim..." property="og:description"/>
    <meta content="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2pbei1RaGxhl1If9Jg5HEcK3w5QWdQHGE1Cen1PwnDoAHmZgYF3wMgUoJE6kWZ6jqR1hG9mlaISmJZL0wX_n_hhpJSvUvpC30OM6lKudowaFBFR-jSlTUBY1JkZ4BpwnVx1Ewil4ORdQEIIKSkQig=w1200-h630-p-k-no-nu" property="og:image"/>
    <title>Dave's Music Database: The Top Songs by Decade, 1890-2019</title>
    <style id="page-skin-1" type="text/css"><!--
    /*
    -----------------------------------------------
    Blogger Template Style
    Name:     Simple
    Designer: Blogger
    URL:      www.blogger.com
    ----------------------------------------------- */
    /* Content
    ----------------------------------------------- */
    body {
    font: normal normal 12px 'Trebuchet MS', Trebuchet, Verdana, sans-serif;
    color: #666666;
    background: #ffffff none repeat scroll top left;
    padding: 0 0 0 0;
    }
    html body .region-inner {
    min-width: 0;
    max-width: 100%;
    width: auto;
    }
    h2 {
    font-size: 22px;
    }
    a:link {
    text-decoration:none;
    color: #2288bb;
    }
    a:visited {
    text-decoration:none;
    color: #888888;
    }
    a:hover {
    text-decoration:underline;
    color: #33aaff;
    }
    .body-fauxcolumn-outer .fauxcolumn-inner {
    background: transparent none repeat scroll top left;
    _background-image: none;
    }
    .body-fauxcolumn-outer .cap-top {
    position: absolute;
    z-index: 1;
    height: 400px;
    width: 100%;
    }
    .body-fauxcolumn-outer .cap-top .cap-left {
    width: 100%;
    background: transparent none repeat-x scroll top left;
    _background-image: none;
    }
    .content-outer {
    -moz-box-shadow: 0 0 0 rgba(0, 0, 0, .15);
    -webkit-box-shadow: 0 0 0 rgba(0, 0, 0, .15);
    -goog-ms-box-shadow: 0 0 0 #333333;
    box-shadow: 0 0 0 rgba(0, 0, 0, .15);
    margin-bottom: 1px;
    }
    .content-inner {
    padding: 10px 40px;
    }
    .content-inner {
    background-color: #ffffff;
    }
    /* Header
    ----------------------------------------------- */
    .header-outer {
    background: transparent none repeat-x scroll 0 -400px;
    _background-image: none;
    }
    .Header h1 {
    font: normal normal 40px 'Trebuchet MS',Trebuchet,Verdana,sans-serif;
    color: #000000;
    text-shadow: 0 0 0 rgba(0, 0, 0, .2);
    }
    .Header h1 a {
    color: #000000;
    }
    .Header .description {
    font-size: 18px;
    color: #000000;
    }
    .header-inner .Header .titlewrapper {
    padding: 22px 0;
    }
    .header-inner .Header .descriptionwrapper {
    padding: 0 0;
    }
    /* Tabs
    ----------------------------------------------- */
    .tabs-inner .section:first-child {
    border-top: 0 solid #dddddd;
    }
    .tabs-inner .section:first-child ul {
    margin-top: -1px;
    border-top: 1px solid #dddddd;
    border-left: 1px solid #dddddd;
    border-right: 1px solid #dddddd;
    }
    .tabs-inner .widget ul {
    background: transparent none repeat-x scroll 0 -800px;
    _background-image: none;
    border-bottom: 1px solid #dddddd;
    margin-top: 0;
    margin-left: -30px;
    margin-right: -30px;
    }
    .tabs-inner .widget li a {
    display: inline-block;
    padding: .6em 1em;
    font: normal normal 12px 'Trebuchet MS', Trebuchet, Verdana, sans-serif;
    color: #000000;
    border-left: 1px solid #ffffff;
    border-right: 1px solid #dddddd;
    }
    .tabs-inner .widget li:first-child a {
    border-left: none;
    }
    .tabs-inner .widget li.selected a, .tabs-inner .widget li a:hover {
    color: #000000;
    background-color: #eeeeee;
    text-decoration: none;
    }
    /* Columns
    ----------------------------------------------- */
    .main-outer {
    border-top: 0 solid transparent;
    }
    .fauxcolumn-left-outer .fauxcolumn-inner {
    border-right: 1px solid transparent;
    }
    .fauxcolumn-right-outer .fauxcolumn-inner {
    border-left: 1px solid transparent;
    }
    /* Headings
    ----------------------------------------------- */
    div.widget > h2,
    div.widget h2.title {
    margin: 0 0 1em 0;
    font: normal bold 11px 'Trebuchet MS',Trebuchet,Verdana,sans-serif;
    color: #000000;
    }
    /* Widgets
    ----------------------------------------------- */
    .widget .zippy {
    color: #999999;
    text-shadow: 2px 2px 1px rgba(0, 0, 0, .1);
    }
    .widget .popular-posts ul {
    list-style: none;
    }
    /* Posts
    ----------------------------------------------- */
    h2.date-header {
    font: normal bold 11px Arial, Tahoma, Helvetica, FreeSans, sans-serif;
    }
    .date-header span {
    background-color: #bbbbbb;
    color: #ffffff;
    padding: 0.4em;
    letter-spacing: 3px;
    margin: inherit;
    }
    .main-inner {
    padding-top: 35px;
    padding-bottom: 65px;
    }
    .main-inner .column-center-inner {
    padding: 0 0;
    }
    .main-inner .column-center-inner .section {
    margin: 0 1em;
    }
    .post {
    margin: 0 0 45px 0;
    }
    h3.post-title, .comments h4 {
    font: normal normal 22px 'Trebuchet MS',Trebuchet,Verdana,sans-serif;
    margin: .75em 0 0;
    }
    .post-body {
    font-size: 110%;
    line-height: 1.4;
    position: relative;
    }
    .post-body img, .post-body .tr-caption-container, .Profile img, .Image img,
    .BlogList .item-thumbnail img {
    padding: 2px;
    background: #ffffff;
    border: 1px solid #eeeeee;
    -moz-box-shadow: 1px 1px 5px rgba(0, 0, 0, .1);
    -webkit-box-shadow: 1px 1px 5px rgba(0, 0, 0, .1);
    box-shadow: 1px 1px 5px rgba(0, 0, 0, .1);
    }
    .post-body img, .post-body .tr-caption-container {
    padding: 5px;
    }
    .post-body .tr-caption-container {
    color: #666666;
    }
    .post-body .tr-caption-container img {
    padding: 0;
    background: transparent;
    border: none;
    -moz-box-shadow: 0 0 0 rgba(0, 0, 0, .1);
    -webkit-box-shadow: 0 0 0 rgba(0, 0, 0, .1);
    box-shadow: 0 0 0 rgba(0, 0, 0, .1);
    }
    .post-header {
    margin: 0 0 1.5em;
    line-height: 1.6;
    font-size: 90%;
    }
    .post-footer {
    margin: 20px -2px 0;
    padding: 5px 10px;
    color: #666666;
    background-color: #eeeeee;
    border-bottom: 1px solid #eeeeee;
    line-height: 1.6;
    font-size: 90%;
    }
    #comments .comment-author {
    padding-top: 1.5em;
    border-top: 1px solid transparent;
    background-position: 0 1.5em;
    }
    #comments .comment-author:first-child {
    padding-top: 0;
    border-top: none;
    }
    .avatar-image-container {
    margin: .2em 0 0;
    }
    #comments .avatar-image-container img {
    border: 1px solid #eeeeee;
    }
    /* Comments
    ----------------------------------------------- */
    .comments .comments-content .icon.blog-author {
    background-repeat: no-repeat;
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAASCAYAAABWzo5XAAAAAXNSR0IArs4c6QAAAAZiS0dEAP8A/wD/oL2nkwAAAAlwSFlzAAALEgAACxIB0t1+/AAAAAd0SU1FB9sLFwMeCjjhcOMAAAD+SURBVDjLtZSvTgNBEIe/WRRnm3U8RC1neQdsm1zSBIU9VVF1FkUguQQsD9ITmD7ECZIJSE4OZo9stoVjC/zc7ky+zH9hXwVwDpTAWWLrgS3QAe8AZgaAJI5zYAmc8r0G4AHYHQKVwII8PZrZFsBFkeRCABYiMh9BRUhnSkPTNCtVXYXURi1FpBDgArj8QU1eVXUzfnjv7yP7kwu1mYrkWlU33vs1QNu2qU8pwN0UpKoqokjWwCztrMuBhEhmh8bD5UDqur75asbcX0BGUB9/HAMB+r32hznJgXy2v0sGLBcyAJ1EK3LFcbo1s91JeLwAbwGYu7TP/3ZGfnXYPgAVNngtqatUNgAAAABJRU5ErkJggg==);
    }
    .comments .comments-content .loadmore a {
    border-top: 1px solid #999999;
    border-bottom: 1px solid #999999;
    }
    .comments .comment-thread.inline-thread {
    background-color: #eeeeee;
    }
    .comments .continue {
    border-top: 2px solid #999999;
    }
    /* Accents
    ---------------------------------------------- */
    .section-columns td.columns-cell {
    border-left: 1px solid transparent;
    }
    .blog-pager {
    background: transparent url(https://resources.blogblog.com/blogblog/data/1kt/simple/paging_dot.png) repeat-x scroll top center;
    }
    .blog-pager-older-link, .home-link,
    .blog-pager-newer-link {
    background-color: #ffffff;
    padding: 5px;
    }
    .footer-outer {
    border-top: 1px dashed #bbbbbb;
    }
    /* Mobile
    ----------------------------------------------- */
    body.mobile  {
    background-size: auto;
    }
    .mobile .body-fauxcolumn-outer {
    background: transparent none repeat scroll top left;
    }
    .mobile .body-fauxcolumn-outer .cap-top {
    background-size: 100% auto;
    }
    .mobile .content-outer {
    -webkit-box-shadow: 0 0 3px rgba(0, 0, 0, .15);
    box-shadow: 0 0 3px rgba(0, 0, 0, .15);
    }
    .mobile .tabs-inner .widget ul {
    margin-left: 0;
    margin-right: 0;
    }
    .mobile .post {
    margin: 0;
    }
    .mobile .main-inner .column-center-inner .section {
    margin: 0;
    }
    .mobile .date-header span {
    padding: 0.1em 10px;
    margin: 0 -10px;
    }
    .mobile h3.post-title {
    margin: 0;
    }
    .mobile .blog-pager {
    background: transparent none no-repeat scroll top center;
    }
    .mobile .footer-outer {
    border-top: none;
    }
    .mobile .main-inner, .mobile .footer-inner {
    background-color: #ffffff;
    }
    .mobile-index-contents {
    color: #666666;
    }
    .mobile-link-button {
    background-color: #2288bb;
    }
    .mobile-link-button a:link, .mobile-link-button a:visited {
    color: #ffffff;
    }
    .mobile .tabs-inner .section:first-child {
    border-top: none;
    }
    .mobile .tabs-inner .PageList .widget-content {
    background-color: #eeeeee;
    color: #000000;
    border-top: 1px solid #dddddd;
    border-bottom: 1px solid #dddddd;
    }
    .mobile .tabs-inner .PageList .widget-content .pagelist-arrow {
    border-left: 1px solid #dddddd;
    }
    
    --></style>
    <style id="template-skin-1" type="text/css"><!--
    body {
    min-width: 1003px;
    }
    .content-outer, .content-fauxcolumn-outer, .region-inner {
    min-width: 1003px;
    max-width: 1003px;
    _width: 1003px;
    }
    .main-inner .columns {
    padding-left: 0px;
    padding-right: 260px;
    }
    .main-inner .fauxcolumn-center-outer {
    left: 0px;
    right: 260px;
    /* IE6 does not respect left and right together */
    _width: expression(this.parentNode.offsetWidth -
    parseInt("0px") -
    parseInt("260px") + 'px');
    }
    .main-inner .fauxcolumn-left-outer {
    width: 0px;
    }
    .main-inner .fauxcolumn-right-outer {
    width: 260px;
    }
    .main-inner .column-left-outer {
    width: 0px;
    right: 100%;
    margin-left: -0px;
    }
    .main-inner .column-right-outer {
    width: 260px;
    margin-right: -260px;
    }
    #layout {
    min-width: 0;
    }
    #layout .content-outer {
    min-width: 0;
    width: 800px;
    }
    #layout .region-inner {
    min-width: 0;
    width: auto;
    }
    body#layout div.add_widget {
    padding: 8px;
    }
    body#layout div.add_widget a {
    margin-left: 32px;
    }
    --></style>
    <link href="https://www.blogger.com/dyn-css/authorization.css?targetBlogID=1443292966174170672&amp;zx=12f138d1-f2a0-40bd-b3b1-08be66c68cf4" media="none" onload="if(media!='all')media='all'" rel="stylesheet"/><noscript><link href="https://www.blogger.com/dyn-css/authorization.css?targetBlogID=1443292966174170672&amp;zx=12f138d1-f2a0-40bd-b3b1-08be66c68cf4" rel="stylesheet"/></noscript>
    <meta content="ca-host-pub-1556223355139109" name="google-adsense-platform-account"/>
    <meta content="blogspot.com" name="google-adsense-platform-domain"/>
    <!-- data-ad-client=ca-pub-2683813143377667 -->
    </head>
    <body class="loading variant-simplysimple">
    <div class="navbar section" id="navbar" name="Navbar"><div class="widget Navbar" data-version="1" id="Navbar1"><script type="text/javascript">
        function setAttributeOnload(object, attribute, val) {
          if(window.addEventListener) {
            window.addEventListener('load',
              function(){ object[attribute] = val; }, false);
          } else {
            window.attachEvent('onload', function(){ object[attribute] = val; });
          }
        }
      </script>
    <div id="navbar-iframe-container"></div>
    <script src="https://apis.google.com/js/platform.js" type="text/javascript"></script>
    <script type="text/javascript">
          gapi.load("gapi.iframes:gapi.iframes.style.bubble", function() {
            if (gapi.iframes && gapi.iframes.getContext) {
              gapi.iframes.getContext().openChild({
                  url: 'https://www.blogger.com/navbar.g?targetBlogID\x3d1443292966174170672\x26blogName\x3dDave\x27s+Music+Database\x26publishMode\x3dPUBLISH_MODE_BLOGSPOT\x26navbarType\x3dLIGHT\x26layoutType\x3dLAYOUTS\x26searchRoot\x3dhttps://davesmusicdatabase.blogspot.com/search\x26blogLocale\x3den\x26v\x3d2\x26homepageUrl\x3dhttps://davesmusicdatabase.blogspot.com/\x26targetPostID\x3d6640189637110144996\x26blogPostOrPageUrl\x3dhttps://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html\x26vt\x3d-3890461336695527137',
                  where: document.getElementById("navbar-iframe-container"),
                  id: "navbar-iframe"
              });
            }
          });
        </script><script type="text/javascript">
    (function() {
    var script = document.createElement('script');
    script.type = 'text/javascript';
    script.src = '//pagead2.googlesyndication.com/pagead/js/google_top_exp.js';
    var head = document.getElementsByTagName('head')[0];
    if (head) {
    head.appendChild(script);
    }})();
    </script>
    </div></div>
    <div class="body-fauxcolumns">
    <div class="fauxcolumn-outer body-fauxcolumn-outer">
    <div class="cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left">
    <div class="fauxborder-right"></div>
    <div class="fauxcolumn-inner">
    </div>
    </div>
    <div class="cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    </div>
    <div class="content">
    <div class="content-fauxcolumns">
    <div class="fauxcolumn-outer content-fauxcolumn-outer">
    <div class="cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left">
    <div class="fauxborder-right"></div>
    <div class="fauxcolumn-inner">
    </div>
    </div>
    <div class="cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    </div>
    <div class="content-outer">
    <div class="content-cap-top cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left content-fauxborder-left">
    <div class="fauxborder-right content-fauxborder-right"></div>
    <div class="content-inner">
    <header>
    <div class="header-outer">
    <div class="header-cap-top cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left header-fauxborder-left">
    <div class="fauxborder-right header-fauxborder-right"></div>
    <div class="region-inner header-inner">
    <div class="header section" id="header" name="Header"><div class="widget Header" data-version="1" id="Header1">
    <div id="header-inner">
    <a href="https://davesmusicdatabase.blogspot.com/" style="display: block">
    <img alt="Dave's Music Database" height="173px; " id="Header1_headerimg" src="//1.bp.blogspot.com/-nNjjcPXZ-Xo/X8pDAGeUcQI/AAAAAAAACzw/CGNRw9OITFUNzWj95cBYeSoQG4axtdX8wCK4BGAYYCw/s1600/banner_purple.jpg" style="display: block" width="900px; "/>
    </a>
    <div class="descriptionwrapper">
    <p class="description"><span>DavesMusicDatabase.com is devoted to ranking, rating, and reviewing music of all genres and eras. The DMDB blog serves up album and song reviews, best-of lists, music history snapshots, and music-related essays.</span></p>
    </div>
    </div>
    </div></div>
    </div>
    </div>
    <div class="header-cap-bottom cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    </header>
    <div class="tabs-outer">
    <div class="tabs-cap-top cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left tabs-fauxborder-left">
    <div class="fauxborder-right tabs-fauxborder-right"></div>
    <div class="region-inner tabs-inner">
    <div class="tabs no-items section" id="crosscol" name="Cross-Column"></div>
    <div class="tabs section" id="crosscol-overflow" name="Cross-Column 2"><div class="widget PageList" data-version="1" id="PageList1">
    <h2>Pages</h2>
    <div class="widget-content">
    <ul>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/about-daves-music-database.html">Home</a>
    </li>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/best-of-lists.html">Best-of Lists</a>
    </li>
    <li>
    <a href="https://davesmusicdatabase.blogspot.com/p/podcast.html">Podcast</a>
    </li>
    <li>
    <a href="http://www.facebook.com/davesmusicdatabase">Facebook</a>
    </li>
    <li>
    <a href="https://davesmusicdatabase.blogspot.com/p/hall-of-fame.html">Hall of Fame</a>
    </li>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/books.html">Books</a>
    </li>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/aural-fixation.html">Aural Fixation</a>
    </li>
    <li>
    <a href="https://davesmusicdatabase.blogspot.com/p/the-all-time-music-makers-home-about.html">DMDB Encyclopedia</a>
    </li>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/birthdays.html">Birthdays</a>
    </li>
    <li>
    <a href="https://davesmusicdatabase.blogspot.com/p/concerts.html">Concerts</a>
    </li>
    <li>
    <a href="http://davesmusicdatabase.blogspot.com/p/links.html">Links</a>
    </li>
    <li>
    <a href="https://davesmusicdatabase.blogspot.com/p/index.html">Index</a>
    </li>
    </ul>
    <div class="clear"></div>
    </div>
    </div><div class="widget HTML" data-version="1" id="HTML1">
    <div class="widget-content">
    <table><center><b><i>Check out Dave’s Music Database books and more at <a href="http://writbywhit.blogspot.com/p/titles.html">WritbyWhit.com</a> or <a href="https://www.amazon.com/David-L.-Whitaker/e/B001KMOGJI/ref=sr_ntt_srch_lnk_1?qid=1500300514&amp;sr=8-1">David L. Whitaker's author page at Amazon.com</a>.</i></b> <p></p></center></table>
    <table align="center"><tr>
    <td>&lt;!—music of the 1980s--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2021/12/daves-music-database-book-music-of-1980s.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/413NbWFgBvL._SX398_BO1,204,203,200_.jpg"/></a>
    !—music&gt;</td>
    <td>&lt;!—the top songs of the digital era, 2000-2019--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2020/02/digital-era-2000-2019-top-100.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/51eQ2H38yyL._SX398_BO1,204,203,200_.jpg"/></a>
    !—the&gt;</td>
    <td>&lt;!—the top 100 songs of the rock era, 1954-1999--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2011/07/top-100-songs-of-rock-era-1954-1999.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/51gdBlDMc2L._UY250_.jpg"/></a>
    !—the&gt;</td>
    <td>&lt;!—the top 100 songs of the pre-rock era, 1890-1953--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2012/06/top-100-songs-of-pre-rock-era-1890-1953.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/51EhrD2kVOL._SX398_BO1,204,203,200_.jpg"/></a>
    !—the&gt;</td>
    <td>&lt;!—charting the classic rock hits, 1962-1981--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/p/books.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/41V0RWgZp1L._SX218_BO1,204,203,200_QL40_FMwebp_.jpg"/></a>
    !—charting&gt;</td>
    <td>&lt;!—the top 100 albums of the 21st century--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2020/12/top-100-albums-of-21st-century.html"><img height="100" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha0Jc9dKN5aSgVtCsVtnqpEIRx-rHAEqGcLASPPkzjWEwxb2zV7BAEPpn8X7nGgKKEouDuXOJHt-YimnLgqBmjRN9K2Jnoschqh0Xg6sr40vcRUsLaDy-_hopr_O6E5RKpQ0sOb9kGm_HqFniQ=s0-d"/></a>
    !—the&gt;</td>
    <td>&lt;!—the top 100 albums of all time--&gt;
    <a href="https://davesmusicdatabase.blogspot.com/2012/03/top-100-albums-of-all-time.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/51+nrNm1dCL._SX258_BO1,204,203,200_.jpg"/></a>
    !—the&gt;</td>
    <td>&lt;!—aural fixation--&gt;
    <a href="http://davesmusicdatabase.blogspot.com/p/books.html#aural_fixation"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/41Nu6CORUcL._SY291_BO1,204,203,200_QL40_FMwebp_.jpg"/></a>
    !—aural&gt;</td>
    <td>&lt;!—no one needs 21 versions of ‘purple haze’--&gt;
    <a href="http://davesmusicdatabase.blogspot.com/p/books.html#purple_haze"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/61bfsxos2YL._UY250_.jpg"/></a>
    !—no&gt;</td>
    <td>&lt;!—100 music activities--&gt;
    <a href="http://toolboxtraining.blogspot.com/2012/09/book-100-music-activities-for-kids.html"><img height="100" src="https://images-na.ssl-images-amazon.com/images/I/41TdW4xRjCL._UY250_.jpg"/></a>
    !—100&gt;</td>
    </tr></table>
    </div>
    <div class="clear"></div>
    </div></div>
    </div>
    </div>
    <div class="tabs-cap-bottom cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    <div class="main-outer">
    <div class="main-cap-top cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left main-fauxborder-left">
    <div class="fauxborder-right main-fauxborder-right"></div>
    <div class="region-inner main-inner">
    <div class="columns fauxcolumns">
    <div class="fauxcolumn-outer fauxcolumn-center-outer">
    <div class="cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left">
    <div class="fauxborder-right"></div>
    <div class="fauxcolumn-inner">
    </div>
    </div>
    <div class="cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    <div class="fauxcolumn-outer fauxcolumn-left-outer">
    <div class="cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left">
    <div class="fauxborder-right"></div>
    <div class="fauxcolumn-inner">
    </div>
    </div>
    <div class="cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    <div class="fauxcolumn-outer fauxcolumn-right-outer">
    <div class="cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left">
    <div class="fauxborder-right"></div>
    <div class="fauxcolumn-inner">
    </div>
    </div>
    <div class="cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    <!-- corrects IE6 width calculation -->
    <div class="columns-inner">
    <div class="column-center-outer">
    <div class="column-center-inner">
    <div class="main section" id="main" name="Main"><div class="widget Blog" data-version="1" id="Blog1">
    <div class="blog-posts hfeed">
    <div class="date-outer">
    <h2 class="date-header"><span>Friday, August 5, 2022</span></h2>
    <div class="date-posts">
    <div class="post-outer">
    <div class="post hentry uncustomized-post-template" itemprop="blogPost" itemscope="itemscope" itemtype="http://schema.org/BlogPosting">
    <meta content="https://musiccanada.files.wordpress.com/2017/06/decades.jpg?w=350&amp;h=200&amp;crop=1" itemprop="image_url"/>
    <meta content="1443292966174170672" itemprop="blogId"/>
    <meta content="6640189637110144996" itemprop="postId"/>
    <a name="6640189637110144996"></a>
    <h3 class="post-title entry-title" itemprop="name">
    The Top Songs by Decade, 1890-2019
    </h3>
    <div class="post-header">
    <div class="post-header-line-1"></div>
    </div>
    <div class="post-body entry-content" id="post-body-6640189637110144996" itemprop="description articleBody">
    <style> a:hover{color:red} a:link{color:blue} a:visited{color:purple} H1 {font-family: arial; font-size: 24pt; color: white} H2 {font-family: arial; font-size: 18pt; color: black} H3 {font-family: arial; font-size: 12pt; color: blue} </style><table border="0" cellpadding="10" cellspacing="0" width="640"><tr><td bgcolor="blue">
    <!--&#8212;Image ----><img border="0" src="https://musiccanada.files.wordpress.com/2017/06/decades.jpg?w=350&amp;h=200&amp;crop=1" width="350"/><p><font color="white"></font></p><center><i>image from musiccanada.files.wordpress.com</i></center></td><td bgcolor="blue"><h1>
    
    Top Songs by Decade:</h1><i><h2>
    1890-2019</h2></i></td></tr></table><table border="10" bordercolor="blue" cellpadding="10" width="640"><tr><td bgcolor="#d6eaf8"><p>
    Dave’s Music Database has compiled the best songs of all-time into a variety of lists over the years. Check out the full array of DMDB best-of lists <a href="http://davesmusicdatabase.blogspot.com/p/best-of-lists.html">here</a>. However, this page – which at 72,000+ hits is the second most visited on the DMDB blog – offers snapshots of the top 10 songs of each decade from 1890 to present. </p><p>
    <a href="https://davesmusicdatabase.blogspot.com/p/best-of-lists.html#songs-era">Click here to see ‘Top 100 Songs of the Decade’ lists</a> or click on the corresponding badges below. 
    
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2017/10/the-top-50-songs-from-2010-2016.html" title="2010-2019: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha1MS7Jtbdvypw8BI4BRQf2l44ZFt3km5CnV86YeO-1RNHy_8EKtG8p42L43MIfvsPybdkbYk7eybyZtycuyp5cuhvK64ZLiRzk26w-BCYwK5D3Hv8NtijOQbvmCpHeyK-Q=s0-d"/></a></center><p>
    
    1.	Mark Ronson with Bruno Mars “<a href="http://davesmusicdatabase.blogspot.com/2015/04/april-18-2015-uptown-funk-lands-14th.html">Uptown Funk!</a>” (2014) <br/>
    2.	Ed Sheeran “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1282017-ed-sheeran-debuts-at-1-with.html">Shape of You</a>” (2017) <br/>
    3.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2011/12/2011-song-of-year-adeles-rolling-in.html">Rolling in the Deep</a>” (2010) <br/>
    4.	Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2014/03/pharrell-williams-hit-1-in-us-with-happy.html">Happy</a>” (2013) <br/>
    5.	Luis Fonsi with Daddy Yankee &amp; Justin Bieber “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1122017-despacito-is-released.html">Despacito</a>” (2017) <br/>
    6.	Gotye with Kimbra “<a href="http://www.davesmusicdatabase.blogspot.com/2013/01/gotye-charts-with-somebody-that-i-used.html">Somebody That I Used to Know</a>” (2011) <br/>
    7.	Robin Thicke with T.I. &amp; Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2013/03/robin-thickes-blurred-lines-released.html">Blurred Lines</a>” (2013)<br/>
    8.	Carly Rae Jepsen “<a href="http://davesmusicdatabase.blogspot.com/2011/09/september-20-2011-call-me-maybe-is.html">Call Me Maybe</a>” (2011) <br/>
    9.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2015/11/adeles-hello-debuts-at-1.html">Hello</a>” (2015) <br/>
    10.	Lil Nas X with Billy Ray Cyrus “<a href="https://davesmusicdatabase.blogspot.com/2019/07/old-town-road-lands-14th-week-at-1.html">Old Town Road</a>” (2018) <br/>
    </p><p></p><center><!--&#8212;Video: Uptown Funk----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/OPf0YbXqDm0" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2017/10/the-top-100-songs-from-2000-2009.html" title="2000-2009: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha1EWPAcpOmFYDs7jvDCek3pTINMXheF2xEcxrtqNeJNZaZwkNy11A0fPNaTPqvAXyUBZClLiyMJRsMNSaAtHqRZIC9k5yieNvcnRsGjmvuD7IbOEbKGXoQp_YY2qBmeE6E=s0-d"/></a></center><p>
    
    1.	OutKast “<a href="http://davesmusicdatabase.blogspot.com/2011/10/outkast-charted-with-song-of-decade-hey.html">Hey Ya!</a>” (2003) <br/>
    2.	Black Eyed Peas “<a href="http://davesmusicdatabase.blogspot.com/2011/07/black-eyed-peas-knock-themselves-from-1.html">I Gotta Feeling</a>” (2009) <br/>
    3.	Eminem “<a href="http://davesmusicdatabase.blogspot.com/2011/10/eminem-charts-with-lose-yourself.html">Lose Yourself</a>” (2002) <br/>
    4.	Usher with Lil’ Jon &amp; Ludacris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/usher-launches-his-first-of-28-weeks-at.html">Yeah!</a>” (2004) <br/>
    5.	Beyoncé with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2003/07/beyonce-hits-1-with-crazy-in-love-july.html">Crazy in Love</a>” (2003) <br/>
    6.	Gnarls Barkley “<a href="http://davesmusicdatabase.blogspot.com/2006/04/4292006-gnarls-barkley-charts-with-crazy.html">Crazy</a>” (2006) <br/>
    7.	Beyoncé “<a href="http://davesmusicdatabase.blogspot.com/2011/12/beyonce-hit-1-with-single-ladies.html">Single Ladies (Put a Ring on It)</a>” (2008) <br/>
    8.	Rihanna with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2007/06/rihanna-hit-1-with-umbrella-june-9-2007.html">Umbrella</a>” (2007) <br/>
    9.	Flo Rida with T-Pain “<a href="http://davesmusicdatabase.blogspot.com/2008/03/flo-ridas-low-spends-10th-week-at-1.html">Low</a>” (2007) <br/>
    10.	Mariah Carey “<a href="http://davesmusicdatabase.blogspot.com/2012/06/mariah-carey-hit-1-with-we-belong.html">We Belong Together</a>” (2005) <br/>
    </p><p></p><center><!--&#8212;Video: Hey Ya ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/PWgvGjAhvIw" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/08/top-songs-from-1990-to-1999.html" title="1990-1999: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha09e3cDRtR1uBO1tZM-eyZcADfm--sh84ke6nBHFQerqzTfTlIVKrFE-7v3qKsOr9K-G8Ugnwxr16eSEsFJ9p9ScbcbKmXon2j6p9K1tEzBVUkwN3I0LyZWrEu-1jeB2YU=s0-d"/></a></center><p>
    
    1.	Whitney Houston “<a href="http://davesmusicdatabase.blogspot.com/2011/11/whitney-houston-hit-1-with-i-will.html">I Will Always Love You</a>” (1992) <br/>
    2.	Nirvana “<a href="http://davesmusicdatabase.blogspot.com/1991/09/nirvana-charted-with-smells-like-teen.html">Smells Like Teen Spirit</a>” (1991) <br/>
    3.	Bryan Adams “<a href="http://davesmusicdatabase.blogspot.com/2012/06/bryan-adams-charted-with-everything-i.html">(Everything I Do) I Do It for You</a>” (1991) <br/>
    4.	Sinéad O’Connor “<a href="http://davesmusicdatabase.blogspot.com/2013/01/sinead-oconnor-charted-with-nothing.html">Nothing Compares 2 U</a>” (1990) <br/>
    5.	Celine Dion “<a href="http://davesmusicdatabase.blogspot.com/1998/02/celine-dion-hit-1-with-my-heart-will-go.html">My Heart Will Go On</a>” (1997) <br/>
    6.	Elton John “<a href="http://davesmusicdatabase.blogspot.com/2011/09/elton-john-performs-candle-in-wind-at.html">Candle in the Wind 1997 (Goodbye England’s Rose)</a>” (1997) <br/>
    7.	R.E.M. “<a href="http://davesmusicdatabase.blogspot.com/1991/03/rem-charts-with-losing-my-religion.html">Losing My Religion</a>” (1991) <br/>
    8.	Oasis “<a href="http://davesmusicdatabase.blogspot.com/1995/11/oasis-chart-with-wonderwall.html">Wonderwall</a>” (1995) <br/>
    9.	Los Del Rio “<a href="https://davesmusicdatabase.blogspot.com/1996/11/macarena-spends-14th-week-on-top.html">Macarena (Bayside Boys Mix)</a>” (1995) <br/>
    10.	U2 “<a href="https://davesmusicdatabase.blogspot.com/1992/01/141992-u2-charted-with-one.html">One</a>” (1991) <br/>
    </p><p></p><center><!--&#8212;Video: I Will Always Love You ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/3JWTaaS7LdU" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/08/top-100-songs-from-1980-to-1989.html" title="1980-1989: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3a2e40S91MpUXPsA0agIEsoG1B76tgIUxs_G8CBgPXPvAEZSvblf3hTqVOvrud58Or7BwspfiYklNIuCvbl1e_V2OV_zCtP69AXjubozUj-JP0htMCh5zjHvAlFz92Sq8=s0-d"/></a></center><p>
    
    1.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/2013/01/michael-jackson-charted-with-billie.html">Billie Jean</a>” (1982) <br/>
    2.	The Police “<a href="http://davesmusicdatabase.blogspot.com/2012/07/police-hit-1-with-every-breath-you-take.html">Every Breath You Take</a>” (1983) <br/>
    3.	Guns N’ Roses “<a href="http://davesmusicdatabase.blogspot.com/2012/06/guns-n-roses-charted-with-sweet-child-o.html">Sweet Child O’ Mine</a>” (1987) <br/>
    4.	Prince “<a href="http://davesmusicdatabase.blogspot.com/2012/06/prince-charted-with-when-doves-cry-june.html">When Doves Cry</a>” (1984) <br/>
    5.	Joan Jett &amp; the Blackhearts “<a href="http://davesmusicdatabase.blogspot.com/1981/12/12121981-joan-jett-rocks-charts.html">I Love Rock and Roll</a>” (1981) <br/>
    6.	U2 “<a href="http://davesmusicdatabase.blogspot.com/1987/05/5161987-u2-hit-1-with-with-or-without.html">With or Without You</a>” (1987) <br/>
    7.	Bon Jovi “<a href="https://davesmusicdatabase.blogspot.com/1987/02/bon-jovi-hit-1-with-livin-on-prayer.html">Livin’ on a Prayer</a>” (1986) <br/>
    8.	Lionel Richie &amp; Diana Ross “<a href="http://davesmusicdatabase.blogspot.com/2012/07/lionel-richie-and-diana-ross-debuted.html">Endless Love</a>” (1981) <br/>
    9.	Van Halen “<a href="https://davesmusicdatabase.blogspot.com/1984/02/van-halen-hit-1-with-jump.html">Jump</a>” (1984) <br/>
    10.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/1983/04/beat-it-becomes-michael-jacksons-second.html">Beat It</a>” (1983) <br/>
    </p><p></p><center><!--&#8212;Video: Billie Jean----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/Zi_XLOBDo_Y" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/08/top-songs-from-1970-1979.html" title="1970-1979: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha12-dY61VIzmykntjDRBtNNHLYqJjt666hv3sYlkzoJJlSZHoesSFN-ewsr_ZamEUF_6aVu4a5WVTXhKxqvxfsE45drtBb0F2uP6qYITMbzdysZgfPSdOtyZGps1Ic4DT4=s0-d"/></a></center><p>
    
    1.	Queen “<a href="http://davesmusicdatabase.blogspot.com/2011/11/queen-charted-with-bohemian-rhapsody.html">Bohemian Rhapsody</a>” (1975) <br/>
    2.	John Lennon “<a href="http://davesmusicdatabase.blogspot.com/1971/10/john-lennon-charted-with-imagine.html">Imagine</a>” (1971) <br/>
    3.	Bee Gees “<a href="http://davesmusicdatabase.blogspot.com/1978/02/bee-gees-hit-1-with-stayin-alive.html">Stayin’ Alive</a>” (1977) <br/>
    4.	Simon &amp; Garfunkel “<a href="http://davesmusicdatabase.blogspot.com/2012/02/simon-garfunkel-hit-1-with-bridge-over.html">Bridge Over Troubled Water</a>” (1970) <br/>
    5.	Eagles “<a href="http://davesmusicdatabase.blogspot.com/2012/05/eagles-hotel-california-hit-1-may-7.html">Hotel California</a>” (1976) <br/>
    6.	Led Zeppelin “<a href="http://davesmusicdatabase.blogspot.com/1971/11/led-zeppelins-stairway-to-heaven-was.html">Stairway to Heaven</a>” (1971) <br/>
    7.	Don McLean “<a href="http://davesmusicdatabase.blogspot.com/2012/01/don-mcleans-american-pie-hit-1-january.html">American Pie</a>” (1971) <br/>
    8.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/1970/04/the-beatles-hit-1-with-let-it-be-april.html">Let It Be</a>” (1970) <br/>
    9.	Stevie Wonder “<a href="http://davesmusicdatabase.blogspot.com/1972/11/11111972-stevie-wonder-charts-with.html">Superstition</a>” (1972) <br/>
    10.	Derek &amp; the Dominos “<a href="http://davesmusicdatabase.blogspot.com/2012/03/derek-and-dominos-charted-with-layla.html">Layla</a>” (1970) <br/>
    </p><p></p><center><!--&#8212;Video: Bohemian Rhapsody----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/fJ9rUzIMcZQ" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/08/top-100-songs-from-1960-1969_2.html" title="1960-1969: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2xP5Gkph5Zw6bywyeRwpEc4dlsSJIDlGsVUr1039WrP433R9WakCC9Z-rAUqROaGIQfeB8Oj-FnSVmOj31i17kVqRcMMaIkAUO_npc5__pp0zic_VhQFCdgf88l-jGzeE=s0-d"/></a></center><p>
    
    1.	The Rolling Stones “<a href="http://davesmusicdatabase.blogspot.com/2015/07/50-years-ago-today-rolling-stones-hit-1.html">(I Can’t Get No) Satisfaction</a>” (1965) <br/>
    2.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2018/11/50-years-ago-today-hey-jude-spent-9th.html">Hey Jude</a>” (1968) <br/>
    3.	Marvin Gaye “<a href="http://davesmusicdatabase.blogspot.com/2011/11/marvin-gayes-i-heard-it-through.html">I Heard It Through the Grapevine</a>” (1968) <br/>
    4.	Aretha Franklin “<a href="http://davesmusicdatabase.blogspot.com/2012/06/aretha-franklin-hit-1-with-respect-june.html">Respect</a>” (1967) <br/>
    5.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2014/02/50-years-ago-today-beatles-hit-1-in-us.html">I Want to Hold Your Hand</a>” (1963) <br/>
    6.	The Beach Boys “<a href="http://davesmusicdatabase.blogspot.com/2011/10/beach-boys-charted-with-good-vibrations.html">Good Vibrations</a>” (1966) <br/>
    7.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/2013/10/the-beatles-hit-1-with-yesterday.html">Yesterday</a>” (1965) <br/>
    8.	Bob Dylan “<a href="http://davesmusicdatabase.blogspot.com/2011/07/bob-dylans-like-rolling-stone-debuts-on.html">Like a Rolling Stone</a>” (1965) <br/>
    9.	Otis Redding “<a href="http://davesmusicdatabase.blogspot.com/2014/01/otis-reddings-sittin-on-dock-of-bay-is.html">(Sittin’ on) The Dock of the Bay</a>” (1968) <br/>
    10.	The Animals “<a href="http://davesmusicdatabase.blogspot.com/2012/06/animals-charted-with-house-of-rising.html">The House of the Rising Sun</a>”(1964) <br/>
    </p><p></p><center><!--&#8212;Video: Satisfaction ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/1ANhU4AcK04" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1950-to-1959.html" title="1950-1959: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3YNvRlkYybWewK43q5Vx_Uw36Y7Fw1ry6ReX-cr2Osmgkx4VsH14W3a0LWpNkvJQpVRs_dbc6t_4hlMvmi-luXmOfHb4eO9B8tai7J5mkDNk3ZUtGdDHkBq1vNQ2wTj_s=s0-d"/></a></center><p>
    
    1.	Bill Haley &amp; His Comets “<a href="http://davesmusicdatabase.blogspot.com/2010/07/happy-birthday-rock-and-roll-55-years.html">We’re Gonna Rock Around the Clock</a>” (1954) <br/>
    2.	Bobby Darin “<a href="http://davesmusicdatabase.blogspot.com/2011/08/bobby-darin-charts-with-mack-knife.html">Mack the Knife</a>” (1959) <br/>
    3.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2014/04/elvis-presley-hit-1-with-heartbreak.html">Heartbreak Hotel</a>” (1956) <br/>
    4.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2011/07/elvis-presley-performs-for-hound-dog.html">Hound Dog</a>” (1956) <br/>
    5.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2013/08/elvis-presley-hit-1-with-dont-be-cruel.html">Don’t Be Cruel</a>” (1956) <br/>
    6.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2007/09/fifty-years-ago-today-elvis-presley.html">Jailhouse Rock</a>” (1957) <br/>
    7.	Chuck Berry “<a href="http://davesmusicdatabase.blogspot.com/2014/04/chuck-berry-charted-with-johnny-b-goode.html">Johnny B. Goode</a>” (1958) <br/>
    8.	Patti Page “<a href="http://davesmusicdatabase.blogspot.com/2011/11/patti-page-charted-with-tennessee-waltz.html">Tennessee Waltz</a>” (1950) <br/>
    9.	Ray Charles “<a href="http://davesmusicdatabase.blogspot.com/2009/02/fifty-years-ago-today-ray-charles.html">What’d I Say</a>” (1959) <br/>
    10.	The Everly Brothers “<a href="http://davesmusicdatabase.blogspot.com/2008/06/fifty-years-ago-today-everly-brothers.html">All I Have to Do Is Dream</a>” (1958) <br/>
    </p><p></p><center><!--&#8212;Video: Rock Around the Clock ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/dWvVflBMTYs" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1940-1949.html" title="1940-1949: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha0zix18hWYLj_MFlxW3y3sFvvltuDt5VDheA_I2so2SgyLZExno8UND845LasntV8nkQZpw0CKh7sKXI24a4pEpOMZMR70cmqtp7Sxu06Y_8pwuWryR0630aKzxnY2KNuU=s0-d"/></a></center><p>
    
    1.	Bing Crosby with the Ken Darby Singers “<a href="http://davesmusicdatabase.blogspot.com/2011/10/bing-crosby-hit-1-with-white-christmas.html">White Christmas</a>” (1942) <br/> 
    2.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2012/01/artie-shaw-charted-with-star-dust.html">Stardust</a>” (1941) <br/> 
    3.	Gene Autry “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1231949-gene-autry-charts-with-rudolph.html">Rudolph, the Red-Nosed Reindeer</a>” (1949) <br/> 
    4.	Glenn Miller with Tex Beneke &amp; the Four Modernaires “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11291941-glenn-miller-hits-1-with.html">Chattanooga Choo Choo</a>” (1941) <br/> 
    5.	Les Brown with Doris Day “<a href="http://davesmusicdatabase.blogspot.com/2016/03/331945-les-brown-charts-with.html">Sentimental Journey</a>” (1945) <br/> 
    6.	Nat “King” Cole “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11231946-nat-king-cole-charted-with.html">The Christmas Song (Chestnuts Roasting on an Open Fire)</a>” (1946) <br/>
    7.	Tommy Dorsey with Frank Sinatra &amp; The Pied Pipers “<a href="http://davesmusicdatabase.blogspot.com/2011/07/frank-sinatra-hits-1-for-first-time_27.html">I’ll Never Smile Again</a>” (1940) <br/>
    8.	Cliff Edwards “<a href="http://davesmusicdatabase.blogspot.com/2013/02/cliff-edwards-charted-with-when-you.html">When You Wish Upon a Star</a>” (1940) <br/> 
    9.	Duke Ellington “<a href="http://davesmusicdatabase.blogspot.com/2011/07/duke-ellington-charts-with-take-a-train.html">Take the ‘A’ Train</a>” (1941) <br/> 
    10.	Dooley Wilson “<a href="http://davesmusicdatabase.blogspot.com/2014/11/as-time-goes-by-immortalized-by.html">As Time Goes By</a>” (1942) <br/>
    </p><p></p><center><!--&#8212;Video: White Christmas ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/P8Ozdqzjigg" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-of-1930-1939.html" title="1930-1939: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3IN7okThIoqpU6OvMJvtxH4LtDl9BEpJMcXTcqimbwRBIkgZ4fohLhQR0uDr6g6D_mOKPtkOBh3UgCrYNTndN0UmgViqGCslHWlNRx2cK_BDZy5TV5s46yhMKb_46F47g=s0-d"/></a></center><p>
    
    1.	Judy Garland “<a href="http://davesmusicdatabase.blogspot.com/2011/09/judy-garland-charts-with-over-rainbow.html">Over the Rainbow</a>” (1939) <br/>
    2.	Glenn Miller “<a href="http://davesmusicdatabase.blogspot.com/2011/10/glenn-miller-charts-with-in-mood.html">In the Mood</a>” (1939) <br/> 
    3.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2011/12/fred-astaire-hit-1-with-cole-porters.html">Night and Day</a>” (1932) <br/> 
    4.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2013/08/cheek-to-cheek-hits-1-for-first-of-11.html">Cheek to Cheek</a>” (1935) <br/> 
    5.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2013/11/artie-shaws-beguin-beguine-hit-1.html">Begin the Beguine</a>” (1938) <br/> 
    6.	Ethel Waters “<a href="http://davesmusicdatabase.blogspot.com/2014/05/ethel-waters-charted-with-stormy.html">Stormy Weather (Keeps Rainin' All the Time)</a>” (1933) <br/> 
    7.	Fred Astaire with Johnny Green “<a href="http://davesmusicdatabase.blogspot.com/2016/10/1031936-fred-astaire-hits-1-with-way.html">The Way You Look Tonight</a>” (1936) <br/> 
    8.	Bing Crosby with the Guardsmen Quartette “<a href="https://davesmusicdatabase.blogspot.com/1985/12/bing-crosby-charted-with-silent-night.html">Silent Night</a>” (1935) <br/> 
    9.	Ella Fitzgerald with Chick Webb “<a href="http://davesmusicdatabase.blogspot.com/2012/06/ella-fitzgerald-hit-1-with-tisket.html">A-Tisket, A-Tasket</a>” (1938) <br/>
    10.	Tommy Dorsey with Jack Leonard “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1271940-tommy-dorsey-lands-at-1-with.html">All the Things You Are</a>” (1939) <br/>
    </p><p></p><center><!--&#8212;Video: Over the Rainbow ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/1HRa4X07jdE" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1920-1929.html" title="1920-1929: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2KAAUU-FIxQf6Xq9YsZtY_RjibNH88pemqkc2Ylij5Z4FdwDdXb5_YsitVa3gouZyyjapJdpF7NDtGoCcPlb6CaQxQ1My3sAWrXwioDERX1K4qmzNjT1DiPh7xH7qG7PU=s0-d"/></a></center><p>
    
    1.	Bessie Smith with Louis Armstrong “<a href="http://davesmusicdatabase.blogspot.com/2011/11/wc-handy-charted-with-st-louis-blues.html">St. Louis Blues</a>” (1925) <br/>
    2.	Al Jolson “<a href="https://davesmusicdatabase.blogspot.com/2010/05/al-jolson-hit-1-with-swanee-90-years.html">Swanee</a>” (1920) <br/> 
    3.	Gene Austin “<a href="http://davesmusicdatabase.blogspot.com/2013/12/my-blue-heaven-hit-1-december-17-1927.html">My Blue Heaven</a>” (1927) <br/>
    4.	Thomas “Fats” Waller “<a href="http://davesmusicdatabase.blogspot.com/2016/11/1111929-fats-waller-releases-aint.html">Ain’t Misbehavin’</a>” (1929) <br/>
    5.	Paul Whiteman “<a href="http://davesmusicdatabase.blogspot.com/2011/10/paul-whitemans-whispering-hit-1-october.html">Whispering</a>” (1920) <br/>
    6.	Al Jolson "<a href="https://davesmusicdatabase.blogspot.com/2013/01/al-jolson-charted-with-april-showers.html">April Showers</a>” (1922) <br/>
    7.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1241925-marion-harris-charted-with-tea.html">Tea for Two</a>” (1925) <br/>
    8.	Vernon Dalhart “<a href="http://davesmusicdatabase.blogspot.com/2011/08/vernon-dalhart-records-prisoners-song.html">The Prisoner’s Song</a>” (1925) <br/>
    9.	Ben Selvin “<a href="http://davesmusicdatabase.blogspot.com/2013/01/ben-selvin-charted-with-dardanella.html">Dardanella</a>” (1920) <br/>
    10.	Isham Jones “<a href="http://davesmusicdatabase.blogspot.com/2016/09/961924-isham-jones-takes-it-had-to-be.html">It Had to Be You</a>” (1924) <br/>
    </p><p></p><center><!--&#8212;Video: St. Louis Blues ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/3rd9IaA_uJI" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1910-1919.html" title="1910-1919: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha1eHC8xM_esyo48tExud-8XU2pagKOWs0rWjTLCa0NMe8FJUrN-Rn3qzkMGETgLMZNGHlNHy5ysyRo2XEZoC3IQXNZzXj-jYx1-fp_JQoePC7KARPUEzDRvZeO7chb55nQ=s0-d"/></a></center><p>
    
    1.	Arthur Collins &amp; Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2011/09/alexanders-ragtime-band-hits-1.html">Alexander’s Ragtime Band</a>” (1911) <br/>
    2.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/09/american-quartets-over-there-charts.html">Over There</a>” (1917) <br/>
    3.	Peerless Quartet “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1221911-peerless-quartet-hit-1-for.html">Let Me Call You Sweetheart</a>” (1911) <br/>
    4.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2014/10/al-jolson-topped-charts-with-you-made.html">You Made Me Love You (I Didn't Want to Do It)</a>” (1913) <br/>
    5.	Billy Murray with the Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/04/by-light-of-silvery-moon-hit-1-april-23.html">By the Light of the Silvery Moon</a>” (1910) <br/>
    6.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/moonlight-bay-hit-1-march-16-1912.html">Moonlight Bay</a>” (1912) <br/>
    7.	Original Dixieland Jazz Band “<a href="http://davesmusicdatabase.blogspot.com/2014/08/tiger-rag-charts-for-first-time-august.html">Tiger Rag</a>” (1918) <br/>
    8.	Sophie Tucker “<a href="http://davesmusicdatabase.blogspot.com/2014/07/sophie-tucker-charted-with-some-of.html">Some of These Days</a>” (1911) <br/>
    9.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/marion-harris-hit-1-with-after-youve.html">After You’ve Gone</a>” (1919) <br/>
    10.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2016/12/8171918-rock-bye-your-baby-with-dixie.html">Rock-a-Bye Your Baby with a Dixie Melody</a>” (1918) <br/>
    </p><p></p><center><!--&#8212;Video: Alexander&#8217;s Ragtime Band ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/8KDSJhanSSw" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1900-1909.html" title="1900-1909: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2pO0MdSqN7NliM4GVHA4ffgZQ3dlmHYFLxy2GhRGhOxZkNDgjZbNHZeGiN-Ne9dRJKdyw3ASGWzJWY7Un0PkCxaFhXXeCTxwbykBKyq5DMs14E8tfFK-6jgNKQVGprwdo=s0-d"/></a></center><p>
    
    1.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/07/take-me-out-to-ball-game-in-celebration.html">Take Me Out to the Ball Game</a>” (1908) <br/>
    2.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/05/billy-murray-charted-with-youre-grand.html">You’re a Grand Old Flag (aka “The Grand Old Rag”)</a>” (1906) <br/>
    3.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/10/haydn-quartet-charted-with-sweet.html">Sweet Adeline (You’re the Flower of My Heart)</a>” (1904) <br/>
    4.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/02/2251905-billy-murray-takes-yankee.html">Yankee Doodle Boy</a>” (1905) <br/>
    5.	Arthur Collins “<a href="http://davesmusicdatabase.blogspot.com/2014/07/arthur-collins-hit-1-with-bill-bailey.html">Bill Bailey
    Won’t You Please Come Home</a>” (1902) <br/>
    6.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/07/give-my-regards-to-broadway-goes-to-1.html">Give My Regards to Broadway</a>” (1905) <br/>
    7.	Harry MacDonough with Miss Walton “<a href="http://davesmusicdatabase.blogspot.com/2012/04/shine-on-harvest-moon-hit-1-april-10_10.html">Shine on Harvest Moon</a>” (1909) <br/>
    8.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/in-good-old-summertime-hit-1-for-second.html">In the Good Old Summertime</a>” (1903) <br/>
    9.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/07/7231904-billy-murray-hits-1-with-meet.html">Meet Me in St. Louis Louis</a>” (1904) <br/>
    10.	Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2012/05/byron-harlan-hit-1-with-school-days-may.html">School Days (When We Were a Couple of Kids)</a>” (1907) <br/>
    </p><p></p><center><!--&#8212;Video: Take Me Out to the Ball Game ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/HCH-7vyywpE" title="YouTube video player" type="text/html" width="500"></iframe></center><hr/><p>
    </p><center><a href="https://davesmusicdatabase.blogspot.com/2018/07/pre-1900s-top-100-songs.html" title="1890-1899: Top 100"><img border="0" height="75" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3tjxaSP39WULzEkzxIRxtRnzxa14sO8XOS2LOzdybW9x_il1fN_hhxKqSw-oxmnq5S4PjYWHQYWdBiov0oQ25MuACjTJprPxMltNbAo127Is5hJtPjctKvfP_Tv8FPHCw=s0-d"/></a></center><p>
    
    1.	George J. Gaskin “<a href="https://davesmusicdatabase.blogspot.com/1993/04/100-years-ago-george-j-gaskin-hit-1.html">After the Ball</a>” (1893) <br/>
    2.	Arthur Collins “<a href="https://davesmusicdatabase.blogspot.com/1999/04/100-years-ago-arthur-collins-hit-1-with.html">Hello Ma Baby</a>” (1899) <br/>
    3.	John Yorke Atlee “<a href="https://davesmusicdatabase.blogspot.com/1991/08/100-years-ago-listen-to-mocking-bird.html">Listen to the Mocking Bird (aka “The Mocking Bird”)</a>” (1891) <br/>
    4.	John Philip Sousa “The Stars and Stripes Forever” (1897) <br/>
    5.	Dan Quinn “A Hot Time in the Old Town” (1896) <br/>
    6.	Katherine Lee Bates &amp; Samuel A. Ward (songwriters) “America the Beautiful” (1895) <br/>
    7.	Len Spencer “Ta-Ra-Ra Boom-De-Ay” (1892) <br/>
    8.	Scott Joplin “Maple Leaf Rag” (1899) <br/>
    9.	Dan Quinn “Daisy Bell (A Bicycle Built for Two)” (1893) <br/>
    10.	George J. Gaskin “On the Banks of the Wabash” (1897) <br/>
    </p><p></p><center><!--&#8212;Video: After the Ball ----><iframe allowfullscreen="" class="youtube-player" frameborder="0" height="315" src="//www.youtube.com/embed/soxPknRyH-k" title="YouTube video player" type="text/html" width="500"></iframe></center><p>
    </p><hr/><b><h3>Resources/Related Links:</h3></b><ul>
    <li>Dave’s Music Database: “<a href="&lt;a href=" http:="">Best-of Lists</a>”
    </li><li>Dave’s Music Database: “<a href="https://davesmusicdatabase.blogspot.com/p/best-of-lists.html#songs-era">Best-of Song Lists by Era</a>”
    </li></ul>
    <p></p><hr/><i>First posted 4/9/2012; last updated 8/5/2022.</i><p></p></td></tr></table>
    <div style="clear: both;"></div>
    </div>
    <div class="post-footer">
    <div class="post-footer-line post-footer-line-1">
    <span class="post-author vcard">
    </span>
    <span class="post-timestamp">
    at
    <meta content="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html" itemprop="url"/>
    <a class="timestamp-link" href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html" rel="bookmark" title="permanent link"><abbr class="published" itemprop="datePublished" title="2022-08-05T15:38:00-05:00">August 05, 2022</abbr></a>
    </span>
    <span class="post-comment-link">
    </span>
    <span class="post-icons">
    <span class="item-action">
    <a href="https://www.blogger.com/email-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996" title="Email Post">
    <img alt="" class="icon-action" height="13" src="https://resources.blogblog.com/img/icon18_email.gif" width="18"/>
    </a>
    </span>
    <span class="item-control blog-admin pid-912096853">
    <a href="https://www.blogger.com/post-edit.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;from=pencil" title="Edit Post">
    <img alt="" class="icon-action" height="18" src="https://resources.blogblog.com/img/icon18_edit_allbkg.gif" width="18"/>
    </a>
    </span>
    </span>
    <div class="post-share-buttons goog-inline-block">
    <a class="goog-inline-block share-button sb-email" href="https://www.blogger.com/share-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;target=email" target="_blank" title="Email This"><span class="share-button-link-text">Email This</span></a><a class="goog-inline-block share-button sb-blog" href="https://www.blogger.com/share-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;target=blog" onclick='window.open(this.href, "_blank", "height=270,width=475"); return false;' target="_blank" title="BlogThis!"><span class="share-button-link-text">BlogThis!</span></a><a class="goog-inline-block share-button sb-twitter" href="https://www.blogger.com/share-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;target=twitter" target="_blank" title="Share to Twitter"><span class="share-button-link-text">Share to Twitter</span></a><a class="goog-inline-block share-button sb-facebook" href="https://www.blogger.com/share-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;target=facebook" onclick='window.open(this.href, "_blank", "height=430,width=640"); return false;' target="_blank" title="Share to Facebook"><span class="share-button-link-text">Share to Facebook</span></a><a class="goog-inline-block share-button sb-pinterest" href="https://www.blogger.com/share-post.g?blogID=1443292966174170672&amp;postID=6640189637110144996&amp;target=pinterest" target="_blank" title="Share to Pinterest"><span class="share-button-link-text">Share to Pinterest</span></a>
    </div>
    </div>
    <div class="post-footer-line post-footer-line-2">
    <span class="post-labels">
    Labels:
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1890s" rel="tag">1890s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1900s" rel="tag">1900s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1910s" rel="tag">1910s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1920s" rel="tag">1920s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1930s" rel="tag">1930s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1940s" rel="tag">1940s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1950s" rel="tag">1950s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1960s" rel="tag">1960s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1970s" rel="tag">1970s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1980s" rel="tag">1980s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/1990s" rel="tag">1990s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/2000s" rel="tag">2000s</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/best%20songs%20by%20decade" rel="tag">best songs by decade</a>,
    <a href="https://davesmusicdatabase.blogspot.com/search/label/top%20songs" rel="tag">top songs</a>
    </span>
    </div>
    <div class="post-footer-line post-footer-line-3">
    <span class="post-location">
    </span>
    </div>
    </div>
    </div>
    <div class="comments" id="comments">
    <a name="comments"></a>
    <h4>12 comments:</h4>
    <div class="comments-content">
    <script async="async" src="" type="text/javascript"></script>
    <script type="text/javascript">
        (function() {
          var items = null;
          var msgs = null;
          var config = {};
    
    // <![CDATA[
          var cursor = null;
          if (items && items.length > 0) {
            cursor = parseInt(items[items.length - 1].timestamp) + 1;
          }
    
          var bodyFromEntry = function(entry) {
            var text = (entry &&
                        ((entry.content && entry.content.$t) ||
                         (entry.summary && entry.summary.$t))) ||
                '';
            if (entry && entry.gd$extendedProperty) {
              for (var k in entry.gd$extendedProperty) {
                if (entry.gd$extendedProperty[k].name == 'blogger.contentRemoved') {
                  return '<span class="deleted-comment">' + text + '</span>';
                }
              }
            }
            return text;
          }
    
          var parse = function(data) {
            cursor = null;
            var comments = [];
            if (data && data.feed && data.feed.entry) {
              for (var i = 0, entry; entry = data.feed.entry[i]; i++) {
                var comment = {};
                // comment ID, parsed out of the original id format
                var id = /blog-(\d+).post-(\d+)/.exec(entry.id.$t);
                comment.id = id ? id[2] : null;
                comment.body = bodyFromEntry(entry);
                comment.timestamp = Date.parse(entry.published.$t) + '';
                if (entry.author && entry.author.constructor === Array) {
                  var auth = entry.author[0];
                  if (auth) {
                    comment.author = {
                      name: (auth.name ? auth.name.$t : undefined),
                      profileUrl: (auth.uri ? auth.uri.$t : undefined),
                      avatarUrl: (auth.gd$image ? auth.gd$image.src : undefined)
                    };
                  }
                }
                if (entry.link) {
                  if (entry.link[2]) {
                    comment.link = comment.permalink = entry.link[2].href;
                  }
                  if (entry.link[3]) {
                    var pid = /.*comments\/default\/(\d+)\?.*/.exec(entry.link[3].href);
                    if (pid && pid[1]) {
                      comment.parentId = pid[1];
                    }
                  }
                }
                comment.deleteclass = 'item-control blog-admin';
                if (entry.gd$extendedProperty) {
                  for (var k in entry.gd$extendedProperty) {
                    if (entry.gd$extendedProperty[k].name == 'blogger.itemClass') {
                      comment.deleteclass += ' ' + entry.gd$extendedProperty[k].value;
                    } else if (entry.gd$extendedProperty[k].name == 'blogger.displayTime') {
                      comment.displayTime = entry.gd$extendedProperty[k].value;
                    }
                  }
                }
                comments.push(comment);
              }
            }
            return comments;
          };
    
          var paginator = function(callback) {
            if (hasMore()) {
              var url = config.feed + '?alt=json&v=2&orderby=published&reverse=false&max-results=50';
              if (cursor) {
                url += '&published-min=' + new Date(cursor).toISOString();
              }
              window.bloggercomments = function(data) {
                var parsed = parse(data);
                cursor = parsed.length < 50 ? null
                    : parseInt(parsed[parsed.length - 1].timestamp) + 1
                callback(parsed);
                window.bloggercomments = null;
              }
              url += '&callback=bloggercomments';
              var script = document.createElement('script');
              script.type = 'text/javascript';
              script.src = url;
              document.getElementsByTagName('head')[0].appendChild(script);
            }
          };
          var hasMore = function() {
            return !!cursor;
          };
          var getMeta = function(key, comment) {
            if ('iswriter' == key) {
              var matches = !!comment.author
                  && comment.author.name == config.authorName
                  && comment.author.profileUrl == config.authorUrl;
              return matches ? 'true' : '';
            } else if ('deletelink' == key) {
              return config.baseUri + '/delete-comment.g?blogID='
                   + config.blogId + '&postID=' + comment.id;
            } else if ('deleteclass' == key) {
              return comment.deleteclass;
            }
            return '';
          };
    
          var replybox = null;
          var replyUrlParts = null;
          var replyParent = undefined;
    
          var onReply = function(commentId, domId) {
            if (replybox == null) {
              // lazily cache replybox, and adjust to suit this style:
              replybox = document.getElementById('comment-editor');
              if (replybox != null) {
                replybox.height = '250px';
                replybox.style.display = 'block';
                replyUrlParts = replybox.src.split('#');
              }
            }
            if (replybox && (commentId !== replyParent)) {
              replybox.src = '';
              document.getElementById(domId).insertBefore(replybox, null);
              replybox.src = replyUrlParts[0]
                  + (commentId ? '&parentID=' + commentId : '')
                  + '#' + replyUrlParts[1];
              replyParent = commentId;
            }
          };
    
          var hash = (window.location.hash || '#').substring(1);
          var startThread, targetComment;
          if (/^comment-form_/.test(hash)) {
            startThread = hash.substring('comment-form_'.length);
          } else if (/^c[0-9]+$/.test(hash)) {
            targetComment = hash.substring(1);
          }
    
          // Configure commenting API:
          var configJso = {
            'maxDepth': config.maxThreadDepth
          };
          var provider = {
            'id': config.postId,
            'data': items,
            'loadNext': paginator,
            'hasMore': hasMore,
            'getMeta': getMeta,
            'onReply': onReply,
            'rendered': true,
            'initComment': targetComment,
            'initReplyThread': startThread,
            'config': configJso,
            'messages': msgs
          };
    
          var render = function() {
            if (window.goog && window.goog.comments) {
              var holder = document.getElementById('comment-holder');
              window.goog.comments.render(holder, provider);
            }
          };
    
          // render now, or queue to render when library loads:
          if (window.goog && window.goog.comments) {
            render();
          } else {
            window.goog = window.goog || {};
            window.goog.comments = window.goog.comments || {};
            window.goog.comments.loadQueue = window.goog.comments.loadQueue || [];
            window.goog.comments.loadQueue.push(render);
          }
        })();
    // ]]>
      </script>
    <div id="comment-holder">
    <div class="comment-thread toplevel-thread"><ol id="top-ra"><li class="comment" id="c5177765368903808290"><div class="avatar-image-container"><img alt="" src="//resources.blogblog.com/img/blank.gif"/></div><div class="comment-block"><div class="comment-header"><cite class="user">Pat Conolly</cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1436773189444#c5177765368903808290" rel="nofollow">July 13, 2015 at 2:39 AM</a></span></div><p class="comment-content">Dave should fix this. He has "I Heard It Through the Grapevine" twice - once by Marvin Gaye in 1968, which is correct, and once by the Beach Boys in 1966, which is wrong. I'm pretty sure the Beach Boys song was intended to be "Good Vibrations".</p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="5177765368903808290" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-1806161938"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=5177765368903808290" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread" id="c5177765368903808290-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c5177765368903808290-ra"><div><li class="comment" id="c3226175790437345962"><div class="avatar-image-container"><img alt="" src="//4.bp.blogspot.com/-iqwocxPPAnc/YEvjQ2RnvGI/AAAAAAAAC9g/JC_9aVBVdxI-htwyY_-JlijvoRDVcgt3ACK4BGAYYCw/s35/dave_foto.jpg"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/00469458199584765423" rel="nofollow">Dave Whitaker</a></cite><span class="icon user blog-author"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1436805652684#c3226175790437345962" rel="nofollow">July 13, 2015 at 11:40 AM</a></span></div><p class="comment-content">Thanks for the catch, Pat. It has been corrected.</p><span class="comment-actions secondary-text"><span class="item-control blog-admin blog-admin pid-912096853"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=3226175790437345962" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c3226175790437345962-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c3226175790437345962-ra"><div></div><div class="continue" id="c3226175790437345962-continue"><a class="comment-reply" data-comment-id="3226175790437345962" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c3226175790437345962-ce"></div></li></div><div class="continue" id="c5177765368903808290-continue"><a class="comment-reply" data-comment-id="5177765368903808290" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c5177765368903808290-ce"></div></li><li class="comment" id="c3343963119458474503"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/17862269622394944965" rel="nofollow">Unknown</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1514984870869#c3343963119458474503" rel="nofollow">January 3, 2018 at 7:07 AM</a></span></div><p class="comment-content">I love all of them. Incredible list. Thanks for sharing with us. "My Blue Heaven" is my all-time favorite song. I still know that I used to dance on this track like crazy. Here is a website which has huge collection of such 90's Era songs. <a href="http://www.tubemp3.audio/" rel="nofollow">Visit Here</a></p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="3343963119458474503" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-1986696752"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=3343963119458474503" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c3343963119458474503-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c3343963119458474503-ra"><div></div><div class="continue" id="c3343963119458474503-continue"><a class="comment-reply" data-comment-id="3343963119458474503" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c3343963119458474503-ce"></div></li><li class="comment" id="c920870995884200349"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/14290683659429491946" rel="nofollow">Alvex</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1545075247183#c920870995884200349" rel="nofollow">December 17, 2018 at 1:34 PM</a></span></div><p class="comment-content">Great list of songs from each decade, I really love some of the older ones. <br/>Just one question, how come "Charleston" isn't with list of 1920s hits?<br/>Other than that, very good list of some of the best music from the times</p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="920870995884200349" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-872233413"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=920870995884200349" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread" id="c920870995884200349-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c920870995884200349-ra"><div><li class="comment" id="c470303456286539908"><div class="avatar-image-container"><img alt="" src="//4.bp.blogspot.com/-iqwocxPPAnc/YEvjQ2RnvGI/AAAAAAAAC9g/JC_9aVBVdxI-htwyY_-JlijvoRDVcgt3ACK4BGAYYCw/s35/dave_foto.jpg"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/00469458199584765423" rel="nofollow">Dave Whitaker</a></cite><span class="icon user blog-author"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1554014665369#c470303456286539908" rel="nofollow">March 31, 2019 at 1:44 AM</a></span></div><p class="comment-content">Thanks for the feedback. "Charleston" doesn't make the top 10, but it is on the list of the best songs of the 1920s. You can see the full list here: http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1920-1929.html</p><span class="comment-actions secondary-text"><span class="item-control blog-admin blog-admin pid-912096853"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=470303456286539908" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c470303456286539908-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c470303456286539908-ra"><div></div><div class="continue" id="c470303456286539908-continue"><a class="comment-reply" data-comment-id="470303456286539908" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c470303456286539908-ce"></div></li></div><div class="continue" id="c920870995884200349-continue"><a class="comment-reply" data-comment-id="920870995884200349" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c920870995884200349-ce"></div></li><li class="comment" id="c570117095976815695"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/08094444433094383986" rel="nofollow">Unknown</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1558515393052#c570117095976815695" rel="nofollow">May 22, 2019 at 3:56 AM</a></span></div><p class="comment-content">Hi trying to find song sung in australian schools late 1920 or early 1930 called buttercups and daisies. Anyone able to help identify </p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="570117095976815695" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-1682926206"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=570117095976815695" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread" id="c570117095976815695-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c570117095976815695-ra"><div><li class="comment" id="c852471172299894298"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/01211818806024300226" rel="nofollow">Unknown</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1630478002542#c852471172299894298" rel="nofollow">September 1, 2021 at 1:33 AM</a></span></div><p class="comment-content">Do you mean the old folk song Rolling on the Grass - that has the line in it "Rolling on the grass amongst the buttercups and daisies" in the chorus? If so, it's by Michael Kilgarriff, who wrote popular folk songs from the late 1800s to around 1920.</p><span class="comment-actions secondary-text"><span class="item-control blog-admin blog-admin pid-216385188"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=852471172299894298" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c852471172299894298-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c852471172299894298-ra"><div></div><div class="continue" id="c852471172299894298-continue"><a class="comment-reply" data-comment-id="852471172299894298" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c852471172299894298-ce"></div></li></div><div class="continue" id="c570117095976815695-continue"><a class="comment-reply" data-comment-id="570117095976815695" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c570117095976815695-ce"></div></li><li class="comment" id="c2371340618086233597"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/06464289489222293095" rel="nofollow">anonymous responder</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1595861165183#c2371340618086233597" rel="nofollow">July 27, 2020 at 9:46 AM</a></span></div><p class="comment-content">LOVE this site, btw. You really should be commended! Dana Graybeal</p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="2371340618086233597" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-628442011"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=2371340618086233597" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c2371340618086233597-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c2371340618086233597-ra"><div></div><div class="continue" id="c2371340618086233597-continue"><a class="comment-reply" data-comment-id="2371340618086233597" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c2371340618086233597-ce"></div></li><li class="comment" id="c5123435003892481849"><div class="avatar-image-container"><img alt="" src="//resources.blogblog.com/img/blank.gif"/></div><div class="comment-block"><div class="comment-header"><cite class="user">Anonymous</cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1612848664219#c5123435003892481849" rel="nofollow">February 8, 2021 at 11:31 PM</a></span></div><p class="comment-content">Great song collection </p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="5123435003892481849" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-1806161938"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=5123435003892481849" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c5123435003892481849-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c5123435003892481849-ra"><div></div><div class="continue" id="c5123435003892481849-continue"><a class="comment-reply" data-comment-id="5123435003892481849" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c5123435003892481849-ce"></div></li><li class="comment" id="c3168841864392246310"><div class="avatar-image-container"><img alt="" src="//www.blogger.com/img/blogger_logo_round_35.png"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/13965963880488886158" rel="nofollow">Unknown</a></cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1647189680071#c3168841864392246310" rel="nofollow">March 13, 2022 at 11:41 AM</a></span></div><p class="comment-content">What information was used to create lists for 1890s, 1900s and 1910s<br/><br/></p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="3168841864392246310" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-62489318"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=3168841864392246310" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread" id="c3168841864392246310-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c3168841864392246310-ra"><div><li class="comment" id="c1505998580966289101"><div class="avatar-image-container"><img alt="" src="//4.bp.blogspot.com/-iqwocxPPAnc/YEvjQ2RnvGI/AAAAAAAAC9g/JC_9aVBVdxI-htwyY_-JlijvoRDVcgt3ACK4BGAYYCw/s35/dave_foto.jpg"/></div><div class="comment-block"><div class="comment-header"><cite class="user"><a href="https://www.blogger.com/profile/00469458199584765423" rel="nofollow">Dave Whitaker</a></cite><span class="icon user blog-author"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1647373238767#c1505998580966289101" rel="nofollow">March 15, 2022 at 2:40 PM</a></span></div><p class="comment-content">Appearances on best-of lists, chart peaks, and sales all factor in.</p><span class="comment-actions secondary-text"><span class="item-control blog-admin blog-admin pid-912096853"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=1505998580966289101" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c1505998580966289101-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c1505998580966289101-ra"><div></div><div class="continue" id="c1505998580966289101-continue"><a class="comment-reply" data-comment-id="1505998580966289101" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c1505998580966289101-ce"></div></li></div><div class="continue" id="c3168841864392246310-continue"><a class="comment-reply" data-comment-id="3168841864392246310" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c3168841864392246310-ce"></div></li><li class="comment" id="c7864417769661132431"><div class="avatar-image-container"><img alt="" src="//resources.blogblog.com/img/blank.gif"/></div><div class="comment-block"><div class="comment-header"><cite class="user">Anonymous</cite><span class="icon user"></span><span class="datetime secondary-text"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html?showComment=1665767913185#c7864417769661132431" rel="nofollow">October 14, 2022 at 12:18 PM</a></span></div><p class="comment-content">It would be interesting to see a similar page to this but for Albums and Musical Acts</p><span class="comment-actions secondary-text"><a class="comment-reply" data-comment-id="7864417769661132431" target="_self">Reply</a><span class="item-control blog-admin blog-admin pid-1806161938"><a href="https://www.blogger.com/delete-comment.g?blogID=1443292966174170672&amp;postID=7864417769661132431" target="_self">Delete</a></span></span></div><div class="comment-replies"><div class="comment-thread inline-thread hidden" id="c7864417769661132431-rt"><span class="thread-toggle thread-expanded"><span class="thread-arrow"></span><span class="thread-count"><a target="_self">Replies</a></span></span><ol class="thread-chrome thread-expanded" id="c7864417769661132431-ra"><div></div><div class="continue" id="c7864417769661132431-continue"><a class="comment-reply" data-comment-id="7864417769661132431" target="_self">Reply</a></div></ol></div></div><div class="comment-replybox-single" id="c7864417769661132431-ce"></div></li></ol><div class="continue" id="top-continue"><a class="comment-reply" target="_self">Add comment</a></div><div class="comment-replybox-thread" id="top-ce"></div><div class="loadmore hidden" data-post-id="6640189637110144996"><a target="_self">Load more...</a></div></div>
    </div>
    </div>
    <p class="comment-footer">
    </p><div class="comment-form">
    <a name="comment-form"></a>
    <p>
    </p>
    <a href="https://www.blogger.com/comment/frame/1443292966174170672?po=6640189637110144996&amp;hl=en" id="comment-editor-src"></a>
    <iframe allowtransparency="true" class="blogger-iframe-colorize blogger-comment-from-post" frameborder="0" height="410px" id="comment-editor" name="comment-editor" src="" width="100%"></iframe>
    <script src="https://www.blogger.com/static/v1/jsbin/3469866930-comment_from_post_iframe.js" type="text/javascript"></script>
    <script type="text/javascript">
          BLOG_CMT_createIframe('https://www.blogger.com/rpc_relay.html');
        </script>
    </div>
    <div id="backlinks-container">
    <div id="Blog1_backlinks-container">
    </div>
    </div>
    </div>
    </div>
    </div></div>
    </div>
    <div class="blog-pager" id="blog-pager">
    <span id="blog-pager-newer-link">
    <a class="blog-pager-newer-link" href="https://davesmusicdatabase.blogspot.com/2011/07/daves-faves-my-personal-top-100-songs.html" id="Blog1_blog-pager-newer-link" title="Newer Post">Newer Post</a>
    </span>
    <span id="blog-pager-older-link">
    <a class="blog-pager-older-link" href="https://davesmusicdatabase.blogspot.com/2022/07/beyonce-top-50-songs.html" id="Blog1_blog-pager-older-link" title="Older Post">Older Post</a>
    </span>
    <a class="home-link" href="https://davesmusicdatabase.blogspot.com/">Home</a>
    </div>
    <div class="clear"></div>
    <div class="post-feeds">
    <div class="feed-links">
    Subscribe to:
    <a class="feed-link" href="https://davesmusicdatabase.blogspot.com/feeds/6640189637110144996/comments/default" target="_blank" type="application/atom+xml">Post Comments (Atom)</a>
    </div>
    </div>
    </div></div>
    </div>
    </div>
    <div class="column-left-outer">
    <div class="column-left-inner">
    <aside>
    </aside>
    </div>
    </div>
    <div class="column-right-outer">
    <div class="column-right-inner">
    <aside>
    <div class="sidebar section" id="sidebar-right-1"><div class="widget BlogSearch" data-version="1" id="BlogSearch1">
    <h2 class="title">Search This Blog</h2>
    <div class="widget-content">
    <div id="BlogSearch1_form">
    <form action="https://davesmusicdatabase.blogspot.com/search" class="gsc-search-box" target="_top">
    <table cellpadding="0" cellspacing="0" class="gsc-search-box">
    <tbody>
    <tr>
    <td class="gsc-input">
    <input autocomplete="off" class="gsc-input" name="q" size="10" title="search" type="text" value=""/>
    </td>
    <td class="gsc-search-button">
    <input class="gsc-search-button" title="search" type="submit" value="Search"/>
    </td>
    </tr>
    </tbody>
    </table>
    </form>
    </div>
    </div>
    <div class="clear"></div>
    </div><div class="widget Profile" data-version="1" id="Profile1">
    <h2>About Me</h2>
    <div class="widget-content">
    <a href="https://www.blogger.com/profile/00469458199584765423"><img alt="My photo" class="profile-img" height="80" src="//2.bp.blogspot.com/-YCMJ63Dadjs/XJ8YPrhurfI/AAAAAAAAAPY/n1Tj4PABovMT65s5QFP-9GKAW7mv-s39wCK4BGAYYCw/s80/dave_foto.jpg" width="80"/></a>
    <dl class="profile-datablock">
    <dt class="profile-data">
    <a class="profile-name-link g-profile" href="https://www.blogger.com/profile/00469458199584765423" rel="author" style="background-image: url(//www.blogger.com/img/logo-16.png);">
    Dave Whitaker
    </a>
    </dt>
    </dl>
    <a class="profile-link" href="https://www.blogger.com/profile/00469458199584765423" rel="author">View my complete profile</a>
    <div class="clear"></div>
    </div>
    </div><div class="widget BlogArchive" data-version="1" id="BlogArchive1">
    <h2>Blog Archive</h2>
    <div class="widget-content">
    <div id="ArchiveList">
    <div id="BlogArchive1_ArchiveList">
    <ul class="hierarchy">
    <li class="archivedate expanded">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy toggle-open">
    
            ▼ 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/">
    2022
    </a>
    <span class="post-count" dir="ltr">(144)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/12/">
    Dec 2022
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/11/">
    Nov 2022
    </a>
    <span class="post-count" dir="ltr">(17)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/10/">
    Oct 2022
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/09/">
    Sep 2022
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate expanded">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy toggle-open">
    
            ▼ 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/08/">
    Aug 2022
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    <ul class="posts">
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/08/a-ha-top-50-songs.html">A-ha: Top 50 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/08/simple-minds-top-50-songs.html">Simple Minds: Top 50 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/08/top-50-nu-metal-songs.html">Top 50 Nu-Metal Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2020/08/mtv-video-of-year-awards-1984-2020.html">MTV Video of the Year Awards, 1984-2022</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/07/eminem-top-50-songs.html">Eminem: Top 50 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/08/olivia-newton-john-her-top-50-songs-in.html">Olivia Newton-John: Her Top 50 Songs in Celebratio...</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2012/03/madonnas-top-50-songs.html">Madonna: Top 100 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2009/09/sept-18-2009-madonna-released-career.html">Madonna: A Retrospective, 1982-2022</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2022/08/steve-sullivan-personal-top-100-songs.html">Steve Sullivan: Personal Top 100 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2011/07/daves-faves-my-personal-top-100-songs.html">Dave’s Faves: My Top 100 Songs</a></li>
    <li><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html">The Top Songs by Decade, 1890-2019</a></li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/07/">
    Jul 2022
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/06/">
    Jun 2022
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/05/">
    May 2022
    </a>
    <span class="post-count" dir="ltr">(17)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/04/">
    Apr 2022
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/03/">
    Mar 2022
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/02/">
    Feb 2022
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2022/01/">
    Jan 2022
    </a>
    <span class="post-count" dir="ltr">(21)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/">
    2021
    </a>
    <span class="post-count" dir="ltr">(169)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/12/">
    Dec 2021
    </a>
    <span class="post-count" dir="ltr">(25)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/11/">
    Nov 2021
    </a>
    <span class="post-count" dir="ltr">(18)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/10/">
    Oct 2021
    </a>
    <span class="post-count" dir="ltr">(15)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/09/">
    Sep 2021
    </a>
    <span class="post-count" dir="ltr">(22)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/08/">
    Aug 2021
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/07/">
    Jul 2021
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/06/">
    Jun 2021
    </a>
    <span class="post-count" dir="ltr">(17)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/05/">
    May 2021
    </a>
    <span class="post-count" dir="ltr">(23)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/04/">
    Apr 2021
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/03/">
    Mar 2021
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/02/">
    Feb 2021
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2021/01/">
    Jan 2021
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/">
    2020
    </a>
    <span class="post-count" dir="ltr">(93)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/12/">
    Dec 2020
    </a>
    <span class="post-count" dir="ltr">(14)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/11/">
    Nov 2020
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/10/">
    Oct 2020
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/09/">
    Sep 2020
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/08/">
    Aug 2020
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/07/">
    Jul 2020
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/06/">
    Jun 2020
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/05/">
    May 2020
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/04/">
    Apr 2020
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/03/">
    Mar 2020
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/02/">
    Feb 2020
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2020/01/">
    Jan 2020
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/">
    2019
    </a>
    <span class="post-count" dir="ltr">(94)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/12/">
    Dec 2019
    </a>
    <span class="post-count" dir="ltr">(18)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/11/">
    Nov 2019
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/10/">
    Oct 2019
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/09/">
    Sep 2019
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/08/">
    Aug 2019
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/07/">
    Jul 2019
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/06/">
    Jun 2019
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/05/">
    May 2019
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/04/">
    Apr 2019
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/03/">
    Mar 2019
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/02/">
    Feb 2019
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2019/01/">
    Jan 2019
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/">
    2018
    </a>
    <span class="post-count" dir="ltr">(85)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/12/">
    Dec 2018
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/11/">
    Nov 2018
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/10/">
    Oct 2018
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/09/">
    Sep 2018
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/08/">
    Aug 2018
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/07/">
    Jul 2018
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/06/">
    Jun 2018
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/05/">
    May 2018
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/04/">
    Apr 2018
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/03/">
    Mar 2018
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/02/">
    Feb 2018
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2018/01/">
    Jan 2018
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/">
    2017
    </a>
    <span class="post-count" dir="ltr">(95)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/12/">
    Dec 2017
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/11/">
    Nov 2017
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/10/">
    Oct 2017
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/09/">
    Sep 2017
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/08/">
    Aug 2017
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/07/">
    Jul 2017
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/06/">
    Jun 2017
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/05/">
    May 2017
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/04/">
    Apr 2017
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/03/">
    Mar 2017
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/02/">
    Feb 2017
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2017/01/">
    Jan 2017
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/">
    2016
    </a>
    <span class="post-count" dir="ltr">(63)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/12/">
    Dec 2016
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/11/">
    Nov 2016
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/10/">
    Oct 2016
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/09/">
    Sep 2016
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/08/">
    Aug 2016
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/07/">
    Jul 2016
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/06/">
    Jun 2016
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/05/">
    May 2016
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/04/">
    Apr 2016
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/03/">
    Mar 2016
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/02/">
    Feb 2016
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2016/01/">
    Jan 2016
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/">
    2015
    </a>
    <span class="post-count" dir="ltr">(64)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/12/">
    Dec 2015
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/11/">
    Nov 2015
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/10/">
    Oct 2015
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/09/">
    Sep 2015
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/08/">
    Aug 2015
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/07/">
    Jul 2015
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/06/">
    Jun 2015
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/05/">
    May 2015
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/04/">
    Apr 2015
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/03/">
    Mar 2015
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/02/">
    Feb 2015
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2015/01/">
    Jan 2015
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/">
    2014
    </a>
    <span class="post-count" dir="ltr">(63)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/12/">
    Dec 2014
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/11/">
    Nov 2014
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/10/">
    Oct 2014
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/09/">
    Sep 2014
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/08/">
    Aug 2014
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/07/">
    Jul 2014
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/06/">
    Jun 2014
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/05/">
    May 2014
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/04/">
    Apr 2014
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/03/">
    Mar 2014
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/02/">
    Feb 2014
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2014/01/">
    Jan 2014
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/">
    2013
    </a>
    <span class="post-count" dir="ltr">(79)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/12/">
    Dec 2013
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/11/">
    Nov 2013
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/10/">
    Oct 2013
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/09/">
    Sep 2013
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/08/">
    Aug 2013
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/07/">
    Jul 2013
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/06/">
    Jun 2013
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/05/">
    May 2013
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/04/">
    Apr 2013
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/03/">
    Mar 2013
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/02/">
    Feb 2013
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2013/01/">
    Jan 2013
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/">
    2012
    </a>
    <span class="post-count" dir="ltr">(126)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/12/">
    Dec 2012
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/11/">
    Nov 2012
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/10/">
    Oct 2012
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/09/">
    Sep 2012
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/08/">
    Aug 2012
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/07/">
    Jul 2012
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/06/">
    Jun 2012
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/05/">
    May 2012
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/04/">
    Apr 2012
    </a>
    <span class="post-count" dir="ltr">(14)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/03/">
    Mar 2012
    </a>
    <span class="post-count" dir="ltr">(11)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/02/">
    Feb 2012
    </a>
    <span class="post-count" dir="ltr">(14)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2012/01/">
    Jan 2012
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/">
    2011
    </a>
    <span class="post-count" dir="ltr">(103)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/12/">
    Dec 2011
    </a>
    <span class="post-count" dir="ltr">(15)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/11/">
    Nov 2011
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/10/">
    Oct 2011
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/09/">
    Sep 2011
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/08/">
    Aug 2011
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/07/">
    Jul 2011
    </a>
    <span class="post-count" dir="ltr">(13)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/06/">
    Jun 2011
    </a>
    <span class="post-count" dir="ltr">(14)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/05/">
    May 2011
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/04/">
    Apr 2011
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/03/">
    Mar 2011
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/02/">
    Feb 2011
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2011/01/">
    Jan 2011
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/">
    2010
    </a>
    <span class="post-count" dir="ltr">(65)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/12/">
    Dec 2010
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/11/">
    Nov 2010
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/10/">
    Oct 2010
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/09/">
    Sep 2010
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/08/">
    Aug 2010
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/07/">
    Jul 2010
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/06/">
    Jun 2010
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/05/">
    May 2010
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/04/">
    Apr 2010
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/02/">
    Feb 2010
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2010/01/">
    Jan 2010
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/">
    2009
    </a>
    <span class="post-count" dir="ltr">(57)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/12/">
    Dec 2009
    </a>
    <span class="post-count" dir="ltr">(12)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/11/">
    Nov 2009
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/10/">
    Oct 2009
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/09/">
    Sep 2009
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/08/">
    Aug 2009
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/07/">
    Jul 2009
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/06/">
    Jun 2009
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/05/">
    May 2009
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/04/">
    Apr 2009
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/02/">
    Feb 2009
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2009/01/">
    Jan 2009
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/">
    2008
    </a>
    <span class="post-count" dir="ltr">(38)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/12/">
    Dec 2008
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/11/">
    Nov 2008
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/10/">
    Oct 2008
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/09/">
    Sep 2008
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/08/">
    Aug 2008
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/07/">
    Jul 2008
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/06/">
    Jun 2008
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/05/">
    May 2008
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/04/">
    Apr 2008
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/02/">
    Feb 2008
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2008/01/">
    Jan 2008
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/">
    2007
    </a>
    <span class="post-count" dir="ltr">(44)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/12/">
    Dec 2007
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/11/">
    Nov 2007
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/10/">
    Oct 2007
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/09/">
    Sep 2007
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/08/">
    Aug 2007
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/07/">
    Jul 2007
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/06/">
    Jun 2007
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/05/">
    May 2007
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/04/">
    Apr 2007
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/03/">
    Mar 2007
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2007/02/">
    Feb 2007
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/">
    2006
    </a>
    <span class="post-count" dir="ltr">(45)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/12/">
    Dec 2006
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/11/">
    Nov 2006
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/10/">
    Oct 2006
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/09/">
    Sep 2006
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/08/">
    Aug 2006
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/07/">
    Jul 2006
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/06/">
    Jun 2006
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/05/">
    May 2006
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/04/">
    Apr 2006
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/03/">
    Mar 2006
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/02/">
    Feb 2006
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2006/01/">
    Jan 2006
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/">
    2005
    </a>
    <span class="post-count" dir="ltr">(31)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/11/">
    Nov 2005
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/10/">
    Oct 2005
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/09/">
    Sep 2005
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/08/">
    Aug 2005
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/07/">
    Jul 2005
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/06/">
    Jun 2005
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/05/">
    May 2005
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/04/">
    Apr 2005
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/03/">
    Mar 2005
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2005/02/">
    Feb 2005
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/">
    2004
    </a>
    <span class="post-count" dir="ltr">(45)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/12/">
    Dec 2004
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/11/">
    Nov 2004
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/10/">
    Oct 2004
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/09/">
    Sep 2004
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/08/">
    Aug 2004
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/07/">
    Jul 2004
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/06/">
    Jun 2004
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/05/">
    May 2004
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/04/">
    Apr 2004
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/03/">
    Mar 2004
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/02/">
    Feb 2004
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2004/01/">
    Jan 2004
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/">
    2003
    </a>
    <span class="post-count" dir="ltr">(34)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/12/">
    Dec 2003
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/11/">
    Nov 2003
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/10/">
    Oct 2003
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/09/">
    Sep 2003
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/08/">
    Aug 2003
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/07/">
    Jul 2003
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/06/">
    Jun 2003
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/05/">
    May 2003
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/04/">
    Apr 2003
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/03/">
    Mar 2003
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/02/">
    Feb 2003
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2003/01/">
    Jan 2003
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/">
    2002
    </a>
    <span class="post-count" dir="ltr">(37)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/12/">
    Dec 2002
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/11/">
    Nov 2002
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/10/">
    Oct 2002
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/09/">
    Sep 2002
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/08/">
    Aug 2002
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/07/">
    Jul 2002
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/06/">
    Jun 2002
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/05/">
    May 2002
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/04/">
    Apr 2002
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/03/">
    Mar 2002
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/02/">
    Feb 2002
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2002/01/">
    Jan 2002
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/">
    2001
    </a>
    <span class="post-count" dir="ltr">(35)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/12/">
    Dec 2001
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/11/">
    Nov 2001
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/10/">
    Oct 2001
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/09/">
    Sep 2001
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/08/">
    Aug 2001
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/07/">
    Jul 2001
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/06/">
    Jun 2001
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/05/">
    May 2001
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/04/">
    Apr 2001
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/03/">
    Mar 2001
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/02/">
    Feb 2001
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2001/01/">
    Jan 2001
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/">
    2000
    </a>
    <span class="post-count" dir="ltr">(40)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/12/">
    Dec 2000
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/11/">
    Nov 2000
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/10/">
    Oct 2000
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/09/">
    Sep 2000
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/08/">
    Aug 2000
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/07/">
    Jul 2000
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/06/">
    Jun 2000
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/05/">
    May 2000
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/04/">
    Apr 2000
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/03/">
    Mar 2000
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/02/">
    Feb 2000
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/2000/01/">
    Jan 2000
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/">
    1999
    </a>
    <span class="post-count" dir="ltr">(35)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/12/">
    Dec 1999
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/10/">
    Oct 1999
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/09/">
    Sep 1999
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/08/">
    Aug 1999
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/07/">
    Jul 1999
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/06/">
    Jun 1999
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/05/">
    May 1999
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/04/">
    Apr 1999
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/03/">
    Mar 1999
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/02/">
    Feb 1999
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1999/01/">
    Jan 1999
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/">
    1998
    </a>
    <span class="post-count" dir="ltr">(24)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/12/">
    Dec 1998
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/11/">
    Nov 1998
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/10/">
    Oct 1998
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/09/">
    Sep 1998
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/08/">
    Aug 1998
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/06/">
    Jun 1998
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/05/">
    May 1998
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/03/">
    Mar 1998
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/02/">
    Feb 1998
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1998/01/">
    Jan 1998
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/">
    1997
    </a>
    <span class="post-count" dir="ltr">(29)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/12/">
    Dec 1997
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/11/">
    Nov 1997
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/09/">
    Sep 1997
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/08/">
    Aug 1997
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/06/">
    Jun 1997
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/05/">
    May 1997
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/04/">
    Apr 1997
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/03/">
    Mar 1997
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1997/02/">
    Feb 1997
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/">
    1996
    </a>
    <span class="post-count" dir="ltr">(26)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/12/">
    Dec 1996
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/11/">
    Nov 1996
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/10/">
    Oct 1996
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/09/">
    Sep 1996
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/07/">
    Jul 1996
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/06/">
    Jun 1996
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/05/">
    May 1996
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/03/">
    Mar 1996
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/02/">
    Feb 1996
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1996/01/">
    Jan 1996
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/">
    1995
    </a>
    <span class="post-count" dir="ltr">(35)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/12/">
    Dec 1995
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/11/">
    Nov 1995
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/10/">
    Oct 1995
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/09/">
    Sep 1995
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/08/">
    Aug 1995
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/07/">
    Jul 1995
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/06/">
    Jun 1995
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/05/">
    May 1995
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/04/">
    Apr 1995
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/03/">
    Mar 1995
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/02/">
    Feb 1995
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1995/01/">
    Jan 1995
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/">
    1994
    </a>
    <span class="post-count" dir="ltr">(26)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/11/">
    Nov 1994
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/09/">
    Sep 1994
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/08/">
    Aug 1994
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/07/">
    Jul 1994
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/05/">
    May 1994
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/04/">
    Apr 1994
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/03/">
    Mar 1994
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/02/">
    Feb 1994
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1994/01/">
    Jan 1994
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/">
    1993
    </a>
    <span class="post-count" dir="ltr">(28)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/12/">
    Dec 1993
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/11/">
    Nov 1993
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/10/">
    Oct 1993
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/09/">
    Sep 1993
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/08/">
    Aug 1993
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/06/">
    Jun 1993
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/05/">
    May 1993
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/04/">
    Apr 1993
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/03/">
    Mar 1993
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/02/">
    Feb 1993
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1993/01/">
    Jan 1993
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/">
    1992
    </a>
    <span class="post-count" dir="ltr">(30)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/12/">
    Dec 1992
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/11/">
    Nov 1992
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/10/">
    Oct 1992
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/09/">
    Sep 1992
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/08/">
    Aug 1992
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/06/">
    Jun 1992
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/05/">
    May 1992
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/03/">
    Mar 1992
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/02/">
    Feb 1992
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1992/01/">
    Jan 1992
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/">
    1991
    </a>
    <span class="post-count" dir="ltr">(44)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/12/">
    Dec 1991
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/11/">
    Nov 1991
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/10/">
    Oct 1991
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/09/">
    Sep 1991
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/08/">
    Aug 1991
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/07/">
    Jul 1991
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/06/">
    Jun 1991
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/05/">
    May 1991
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/04/">
    Apr 1991
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/03/">
    Mar 1991
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/02/">
    Feb 1991
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1991/01/">
    Jan 1991
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/">
    1990
    </a>
    <span class="post-count" dir="ltr">(34)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/12/">
    Dec 1990
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/11/">
    Nov 1990
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/10/">
    Oct 1990
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/08/">
    Aug 1990
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/07/">
    Jul 1990
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/06/">
    Jun 1990
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/05/">
    May 1990
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/04/">
    Apr 1990
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/03/">
    Mar 1990
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/02/">
    Feb 1990
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1990/01/">
    Jan 1990
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/">
    1989
    </a>
    <span class="post-count" dir="ltr">(53)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/12/">
    Dec 1989
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/11/">
    Nov 1989
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/10/">
    Oct 1989
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/09/">
    Sep 1989
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/08/">
    Aug 1989
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/07/">
    Jul 1989
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/06/">
    Jun 1989
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/05/">
    May 1989
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/04/">
    Apr 1989
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/03/">
    Mar 1989
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/02/">
    Feb 1989
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1989/01/">
    Jan 1989
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/">
    1988
    </a>
    <span class="post-count" dir="ltr">(37)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/12/">
    Dec 1988
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/11/">
    Nov 1988
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/10/">
    Oct 1988
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/09/">
    Sep 1988
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/08/">
    Aug 1988
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/07/">
    Jul 1988
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/06/">
    Jun 1988
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/05/">
    May 1988
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/04/">
    Apr 1988
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/02/">
    Feb 1988
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1988/01/">
    Jan 1988
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/">
    1987
    </a>
    <span class="post-count" dir="ltr">(52)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/12/">
    Dec 1987
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/11/">
    Nov 1987
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/10/">
    Oct 1987
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/09/">
    Sep 1987
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/08/">
    Aug 1987
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/07/">
    Jul 1987
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/06/">
    Jun 1987
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/05/">
    May 1987
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/04/">
    Apr 1987
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/03/">
    Mar 1987
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/02/">
    Feb 1987
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1987/01/">
    Jan 1987
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/">
    1986
    </a>
    <span class="post-count" dir="ltr">(54)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/12/">
    Dec 1986
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/11/">
    Nov 1986
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/10/">
    Oct 1986
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/09/">
    Sep 1986
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/08/">
    Aug 1986
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/07/">
    Jul 1986
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/06/">
    Jun 1986
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/05/">
    May 1986
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/04/">
    Apr 1986
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/03/">
    Mar 1986
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/02/">
    Feb 1986
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1986/01/">
    Jan 1986
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/">
    1985
    </a>
    <span class="post-count" dir="ltr">(51)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/12/">
    Dec 1985
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/11/">
    Nov 1985
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/10/">
    Oct 1985
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/09/">
    Sep 1985
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/08/">
    Aug 1985
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/07/">
    Jul 1985
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/06/">
    Jun 1985
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/05/">
    May 1985
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/04/">
    Apr 1985
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/03/">
    Mar 1985
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/02/">
    Feb 1985
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1985/01/">
    Jan 1985
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/">
    1984
    </a>
    <span class="post-count" dir="ltr">(55)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/12/">
    Dec 1984
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/11/">
    Nov 1984
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/10/">
    Oct 1984
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/09/">
    Sep 1984
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/08/">
    Aug 1984
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/07/">
    Jul 1984
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/06/">
    Jun 1984
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/05/">
    May 1984
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/04/">
    Apr 1984
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/03/">
    Mar 1984
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/02/">
    Feb 1984
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1984/01/">
    Jan 1984
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/">
    1983
    </a>
    <span class="post-count" dir="ltr">(65)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/12/">
    Dec 1983
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/11/">
    Nov 1983
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/10/">
    Oct 1983
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/09/">
    Sep 1983
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/08/">
    Aug 1983
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/07/">
    Jul 1983
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/06/">
    Jun 1983
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/05/">
    May 1983
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/04/">
    Apr 1983
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/03/">
    Mar 1983
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/02/">
    Feb 1983
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1983/01/">
    Jan 1983
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/">
    1982
    </a>
    <span class="post-count" dir="ltr">(57)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/12/">
    Dec 1982
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/11/">
    Nov 1982
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/10/">
    Oct 1982
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/09/">
    Sep 1982
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/08/">
    Aug 1982
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/07/">
    Jul 1982
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/06/">
    Jun 1982
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/05/">
    May 1982
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/04/">
    Apr 1982
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/03/">
    Mar 1982
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/02/">
    Feb 1982
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1982/01/">
    Jan 1982
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/">
    1981
    </a>
    <span class="post-count" dir="ltr">(44)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/12/">
    Dec 1981
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/11/">
    Nov 1981
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/10/">
    Oct 1981
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/09/">
    Sep 1981
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/08/">
    Aug 1981
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/07/">
    Jul 1981
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/06/">
    Jun 1981
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/05/">
    May 1981
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/04/">
    Apr 1981
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/03/">
    Mar 1981
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/02/">
    Feb 1981
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1981/01/">
    Jan 1981
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/">
    1980
    </a>
    <span class="post-count" dir="ltr">(60)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/12/">
    Dec 1980
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/11/">
    Nov 1980
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/10/">
    Oct 1980
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/09/">
    Sep 1980
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/08/">
    Aug 1980
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/07/">
    Jul 1980
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/06/">
    Jun 1980
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/05/">
    May 1980
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/04/">
    Apr 1980
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/03/">
    Mar 1980
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/02/">
    Feb 1980
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1980/01/">
    Jan 1980
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/">
    1979
    </a>
    <span class="post-count" dir="ltr">(55)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/12/">
    Dec 1979
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/11/">
    Nov 1979
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/10/">
    Oct 1979
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/09/">
    Sep 1979
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/08/">
    Aug 1979
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/07/">
    Jul 1979
    </a>
    <span class="post-count" dir="ltr">(8)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/05/">
    May 1979
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/04/">
    Apr 1979
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/03/">
    Mar 1979
    </a>
    <span class="post-count" dir="ltr">(7)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1979/02/">
    Feb 1979
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/">
    1978
    </a>
    <span class="post-count" dir="ltr">(45)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/12/">
    Dec 1978
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/11/">
    Nov 1978
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/10/">
    Oct 1978
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/09/">
    Sep 1978
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/08/">
    Aug 1978
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/07/">
    Jul 1978
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/06/">
    Jun 1978
    </a>
    <span class="post-count" dir="ltr">(10)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/05/">
    May 1978
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/04/">
    Apr 1978
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/03/">
    Mar 1978
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/02/">
    Feb 1978
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1978/01/">
    Jan 1978
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/">
    1977
    </a>
    <span class="post-count" dir="ltr">(35)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/12/">
    Dec 1977
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/11/">
    Nov 1977
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/10/">
    Oct 1977
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/09/">
    Sep 1977
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/07/">
    Jul 1977
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/06/">
    Jun 1977
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/05/">
    May 1977
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/04/">
    Apr 1977
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/03/">
    Mar 1977
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/02/">
    Feb 1977
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1977/01/">
    Jan 1977
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/">
    1976
    </a>
    <span class="post-count" dir="ltr">(31)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/12/">
    Dec 1976
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/11/">
    Nov 1976
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/10/">
    Oct 1976
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/09/">
    Sep 1976
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/08/">
    Aug 1976
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/07/">
    Jul 1976
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/06/">
    Jun 1976
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/05/">
    May 1976
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/04/">
    Apr 1976
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/03/">
    Mar 1976
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/02/">
    Feb 1976
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1976/01/">
    Jan 1976
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/">
    1975
    </a>
    <span class="post-count" dir="ltr">(31)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/12/">
    Dec 1975
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/11/">
    Nov 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/10/">
    Oct 1975
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/09/">
    Sep 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/08/">
    Aug 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/07/">
    Jul 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/06/">
    Jun 1975
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/05/">
    May 1975
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/04/">
    Apr 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/03/">
    Mar 1975
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/02/">
    Feb 1975
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1975/01/">
    Jan 1975
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/">
    1974
    </a>
    <span class="post-count" dir="ltr">(28)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/12/">
    Dec 1974
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/11/">
    Nov 1974
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/10/">
    Oct 1974
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/09/">
    Sep 1974
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/08/">
    Aug 1974
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/07/">
    Jul 1974
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/06/">
    Jun 1974
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/05/">
    May 1974
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/04/">
    Apr 1974
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/03/">
    Mar 1974
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1974/02/">
    Feb 1974
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/">
    1973
    </a>
    <span class="post-count" dir="ltr">(35)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/12/">
    Dec 1973
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/11/">
    Nov 1973
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/10/">
    Oct 1973
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/09/">
    Sep 1973
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/08/">
    Aug 1973
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/07/">
    Jul 1973
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/06/">
    Jun 1973
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/05/">
    May 1973
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/04/">
    Apr 1973
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/03/">
    Mar 1973
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/02/">
    Feb 1973
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1973/01/">
    Jan 1973
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/">
    1972
    </a>
    <span class="post-count" dir="ltr">(28)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/12/">
    Dec 1972
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/11/">
    Nov 1972
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/10/">
    Oct 1972
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/09/">
    Sep 1972
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/07/">
    Jul 1972
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/06/">
    Jun 1972
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/05/">
    May 1972
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/04/">
    Apr 1972
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/03/">
    Mar 1972
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/02/">
    Feb 1972
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1972/01/">
    Jan 1972
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/">
    1971
    </a>
    <span class="post-count" dir="ltr">(31)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/12/">
    Dec 1971
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/11/">
    Nov 1971
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/10/">
    Oct 1971
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/09/">
    Sep 1971
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/08/">
    Aug 1971
    </a>
    <span class="post-count" dir="ltr">(1)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/07/">
    Jul 1971
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/06/">
    Jun 1971
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/05/">
    May 1971
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/04/">
    Apr 1971
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/03/">
    Mar 1971
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1971/01/">
    Jan 1971
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/">
    1970
    </a>
    <span class="post-count" dir="ltr">(40)</span>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/12/">
    Dec 1970
    </a>
    <span class="post-count" dir="ltr">(4)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/11/">
    Nov 1970
    </a>
    <span class="post-count" dir="ltr">(9)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/10/">
    Oct 1970
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/09/">
    Sep 1970
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/08/">
    Aug 1970
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/07/">
    Jul 1970
    </a>
    <span class="post-count" dir="ltr">(5)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/05/">
    May 1970
    </a>
    <span class="post-count" dir="ltr">(3)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/04/">
    Apr 1970
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/03/">
    Mar 1970
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/02/">
    Feb 1970
    </a>
    <span class="post-count" dir="ltr">(2)</span>
    </li>
    </ul>
    <ul class="hierarchy">
    <li class="archivedate collapsed">
    <a class="toggle" href="javascript:void(0)">
    <span class="zippy">
    
            ► 
          
    </span>
    </a>
    <a class="post-count-link" href="https://davesmusicdatabase.blogspot.com/1970/01/">
    Jan 1970
    </a>
    <span class="post-count" dir="ltr">(6)</span>
    </li>
    </ul>
    </li>
    </ul>
    </div>
    </div>
    <div class="clear"></div>
    </div>
    </div><div class="widget ReportAbuse" data-version="1" id="ReportAbuse1">
    <h3 class="title">
    <a class="report_abuse" href="https://www.blogger.com/go/report-abuse" rel="noopener nofollow" target="_blank">
    Report Abuse
    </a>
    </h3>
    </div><div class="widget PopularPosts" data-version="1" id="PopularPosts1">
    <h2>Popular Posts</h2>
    <div class="widget-content popular-posts">
    <ul>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2014/12/radios-most-played-songs-in-history.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2VnER2YlTgfQ4PVEyQPyPzJonrJoiOv805UUvaUDd99ys31C8gRgObYziyJi038T_ki0Ny0JOdcGIxBuM1ktUlu7y460YMZIdLLvul6BBPCqis8UoxqrlJ2quNRpdhLL8=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2014/12/radios-most-played-songs-in-history.html">Radio’s Most-Played Songs in History</a></div>
    <div class="item-snippet">    Radio’s Most-Played Songs in History:  Top 100+ Songs  These are, according to various sources (see bottom of page), the all-time most-p...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2pbei1RaGxhl1If9Jg5HEcK3w5QWdQHGE1Cen1PwnDoAHmZgYF3wMgUoJE6kWZ6jqR1hG9mlaISmJZL0wX_n_hhpJSvUvpC30OM6lKudowaFBFR-jSlTUBY1JkZ4BpwnVx1Ewil4ORdQEIIKSkQig=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html">The Top Songs by Decade, 1890-2019</a></div>
    <div class="item-snippet">  image from musiccanada.files.wordpress.com   Top Songs by Decade:  1890-2019  Dave’s Music Database has compiled the best songs of all-tim...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2011/12/top-100-r-songs-of-all-time.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3Z564VK_lfMxUsMm06Kv_wLFfvY7jNM06EY1zqPPCm7lDZVxnHvWjVzHHM1VAAZl-B0y1m2XSLIWUZvJVkFGmF-dgk7ZMrfbFDpOAMtDKlYcmXkKfFDDVGxU2pOCi8jqaouQ=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2011/12/top-100-r-songs-of-all-time.html">The Top 100 R&amp;B Songs of All Time</a></div>
    <div class="item-snippet">    R&amp;B:  Top 100 Songs  Like most DMDB lists, this was created by aggregrating multiple genre-specific lists. In this case, 33 R&amp;B-...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2013/08/billboard-hot-100-55th-anniversary-all.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3OwmcdhyT3fQOAFa080RrRI_goOrH8jta3SJ0PWLUnOJIJS0YYshVNW_LAw6ACTwLpMKnEYEhlcJdGimEgYI9WrhSd9IJRC5w9dYVg3kCjKZqaqUxVhALyEueXIeEHeK4fobgy=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2013/08/billboard-hot-100-55th-anniversary-all.html">Billboard Hot 100: The Top 300+ Songs, 1958-2021</a></div>
    <div class="item-snippet">     Billboard  Hot 100:  Top 300+ Songs, 1958-2021  In 2008, Billboard  published a list of the top 100 songs of all-time in celebration of...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2012/05/top-100-classic-rock-songs-of-all-time.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha1uAYXOnn7d1fAep38LHtzhj6_ruNgmH7pLZAIznHdU3ryQky7It_dyOGkSvliwyfynipcpNZ5yA2FEchIYxUsl4jf2-ZXw0SG_yP9Ol-5b2inwk16fxrqRp5gQa8tSkpWl5XrXHAY=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2012/05/top-100-classic-rock-songs-of-all-time.html">The Top 100 Classic Rock Songs, 1964-1981</a></div>
    <div class="item-snippet">    Classic Rock:  Top 100 Songs, 1964-1981  This originated as a post on Dave’s Music Database Facebook page  and was updated in April 2012...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2012/03/riaaneas-top-365-songs-of-20th-century.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha0FS2FKJPnyctYyFSUcE9J6T2zKGQBOxUDQ3viXDc1i-_t4oVKO4Zp2ZXO6OapxRrmm18zGCNU9S9yZMyt3ssB5o8wMz6O9Je0Hhfg8IaEr9EnlUf_TPMUeaLkgHptMDg=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2012/03/riaaneas-top-365-songs-of-20th-century.html">The RIAA/NEA's Songs of the Century</a></div>
    <div class="item-snippet">    RIAA/NEA:  Top 365 Songs of the 20th Century  Description here On March 7, 2001, The National Endowment for the Arts (NEA) and the Recor...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2014/08/top-100-songs-from-1980-to-1989.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha3a2e40S91MpUXPsA0agIEsoG1B76tgIUxs_G8CBgPXPvAEZSvblf3hTqVOvrud58Or7BwspfiYklNIuCvbl1e_V2OV_zCtP69AXjubozUj-JP0htMCh5zjHvAlFz92Sq8=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2014/08/top-100-songs-from-1980-to-1989.html">Top 100 Songs from 1980 to 1989</a></div>
    <div class="item-snippet">    Top 100 Songs of the Decade:  1980-1989  These are the top 100 songs from the 1980s according to Dave’s Music Database. Rankings are fig...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2021/04/big-band-top-100-songs.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2dqDZh-TcEW3mq9iD5PUZj2cUruD-qFXn-0NGvGFp4gBnZ-hA8VWyc2Gm8zmDQYafSyCpZ_8HRFk-lbz6Z_BZnheRRbydj5fooEQAOyOxvOEHpWZgJjxv388_UWySJhTRXLNQ=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2021/04/big-band-top-100-songs.html">Big Band: Top 100 Songs</a></div>
    <div class="item-snippet">    Big Band:  Top 100 Songs  Big Band, or Swing music, was especially popular in the 1930s and ‘40s. They were generally jazz-oriented orch...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1940-1949.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha0zix18hWYLj_MFlxW3y3sFvvltuDt5VDheA_I2so2SgyLZExno8UND845LasntV8nkQZpw0CKh7sKXI24a4pEpOMZMR70cmqtp7Sxu06Y_8pwuWryR0630aKzxnY2KNuU=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1940-1949.html">Top 100 Songs from 1940-1949</a></div>
    <div class="item-snippet">First posted 4/4/2012; last updated 10/26/2020.     Top 100 Songs of the Decade:  1940-1949  These are the top 100 songs from the 1940s acco...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    <li>
    <div class="item-content">
    <div class="item-thumbnail">
    <a href="https://davesmusicdatabase.blogspot.com/2011/08/top-100-country-songs-of-all-time.html" target="_blank">
    <img alt="" border="0" src="https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha1kzPQ_ZAfNZI2XF2GgcC_GHhpj2S85kis1OJyAT4CpM88hfOTPdCacNqg-whBRKl53yJ_cfi9bz7u0UNJbLnE31qbE8dszvJYJWPeghAX3Uze5fGQm6pEzmJVGAlxuNLFmxw=w72-h72-p-k-no-nu"/>
    </a>
    </div>
    <div class="item-title"><a href="https://davesmusicdatabase.blogspot.com/2011/08/top-100-country-songs-of-all-time.html">The Top 200 Country Songs of All Time</a></div>
    <div class="item-snippet">    Country Music:  Top 200 Songs  The DMDB’s list of the top 100 country songs of all time was created by aggregating 90 best-of lists focu...</div>
    </div>
    <div style="clear: both;"></div>
    </li>
    </ul>
    <div class="clear"></div>
    </div>
    </div><div class="widget HTML" data-version="1" id="HTML2">
    <h2 class="title">DMDB on Facebook</h2>
    <div class="widget-content">
    <div id="fb-root"></div>
    <script>(function(d, s, id) {
      var js, fjs = d.getElementsByTagName(s)[0];
      if (d.getElementById(id)) return;
      js = d.createElement(s); js.id = id;
      js.src = "//connect.facebook.net/en_US/all.js#xfbml=1&appId=117991284891372";
      fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'facebook-jssdk'));</script>
    <div class="fb-like-box" data-header="true" data-href="http://www.facebook.com/davesmusicdatabase" data-show-faces="true" data-stream="true" data-width="300"></div>
    </div>
    <div class="clear"></div>
    </div>
    </div>
    </aside>
    </div>
    </div>
    </div>
    <div style="clear: both"></div>
    <!-- columns -->
    </div>
    <!-- main -->
    </div>
    </div>
    <div class="main-cap-bottom cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    <footer>
    <div class="footer-outer">
    <div class="footer-cap-top cap-top">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    <div class="fauxborder-left footer-fauxborder-left">
    <div class="fauxborder-right footer-fauxborder-right"></div>
    <div class="region-inner footer-inner">
    <div class="foot no-items section" id="footer-1">
    </div>
    <table border="0" cellpadding="0" cellspacing="0" class="section-columns columns-2">
    <tbody>
    <tr>
    <td class="first columns-cell">
    <div class="foot no-items section" id="footer-2-1"></div>
    </td>
    <td class="columns-cell">
    <div class="foot no-items section" id="footer-2-2"></div>
    </td>
    </tr>
    </tbody>
    </table>
    <!-- outside of the include in order to lock Attribution widget -->
    <div class="foot section" id="footer-3" name="Footer"><div class="widget Attribution" data-version="1" id="Attribution1">
    <div class="widget-content" style="text-align: center;">
    2012. Dave's Music Database.. Simple theme. Powered by <a href="https://www.blogger.com" target="_blank">Blogger</a>.
    </div>
    <div class="clear"></div>
    </div></div>
    </div>
    </div>
    <div class="footer-cap-bottom cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    </footer>
    <!-- content -->
    </div>
    </div>
    <div class="content-cap-bottom cap-bottom">
    <div class="cap-left"></div>
    <div class="cap-right"></div>
    </div>
    </div>
    </div>
    <script type="text/javascript">
        window.setTimeout(function() {
            document.body.className = document.body.className.replace('loading', '');
          }, 10);
      </script>
    <script src="https://apis.google.com/js/platform.js" type="text/javascript"></script>
    <script src="https://www.blogger.com/static/v1/widgets/1197256859-widgets.js" type="text/javascript"></script>
    <script type="text/javascript">
    window['__wavt'] = 'AOuZoY7fBcS3QdIE6deI9veNLme7EDI-AQ:1671596202662';_WidgetManager._Init('//www.blogger.com/rearrange?blogID\x3d1443292966174170672','//davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html','1443292966174170672');
    _WidgetManager._SetDataContext([{'name': 'blog', 'data': {'blogId': '1443292966174170672', 'title': 'Dave\x27s Music Database', 'url': 'https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html', 'canonicalUrl': 'https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html', 'homepageUrl': 'https://davesmusicdatabase.blogspot.com/', 'searchUrl': 'https://davesmusicdatabase.blogspot.com/search', 'canonicalHomepageUrl': 'https://davesmusicdatabase.blogspot.com/', 'blogspotFaviconUrl': 'https://davesmusicdatabase.blogspot.com/favicon.ico', 'bloggerUrl': 'https://www.blogger.com', 'hasCustomDomain': false, 'httpsEnabled': true, 'enabledCommentProfileImages': true, 'gPlusViewType': 'FILTERED_POSTMOD', 'adultContent': false, 'analyticsAccountNumber': '', 'encoding': 'UTF-8', 'locale': 'en', 'localeUnderscoreDelimited': 'en', 'languageDirection': 'ltr', 'isPrivate': false, 'isMobile': false, 'isMobileRequest': false, 'mobileClass': '', 'isPrivateBlog': false, 'isDynamicViewsAvailable': true, 'feedLinks': '\x3clink rel\x3d\x22alternate\x22 type\x3d\x22application/atom+xml\x22 title\x3d\x22Dave\x26#39;s Music Database - Atom\x22 href\x3d\x22https://davesmusicdatabase.blogspot.com/feeds/posts/default\x22 /\x3e\n\x3clink rel\x3d\x22alternate\x22 type\x3d\x22application/rss+xml\x22 title\x3d\x22Dave\x26#39;s Music Database - RSS\x22 href\x3d\x22https://davesmusicdatabase.blogspot.com/feeds/posts/default?alt\x3drss\x22 /\x3e\n\x3clink rel\x3d\x22service.post\x22 type\x3d\x22application/atom+xml\x22 title\x3d\x22Dave\x26#39;s Music Database - Atom\x22 href\x3d\x22https://www.blogger.com/feeds/1443292966174170672/posts/default\x22 /\x3e\n\n\x3clink rel\x3d\x22alternate\x22 type\x3d\x22application/atom+xml\x22 title\x3d\x22Dave\x26#39;s Music Database - Atom\x22 href\x3d\x22https://davesmusicdatabase.blogspot.com/feeds/6640189637110144996/comments/default\x22 /\x3e\n', 'meTag': '', 'adsenseClientId': 'ca-pub-2683813143377667', 'adsenseHostId': 'ca-host-pub-1556223355139109', 'adsenseHasAds': false, 'adsenseAutoAds': false, 'boqCommentIframeForm': true, 'loginRedirectParam': '', 'view': '', 'dynamicViewsCommentsSrc': '//www.blogblog.com/dynamicviews/4224c15c4e7c9321/js/comments.js', 'dynamicViewsScriptSrc': '//www.blogblog.com/dynamicviews/ef92609af3888d71', 'plusOneApiSrc': 'https://apis.google.com/js/platform.js', 'disableGComments': true, 'sharing': {'platforms': [{'name': 'Get link', 'key': 'link', 'shareMessage': 'Get link', 'target': ''}, {'name': 'Facebook', 'key': 'facebook', 'shareMessage': 'Share to Facebook', 'target': 'facebook'}, {'name': 'BlogThis!', 'key': 'blogThis', 'shareMessage': 'BlogThis!', 'target': 'blog'}, {'name': 'Twitter', 'key': 'twitter', 'shareMessage': 'Share to Twitter', 'target': 'twitter'}, {'name': 'Pinterest', 'key': 'pinterest', 'shareMessage': 'Share to Pinterest', 'target': 'pinterest'}, {'name': 'Email', 'key': 'email', 'shareMessage': 'Email', 'target': 'email'}], 'disableGooglePlus': true, 'googlePlusShareButtonWidth': 0, 'googlePlusBootstrap': '\x3cscript type\x3d\x22text/javascript\x22\x3ewindow.___gcfg \x3d {\x27lang\x27: \x27en\x27};\x3c/script\x3e'}, 'hasCustomJumpLinkMessage': false, 'jumpLinkMessage': 'Read more', 'pageType': 'item', 'postId': '6640189637110144996', 'postImageThumbnailUrl': 'https://i.ytimg.com/vi/OPf0YbXqDm0/default.jpg', 'postImageUrl': 'https://musiccanada.files.wordpress.com/2017/06/decades.jpg?w\x3d350\x26h\x3d200\x26crop\x3d1', 'pageName': 'The Top Songs by Decade, 1890-2019', 'pageTitle': 'Dave\x27s Music Database: The Top Songs by Decade, 1890-2019'}}, {'name': 'features', 'data': {'sharing_get_link_dialog': 'true', 'sharing_native': 'false'}}, {'name': 'messages', 'data': {'edit': 'Edit', 'linkCopiedToClipboard': 'Link copied to clipboard!', 'ok': 'Ok', 'postLink': 'Post Link'}}, {'name': 'template', 'data': {'name': 'Simple', 'localizedName': 'Simple', 'isResponsive': false, 'isAlternateRendering': false, 'isCustom': false, 'variant': 'simplysimple', 'variantId': 'simplysimple'}}, {'name': 'view', 'data': {'classic': {'name': 'classic', 'url': '?view\x3dclassic'}, 'flipcard': {'name': 'flipcard', 'url': '?view\x3dflipcard'}, 'magazine': {'name': 'magazine', 'url': '?view\x3dmagazine'}, 'mosaic': {'name': 'mosaic', 'url': '?view\x3dmosaic'}, 'sidebar': {'name': 'sidebar', 'url': '?view\x3dsidebar'}, 'snapshot': {'name': 'snapshot', 'url': '?view\x3dsnapshot'}, 'timeslide': {'name': 'timeslide', 'url': '?view\x3dtimeslide'}, 'isMobile': false, 'title': 'The Top Songs by Decade, 1890-2019', 'description': '  image from musiccanada.files.wordpress.com   Top Songs by Decade:  1890-2019  Dave\u2019s Music Database has compiled the best songs of all-tim...', 'featuredImage': 'https://lh3.googleusercontent.com/blogger_img_proxy/ANbyha2pbei1RaGxhl1If9Jg5HEcK3w5QWdQHGE1Cen1PwnDoAHmZgYF3wMgUoJE6kWZ6jqR1hG9mlaISmJZL0wX_n_hhpJSvUvpC30OM6lKudowaFBFR-jSlTUBY1JkZ4BpwnVx1Ewil4ORdQEIIKSkQig', 'url': 'https://davesmusicdatabase.blogspot.com/2012/04/top-songs-by-decade-1900-present.html', 'type': 'item', 'isSingleItem': true, 'isMultipleItems': false, 'isError': false, 'isPage': false, 'isPost': true, 'isHomepage': false, 'isArchive': false, 'isLabelSearch': false, 'postId': 6640189637110144996}}]);
    _WidgetManager._RegisterWidget('_NavbarView', new _WidgetInfo('Navbar1', 'navbar', document.getElementById('Navbar1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_HeaderView', new _WidgetInfo('Header1', 'header', document.getElementById('Header1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_PageListView', new _WidgetInfo('PageList1', 'crosscol-overflow', document.getElementById('PageList1'), {'title': 'Pages', 'links': [{'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/about-daves-music-database.html', 'title': 'Home'}, {'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/best-of-lists.html', 'title': 'Best-of Lists'}, {'isCurrentPage': false, 'href': 'https://davesmusicdatabase.blogspot.com/p/podcast.html', 'id': '3913103639768989026', 'title': 'Podcast'}, {'isCurrentPage': false, 'href': 'http://www.facebook.com/davesmusicdatabase', 'title': 'Facebook'}, {'isCurrentPage': false, 'href': 'https://davesmusicdatabase.blogspot.com/p/hall-of-fame.html', 'id': '1396013403532718754', 'title': 'Hall of Fame'}, {'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/books.html', 'title': 'Books'}, {'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/aural-fixation.html', 'title': 'Aural Fixation'}, {'isCurrentPage': false, 'href': 'https://davesmusicdatabase.blogspot.com/p/the-all-time-music-makers-home-about.html', 'id': '6807805303859256841', 'title': 'DMDB Encyclopedia'}, {'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/birthdays.html', 'title': 'Birthdays'}, {'isCurrentPage': false, 'href': 'https://davesmusicdatabase.blogspot.com/p/concerts.html', 'id': '5535360846834119783', 'title': 'Concerts'}, {'isCurrentPage': false, 'href': 'http://davesmusicdatabase.blogspot.com/p/links.html', 'title': 'Links'}, {'isCurrentPage': false, 'href': 'https://davesmusicdatabase.blogspot.com/p/index.html', 'id': '1621308797869206759', 'title': 'Index'}], 'mobile': false}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_HTMLView', new _WidgetInfo('HTML1', 'crosscol-overflow', document.getElementById('HTML1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_BlogView', new _WidgetInfo('Blog1', 'main', document.getElementById('Blog1'), {'cmtInteractionsEnabled': false, 'lightboxEnabled': true, 'lightboxModuleUrl': 'https://www.blogger.com/static/v1/jsbin/1520561359-lbx.js', 'lightboxCssUrl': 'https://www.blogger.com/static/v1/v-css/4046960807-lightbox_bundle.css'}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_BlogSearchView', new _WidgetInfo('BlogSearch1', 'sidebar-right-1', document.getElementById('BlogSearch1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_ProfileView', new _WidgetInfo('Profile1', 'sidebar-right-1', document.getElementById('Profile1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_BlogArchiveView', new _WidgetInfo('BlogArchive1', 'sidebar-right-1', document.getElementById('BlogArchive1'), {'languageDirection': 'ltr', 'loadingMessage': 'Loading\x26hellip;'}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_ReportAbuseView', new _WidgetInfo('ReportAbuse1', 'sidebar-right-1', document.getElementById('ReportAbuse1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_PopularPostsView', new _WidgetInfo('PopularPosts1', 'sidebar-right-1', document.getElementById('PopularPosts1'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_HTMLView', new _WidgetInfo('HTML2', 'sidebar-right-1', document.getElementById('HTML2'), {}, 'displayModeFull'));
    _WidgetManager._RegisterWidget('_AttributionView', new _WidgetInfo('Attribution1', 'footer-3', document.getElementById('Attribution1'), {}, 'displayModeFull'));
    </script>
    </body>
    </html>




```python
soup.find('p')
soup.find('p').text
```




    'DavesMusicDatabase.com is devoted to ranking, rating, and reviewing music of all genres and eras. The DMDB blog serves up album and song reviews, best-of lists, music history snapshots, and music-related essays.'




```python
print(len(soup.find_all('p')))
soup.find_all('p')
```

    60





    [<p class="description"><span>DavesMusicDatabase.com is devoted to ranking, rating, and reviewing music of all genres and eras. The DMDB blog serves up album and song reviews, best-of lists, music history snapshots, and music-related essays.</span></p>,
     <p></p>,
     <p><font color="white"></font></p>,
     <p>
     Dave’s Music Database has compiled the best songs of all-time into a variety of lists over the years. Check out the full array of DMDB best-of lists <a href="http://davesmusicdatabase.blogspot.com/p/best-of-lists.html">here</a>. However, this page – which at 72,000+ hits is the second most visited on the DMDB blog – offers snapshots of the top 10 songs of each decade from 1890 to present. </p>,
     <p>
     <a href="https://davesmusicdatabase.blogspot.com/p/best-of-lists.html#songs-era">Click here to see ‘Top 100 Songs of the Decade’ lists</a> or click on the corresponding badges below. 
     
     </p>,
     <p>
     
     1.	Mark Ronson with Bruno Mars “<a href="http://davesmusicdatabase.blogspot.com/2015/04/april-18-2015-uptown-funk-lands-14th.html">Uptown Funk!</a>” (2014) <br/>
     2.	Ed Sheeran “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1282017-ed-sheeran-debuts-at-1-with.html">Shape of You</a>” (2017) <br/>
     3.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2011/12/2011-song-of-year-adeles-rolling-in.html">Rolling in the Deep</a>” (2010) <br/>
     4.	Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2014/03/pharrell-williams-hit-1-in-us-with-happy.html">Happy</a>” (2013) <br/>
     5.	Luis Fonsi with Daddy Yankee &amp; Justin Bieber “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1122017-despacito-is-released.html">Despacito</a>” (2017) <br/>
     6.	Gotye with Kimbra “<a href="http://www.davesmusicdatabase.blogspot.com/2013/01/gotye-charts-with-somebody-that-i-used.html">Somebody That I Used to Know</a>” (2011) <br/>
     7.	Robin Thicke with T.I. &amp; Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2013/03/robin-thickes-blurred-lines-released.html">Blurred Lines</a>” (2013)<br/>
     8.	Carly Rae Jepsen “<a href="http://davesmusicdatabase.blogspot.com/2011/09/september-20-2011-call-me-maybe-is.html">Call Me Maybe</a>” (2011) <br/>
     9.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2015/11/adeles-hello-debuts-at-1.html">Hello</a>” (2015) <br/>
     10.	Lil Nas X with Billy Ray Cyrus “<a href="https://davesmusicdatabase.blogspot.com/2019/07/old-town-road-lands-14th-week-at-1.html">Old Town Road</a>” (2018) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	OutKast “<a href="http://davesmusicdatabase.blogspot.com/2011/10/outkast-charted-with-song-of-decade-hey.html">Hey Ya!</a>” (2003) <br/>
     2.	Black Eyed Peas “<a href="http://davesmusicdatabase.blogspot.com/2011/07/black-eyed-peas-knock-themselves-from-1.html">I Gotta Feeling</a>” (2009) <br/>
     3.	Eminem “<a href="http://davesmusicdatabase.blogspot.com/2011/10/eminem-charts-with-lose-yourself.html">Lose Yourself</a>” (2002) <br/>
     4.	Usher with Lil’ Jon &amp; Ludacris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/usher-launches-his-first-of-28-weeks-at.html">Yeah!</a>” (2004) <br/>
     5.	Beyoncé with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2003/07/beyonce-hits-1-with-crazy-in-love-july.html">Crazy in Love</a>” (2003) <br/>
     6.	Gnarls Barkley “<a href="http://davesmusicdatabase.blogspot.com/2006/04/4292006-gnarls-barkley-charts-with-crazy.html">Crazy</a>” (2006) <br/>
     7.	Beyoncé “<a href="http://davesmusicdatabase.blogspot.com/2011/12/beyonce-hit-1-with-single-ladies.html">Single Ladies (Put a Ring on It)</a>” (2008) <br/>
     8.	Rihanna with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2007/06/rihanna-hit-1-with-umbrella-june-9-2007.html">Umbrella</a>” (2007) <br/>
     9.	Flo Rida with T-Pain “<a href="http://davesmusicdatabase.blogspot.com/2008/03/flo-ridas-low-spends-10th-week-at-1.html">Low</a>” (2007) <br/>
     10.	Mariah Carey “<a href="http://davesmusicdatabase.blogspot.com/2012/06/mariah-carey-hit-1-with-we-belong.html">We Belong Together</a>” (2005) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Whitney Houston “<a href="http://davesmusicdatabase.blogspot.com/2011/11/whitney-houston-hit-1-with-i-will.html">I Will Always Love You</a>” (1992) <br/>
     2.	Nirvana “<a href="http://davesmusicdatabase.blogspot.com/1991/09/nirvana-charted-with-smells-like-teen.html">Smells Like Teen Spirit</a>” (1991) <br/>
     3.	Bryan Adams “<a href="http://davesmusicdatabase.blogspot.com/2012/06/bryan-adams-charted-with-everything-i.html">(Everything I Do) I Do It for You</a>” (1991) <br/>
     4.	Sinéad O’Connor “<a href="http://davesmusicdatabase.blogspot.com/2013/01/sinead-oconnor-charted-with-nothing.html">Nothing Compares 2 U</a>” (1990) <br/>
     5.	Celine Dion “<a href="http://davesmusicdatabase.blogspot.com/1998/02/celine-dion-hit-1-with-my-heart-will-go.html">My Heart Will Go On</a>” (1997) <br/>
     6.	Elton John “<a href="http://davesmusicdatabase.blogspot.com/2011/09/elton-john-performs-candle-in-wind-at.html">Candle in the Wind 1997 (Goodbye England’s Rose)</a>” (1997) <br/>
     7.	R.E.M. “<a href="http://davesmusicdatabase.blogspot.com/1991/03/rem-charts-with-losing-my-religion.html">Losing My Religion</a>” (1991) <br/>
     8.	Oasis “<a href="http://davesmusicdatabase.blogspot.com/1995/11/oasis-chart-with-wonderwall.html">Wonderwall</a>” (1995) <br/>
     9.	Los Del Rio “<a href="https://davesmusicdatabase.blogspot.com/1996/11/macarena-spends-14th-week-on-top.html">Macarena (Bayside Boys Mix)</a>” (1995) <br/>
     10.	U2 “<a href="https://davesmusicdatabase.blogspot.com/1992/01/141992-u2-charted-with-one.html">One</a>” (1991) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/2013/01/michael-jackson-charted-with-billie.html">Billie Jean</a>” (1982) <br/>
     2.	The Police “<a href="http://davesmusicdatabase.blogspot.com/2012/07/police-hit-1-with-every-breath-you-take.html">Every Breath You Take</a>” (1983) <br/>
     3.	Guns N’ Roses “<a href="http://davesmusicdatabase.blogspot.com/2012/06/guns-n-roses-charted-with-sweet-child-o.html">Sweet Child O’ Mine</a>” (1987) <br/>
     4.	Prince “<a href="http://davesmusicdatabase.blogspot.com/2012/06/prince-charted-with-when-doves-cry-june.html">When Doves Cry</a>” (1984) <br/>
     5.	Joan Jett &amp; the Blackhearts “<a href="http://davesmusicdatabase.blogspot.com/1981/12/12121981-joan-jett-rocks-charts.html">I Love Rock and Roll</a>” (1981) <br/>
     6.	U2 “<a href="http://davesmusicdatabase.blogspot.com/1987/05/5161987-u2-hit-1-with-with-or-without.html">With or Without You</a>” (1987) <br/>
     7.	Bon Jovi “<a href="https://davesmusicdatabase.blogspot.com/1987/02/bon-jovi-hit-1-with-livin-on-prayer.html">Livin’ on a Prayer</a>” (1986) <br/>
     8.	Lionel Richie &amp; Diana Ross “<a href="http://davesmusicdatabase.blogspot.com/2012/07/lionel-richie-and-diana-ross-debuted.html">Endless Love</a>” (1981) <br/>
     9.	Van Halen “<a href="https://davesmusicdatabase.blogspot.com/1984/02/van-halen-hit-1-with-jump.html">Jump</a>” (1984) <br/>
     10.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/1983/04/beat-it-becomes-michael-jacksons-second.html">Beat It</a>” (1983) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Queen “<a href="http://davesmusicdatabase.blogspot.com/2011/11/queen-charted-with-bohemian-rhapsody.html">Bohemian Rhapsody</a>” (1975) <br/>
     2.	John Lennon “<a href="http://davesmusicdatabase.blogspot.com/1971/10/john-lennon-charted-with-imagine.html">Imagine</a>” (1971) <br/>
     3.	Bee Gees “<a href="http://davesmusicdatabase.blogspot.com/1978/02/bee-gees-hit-1-with-stayin-alive.html">Stayin’ Alive</a>” (1977) <br/>
     4.	Simon &amp; Garfunkel “<a href="http://davesmusicdatabase.blogspot.com/2012/02/simon-garfunkel-hit-1-with-bridge-over.html">Bridge Over Troubled Water</a>” (1970) <br/>
     5.	Eagles “<a href="http://davesmusicdatabase.blogspot.com/2012/05/eagles-hotel-california-hit-1-may-7.html">Hotel California</a>” (1976) <br/>
     6.	Led Zeppelin “<a href="http://davesmusicdatabase.blogspot.com/1971/11/led-zeppelins-stairway-to-heaven-was.html">Stairway to Heaven</a>” (1971) <br/>
     7.	Don McLean “<a href="http://davesmusicdatabase.blogspot.com/2012/01/don-mcleans-american-pie-hit-1-january.html">American Pie</a>” (1971) <br/>
     8.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/1970/04/the-beatles-hit-1-with-let-it-be-april.html">Let It Be</a>” (1970) <br/>
     9.	Stevie Wonder “<a href="http://davesmusicdatabase.blogspot.com/1972/11/11111972-stevie-wonder-charts-with.html">Superstition</a>” (1972) <br/>
     10.	Derek &amp; the Dominos “<a href="http://davesmusicdatabase.blogspot.com/2012/03/derek-and-dominos-charted-with-layla.html">Layla</a>” (1970) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	The Rolling Stones “<a href="http://davesmusicdatabase.blogspot.com/2015/07/50-years-ago-today-rolling-stones-hit-1.html">(I Can’t Get No) Satisfaction</a>” (1965) <br/>
     2.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2018/11/50-years-ago-today-hey-jude-spent-9th.html">Hey Jude</a>” (1968) <br/>
     3.	Marvin Gaye “<a href="http://davesmusicdatabase.blogspot.com/2011/11/marvin-gayes-i-heard-it-through.html">I Heard It Through the Grapevine</a>” (1968) <br/>
     4.	Aretha Franklin “<a href="http://davesmusicdatabase.blogspot.com/2012/06/aretha-franklin-hit-1-with-respect-june.html">Respect</a>” (1967) <br/>
     5.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2014/02/50-years-ago-today-beatles-hit-1-in-us.html">I Want to Hold Your Hand</a>” (1963) <br/>
     6.	The Beach Boys “<a href="http://davesmusicdatabase.blogspot.com/2011/10/beach-boys-charted-with-good-vibrations.html">Good Vibrations</a>” (1966) <br/>
     7.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/2013/10/the-beatles-hit-1-with-yesterday.html">Yesterday</a>” (1965) <br/>
     8.	Bob Dylan “<a href="http://davesmusicdatabase.blogspot.com/2011/07/bob-dylans-like-rolling-stone-debuts-on.html">Like a Rolling Stone</a>” (1965) <br/>
     9.	Otis Redding “<a href="http://davesmusicdatabase.blogspot.com/2014/01/otis-reddings-sittin-on-dock-of-bay-is.html">(Sittin’ on) The Dock of the Bay</a>” (1968) <br/>
     10.	The Animals “<a href="http://davesmusicdatabase.blogspot.com/2012/06/animals-charted-with-house-of-rising.html">The House of the Rising Sun</a>”(1964) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Bill Haley &amp; His Comets “<a href="http://davesmusicdatabase.blogspot.com/2010/07/happy-birthday-rock-and-roll-55-years.html">We’re Gonna Rock Around the Clock</a>” (1954) <br/>
     2.	Bobby Darin “<a href="http://davesmusicdatabase.blogspot.com/2011/08/bobby-darin-charts-with-mack-knife.html">Mack the Knife</a>” (1959) <br/>
     3.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2014/04/elvis-presley-hit-1-with-heartbreak.html">Heartbreak Hotel</a>” (1956) <br/>
     4.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2011/07/elvis-presley-performs-for-hound-dog.html">Hound Dog</a>” (1956) <br/>
     5.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2013/08/elvis-presley-hit-1-with-dont-be-cruel.html">Don’t Be Cruel</a>” (1956) <br/>
     6.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2007/09/fifty-years-ago-today-elvis-presley.html">Jailhouse Rock</a>” (1957) <br/>
     7.	Chuck Berry “<a href="http://davesmusicdatabase.blogspot.com/2014/04/chuck-berry-charted-with-johnny-b-goode.html">Johnny B. Goode</a>” (1958) <br/>
     8.	Patti Page “<a href="http://davesmusicdatabase.blogspot.com/2011/11/patti-page-charted-with-tennessee-waltz.html">Tennessee Waltz</a>” (1950) <br/>
     9.	Ray Charles “<a href="http://davesmusicdatabase.blogspot.com/2009/02/fifty-years-ago-today-ray-charles.html">What’d I Say</a>” (1959) <br/>
     10.	The Everly Brothers “<a href="http://davesmusicdatabase.blogspot.com/2008/06/fifty-years-ago-today-everly-brothers.html">All I Have to Do Is Dream</a>” (1958) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Bing Crosby with the Ken Darby Singers “<a href="http://davesmusicdatabase.blogspot.com/2011/10/bing-crosby-hit-1-with-white-christmas.html">White Christmas</a>” (1942) <br/> 
     2.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2012/01/artie-shaw-charted-with-star-dust.html">Stardust</a>” (1941) <br/> 
     3.	Gene Autry “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1231949-gene-autry-charts-with-rudolph.html">Rudolph, the Red-Nosed Reindeer</a>” (1949) <br/> 
     4.	Glenn Miller with Tex Beneke &amp; the Four Modernaires “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11291941-glenn-miller-hits-1-with.html">Chattanooga Choo Choo</a>” (1941) <br/> 
     5.	Les Brown with Doris Day “<a href="http://davesmusicdatabase.blogspot.com/2016/03/331945-les-brown-charts-with.html">Sentimental Journey</a>” (1945) <br/> 
     6.	Nat “King” Cole “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11231946-nat-king-cole-charted-with.html">The Christmas Song (Chestnuts Roasting on an Open Fire)</a>” (1946) <br/>
     7.	Tommy Dorsey with Frank Sinatra &amp; The Pied Pipers “<a href="http://davesmusicdatabase.blogspot.com/2011/07/frank-sinatra-hits-1-for-first-time_27.html">I’ll Never Smile Again</a>” (1940) <br/>
     8.	Cliff Edwards “<a href="http://davesmusicdatabase.blogspot.com/2013/02/cliff-edwards-charted-with-when-you.html">When You Wish Upon a Star</a>” (1940) <br/> 
     9.	Duke Ellington “<a href="http://davesmusicdatabase.blogspot.com/2011/07/duke-ellington-charts-with-take-a-train.html">Take the ‘A’ Train</a>” (1941) <br/> 
     10.	Dooley Wilson “<a href="http://davesmusicdatabase.blogspot.com/2014/11/as-time-goes-by-immortalized-by.html">As Time Goes By</a>” (1942) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Judy Garland “<a href="http://davesmusicdatabase.blogspot.com/2011/09/judy-garland-charts-with-over-rainbow.html">Over the Rainbow</a>” (1939) <br/>
     2.	Glenn Miller “<a href="http://davesmusicdatabase.blogspot.com/2011/10/glenn-miller-charts-with-in-mood.html">In the Mood</a>” (1939) <br/> 
     3.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2011/12/fred-astaire-hit-1-with-cole-porters.html">Night and Day</a>” (1932) <br/> 
     4.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2013/08/cheek-to-cheek-hits-1-for-first-of-11.html">Cheek to Cheek</a>” (1935) <br/> 
     5.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2013/11/artie-shaws-beguin-beguine-hit-1.html">Begin the Beguine</a>” (1938) <br/> 
     6.	Ethel Waters “<a href="http://davesmusicdatabase.blogspot.com/2014/05/ethel-waters-charted-with-stormy.html">Stormy Weather (Keeps Rainin' All the Time)</a>” (1933) <br/> 
     7.	Fred Astaire with Johnny Green “<a href="http://davesmusicdatabase.blogspot.com/2016/10/1031936-fred-astaire-hits-1-with-way.html">The Way You Look Tonight</a>” (1936) <br/> 
     8.	Bing Crosby with the Guardsmen Quartette “<a href="https://davesmusicdatabase.blogspot.com/1985/12/bing-crosby-charted-with-silent-night.html">Silent Night</a>” (1935) <br/> 
     9.	Ella Fitzgerald with Chick Webb “<a href="http://davesmusicdatabase.blogspot.com/2012/06/ella-fitzgerald-hit-1-with-tisket.html">A-Tisket, A-Tasket</a>” (1938) <br/>
     10.	Tommy Dorsey with Jack Leonard “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1271940-tommy-dorsey-lands-at-1-with.html">All the Things You Are</a>” (1939) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Bessie Smith with Louis Armstrong “<a href="http://davesmusicdatabase.blogspot.com/2011/11/wc-handy-charted-with-st-louis-blues.html">St. Louis Blues</a>” (1925) <br/>
     2.	Al Jolson “<a href="https://davesmusicdatabase.blogspot.com/2010/05/al-jolson-hit-1-with-swanee-90-years.html">Swanee</a>” (1920) <br/> 
     3.	Gene Austin “<a href="http://davesmusicdatabase.blogspot.com/2013/12/my-blue-heaven-hit-1-december-17-1927.html">My Blue Heaven</a>” (1927) <br/>
     4.	Thomas “Fats” Waller “<a href="http://davesmusicdatabase.blogspot.com/2016/11/1111929-fats-waller-releases-aint.html">Ain’t Misbehavin’</a>” (1929) <br/>
     5.	Paul Whiteman “<a href="http://davesmusicdatabase.blogspot.com/2011/10/paul-whitemans-whispering-hit-1-october.html">Whispering</a>” (1920) <br/>
     6.	Al Jolson "<a href="https://davesmusicdatabase.blogspot.com/2013/01/al-jolson-charted-with-april-showers.html">April Showers</a>” (1922) <br/>
     7.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1241925-marion-harris-charted-with-tea.html">Tea for Two</a>” (1925) <br/>
     8.	Vernon Dalhart “<a href="http://davesmusicdatabase.blogspot.com/2011/08/vernon-dalhart-records-prisoners-song.html">The Prisoner’s Song</a>” (1925) <br/>
     9.	Ben Selvin “<a href="http://davesmusicdatabase.blogspot.com/2013/01/ben-selvin-charted-with-dardanella.html">Dardanella</a>” (1920) <br/>
     10.	Isham Jones “<a href="http://davesmusicdatabase.blogspot.com/2016/09/961924-isham-jones-takes-it-had-to-be.html">It Had to Be You</a>” (1924) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Arthur Collins &amp; Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2011/09/alexanders-ragtime-band-hits-1.html">Alexander’s Ragtime Band</a>” (1911) <br/>
     2.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/09/american-quartets-over-there-charts.html">Over There</a>” (1917) <br/>
     3.	Peerless Quartet “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1221911-peerless-quartet-hit-1-for.html">Let Me Call You Sweetheart</a>” (1911) <br/>
     4.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2014/10/al-jolson-topped-charts-with-you-made.html">You Made Me Love You (I Didn't Want to Do It)</a>” (1913) <br/>
     5.	Billy Murray with the Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/04/by-light-of-silvery-moon-hit-1-april-23.html">By the Light of the Silvery Moon</a>” (1910) <br/>
     6.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/moonlight-bay-hit-1-march-16-1912.html">Moonlight Bay</a>” (1912) <br/>
     7.	Original Dixieland Jazz Band “<a href="http://davesmusicdatabase.blogspot.com/2014/08/tiger-rag-charts-for-first-time-august.html">Tiger Rag</a>” (1918) <br/>
     8.	Sophie Tucker “<a href="http://davesmusicdatabase.blogspot.com/2014/07/sophie-tucker-charted-with-some-of.html">Some of These Days</a>” (1911) <br/>
     9.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/marion-harris-hit-1-with-after-youve.html">After You’ve Gone</a>” (1919) <br/>
     10.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2016/12/8171918-rock-bye-your-baby-with-dixie.html">Rock-a-Bye Your Baby with a Dixie Melody</a>” (1918) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/07/take-me-out-to-ball-game-in-celebration.html">Take Me Out to the Ball Game</a>” (1908) <br/>
     2.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/05/billy-murray-charted-with-youre-grand.html">You’re a Grand Old Flag (aka “The Grand Old Rag”)</a>” (1906) <br/>
     3.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/10/haydn-quartet-charted-with-sweet.html">Sweet Adeline (You’re the Flower of My Heart)</a>” (1904) <br/>
     4.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/02/2251905-billy-murray-takes-yankee.html">Yankee Doodle Boy</a>” (1905) <br/>
     5.	Arthur Collins “<a href="http://davesmusicdatabase.blogspot.com/2014/07/arthur-collins-hit-1-with-bill-bailey.html">Bill Bailey
     Won’t You Please Come Home</a>” (1902) <br/>
     6.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/07/give-my-regards-to-broadway-goes-to-1.html">Give My Regards to Broadway</a>” (1905) <br/>
     7.	Harry MacDonough with Miss Walton “<a href="http://davesmusicdatabase.blogspot.com/2012/04/shine-on-harvest-moon-hit-1-april-10_10.html">Shine on Harvest Moon</a>” (1909) <br/>
     8.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/in-good-old-summertime-hit-1-for-second.html">In the Good Old Summertime</a>” (1903) <br/>
     9.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/07/7231904-billy-murray-hits-1-with-meet.html">Meet Me in St. Louis Louis</a>” (1904) <br/>
     10.	Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2012/05/byron-harlan-hit-1-with-school-days-may.html">School Days (When We Were a Couple of Kids)</a>” (1907) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p>
     
     1.	George J. Gaskin “<a href="https://davesmusicdatabase.blogspot.com/1993/04/100-years-ago-george-j-gaskin-hit-1.html">After the Ball</a>” (1893) <br/>
     2.	Arthur Collins “<a href="https://davesmusicdatabase.blogspot.com/1999/04/100-years-ago-arthur-collins-hit-1-with.html">Hello Ma Baby</a>” (1899) <br/>
     3.	John Yorke Atlee “<a href="https://davesmusicdatabase.blogspot.com/1991/08/100-years-ago-listen-to-mocking-bird.html">Listen to the Mocking Bird (aka “The Mocking Bird”)</a>” (1891) <br/>
     4.	John Philip Sousa “The Stars and Stripes Forever” (1897) <br/>
     5.	Dan Quinn “A Hot Time in the Old Town” (1896) <br/>
     6.	Katherine Lee Bates &amp; Samuel A. Ward (songwriters) “America the Beautiful” (1895) <br/>
     7.	Len Spencer “Ta-Ra-Ra Boom-De-Ay” (1892) <br/>
     8.	Scott Joplin “Maple Leaf Rag” (1899) <br/>
     9.	Dan Quinn “Daisy Bell (A Bicycle Built for Two)” (1893) <br/>
     10.	George J. Gaskin “On the Banks of the Wabash” (1897) <br/>
     </p>,
     <p></p>,
     <p>
     </p>,
     <p></p>,
     <p></p>,
     <p class="comment-content">Dave should fix this. He has "I Heard It Through the Grapevine" twice - once by Marvin Gaye in 1968, which is correct, and once by the Beach Boys in 1966, which is wrong. I'm pretty sure the Beach Boys song was intended to be "Good Vibrations".</p>,
     <p class="comment-content">Thanks for the catch, Pat. It has been corrected.</p>,
     <p class="comment-content">I love all of them. Incredible list. Thanks for sharing with us. "My Blue Heaven" is my all-time favorite song. I still know that I used to dance on this track like crazy. Here is a website which has huge collection of such 90's Era songs. <a href="http://www.tubemp3.audio/" rel="nofollow">Visit Here</a></p>,
     <p class="comment-content">Great list of songs from each decade, I really love some of the older ones. <br/>Just one question, how come "Charleston" isn't with list of 1920s hits?<br/>Other than that, very good list of some of the best music from the times</p>,
     <p class="comment-content">Thanks for the feedback. "Charleston" doesn't make the top 10, but it is on the list of the best songs of the 1920s. You can see the full list here: http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1920-1929.html</p>,
     <p class="comment-content">Hi trying to find song sung in australian schools late 1920 or early 1930 called buttercups and daisies. Anyone able to help identify </p>,
     <p class="comment-content">Do you mean the old folk song Rolling on the Grass - that has the line in it "Rolling on the grass amongst the buttercups and daisies" in the chorus? If so, it's by Michael Kilgarriff, who wrote popular folk songs from the late 1800s to around 1920.</p>,
     <p class="comment-content">LOVE this site, btw. You really should be commended! Dana Graybeal</p>,
     <p class="comment-content">Great song collection </p>,
     <p class="comment-content">What information was used to create lists for 1890s, 1900s and 1910s<br/><br/></p>,
     <p class="comment-content">Appearances on best-of lists, chart peaks, and sales all factor in.</p>,
     <p class="comment-content">It would be interesting to see a similar page to this but for Albums and Musical Acts</p>,
     <p class="comment-footer">
     </p>,
     <p>
     </p>]




```python
for p in soup.find_all('p',attrs=None): 
    print(p)
```

    <p class="description"><span>DavesMusicDatabase.com is devoted to ranking, rating, and reviewing music of all genres and eras. The DMDB blog serves up album and song reviews, best-of lists, music history snapshots, and music-related essays.</span></p>
    <p></p>
    <p><font color="white"></font></p>
    <p>
    Dave’s Music Database has compiled the best songs of all-time into a variety of lists over the years. Check out the full array of DMDB best-of lists <a href="http://davesmusicdatabase.blogspot.com/p/best-of-lists.html">here</a>. However, this page – which at 72,000+ hits is the second most visited on the DMDB blog – offers snapshots of the top 10 songs of each decade from 1890 to present. </p>
    <p>
    <a href="https://davesmusicdatabase.blogspot.com/p/best-of-lists.html#songs-era">Click here to see ‘Top 100 Songs of the Decade’ lists</a> or click on the corresponding badges below. 
    
    </p>
    <p>
    
    1.	Mark Ronson with Bruno Mars “<a href="http://davesmusicdatabase.blogspot.com/2015/04/april-18-2015-uptown-funk-lands-14th.html">Uptown Funk!</a>” (2014) <br/>
    2.	Ed Sheeran “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1282017-ed-sheeran-debuts-at-1-with.html">Shape of You</a>” (2017) <br/>
    3.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2011/12/2011-song-of-year-adeles-rolling-in.html">Rolling in the Deep</a>” (2010) <br/>
    4.	Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2014/03/pharrell-williams-hit-1-in-us-with-happy.html">Happy</a>” (2013) <br/>
    5.	Luis Fonsi with Daddy Yankee &amp; Justin Bieber “<a href="http://davesmusicdatabase.blogspot.com/2017/01/1122017-despacito-is-released.html">Despacito</a>” (2017) <br/>
    6.	Gotye with Kimbra “<a href="http://www.davesmusicdatabase.blogspot.com/2013/01/gotye-charts-with-somebody-that-i-used.html">Somebody That I Used to Know</a>” (2011) <br/>
    7.	Robin Thicke with T.I. &amp; Pharrell Williams “<a href="http://davesmusicdatabase.blogspot.com/2013/03/robin-thickes-blurred-lines-released.html">Blurred Lines</a>” (2013)<br/>
    8.	Carly Rae Jepsen “<a href="http://davesmusicdatabase.blogspot.com/2011/09/september-20-2011-call-me-maybe-is.html">Call Me Maybe</a>” (2011) <br/>
    9.	Adele “<a href="http://davesmusicdatabase.blogspot.com/2015/11/adeles-hello-debuts-at-1.html">Hello</a>” (2015) <br/>
    10.	Lil Nas X with Billy Ray Cyrus “<a href="https://davesmusicdatabase.blogspot.com/2019/07/old-town-road-lands-14th-week-at-1.html">Old Town Road</a>” (2018) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	OutKast “<a href="http://davesmusicdatabase.blogspot.com/2011/10/outkast-charted-with-song-of-decade-hey.html">Hey Ya!</a>” (2003) <br/>
    2.	Black Eyed Peas “<a href="http://davesmusicdatabase.blogspot.com/2011/07/black-eyed-peas-knock-themselves-from-1.html">I Gotta Feeling</a>” (2009) <br/>
    3.	Eminem “<a href="http://davesmusicdatabase.blogspot.com/2011/10/eminem-charts-with-lose-yourself.html">Lose Yourself</a>” (2002) <br/>
    4.	Usher with Lil’ Jon &amp; Ludacris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/usher-launches-his-first-of-28-weeks-at.html">Yeah!</a>” (2004) <br/>
    5.	Beyoncé with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2003/07/beyonce-hits-1-with-crazy-in-love-july.html">Crazy in Love</a>” (2003) <br/>
    6.	Gnarls Barkley “<a href="http://davesmusicdatabase.blogspot.com/2006/04/4292006-gnarls-barkley-charts-with-crazy.html">Crazy</a>” (2006) <br/>
    7.	Beyoncé “<a href="http://davesmusicdatabase.blogspot.com/2011/12/beyonce-hit-1-with-single-ladies.html">Single Ladies (Put a Ring on It)</a>” (2008) <br/>
    8.	Rihanna with Jay-Z “<a href="http://davesmusicdatabase.blogspot.com/2007/06/rihanna-hit-1-with-umbrella-june-9-2007.html">Umbrella</a>” (2007) <br/>
    9.	Flo Rida with T-Pain “<a href="http://davesmusicdatabase.blogspot.com/2008/03/flo-ridas-low-spends-10th-week-at-1.html">Low</a>” (2007) <br/>
    10.	Mariah Carey “<a href="http://davesmusicdatabase.blogspot.com/2012/06/mariah-carey-hit-1-with-we-belong.html">We Belong Together</a>” (2005) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Whitney Houston “<a href="http://davesmusicdatabase.blogspot.com/2011/11/whitney-houston-hit-1-with-i-will.html">I Will Always Love You</a>” (1992) <br/>
    2.	Nirvana “<a href="http://davesmusicdatabase.blogspot.com/1991/09/nirvana-charted-with-smells-like-teen.html">Smells Like Teen Spirit</a>” (1991) <br/>
    3.	Bryan Adams “<a href="http://davesmusicdatabase.blogspot.com/2012/06/bryan-adams-charted-with-everything-i.html">(Everything I Do) I Do It for You</a>” (1991) <br/>
    4.	Sinéad O’Connor “<a href="http://davesmusicdatabase.blogspot.com/2013/01/sinead-oconnor-charted-with-nothing.html">Nothing Compares 2 U</a>” (1990) <br/>
    5.	Celine Dion “<a href="http://davesmusicdatabase.blogspot.com/1998/02/celine-dion-hit-1-with-my-heart-will-go.html">My Heart Will Go On</a>” (1997) <br/>
    6.	Elton John “<a href="http://davesmusicdatabase.blogspot.com/2011/09/elton-john-performs-candle-in-wind-at.html">Candle in the Wind 1997 (Goodbye England’s Rose)</a>” (1997) <br/>
    7.	R.E.M. “<a href="http://davesmusicdatabase.blogspot.com/1991/03/rem-charts-with-losing-my-religion.html">Losing My Religion</a>” (1991) <br/>
    8.	Oasis “<a href="http://davesmusicdatabase.blogspot.com/1995/11/oasis-chart-with-wonderwall.html">Wonderwall</a>” (1995) <br/>
    9.	Los Del Rio “<a href="https://davesmusicdatabase.blogspot.com/1996/11/macarena-spends-14th-week-on-top.html">Macarena (Bayside Boys Mix)</a>” (1995) <br/>
    10.	U2 “<a href="https://davesmusicdatabase.blogspot.com/1992/01/141992-u2-charted-with-one.html">One</a>” (1991) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/2013/01/michael-jackson-charted-with-billie.html">Billie Jean</a>” (1982) <br/>
    2.	The Police “<a href="http://davesmusicdatabase.blogspot.com/2012/07/police-hit-1-with-every-breath-you-take.html">Every Breath You Take</a>” (1983) <br/>
    3.	Guns N’ Roses “<a href="http://davesmusicdatabase.blogspot.com/2012/06/guns-n-roses-charted-with-sweet-child-o.html">Sweet Child O’ Mine</a>” (1987) <br/>
    4.	Prince “<a href="http://davesmusicdatabase.blogspot.com/2012/06/prince-charted-with-when-doves-cry-june.html">When Doves Cry</a>” (1984) <br/>
    5.	Joan Jett &amp; the Blackhearts “<a href="http://davesmusicdatabase.blogspot.com/1981/12/12121981-joan-jett-rocks-charts.html">I Love Rock and Roll</a>” (1981) <br/>
    6.	U2 “<a href="http://davesmusicdatabase.blogspot.com/1987/05/5161987-u2-hit-1-with-with-or-without.html">With or Without You</a>” (1987) <br/>
    7.	Bon Jovi “<a href="https://davesmusicdatabase.blogspot.com/1987/02/bon-jovi-hit-1-with-livin-on-prayer.html">Livin’ on a Prayer</a>” (1986) <br/>
    8.	Lionel Richie &amp; Diana Ross “<a href="http://davesmusicdatabase.blogspot.com/2012/07/lionel-richie-and-diana-ross-debuted.html">Endless Love</a>” (1981) <br/>
    9.	Van Halen “<a href="https://davesmusicdatabase.blogspot.com/1984/02/van-halen-hit-1-with-jump.html">Jump</a>” (1984) <br/>
    10.	Michael Jackson “<a href="http://davesmusicdatabase.blogspot.com/1983/04/beat-it-becomes-michael-jacksons-second.html">Beat It</a>” (1983) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Queen “<a href="http://davesmusicdatabase.blogspot.com/2011/11/queen-charted-with-bohemian-rhapsody.html">Bohemian Rhapsody</a>” (1975) <br/>
    2.	John Lennon “<a href="http://davesmusicdatabase.blogspot.com/1971/10/john-lennon-charted-with-imagine.html">Imagine</a>” (1971) <br/>
    3.	Bee Gees “<a href="http://davesmusicdatabase.blogspot.com/1978/02/bee-gees-hit-1-with-stayin-alive.html">Stayin’ Alive</a>” (1977) <br/>
    4.	Simon &amp; Garfunkel “<a href="http://davesmusicdatabase.blogspot.com/2012/02/simon-garfunkel-hit-1-with-bridge-over.html">Bridge Over Troubled Water</a>” (1970) <br/>
    5.	Eagles “<a href="http://davesmusicdatabase.blogspot.com/2012/05/eagles-hotel-california-hit-1-may-7.html">Hotel California</a>” (1976) <br/>
    6.	Led Zeppelin “<a href="http://davesmusicdatabase.blogspot.com/1971/11/led-zeppelins-stairway-to-heaven-was.html">Stairway to Heaven</a>” (1971) <br/>
    7.	Don McLean “<a href="http://davesmusicdatabase.blogspot.com/2012/01/don-mcleans-american-pie-hit-1-january.html">American Pie</a>” (1971) <br/>
    8.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/1970/04/the-beatles-hit-1-with-let-it-be-april.html">Let It Be</a>” (1970) <br/>
    9.	Stevie Wonder “<a href="http://davesmusicdatabase.blogspot.com/1972/11/11111972-stevie-wonder-charts-with.html">Superstition</a>” (1972) <br/>
    10.	Derek &amp; the Dominos “<a href="http://davesmusicdatabase.blogspot.com/2012/03/derek-and-dominos-charted-with-layla.html">Layla</a>” (1970) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	The Rolling Stones “<a href="http://davesmusicdatabase.blogspot.com/2015/07/50-years-ago-today-rolling-stones-hit-1.html">(I Can’t Get No) Satisfaction</a>” (1965) <br/>
    2.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2018/11/50-years-ago-today-hey-jude-spent-9th.html">Hey Jude</a>” (1968) <br/>
    3.	Marvin Gaye “<a href="http://davesmusicdatabase.blogspot.com/2011/11/marvin-gayes-i-heard-it-through.html">I Heard It Through the Grapevine</a>” (1968) <br/>
    4.	Aretha Franklin “<a href="http://davesmusicdatabase.blogspot.com/2012/06/aretha-franklin-hit-1-with-respect-june.html">Respect</a>” (1967) <br/>
    5.	The Beatles “<a href="https://davesmusicdatabase.blogspot.com/2014/02/50-years-ago-today-beatles-hit-1-in-us.html">I Want to Hold Your Hand</a>” (1963) <br/>
    6.	The Beach Boys “<a href="http://davesmusicdatabase.blogspot.com/2011/10/beach-boys-charted-with-good-vibrations.html">Good Vibrations</a>” (1966) <br/>
    7.	The Beatles “<a href="http://davesmusicdatabase.blogspot.com/2013/10/the-beatles-hit-1-with-yesterday.html">Yesterday</a>” (1965) <br/>
    8.	Bob Dylan “<a href="http://davesmusicdatabase.blogspot.com/2011/07/bob-dylans-like-rolling-stone-debuts-on.html">Like a Rolling Stone</a>” (1965) <br/>
    9.	Otis Redding “<a href="http://davesmusicdatabase.blogspot.com/2014/01/otis-reddings-sittin-on-dock-of-bay-is.html">(Sittin’ on) The Dock of the Bay</a>” (1968) <br/>
    10.	The Animals “<a href="http://davesmusicdatabase.blogspot.com/2012/06/animals-charted-with-house-of-rising.html">The House of the Rising Sun</a>”(1964) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Bill Haley &amp; His Comets “<a href="http://davesmusicdatabase.blogspot.com/2010/07/happy-birthday-rock-and-roll-55-years.html">We’re Gonna Rock Around the Clock</a>” (1954) <br/>
    2.	Bobby Darin “<a href="http://davesmusicdatabase.blogspot.com/2011/08/bobby-darin-charts-with-mack-knife.html">Mack the Knife</a>” (1959) <br/>
    3.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2014/04/elvis-presley-hit-1-with-heartbreak.html">Heartbreak Hotel</a>” (1956) <br/>
    4.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2011/07/elvis-presley-performs-for-hound-dog.html">Hound Dog</a>” (1956) <br/>
    5.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2013/08/elvis-presley-hit-1-with-dont-be-cruel.html">Don’t Be Cruel</a>” (1956) <br/>
    6.	Elvis Presley “<a href="http://davesmusicdatabase.blogspot.com/2007/09/fifty-years-ago-today-elvis-presley.html">Jailhouse Rock</a>” (1957) <br/>
    7.	Chuck Berry “<a href="http://davesmusicdatabase.blogspot.com/2014/04/chuck-berry-charted-with-johnny-b-goode.html">Johnny B. Goode</a>” (1958) <br/>
    8.	Patti Page “<a href="http://davesmusicdatabase.blogspot.com/2011/11/patti-page-charted-with-tennessee-waltz.html">Tennessee Waltz</a>” (1950) <br/>
    9.	Ray Charles “<a href="http://davesmusicdatabase.blogspot.com/2009/02/fifty-years-ago-today-ray-charles.html">What’d I Say</a>” (1959) <br/>
    10.	The Everly Brothers “<a href="http://davesmusicdatabase.blogspot.com/2008/06/fifty-years-ago-today-everly-brothers.html">All I Have to Do Is Dream</a>” (1958) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Bing Crosby with the Ken Darby Singers “<a href="http://davesmusicdatabase.blogspot.com/2011/10/bing-crosby-hit-1-with-white-christmas.html">White Christmas</a>” (1942) <br/> 
    2.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2012/01/artie-shaw-charted-with-star-dust.html">Stardust</a>” (1941) <br/> 
    3.	Gene Autry “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1231949-gene-autry-charts-with-rudolph.html">Rudolph, the Red-Nosed Reindeer</a>” (1949) <br/> 
    4.	Glenn Miller with Tex Beneke &amp; the Four Modernaires “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11291941-glenn-miller-hits-1-with.html">Chattanooga Choo Choo</a>” (1941) <br/> 
    5.	Les Brown with Doris Day “<a href="http://davesmusicdatabase.blogspot.com/2016/03/331945-les-brown-charts-with.html">Sentimental Journey</a>” (1945) <br/> 
    6.	Nat “King” Cole “<a href="http://davesmusicdatabase.blogspot.com/2016/11/11231946-nat-king-cole-charted-with.html">The Christmas Song (Chestnuts Roasting on an Open Fire)</a>” (1946) <br/>
    7.	Tommy Dorsey with Frank Sinatra &amp; The Pied Pipers “<a href="http://davesmusicdatabase.blogspot.com/2011/07/frank-sinatra-hits-1-for-first-time_27.html">I’ll Never Smile Again</a>” (1940) <br/>
    8.	Cliff Edwards “<a href="http://davesmusicdatabase.blogspot.com/2013/02/cliff-edwards-charted-with-when-you.html">When You Wish Upon a Star</a>” (1940) <br/> 
    9.	Duke Ellington “<a href="http://davesmusicdatabase.blogspot.com/2011/07/duke-ellington-charts-with-take-a-train.html">Take the ‘A’ Train</a>” (1941) <br/> 
    10.	Dooley Wilson “<a href="http://davesmusicdatabase.blogspot.com/2014/11/as-time-goes-by-immortalized-by.html">As Time Goes By</a>” (1942) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Judy Garland “<a href="http://davesmusicdatabase.blogspot.com/2011/09/judy-garland-charts-with-over-rainbow.html">Over the Rainbow</a>” (1939) <br/>
    2.	Glenn Miller “<a href="http://davesmusicdatabase.blogspot.com/2011/10/glenn-miller-charts-with-in-mood.html">In the Mood</a>” (1939) <br/> 
    3.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2011/12/fred-astaire-hit-1-with-cole-porters.html">Night and Day</a>” (1932) <br/> 
    4.	Fred Astaire with Leo Reisman “<a href="http://davesmusicdatabase.blogspot.com/2013/08/cheek-to-cheek-hits-1-for-first-of-11.html">Cheek to Cheek</a>” (1935) <br/> 
    5.	Artie Shaw “<a href="http://davesmusicdatabase.blogspot.com/2013/11/artie-shaws-beguin-beguine-hit-1.html">Begin the Beguine</a>” (1938) <br/> 
    6.	Ethel Waters “<a href="http://davesmusicdatabase.blogspot.com/2014/05/ethel-waters-charted-with-stormy.html">Stormy Weather (Keeps Rainin' All the Time)</a>” (1933) <br/> 
    7.	Fred Astaire with Johnny Green “<a href="http://davesmusicdatabase.blogspot.com/2016/10/1031936-fred-astaire-hits-1-with-way.html">The Way You Look Tonight</a>” (1936) <br/> 
    8.	Bing Crosby with the Guardsmen Quartette “<a href="https://davesmusicdatabase.blogspot.com/1985/12/bing-crosby-charted-with-silent-night.html">Silent Night</a>” (1935) <br/> 
    9.	Ella Fitzgerald with Chick Webb “<a href="http://davesmusicdatabase.blogspot.com/2012/06/ella-fitzgerald-hit-1-with-tisket.html">A-Tisket, A-Tasket</a>” (1938) <br/>
    10.	Tommy Dorsey with Jack Leonard “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1271940-tommy-dorsey-lands-at-1-with.html">All the Things You Are</a>” (1939) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Bessie Smith with Louis Armstrong “<a href="http://davesmusicdatabase.blogspot.com/2011/11/wc-handy-charted-with-st-louis-blues.html">St. Louis Blues</a>” (1925) <br/>
    2.	Al Jolson “<a href="https://davesmusicdatabase.blogspot.com/2010/05/al-jolson-hit-1-with-swanee-90-years.html">Swanee</a>” (1920) <br/> 
    3.	Gene Austin “<a href="http://davesmusicdatabase.blogspot.com/2013/12/my-blue-heaven-hit-1-december-17-1927.html">My Blue Heaven</a>” (1927) <br/>
    4.	Thomas “Fats” Waller “<a href="http://davesmusicdatabase.blogspot.com/2016/11/1111929-fats-waller-releases-aint.html">Ain’t Misbehavin’</a>” (1929) <br/>
    5.	Paul Whiteman “<a href="http://davesmusicdatabase.blogspot.com/2011/10/paul-whitemans-whispering-hit-1-october.html">Whispering</a>” (1920) <br/>
    6.	Al Jolson "<a href="https://davesmusicdatabase.blogspot.com/2013/01/al-jolson-charted-with-april-showers.html">April Showers</a>” (1922) <br/>
    7.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2016/01/1241925-marion-harris-charted-with-tea.html">Tea for Two</a>” (1925) <br/>
    8.	Vernon Dalhart “<a href="http://davesmusicdatabase.blogspot.com/2011/08/vernon-dalhart-records-prisoners-song.html">The Prisoner’s Song</a>” (1925) <br/>
    9.	Ben Selvin “<a href="http://davesmusicdatabase.blogspot.com/2013/01/ben-selvin-charted-with-dardanella.html">Dardanella</a>” (1920) <br/>
    10.	Isham Jones “<a href="http://davesmusicdatabase.blogspot.com/2016/09/961924-isham-jones-takes-it-had-to-be.html">It Had to Be You</a>” (1924) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Arthur Collins &amp; Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2011/09/alexanders-ragtime-band-hits-1.html">Alexander’s Ragtime Band</a>” (1911) <br/>
    2.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/09/american-quartets-over-there-charts.html">Over There</a>” (1917) <br/>
    3.	Peerless Quartet “<a href="http://davesmusicdatabase.blogspot.com/2015/12/1221911-peerless-quartet-hit-1-for.html">Let Me Call You Sweetheart</a>” (1911) <br/>
    4.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2014/10/al-jolson-topped-charts-with-you-made.html">You Made Me Love You (I Didn't Want to Do It)</a>” (1913) <br/>
    5.	Billy Murray with the Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/04/by-light-of-silvery-moon-hit-1-april-23.html">By the Light of the Silvery Moon</a>” (1910) <br/>
    6.	American Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/moonlight-bay-hit-1-march-16-1912.html">Moonlight Bay</a>” (1912) <br/>
    7.	Original Dixieland Jazz Band “<a href="http://davesmusicdatabase.blogspot.com/2014/08/tiger-rag-charts-for-first-time-august.html">Tiger Rag</a>” (1918) <br/>
    8.	Sophie Tucker “<a href="http://davesmusicdatabase.blogspot.com/2014/07/sophie-tucker-charted-with-some-of.html">Some of These Days</a>” (1911) <br/>
    9.	Marion Harris “<a href="http://davesmusicdatabase.blogspot.com/2013/02/marion-harris-hit-1-with-after-youve.html">After You’ve Gone</a>” (1919) <br/>
    10.	Al Jolson “<a href="http://davesmusicdatabase.blogspot.com/2016/12/8171918-rock-bye-your-baby-with-dixie.html">Rock-a-Bye Your Baby with a Dixie Melody</a>” (1918) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2012/07/take-me-out-to-ball-game-in-celebration.html">Take Me Out to the Ball Game</a>” (1908) <br/>
    2.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/05/billy-murray-charted-with-youre-grand.html">You’re a Grand Old Flag (aka “The Grand Old Rag”)</a>” (1906) <br/>
    3.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2011/10/haydn-quartet-charted-with-sweet.html">Sweet Adeline (You’re the Flower of My Heart)</a>” (1904) <br/>
    4.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/02/2251905-billy-murray-takes-yankee.html">Yankee Doodle Boy</a>” (1905) <br/>
    5.	Arthur Collins “<a href="http://davesmusicdatabase.blogspot.com/2014/07/arthur-collins-hit-1-with-bill-bailey.html">Bill Bailey
    Won’t You Please Come Home</a>” (1902) <br/>
    6.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2014/07/give-my-regards-to-broadway-goes-to-1.html">Give My Regards to Broadway</a>” (1905) <br/>
    7.	Harry MacDonough with Miss Walton “<a href="http://davesmusicdatabase.blogspot.com/2012/04/shine-on-harvest-moon-hit-1-april-10_10.html">Shine on Harvest Moon</a>” (1909) <br/>
    8.	Haydn Quartet “<a href="http://davesmusicdatabase.blogspot.com/2014/03/in-good-old-summertime-hit-1-for-second.html">In the Good Old Summertime</a>” (1903) <br/>
    9.	Billy Murray “<a href="http://davesmusicdatabase.blogspot.com/2016/07/7231904-billy-murray-hits-1-with-meet.html">Meet Me in St. Louis Louis</a>” (1904) <br/>
    10.	Byron Harlan “<a href="http://davesmusicdatabase.blogspot.com/2012/05/byron-harlan-hit-1-with-school-days-may.html">School Days (When We Were a Couple of Kids)</a>” (1907) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p>
    
    1.	George J. Gaskin “<a href="https://davesmusicdatabase.blogspot.com/1993/04/100-years-ago-george-j-gaskin-hit-1.html">After the Ball</a>” (1893) <br/>
    2.	Arthur Collins “<a href="https://davesmusicdatabase.blogspot.com/1999/04/100-years-ago-arthur-collins-hit-1-with.html">Hello Ma Baby</a>” (1899) <br/>
    3.	John Yorke Atlee “<a href="https://davesmusicdatabase.blogspot.com/1991/08/100-years-ago-listen-to-mocking-bird.html">Listen to the Mocking Bird (aka “The Mocking Bird”)</a>” (1891) <br/>
    4.	John Philip Sousa “The Stars and Stripes Forever” (1897) <br/>
    5.	Dan Quinn “A Hot Time in the Old Town” (1896) <br/>
    6.	Katherine Lee Bates &amp; Samuel A. Ward (songwriters) “America the Beautiful” (1895) <br/>
    7.	Len Spencer “Ta-Ra-Ra Boom-De-Ay” (1892) <br/>
    8.	Scott Joplin “Maple Leaf Rag” (1899) <br/>
    9.	Dan Quinn “Daisy Bell (A Bicycle Built for Two)” (1893) <br/>
    10.	George J. Gaskin “On the Banks of the Wabash” (1897) <br/>
    </p>
    <p></p>
    <p>
    </p>
    <p></p>
    <p></p>
    <p class="comment-content">Dave should fix this. He has "I Heard It Through the Grapevine" twice - once by Marvin Gaye in 1968, which is correct, and once by the Beach Boys in 1966, which is wrong. I'm pretty sure the Beach Boys song was intended to be "Good Vibrations".</p>
    <p class="comment-content">Thanks for the catch, Pat. It has been corrected.</p>
    <p class="comment-content">I love all of them. Incredible list. Thanks for sharing with us. "My Blue Heaven" is my all-time favorite song. I still know that I used to dance on this track like crazy. Here is a website which has huge collection of such 90's Era songs. <a href="http://www.tubemp3.audio/" rel="nofollow">Visit Here</a></p>
    <p class="comment-content">Great list of songs from each decade, I really love some of the older ones. <br/>Just one question, how come "Charleston" isn't with list of 1920s hits?<br/>Other than that, very good list of some of the best music from the times</p>
    <p class="comment-content">Thanks for the feedback. "Charleston" doesn't make the top 10, but it is on the list of the best songs of the 1920s. You can see the full list here: http://davesmusicdatabase.blogspot.com/2014/07/top-100-songs-from-1920-1929.html</p>
    <p class="comment-content">Hi trying to find song sung in australian schools late 1920 or early 1930 called buttercups and daisies. Anyone able to help identify </p>
    <p class="comment-content">Do you mean the old folk song Rolling on the Grass - that has the line in it "Rolling on the grass amongst the buttercups and daisies" in the chorus? If so, it's by Michael Kilgarriff, who wrote popular folk songs from the late 1800s to around 1920.</p>
    <p class="comment-content">LOVE this site, btw. You really should be commended! Dana Graybeal</p>
    <p class="comment-content">Great song collection </p>
    <p class="comment-content">What information was used to create lists for 1890s, 1900s and 1910s<br/><br/></p>
    <p class="comment-content">Appearances on best-of lists, chart peaks, and sales all factor in.</p>
    <p class="comment-content">It would be interesting to see a similar page to this but for Albums and Musical Acts</p>
    <p class="comment-footer">
    </p>
    <p>
    </p>



```python
started = False
all_songs = []
#create and clean up list of all songs

for song in soup.find_all('a'): 
    if 'Uptown Funk!' in song.text:
        started = True
    if started:
        if not song.text == '\n' and not song.text == " " and not song.text == '':
            if "Best-of Lists" in song.text:
                break
            print("SONG ", song.text)
            all_songs.append(song.text)
            
#manual fixes
all_songs += ["The Stars and Stripes Forever", "A Hot Time in the Old Town", "America the Beautiful”, Ta-Ra-Ra Boom-De-Ay", "Maple Leaf Rag", "Daisy Bell (A Bicycle Built for Two)", "On the Banks of the Wabash"] 
print(all_songs)
```

    SONG  Uptown Funk!
    SONG  Shape of You
    SONG  Rolling in the Deep
    SONG  Happy
    SONG  Despacito
    SONG  Somebody That I Used to Know
    SONG  Blurred Lines
    SONG  Call Me Maybe
    SONG  Hello
    SONG  Old Town Road
    SONG  Hey Ya!
    SONG  I Gotta Feeling
    SONG  Lose Yourself
    SONG  Yeah!
    SONG  Crazy in Love
    SONG  Crazy
    SONG  Single Ladies (Put a Ring on It)
    SONG  Umbrella
    SONG  Low
    SONG  We Belong Together
    SONG  I Will Always Love You
    SONG  Smells Like Teen Spirit
    SONG  (Everything I Do) I Do It for You
    SONG  Nothing Compares 2 U
    SONG  My Heart Will Go On
    SONG  Candle in the Wind 1997 (Goodbye England’s Rose)
    SONG  Losing My Religion
    SONG  Wonderwall
    SONG  Macarena (Bayside Boys Mix)
    SONG  One
    SONG  Billie Jean
    SONG  Every Breath You Take
    SONG  Sweet Child O’ Mine
    SONG  When Doves Cry
    SONG  I Love Rock and Roll
    SONG  With or Without You
    SONG  Livin’ on a Prayer
    SONG  Endless Love
    SONG  Jump
    SONG  Beat It
    SONG  Bohemian Rhapsody
    SONG  Imagine
    SONG  Stayin’ Alive
    SONG  Bridge Over Troubled Water
    SONG  Hotel California
    SONG  Stairway to Heaven
    SONG  American Pie
    SONG  Let It Be
    SONG  Superstition
    SONG  Layla
    SONG  (I Can’t Get No) Satisfaction
    SONG  Hey Jude
    SONG  I Heard It Through the Grapevine
    SONG  Respect
    SONG  I Want to Hold Your Hand
    SONG  Good Vibrations
    SONG  Yesterday
    SONG  Like a Rolling Stone
    SONG  (Sittin’ on) The Dock of the Bay
    SONG  The House of the Rising Sun
    SONG  We’re Gonna Rock Around the Clock
    SONG  Mack the Knife
    SONG  Heartbreak Hotel
    SONG  Hound Dog
    SONG  Don’t Be Cruel
    SONG  Jailhouse Rock
    SONG  Johnny B. Goode
    SONG  Tennessee Waltz
    SONG  What’d I Say
    SONG  All I Have to Do Is Dream
    SONG  White Christmas
    SONG  Stardust
    SONG  Rudolph, the Red-Nosed Reindeer
    SONG  Chattanooga Choo Choo
    SONG  Sentimental Journey
    SONG  The Christmas Song (Chestnuts Roasting on an Open Fire)
    SONG  I’ll Never Smile Again
    SONG  When You Wish Upon a Star
    SONG  Take the ‘A’ Train
    SONG  As Time Goes By
    SONG  Over the Rainbow
    SONG  In the Mood
    SONG  Night and Day
    SONG  Cheek to Cheek
    SONG  Begin the Beguine
    SONG  Stormy Weather (Keeps Rainin' All the Time)
    SONG  The Way You Look Tonight
    SONG  Silent Night
    SONG  A-Tisket, A-Tasket
    SONG  All the Things You Are
    SONG  St. Louis Blues
    SONG  Swanee
    SONG  My Blue Heaven
    SONG  Ain’t Misbehavin’
    SONG  Whispering
    SONG  April Showers
    SONG  Tea for Two
    SONG  The Prisoner’s Song
    SONG  Dardanella
    SONG  It Had to Be You
    SONG  Alexander’s Ragtime Band
    SONG  Over There
    SONG  Let Me Call You Sweetheart
    SONG  You Made Me Love You (I Didn't Want to Do It)
    SONG  By the Light of the Silvery Moon
    SONG  Moonlight Bay
    SONG  Tiger Rag
    SONG  Some of These Days
    SONG  After You’ve Gone
    SONG  Rock-a-Bye Your Baby with a Dixie Melody
    SONG  Take Me Out to the Ball Game
    SONG  You’re a Grand Old Flag (aka “The Grand Old Rag”)
    SONG  Sweet Adeline (You’re the Flower of My Heart)
    SONG  Yankee Doodle Boy
    SONG  Bill Bailey
    Won’t You Please Come Home
    SONG  Give My Regards to Broadway
    SONG  Shine on Harvest Moon
    SONG  In the Good Old Summertime
    SONG  Meet Me in St. Louis Louis
    SONG  School Days (When We Were a Couple of Kids)
    SONG  After the Ball
    SONG  Hello Ma Baby
    SONG  Listen to the Mocking Bird (aka “The Mocking Bird”)
    ['Uptown Funk!', 'Shape of You', 'Rolling in the Deep', 'Happy', 'Despacito', 'Somebody That I Used to Know', 'Blurred Lines', 'Call Me Maybe', 'Hello', 'Old Town Road', 'Hey Ya!', 'I Gotta Feeling', 'Lose Yourself', 'Yeah!', 'Crazy in Love', 'Crazy', 'Single Ladies (Put a Ring on It)', 'Umbrella', 'Low', 'We Belong Together', 'I Will Always Love You', 'Smells Like Teen Spirit', '(Everything I Do) I Do It for You', 'Nothing Compares 2 U', 'My Heart Will Go On', 'Candle in the Wind 1997 (Goodbye England’s Rose)', 'Losing My Religion', 'Wonderwall', 'Macarena (Bayside Boys Mix)', 'One', 'Billie Jean', 'Every Breath You Take', 'Sweet Child O’ Mine', 'When Doves Cry', 'I Love Rock and Roll', 'With or Without You', 'Livin’ on a Prayer', 'Endless Love', 'Jump', 'Beat It', 'Bohemian Rhapsody', 'Imagine', 'Stayin’ Alive', 'Bridge Over Troubled Water', 'Hotel California', 'Stairway to Heaven', 'American Pie', 'Let It Be', 'Superstition', 'Layla', '(I Can’t Get No) Satisfaction', 'Hey Jude', 'I Heard It Through the Grapevine', 'Respect', 'I Want to Hold Your Hand', 'Good Vibrations', 'Yesterday', 'Like a Rolling Stone', '(Sittin’ on) The Dock of the Bay', 'The House of the Rising Sun', 'We’re Gonna Rock Around the Clock', 'Mack the Knife', 'Heartbreak Hotel', 'Hound Dog', 'Don’t Be Cruel', 'Jailhouse Rock', 'Johnny B. Goode', 'Tennessee Waltz', 'What’d I Say', 'All I Have to Do Is Dream', 'White Christmas', 'Stardust', 'Rudolph, the Red-Nosed Reindeer', 'Chattanooga Choo Choo', 'Sentimental Journey', 'The Christmas Song (Chestnuts Roasting on an Open Fire)', 'I’ll Never Smile Again', 'When You Wish Upon a Star', 'Take the ‘A’ Train', 'As Time Goes By', 'Over the Rainbow', 'In the Mood', 'Night and Day', 'Cheek to Cheek', 'Begin the Beguine', "Stormy Weather (Keeps Rainin' All the Time)", 'The Way You Look Tonight', 'Silent Night', 'A-Tisket, A-Tasket', 'All the Things You Are', 'St. Louis Blues', 'Swanee', 'My Blue Heaven', 'Ain’t Misbehavin’', 'Whispering', 'April Showers', 'Tea for Two', 'The Prisoner’s Song', 'Dardanella', 'It Had to Be You', 'Alexander’s Ragtime Band', 'Over There', 'Let Me Call You Sweetheart', "You Made Me Love You (I Didn't Want to Do It)", 'By the Light of the Silvery Moon', 'Moonlight Bay', 'Tiger Rag', 'Some of These Days', 'After You’ve Gone', 'Rock-a-Bye Your Baby with a Dixie Melody', 'Take Me Out to the Ball Game', 'You’re a Grand Old Flag (aka “The Grand Old Rag”)', 'Sweet Adeline (You’re the Flower of My Heart)', 'Yankee Doodle Boy', 'Bill Bailey\nWon’t You Please Come Home', 'Give My Regards to Broadway', 'Shine on Harvest Moon', 'In the Good Old Summertime', 'Meet Me in St. Louis Louis', 'School Days (When We Were a Couple of Kids)', 'After the Ball', 'Hello Ma Baby', 'Listen to the Mocking Bird (aka “The Mocking Bird”)', 'The Stars and Stripes Forever', 'A Hot Time in the Old Town', 'America the Beautiful”, Ta-Ra-Ra Boom-De-Ay', 'Maple Leaf Rag', 'Daisy Bell (A Bicycle Built for Two)', 'On the Banks of the Wabash']



```python
#Create a dictionary to store songs for each decade
import collections
from bs4.element import NavigableString
num_decades = 13
decades_dict = {}
starting_decade = 1890
for i in range(num_decades):
    decades_dict[starting_decade] = []
    starting_decade += 10
#put songs into their decade dicts
decade = 2020
for i in range(len(all_songs)):
    if i % 10 == 0:
        decade -= 10
    if decade < 1890:
        break
    decades_dict[decade].append(all_songs[i])

#Now we have all our song titles in their appropriate decade dictionaries! Woo!
print(decades_dict)
```

    {1890: ['After the Ball', 'Hello Ma Baby', 'Listen to the Mocking Bird (aka “The Mocking Bird”)', 'The Stars and Stripes Forever', 'A Hot Time in the Old Town', 'America the Beautiful”, Ta-Ra-Ra Boom-De-Ay', 'Maple Leaf Rag', 'Daisy Bell (A Bicycle Built for Two)', 'On the Banks of the Wabash'], 1900: ['Take Me Out to the Ball Game', 'You’re a Grand Old Flag (aka “The Grand Old Rag”)', 'Sweet Adeline (You’re the Flower of My Heart)', 'Yankee Doodle Boy', 'Bill Bailey\nWon’t You Please Come Home', 'Give My Regards to Broadway', 'Shine on Harvest Moon', 'In the Good Old Summertime', 'Meet Me in St. Louis Louis', 'School Days (When We Were a Couple of Kids)'], 1910: ['Alexander’s Ragtime Band', 'Over There', 'Let Me Call You Sweetheart', "You Made Me Love You (I Didn't Want to Do It)", 'By the Light of the Silvery Moon', 'Moonlight Bay', 'Tiger Rag', 'Some of These Days', 'After You’ve Gone', 'Rock-a-Bye Your Baby with a Dixie Melody'], 1920: ['St. Louis Blues', 'Swanee', 'My Blue Heaven', 'Ain’t Misbehavin’', 'Whispering', 'April Showers', 'Tea for Two', 'The Prisoner’s Song', 'Dardanella', 'It Had to Be You'], 1930: ['Over the Rainbow', 'In the Mood', 'Night and Day', 'Cheek to Cheek', 'Begin the Beguine', "Stormy Weather (Keeps Rainin' All the Time)", 'The Way You Look Tonight', 'Silent Night', 'A-Tisket, A-Tasket', 'All the Things You Are'], 1940: ['White Christmas', 'Stardust', 'Rudolph, the Red-Nosed Reindeer', 'Chattanooga Choo Choo', 'Sentimental Journey', 'The Christmas Song (Chestnuts Roasting on an Open Fire)', 'I’ll Never Smile Again', 'When You Wish Upon a Star', 'Take the ‘A’ Train', 'As Time Goes By'], 1950: ['We’re Gonna Rock Around the Clock', 'Mack the Knife', 'Heartbreak Hotel', 'Hound Dog', 'Don’t Be Cruel', 'Jailhouse Rock', 'Johnny B. Goode', 'Tennessee Waltz', 'What’d I Say', 'All I Have to Do Is Dream'], 1960: ['(I Can’t Get No) Satisfaction', 'Hey Jude', 'I Heard It Through the Grapevine', 'Respect', 'I Want to Hold Your Hand', 'Good Vibrations', 'Yesterday', 'Like a Rolling Stone', '(Sittin’ on) The Dock of the Bay', 'The House of the Rising Sun'], 1970: ['Bohemian Rhapsody', 'Imagine', 'Stayin’ Alive', 'Bridge Over Troubled Water', 'Hotel California', 'Stairway to Heaven', 'American Pie', 'Let It Be', 'Superstition', 'Layla'], 1980: ['Billie Jean', 'Every Breath You Take', 'Sweet Child O’ Mine', 'When Doves Cry', 'I Love Rock and Roll', 'With or Without You', 'Livin’ on a Prayer', 'Endless Love', 'Jump', 'Beat It'], 1990: ['I Will Always Love You', 'Smells Like Teen Spirit', '(Everything I Do) I Do It for You', 'Nothing Compares 2 U', 'My Heart Will Go On', 'Candle in the Wind 1997 (Goodbye England’s Rose)', 'Losing My Religion', 'Wonderwall', 'Macarena (Bayside Boys Mix)', 'One'], 2000: ['Hey Ya!', 'I Gotta Feeling', 'Lose Yourself', 'Yeah!', 'Crazy in Love', 'Crazy', 'Single Ladies (Put a Ring on It)', 'Umbrella', 'Low', 'We Belong Together'], 2010: ['Uptown Funk!', 'Shape of You', 'Rolling in the Deep', 'Happy', 'Despacito', 'Somebody That I Used to Know', 'Blurred Lines', 'Call Me Maybe', 'Hello', 'Old Town Road']}



```python
#Time to Scrape from Genius to get the lyrics. The goal is to get the lyrics of each decade into one file or string.
!pip install lyricsgenius
```

    Collecting lyricsgenius
      Downloading lyricsgenius-3.0.1-py3-none-any.whl (59 kB)
    [K     |████████████████████████████████| 59 kB 8.0 MB/s  eta 0:00:01
    [?25hRequirement already satisfied: requests>=2.20.0 in /opt/anaconda3/lib/python3.9/site-packages (from lyricsgenius) (2.27.1)
    Requirement already satisfied: beautifulsoup4>=4.6.0 in /opt/anaconda3/lib/python3.9/site-packages (from lyricsgenius) (4.11.1)
    Requirement already satisfied: soupsieve>1.2 in /opt/anaconda3/lib/python3.9/site-packages (from beautifulsoup4>=4.6.0->lyricsgenius) (2.3.1)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda3/lib/python3.9/site-packages (from requests>=2.20.0->lyricsgenius) (1.26.9)
    Requirement already satisfied: idna<4,>=2.5 in /opt/anaconda3/lib/python3.9/site-packages (from requests>=2.20.0->lyricsgenius) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda3/lib/python3.9/site-packages (from requests>=2.20.0->lyricsgenius) (2021.10.8)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /opt/anaconda3/lib/python3.9/site-packages (from requests>=2.20.0->lyricsgenius) (2.0.4)
    Installing collected packages: lyricsgenius
    Successfully installed lyricsgenius-3.0.1



```python
import requests
import urllib.parse
import urllib.request
import json

#this function gets the genius url associated with the song title
def get_url(title):
    client_access_token = '1WP4zC8-nOFFg6ijbocMUGMVBA2Ik1God5SFl7ILwBjDD9fhNJF0jx-dyu5yS2HG'
    # Format a request URI for the Genius API
    search_term = title
    _URL_API = "https://api.genius.com/"
    _URL_SEARCH = "search?q="
    querystring = _URL_API + _URL_SEARCH + urllib.parse.quote(search_term)
    request = urllib.request.Request(querystring)
    request.add_header("Authorization", "Bearer " + client_access_token)
    request.add_header("User-Agent", "")

    response = urllib.request.urlopen(request, timeout=3)
    data = response.read()
    json_obj = json.loads(data)
    
    return json_obj['response']['hits'][0]['result']['url']

import urllib.request
import urllib.parse
import urllib.error
from bs4 import BeautifulSoup
import ssl
import json
import ast
import os
from urllib.request import Request, urlopen

# For ignoring SSL certificate errors
def output_json(url, decade):
    ctx = ssl.create_default_context()
    ctx.check_hostname = False
    ctx.verify_mode = ssl.CERT_NONE

    # Making the website believe that you are accessing it using a mozilla browser
    req = Request(url, headers = {'User-Agent': 'Mozilla/5.0'})
    webpage = urlopen(req).read()

    # Creating a BeautifulSoup object of the html page for easy extraction of data.

    soup = BeautifulSoup(webpage, 'html.parser')
    html = soup.prettify('utf-8')
    song_json = {}
    song_json["Lyrics"] = [];

    #Extract the Lyrics of the song
    for div in soup.findAll('div'): #not cleaned, but workable
        song_json['Lyrics'].append(div.text.strip().split("n"));
    
    #Save to a file
    with open(str(decade) + '.json', 'a') as outfile:
        json.dump(song_json, outfile, indent = 4, ensure_ascii = False)


for decade in decades_dict.keys():
    for song in decades_dict[decade]:
        try:
            url = get_url(song)
            print(url)
            output_json(url, decade)
        except Exception:
            print(song + " not available on genius")
      
```

    https://genius.com/Paul-mccartney-and-wings-after-the-ball-million-miles-lyrics
    https://genius.com/Arthur-collins-hello-ma-baby-lyrics
    https://genius.com/Js-aka-the-best-red-rum-lyrics
    https://genius.com/John-philip-sousa-the-stars-and-stripes-forever-lyrics
    https://genius.com/Lavern-baker-therell-be-a-hot-time-in-the-old-town-tonight-lyrics
    America the Beautiful”, Ta-Ra-Ra Boom-De-Ay not available on genius
    https://genius.com/Scott-joplin-maple-leaf-rag-lyrics
    https://genius.com/Nat-king-cole-daisy-bell-bicycle-built-for-two-lyrics
    https://genius.com/Rufus-wainwright-on-the-banks-of-the-wabash-lyrics
    https://genius.com/Melvins-take-me-out-to-the-ball-game-lyrics
    https://genius.com/Grind-time-now-dizaster-vs-organik-lyrics
    https://genius.com/Four-harmony-kings-sweet-adeline-lyrics
    https://genius.com/Bing-crosby-yankee-doodle-boy-lyrics
    https://genius.com/Bobby-darin-bill-bailey-wont-you-please-come-home-lyrics
    https://genius.com/George-m-cohan-give-my-regards-to-broadway-lyrics
    https://genius.com/Judy-garland-judy-at-the-palace-medley-shine-on-harvest-moon-some-of-these-days-my-man-i-dont-care-lyrics
    https://genius.com/Nat-king-cole-in-the-good-old-summertime-lyrics
    https://genius.com/Judy-garland-meet-me-in-st-louis-louis-lyrics
    https://genius.com/Julian-velard-the-guy-who-lyrics
    https://genius.com/Irving-berlin-alexanders-ragtime-band-lyrics
    https://genius.com/The-boondocks-dont-trust-them-new-niggas-over-there-annotated
    https://genius.com/Bing-crosby-let-me-call-you-sweetheart-1934-lyrics
    https://genius.com/Patsy-cline-you-made-me-love-you-i-didnt-want-to-do-it-lyrics
    https://genius.com/Doris-day-by-the-light-of-the-silvery-moon-lyrics
    https://genius.com/Doris-day-moonlight-bay-lyrics
    https://genius.com/Art-tatum-tiger-rag-lyrics
    https://genius.com/Sophie-tucker-some-of-these-days-lyrics
    https://genius.com/Bessie-smith-after-youve-gone-lyrics
    https://genius.com/Al-jolson-rock-a-bye-your-baby-with-a-dixie-melody-lyrics
    https://genius.com/W-c-handy-st-louis-blues-lyrics
    https://genius.com/Al-jolson-swanee-lyrics
    https://genius.com/Taking-back-sunday-my-blue-heaven-lyrics
    https://genius.com/Fats-waller-aint-misbehavin-lyrics
    https://genius.com/Duncan-sheik-whispering-lyrics
    https://genius.com/Proleter-april-showers-lyrics
    https://genius.com/Ella-fitzgerald-tea-for-two-lyrics
    https://genius.com/Vernon-dalhart-the-prisoners-song-lyrics
    https://genius.com/Bing-crosby-and-louis-armstrong-dardanella-lyrics
    https://genius.com/Frank-sinatra-it-had-to-be-you-lyrics
    https://genius.com/Judy-garland-over-the-rainbow-lyrics
    https://genius.com/Lil-tjay-fivio-foreign-and-kay-flock-not-in-the-mood-lyrics
    https://genius.com/Ella-fitzgerald-night-and-day-lyrics
    https://genius.com/Ella-fitzgerald-and-louis-armstrong-cheek-to-cheek-lyrics
    https://genius.com/Frank-sinatra-begin-the-beguine-lyrics
    https://genius.com/Ana-canas-stormy-weather-keeps-rainin-all-the-time-lyrics
    https://genius.com/Frank-sinatra-the-way-you-look-tonight-lyrics
    https://genius.com/Christmas-songs-silent-night-lyrics
    https://genius.com/Ella-fitzgerald-a-tisket-a-tasket-lyrics
    https://genius.com/Michael-jackson-all-the-things-you-are-lyrics
    https://genius.com/Bing-crosby-white-christmas-1947-release-lyrics
    https://genius.com/David-bowie-space-oddity-lyrics
    https://genius.com/Christmas-songs-rudolph-the-red-nosed-reindeer-lyrics
    https://genius.com/Glenn-miller-and-his-orchestra-chattanooga-choo-choo-lyrics
    https://genius.com/Doris-day-sentimental-journey-lyrics
    https://genius.com/Justin-bieber-the-christmas-song-chestnuts-roasting-on-an-open-fire-lyrics
    https://genius.com/Frank-sinatra-ill-never-smile-again-lyrics
    https://genius.com/Cliff-edwards-and-disney-studio-chorus-when-you-wish-upon-a-star-lyrics
    https://genius.com/Ella-fitzgerald-take-the-a-train-lyrics
    https://genius.com/Phora-as-time-goes-by-lyrics
    https://genius.com/Bill-haley-and-his-comets-were-gonna-rock-around-the-clock-lyrics
    https://genius.com/Bobby-darin-mack-the-knife-lyrics
    https://genius.com/Elvis-presley-heartbreak-hotel-lyrics
    https://genius.com/Elvis-presley-hound-dog-lyrics
    https://genius.com/Elvis-presley-dont-be-cruel-lyrics
    https://genius.com/Elvis-presley-jailhouse-rock-lyrics
    https://genius.com/Chuck-berry-johnny-b-goode-lyrics
    https://genius.com/Patti-page-tennessee-waltz-lyrics
    https://genius.com/Ray-charles-whatd-i-say-lyrics
    https://genius.com/The-everly-brothers-all-i-have-to-do-is-dream-lyrics
    https://genius.com/The-rolling-stones-i-cant-get-no-satisfaction-lyrics
    https://genius.com/The-beatles-hey-jude-lyrics
    https://genius.com/Marvin-gaye-i-heard-it-through-the-grapevine-lyrics
    https://genius.com/Damso-n-j-respect-r-lyrics
    https://genius.com/The-beatles-i-want-to-hold-your-hand-lyrics
    https://genius.com/The-beach-boys-good-vibrations-lyrics
    https://genius.com/The-beatles-yesterday-lyrics
    https://genius.com/Bob-dylan-like-a-rolling-stone-lyrics
    https://genius.com/Otis-redding-sittin-on-the-dock-of-the-bay-lyrics
    https://genius.com/The-animals-the-house-of-the-rising-sun-lyrics
    https://genius.com/Queen-bohemian-rhapsody-lyrics
    https://genius.com/Imagine-dragons-believer-lyrics
    https://genius.com/Bee-gees-stayin-alive-lyrics
    https://genius.com/Simon-and-garfunkel-bridge-over-troubled-water-lyrics
    https://genius.com/Eagles-hotel-california-lyrics
    https://genius.com/Led-zeppelin-stairway-to-heaven-lyrics
    https://genius.com/Don-mclean-american-pie-lyrics
    https://genius.com/The-beatles-let-it-be-lyrics
    https://genius.com/Stevie-wonder-superstition-lyrics
    https://genius.com/Dj-robin-and-schurze-layla-lyrics
    https://genius.com/Michael-jackson-billie-jean-lyrics
    https://genius.com/The-police-every-breath-you-take-lyrics
    https://genius.com/Guns-n-roses-sweet-child-o-mine-lyrics
    https://genius.com/Prince-and-the-revolution-when-doves-cry-lyrics
    https://genius.com/Ghoti-hook-i-love-rock-and-roll-lyrics
    https://genius.com/U2-with-or-without-you-lyrics
    https://genius.com/Bon-jovi-livin-on-a-prayer-lyrics
    https://genius.com/Lionel-richie-and-diana-ross-endless-love-lyrics
    https://genius.com/Drake-and-future-jumpman-lyrics
    https://genius.com/Michael-jackson-beat-it-lyrics
    https://genius.com/Whitney-houston-i-will-always-love-you-lyrics
    https://genius.com/Nirvana-smells-like-teen-spirit-lyrics
    https://genius.com/Bryan-adams-everything-i-do-i-do-it-for-you-lyrics
    https://genius.com/Sinead-oconnor-nothing-compares-2-u-lyrics
    https://genius.com/Celine-dion-my-heart-will-go-on-lyrics
    https://genius.com/Elton-john-candle-in-the-wind-1997-lyrics
    https://genius.com/Rem-losing-my-religion-lyrics
    https://genius.com/Oasis-wonderwall-lyrics
    https://genius.com/Miguel-de-cervantes-dialogue-between-scipio-and-berganza-annotated
    https://genius.com/Drake-one-dance-lyrics
    https://genius.com/Outkast-hey-ya-lyrics
    https://genius.com/Black-eyed-peas-i-gotta-feeling-lyrics
    https://genius.com/Eminem-lose-yourself-lyrics
    https://genius.com/Joji-yeah-right-lyrics
    https://genius.com/Beyonce-crazy-in-love-lyrics
    https://genius.com/Afroman-crazy-rap-colt-45-and-2-zig-zags-lyrics
    https://genius.com/Beyonce-single-ladies-put-a-ring-on-it-lyrics
    https://genius.com/Rihanna-umbrella-lyrics
    https://genius.com/Future-low-life-lyrics
    https://genius.com/Mariah-carey-we-belong-together-lyrics
    https://genius.com/Mark-ronson-uptown-funk-lyrics
    https://genius.com/Ed-sheeran-shape-of-you-lyrics
    https://genius.com/Adele-rolling-in-the-deep-lyrics
    https://genius.com/Pharrell-williams-happy-lyrics
    https://genius.com/Luis-fonsi-and-daddy-yankee-despacito-remix-lyrics
    https://genius.com/Gotye-somebody-that-i-used-to-know-lyrics
    https://genius.com/Robin-thicke-blurred-lines-lyrics
    https://genius.com/Carly-rae-jepsen-call-me-maybe-lyrics
    https://genius.com/Adele-hello-lyrics
    https://genius.com/Lil-nas-x-old-town-road-remix-lyrics



```python
from pathlib import Path
gazetteer = Path("all_places.txt").read_text()
gazetteer = gazetteer.split("\n")
print(gazetteer)

#list of all the places in the world
```

    ['Alabama', 'Alexander City', 'Andalusia', 'Anniston', 'Athens', 'Atmore', 'Auburn', 'Bessemer', 'Birmingham', 'Chickasaw', 'Clanton', 'Cullman', 'Decatur', 'Demopolis', 'Dothan', 'Enterprise', 'Eufaula', 'Florence', 'Fort Payne', 'Gadsden', 'Greenville', 'Guntersville', 'Huntsville', 'Jasper', 'Marion', 'Mobile', 'Montgomery', 'Opelika', 'Ozark', 'Phenix City', 'Prichard', 'Scottsboro', 'Selma', 'Sheffield', 'Sylacauga', 'Talladega', 'Troy', 'Tuscaloosa', 'Tuscumbia', 'Tuskegee', 'Alaska', 'Anchorage', 'Cordova', 'Fairbanks', 'Haines', 'Homer', 'Juneau', 'Ketchikan', 'Kodiak', 'Kotzebue', 'Nome', 'Palmer', 'Seward', 'Sitka', 'Skagway', 'Valdez', 'Arizona', 'Ajo', 'Avondale', 'Bisbee', 'Casa Grande', 'Chandler', 'Clifton', 'Douglas', 'Flagstaff', 'Florence', 'Gila Bend', 'Glendale', 'Globe', 'Kingman', 'Lake Havasu City', 'Mesa', 'Nogales', 'Oraibi', 'Phoenix', 'Prescott', 'Scottsdale', 'Sierra Vista', 'Tempe', 'Tombstone', 'Tucson', 'Walpi', 'Window Rock', 'Winslow', 'Yuma', 'Arkansas', 'Arkadelphia', 'Arkansas Post', 'Batesville', 'Benton', 'Blytheville', 'Camden', 'Conway', 'Crossett', 'El Dorado', 'Fayetteville', 'Forrest City', 'Fort Smith', 'Harrison', 'Helena', 'Hope', 'Hot Springs', 'Jacksonville', 'Jonesboro', 'Little Rock', 'Magnolia', 'Morrilton', 'Newport', 'North Little Rock', 'Osceola', 'Pine Bluff', 'Rogers', 'Searcy', 'Stuttgart', 'Van Buren', 'West Memphis', 'California', 'Alameda', 'Alhambra', 'Anaheim', 'Antioch', 'Arcadia', 'Bakersfield', 'Barstow', 'Belmont', 'Berkeley', 'Beverly Hills', 'Brea', 'Buena Park', 'Burbank', 'Calexico', 'Calistoga', 'Carlsbad', 'Carmel', 'Chico', 'Chula Vista', 'Claremont', 'Compton', 'Concord', 'Corona', 'Coronado', 'Costa Mesa', 'Culver City', 'Daly City', 'Davis', 'Downey', 'El Centro', 'El Cerrito', 'El Monte', 'Escondido', 'Eureka', 'Fairfield', 'Fontana', 'Fremont', 'Fresno', 'Fullerton', 'Garden Grove', 'Glendale', 'Hayward', 'Hollywood', 'Huntington Beach', 'Indio', 'Inglewood', 'Irvine', 'La Habra', 'Laguna Beach', 'Lancaster', 'Livermore', 'Lodi', 'Lompoc', 'Long Beach', 'Los Angeles', 'Malibu', 'Martinez', 'Marysville', 'Menlo Park', 'Merced', 'Modesto', 'Monterey', 'Mountain View', 'Napa', 'Needles', 'Newport Beach', 'Norwalk', 'Novato', 'Oakland', 'Oceanside', 'Ojai', 'Ontario', 'Orange', 'Oroville', 'Oxnard', 'Pacific Grove', 'Palm Springs', 'Palmdale', 'Palo Alto', 'Pasadena', 'Petaluma', 'Pomona', 'Port Hueneme', 'Rancho Cucamonga', 'Red Bluff', 'Redding', 'Redlands', 'Redondo Beach', 'Redwood City', 'Richmond', 'Riverside', 'Roseville', 'Sacramento', 'Salinas', 'San Bernardino', 'San Clemente', 'San Diego', 'San Fernando', 'San Francisco', 'San Gabriel', 'San Jose', 'San Juan Capistrano', 'San Leandro', 'San Luis Obispo', 'San Marino', 'San Mateo', 'San Pedro', 'San Rafael', 'San Simeon', 'Santa Ana', 'Santa Barbara', 'Santa Clara', 'Santa Clarita', 'Santa Cruz', 'Santa Monica', 'Santa Rosa', 'Sausalito', 'Simi Valley', 'Sonoma', 'South San Francisco', 'Stockton', 'Sunnyvale', 'Susanville', 'Thousand Oaks', 'Torrance', 'Turlock', 'Ukiah', 'Vallejo', 'Ventura', 'Victorville', 'Visalia', 'Walnut Creek', 'Watts', 'West Covina', 'Whittier', 'Woodland', 'Yorba Linda', 'Yuba City', 'Colorado', 'Alamosa', 'Aspen', 'Aurora', 'Boulder', 'Breckenridge', 'Brighton', 'Canon City', 'Central City', 'Climax', 'Colorado Springs', 'Cortez', 'Cripple Creek', 'Denver', 'Durango', 'Englewood', 'Estes Park', 'Fort Collins', 'Fort Morgan', 'Georgetown', 'Glenwood Springs', 'Golden', 'Grand Junction', 'Greeley', 'Gunnison', 'La Junta', 'Leadville', 'Littleton', 'Longmont', 'Loveland', 'Montrose', 'Ouray', 'Pagosa Springs', 'Pueblo', 'Silverton', 'Steamboat Springs', 'Sterling', 'Telluride', 'Trinidad', 'Vail', 'Walsenburg', 'Westminster', 'Connecticut', 'Ansonia', 'Berlin', 'Bloomfield', 'Branford', 'Bridgeport', 'Bristol', 'Coventry', 'Danbury', 'Darien', 'Derby', 'East Hartford', 'East Haven', 'Enfield', 'Fairfield', 'Farmington', 'Greenwich', 'Groton', 'Guilford', 'Hamden', 'Hartford', 'Lebanon', 'Litchfield', 'Manchester', 'Mansfield', 'Meriden', 'Middletown', 'Milford', 'Mystic', 'Naugatuck', 'New Britain', 'New Haven', 'New London', 'North Haven', 'Norwalk', 'Norwich', 'Old Saybrook', 'Orange', 'Seymour', 'Shelton', 'Simsbury', 'Southington', 'Stamford', 'Stonington', 'Stratford', 'Torrington', 'Wallingford', 'Waterbury', 'Waterford', 'Watertown', 'West Hartford', 'West Haven', 'Westport', 'Wethersfield', 'Willimantic', 'Windham', 'Windsor', 'Windsor Locks', 'Winsted', 'Delaware', 'Dover', 'Lewes', 'Milford', 'New Castle', 'Newark', 'Smyrna', 'Wilmington', 'Florida', 'Apalachicola', 'Bartow', 'Belle Glade', 'Boca Raton', 'Bradenton', 'Cape Coral', 'Clearwater', 'Cocoa Beach', 'Cocoa-Rockledge', 'Coral Gables', 'Daytona Beach', 'De Land', 'Deerfield Beach', 'Delray Beach', 'Fernandina Beach', 'Fort Lauderdale', 'Fort Myers', 'Fort Pierce', 'Fort Walton Beach', 'Gainesville', 'Hallandale Beach', 'Hialeah', 'Hollywood', 'Homestead', 'Jacksonville', 'Key West', 'Lake City', 'Lake Wales', 'Lakeland', 'Largo', 'Melbourne', 'Miami', 'Miami Beach', 'Naples', 'New Smyrna Beach', 'Ocala', 'Orlando', 'Ormond Beach', 'Palatka', 'Palm Bay', 'Palm Beach', 'Panama City', 'Pensacola', 'Pompano Beach', 'Saint Augustine', 'Saint Petersburg', 'Sanford', 'Sarasota', 'Sebring', 'Tallahassee', 'Tampa', 'Tarpon Springs', 'Titusville', 'Venice', 'West Palm Beach', 'White Springs', 'Winter Haven', 'Winter Park', 'Georgia', 'Albany', 'Americus', 'Andersonville', 'Athens', 'Atlanta', 'Augusta', 'Bainbridge', 'Blairsville', 'Brunswick', 'Calhoun', 'Carrollton', 'Columbus', 'Dahlonega', 'Dalton', 'Darien', 'Decatur', 'Douglas', 'East Point', 'Fitzgerald', 'Fort Valley', 'Gainesville', 'La Grange', 'Macon', 'Marietta', 'Milledgeville', 'Plains', 'Rome', 'Savannah', 'Toccoa', 'Valdosta', 'Warm Springs', 'Warner Robins', 'Washington', 'Waycross', 'Hawaii', 'Hanalei', 'Hilo', 'Honaunau', 'Honolulu', 'Kahului', 'Kaneohe', 'Kapaa', 'Kawaihae', 'Lahaina', 'Laie', 'Wahiawa', 'Wailuku', 'Waimea', 'Idaho', 'Blackfoot', 'Boise', 'Bonners Ferry', 'Caldwell', 'Coeur d’Alene', 'Idaho City', 'Idaho Falls', 'Kellogg', 'Lewiston', 'Moscow', 'Nampa', 'Pocatello', 'Priest River', 'Rexburg', 'Sun Valley', 'Twin Falls', 'Illinois', 'Alton', 'Arlington Heights', 'Arthur', 'Aurora', 'Belleville', 'Belvidere', 'Bloomington', 'Brookfield', 'Cahokia', 'Cairo', 'Calumet City', 'Canton', 'Carbondale', 'Carlinville', 'Carthage', 'Centralia', 'Champaign', 'Charleston', 'Chester', 'Chicago', 'Chicago Heights', 'Cicero', 'Collinsville', 'Danville', 'Decatur', 'DeKalb', 'Des Plaines', 'Dixon', 'East Moline', 'East Saint Louis', 'Effingham', 'Elgin', 'Elmhurst', 'Evanston', 'Freeport', 'Galena', 'Galesburg', 'Glen Ellyn', 'Glenview', 'Granite City', 'Harrisburg', 'Herrin', 'Highland Park', 'Jacksonville', 'Joliet', 'Kankakee', 'Kaskaskia', 'Kewanee', 'La Salle', 'Lake Forest', 'Libertyville', 'Lincoln', 'Lisle', 'Lombard', 'Macomb', 'Mattoon', 'Moline', 'Monmouth', 'Mount Vernon', 'Mundelein', 'Naperville', 'Nauvoo', 'Normal', 'North Chicago', 'Oak Park', 'Oregon', 'Ottawa', 'Palatine', 'Park Forest', 'Park Ridge', 'Pekin', 'Peoria', 'Petersburg', 'Pontiac', 'Quincy', 'Rantoul', 'River Forest', 'Rock Island', 'Rockford', 'Salem', 'Shawneetown', 'Skokie', 'South Holland', 'Springfield', 'Streator', 'Summit', 'Urbana', 'Vandalia', 'Virden', 'Waukegan', 'Wheaton', 'Wilmette', 'Winnetka', 'Wood River', 'Zion', 'Indiana', 'Anderson', 'Bedford', 'Bloomington', 'Columbus', 'Connersville', 'Corydon', 'Crawfordsville', 'East Chicago', 'Elkhart', 'Elwood', 'Evansville', 'Fort Wayne', 'French Lick', 'Gary', 'Geneva', 'Goshen', 'Greenfield', 'Hammond', 'Hobart', 'Huntington', 'Indianapolis', 'Jeffersonville', 'Kokomo', 'Lafayette', 'Madison', 'Marion', 'Michigan City', 'Mishawaka', 'Muncie', 'Nappanee', 'Nashville', 'New Albany', 'New Castle', 'New Harmony', 'Peru', 'Plymouth', 'Richmond', 'Santa Claus', 'Shelbyville', 'South Bend', 'Terre Haute', 'Valparaiso', 'Vincennes', 'Wabash', 'West Lafayette', 'Iowa', 'Amana Colonies', 'Ames', 'Boone', 'Burlington', 'Cedar Falls', 'Cedar Rapids', 'Charles City', 'Cherokee', 'Clinton', 'Council Bluffs', 'Davenport', 'Des Moines', 'Dubuque', 'Estherville', 'Fairfield', 'Fort Dodge', 'Grinnell', 'Indianola', 'Iowa City', 'Keokuk', 'Mason City', 'Mount Pleasant', 'Muscatine', 'Newton', 'Oskaloosa', 'Ottumwa', 'Sioux City', 'Waterloo', 'Webster City', 'West Des Moines', 'Kansas', 'Abilene', 'Arkansas City', 'Atchison', 'Chanute', 'Coffeyville', 'Council Grove', 'Dodge City', 'Emporia', 'Fort Scott', 'Garden City', 'Great Bend', 'Hays', 'Hutchinson', 'Independence', 'Junction City', 'Kansas City', 'Lawrence', 'Leavenworth', 'Liberal', 'Manhattan', 'McPherson', 'Medicine Lodge', 'Newton', 'Olathe', 'Osawatomie', 'Ottawa', 'Overland Park', 'Pittsburg', 'Salina', 'Shawnee', 'Smith Center', 'Topeka', 'Wichita', 'Kentucky', 'Ashland', 'Barbourville', 'Bardstown', 'Berea', 'Boonesborough', 'Bowling Green', 'Campbellsville', 'Covington', 'Danville', 'Elizabethtown', 'Frankfort', 'Harlan', 'Harrodsburg', 'Hazard', 'Henderson', 'Hodgenville', 'Hopkinsville', 'Lexington', 'Louisville', 'Mayfield', 'Maysville', 'Middlesboro', 'Newport', 'Owensboro', 'Paducah', 'Paris', 'Richmond', 'Louisiana', 'Abbeville', 'Alexandria', 'Bastrop', 'Baton Rouge', 'Bogalusa', 'Bossier City', 'Gretna', 'Houma', 'Lafayette', 'Lake Charles', 'Monroe', 'Morgan City', 'Natchitoches', 'New Iberia', 'New Orleans', 'Opelousas', 'Ruston', 'Saint Martinville', 'Shreveport', 'Thibodaux', 'Maine', 'Auburn', 'Augusta', 'Bangor', 'Bar Harbor', 'Bath', 'Belfast', 'Biddeford', 'Boothbay Harbor', 'Brunswick', 'Calais', 'Caribou', 'Castine', 'Eastport', 'Ellsworth', 'Farmington', 'Fort Kent', 'Gardiner', 'Houlton', 'Kennebunkport', 'Kittery', 'Lewiston', 'Lubec', 'Machias', 'Orono', 'Portland', 'Presque Isle', 'Rockland', 'Rumford', 'Saco', 'Scarborough', 'Waterville', 'York', 'Maryland', 'Aberdeen', 'Annapolis', 'Baltimore', 'Bethesda-Chevy Chase', 'Bowie', 'Cambridge', 'Catonsville', 'College Park', 'Columbia', 'Cumberland', 'Easton', 'Elkton', 'Emmitsburg', 'Frederick', 'Greenbelt', 'Hagerstown', 'Hyattsville', 'Laurel', 'Oakland', 'Ocean City', 'Rockville', 'Saint Marys City', 'Salisbury', 'Silver Spring', 'Takoma Park', 'Towson', 'Westminster', 'Massachusetts', 'Abington', 'Adams', 'Amesbury', 'Amherst', 'Andover', 'Arlington', 'Athol', 'Attleboro', 'Barnstable', 'Bedford', 'Beverly', 'Boston', 'Bourne', 'Braintree', 'Brockton', 'Brookline', 'Cambridge', 'Canton', 'Charlestown', 'Chelmsford', 'Chelsea', 'Chicopee', 'Clinton', 'Cohasset', 'Concord', 'Danvers', 'Dartmouth', 'Dedham', 'Dennis', 'Duxbury', 'Eastham', 'Edgartown', 'Everett', 'Fairhaven', 'Fall River', 'Falmouth', 'Fitchburg', 'Framingham', 'Gloucester', 'Great Barrington', 'Greenfield', 'Groton', 'Harwich', 'Haverhill', 'Hingham', 'Holyoke', 'Hyannis', 'Ipswich', 'Lawrence', 'Lenox', 'Leominster', 'Lexington', 'Lowell', 'Ludlow', 'Lynn', 'Malden', 'Marblehead', 'Marlborough', 'Medford', 'Milton', 'Nahant', 'Natick', 'New Bedford', 'Newburyport', 'Newton', 'North Adams', 'Northampton', 'Norton', 'Norwood', 'Peabody', 'Pittsfield', 'Plymouth', 'Provincetown', 'Quincy', 'Randolph', 'Revere', 'Salem', 'Sandwich', 'Saugus', 'Somerville', 'South Hadley', 'Springfield', 'Stockbridge', 'Stoughton', 'Sturbridge', 'Sudbury', 'Taunton', 'Tewksbury', 'Truro', 'Watertown', 'Webster', 'Wellesley', 'Wellfleet', 'West Bridgewater', 'West Springfield', 'Westfield', 'Weymouth', 'Whitman', 'Williamstown', 'Woburn', 'Woods Hole', 'Worcester', 'Michigan', 'Adrian', 'Alma', 'Ann Arbor', 'Battle Creek', 'Bay City', 'Benton Harbor', 'Bloomfield Hills', 'Cadillac', 'Charlevoix', 'Cheboygan', 'Dearborn', 'Detroit', 'East Lansing', 'Eastpointe', 'Ecorse', 'Escanaba', 'Flint', 'Grand Haven', 'Grand Rapids', 'Grayling', 'Grosse Pointe', 'Hancock', 'Highland Park', 'Holland', 'Houghton', 'Interlochen', 'Iron Mountain', 'Ironwood', 'Ishpeming', 'Jackson', 'Kalamazoo', 'Lansing', 'Livonia', 'Ludington', 'Mackinaw City', 'Manistee', 'Marquette', 'Menominee', 'Midland', 'Monroe', 'Mount Clemens', 'Mount Pleasant', 'Muskegon', 'Niles', 'Petoskey', 'Pontiac', 'Port Huron', 'Royal Oak', 'Saginaw', 'Saint Ignace', 'Saint Joseph', 'Sault Sainte Marie', 'Traverse City', 'Trenton', 'Warren', 'Wyandotte', 'Ypsilanti', 'Minnesota', 'Albert Lea', 'Alexandria', 'Austin', 'Bemidji', 'Bloomington', 'Brainerd', 'Crookston', 'Duluth', 'Ely', 'Eveleth', 'Faribault', 'Fergus Falls', 'Hastings', 'Hibbing', 'International Falls', 'Little Falls', 'Mankato', 'Minneapolis', 'Moorhead', 'New Ulm', 'Northfield', 'Owatonna', 'Pipestone', 'Red Wing', 'Rochester', 'Saint Cloud', 'Saint Paul', 'Sauk Centre', 'South Saint Paul', 'Stillwater', 'Virginia', 'Willmar', 'Winona', 'Mississippi', 'Bay Saint Louis', 'Biloxi', 'Canton', 'Clarksdale', 'Columbia', 'Columbus', 'Corinth', 'Greenville', 'Greenwood', 'Grenada', 'Gulfport', 'Hattiesburg', 'Holly Springs', 'Jackson', 'Laurel', 'Meridian', 'Natchez', 'Ocean Springs', 'Oxford', 'Pascagoula', 'Pass Christian', 'Philadelphia', 'Port Gibson', 'Starkville', 'Tupelo', 'Vicksburg', 'West Point', 'Yazoo City', 'Missouri', 'Boonville', 'Branson', 'Cape Girardeau', 'Carthage', 'Chillicothe', 'Clayton', 'Columbia', 'Excelsior Springs', 'Ferguson', 'Florissant', 'Fulton', 'Hannibal', 'Independence', 'Jefferson City', 'Joplin', 'Kansas City', 'Kirksville', 'Lamar', 'Lebanon', 'Lexington', 'Maryville', 'Mexico', 'Monett', 'Neosho', 'New Madrid', 'Rolla', 'Saint Charles', 'Saint Joseph', 'Saint Louis', 'Sainte Genevieve', 'Salem', 'Sedalia', 'Springfield', 'Warrensburg', 'West Plains', 'Montana', 'Anaconda', 'Billings', 'Bozeman', 'Butte', 'Dillon', 'Fort Benton', 'Glendive', 'Great Falls', 'Havre', 'Helena', 'Kalispell', 'Lewistown', 'Livingston', 'Miles City', 'Missoula', 'Virginia City', 'Nebraska', 'Beatrice', 'Bellevue', 'Boys Town', 'Chadron', 'Columbus', 'Fremont', 'Grand Island', 'Hastings', 'Kearney', 'Lincoln', 'McCook', 'Minden', 'Nebraska City', 'Norfolk', 'North Platte', 'Omaha', 'Plattsmouth', 'Red Cloud', 'Sidney', 'Nevada', 'Boulder City', 'Carson City', 'Elko', 'Ely', 'Fallon', 'Genoa', 'Goldfield', 'Henderson', 'Las Vegas', 'North Las Vegas', 'Reno', 'Sparks', 'Virginia City', 'Winnemucca', 'New Hampshire', 'Berlin', 'Claremont', 'Concord', 'Derry', 'Dover', 'Durham', 'Exeter', 'Franklin', 'Hanover', 'Hillsborough', 'Keene', 'Laconia', 'Lebanon', 'Manchester', 'Nashua', 'Peterborough', 'Plymouth', 'Portsmouth', 'Rochester', 'Salem', 'Somersworth', 'New Jersey', 'Asbury Park', 'Atlantic City', 'Bayonne', 'Bloomfield', 'Bordentown', 'Bound Brook', 'Bridgeton', 'Burlington', 'Caldwell', 'Camden', 'Cape May', 'Clifton', 'Cranford', 'East Orange', 'Edison', 'Elizabeth', 'Englewood', 'Fort Lee', 'Glassboro', 'Hackensack', 'Haddonfield', 'Hoboken', 'Irvington', 'Jersey City', 'Lakehurst', 'Lakewood', 'Long Beach', 'Long Branch', 'Madison', 'Menlo Park', 'Millburn', 'Millville', 'Montclair', 'Morristown', 'Mount Holly', 'New Brunswick', 'New Milford', 'Newark', 'Ocean City', 'Orange', 'Parsippany–Troy Hills', 'Passaic', 'Paterson', 'Perth Amboy', 'Plainfield', 'Princeton', 'Ridgewood', 'Roselle', 'Rutherford', 'Salem', 'Somerville', 'South Orange Village', 'Totowa', 'Trenton', 'Union', 'Union City', 'Vineland', 'Wayne', 'Weehawken', 'West New York', 'West Orange', 'Willingboro', 'Woodbridge', 'New Mexico', 'Acoma', 'Alamogordo', 'Albuquerque', 'Artesia', 'Belen', 'Carlsbad', 'Clovis', 'Deming', 'Farmington', 'Gallup', 'Grants', 'Hobbs', 'Las Cruces', 'Las Vegas', 'Los Alamos', 'Lovington', 'Portales', 'Raton', 'Roswell', 'Santa Fe', 'Shiprock', 'Silver City', 'Socorro', 'Taos', 'Truth or Consequences', 'Tucumcari', 'New York', 'Albany', 'Amsterdam', 'Auburn', 'Babylon', 'Batavia', 'Beacon', 'Bedford', 'Binghamton', 'Bronx', 'Brooklyn', 'Buffalo', 'Chautauqua', 'Cheektowaga', 'Clinton', 'Cohoes', 'Coney Island', 'Cooperstown', 'Corning', 'Cortland', 'Crown Point', 'Dunkirk', 'East Aurora', 'East Hampton', 'Eastchester', 'Elmira', 'Flushing', 'Forest Hills', 'Fredonia', 'Garden City', 'Geneva', 'Glens Falls', 'Gloversville', 'Great Neck', 'Hammondsport', 'Harlem', 'Hempstead', 'Herkimer', 'Hudson', 'Huntington', 'Hyde Park', 'Ilion', 'Ithaca', 'Jamestown', 'Johnstown', 'Kingston', 'Lackawanna', 'Lake Placid', 'Levittown', 'Lockport', 'Mamaroneck', 'Manhattan', 'Massena', 'Middletown', 'Mineola', 'Mount Vernon', 'New Paltz', 'New Rochelle', 'New Windsor', 'New York City', 'Newburgh', 'Niagara Falls', 'North Hempstead', 'Nyack', 'Ogdensburg', 'Olean', 'Oneida', 'Oneonta', 'Ossining', 'Oswego', 'Oyster Bay', 'Palmyra', 'Peekskill', 'Plattsburgh', 'Port Washington', 'Potsdam', 'Poughkeepsie', 'Queens', 'Rensselaer', 'Rochester', 'Rome', 'Rotterdam', 'Rye', 'Sag Harbor', 'Saranac Lake', 'Saratoga Springs', 'Scarsdale', 'Schenectady', 'Seneca Falls', 'Southampton', 'Staten Island', 'Stony Brook', 'Stony Point', 'Syracuse', 'Tarrytown', 'Ticonderoga', 'Tonawanda', 'Troy', 'Utica', 'Watertown', 'Watervliet', 'Watkins Glen', 'West Seneca', 'White Plains', 'Woodstock', 'Yonkers', 'North Carolina', 'Asheboro', 'Asheville', 'Bath', 'Beaufort', 'Boone', 'Burlington', 'Chapel Hill', 'Charlotte', 'Concord', 'Durham', 'Edenton', 'Elizabeth City', 'Fayetteville', 'Gastonia', 'Goldsboro', 'Greensboro', 'Greenville', 'Halifax', 'Henderson', 'Hickory', 'High Point', 'Hillsborough', 'Jacksonville', 'Kinston', 'Kitty Hawk', 'Lumberton', 'Morehead City', 'Morganton', 'Nags Head', 'New Bern', 'Pinehurst', 'Raleigh', 'Rocky Mount', 'Salisbury', 'Shelby', 'Washington', 'Wilmington', 'Wilson', 'Winston-Salem', 'North Dakota', 'Bismarck', 'Devils Lake', 'Dickinson', 'Fargo', 'Grand Forks', 'Jamestown', 'Mandan', 'Minot', 'Rugby', 'Valley City', 'Wahpeton', 'Williston', 'Ohio', 'Akron', 'Alliance', 'Ashtabula', 'Athens', 'Barberton', 'Bedford', 'Bellefontaine', 'Bowling Green', 'Canton', 'Chillicothe', 'Cincinnati', 'Cleveland', 'Cleveland Heights', 'Columbus', 'Conneaut', 'Cuyahoga Falls', 'Dayton', 'Defiance', 'Delaware', 'East Cleveland', 'East Liverpool', 'Elyria', 'Euclid', 'Findlay', 'Gallipolis', 'Greenville', 'Hamilton', 'Kent', 'Kettering', 'Lakewood', 'Lancaster', 'Lima', 'Lorain', 'Mansfield', 'Marietta', 'Marion', 'Martins Ferry', 'Massillon', 'Mentor', 'Middletown', 'Milan', 'Mount Vernon', 'New Philadelphia', 'Newark', 'Niles', 'North College Hill', 'Norwalk', 'Oberlin', 'Painesville', 'Parma', 'Piqua', 'Portsmouth', 'Put-in-Bay', 'Salem', 'Sandusky', 'Shaker Heights', 'Springfield', 'Steubenville', 'Tiffin', 'Toledo', 'Urbana', 'Warren', 'Wooster', 'Worthington', 'Xenia', 'Yellow Springs', 'Youngstown', 'Zanesville', 'Oklahoma', 'Ada', 'Altus', 'Alva', 'Anadarko', 'Ardmore', 'Bartlesville', 'Bethany', 'Chickasha', 'Claremore', 'Clinton', 'Cushing', 'Duncan', 'Durant', 'Edmond', 'El Reno', 'Elk City', 'Enid', 'Eufaula', 'Frederick', 'Guthrie', 'Guymon', 'Hobart', 'Holdenville', 'Hugo', 'Lawton', 'McAlester', 'Miami', 'Midwest City', 'Moore', 'Muskogee', 'Norman', 'Oklahoma City', 'Okmulgee', 'Pauls Valley', 'Pawhuska', 'Perry', 'Ponca City', 'Pryor', 'Sallisaw', 'Sand Springs', 'Sapulpa', 'Seminole', 'Shawnee', 'Stillwater', 'Tahlequah', 'The Village', 'Tulsa', 'Vinita', 'Wewoka', 'Woodward', 'Oregon', 'Albany', 'Ashland', 'Astoria', 'Baker City', 'Beaverton', 'Bend', 'Brookings', 'Burns', 'Coos Bay', 'Corvallis', 'Eugene', 'Grants Pass', 'Hillsboro', 'Hood River', 'Jacksonville', 'John Day', 'Klamath Falls', 'La Grande', 'Lake Oswego', 'Lakeview', 'McMinnville', 'Medford', 'Newberg', 'Newport', 'Ontario', 'Oregon City', 'Pendleton', 'Port Orford', 'Portland', 'Prineville', 'Redmond', 'Reedsport', 'Roseburg', 'Salem', 'Seaside', 'Springfield', 'The Dalles', 'Tillamook', 'Pennsylvania', 'Abington', 'Aliquippa', 'Allentown', 'Altoona', 'Ambridge', 'Bedford', 'Bethlehem', 'Bloomsburg', 'Bradford', 'Bristol', 'Carbondale', 'Carlisle', 'Chambersburg', 'Chester', 'Columbia', 'Easton', 'Erie', 'Franklin', 'Germantown', 'Gettysburg', 'Greensburg', 'Hanover', 'Harmony', 'Harrisburg', 'Hazleton', 'Hershey', 'Homestead', 'Honesdale', 'Indiana', 'Jeannette', 'Jim Thorpe', 'Johnstown', 'Lancaster', 'Lebanon', 'Levittown', 'Lewistown', 'Lock Haven', 'Lower Southampton', 'McKeesport', 'Meadville', 'Middletown', 'Monroeville', 'Nanticoke', 'New Castle', 'New Hope', 'New Kensington', 'Norristown', 'Oil City', 'Philadelphia', 'Phoenixville', 'Pittsburgh', 'Pottstown', 'Pottsville', 'Reading', 'Scranton', 'Shamokin', 'Sharon', 'State College', 'Stroudsburg', 'Sunbury', 'Swarthmore', 'Tamaqua', 'Titusville', 'Uniontown', 'Warren', 'Washington', 'West Chester', 'Wilkes-Barre', 'Williamsport', 'York', 'Rhode Island', 'Barrington', 'Bristol', 'Central Falls', 'Cranston', 'East Greenwich', 'East Providence', 'Kingston', 'Middletown', 'Narragansett', 'Newport', 'North Kingstown', 'Pawtucket', 'Portsmouth', 'Providence', 'South Kingstown', 'Tiverton', 'Warren', 'Warwick', 'Westerly', 'Wickford', 'Woonsocket', 'South Carolina', 'Abbeville', 'Aiken', 'Anderson', 'Beaufort', 'Camden', 'Charleston', 'Columbia', 'Darlington', 'Florence', 'Gaffney', 'Georgetown', 'Greenville', 'Greenwood', 'Hartsville', 'Lancaster', 'Mount Pleasant', 'Myrtle Beach', 'Orangeburg', 'Rock Hill', 'Spartanburg', 'Sumter', 'Union', 'South Dakota', 'Aberdeen', 'Belle Fourche', 'Brookings', 'Canton', 'Custer', 'De Smet', 'Deadwood', 'Hot Springs', 'Huron', 'Lead', 'Madison', 'Milbank', 'Mitchell', 'Mobridge', 'Pierre', 'Rapid City', 'Sioux Falls', 'Spearfish', 'Sturgis', 'Vermillion', 'Watertown', 'Yankton', 'Tennessee', 'Alcoa', 'Athens', 'Chattanooga', 'Clarksville', 'Cleveland', 'Columbia', 'Cookeville', 'Dayton', 'Elizabethton', 'Franklin', 'Gallatin', 'Gatlinburg', 'Greeneville', 'Jackson', 'Johnson City', 'Jonesborough', 'Kingsport', 'Knoxville', 'Lebanon', 'Maryville', 'Memphis', 'Morristown', 'Murfreesboro', 'Nashville', 'Norris', 'Oak Ridge', 'Shelbyville', 'Tullahoma', 'Texas', 'Abilene', 'Alpine', 'Amarillo', 'Arlington', 'Austin', 'Baytown', 'Beaumont', 'Big Spring', 'Borger', 'Brownsville', 'Bryan', 'Canyon', 'Cleburne', 'College Station', 'Corpus Christi', 'Crystal City', 'Dallas', 'Del Rio', 'Denison', 'Denton', 'Eagle Pass', 'Edinburg', 'El Paso', 'Fort Worth', 'Freeport', 'Galveston', 'Garland', 'Goliad', 'Greenville', 'Harlingen', 'Houston', 'Huntsville', 'Irving', 'Johnson City', 'Kilgore', 'Killeen', 'Kingsville', 'Laredo', 'Longview', 'Lubbock', 'Lufkin', 'Marshall', 'McAllen', 'McKinney', 'Mesquite', 'Midland', 'Mission', 'Nacogdoches', 'New Braunfels', 'Odessa', 'Orange', 'Pampa', 'Paris', 'Pasadena', 'Pecos', 'Pharr', 'Plainview', 'Plano', 'Port Arthur', 'Port Lavaca', 'Richardson', 'San Angelo', 'San Antonio', 'San Felipe', 'San Marcos', 'Sherman', 'Sweetwater', 'Temple', 'Texarkana', 'Texas City', 'Tyler', 'Uvalde', 'Victoria', 'Waco', 'Weatherford', 'Wichita Falls', 'Ysleta', 'Utah', 'Alta', 'American Fork', 'Bountiful', 'Brigham City', 'Cedar City', 'Clearfield', 'Delta', 'Fillmore', 'Green River', 'Heber City', 'Kanab', 'Layton', 'Lehi', 'Logan', 'Manti', 'Moab', 'Monticello', 'Murray', 'Nephi', 'Ogden', 'Orderville', 'Orem', 'Panguitch', 'Park City', 'Payson', 'Price', 'Provo', 'Saint George', 'Salt Lake City', 'Spanish Fork', 'Springville', 'Tooele', 'Vernal', 'Vermont', 'Barre', 'Bellows Falls', 'Bennington', 'Brattleboro', 'Burlington', 'Essex', 'Manchester', 'Middlebury', 'Montpelier', 'Newport', 'Plymouth', 'Rutland', 'Saint Albans', 'Saint Johnsbury', 'Sharon', 'Winooski', 'Virginia', 'Abingdon', 'Alexandria', 'Bristol', 'Charlottesville', 'Chesapeake', 'Danville', 'Fairfax', 'Falls Church', 'Fredericksburg', 'Hampton', 'Hanover', 'Hopewell', 'Lexington', 'Lynchburg', 'Manassas', 'Martinsville', 'New Market', 'Newport News', 'Norfolk', 'Petersburg', 'Portsmouth', 'Reston', 'Richmond', 'Roanoke', 'Staunton', 'Suffolk', 'Virginia Beach', 'Waynesboro', 'Williamsburg', 'Winchester', 'Washington', 'Aberdeen', 'Anacortes', 'Auburn', 'Bellevue', 'Bellingham', 'Bremerton', 'Centralia', 'Coulee Dam', 'Coupeville', 'Ellensburg', 'Ephrata', 'Everett', 'Hoquiam', 'Kelso', 'Kennewick', 'Longview', 'Moses Lake', 'Oak Harbor', 'Olympia', 'Pasco', 'Point Roberts', 'Port Angeles', 'Pullman', 'Puyallup', 'Redmond', 'Renton', 'Richland', 'Seattle', 'Spokane', 'Tacoma', 'Vancouver', 'Walla Walla', 'Wenatchee', 'Yakima', 'West Virginia', 'Bath', 'Beckley', 'Bluefield', 'Buckhannon', 'Charles Town', 'Charleston', 'Clarksburg', 'Elkins', 'Fairmont', 'Grafton', 'Harpers Ferry', 'Hillsboro', 'Hinton', 'Huntington', 'Keyser', 'Lewisburg', 'Logan', 'Martinsburg', 'Morgantown', 'Moundsville', 'New Martinsville', 'Parkersburg', 'Philippi', 'Point Pleasant', 'Princeton', 'Romney', 'Shepherdstown', 'South Charleston', 'Summersville', 'Weirton', 'Welch', 'Wellsburg', 'Weston', 'Wheeling', 'White Sulphur Springs', 'Williamson', 'Wisconsin', 'Appleton', 'Ashland', 'Baraboo', 'Belmont', 'Beloit', 'Eau Claire', 'Fond du Lac', 'Green Bay', 'Hayward', 'Janesville', 'Kenosha', 'La Crosse', 'Lake Geneva', 'Madison', 'Manitowoc', 'Marinette', 'Menasha', 'Milwaukee', 'Neenah', 'New Glarus', 'Oconto', 'Oshkosh', 'Peshtigo', 'Portage', 'Prairie du Chien', 'Racine', 'Rhinelander', 'Ripon', 'Sheboygan', 'Spring Green', 'Stevens Point', 'Sturgeon Bay', 'Superior', 'Waukesha', 'Wausau', 'Wauwatosa', 'West Allis', 'West Bend', 'Wisconsin Dells', 'Wyoming', 'Buffalo', 'Casper', 'Cheyenne', 'Cody', 'Douglas', 'Evanston', 'Gillette', 'Green River', 'Jackson', 'Lander', 'Laramie', 'Newcastle', 'Powell', 'Rawlins', 'Riverton', 'Rock Springs', 'Sheridan', 'Ten Sleep', 'Thermopolis', 'Torrington', 'Worland', 'A Coruña', 'Aachen', 'Aarhus', 'Abbeville', 'Aberdeen (UK)', 'Aberdeen (South Dakota)', 'Aberdeen (Washington)', 'Abidjan', 'Abilene', 'Abu Dhabi', 'Abuja', 'Acapulco', 'Accra', 'Adamstown', 'Addis Ababa', 'Adelaide', 'Adelboden', 'Agadir', 'Agde', 'Agen', 'Agios Nikolaos', 'Agra', 'Agrigento', 'Agropoli', 'Ahmedabad', 'Aigues-Mortes', 'Aix-en-Provence', 'Aix-les-Bains', 'Ajaccio', 'Ajman', 'Akron', 'Al Ain', 'Alanya', 'Alaró', 'Albacete', 'Albany', 'Albenga', 'Albi', 'Albufeira', 'Albuquerque', 'Alcudia', 'Aleppo', 'Alessandria', 'Ålesund', 'Alexandria (U.S.)', 'Alexandria (Egypt)', 'Algeciras', 'Alghero', 'Algiers', 'Alicante', 'Alkmaar', 'Allentown', 'Almaty', 'Alofi', "Alpe d'Huez", 'Alta Badia', 'Altea', 'Altoona', 'Amalfi', 'Amapala', 'Amarillo', 'Ambon', 'Amersfoort', 'Amiens', 'Amman', 'Amsterdam', 'Anaheim', 'Anchorage', 'Ancona', 'Andalo', 'Andermatt', 'Andorra la Vella', 'Andratx', 'Andria', 'Angeles City', 'Angers', 'Angoulême', 'Ankara', 'Ann Arbor', 'Anna Maria City', 'Annapolis', 'Annecy', 'Antalya', 'Antananarivo', 'Antibes', 'Antigua Guatemala', 'Antwerp', 'Anzio', 'Ao Nang', 'Aosta', 'Apeldoorn', 'Apia', 'Appleton', 'Aqaba', 'Aracaju', 'Arcachon', 'Arenzano', 'Arequipa', 'Arezzo', 'Argostoli', 'Arica', 'Arles', 'Arlington (Virginia)', 'Arlington (Texas)', 'Armagh', 'Arnhem', 'Arosa', 'Arras', 'Arrecife', 'Artà', 'Asbury Park', 'Ascoli Piceno', 'Ascona', 'Ashdod', 'Ashgabat', 'Ashkelon', 'Asmara', 'Aspen', 'Asti', 'Astoria', 'Asunción', 'Atafu', 'Athens', 'Athlone', 'Atlanta', 'Atlantic City', 'Auckland', 'Augsburg', 'Augusta (Georgia)', 'Augusta (Maine)', 'Aurora (Colorado)', 'Aurora (Illinois)', 'Austin', 'Auxerre', 'Avalon (California)', 'Avalon (New Jersey)', 'Avarua', 'Aveiro', 'Avellino', 'Avignon', 'Avila Beach', 'Avoriaz', 'Axamer Lizum', 'Ayia Napa', 'Azusa', 'Bad Gastein', 'Bad Hofgastein', 'Baden', 'Baghdad', 'Baiona', 'Bakersfield', 'Baku', 'Baltimore', 'Bamako', 'Banda Aceh', 'Bandar Seri Begawan', 'Bandol', 'Banff', 'Bangalore', 'Bangkok', 'Bangor', 'Bangui', 'Banjul', 'Bar', 'Bar Harbor', 'Barcelona', 'Bari', 'Barletta', 'Barrie', 'Barstow', 'Basel', 'Basey', 'Basseterre', 'Basse-Terre', 'Bastia', 'Bata', 'Batam', 'Bath', 'Baton Rouge', 'Batu', 'Batumi', 'Bayonne', 'Beaulieu-sur-Mer', 'Beaumont', 'Beaune', 'Beersheba', 'Beijing', 'Beirut', 'Belek', 'Belfast', 'Belfort', 'Belgrade', 'Belize City', 'Bellingham', 'Bellinzona', 'Belluno', 'Belmopan', 'Belo Horizonte', 'Bemidji', 'Benalmadena', 'Bend', 'Bendigo', 'Benevento', 'Benicàssim', 'Benidorm', 'Bergamo', 'Bergen', 'Bergerac', 'Berkeley', 'Berlin', 'Bern', 'Besançon', 'Bethlehem', 'Beverly Hills', 'Béziers', 'Biarritz', 'Biel/Bienne', 'Bielefeld', 'Biella', 'Big Pine Key', 'Bilbao', 'Billings', 'Biloxi', 'Birmingham (UK)', 'Birmingham (U.S.)', 'Bishkek', 'Bismarck', 'Bissau', 'Blanes', 'Bled', 'Blois', 'Bloomington', 'Blumenau', 'Boca Chica', 'Boca Grande', 'Boca Raton', 'Bochum', 'Bodrum', 'Bogotá', 'Boise', 'Bologna', 'Bolzano', 'Bonifacio', 'Bonn', 'Bordeaux', 'Bordighera', 'Bormio', 'Boston', 'Boulder', 'Boulogne-sur-Mer', 'Bourges', 'Bowling Green', 'Boynton Beach', 'Bozeman', 'Bradenton', 'Bradenton Beach', 'Bradford', 'Braga', 'Brampton', 'Brandon', 'Brantford', 'Brasilia', 'Bratislava', 'Braunschweig', 'Brazzaville', 'Breda', 'Bregenz', 'Brela', 'Bremen', 'Bremerhaven', 'Brescia', 'Brest', 'Briançon', 'Bridgeport', 'Bridgetown', 'Brighton', 'Brindisi', 'Brisbane', 'Bristol', 'Brixen', 'Brixental', 'Brno', 'Brookings', 'Brownsville', 'Bruges', 'Brunswick', 'Brussels', 'Bucharest', 'Budapest', 'Budva', 'Buenos Aires', 'Buffalo', 'Bujumbura', 'Bukittinggi', 'Burgas', 'Burlington (U.S.)', 'Burlington (Canada)', 'Burnt Pine', 'Butte', 'Cabo San Lucas', 'Cadaqués', 'Cádiz', 'Caen', 'Cagliari', 'Cagnes-sur-Mer', 'Cairns', 'Cairo', 'Cala Bona', "Cala d'Or", 'Cala Millor', 'Cala Ratjada', 'Calais', 'Calella', 'Calgary', 'Cali', 'Caloundra', 'Calp', 'Caltanissetta', 'Calvi', 'Cambridge (UK)', 'Cambridge (U.S.)', 'Cambrils', 'Camden', 'Campbell River', 'Campinas', 'Campobasso', 'Can Pastilla', 'Can Picafort', 'Canazei', 'Canberra', 'Cancun', 'Cannes', 'Cannon Beach', 'Canterbury', 'Canton', 'Canyamel', 'Capdepera', 'Cape Canaveral', 'Cape Coral', 'Cape May', 'Cape Town', 'Capitola', 'Captiva', 'Caracas', 'Carbonia', 'Carcassonne', 'Cardiff', 'Carlisle', 'Carlsbad', 'Carmel-by-the-Sea', 'Carpi', 'Carpinteria', 'Carrara', 'Carson City', 'Cartagena (Colombia)', 'Cartagena (Spain)', 'Casablanca', 'Caserta', 'Casper', 'Cassis', 'Castellón de la Plana', 'Castelrotto', 'Castletown', 'Castries', 'Catania', 'Catanzaro', 'Caxias do Sul', 'Cayenne', 'Cebu City', 'Cedar Key', 'Cedar Rapids', 'Celle', 'Cervinia', 'Cesena', 'Český Krumlov', 'Çeşme', 'Chamonix', 'Chandler', 'Chania', 'Charleroi', 'Charleston (West Virginia)', 'Charleston (South Carolina)', 'Charlestown', 'Charlotte', 'Charlotte Amalie', 'Charlottetown', 'Chartres', 'Chatham', 'Chattanooga', 'Chelmsford', 'Chemnitz', 'Chennai', 'Cherbourg', 'Chesapeake', 'Chester', 'Cheyenne', 'Chiang Mai', 'Chiang Rai', 'Chiavari', 'Chicago', 'Chichester', 'Chiclayo', 'Chieti', 'Chincoteague', 'Chioggia', 'Chios', 'Chișinău', 'Chokoloskee', 'Chonburi', 'Christchurch', 'Christiansted', 'Chula Vista', 'Chur', 'Cincinnati', 'Ciutadella de Menorca', 'Civitavecchia', 'Clarksville', 'Clearwater', 'Clearwater Beach', 'Clermont-Ferrand', 'Cleveland', 'Cockburn Town', 'Cocoa Beach', 'Coconut Creek', 'Coimbra', 'Collioure', 'Colmar', 'Cologne', 'Colombo', 'Colón', 'Colonia del Sacramento', 'Colorado Springs', 'Columbia (South Carolina)', 'Columbia (Missouri)', 'Columbus', 'Como', 'Conakry', 'Concepción', 'Concord', 'Conil de la Frontera', 'Conway', 'Copenhagen', 'Coral Springs', 'Córdoba (Argentina)', 'Córdoba (Spain)', 'Corfu', 'Corinth', 'Cork', 'Coro', 'Coron Town', 'Corpus Christi', 'Corralejo', "Cortina d'Ampezzo", 'Cosenza', 'Costa Adeje', 'Cotabato City', 'Cottbus', 'Courchevel', 'Courmayeur', 'Courtenay', 'Coventry', 'Covington', 'Coxen Hole', 'Coyhaique', 'Cozumel', 'Crans-Montana', 'Cremona', 'Crotone', 'Cruz Bay', 'Cudjoe Key', 'Cuenca (Ecuador)', 'Cuenca (Spain)', 'Cumaná', 'Cuneo', 'Cusco', 'Da Nang', 'Dachau', 'Dahab', 'Dakar', 'Dallas', 'Damascus', 'Dana Point', 'Dar es Salaam', 'Darien', 'Darmstadt', 'Darwin', 'Daugavpils', 'Dauphin Island', 'Davao City', 'Davenport', 'Davos', 'Dayton', 'Daytona Beach', 'Deauville', 'Decatur', 'Deerfield Beach', 'Del Mar', 'Delft', 'Delhi', 'Delray Beach', 'Den Bosch', 'Denia', 'Denpasar', 'Denton', 'Denver', 'Derby', 'Derry', 'Des Moines', 'Detroit', 'Dhaka', 'Didim', 'Dieppe', 'Dijon', 'Dili', 'Djibouti', 'Dodoma', 'Doha', 'Dolomiti Superski', 'Dordrecht', 'Dorfgastein', 'Dortmund', 'Dothan', 'Douala', 'Douglas', 'Dover (Delaware)', 'Dover (New Hampshire)', 'Dresden', 'Dubai', 'Dublin', 'Dubrovnik', 'Duisburg', 'Duluth', 'Dumaguete', 'Dumai', 'Duncan', 'Dundalk', 'Dundee', 'Dunedin', 'Dunkirk', 'Durham (UK)', 'Durham (U.S.)', 'Dushanbe', 'Düsseldorf', '', 'Eastbourne', 'Eau Claire', 'Edgartown', 'Edinburgh', 'Edmonton', 'Eilat', 'Eindhoven', 'El Nido', 'El Paso', 'Elche', 'Elizabeth', 'Elko', 'Ellmau', 'Elm', 'Empuriabrava', 'Encinitas', 'Engelberg', 'Englewood Beach', 'Enna', 'Enschede', 'Épinal', 'Erfurt', 'Erie', 'Erlangen', 'Esbjerg', 'Espace Killy', 'Essaouira', 'Essen', 'Estepona', 'Eugene', 'Eureka', 'Evansville', 'Everett', 'Everglades City', 'Exeter', 'Èze', 'Faenza', 'Fairbanks', 'Fakaofo', 'Falmouth', 'Famagusta', 'Fano', 'Fargo', 'Faro', 'Fayetteville (North Carolina)', 'Fayetteville (Arkansas)', 'Fermo', 'Fernandina Beach', 'Ferrara', 'Fethiye', 'Fez', 'Fieberbrunn', 'Filzmoos', 'Finale Ligure', 'Fisher Island', 'Fiumicino', 'Flagstaff', 'Flaine', 'Flint', 'Florence', 'Florence (Alabama)', 'Flores', 'Foggia', 'Folgarida', 'Fontana', 'Forlì', 'Fort Collins', 'Fort Lauderdale', 'Fort Myers', 'Fort Myers Beach', 'Fort Pierce', 'Fort Smith', 'Fort Wayne', 'Fort Worth', 'Fort-de-France', 'Forte dei Marmi', 'Foz do Iguaçu', 'Frankfort', 'Frankfurt am Main', 'Franklin', 'Frederick', 'Fredericton', 'Frederiksted', 'Freeport', 'Freetown', 'Freiburg', 'Fremont', 'Fresno', 'Fribourg', 'Frosinone', 'Fuengirola', 'Fujairah', 'Fukuoka', 'Funafuti', 'Funchal', 'Gaborone', 'Gainesville', 'Galtür', 'Galway', 'Gandia', 'Garden Grove', 'Garland', 'Gastonia', 'Gatineau', 'Gaza City', 'Gdansk', 'Gdynia', 'Geelong', 'Gelsenkirchen', 'Geneva', 'Genoa', 'George Town (Cayman Islands)', 'George Town (Malaysia)', 'Georgetown', 'Ghent', 'Gijón', 'Gilbert', 'Girona', 'Gitega', 'Giza', 'Glasgow', 'Glendale (Arizona)', 'Glendale (California)', 'Gloucester', 'Gold Coast', 'Gorizia', 'Gosau', 'Gothenburg', 'Göttingen', 'Gouda', 'Granada (Spain)', 'Granada (Nicaragua)', 'Grand Forks', 'Grand Island', 'Grand Junction', 'Grand Prairie', 'Grand Rapids', 'Grande Prairie', 'Granville', 'Grasse', 'Graz', 'Great Falls', 'Greeley', 'Green Bay', 'Greensboro', 'Greenville NC', 'Greenville SC', 'Grenoble', 'Grindelwald', 'Groningen', 'Grossarl', 'Grosseto', 'Grover Beach', 'Gstaad', 'Guadalajara', 'Guadalupe', 'Guangzhou', 'Guatemala City', 'Guayaquil', 'Guelph', 'Guimarães', 'Gulf Shores', 'Gulfport', 'Gustavia', 'Haarlem', 'Haifa', 'Half Moon Bay', 'Halifax', 'Halle', 'Hamburg', 'Hamilton (Bermuda)', 'Hamilton (Canada)', 'Hamilton (New Zealand)', 'Hampton', 'Hanford', 'Hangzhou', 'Hannover', 'Hanoi', 'Harare', 'Hargeisa', 'Harrisburg', 'Hartford', 'Hasselt', 'Hastings', 'Hat Yai', 'Hattiesburg', 'Havana', 'Heidelberg', 'Heilbronn', 'Heiligenblut', 'Helena', 'Helsinki', 'Henderson', 'Heraklion', 'Herceg Novi', 'Hereford', 'Hermosa Beach', 'Hervey Bay', 'Hialeah', 'Hillsboro', 'Hinterglemm', 'Hinterstoder', 'Hiroshima', 'Hoi An', 'Hobart', 'Ho Chi Minh City', 'Holbrook', 'Hollywood (Florida)', 'Holmes Beach', 'Honfleur', 'Hong Kong', 'Honiara', 'Honolulu', 'Horsens', 'Hot Springs', 'Houston', 'Hua Hin', 'Hue', 'Huntington', 'Huntington Beach', 'Huntsville', 'Hurghada', 'Hvar', 'Hyères', 'Ibiza Town', 'Iloilo City', 'Imola', 'Imperia', 'Inca', 'Indianapolis', 'Ingolstadt', 'Innsbruck', 'Interlaken', 'Inverness', 'Ioannina', 'Iqaluit', 'Iquitos', 'Irvine', 'Irving', 'Ischgl', 'Isernia', 'Lahore', 'Islamorada', 'Istanbul', 'İzmir', 'Izola', 'Jackson', 'Jackson (Tennessee)', 'Jacksonville', 'Jaipur', 'Jakarta', 'Jefferson City', 'Jekyll Island', 'Jena', 'Jerez de la Frontera', 'Jersey City', 'Jerusalem', 'Johannesburg', 'Johnson City', 'Joinville', 'Jonesboro', 'Juan Griego', 'Juan-les-Pins', 'Juba', 'Juiz de Fora', 'Juneau', 'Jungfrau', 'Jupiter', 'Jupiter Island', 'Jūrmala', 'Kabul', 'Kaiserslautern', 'Kalamata', 'Kalamazoo', 'Kamloops', 'Kampala', 'Kanchanaburi', 'Kansas City', 'Kansas City (Kansas)', 'Kappl', 'Kaprun', 'Islamabad', 'Karlovy Vary', 'Karlsruhe', 'Kassel', 'Kastoria', 'Kathmandu', 'Kaunas', 'Kavala', 'Kearney', 'Keene', 'Kelowna', 'Kemer', 'Kenosha', 'Key Biscayne', 'Key Largo', 'Key West', 'Khao Lak', 'Khartoum', 'Kiel', 'Kigali', 'Kilkenny', 'Kingman', 'Kingston (Jamaica)', 'Kingston (Norfolk Island)', 'Kingston (Canada)', 'Kingston upon Hull', 'Kingstown', 'Kinshasa', 'Kissimmee', 'Kitchener', 'Kitzbühel', 'Klagenfurt', 'Klaipėda', 'Knoxville', 'Kobe', 'Koblenz', 'Kolding', 'Kolkata', 'Komotini', 'Koper', 'Koror', 'Kos', 'Košice', 'Kotor', 'Krabi', 'Krakow', 'Kralendijk', 'Krefeld', 'Kuah', 'Kuala Lumpur', 'Kuşadası', 'Kuta', 'Kutná Hora', 'Kuwait City', 'Kyiv', 'Kyoto', 'Kyrenia', 'La Ceiba', 'La Ciotat', 'La Clusaz', 'La Laguna', 'La Maddalena', 'La Manga', 'La Paz', 'La Plagne', 'La Plata', 'La Rochelle', 'La Romana', 'La Serena', 'La Seyne-sur-Mer', 'La Spezia', 'La Thuile', 'Laax', 'Labasa', 'Labrador City', 'Labuan Bajo', 'Ladysmith', 'Lafayette (Indiana)', 'Lafayette (Louisiana)', 'Lagos (Nigeria)', 'Lagos (Portugal)', 'Laguna Beach', 'Karachi', 'Lakeland', 'Lalitpur', 'Lamezia Terme', 'Lancaster', 'Lancaster (U.S.)', 'Landshut', 'Lansing', "L'Aquila", 'Laredo', 'Largo', 'Larnaca', 'Las Cruces', 'Las Palmas', 'Las Vegas', 'Latina', 'Lausanne', 'Lautoka', 'Laval', 'Lawton', 'Layton', 'Le Havre', 'Le Lavandou', 'Le Mans', 'Le Puy-en-Velay', 'Lecce', 'Lecco', 'Lech', 'Leeds', 'Legian', 'Legnano', 'Leicester', 'Leiden', 'Leipzig', 'Lemgo', 'Leogang', 'León', 'Les Arcs', 'Les Deux Alpes', 'Les Gets', 'Les Houches', 'Les Menuires', 'Lethbridge', 'Leuven', 'Leverkusen', 'Lexington', 'Liberec', 'Libreville', 'Lichfield', 'Lido Key', 'Liège', 'Lienz', 'Liepāja', 'Lille', 'Lilongwe', 'Lima', 'Limassol', 'Limerick', 'Limoges', 'Lincoln', 'Lincoln', 'Lindos', 'Linz', 'Lisbon', 'Lisburn', 'Little Rock', 'Liverpool', 'Livigno', 'Livorno', 'Ljubljana', 'Lloret de Mar', 'Llucmajor', 'Loano', 'Locarno', 'Lodi', 'Lodz', 'Logan', 'Logroño', 'Lomé', 'London (Canada)', 'London (UK)', 'Londrina', 'Long Beach', 'Long Beach (New York)', 'Long Branch', 'Longboat Key', 'Longview (Texas)', 'Longview (Washington)', 'Lorain', 'Los Alamos', 'Los Angeles', 'Los Cabos', 'Los Cristianos', 'Louisville', 'Lourdes', 'Loutraki', 'Louvain-la-Neuve', 'Lowell', 'Luanda', 'Lubbock', 'Lübeck', 'Lublin', 'Lucca', 'Lucerne', 'Lugano', 'Luganville', 'Lund', 'Lusaka', 'Luxembourg', 'Luxor', 'Lyon', 'Maastricht', 'Macerata', 'Machu Picchu', 'Macon', 'Madera', 'Madison', 'Madonna di Campiglio', 'Madrid', 'Magaluf', 'Magdeburg', 'Mahón', 'Mainz', 'Majuro', 'Makarska', 'Malabo', 'Malaga', 'Malang', 'Maldonado', 'Malé', 'Malia', 'Malibu', 'Malmö', 'Manacor', 'Manado', 'Managua', 'Manama', 'Manchester (UK)', 'Manchester (U.S.)', 'Máncora', 'Mandalika', 'Manhattan Beach', 'Manhattan, KS', 'Manila', 'Mannheim', 'Manosque', 'Mantua', 'Maputo', 'Mar del Plata', 'Maracaibo', 'Marathon', 'Marbella', 'Marco Island', 'Maria Alm', 'Maribor', 'Marigot', 'Markham', 'Marmaris', 'Maroochydore', 'Marquette', 'Marrakesh', 'Marsa Alam', 'Marsala', 'Marseille', 'Martigues', 'Masaya', 'Maseru', 'Maspalomas', 'Massa', 'Mataram', 'Matera', 'Mayrhofen', 'Mazara del Vallo', 'Mbabane', 'McKinney', 'Mechelen', 'Medan', 'Medellín', 'Medford', 'Megève', 'Melbourne (Australia)', 'Melbourne (U.S.)', 'Memphis', 'Menton', 'Merano', 'Merced', 'Meribel', 'Mérida (Spain)', 'Mérida (Venezuela)', 'Meridian', 'Merritt Island', 'Mesa', 'Messina', 'Mestre', 'Metz', 'Mexico City', 'Miami', 'Middelburg', 'Midland', 'Mijas', 'Milan', 'Milford', 'Millau', 'Milwaukee', 'Mindelo', 'Minneapolis', 'Minot', 'Minsk', 'Miramar', 'Mishawaka', 'Mississauga', 'Missoula', 'Moab', 'Mobile', 'Modena', 'Modesto', 'Modica', 'Moena', 'Mogadishu', 'Mogi das Cruzes', 'Mombasa', 'Monaco City', 'Mönchengladbach', 'Moncton', 'Monrovia (Liberia)', 'Monrovia (U.S.)', 'Mons', 'Monschau', 'Monte Carlo', 'Monte Rosa', 'Montego Bay', 'Montepulciano', 'Monterey', 'Montevideo', 'Montgomery', 'Montluçon', 'Montpelier', 'Montpellier', 'Montreal', 'Montreux', 'Monza', 'Moose Jaw', 'Moraira', 'Moreno Valley', 'Morgantown', 'Moroni', 'Morro Bay', 'Morzine', 'Moscow', 'Mount Vernon', 'Mountain View', 'Moutier', 'Mulhouse', 'Mumbai', 'Munich', 'Münster', 'Murcia', 'Murfreesboro', 'Murter', 'Mykonos', 'Mytilene', 'Nadi', 'Nafplio', 'Nagoya', 'Nags Head', 'Nairobi', 'Namur', 'Nanaimo', 'Nancy', 'Nantes', 'Napa', 'Naples (Italy)', 'Naples (U.S.)', 'Narbonne', 'Narva', 'Nashua', 'Nashville', 'Nassau', 'Navarre Beach', 'Naxos', 'Nazareth', "N'Djamena", 'Negril', 'Neiafu', 'Nelson', 'Nerja', 'Netanya', 'Nevers', 'New Haven', 'New London', 'New Orleans', 'New Smyrna Beach', 'New York City', 'Newark', 'Newcastle (Australia)', 'Newcastle (UK)', 'Newport (UK)', 'Newport (Rhode Island)', 'Newport (Vermont)', 'Newport Beach', 'Newport News', 'Newry', 'Ngerulmud', 'Nha Trang', 'Niagara Falls (U.S.)', 'Niagara Falls (Canada)', 'Niamey', 'Nice', 'Nicosia', 'Nijmegen', 'Nimes', 'Niort', 'Noosa Heads', 'Norfolk', 'Normal', 'Norman', 'North Captiva Island', 'North Las Vegas', 'North Port', 'Norwalk', 'Norwich', 'Nottingham', 'Nouakchott', 'Novara', 'Novigrad', 'Nukuʻalofa', 'Nukunonu', 'Nuoro', 'Nürnberg', 'Nur-Sultan', 'Nusa Dua', 'Nuuk', 'Nyon', 'Oakland', 'Oakville', 'Oaxaca', 'Obergurgl', 'Oberhausen', 'Ocala', 'Ocean City', 'Ocean Grove', 'Oceanside', 'Ocho Rios', 'Odense', 'Odessa', 'Ogden', 'Oia', 'Okaloosa Island', 'Oklahoma City', 'Olbia', 'Oldenburg', 'Olomouc', 'Olympia', 'Omaha', 'Omoa', 'Opatija', 'Orange Beach', 'Oranjestad (Aruba)', 'Oranjestad (Sint Eustatius)', 'Orem', 'Oristano', 'Orlando', 'Orléans', 'Ortisei', 'Osaka', 'Oshawa', 'Oshkosh', 'Oslo', 'Osnabrück', 'Ostrava', 'Ottawa', 'Ouagadougou', 'Oulu', 'Ourense', 'Overland Park', 'Oviedo', 'Owensboro', 'Oxford', 'Oxnard', 'Pacific Grove', 'Padang', 'Paderborn', 'Padova', 'Pago Pago', 'Palanga', 'Palavas-les-Flots', 'Palembang', 'Palermo', 'Palikir', 'Palm Bay', 'Palm Beach', 'Palm Springs', 'Palma de Mallorca', 'Palma Nova', 'Palmetto', 'Palo Alto', 'Pamplona', 'Panama City (U.S.)', 'Panama City (Panama)', 'Paphos', 'Paradiski', 'Paralia', 'Paramaribo', 'Parikia', 'Paris', 'Parkersburg', 'Parksville', 'Parma', 'Pärnu', 'Pasadena', 'Passo del Tonale', 'Passo Rolle', 'Paterson', 'Patras', 'Pattaya', 'Pau', 'Pavia', 'Peel', 'Peguera', 'Pembroke Pines', 'Peniscola', 'Pensacola', 'Pensacola Beach', 'Peoria', 'Perast', 'Perdido Key', 'Périgueux', 'Perpignan', 'Perros-Guirec', 'Perth (Australia)', 'Perth (UK)', 'Perugia', 'Pesaro', 'Pescara', 'Pescasseroli', 'Petah Tikva', 'Peterborough', 'Petra', 'Petrovac', 'Pforzheim', 'Phang Nga', 'Phetchabun', 'Philadelphia', 'Philipsburg', 'Phoenix', 'Phuket City', 'Piacenza', 'Pierre', 'Pine Bluff', 'Piraeus', 'Piran', 'Pisa', 'Pistoia', 'Pittsburgh', 'Placencia', 'Plano', 'Playa Blanca', 'Playa de las Américas', 'Playa del Carmen', 'Pleasure Point', 'Plovdiv', 'Plymouth', 'Plzeň', 'Podgorica', 'Pointe-à-Pitre', 'Poitiers', 'Pollença', 'Pompano Beach', 'Pontevedra', 'Pordenone', 'Poreč', 'Porlamar', 'Port Alberni', 'Port Angeles', 'Port Charlotte', "Port d'Andratx", 'Port Louis', 'Port Moresby', 'Port of Spain', 'Port St. Lucie', 'Port Townsend', 'Port Vila', 'Port-au-Prince', 'Portimão', 'Portland (Oregon)', 'Portland (Maine)', 'Porto', 'Porto Cervo', 'Porto Cristo', 'Porto Torres', 'Portocolom', 'Portoferraio', 'Portofino', 'Porto-Novo', 'Portorož', 'Porto-Vecchio', 'Portsmouth (UK)', 'Portsmouth (U.S.)', 'Positano', 'Potenza', 'Potsdam', 'Poznan', 'Pozzuoli', 'Prague', 'Praia', 'Praia da Rocha', 'Prato', 'Prescott', 'Preston', 'Pretoria', 'Prince Albert', 'Prince George', 'Prince Rupert', 'Pristina', 'Propriano', 'Protaras', 'Providence', 'Provincetown', 'Provo', 'Pueblo', 'Puerto Baquerizo Moreno', 'Puerto Cortés', 'Puerto de la Cruz', 'Puerto la Cruz', 'Puerto Plata', 'Puerto Princesa', 'Puerto Rico de Gran Canaria', 'Puerto Vallarta', 'Pula', 'Punta Arenas', 'Punta Cana', 'Punta del Este', 'Punta Gorda', 'Pyeongchang', 'Pyongyang', 'Quarteira', 'Quebec', 'Quetzaltenango', 'Quezon City', 'Quimper', 'Quito', 'Rabat', 'Racine', 'Ragusa', 'Railay Beach', 'Raleigh', 'Ramallah', 'Ramsey', 'Rancho Cucamonga', 'Randers', 'Rapallo', 'Rapid City', 'Ras al-Khaimah', 'Ras Sedr', 'Ratingen', 'Ravello', 'Ravenna', 'Rayong', 'Reading', 'Red Deer', 'Redding', 'Redondo Beach', 'Regensburg', 'Reggio Calabria', 'Reggio Emilia', 'Regina', 'Rehovot', 'Reims', 'Rennes', 'Reno', 'Rethymno', 'Reus', 'Reutlingen', 'Reykjavik', 'Rhodes', 'Richmond', 'Rieti', 'Riga', 'Rijeka', 'Rimini', 'Rio de Janeiro', 'Riomaggiore', 'Rishon LeZion', 'Rivas', 'Riverside', 'Riviera Maya', 'Road Town', 'Roanoke', 'Rocamadour', 'Rochester (Minnesota)', 'Rochester (New York)', 'Rock Hill', 'Rockford', 'Rockville', 'Rodez', 'Rogers', 'Rome', 'Ronda', 'Rosario', 'Roseau', 'Roskilde', 'Rostock', 'Roswell', 'Rotterdam', 'Roubaix', 'Rouen', 'Rovigo', 'Rovinj', 'Rutland', 'Sa Coma', 'Sa Pobla', 'Saalbach', 'Saarbrücken', 'Saas-Fee', 'Sacramento', 'Safaga', 'Saguenay', 'Saint John', 'Saint Paul', 'Saint Petersburg', 'Saint-Brieuc', 'Sainte-Maxime', 'Saintes-Maries-de-la-Mer', 'Saint-Étienne', 'Saint-Jean-Cap-Ferrat', 'Saint-Jean-sur-Richelieu', 'Saint-Jérôme', 'Saint-Laurent-du-Maroni', 'Saint-Malo', 'Saint-Tropez', 'Salamanca', 'Salem (Oregon)', 'Salem (Massachusetts)', 'Salerno', 'Salinas', 'Salisbury', 'Salou', 'Salt Lake City', 'Salta', 'Salvador', 'Salzburg', 'Samaná', 'San Angelo', 'San Antonio', 'San Bernardino', 'San Clemente', 'San Cristóbal', 'San Diego', 'San Fernando', 'San Francisco', 'San José (Costa Rica)', 'San Jose (U.S.)', 'San Juan', 'San Juan del Sur', 'San Lorenzo', 'San Luis Obispo', 'San Marino', 'San Mateo', 'San Miguel', 'San Pedro', 'San Pedro de Atacama', 'San Pedro Sula', 'San Rafael', 'San Salvador', 'San Sebastián', 'Sanaa', 'Sanford', 'Sanibel Island', 'Sanremo', 'Sant Antoni de Portmany', 'Santa Ana (U.S.)', 'Santa Ana (El Salvador)', 'Santa Barbara', 'Santa Clara', 'Santa Clarita', 'Santa Cruz', 'Santa Cruz de la Sierra', 'Santa Cruz de Tenerife', 'Santa Eulària des Riu', 'Santa Fe', 'Santa Lucía', 'Santa Margherita Ligure', 'Santa Maria (Cape Verde)', 'Santa Maria (U.S.)', 'Santa Monica', 'Santa Pola', 'Santa Ponsa', 'Santa Rosa', 'Santa Tecla', 'Santander', 'Santanyí', 'Santiago (Chile)', 'Santiago (Dominican Rep.)', 'Santiago de Compostela', 'Santo Domingo', 'Sanur', 'Sao Paulo', 'São Tomé', 'Sapporo', 'Sarajevo', 'Sarasota', 'Saratoga Springs', "S'Arenal", 'Sariaya', 'Sarlat-la-Canéda', 'Saskatoon', 'Sassari', 'Sault Ste. Marie', 'Saumur', 'Savannah', 'Savona', 'Savusavu', 'Schaffhausen', 'Schenectady', 'Schladming', 'Scottsdale', 'Scranton', 'Sea Island', 'Sea Isle City', 'Seal Beach', 'Seaside', 'Seattle', 'Sedona', 'Seefeld', 'Segovia', 'Semarang', 'Seminyak', 'Seoul', 'Serre Chevalier', 'Sète', 'Seville', 'Shanghai', 'Sharjah', 'Sharm el-Sheikh', 'Sheffield', 'Shenzhen', 'Sherbrooke', 'Shreveport', 'Šiauliai', 'Šibenik', 'Side', 'Siegen', 'Siena', 'Siesta Key', 'Sineu', 'Singapore', 'Singaraja', 'Sion', 'Sioux City', 'Sioux Falls', 'Sitges', 'Skiathos', 'Skopje', 'Sofia', 'Sölden', 'Söll', 'Soller', 'Solothurn', 'Sondrio', 'Sopot', 'Sorocaba', 'Sorrento', 'South Bend', 'Southampton', 'Split', 'Spokane', 'Springdale', 'Springfield (Illinois)', 'Springfield (Massachusetts)', 'Springfield (Missouri)', 'Springfield (Oregon)', 'St Albans', "St George's (Bermuda)", 'St Pete Beach', 'St. Albans', 'St. Anton', 'St. Augustine', 'St. Catharines', 'St. Cloud', 'St. Gallen', 'St. George', 'St. George Island', "St. George's (Grenada)", "St. John's (Antigua and Barbuda)", "St. John's (Canada)", 'St. Louis', 'St. Moritz', 'St. Petersburg (U.S.)', 'St. Simons Island', 'Stamford', 'Stanley', 'Stavanger', 'Steinbach', 'Stillwater', 'Stirling', 'Stock Island', 'Stockholm', 'Stockton', 'Stoke-on-Trent', 'Stone Harbor', 'Strasbourg', 'Stuttgart', 'Sucre', 'Sudbury', 'Suez', 'Sukhothai', 'Sukhumi', 'Summerside', 'Sumter', 'Sunderland', 'Sunnyvale', 'Sunshine Coast', 'Superior', 'Surabaya', 'Surrey', 'Suva', 'Sveti Stefan', 'Swansea', 'Sydney (Australia)', 'Sydney (Canada)', 'Syracuse (Italy)', 'Syracuse (U.S.)', 'Szczecin', 'Taba', 'Tacloban', 'Tacoma', 'Tagbilaran', 'Taipei', 'Tallahassee', 'Tallinn', 'Tampa', 'Tampere', 'Tamworth', 'Tangier', 'Taormina', 'Taranto', 'Tarifa', 'Tarragona', 'Tartu', 'Tashkent', 'Tauplitz', 'Tauranga', 'Tavira', 'Tbilisi', 'Tegucigalpa', 'Tel Aviv', 'Temecula', 'Tempe', 'Teramo', 'Ternate', 'Terni', 'Texarkana AR', 'Texarkana TX', 'The Bottom', 'The Hague', 'The Valley', 'The Woodlands', 'Thessaloniki', 'Thimphu', 'Thunder Bay', 'Tignes', 'Tijuana', 'Tilburg', 'Timmins', 'Tinos', 'Tirana', 'Tivat', 'Tivoli', 'Tokyo', 'Toledo (Spain)', 'Toledo (U.S.)', 'Tooele', 'Toowoomba', 'Topeka', 'Toronto', 'Torre del Greco', 'Torre del Mar', 'Torremolinos', 'Torrevieja', 'Tórshavn', 'Toruń', 'Tossa de Mar', 'Toulon', 'Toulouse', 'Tours', 'Townsville', 'Trani', 'Trapani', 'Treasure Island', 'Trento', 'Trenton', 'Treviso', 'Trier', 'Trieste', 'Tripoli', 'Trogir', 'Trois-Rivières', 'Tromsø', 'Trondheim', 'Trouville-sur-Mer', 'Troy', 'Troyes', 'Trujillo', 'Tucson', 'Tui', 'Tulsa', 'Tulum', 'Turin', 'Turku', 'Tuscaloosa', 'Twin Falls', 'Two Harbors', 'Tybee Island', 'Tyler', 'Ubud', 'Udine', 'Udon Thani', 'Ukiah', 'Ulaanbaatar', 'Ulcinj', 'Ulm', 'Umag', 'Uppsala', 'Urbino', 'Urubamba', 'Ushuaia', 'Utica', 'Utrecht', 'Vaduz', 'Val d’Isère', 'Val di Fassa', 'Val Gardena', 'Val Thorens', 'Valence', 'Valencia (Spain)', 'Valencia (Venezuela)', 'Valladolid', 'Valldemossa', 'Valle Isarco', 'Valletta', 'Valparaíso', 'Vancouver (Canada)', 'Vancouver (U.S.)', 'Varazze', 'Varese', 'Varna', 'Vaughan', 'Vejle', 'Venice (Italy)', 'Venice (U.S.)', 'Ventimiglia', 'Ventspils', 'Ventura', 'Verbania', 'Verbier', 'Vercelli', 'Vero Beach', 'Verona', 'Versailles', 'Vevey', 'Viareggio', 'Vibo Valentia', 'Viborg', 'Vicenza', 'Vichy', 'Victoria (Canada)', 'Victoria (Seychelles)', 'Victorville', 'Vienna', 'Vigan', 'Vigo', 'Vilamoura', 'Villach', 'Villefranche-sur-Mer', 'Vilnius', 'Viña del Mar', 'Virginia Beach', 'Visalia', 'Viterbo', 'Vitoria-Gasteiz', 'Volos', 'Vrsar', 'Waco', 'Wakefield', 'Warsaw', 'Warth', 'Washington D.C.', 'Waterford', 'Watertown', 'Watsonville', 'Waukegan', 'Waukesha', 'Wellington (New Zealand)', 'Wellington (U.S.)', 'Wengen', 'Weno', 'West Lafayette', 'West Palm Beach', 'Westendorf', 'Westminster', 'Weston', 'Wheeling', 'White Plains', 'Whitehorse', 'Wichita', 'Wichita Falls', 'Wiesbaden', 'Wildwood', 'Wilkes-Barre', 'Willemstad', 'Williams', 'Wilmington (Delaware)', 'Wilmington (North Carolina)', 'Winchester', 'Windhoek', 'Windsor', 'Winnipeg', 'Winslow', 'Winston–Salem', 'Winterthur', 'Wolfsburg', 'Wollongong', 'Wolverhampton', 'Woodburn', 'Worcester (UK)', 'Worcester (U.S.)', 'Worthing', 'Wroclaw', 'Wuppertal', 'Würzburg', 'Yakima', 'Yamoussoukro', 'Yaoundé', 'Yaren', 'Yellowknife', 'Yerevan', 'Yogyakarta', 'Yokohama', 'Yonkers', 'York (UK)', 'York (U.S.)', 'Youngstown', 'Yuma', 'Zadar', 'Zagreb', 'Zakopane', 'Zamboanga City', 'Zanzibar', 'Zaragoza', 'Zell am See', 'Zell am Ziller', 'Zermatt', 'Zug', 'Zurich', 'Zwickau', 'Zwolle', 'Afghanistan', 'Albania', 'Algeria', 'Andorra', 'Angola', 'Antigua and Barbuda', 'Argentina', 'Armenia', 'Australia', 'Austria', 'Azerbaijan', 'The Bahamas', 'Bahrain', 'Bangladesh', 'Barbados', 'Belarus', 'Belgium', 'Belize', 'Benin', 'Bhutan', 'Bolivia', 'Bosnia and Herzegovina', 'Botswana', 'Brazil', 'Brunei', 'Bulgaria', 'Burkina Faso', 'Burundi', 'Cabo Verde', 'Cambodia', 'Cameroon', 'Canada', 'Central African Republic', 'Chad', 'Chile', 'China', 'Colombia', 'Comoros', 'Congo, Democratic Republic of the', 'Congo, Republic of the', 'Costa Rica', 'Côte d’Ivoire', 'Croatia', 'Cuba', 'Cyprus', 'Czech Republic', 'Denmark', 'Djibouti', 'Dominica', 'Dominican Republic', 'East Timor (Timor-Leste)', 'Ecuador', 'Egypt', 'El Salvador', 'Equatorial Guinea', 'Eritrea', 'Estonia', 'Eswatini', 'Ethiopia', 'Fiji', 'Finland', 'France', 'Gabon', 'The Gambia', 'Georgia', 'Germany', 'Ghana', 'Greece', 'Grenada', 'Guatemala', 'Guinea', 'Guinea-Bissau', 'Guyana', 'H', 'Haiti', 'Honduras', 'Hungary', 'Iceland', 'India', 'Indonesia', 'Iran', 'Iraq', 'Ireland', 'Israel', 'Italy', 'Jamaica', 'Japan', 'Jordan', 'Kazakhstan', 'Kenya', 'Kiribati', 'Korea, North', 'Korea, South', 'Kosovo', 'Kuwait', 'Kyrgyzstan', 'Laos', 'Latvia', 'Lebanon', 'Lesotho', 'Liberia', 'Libya', 'Liechtenstein', 'Lithuania', 'Luxembourg', 'Madagascar', 'Malawi', 'Malaysia', 'Maldives', 'Mali', 'Malta', 'Marshall Islands', 'Mauritania', 'Mauritius', 'Mexico', 'Micronesia, Federated States of', 'Moldova', 'Monaco', 'Mongolia', 'Montenegro', 'Morocco', 'Mozambique', 'Myanmar (Burma)', 'Namibia', 'Nauru', 'Nepal', 'Netherlands', 'New Zealand', 'Nicaragua', 'Niger', 'Nigeria', 'North Macedonia', 'Norway', 'Oman', 'Pakistan', 'Palau', 'Panama', 'Papua New Guinea', 'Paraguay', 'Peru', 'Philippines', 'Poland', 'Portugal', 'Qatar', 'Romania', 'Russia', 'Rwanda', 'Saint Kitts and Nevis', 'Saint Lucia', 'Saint Vincent and the Grenadines', 'Samoa', 'San Marino', 'Sao Tome and Principe', 'Saudi Arabia', 'Senegal', 'Serbia', 'Seychelles', 'Sierra Leone', 'Singapore', 'Slovakia', 'Slovenia', 'Solomon Islands', 'Somalia', 'South Africa', 'Spain', 'Sri Lanka', 'Sudan', 'Sudan, South', 'Suriname', 'Sweden', 'Switzerland', 'Syria', 'Taiwan', 'Tajikistan', 'Tanzania', 'Thailand', 'Togo', 'Tonga', 'Trinidad and Tobago', 'Tunisia', 'Turkey', 'Turkmenistan', 'Tuvalu', 'Uganda', 'Ukraine', 'United Arab Emirates', 'United Kingdom', 'United States', 'Uruguay', 'Uzbekistan', 'Vanuatu', 'Vatican City', 'Venezuela', 'Vietnam', 'Yemen', 'Zambia', 'Zimbabwe']



```python
from spacy.matcher import Matcher
import spacy
from collections import Counter
#this function will read a decades file and write all the locations mentioned and their frequencies in a csv file
def store_places(decade):
    nlp = spacy.load("en_core_web_sm")
    nlp.max_length = 3000000 #fixes bug bc file exceeds og limit
    text = Path(str(decade) + ".json").read_text()
    doc = nlp(text)
    matcher = Matcher(nlp.vocab)
    for place in gazetteer:
        pattern = [{'LOWER': place.lower()}]
        matcher.add(place, [pattern])

    matches = matcher(doc)
    # Open the file in "write" mode
    count_list = []
    with open(str(decade) + "places.csv", "w") as file:
        #write the most frequent places
        file.write("place_name,frequency\n")
        for match_id, start, end in matches:
            count_list.append(doc[start:end].text)
        counter = Counter(count_list)
        for term, count in counter.most_common(20):
            line = term + "," + str(count) + '\n'
            file.write(line)
decade = 1890
#time to go through all the decades and write the most frequent locs
while decade <= 2010:
    store_places(decade)
    decade += 10
```

# Now with the csv files from each decade, I can map the locations in ArcGIS


### Resulting Map: https://arcg.is/14mevK0


```python

```

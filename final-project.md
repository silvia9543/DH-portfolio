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




    '<!DOCTYPE html>\n<html lang="en">\n  <head>\n    <meta charset="UTF-8">\n    <meta http-equiv="X-UA-Compatible" content="IE=edge">\n    <meta name="viewport" content="width=device-width, initial-scale=1.0">\n    <title>Genius</title>\n    <style>*{box-sizing:border-box}body{width:100%;margin:0;color:#fff;background:#000;font-family:Helvetica Neue,Arial,Helvetica,Geneva,sans-serif;font-size:20px;font-weight:700}a,a:active,a:focus{color:#3d85c6;text-decoration:none}a:hover{border-bottom:1px dotted}header'




```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(response_text)
print(type(soup))
```

    <class 'bs4.BeautifulSoup'>



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

## Now with the csv files from each decade, I can map the locations in ArcGIS


### Resulting Map/Artifact: https://arcg.is/14mevK0

# Written Discussion:


#### In my final project, I tracked the locations mentioned by popular music in the U.S. and how they have changed in the past century. My research question looks at how the locations mentioned by popular music may correlate to historical events and other media of the time and any dramatic shifts that may reflect societal trends. 

#### My dataset was comprised of the lyrics of the top ten songs in each decade since 1890, along with a clean list of all the cities in the U.S. and countries in the world. I used the titles of the most popular songs per decade provided by Dave’s Music Database, then used Genius to access the song lyrics of each, and used online Gazeteer resources to manually compile a list of place names, which includes cities both in and out of the US and the name of every country in the world. 

#### Preparing my data was the most challenging and time-consuming part of the project. I would estimate a total of 20 hours spent on the entire project, with at least half being spent on data preparation. This was because it was extremely difficult to clean all the data or to even extract it from the website. First, I used web scraping which we learned in class to scrape the song titles from Dave’s Music Database. Using the Beautiful Soup library, I first looked for all the “p” tags, but that included much more than the song titles, so I was then able to narrow it down to all the “a” tags. I wrote code in python to clean the final list, skipping over newline and space characters, and checked to make sure that all the titles were in the list. In the end, there were a few missing and I wasn’t sure why, so I manually added them by appending them to the list. 

#### The second step of preparing this data for use was designing my data structures to store them. I decided upon a Python dictionary with keys being the decade and values being the song titles from that decade. Working with loops and a lot of debugging, I was eventually able to get a clean dictionary to store all the song titles in an organized format. 

#### To prepare the song lyrics, I used the Genius API to search up the title of the song, get the URL, and then scrape the lyrics from the URL. Here, I ran into multiple issues with accessing the page, such as error messages saying that cookies need to be enabled and JavaScript needs to be on. By googling issues like these, I was eventually able to access the correct pages for most all the songs (some of the older songs were not available on Genius) and organized my code by putting them in functions to make it easier to read. The lyrics data is not clean because I couldn’t figure out how to clean all of it even after hours, but I figured it would probably be negligible in the grand scheme of the project, since the words with the locations would still be there regardless.

#### Then to analyze the song lyrics, I used the programming historian lesson: Finding Places in Text using the World Historical Gazeteer. This was challenging as well, since I had 13 different files to analyze and find matches with, so I ran into memory issues with the nlp library. This was fixed by adjusting nlp.max length. I also wanted to create a GIS Web App at the end, so I altered the code to produce .csv files storing the locations and their frequency per decade. Using a for loop that ran the function on each decade, I produced 13 .csv files.

#### The final step was to create my GIS web app that would show each decade as a different layer. I imported my .csv files and made it so that users could toggle layers on and off, as well as see the exact place names per decade. One limitation here is that it only names the top nine locations in each layer, and shows the rest as “other,” but I couldn’t figure out how to change that in ArcGIS. 

#### To interpret my artifact, I used secondary sources such as “Progression of Music Throughout American History” on Sutori’s website to contextualize my findings. There were a few patterns that I noticed. First, important places of Black history like Harlem and Memphis were mentioned starting in the 1910’s, which corresponds to the rise of Blues and Jazz. Second, Hollywood came up frequently starting in the 1940’s, which makes sense since the film industry was established in the 1920’s with sound being synchronized to film later. I also noticed that as time progresses, there are more non-US locations that pop up, like Paris and Australia, perhaps showing increased globalization and travel in society.

#### In conclusion, the locations that popped up in popular music can reflect certain societal trends, such as the rise of Hollywood and entertainment, popularization/appropriation of African American music, and globalization. This project reinforced the techniques of web-scraping, using APIs, using nlp, NER, and gazetteer, opening and closing files of different formats, ArcGIS web mapping, and generally using python to process, prepare, and analyze texts. There are a few important limitations to my project that I couldn’t resolve – for example, there are some lyrics that may match a place name but mean something else not tied to that place. Also, the lyrics data are not fully cleaned, so there may be matches outside of the lyrics. But despite these limitations, my project accomplishes my goal of inspecting locations in popular music, works with a large enough dataset to produce accurate results, and was able to create a visualization of the data through a web app that allows for user interaction.  


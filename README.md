PHP-Excerpt
===========

During some contracting I was doing recently there was a requirement to implement some search logic using only PHP. There are no issues with that but it turns out I couldn’t find a decent extract generator handy as usually one would just plug into the search engines provided version to do this.

Off the top of my head I could only think of one example I was aware of which lives in Sphider (for the record it lives in searchfuncs.php from line 529 to 566). Sadly it has a few issues. Firstly the code is rather difficult to understand, and more importantly it usually has accuracy issues. A quick search turned up this link http://stackoverflow.com/questions/1436582/how-to-generate-excerpt-with-most-searched-words-in-php on StackOverflow. The second answer looked promising but its even more difficult to understand and a bit of profiling showed some performance issues will all of the regex going on in there.

Since I couldn’t find a solution I was happy with I naturally decided to write my own. The nice thing about reinventing the wheel is you can get a round one. The algorithm is fairly simple,

Identify all the matching word locations.
Work out a section of text that best matches the terms.
Based on the snip location we trim around the string ensuring we don’t skip whole words and don’t remove the last or first word if that’s the actual match.
Sounds good in theory, but lets see the results.

Sample Text

“Welcome to Yahoo!, the world’s most visited home page. Quickly find what you’re searching for, get in touch with friends and stay in-the-know with the latest news and information. CloudSponge provides an interface to easily enable your users to import contacts from a variety of the most popular webmail services including Yahoo, Gmail and Hotmail/MSN as well as popular desktop address books such as Mac Address Book and Outlook.”

Search Term “yahoo and outlook”

Sphider Snippet

“get in touch with friends and stay in-the-know with the latest news and information. CloudSponge provides an interface to easily enable your users to import contacts from a variety of the most popular webmail services including Yahoo, Gmail and Hotmail/MSN as well as popular desktop address books such as Mac Address Book and”

Stackoverflow Snippet

“Welcome to Yahoo!, the world’s most visited home page. Quickly find what you’re searching for, get in touch with friends and stay in-the-know with the latest news and information. CloudSponge provides an interface to easily enable your users to import contacts from a variety of the most…“

My Snippet

”..an interface to easily enable your users to import contacts from a variety of the most popular webmail services including Yahoo, Gmail and Hotmail/MSN as well as popular desktop address books such as Mac Address Book and Outlook.”

I consider the results to be equally good in the worst case and better in most cases I tried. I also tried each over much larger portions of text and both the Sphider and Stackoverflow seemed to produce either nothing relevant or were missing what I thought was the best match.

SOURCE: http://www.boyter.org/2013/04/building-a-search-result-extract-generator-in-php/

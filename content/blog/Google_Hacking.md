
---
title: "Google Hacking"
date: "2011-08-11T12:39:00-04:00"
draft: false
---

Weeks ago I downloaded a Google+ app for my phone. While it is a convenient means to stay abreast of what folks are posting in my circles, there is one glaring "feature" I detest: if you enable location services (GPS, and Google/Verizon), the app will show you people near your location that also have G+ profiles. You can add nearby folks to your circles using this information.

I keep location services off because, as an Android phone, I have about 14 seconds of battery life, and enabling the GPS exacerbates the problem. On Saturday I was weak with a head cold, and for a moment I turned the services on so that my phone would realize it was no longer in California and set the weather/time accordingly. But I forgot to turn them off.

Saturday morning I noticed I have dozens of Google notifications; and sudden 10 more followers. I don't know these people at all.

Now, I get that I'm at fault here. I knew the risk when I got the app. I know I can hide/block all of these folks on my G+ account. Their posts are off to the side and I can ignore them easily. Maybe I'm just not comfortable with social networking. It irks me a little that if I make a public post, these folks can comment on it (I think). The whole affair just makes me feel... uncomfortable.

So the rest of this post is about making Google do your bidding, since I accidentally did theirs to a larger degree than I'm comfortable with. In a Google search you have several search operators and modifiers as shown on this table. This is not a complete list either, just the most useful ones in my experience.

<table border="1">
  <tr>
    <th colspan="4">Basic Operators</th>
  </tr>
  <tr>
    <th>Operator</th><th>Name</th><th>Description</th><th>Example</th>
  </tr>
  <tr>
    <td>*</td><td>Word Wildcard</td><td>Will match against any word (exactly 1)</td><td>Take Out * Food</td>
  </tr>
  <tr>
    <td>.</td><td>Character Wildcard</td><td>Will match against any word (exactly 1)</td><td>index.of</td>
  </tr>
  <tr>
    <td>-</td><td>NOT operator</td><td>Google will return sites that do NOT have the term in the text.</td><td>hacker -coughing</td>
  </tr>
  <tr>
    <td>|</td><td>OR operator</td><td>Google will return sites that match the term before or the term after the |. The normal action is to AND terms together.</td><td>hot | not</td>
  </tr>
  <tr>
    <td>+</td><td>Force Include</td><td>Forcibly include a term in your search. Google normally ignores common terms like "the", "and", or "for". This overrides that.</td><td>+and justice +for all</td>
  </tr>
  <tr>
    <td>"</td><td>Phrase Search</td><td>Treat all words as a single search term. This renders <strong>+</strong> fairly useless.</td><td>"and justice for all"</td>
  </tr>
  <tr>
    <th colspan="4">Advanced Operators</th>
  </tr>
  <tr>
    <td>site:</td><td>Site search</td><td>Only return results that match on a given site.</td><td>site:brolem.net Nehrim</td>
  </tr>
  <tr>
    <td>intitle:</td><td>Title search</td><td>Only return results where the search terms match in site titles</td><td>intitle:"Build System Info" "Welcome to Kojiweb"</td>
  </tr>
  <tr>
    <td>inurl:</td><td>URL search</td><td>Like site:, but you're not restricted to just a domain name. This will search arguments and parameters in URLs too, so it'll return a lot of results potentially.</td><td>inurl:backup</td>
  </tr>
  <tr>
    <td>filetype:</td><td>File type filter</td><td>Only return results where the document searched matches a given type such as html, htm, doc, xls, pdf, or whatever else.</td><td>filetype:ini password</td>
  </tr>
  <tr>
    <td>numrange:</td><td>Number range</td><td>Matches against a range of numbers. This is how you find phone numbers or ... I better not say what else you can get.</td><td>numrange:1-999</td>
  </tr>
</table>
<br/>
Yeah those last rows are juicy. Let's combine this information into some interesting searches.

<table border="1">
  <tr>
    <th>Query</th><th>Results</th>
  </tr>
  <tr>
    <td>"Apache/WWW" intitle:index.of</td><td>Apache-served sites we can do directory traversal of</td>
  </tr>
  <tr>
    <td>"Microsoft-IIS/6.0" intitle:index.of</td><td>IIS6-served sites we can do directory traversal of</td>
  </tr>
  <tr>
    <td>filetype:conf inurl:proftpd -sample</td><td>Accidentally served FTP configuration</td>
  </tr>
  <tr>
    <td>intitle:index.of config.php</td><td>Accidentally served PHP configuration</td>
  </tr>
  <tr>
    <td>filetype:log "admin account info"</td><td>Admin account logs. Oops.</td>
  </tr>
</table>
<br/>
I don't really need to go on, you can get creative. If you can think of well-known log files, configuration files, error messages, database logs or other bits of default software installation content... you can find it on Google. The trick is to start with a broad search, and then continue adding terms to narrow your results. You can cram 32 search terms at once, unless you're using wildcards... then you can cram more because they are not part of the count!

You can find more information about the [basic search terms](http://www.google.com/support/websearch/bin/static.py?page=guide.cs&guide=1221265&answer=136861) on Google's own site. There used to be a Google Hacking Database until 2008 when the maintainer, <a href="http://en.wikipedia.org/wiki/Johnny_Long">Johnny Long</a>, found Jesus. Then he started a "Hackers for Charity" site, and the GHDB was <a href="http://www.hackersforcharity.org/ghdb/">reposted there</a>.

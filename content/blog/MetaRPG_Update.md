
---
title: "MetaRPG Update"
date: "2009-10-04T10:57:00-04:00"
draft: false
---

Just wanted to update you guys on MetaRPG development. The stat window is near completion, at least for my initial design goals. The main difference from OpenRPG's stat window is a lack of "container" objects, and all dice rolls and such are represented as python objects rather than a formatted string that is processed.

Recall that in OpenRPG you could type [1d20+2] and that would roll a die for you. When I write the chat window code I intend to have that kind of processing but not in how a stat (or full character sheet) is defined in the stat window. What this brings to the user (and more so to the DM), is the ability to send parts of the tree around to other players and anchor them to specific nodes based on name. If you have multiple stats with the same name, it will anchor a copy to each of them.

I'll try to explain this with examples, because this probably doesn't make a lot of sense to non-programmers. Lets say you get hit with a spell that reduces attack rolls. The DM could put together a modifier stat (a -4 or something), and say to MetaRPG, "send this to Player A and apply it to all nodes labeled 'Attack'", and poof all of your attack rolls have a -4 modifier. Another example would be if a player had an "Inventory", and if you picked up an Axe, the DM could put together stats for the axe, and send it to your "Inventory".

I don't have anything of a demo yet because I haven't written the server code, nor have I ported the code to Windows. But I wanted to say the foundation for doing this kind of thing has been written. I can build a complete (static) character sheet with the code I've written so far; it's about 1500 lines of Python code. I will be starting the chat window code soon, and it'll be very similar to what OpenRPG provides. After that comes the server code which is still months out.



---
title: "Dirty Coding"
date: "2010-10-23T11:44:00-04:00"
draft: false
---

Recently I came into possession of the sources for Agobot3, the parent of many modern worms that join grandma's computer to botnets. I've been studying the code a bit and found a couple blocks I found rather interesting.

Notably, Agobot3 has code in it to detect if it is being run in a debugger. This is specifically to make reverse engineering it harder for the security community. Now that the sources are out it's rather moot, but still worth walking through for the sake of learning. Observe:
```
__inline bool IsBPX(void *address) {
    _asm {
        mov esi, address  (1)
        mov al, [esi]     (2)
        cmp al, 0xCC      (3)
        je BPXed          (4)
        xor eax, eax      (5)
        jmp NOBPX         (6)
BPXed:
        mov eax, 1        (7)
NOBPX:
    }
}
```
This function checks to see if the given address has been set as a break point in a debugger, and returns True if so, False if not. Notice the use of raw assembly here; I'll translate it:

* First we take the function address (the place the code lives in memory) and store that value in a register called "esi"
* Next we take the first opcode (machine level processor instruction) and store that into "al". This is the very first thing the code pointed to by "esi" would attempt to do.
* This is the magic. We compare that first opcode with with value 0xCC, which is a special opcode injected into running code by debugging programs to signal a breakpoint. I'll explain below.
* If 3's comparison was true, jump (read: goto) to BPXed.
* This line only is evaluated if we didn't jump before. We XOR the contents of "eax" with itself, which if you know your boolean logic, you know that always returns false.
* Jump to NOBPX. Note there is no code beyond that location, so the function returns the contents of "eax". If we didn't jump after line 3, eax is false.
* Move the value '1' into "eax". '1' in this context is synonymous with "True". Since there is no code to execute in this function, the function returns the contents of "eax".

Break points are places in running code programmers set to halt execution. When a breakpoint is hit, execution stops and usually the debugger (such as gdb, SoftICE, etc) lets you poke around different parts of memory to see what is what. The way setting breakpoints work is the debugger injects a special opcode at the beginning of the piece of code you're going to execute which causes the executing program to return control the debugger.

That special opcode's ID number is 0xCC, and this is true for almost all debuggers. By detecting this opcode, Agobot3 can figure out it is being run in a debugger, and do some nasty things to itself to make reverse engineering the binary much harder. Indeed, this function is used in many places:
```
08:44 PM box:~/downloads/bot $ grep IsBPX *
Binary file agobot3.ncb matches
utility.cpp:__inline bool IsBPX(void *address) {
utility.cpp:	if(IsBPX(&IsBPX)) {
utility.cpp:		g_pMainCtrl->m_cConsDbg.Log(5, "Breakpoint set on IsBPX, debugger active...n");
utility.cpp:	if(IsBPX(&IsSICELoaded)) {
utility.cpp:	if(IsBPX(&IsSoftIceNTLoaded)) {
utility.cpp:	if(IsBPX(&IsVMWare)) {
utility.cpp:		if(IsBPX(&IsDbgPresent)) {
```
Specifically, it looks to see if breakpoints are placed where the author expects security professionals to place them: on functions that check for debuggers or whether it is being run in a virtual machine. So what does Agobot3 do when it figures out it is in a debugger, or running in a VM? It terminates itself immediately.


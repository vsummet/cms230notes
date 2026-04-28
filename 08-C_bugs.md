#Cool Bugs in C

## Heartbleed bug (April 2014)

*Aspect of C:* We've talked a lot about buffer overruns this semester and the need to program defensively.  This is a great case study in why you need to be aware of this particular aspect of C programming.

*Why was it a big deal*: 
This bug was in a code base known as OpenSSL.  SSL stands for Secure Sockets Layer and is a protocol (set of rules) by which information is securely passed around the internet.  The bug was in a crucial bit of C code which implemented this (and other) protocols.  OpenSSL is used by many, many webservers which need secure communication (17% of all those on the internet, actually) so this was a widespread problem.  This bug allowed malicious attackers to gain access to memory which could have been used to store decrypted passwords.

*How it worked:*
As always, the webcomic XKCD does a great job breaking down a complex bit of code into something understandable:
https://xkcd.com/1354/

Essentially two computers are connected to each other (securely, we hope).  These computers occasionally send a "heartbeat request" -- just a little query asking, "Hey, are we still connected?"  There's a response of just a few bytes to this query, and the request that is sent includes the correct length of the response.  When a computer receives a request, it recieves two pieces of information: the response to be sent, and the length of that response.

The receiver then allocates a buffer to store the response in.  However, the code *did not verify* that the length of the buffer actually matched the length of the response.  Using pointer arithmetic, the receiver began at the start of the requested response, cheerfully read the number of bytes requested, and sent them back to the requester.

*C code*
```
memcpy(bp, pl, payload);
```
Yep.  That's it.  Let's break it down a bit.  `memcpy` is (as you might infer) a function which copies the contents of memory from one location to another.  The parameters are `bp`, `pl` and `payload`.  

*Sources:*
https://www.seancassidy.me/diagnosis-of-the-openssl-heartbleed-bug.html
https://www.csoonline.com/article/3223203/vulnerabilities/what-is-the-heartbleed-bug-how-does-it-work-and-how-was-it-fixed.html
https://gizmodo.com/how-heartbleed-works-the-code-behind-the-internets-se-1561341209
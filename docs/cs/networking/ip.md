## Time to live

Every packages has a tome to live counter which MUST decrease on every hop.
It also should decrease after sitting on a router for 1 second (but where does a packet hang 1 second nowadays?)
If you are the one to recieve it from 1 to 0, you __MUST__ throw it away.
This avoids loops. (this is your packet - no, it's your - no it's yours).

## Fragmentation

The ip header defines that an ip package is maximum 64 kb.

the mtu (maximum transmission unit) is the size of the larges protocol data unit.
Basically what fits through the pipe. 
For example you gave me an ethernet package with 1500 bytes, but my next hop is on an anna-lena network with 1000 bytes.

### Old way

The packages get splits up and the header get dupplicates along the fragments.
The bad thing is that the reciever then needs to glue them back together.

The following routers do not do that, since that could lead to constant repackaging and splitting of the packages.
The end user then needs to put them back together
This requires the right order and to know what packages got split up and what not.

the ip header includes a mfbit (more fragment bit) which tells, that there are still packages coming.
This is set through the router fragmenting.
Only the last one is then set to 0, which means this was the last one.

The ip layer has no garantee for packages.
The router can look at this and say if it does not arrive in the right order, we just throw it away.

The header includes the next layer (tcp/udp) or port numbers.
This allow firewalls to allow/dissallow traffic.
Fragmentation in the wrong order will circumvent these.

Since ip does not repeat lossed package, you will have to transmit bytes that are not used.
If 10 fragments are pushed and 9 arrive, you will have to retransmit all those 9.
This will spam the already stressed lines.

There is a bit to restrict fragmentation.
If it is set we just throw away the whole package.
The german isp telekom does not care about it.


### New way

If it does not fit the MTU, we just throw it away and tell the sender that it does not fit.


## ICMP

While 99 % are going smothly and will propably be encoded through hardware, the 1%, which are special will be addressed special
This will be addressed by icmp (Internet control message protocoll)

This is the control mechanism, since ip only throws away.

very usefull for debugging, for example through wireshark.

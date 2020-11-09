# The data link layer

The data link layer deals with the Detection and errors in the transmission of frames.
The sender can add a id and a checksum variant
(like [crc](https://en.wikipedia.org/wiki/Cyclic_redundancy_check)
to a SDU(Service Data Unit - The data we are sending).

### Finite-state machinge

an [FSM](https://en.wikipedia.org/wiki/Finite-state_machine)
is a model that can be in exactly one state at any given time.
It is usefull for moddeling The reviever/sender view seperatly and reasoning about them.

### The Id

The simplest form is the [alternating bit protocol](https://en.wikipedia.org/wiki/Alternating_bit_protocol)
which waits for the response of each Data request.
The single bit is used to avoid problems caused by missing/faulty responses.

The use of [sliding windows](todo) then allows __Pipelining__,
which allow the sender to transmit frames without waiting for each response.

### Piggibacking

Because Protocols often need to send data in both directions, they use piggibacking to pair acknowledgment with the data.
This  reduces overhead subst.

## Networking

- Point to point layer:
Only 2 communicating systems directly connected.
- Lan layer
Set of communicating devices such as any 2 devices can directly exchange frames.
For example:

Endhost: device which is able to send and receive data for it's own usage.
Roters: multiple links to neughbouring routers or endhosts.

To know the way around the network the Data gets bundled into a __packet__.
The packet also includes the Address of the source, destination and information about the path.

### The datagram organisation

Organisation = way to order adresses/network

Each host is identified by a network layer address.
To transfer a Packet __hop by hop__ forwarding is used.
Each router has a forwarding table, that maps destinations address to one of its outgoing interface.
This happens for each `hop` over the network until the destination is reached.

This forwarding table cannot be maintained by hand due to the dynamic nature of networks.
There are multiple approaches toward solving this like a seperate network or computed approach.
In the later the next hop is calculated and stored if a package to an unknown address is recieved.
[computing forwarding tables](computing_forwarding_tables.md)


## flat addresses

When working with a flat addressing scheme each host and network node has a uniqe address (mac address)
This forces the router toknow the path for each address.

A hirachical Addressing scheme groups addresses under a name (e.g.city).
When the router looks up an adress, it then only checks this group and forwards it there.
The rest is handled by local routers.

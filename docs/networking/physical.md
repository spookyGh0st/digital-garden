# The physical Layer

Network speeds are always meaured in bits per second, so 1 kb will take 8 seconds on a 1kb/s.
There are electrical (copper) cabels, optical fiber cabels and wireless connections.

- electrical: local connections under 1000 meters
- fiber above 1000 meters most often in isp
- wireless: very smoal

Then there are ways to transmit these data, for example the sender and reciever aggrees,
that +5 volt means 1 and -5 volt means 0.
__Both have to agree to that__

There also exist other encoding standards, called [line codes](line_coe.md) 

The reciever has to check on the same interval as the sender sends.
This can lead to problems when the 2 clocks on the host are not synced, 
for example through temperature changes.

### Time-sequence diagramm

common diagram used to describe interaction between hosts.
```
            Host A      Host B
Data.req(0)   |         |
              |\        | 
              |  \      | 
              |    \    | 
              |      \  |  Data.ind(0)
```

- Data.req = Requesting some Data to be transmitted
- Data.ind = Indication correspond to the reception of some information
- 0 = The Data Transmitted (1 Bit).

It can happen, that Data is not transmitted correctly.
__Perfect Reliability is never archived:__
The physical layer may change or deliver more or less bits

### A frame

When reasoning about the physical layer one continuous stream of a single source is called a frame.
Bit and Character stuffing encodes a frame into special codes.
When the special code is then encountered in the frame it then gets chopped up and split into multiple frames.
This allows to reover frameson error, but comes at high tramsmission costs.


# The data link layer

The data link layer deals with the Detection and errors in the transmission of frames.
The sender can add a id and a checksum variant
(like [crc](https://en.wikipedia.org/wiki/Cyclic_redundancy_check)
to a SDU(Service Data Unit - The data we are sending)

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

## Piggibacking

Because Protocols often need to send data in both directions, they use piggibacking to pair acknowledgment with the data.
This  reduces overhead subst.

# The physical Layer

Network speeds are always meaured in bits per second, so 1 kb will take 8 seconds on a 1kb/s.
There are electrical (copper) cabels, optical fiber cabels and wireless connections.

- electrical: local connections under 1000 meters
- fiber above 1000 meters most often in isp
- wireless: very smoal

Then there are ways to transmit these data, for example the sender and reciever aggrees,
that +5 volt means 1 and -5 volt means 0.
__Both have to agree to that__

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
__Perfect Reliability is never archived__







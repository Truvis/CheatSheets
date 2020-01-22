## Queuing Schedulers
### Priority Queueing (PRIQ)
Priority queuing is the simplest form of traffic shaping, and often the most effective. It performs prioritization of traffic only, without regard for bandwidth. A flat hierarchy of priority levels is created, all packets at the highest priority level are always processed first.

Pros
+ Easy to configure and understand.

Cons
+ Lower priority queues can be completely starved for bandwidth easily.

### Class Based Queueing (CBQ)
CBQ is the next step up from priority queuing. A tree hierarchy of classes is created; each with an assigned priority and bandwidth limit. Priority works much in the same way that it does in the PRIQ however, instead of processing all packets from the class, it will only process enough packets until the bandwidth limit is reached.

### Hierarchical Fair Service Curve (HFSC)
Hierarchical Fair Service Curve (HFSC) is the most complex of the ALTQ shaper types. In older versions of pfSense software, it was the only option available. It has a hierarchy of queues and is capable of real-time traffic guarantees.

It can be very effective for VoIP on links that degrade quickly, such as 3G/4G, but it can be complex to configure and tweak for proper operation.

### Controlled Delay (CoDel)
Attempts to combat bufferbloat.

### Fair Queuing (FAIRQ)
Attempts to fairly distribute bandwidth among all connections.

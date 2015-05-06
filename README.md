# Token_Bucket_Emulation
The code implemented a token bucket traffic shaper system, which simulate a traffic shaper who transmits packets controlled by a token bucket filter 
using multi-threading within a single process.<br \>

Packets arrive at the token bucket filter at a rate of lambda packets per secondand each packet requires P tokens in order for it to be eligiable for transmission. 
(Packets that are eligiable for transmission are queued at the Q2 facility.) When a packet arrives, 
if Q1 is not empty, it will just get queued onto the Q1 facility. Otherwise, it will check if the token bucket
has P or more tokens in it. If the token bucket has P or more tokens in it, P tokens will be removed from the token
bucket and the packet will join the Q2 facility. If the token bucket does not have enough tokens, the packet gets queued into the Q1 facility. 
Finally, if the number of tokens required by a packet is larget than the bucket depth, the packet must be dropped.<br \>

The transmission facility serves packets in Q2 in the first-come-first-served order and at a service rate of mu per second. 
When a server becomes available, it will dequeue the first packet from Q2 and start transmitting the packet.
When a packet has received 1/mu seconds of service, it leaves the system. <br \>

When a token arrives at the token bucket, it will add a token into the token bucket. 
If the bucket is already full, the token will be lost. It will then check to see if Q1 is empty.
If Q1 is not empty, it will see if there is enough tokens to make the packet at the head of Q1 be eligiable for transmission
(packets in Q1 in also served in the first-come-first-served order). If it does, 
it will remove the corresponding number of tokens from the token bucket, remove that packet from Q1 and move it into Q2,
and wake up the servers in case they are sleeping. It will then check the packet that is now at the head of Q1 to see
if it's also eligiable for transmission, and so on.

# Reliable-transport-protocol
Evan Chen & Kevin Jen

# Approach --- 
For this project we follow the suggested implementation strategy from the assignment page. 
- In level 1, we have a window of 2 by using a loop of 2 range. This will send 2 packet at a time.
- In level 2, we added the sequence number to the msg json as a field. Both send and recv increment the sequence number and recv will only send ack back when the number    matches. 
- In level 3, we implemented window on the receiver side as an array. The receiver will store it and send the corresponding ack back in order. 
- In level 4, we added timestamp and retransmitted field to the json message. The program will retransmit messages that had exceeded 1 sec since it was sent. The -         retransmitted field will also be true which will let the receiver side know to send ack for it. 
-In level 5, we made sure that the program will drop a packet if 
  1) Json had trouble loading or invalid
  2) The fields are incorrect 
  3) The compression of the data is inconsistent after sending by implementing a checksum field. This field stores encoded data using zlib.
- In level 6, we changed the retransmission timeout from 1 second to 2 x RTT. The estimated RTT equals the time of the most recently received ACK subtracted by the         corresponding packet’s sent time. If retransmission have to be done, the sender return to slow start.
- In level 7, for a faster program we implemented RENO fast retransmit. When the sender side receives a ack it will store its sequence number in an received_ack array.
  It'll then check if receiver send this ack's sequence number appeared 3 or more time in the array. 
 
# Challenges --- 
- We struggled to think of a way to measure the time since a packet had been sent.
- For level 4 the program was timing out due to excessive retransmission
- The program was often too slow, resulting in time exceeded 

# Design and features --- 

# Testing --- 
For testing, we use the test file in the configs folder. We would run the implementation with the relevant configs test after each step.  

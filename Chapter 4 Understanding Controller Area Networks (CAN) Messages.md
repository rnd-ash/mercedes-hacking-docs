# Chapter 4: Understanding Controller Area Networks (CAN) Messages

Within Most Mercedes vehicles, there are 2 forms of CAN Messages
1. Regular CAN Messages (Up to 8 byte payloads)
2. ISO15765 messages (These are multi-frame payloads that can represent up to a 4096 byte payload).


## Regular CAN Message
TBA

## ISO15765 CAN Message

### Observed uses in Mercedes
1. Diagnostic messages between DAS/Xentry and ECUs
2. Communication between Radio and Cluster
3. Communication between GPS and Radio
4. Communication between Telematics module and other ECUs in the car


### How it works

A ISO15765 message can have 2 forms. A single payload, or a multi-frame payload.

**AN ISO15765 CAN FRAME IS ALWAYS 8 BYTES LONG! - REGARDLESS OF THE ACTUAL PAYLOAD SIZE

#### Single frame payload
Below is an example of a single frame payload
```
ID: 0x01A4 DLC: 8 DATA: [0x02, 0x00, 0x01, 0x00, 0x00, 0x00, 0x0A, 0x0A]
```
In this style of packet, the first byte (shows the number of bytes that are in the payload itself, so for this packet, the actual data would be:
```
[0x00, 0x01]
```

#### Multi-frame payload
Below is an example of a trace of a multi-frame payload
```
ID: 0x01A4, DLC: 8, DATA: [0x10, 0x17, 0x03, 0x24, 0x02, 0x60, 0x01, 0x01]
ID: 0x01D0, DLC: 8, DATA: [0x30, 0x08, 0x28, 0x00, 0x00, 0x00, 0x00, 0x00]
ID: 0x01A4, DLC: 8, DATA: [0x21, 0x00, 0x00, 0x00, 0x13, 0x00, 0x01, 0x00]
ID: 0x01A4, DLC: 8, DATA: [0x22, 0x02, 0x00, 0x04, 0x00, 0x20, 0x20, 0x20]
ID: 0x01A4, DLC: 8, DATA: [0x23, 0x20, 0x00, 0xF3, 0x00, 0x00, 0x12, 0xC0]
```
Notice the `0x01D0` ID Can frame? That is whats called a Flow control frame. More about that below

ISO15765 dictates that to start sending a multi-frame payload, the sender must send a packet starting with `0x1`, followed by the total number of bytes that the payload contains, in this case its `0x017` (0 is carried from the first byte).

When the receiver has sent the first frame, the receiver MUST send a Flow control frame. Broken down, the flow control frame can be interpreted like so:
```
0x30 - Flow control frame (0x3) - Clear to send (0)
0x08 - Block size is 8 frames
0x28 - Send delay between frames is 40 milliseconds
```

Once the sender receives the flow control frame, and is allowed to send, it begins sending the rest of the payload 7 bytes at a time (the first byte of each frame is an ID that starts at `0x21` and sequentially increases until it hits `0x29`, at which point it rolls back to `0x21`. After every frame is sent, the sender waits for the specified delay time set by the receiving ECU.

If the sender hits the specified block size, it must wait for another flow control frame from the receiver before continuing sending the payload.

In the above example, the full payload sent by `0x01A0` would be
```
[0x17, 0x03, 0x24, 0x02, 0x60, 0x01, 0x01, 0x00, 0x00, 0x00, 0x13, 0x00, 0x01, 0x00, 0x02, 0x00, 0x04, 0x00, 0x20, 0x20, 0x20, 0x20, 0x00, 0xF3]
```
<br><br>
[Next Chapter](Chapter%205%20Understanding%20Mercedes-Benz%20Signal%20Acquisition%20Modules%20(SAM).md)

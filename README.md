## WebRTC (p2p)

Notes: 

WebRTC

1. A P2P protocol for real-time communication with low-latency (almost a serverless architecture). 
2. It is used for real-time communication - Zoom, Google Meet calls.
3. To be able to communicate with a peer on the internet, we need to know their IP. 
4. I need to register my IP on a signalling server so that my friend can get to know my IP and vice versa. 
5. But how to tell the exact public IP address and the port number to the signalling server?
6. Using a stun server. I send a request to a STUN server to tell me “hey, can you tell me where you got this request from?” The STUN server will respond with the public IP and the port number. 
7. So, peer -> stun server -> send public IP from stun server to signalling server -> destroy the signalling server -> start the P2P communication. 
8. Note: ICE candidates are potential networking endpoints that webRTC uses to establish a communication between peers. Each ICE candidates represent a possible method for two devices(peers) to communicate, usually in the context of real-time applications like video calls, voice calls, or peer-to-peer data sharing. 
9. We dont’ need TURN servers for 95% of the communication. 
10. TURN server candidates. It is like an intermediate between the peers. It is a fallback when you aren’t able to directly talk to the peer (because of restrictive NATs (Network Address Translation) -> causing latency. Do we need it usually? Yes. Along with a STUN server, we need to introduce a TURN server as well. 
11. Offer: The process of the first browser sending their ICE candidates to signalling. It is creating an offer to the signalling server (the initiator creates an “offer”). The receiver responds (answers). 
12. When both parties are sending data (video call), we need to create two WebRTC conncections. One way communication like live cricket matches, classes, etc. 
13. Usually, we create 2 webRTC connections if both the parties want to share data with each other. 
14. SDP - Session Description Protocol -> Both peers also share some other stuff other than the ICE candidates. like media type (audio, video, two videos - screen view + camera view). It’s a very long file. Hard to read. 
15. RTCPeerConnection -> very similar to fetch, websockets in the past. RTCPeerConnection object is a class to hide a lot of complexities and gives back an offer, answer, etc. for communication.


My Understanding: 

WebRTC is a P2P communication architecture used for real-time communication espescially involving transfer of compressed video frames with low latency. Its usecase is in one-on-one gaming, calling, teaching applications, etc. 

The way it works is that a peer first needs to get its ice candidates from STUN server. A STUN server is a special server that essentially tells you the public IP and port number from where it received the ping (request). The peer use this information to create a speical object that contains information including type of content (audio/video), etc. The peer send this object to a signalling server. the signalling server stores this information and shares this data with second peer who wants to connect with the peer. The second peer also needs to go through the same process of going via the STUN server to get the ice candidates. the second peer also shares the same info to the signalling server. Now that both peers "know" about each other, they can destroy the signalling server and start communicating.

Open Source webRTC projects to check out - 

1. Janus (used by Unacademy).
2. Jitsi (GSOC)
3. MediaSoup (used by most of the companies as an Selective Forwarding Unit = SFU)
4. Pion (a pure webrtc server in Golang).




Credits for the content and the understanding : Harkirat Singh's cohort presentation and docs. The code is mostly taken from @hkirat/omegle repository => https://github.com/hkirat/omegle

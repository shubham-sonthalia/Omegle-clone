## An Omegle clone using WebRTC (p2p)

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

Open Source webRTC projects to check out - 

1. Janus (used by Unacademy).
2. Jitsi (GSOC)
3. MediaSoup (used by most of the companies as an SFU)
4. Pion (a pure webrtc server in Golang)


Credits for the content and the understanding : Harkirat Singh's cohort presentation and docs. The code is mostly taken from @hkirat/omegle repository => https://github.com/hkirat/omegle

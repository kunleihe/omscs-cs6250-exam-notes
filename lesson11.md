# Lesson 11: Applications (Video)
- Compare the bit rate for video, photos, and audio.
    - Videos > photos > audio

- What are the characteristics of streaming stored video?
    - Streamed, interactive, continuous playout, stored on a CDN

- What are the characteristics of streaming live audio and video? 
    - Similar to streaming stored video, but many simultanous users, delay-sensitive

- What are the characteristics of conversational voice and video over IP?
    - Hihgly delay-sensitive, less tolerant, real-time interaction

- How does the encoding of analog audio work (in simple terms)?
    - Quantization: audio is encoded by taking many of samples per second and then rounding each sample's value to a discrete number within a particular 

- What are the three major categories of VoIP encoding schemes?
    - Narrowband
    - Broadband
    - Multimode

- What are the functions that signaling protocols are responsible for?
    - User location
    - Session establishment
    - Session negotiation
    - Call participation management

- What are three QoS VoIP metrics?
    - End-to-end delay
    - Jitter
    - Packet loss

- What kind of delays are included in "end-to-end delay"?
    - The time it takes to encode the audio
    - The time it takes to put it in packets
    - ALl the normal sources of network delay that network traffic encouters
    - Playback delay that comes from the receiver's playback buffer
    - Decoding delay

- How does "delay jitter" occur?
    - Delay jitter occurs because different voice packets experience different amounts of delay caused by factors such as different buffer sizes, queueing delays, network congestion levels.

- What are the mitigation techniques for delay jitter?
    - Maintain a jitter buffer, which helps smooth out and hide the variation in delay between different received packets by buffering them and playing them out for decoding at a steady rate.

- Compare the three major methods for dealing with packet loss in VoIP protocols.
    - Forward Error Correction (FEC)
        - Mechanism: Transmits redundant data alongside the main stream to replace lost packets.
        - Trade-off: Increases bandwidth consumption and increases playout delay.
    - Interleaving
        - Mechanism: Mixes/intersperses audio chunks so that lost packets are not consecutive; no redundant data is added.
        - Trade-off: Increases latency (receiver must wait to reorder chunks), making it less useful for delay-sensitive VoIP.
        - Benefit: No extra bandwidth cost.
    - Error Concealment
        - Mechanism: The receiver guesses the lost audio based on surrounding snippets (e.g., repeating the previous packet).
        - Benefit: No added bandwidth or delay.
        - Trade-off: Effectiveness relies on the audio similarity between adjacent snippets.

- How does FEC (Forward Error Correction) deal with the packet loss in VoIP? What are the tradeoffs of FEC?
    - Covered above

- How does interleaving deal with the packet loss in VoIP/streaming stored audio? What are the tradeoffs of interleaving?
    - Covered above

- How does the error concealment technique deal with the packet loss in VoIP?
    - Covered above

- What developments lead to the popularity of consuming media content over the Internet?
    - The bandwidth for both the core network and last-mile access links increased a lot.
    - The video compression technologies have become more efficient
    - The development of Digital Rights Mangament culture

- Provide a high-level overview of adaptive video streaming.
    - Multi-encoding: The source video is first encoded into multiple versions, each with a different bitrate and resolution
    - Chunkcing: All these versions are then segmented into small, sequential chunks
    - Client adaptation: The player on the user's device monitors network conditions in real time
    - Dynamic switching: the player continuously requests the next video chunk from highest quality version.

- (Optional) What are two ways to achieve efficient video compression?

- (Optional) What are the four steps of JPEG compression?

- (Optional) Explain video compression and temporal redundancy using I-, B-, and P-frames.

- (Optional) Why is video compression unable to use P-frames all the time?

- (Optional) What is the difference between constant bitrate encoding and variable bitrate encoding (CBR vs VBR)?

- Which protocol is preferred for video content delivery - UDP or TCP? Why?
    - TCP, because it provides reliability

- What was the original vision of the application-level protocol for video content delivery, and why was HTTP chosen eventually?
    - The original vision for video delivery was to use specialized, stateful servers that controlled the sending rate, putting all the intelligence at the server. This vision was abandonded in favor of the existing HTTP protocol because it allowed content providers to use existing CDN infrastracture and simplied bypassing middleboxes/firewalls.

- Summarize how progressive download works.  
    - The client sends byte-range requests for specific parts of the video content, downloading data only as needed
    - The client pre-fetches video data ahead of playback and stores it in a playout buffer
    - Streaming states operates in two states: filling state and steady state

- How to handle network and user device diversity?
    - Adaptive bitrate streaming: video is encoded into multiple bitrates (qualities) and segmented into chunks. The client downloads a manifest file containing all the options, then dynamically requests the highest quality chunk that its current network conditions can support, which is known as bitrate adaptation.

- How does the bitrate adaptation work in DASH?
    - The client-side video player uses a bitrate adapatation function to dynamically select the quality of the next chunk to download.

- What are the goals of bitrate adaptation?
    - Low or zero re-buffering
    - High video quality
    - Low video quality variations
    - Low startup latency

- What are the different signals that can serve as an input to a bitrate adaptation algorithm?
    - Network throughput
    - Video Buffer

- Explain buffer-filling rate and buffer-depletion rate calculation.
    - Buffer filling rate = Available bandwidth / chunk bitrate
    - Buffer-depletion rate is 1 second

- What steps does a simple rate-based adaptation algorithm perform?
    - Estimating the future bandwidth
    - Quantization: the continuous throughput mapped to a discrete bitrate

- Explain the problem of bandwidth over-estimation with rate-based adaptation.
    - It requests a chunk that takes too long to download, leading to video stalling

- Explain the problem of bandwidth under-estimation with rate-based adaptation.
    - It cause the network bandwidth to be monopolized by a greedier client.
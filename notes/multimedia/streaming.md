# Streaming

- Two types:
    1. On Demand
    2. Live 
- Buffered- video segments downloaded to be played
- *Rebuffering Event*- the current point of being wathced in the video exceeds the amount of content buffered so the user must wait while the player re-buffers and downloads more of the video
- *Playback Speed*- increasing it from 1x to 2x means if the original video is provided at 60 FPS, the video is now only displayed with every other frame, meaning 30 frames are skipped per second (the 60 FPS remains the same, just more content is compressed in these frames since every other frame is removed meaning it takes 120 frames from the original playback speed to show 1 second at 2x playback speed)

## Pipeline

1. Video encoded to a specific format using a codec 
2. A delivery method such as a CDN is used to get the content to a client
3. Client uses a player to download the manifest file with video metadata and subscribe to the appropriate streams for the desired bitrate 
    - Note: live video regularly updates the manifest 

## Protocols 

- Protocol- set of rules defining how live video and audio travel through a network

1. HTTP Live Streaming (HLS)
    - most widely used in industry
2. MPEG-Dynamic adaptive streaming over HTTP (MPEG-DASH)
    - international standard
3. Real-Time Messaging Protocol (RTMP)

- Using HTTP (e.g. 1 and 2) allows use of content delivery network (CDN) to help speed up delivery 
    - CDNs have caches located closer to the user that can serve the content faster than fetching it from the source

### HLS

- Designed by Apple to deliver videos to their devices wihout having to use Flash 
- Player downloads a `.m3u8` manifest file
    - Contains url where each chunk of video encoded in each of the available bitrates is located
    - Allows player to adaptively select the best bitrate for a specific chunk depending on the available bandwith
- Supported coding formats:
    - audio: AAC and many others
    - video: H.264, H.265

### MPEG-DASH

- agnostic to video/audio coding format

## Adapative Bitrate Streaming (ABS)

- A video is published in streams of multiple bitrates 
- Adpative player switches between the bitrates according to the bandwith available to the player
- Allows a stream to continue playing even during congested/fluctuating bandwith 
    - Lower bitrate is usually better than constant rebuffering for a higher bitrate
- Segmented WebVTT is used for providing subtitles in videos being streamed in chunks

## Key Performance Indicators (KPIs)

- Average Throughput
- Player logs on rebuffering events and dropped bitrate events
- CDN hit/miss ratio
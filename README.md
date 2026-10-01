# whisper-captions

**A scalable live streaming platform with real-time subtitle generation.**

## Highlights

- **Real-time subtitle generation**
- **End-to-end speech recognition latency below 800 ms**
- **Low-latency live playback with LL-HLS**
- **RTSP stream ingestion**
- **Day / night theme switching**
- **Scalable by design**

## Overview

Whisper Captions is a live streaming platform that automatically generates and synchronizes subtitles in real time. It is designed for broadcasts where accessibility, responsiveness, and reliability are important: online lectures, webinars, conferences, educational streams, and other live video scenarios.

The platform receives a live video stream, processes speech in the audio track, generates captions with timestamps, and delivers them to viewers synchronized with playback. The system is built to be modular, scalable, and easy to extend.

https://github.com/nukeboy76/whisper-captions/blob/main/captions-demo.mp4

## Main Features

- Live stream publishing through **RTSP**
- Live playback through **LL-HLS**
- Subtitle delivery through **WebSocket**
- Automatic speech recognition in real time
- Synchronized subtitles with timestamps
- Web client written in JavaScript
- Simple interface for browsing available streams
- Theme switching

## Architecture

The platform uses a modular service-oriented architecture. Each component is responsible for a specific stage of the pipeline, which makes the system easier to maintain and scale.

### Core components

1. **Media server**
   - Receives incoming live streams
   - Serves video to viewers
   - Handles live stream distribution

2. **Stream ingestion layer**
   - Publishes live media into the platform
   - Accepts RTSP input

3. **Subtitle generation service**
   - Processes audio from the live stream
   - Performs speech recognition
   - Produces subtitle fragments with timestamps

4. **Messaging / transport layer**
   - Coordinates data flow between services
   - Supports stream-based communication
   - Helps multiplex subtitle delivery

5. **Web client**
   - Lists available streams
   - Plays live video
   - Displays synchronized captions in the browser

## Technology Stack

- **MediaMTX** — media server
- **FFmpeg** — stream publishing and media handling
- **NATS / JetStream** — message transport and queueing
- **Go** — backend coordination layer
- **Python + PyTorch** — real-time speech recognition and subtitle generation
- **JavaScript** — frontend UI

## API

The platform exposes endpoints for publishing streams, browsing streams, and receiving subtitle updates.

| Endpoint | Method | Purpose |
|---|---:|---|
| `/stream/{id}` | RTSP | Publish an incoming live stream |
| `/streams` | GET | Get the main page with the list of available streams |
| `/stream/{id}` | GET | Open a stream page and receive the live video |
| `/stream/{id}/captions` | WS | Receive live subtitles with timestamps |

## Performance

The prototype demonstrates low-latency speech-to-caption processing, with **end-to-end recognition latency below 800 ms**. This makes the platform suitable for live scenarios where subtitle timeliness is critical.

## Scalability

The system is designed with scalability in mind:

- services are separated by responsibility
- subtitle processing can be expanded independently from media delivery
- transport and queueing layers reduce tight coupling
- the architecture supports future horizontal scaling
- the platform can grow from a prototype into a larger production system

## Project Structure

The repository is organized around the main functional parts of the platform:

- media server configuration
- backend coordination services
- subtitle generation pipeline
- frontend web client
- deployment and containerization files
- stream orchestration logic

## Getting Started

### Prerequisites

- Docker
- Docker Compose

### Run the project

```bash
docker compose up --build
```

After startup, open the web interface in your browser and connect a compatible RTSP source to the ingest endpoint.

### Publishing a stream

Use a compatible RTSP source or FFmpeg to publish a live video stream into the platform. The exact command depends on your environment and stream source configuration.

## Future Improvements

* improving recognition accuracy
* reducing latency even further
* extending stream management tools
* adding archive playback
* improving analytics and monitoring
* supporting richer subtitle styling and controls

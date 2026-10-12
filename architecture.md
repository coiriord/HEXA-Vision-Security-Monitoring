# Architecture and data flow

## 1. Camera acquisition
An authorized IP camera provides an RTSP feed to a Python process. OpenCV reads frames and applies an LBPH face-recognition model. The prototype distinguishes `recognized` and `unknown` outcomes.

## 2. Event production
Recognition results are recorded to a local JSON event log, with a cooldown to reduce repeated entries. A Wazuh ingestion path forwards events for SIEM processing. Exact forwarding configuration is deployment-specific and not included in this public portfolio.

## 3. Detection engineering
Wazuh custom rules map recognition events to alerts. The project uses rule `100801` for unknown faces, `100802` for recognized faces, and `100803` for repeated unknown detections within a defined window. These are lab-specific IDs.

## 4. Read-only retrieval
A dedicated Indexer user with read-only access to alert indices is used by a Python client. The Windows development machine reaches the Indexer over an SSH tunnel to a local loopback port. Indexer credentials are passed to the Flask backend via environment variables and must not be exposed to browser JavaScript.

## 5. Dashboard
Flask serves a live MJPEG camera stream, `/api/events`, and `/api/wazuh-alerts`. The browser polls the JSON endpoints and creates event rows using `textContent`.

## 6. Network boundaries
The initial dashboard was local-only. LAN binding was used temporarily to demonstrate phone access. Authentication and TLS are prerequisites for broader deployment. No router port forwarding is required or recommended.

# projeto-embarcados (FaceGateway)

Face-recognition access control, end to end: from a Raspberry Pi turnstile to a web/mobile panel.

> Coursework · Embedded Systems · 2026-1 · finished (team project)

## Goal
Build a real embedded system, not a simulation. Recognition runs on the Raspberry Pi
(BlazeFace + ArcFace), so the face image never leaves the device: only a 512-float
embedding goes over the network. The edge drives a servo, buzzer and LED, keeps working
offline and syncs its events when the network comes back.

## Stack
- Edge: Raspberry Pi 4, C++17, ONNX Runtime, SQLite, libgpiod (servo, buzzer, RGB LED)
- Backend: Rust (Axum, sqlx), PostgreSQL + pgvector, MQTT (Mosquitto), JWT
- Panel: Angular 20 + Ionic 8 (web + PWA)
- Docker Compose, Caddy, GitHub Actions

## How to run
```bash
cp .env.example .env               # set POSTGRES_PASSWORD, JWT_SECRET, MQTT_*
cd infra && ln -s ../.env .env && bash gen_mqtt_passwords.sh
docker compose up -d --build       # panel at http://localhost/, API at /api/
```
The edge runs on the Pi: see `edge/` (CMake; the ONNX models are not versioned).

## Team
- Ramon Veloso Vieira — edge (C++ vision pipeline) and critical Rust
- Nícolas — backend and database
- Kaique C. — edge integration and UI
- Vinicius D. — frontend and design

## What I took from it
- How computer vision works in practice: detection, alignment, embeddings, matching.
- How to document an engineering process.
- How to build one system out of several languages that talk to each other.
- How to put something in the cloud and make it reachable from the internet.
- How to work as a team with agreed rules.
- How to design access control and a simple system architecture.

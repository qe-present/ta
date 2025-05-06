# Tauri + React + Typescript

This template should help get you started developing with Tauri, React and Typescript in Vite.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)

## Running with Docker

This project provides Dockerfiles and a Docker Compose setup for both the frontend (React + Vite + Typescript) and the Tauri (Rust) backend.

### Requirements

- Docker and Docker Compose installed
- No required environment variables by default (uncomment `env_file` lines in `docker-compose.yaml` if you add any)

### Build and Run

To build and start both services:

```sh
docker compose up --build
```

This will build and run two containers:

- **typescript-root**: Runs the frontend using Node.js v22.14.0 and pnpm v10.4.1. The app is served with Vite preview on port **4173** (exposed as `4173:4173`).
- **rust-src-tauri**: Builds and runs the Tauri (Rust) backend using Rust 1.77. No ports are exposed by default, as Tauri desktop apps typically do not require them.

### Notes

- No persistent volumes or external services are configured by default.
- If you need to add environment variables, create a `.env` file and uncomment the `env_file` lines in the `docker-compose.yaml`.
- If you want to change the frontend port, update the `ports` section in the compose file and the `EXPOSE` directive in the Dockerfile accordingly.

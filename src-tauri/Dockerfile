# syntax=docker/dockerfile:1

# ----------- Build Stage -----------
FROM rust:1.77-slim as builder

# Install build dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends pkg-config libssl-dev build-essential && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy only Cargo.toml and Cargo.lock first for dependency caching
COPY --link Cargo.toml Cargo.lock ./
COPY --link src ./src
COPY --link build.rs ./
COPY --link tauri.conf.json ./
COPY --link capabilities ./capabilities
COPY --link gen ./gen
COPY --link icons ./icons

# Build the application in release mode
RUN cargo build --release

# ----------- Runtime Stage -----------
FROM debian:bookworm-slim AS runtime

# Install runtime dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends libssl3 ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Create a non-root user
RUN useradd -m tauriuser

WORKDIR /app

# Copy the built binary from the builder stage
COPY --from=builder /app/target/release/ta .

# Copy any required runtime assets (if needed)
COPY --link tauri.conf.json ./
COPY --link icons ./icons

USER tauriuser

# Expose port if your app listens on one (Tauri desktop apps usually don't, but for completeness)
# EXPOSE 8080

CMD ["./ta"]

# Use the official rindexer image
FROM ghcr.io/bh2smith/rindexer:sha-c0ea448eaabbff6a331c6538fae3016702e53817

# Install SQLite runtime library for local testing
RUN apt-get update && apt-get install -y libsqlite3-0 && rm -rf /var/lib/apt/lists/*

ENV DATABASE_URL=/app/data/rindexer.db

# Copy the rindexer configuration
WORKDIR /app/project_path
COPY rindexer.yaml .
COPY abis ./abis

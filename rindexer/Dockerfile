# Use the official rindexer image
FROM ghcr.io/joshstevens19/rindexer

ENV DATABASE_URL=postgres://postgres:rindexer@database:5432/postgres

# Copy the rindexer configuration
WORKDIR /app/project_path
COPY rindexer.yaml .
COPY abis ./abis

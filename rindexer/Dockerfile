# Use the official rindexer image
FROM ghcr.io/joshstevens19/rindexer:sha-de24c808b8af5ad8c07c9f8dda4c11965d5dfa04

# Copy the rindexer configuration
WORKDIR /app/project_path
COPY rindexer.yaml .
COPY abis ./abis

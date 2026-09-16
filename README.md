# Treeview contract

OpenAPI 3.1 contract for a small tree editor. Every node owns exactly one typed
datum and zero or more child nodes.

Supported datum variants are `text`, `number`, and `boolean`. Node IDs are
client-generated identifiers containing 1-64 letters, digits, underscores, or
hyphens. A tree may contain at most 5,000 nodes and be at most 32 levels deep.

## API

- `GET /tree` returns the current root and integer revision.
- `PUT /tree` atomically replaces the tree when `expectedRevision` matches.
- A stale write receives `409`; an invalid tree receives `422`.

The canonical machine-readable definition is [openapi.json](openapi.json).
Run `npm test` to verify the contract and example payload.

## Run the complete application

Clone the contract, backend, and frontend repositories into sibling directories
with their default names, then run from this repository:

```sh
docker compose up --build
```

Open `http://localhost:4173`. The API is available at
`http://localhost:8787`, and tree data is retained in the `tree-data` volume.
The contract tests must pass before the backend starts; the frontend waits for
the backend health check. Stop the application with `docker compose down`, or
also remove saved tree data with `docker compose down --volumes`.

## Integration order

Merge this contract before the backend and frontend changes. The consumer PRs
implement version `0.1.0` of this document.

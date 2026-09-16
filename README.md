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

## Integration order

Merge this contract before the backend and frontend changes. The consumer PRs
implement version `0.1.0` of this document.

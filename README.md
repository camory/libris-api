# Libris API contract

`openapi.yaml` is the single source of truth of the Libris HTTP API
(OpenAPI 3.0.3), verified on both sides with [Contracteer](https://contracteer.dev).

## Versions

One release per contract change. The tag is `v` followed by the document's
`info.version`. Releases are immutable: a tag never moves once published.

Consumers pin the tag they implement:

```
https://raw.githubusercontent.com/camory/libris-api/v0.1.0/openapi.yaml
```

- Backend (`camory/libris`): the Contracteer verifier test loads this URL.
- Frontend (`camory/libris`): `contracteer mock <url>` serves it to the tests
  and the dev proxy.

## Releasing

1. Edit `openapi.yaml`, bump `info.version`, add a line to `CHANGELOG.md`.
2. Commit on `main`.
3. `gh release create vX.Y.Z --title vX.Y.Z --notes "<the changelog line>"`.

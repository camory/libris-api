# Changelog

## v0.1.0
- `GET /api/v1/me`: the current reader.

## v0.2.0
- `GET /api/v1/isbn/{isbn}`: what the public sources know about an ISBN; nothing is stored.

## v0.3.0
- `GET /api/v1/isbn/{isbn}` takes the ISBN-13 as thirteen digits; schemas `Isbn`, `IsbnAuthor`, `IsbnSeries`; problems carry no `detail`, validation errors carry `{field, code}`; a problem body marks an answer from Libris itself. Supersedes v0.2.0, which nothing pins.
